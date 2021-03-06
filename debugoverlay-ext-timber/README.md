Timber Extension Module
===========

**TimberModule** is an extension module for DebugOverlay which shows timber logs for debugging. 

<img src="../art/overlay_with_timber_module_small.png" width="50%" alt="DebugOverlay Screen Capture">

Setup
------

Gradle:

```groovy
dependencies {
  debugCompile 'com.ms-square:debugoverlay:1.1.3'
  releaseCompile 'com.ms-square:debugoverlay-no-op:1.1.3'
  testCompile 'com.ms-square:debugoverlay-no-op:1.1.3'
  
  compile ('com.ms-square:debugoverlay-ext-timber:1.1.3') {
    exclude module: 'debugoverlay'
  }
}
```

or

```groovy
dependencies {
  // this will use a full debugoverlay lib even in the test/release build
  compile 'com.ms-square:debugoverlay-ext-timber:1.1.3'
}
```

Usage
------

### Simple Example

In your `Application` class:

```java
public class ExampleApplication extends Application {

  @Override public void onCreate() {
    super.onCreate();
    new DebugOverlay.Builder(this)
            .modules(new CpuUsageModule(),
                     new MemInfoModule(this),
                     new FpsModule(),
                     new TimberModule(BuildConfig.DEBUG))
            .build()
            .install();
    // Normal app init code...
  }
}
```