---
layout: post
title: " Notes on OpenCV-Android-Samples"
---
**notes**

1.Error:(49) undefined reference to '__atomic_fetch_add_4'

in Android.mk, add this:
LOCAL_LDLIBS +=  -latomic

2.Android Studio使用OpenCV后，运行APP不需要安装OpenCV Manager即可运行，按照如下的方式进行修改 "onResume()":

    @Override
    public void onResume()
    {
        super.onResume();

        //OpenCVLoader.initAsync(OpenCVLoader.OPENCV_VERSION_2_4_3, this, mLoaderCallback); // commnent this sentence

        if (!OpenCVLoader.initDebug()) {
            Log.d(TAG, "Internal OpenCV library not found. Using OpenCV Manager for initialization");
            OpenCVLoader.initAsync(OpenCVLoader.OPENCV_VERSION_2_4_3, this, mLoaderCallback);
        } else {
            Log.d(TAG, "OpenCV library found inside package. Using it!");
            mLoaderCallback.onManagerConnected(LoaderCallbackInterface.SUCCESS);
        }
    }

3. add java-edition OpenCVLibrary module to the related app: 
New->Import Module->path/to/OpenCV-2.4.9-android-sdk/sdk/java/, add the 'openCVLibrary249' modular, select the related moudle depends on 'openCVLibrary249', click F4, select Dependences-> click + ->3 Module dependences -> select ':openCVLibrary249' -> OK.

4. copy Native-edition OpenCVLibrary to the related app(如果不安装OpenCV Manager的话，需要执行此步骤):
cp path/to/OpenCV-2.4.9-android-sdk/sdk/native/libs to app/src/main/jniLibs

5. after importing  projects,  click Update in the Adroid Gradle Plugin Update Recommanded dialog.

**ref**
*Android Studio*
1.[Migrate from ndkCompile](https://developer.android.google.cn/studio/projects/add-native-code.html#ndkCompile)
2.[Link Gradle to your native library](https://developer.android.google.cn/studio/projects/add-native-code.html#create-cmake-script)
*OpenCV*
3.[OpenCV4Android Samples](https://opencv.org/platforms/android/opencv4android-samples.html)
4.[Application Development with Static Initialization](https://docs.opencv.org/2.4/doc/tutorials/introduction/android_binary_package/dev_with_OCV_on_Android.html#application-development-with-static-initialization)
*github*
5.[jlhonora/opencv-android-sample](https://github.com/jlhonora/opencv-android-sample)


