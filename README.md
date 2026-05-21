# Money Ledger - Android APK

A Money Ledger application packaged as an Android APK using Capacitor. This project converts the HTML-based Money Ledger web app into a native Android application.

## 📱 Project Structure

```
money-ledger-capacitor/
├── www/                      # Web assets (HTML, CSS, JS)
│   └── index.html           # Main application file
├── android/                 # Android native project
│   ├── app/
│   ├── gradle/
│   └── gradlew
├── capacitor.config.json    # Capacitor configuration
├── package.json
└── .github/workflows/       # GitHub Actions workflows
    └── build-apk.yml       # Automated APK build workflow
```

## 🚀 Quick Start

### Prerequisites

- Node.js 16+ and npm
- Java Development Kit (JDK) 17+
- Android SDK (API level 33+)
- Gradle

### Local Development

1. **Install dependencies:**
   ```bash
   npm install
   ```

2. **Build for Android:**
   ```bash
   npx cap build android
   ```

3. **Open in Android Studio:**
   ```bash
   npx cap open android
   ```

4. **Build APK:**
   ```bash
   cd android
   ./gradlew assembleRelease
   ```

The APK will be generated at: `android/app/build/outputs/apk/release/app-release-unsigned.apk`

## 🔄 Automated Build with GitHub Actions

This project includes a GitHub Actions workflow that automatically builds the APK on every push to the main/master/develop branches.

### Workflow Features

- ✅ Automatic APK generation on push
- ✅ Artifacts stored for 30 days
- ✅ Release creation on version tags
- ✅ Java 17 and Android SDK 33 setup

### View Build Results

1. Go to your GitHub repository
2. Click on the **Actions** tab
3. Select the **Build APK** workflow
4. Click on a completed run to see the APK artifact

### Download APK

After a successful build, download the APK from:
- **Artifacts section** in GitHub Actions (for development builds)
- **Releases section** (for tagged releases)

## 📝 Configuration

### App Details

Edit `capacitor.config.json` to customize:

```json
{
  "appName": "Money Ledger",
  "appId": "com.moneyledger.app",
  "webDir": "www",
  "android": {
    "minVersion": 22,
    "targetSdkVersion": 33
  }
}
```

### Android Manifest

Modify `android/app/src/main/AndroidManifest.xml` to add permissions or customize app behavior.

## 🔐 Signing the APK

For production releases, you need to sign the APK:

1. **Create a keystore:**
   ```bash
   keytool -genkey -v -keystore money-ledger.keystore -keyalg RSA -keysize 2048 -validity 10000 -alias money-ledger
   ```

2. **Update `android/app/build.gradle`:**
   ```gradle
   signingConfigs {
       release {
           storeFile file('money-ledger.keystore')
           storePassword 'your_store_password'
           keyAlias 'money-ledger'
           keyPassword 'your_key_password'
       }
   }
   
   buildTypes {
       release {
           signingConfig signingConfigs.release
       }
   }
   ```

3. **Build signed APK:**
   ```bash
   cd android
   ./gradlew assembleRelease
   ```

## 📦 Building for Release

### Using GitHub Actions (Recommended)

1. Create a version tag:
   ```bash
   git tag v1.0.0
   git push origin v1.0.0
   ```

2. The workflow will automatically build and create a release with the APK

### Manual Build

```bash
cd android
./gradlew assembleRelease
```

## 🐛 Troubleshooting

### Build Fails with Gradle Error

```bash
cd android
./gradlew clean
./gradlew assembleRelease
```

### APK Not Generated

- Check that `www/index.html` exists
- Verify Java and Android SDK are properly installed
- Run `npx cap sync android` to update web assets

### GitHub Actions Build Fails

1. Check the workflow logs in the **Actions** tab
2. Ensure your repository has the correct permissions
3. Verify that all dependencies are properly specified in `package.json`

## 📱 Installation on Device

1. Enable **Developer Mode** on your Android device
2. Enable **USB Debugging**
3. Connect via USB
4. Install APK:
   ```bash
   adb install android/app/build/outputs/apk/release/app-release-unsigned.apk
   ```

Or download from GitHub Actions and install manually.

## 🔗 Resources

- [Capacitor Documentation](https://capacitorjs.com/docs)
- [Android Development Guide](https://developer.android.com/docs)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)

## 📄 License

ISC

## 🤝 Support

For issues or questions, please create an issue in the GitHub repository.
