# 购物助手 SDK 说明

### 功能介绍

购物助手SDK可以监听淘宝、京东、饿了么、美团、美团外卖等几个常用电商App的商品信息来获取相应的商品购物券，并向用户进行提示，帮助用户购物省钱。用户购物下单获得的返利，可以向开发者（流量主）进行结算。

### 准备工作

1. 将 compileSdkVersion ，buildToolsVersion和 targetSdkVersion对应的版本号改为30以下（因为SDK中用到的 setGravity shouldn't be called on text toasts the values won't be used在30以上版本已经被不能用。详情https://developer.android.com/reference/android/widget/Toast#setGravity(int,%20int,%20int) 请开发者放心集成）

例如：

```
compileSdkVersion 29
buildToolsVersion "29.0.3"
defaultConfig {
    ...
    targetSdkVersion 29
    ...
}
```

2. 在项目下build.gradle中添加

```
allprojects {
   repositories {
        ...
        maven { url "https://raw.githubusercontent.com/Pgyer/helpshop/master" }
   }
}
```

3. 在app/build.gradle中添加

```
dependencies {
     ...
     implementation 'com.pgyer:helpshop:1.0.6'
}
```

4. 在 application 中集成

```java
import com.pgyer.help_shop_library.ShopHelpManager;                                                                 
public class {当前应用的application} extends Application {                                                               
   @Override
   public void onCreate() {
      super.onCreate();
      new ShopHelpManager.InitSdk().setContext(this).build();
   }
}
```

5. 在 AndroidManifest.xml 注意修改 android:name="{当前应用的application}"此处的名字对应上面继承 Application 的类名 ,添加ZK_HM_KEY ，添加是否添加检查更新的开关                 

```
 <application
         android:name=".{当前应用的application}"
         android:allowBackup="true"
         android:networkSecurityConfig="@xml/network"
         android:supportsRtl="true"
         android:theme="@style/AppTheme">
         ...
         <meta-dataandroid:name="APP_KEY" android:value="{从服务商获取的appkey}" />
         ...
</application>
```

 ### 调用介绍
##### 判断当前是否打开辅助模式（无障碍），true表示已经打开，false表示为打开

```java
ShopHelpManager.isOpenAccessiblity(Activity activity)
```

##### 去打开辅助模式

a.带参数回到当前activity

```java
ShopHelpManager.startAccessiblityForResult(Activity activity,int requestCode)
```

b.不带参数回到当前activity

```java
ShopHelpManager.startAccessiblity(Activity activity)
```
