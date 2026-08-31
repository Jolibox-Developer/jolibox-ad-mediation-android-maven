# Changelog

> 中文说明：[CHANGELOG_CN.md](CHANGELOG_CN.md)

## 0.6.2

- Rebuilds the Android SDK with Kotlin `2.0.21`, Android Gradle Plugin `8.6.1`, and Gradle `8.7` while retaining `compileSdk 35` and Java 17.
- Preserves Java default-method compatibility for existing Banner and fullscreen callbacks.
- Retains the transitive Google Mobile Ads dependency at `24.0.0`.
- Keeps the cross-platform mediation runtime protocol at `1.0.0`; this release changes build compatibility, not the remote configuration contract.

## 0.6.1

- Republishes the verified `0.6.0` binary at a new immutable coordinate with corrected license metadata.

## 0.6.0

- Rebuilt and republished the Android binary under the unified `0.6.0` release.
- Retains the transitive Google Mobile Ads dependency at `24.0.0`.

## 0.5.0

- First public binary release of Jolibox Ad Mediation for Android.
- Supports AdMob Banner, Interstitial, and Rewarded ad mediation APIs.
- Includes a transitive dependency on Google Mobile Ads `24.0.0`.
