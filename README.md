## Add this statement at defaultConfig section of build.gradle

```
configurations.all {
    resolutionStrategy { force 'androidx.core:core-ktx:1.6.0' }
}
```

## Add this statement at dependencies section of build.gradle

```
implementation 'com.airbnb.android:lottie:3.4.1'
```

## Assets

```
1. https://lottiefiles.com/99681-phone-ringing-animation#

2. https://unsplash.com/
```


https://user-images.githubusercontent.com/43849911/159462862-ad82cab9-8791-4f73-ac5a-2b2282aed2fa.mp4


## activity_introductory.xml

```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".IntroductoryActivity">

 <ImageView
     android:id="@+id/img"
     android:layout_width="wrap_content"
     android:layout_height="match_parent"
     android:scaleType="centerCrop"
     android:src="@drawable/bg"
     app:flow_verticalBias="0"
     app:layout_constraintBottom_toBottomOf="parent"
     app:layout_constraintTop_toTopOf="parent"
     app:layout_constraintStart_toStartOf="parent"
     app:layout_constraintStart_toEndOf="parent"
     tools:ignore="ImageContrastCheck"
     android:contentDescription="TODO" />

<com.airbnb.lottie.LottieAnimationView
    android:id="@+id/lottie"
    app:lottie_autoPlay="true"
    android:layout_width="wrap_content"
    android:layout_height="270dp"
    app:flow_verticalBias="0"
    app:lottie_rawRes="@raw/splash"
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintStart_toEndOf="parent"
    app:layout_constraintTop_toTopOf="parent"
    />

</androidx.constraintlayout.widget.ConstraintLayout>
```

## AndroidManifest.xml

```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.animatedsplashscreen">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.AnimatedSplashScreen">
        <activity
            android:name=".IntroductoryActivity"
            android:theme="@style/splash"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        <activity
            android:name=".MainActivity"
            android:exported="false"
            />
    </application>

</manifest>
```

## drawable/splash.xml

```
<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">

    <item>
        <bitmap
            android:src="@drawable/bg"
            android:gravity="fill"
            />
    </item>

</layer-list>
```


## SplashActivity.java

```
package com.example.animatedsplashscreen

import android.animation.Animator
import android.content.Intent
import android.os.Build
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.view.View
import android.view.WindowManager
import com.airbnb.lottie.LottieAnimationView

class IntroductoryActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        if (Build.VERSION.SDK_INT < 16) {
            window.setFlags(
                WindowManager.LayoutParams.FLAG_FULLSCREEN,
                WindowManager.LayoutParams.FLAG_FULLSCREEN)
        }
        window.decorView.systemUiVisibility = View.SYSTEM_UI_FLAG_FULLSCREEN
        actionBar?.hide()

        setContentView(R.layout.activity_introductory)
        val lottieAnimationView:LottieAnimationView = findViewById(R.id.lottie)
        lottieAnimationView.playAnimation()
        val intent = Intent(this,MainActivity::class.java)
        lottieAnimationView.addAnimatorListener(object : Animator.AnimatorListener{
            override fun onAnimationRepeat(animation: Animator?) {
            }
            override fun onAnimationEnd(animation: Animator?) {
                startActivity(intent)
                finish()
            }
            override fun onAnimationCancel(animation: Animator?) {
            }
            override fun onAnimationStart(animation: Animator?) {
            }

        })
    }
}
```

## themes.xml

```
<resources xmlns:tools="http://schemas.android.com/tools">
    <!-- Base application theme. -->
    <style name="Theme.AnimatedSplashScreen" parent="Theme.MaterialComponents.DayNight.NoActionBar">
        <!-- Primary brand color. -->
        <item name="colorPrimary">@color/purple_500</item>
        <item name="colorPrimaryVariant">@color/purple_700</item>
        <item name="colorOnPrimary">@color/white</item>
        <!-- Secondary brand color. -->
        <item name="colorSecondary">@color/teal_200</item>
        <item name="colorSecondaryVariant">@color/teal_700</item>
        <item name="colorOnSecondary">@color/black</item>
        <!-- Status bar color. -->
        <item name="android:statusBarColor" tools:targetApi="l">?attr/colorPrimaryVariant</item>
        <!-- Customize your theme here. -->
    </style>

    <style name="splash" parent="@style/Theme.AppCompat.Light.NoActionBar">
        <item name="android:windowBackground">
            @drawable/splash
        </item>
        <item name="android:windowNoTitle">true</item>
        <item name="android:windowActionBar">false</item>
        <item name="android:windowFullscreen">true</item>
        <item name="android:windowContentOverlay">@null</item>
<!--        <item name="android:statusBarColor" tools:targetApi="lollipop">@color/blue</item>-->
<!--        <item name="android:windowLightStatusBar" tools:targetApi="m">true</item>-->
    </style>

</resources>
```

## MainActivity.java


```
package com.example.animatedsplashscreen

import android.os.Build
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.view.View
import android.view.WindowManager

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        if (Build.VERSION.SDK_INT < 16) {
            window.setFlags(
                WindowManager.LayoutParams.FLAG_FULLSCREEN,
                WindowManager.LayoutParams.FLAG_FULLSCREEN)
        }
        window.decorView.systemUiVisibility = View.SYSTEM_UI_FLAG_FULLSCREEN
        actionBar?.hide()
        setContentView(R.layout.activity_main)
    }
}
```

