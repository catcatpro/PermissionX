# PermissionX
PermissionX是一个用于简化Android运行时权限用法的开源库。

## 第一步
```shell
git clone https://github.com/catcatpro/PermissionX.git
```
## 第二步
将Library目录复制到项目目录。

## 第三步
在应用模块build.grade的dependencies引入PermissionX模块
```groovy
dependencies {
    implementation project(":Library")
}
```
## 第四步
然后可以使用以下的方式来申请运行时权限了
```kotlin
  PermissionX.request(this, Manifest.permission.CALL_PHONE){ allGrandted, deniedList ->
                if(allGrandted){
                    try {
                        val intent = Intent(Intent.ACTION_CALL)
                        intent.data = Uri.parse("tel:10010")
                        startActivity(intent)
                    }catch (e: SecurityException){
                        e.printStackTrace()
                    }
                }else{
                    Toast.makeText(this, "You denied $deniedList", Toast.LENGTH_SHORT).show()
                }
            }
```
## 最后需要在AndroidManifest.xml文件中添加相应的权限。