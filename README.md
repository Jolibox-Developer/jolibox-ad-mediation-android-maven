# Jolibox Ad Mediation for Android

Binary-only Maven distribution of the Jolibox Ad Mediation Android SDK.

> 中文说明：[README_CN.md](README_CN.md)

## Install

Use the release tag as the Maven repository URL:

```gradle
repositories {
  google()
  mavenCentral()
  maven { url = uri("https://raw.githubusercontent.com/Jolibox-Developer/jolibox-ad-mediation-android-maven/0.6.2/") }
}

dependencies {
  implementation("com.jolibox.android:jolibox-ad-mediation:0.6.2")
}
```

The SDK brings `com.google.android.gms:play-services-ads:24.0.0` transitively.
Keep a single resolved version of Google Mobile Ads in the final Android app;
this release requires that resolved version to remain `24.0.0`.

## Requirements

- Android `minSdk 23`
- Java 17
- Kotlin `2.0.21`
- Google Mobile Ads App ID configured in the host application's manifest

The artifact was built and verified with Android Gradle Plugin `8.6.1`, Gradle
`8.7`, `compileSdk 35`, and `targetSdk 35`. These are verification values rather
than versions every host must copy. A host may use another compatible AGP,
Gradle, compile SDK, or target SDK while keeping Kotlin `2.0.21` and Google
Mobile Ads `24.0.0`.

Set the host's existing `org.jetbrains.kotlin.android` plugin declaration to
exactly `2.0.21` (or set a legacy `ext.kotlin_version` to `2.0.21`). Update the
existing declaration rather than adding a second Kotlin plugin declaration.

Add the host's AdMob App ID inside the `<application>` element of its manifest.
An App ID contains `~`; do not put an ad unit ID containing `/` here.

```xml
<meta-data
    android:name="com.google.android.gms.ads.APPLICATION_ID"
    android:value="YOUR_ANDROID_ADMOB_APP_ID" />
```

Initialize the SDK once during application startup, before loading ads. The
integration value below is supplied separately and must not be added to source
control.

```kotlin
import android.app.Application
import com.jolibox.admediation.JoliboxAds
import com.jolibox.admediation.api.InitializationCallback
import com.jolibox.admediation.api.JoliboxAdError
import com.jolibox.admediation.api.MediationEnvironment

class HostApplication : Application() {
    override fun onCreate() {
        super.onCreate()
        JoliboxAds.initialize(
            this,
            "YOUR_JOLI_SOURCE",
            MediationEnvironment.STAGING,
            object : InitializationCallback {
                override fun onInitialized() {
                    // Enable ad loading only after this callback.
                }

                override fun onInitializationFailed(error: JoliboxAdError) {
                    // Keep ad loading disabled and report the failure.
                }
            },
        )
    }
}
```

Declare the application class in the same manifest; otherwise this startup code
will not run:

```xml
<application
    android:name=".HostApplication"
    ...>
```

## Verify downloads

SHA-256 sidecar files are published beside the AAR and POM in the Maven layout.
The release page also contains the same AAR for manual verification.

## License

Use is governed by [LICENSE](LICENSE). This repository intentionally contains
compiled distribution artifacts only; it does not contain the SDK source code.
