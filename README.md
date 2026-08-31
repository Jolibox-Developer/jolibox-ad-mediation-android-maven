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
Keep a single resolved version of Google Mobile Ads in the final Android app.

## Requirements

- Android `minSdk 23`
- `compileSdk 35`
- Java 17
- Kotlin `2.0.21` compatible metadata
- Google Mobile Ads App ID configured in the host application's manifest

Initialize the SDK once during application startup, before loading ads. Your
Jolibox integration configuration is supplied separately and must not be added
to source control.

## Verify downloads

SHA-256 sidecar files are published beside the AAR and POM in the Maven layout.
The release page also contains the same AAR for manual verification.

## License

Use is governed by [LICENSE](LICENSE). This repository intentionally contains
compiled distribution artifacts only; it does not contain the SDK source code.
