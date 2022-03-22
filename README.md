## Add this statement at defaultConfig section of build.gradle

```
configurations.all {
    resolutionStrategy { force 'androidx.core:core-ktx:1.6.0' }
}
```

## Add this statement at dependencies section of build.gradle

```
implementation 'com.airbnb.android:lottie:3.4.1'
``