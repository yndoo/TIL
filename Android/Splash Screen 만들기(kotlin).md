# Splash Screen 만들기
![](https://velog.velcdn.com/images/kuronuma_daisy/post/93a40a4d-1783-4fc6-ad8f-26c87a88cd3f/image.png)  
스플래시 화면은 앱 실행시 빈 화면 대신 브랜드 로고 등을 크게 띄우는 화면이다. 사용자가 앱을 실행시켰을 때 빈 화면을 보면 로딩이 느리다고 인식하여 부정적 경험을 하게 되기 때문에 이를 방지하는 역할을 한다.

## SplashActivity.kt
```kotlin
package com.example.myfloapp

import android.content.Intent
import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import android.os.Handler

class SplashActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_splash)
        // 타이머가 끝나면 내부 실행
        Handler().postDelayed(Runnable {
            // 앱의 MainActivity로 넘어가기
            val i = Intent(this@SplashActivity,MainActivity::class.java)
            startActivity(i)
            // 현재 액티비티 닫기
            finish()
        }, 3000) // 3초
    }
}
```
## activity_splash.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".SplashActivity"
    android:orientation="vertical">
    <ImageView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:src="@drawable/splash_img"/>
</LinearLayout>
```
## AndroidManifest.xml
* `intent-filter`태그로 MainActivity가 아닌 SplashActivity를 시작화면으로 바꿈
* intent-filter를 쓸 때는 `android:exported`를 "false"로 설정하면 안 됨
* `android:exported`는 다른 애플리케이션의 구성요소로 Activity를 시작할 수 있는지 설정
```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.MyFloApp"
        tools:targetApi="31">

        <activity
            android:name=".SplashActivity"
            android:exported="true"
            android:theme="@style/Theme.Design.NoActionBar" >
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>


        <activity android:name=".MainActivity" />
    </application>

</manifest>
```

### 참고 문서
https://brunch.co.kr/@kangsigner/1  
https://stickode.tistory.com/665  
https://m.blog.naver.com/websearch/221668354461
