# VerusMediaSDK
##### Requirements:

* Java JDK 8
* Android device version: Lolipop or higher
* Android SDK 21
* Gradle 3.2.1 or higher

1. [ Installation ](#ins)
2. [ How to get Video Ads. ](#video)
2. [ How to get Native Ads. ](#native)
2. [ How to get Banner Ads. ](#banner)

<a name="ins"></a>
## Installation
•	Download aar lib from latest release. 
•	In Android studio: File -> New -> New Module and choose Import .jar/.aar Package, press next
•	File name: path to aar
•	File -> Project Structure -> {your_module_tab} -> dependencies and add imported module as dependency.
•	Change your minSdkVersion to >=21 in the Module:app Gradle.
•	Add the jitpack repository to the Project Gradle.
```
allprojects {
    repositories {
        google()
        jcenter()
        maven { url 'https://jitpack.io' }
    }
}
```
•	Add the following code in the Module:app Gradle.
```
Android{
    ...
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
    ...
}


dependencies{
    ...
     final SUPPORT_LIBRARY_VERSION = '28.0.0'
    implementation "com.android.support:appcompat-v7:$SUPPORT_LIBRARY_VERSION"
    implementation "com.android.support:support-v13:$SUPPORT_LIBRARY_VERSION"
    implementation "com.android.support:design:$SUPPORT_LIBRARY_VERSION"
    implementation 'com.android.support.constraint:constraint-layout:1.1.3'
    implementation 'com.squareup.picasso:picasso:2.71828'
    implementation 'com.google.android.gms:play-services-ads-identifier:16.0.0'
    implementation 'com.android.volley:volley:1.1.1'
    implementation 'com.github.vic797:prowebview:2.2.1'
    ...
}

```
<a name="video"></a>
### How to get Video Ads
To get a video ad you need initialize the `Video` class with your `Context`, call the `loadVideoAd()` function and send your placementId, your `VideoOnLoadListener` and a verified flag, the last will determine wether we show a VeriView™ Video Ad or a regular Video Ad.

The `VideoOnLoadListener` has two methods that will be called with a `VideoStatus` when the Ad finishes.
The `VideoStatus` enumeration types are:

`COMPLETED`, `COMPLETED_VERIFIED`, `AD_ERROR_RS` and `NO_INTERNET`

Here is an example on how to get a Video Ad:

```java
    Video video = new Video(Context);
    video.loadVideoAd("YourPlacementId", new VideoOnLoadListener() {
            @Override
            public void onSuccess(VideoState videoState) {
                  //Do something.
            }

            @Override
            public void onFailure(VideoState videoState) {
                  //Do something when the it fails.   
            }
     },flag);
```
You can create a new `VideoOnLoadListener` inside the method call or use your `Activity` class as the listener.

<a name="native"></a>
### How to get Native Ads
To get a native ad you need to initialize the `Native` class with your `Context`. After, you need set your views using the following methods:

```java
      setTitleView(TextView titleView);
      setDescriptionView(TextViewdescView);
      setImageView(ImageView imageView);
      setCtaView(Button callToActionView);
```


After you instance your Native Ad, you need to call `loadNativeAd()` function with your `NativeOnLoadListener` that has two methods that will be called. 

Here is an example on how to get a Native Ad:

```java
       Native nat = new Native(Context);
       nat.setTitleView(titleView);
       nat.setDescriptionView(descView);
       nat.setImageView(imageView);
       nat.setCtaView(cta);
       nat.loadNativeAd(new NativeOnLoadListener() {
            @Override
            public void onSuccess() {
                  //Do something.
            }

            @Override
            public void onFailure() {
                //Do something when the it fails.
            }
       },"YourPlacementId");
```
You can create a new `NativeOnLoadListener` inside the method call or use your `Activity` class as the listener.
<a name="banner"></a>
### How to get Banner Ads
For getting Banner Ads you need to create a Banner in your view.xml
```xml
        <com.verusmedia.sdk.Banner.Banner
            android:id="@+id/banner"
            android:layout_width="YourWidth"
            android:layout_height="YourHeight"/>           
```

You need to call your Banner view in your class and call the `loadNativeAd()` with your widht, height, placementId and your `BannerOnLoadListener` that has two methods that will be called. 

Here is an example on how to get a Banner Ad:
```java
        Banner banner = (Banner) findViewById(R.id.banner);
        banner.loadBannerAd(YourWidth, YourHeight, "YourPlacementId", new BannerOnLoadListener() {
            @Override
            public void onSuccess() {
                //Do something.
            }

            @Override
            public void onFailure() {
                //Do something when the it fails.
            }
        });
```
        
