
# Android Ads SDK
  
  
## Setup Gradle  
Modified your root (project level)  ```settings.gradle``` as belowed code:  
```groovy  
pluginManagement {  
  repositories {  
  gradlePluginPortal()  
  google()  
  mavenCentral()  
  jcenter()  
  maven { url 'https://jitpack.io' }  
  maven { url = uri("https://oss.sonatype.org/content/repositories/snapshots/") }  
  maven { url = uri("https://maven.pkg.jetbrains.space/kotlin/p/kotlin/bootstrap") }  
  maven { url 'https://maven.google.com/' }  
  maven { url 'https://jitpack.io' }  
  maven { url 'https://swisscodemonkeys.github.io/appbrain-sdk/maven' }  
  maven { url 'https://plugins.gradle.org/m2/' }  
  maven { url 'https://dl.bintray.com/kotlin/kotlin-eap' }  
  maven { url 'https://maven.wortise.com/artifactory/public' }  
  maven { url "https://android-sdk.is.com/" }  
  maven { url 'https://artifact.bytedance.com/repository/pangle' }  
  maven { url "https://aa-sdk.s3-eu-west-1.amazonaws.com/android_repo" }  
  maven { url "https://sdk.tapjoy.com/" }  
  maven { url 'https://artifactory.yahooinc.com/artifactory/maven/' }  
  maven { url "https://imobile-maio.github.io/maven" }  
  maven { url "https://dl-maven-android.mintegral.com/repository/mbridge_android_sdk_oversea" }  
  maven { url "https://s3.amazonaws.com/smaato-sdk-releases/" }  
  }  
}  

dependencyResolutionManagement {  
  repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)  
  repositories {  
  google()  
  mavenCentral()  
  gradlePluginPortal()  
  jcenter()  
  maven { url 'https://jitpack.io' }  
  maven { url = uri("https://oss.sonatype.org/content/repositories/snapshots/") }  
  maven { url = uri("https://maven.pkg.jetbrains.space/kotlin/p/kotlin/bootstrap") }  
  maven { url 'https://maven.google.com/' }  
  maven { url 'https://jitpack.io' }  
  maven { url 'https://swisscodemonkeys.github.io/appbrain-sdk/maven' }  
  maven { url 'https://plugins.gradle.org/m2/' }  
  maven { url 'https://dl.bintray.com/kotlin/kotlin-eap' }  
  maven { url 'https://maven.wortise.com/artifactory/public' }  
  maven { url "https://android-sdk.is.com/" }  
  maven { url 'https://artifact.bytedance.com/repository/pangle' }  
  maven { url "https://aa-sdk.s3-eu-west-1.amazonaws.com/android_repo" }  
  maven { url "https://sdk.tapjoy.com/" }  
  maven { url 'https://artifactory.yahooinc.com/artifactory/maven/' }  
  maven { url "https://imobile-maio.github.io/maven" }  
  maven { url "https://dl-maven-android.mintegral.com/repository/mbridge_android_sdk_oversea" }  
  maven { url "https://s3.amazonaws.com/smaato-sdk-releases/" }  
  }  
}  

...

include ':utils'
```  


Must have to add bellowed code in ```AndroidManifest.xml```  before the ```</application>``` :
```xml
<meta-data  
  android:name="com.google.android.gms.ads.APPLICATION_ID"  
  android:value="ca-app-pub-5324507709723505~9525441546" /> 
  ```
  
  
Now add the dependency to your app ```build.gradle```:  
```groovy  
dependencies {  
	 implementation project(path: ':utils')
	 // Also implement admob ads sdk..
 }  
```  
  
## Sertup SplashActivity.kt  
splash screen name should be "SplashActivity.kt" 
  
```SplashActivity.kt```  
```kotlin   
class SplashActivity : CustomActivity(BuildConfig.VERSION_CODE),  
  CustomActivity.OnFetchDataListener {

	override fun onCreate(savedInstanceState: Bundle?) {  
		super.onCreate(savedInstanceState)
		setContentView(R.layout.activity_splash)
		
		super.onFetchDataListener = this
		MobileAds.initialize(this) { }
	}
	
	override fun onDataLoadSuccess() {  
		val intent = Intent(this@SplashActivity, MainActivity::class.java)
		startActivity(i)  
		finish()
	}
}
```

in other activities..


``` MainActivity.kt```

```kotlin
class MainActivity : CustomActivity() {

	override fun onCreate(savedInstanceState: Bundle?) {  
		super.onCreate(savedInstanceState)
		setContentView(R.layout.activity_main)

		//  For banner ads
		GetData.adsManager?.showBanner(findViewById(R.id.adView))

		// For native ads
		GetData.adsManager?.showNativeAds(findViewById(R.id.nativeAdView))

		// interstital ads (Repalce this@MainActivity with your current activity and NextActivity with you preffered activity)
		val i = Intent(this@MainActivity, NextActivity::class.java)
		startAdsActivity(i)
	}	
}

```







