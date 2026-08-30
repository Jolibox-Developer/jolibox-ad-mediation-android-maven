# Jolibox Ad Mediation Android

Jolibox Ad Mediation Android SDK 的仅二进制 Maven 分发仓库。

> English documentation: [README.md](README.md)

## 接入

使用发布 Tag 作为 Maven 仓库地址：

```gradle
repositories {
  google()
  mavenCentral()
  maven { url = uri("https://raw.githubusercontent.com/Jolibox-Developer/jolibox-ad-mediation-android-maven/0.6.0/") }
}

dependencies {
  implementation("com.jolibox.android:jolibox-ad-mediation:0.6.0")
}
```

SDK 会传递引入 `com.google.android.gms:play-services-ads:24.0.0`。最终 Android
应用中应只解析出一个 Google Mobile Ads 版本。

## 环境要求

- Android `minSdk 23`
- `compileSdk 35`
- Java 17
- 在宿主应用 Manifest 中配置 Google Mobile Ads App ID

请在应用启动阶段完成一次 SDK 初始化，再加载广告。Jolibox 的接入配置会单独
提供，不能提交到源码仓库。

## 校验下载

Maven 目录内的 AAR 和 POM 均提供 SHA-256 校验文件；Release 页面也提供同一份
AAR 供手动校验。

## 许可证

使用受 [LICENSE](LICENSE) 约束。本仓库仅包含已编译的发布制品，不包含 SDK
源码。
