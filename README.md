## Add this statement at defaultConfig build.gradle

```
configurations.all {
    resolutionStrategy { force 'androidx.core:core-ktx:1.6.0' }
}
```