### 1.取消原生桌面：

~~~
build/make/target/product/handheld_system_ext.mk
Launcher3QuickStep
~~~

![image-20231209155544647](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202312111508562.png)

```
3588-android12/device/rockchip/common/device.mk
PRODUCT_PACKAGES += Launcher3QuickStepGo
Launcher3QuickStep
```

![image-20231209154408563](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202312111508465.png)

~~~
device/generic/common/mgsi/mgsi_product.mk
~~~

![image-20231209154601429](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202312111508434.png)

### 2.内置app并设置成launcher

在安卓源码下的packages\apps下创建文件夹（名称必须和APK同名），并把apk放进创建的文件夹里面去。

![img](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202312111508416.jpeg) 

在创建的文件夹下创建一个Android.mk文件，内容:

~~~mk
LOCAL_PATH := $(call my-dir)
include $(CLEAR_VARS)
LOCAL_MODULE := hmkq3568s_code_37_1.0.17_11_28_20_38_47
LOCAL_MODULE_TAGS := optional
LOCAL_SRC_FILES := $(LOCAL_MODULE).apk
LOCAL_MODULE_CLASS := APPS
LOCAL_MODULE_SUFFIX := $(COMMON_ANDROID_PACKAGE_SUFFIX)
LOCAL_PRIVILEGED_MODULE :=true
LOCAL_OVERRIDES_PACKAGES := Home Launcher2 Launcher3 Launcher3QuickStep   
LOCAL_CERTIFICATE := platform
include $(BUILD_PREBUILT)
~~~

![image-20231209155950136](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202312111508506.png)



### 3.将内置的app设置成launcher

打开安卓源码下的这个文件

```
3588-android12/build/make/target/product/handheld_product.mk
```

将自己的app加到PRODUCT_PACKAGES列表

![image-20231209160141718](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202312111508484.png)

### 4.删掉开机动画

测试发现，经过上面修改之后会在开机之后仍旧先加载到桌面，随后才进入相应的app，又经过测试发现这是开机动画的影响，所以仍旧需要下面的操作关掉启动中的动画。

**步骤一：**

~~~
vim frameworks/base/services/core/java/com/android/server/wm/ActivityRecord.java
~~~

在onWindowsDrawn方法的最后添加下面的内容

~~~java
//解锁后退出开机动画
// phoebe add for exit bootanim start
if (isHomeIntent(intent) && shortComponentName != null && !shortComponentName.contains("FallbackHome")) {
    SystemProperties.set("service.bootanim.exit", "1");
    android.util.Log.e("ActivityRecord", "real home....." + shortComponentName);

    try {
        IBinder surfaceFlinger = ServiceManager.getService("SurfaceFlinger");
        if (surfaceFlinger != null) {
            Slog.i(TAG_WM, "******* TELLING SURFACE FLINGER WE ARE BOOTED!");
            Parcel data = Parcel.obtain();
            data.writeInterfaceToken("android.ui.ISurfaceComposer");
            surfaceFlinger.transact(IBinder.FIRST_CALL_TRANSACTION, // BOOT_FINISHED
                    data, null, 0);
            data.recycle();
        }
    } catch (RemoteException ex) {
        Slog.e(TAG, "Boot completed: SurfaceFlinger is dead!");
    }
}
// phoebe add for exit bootanim end
~~~

**步骤2**

~~~
vim frameworks/base/services/core/java/com/android/server/wm/WindowManagerService.java
~~~

注释以下内容：
![image-20231211144308708](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202312111508440.png)

**步骤3：**

~~~
vim packages/apps/Settings/src/com/android/settings/FallbackHome.java
~~~

注释掉下面的内容：	

![image-20231211144520230](https://chai-1301855619.cos.ap-beijing.myqcloud.com/202312111508115.png)

随后编译重新烧写即可：

~~~shell
source javaenv.sh 
java -version 
lunch rk3588_s-userdebug
./build.sh -AUCKu
~~~

