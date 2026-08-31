# Jolibox Ad Mediation Android

Jolibox Ad Mediation Android SDK 的仅二进制 Maven 分发仓库。

> English documentation: [README.md](README.md)

## 接入

使用发布 Tag 作为 Maven 仓库地址：

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

SDK 会传递引入 `com.google.android.gms:play-services-ads:24.0.0`。最终 Android
应用中应只解析出一个 Google Mobile Ads 版本，且本版本要求最终解析结果保持
`24.0.0`。

## 环境要求

- Android `minSdk 23`
- Java 17
- Kotlin `2.0.21`
- 在宿主应用 Manifest 中配置 Google Mobile Ads App ID

该制品使用 Android Gradle Plugin `8.6.1`、Gradle `8.7`、`compileSdk 35` 与
`targetSdk 35` 完成构建验收。这些是验收值，不要求所有宿主照搬；宿主可以使用其他兼容的
AGP、Gradle、compile SDK 或 target SDK，但必须保持 Kotlin `2.0.21` 与 Google
Mobile Ads `24.0.0`。

将宿主已有的 `org.jetbrains.kotlin.android` 插件版本精确设置为 `2.0.21`（旧工程则将
`ext.kotlin_version` 设置为 `2.0.21`）。只更新已有声明，不要重复添加第二份 Kotlin
插件声明。

在宿主 Manifest 的 `<application>` 元素内配置 AdMob App ID。App ID 包含 `~`，不要
误填包含 `/` 的广告位 ID。

```xml
<meta-data
    android:name="com.google.android.gms.ads.APPLICATION_ID"
    android:value="YOUR_ANDROID_ADMOB_APP_ID" />
```

请在应用启动阶段完成一次 SDK 初始化，再加载广告。下方接入参数会单独提供，不能提交到
源码仓库。

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
                    // 只在该回调后启用广告加载。
                }

                override fun onInitializationFailed(error: JoliboxAdError) {
                    // 保持广告加载禁用，并上报失败。
                }
            },
        )
    }
}
```

还必须在同一份 Manifest 中声明该 Application 类，否则上述启动代码不会执行：

```xml
<application
    android:name=".HostApplication"
    ...>
```

## 校验下载

Maven 目录内的 AAR 和 POM 均提供 SHA-256 校验文件；Release 页面也提供同一份
AAR 供手动校验。

## 许可证

使用受 [LICENSE](LICENSE) 约束。本仓库仅包含已编译的发布制品，不包含 SDK
源码。
