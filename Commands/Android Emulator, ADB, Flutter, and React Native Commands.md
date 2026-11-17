<%*
if (!tp.file.folder(true).startsWith("05 Knowledge/Study/Programming")) {
  await tp.file.move("05 Knowledge/Study/Programming/" + tp.file.title);
}
-%>
---
type: study-note
created: <% tp.file.creation_date("YYYY-MM-DD") %>
topic: programming
language_framework: "Flutter / Python"
tags:
  - study
  - programming
---

# Android Emulator, ADB, Flutter, and React Native Commands

A practical command reference for Android development on Windows, covering Android Virtual Devices (AVDs), ADB, Flutter, and React Native.

## 1. Android Emulator — AVD Commands

```
# List all available Android Virtual Devices
emulator -list-avds

# Launch a specific emulator
emulator -avd Pixel_8

# Launch without boot animation
emulator -avd Pixel_8 -no-boot-anim

# Launch without saving emulator snapshots
emulator -avd Pixel_8 -no-snapshot-save

# Cold boot without loading a saved snapshot
emulator -avd Pixel_8 -no-snapshot-load

# Wipe emulator user data
emulator -avd Pixel_8 -wipe-data

# Launch with a writable system partition
emulator -avd Pixel_8 -writable-system

# Display emulator version
emulator -version
```

Replace `Pixel_8` with an actual AVD name from `emulator -list-avds`.

> **Warning:** `-wipe-data` deletes the emulator's user data and installed apps.

## 2. ADB — Android Debug Bridge

```
# List connected devices and emulators
adb devices

# List devices with detailed state
adb devices -l

# Restart ADB server
adb kill-server
adb start-server

# Check connected device state
adb get-state

# Open a shell on the device
adb shell

# Reboot device
adb reboot

# Install an APK
adb install app-debug.apk

# Reinstall an APK
adb install -r app-debug.apk

# Uninstall an application
adb uninstall com.example.app

# Clear application data
adb shell pm clear com.example.app

# Forward a local port to a device port
adb forward tcp:8081 tcp:8081

# Reverse a device port to a local port
adb reverse tcp:8081 tcp:8081
```

Use `adb reverse tcp:8081 tcp:8081` when a React Native app running on a USB-connected Android device needs to reach Metro on your development machine.

## 3. Emulator Controls and Testing

```
# List connected devices
adb devices

# Set GPS location (longitude, latitude)
adb emu geo fix 77.2090 28.6139

# Simulate battery level
adb shell dumpsys battery set level 50

# Reset simulated battery state
adb shell dumpsys battery reset

# Check Android OS version
adb shell getprop ro.build.version.release

# Check Android SDK/API level
adb shell getprop ro.build.version.sdk

# Check device model
adb shell getprop ro.product.model

# List installed packages
adb shell pm list packages
```

## 4. Android Logs and Debugging

```
# Display all device logs
adb logcat

# Clear existing logs
adb logcat -c

# Clear logs and capture fresh output
adb logcat -c
adb logcat

# Filter React Native logs
adb logcat "*:S" ReactNative:V ReactNativeJS:V

# Filter Android errors
adb logcat "*:E"

# Display logs for a specific package
adb shell pidof com.example.app

# Inspect app process information
adb shell dumpsys activity processes
```

Replace `com.example.app` with your application's Android package ID.

On Windows, the React Native log filter may vary with the Android and React Native versions. If it returns no useful output, use `adb logcat` and inspect the relevant process logs.

## 5. Flutter Commands

```
# Check Flutter environment
flutter doctor -v

# Accept Android SDK licenses
flutter doctor --android-licenses

# List available devices
flutter devices

# List Flutter-managed emulators
flutter emulators

# Launch an emulator
flutter emulators --launch Pixel_8

# Run app on a specific device
flutter run -d emulator-5554

# Fetch dependencies
flutter pub get

# Clean build artifacts
flutter clean

# Build release APK
flutter build apk --release

# Run tests
flutter test
```

## 6. React Native — Project Commands

Run these commands from your React Native project's root directory.

### Project setup and dependencies

```
# Install dependencies with npm
npm install

# Install dependencies with Yarn
yarn install

# Check Node.js version
node --version

# Check npm version
npm --version

# Check React Native CLI environment
npx @react-native-community/cli doctor

# Display the installed React Native version
npm ls react-native
```

Use the package manager and lockfile already established by the project. Do not mix npm and Yarn arbitrarily.

### Start Metro

Metro is the JavaScript bundler used by React Native.

```
# Start Metro
npm start

# Start Metro and clear its cache
npx react-native start --reset-cache
```

Keep Metro running in a dedicated terminal while developing.

### Run the Android application

```
# Build and launch the Android app
npm run android

# Run using the React Native CLI
npx react-native run-android

# Run on a specific emulator/device
npx react-native run-android --deviceId emulator-5554

# Run in release mode
npx react-native run-android --mode release
```

The available options depend on the React Native CLI version and project configuration. Check `npx react-native run-android --help` if an option is unsupported.

### Debugging and development

```
# Start Metro with a clean cache
npx react-native start --reset-cache

# List connected Android devices
adb devices

# Connect Metro to a USB-connected Android device
adb reverse tcp:8081 tcp:8081

# View Android logs
adb logcat

# View React Native logs
adb logcat "*:S" ReactNative:V ReactNativeJS:V
```

## 7. React Native — Android Gradle Commands

Use these commands when investigating Android build failures.

Run Gradle commands from the `android` directory.

**Windows PowerShell:**

```
# Enter the Android project directory
cd android

# Clean Android build artifacts
.\gradlew.bat clean

# Build debug APK
.\gradlew.bat assembleDebug

# Build release APK
.\gradlew.bat assembleRelease

# Display available Gradle tasks
.\gradlew.bat tasks
```

**Install a generated debug APK:**

```
adb install -r android/app/build/outputs/apk/debug/app-debug.apk
```

Run the installation command from the project root.

Note: A release APK may require signing configuration before it can be distributed. Also, cleaning Gradle artifacts does not fix every dependency, SDK, or configuration problem.

## 8. React Native — Useful Package Scripts

Typical `package.json` scripts include:

```
{
  "scripts": {
    "start": "react-native start",
    "android": "react-native run-android",
    "ios": "react-native run-ios",
    "test": "jest",
    "lint": "eslint ."
  }
}
```

These are illustrative scripts, not a replacement for your project's existing configuration.

Run them with:

```
npm start
npm run android
npm test
npm run lint
```

For iOS development, `npm run ios` generally requires macOS and Xcode.

## 9. Windows Android SDK Configuration

If `emulator` or `adb` is not recognized, add the following paths to your Windows `PATH`:

```
%LOCALAPPDATA%\Android\Sdk\emulator
%LOCALAPPDATA%\Android\Sdk\platform-tools
```

Verify the installation in PowerShell:

```
# Locate Android tools
where.exe emulator
where.exe adb

# Check versions
adb version
emulator -version

# Check Java
java -version

# Check Node.js and npm
node --version
npm --version
```

## 10. Quick Workflow — Flutter

Open two terminals.

**Terminal 1 — Start the emulator:**

```
emulator -list-avds
emulator -avd Pixel_8
```

**Terminal 2 — Run Flutter:**

```
adb devices
flutter doctor
flutter devices
flutter run
```

## 11. Quick Workflow — React Native

Open three terminals for a clear development workflow.

**Terminal 1 — Start the emulator:**

```
emulator -list-avds
emulator -avd Pixel_8
```

**Terminal 2 — Start Metro:**

```
npm start
```

**Terminal 3 — Build and run the application:**

```
adb devices
npm run android
```

If the app is already installed and you only need to refresh JavaScript, keep Metro running and reload the application.

## 12. Common Troubleshooting

### Emulator is not detected

```
adb kill-server
adb start-server
adb devices
flutter devices
```

### React Native Metro cache issues

```
npx react-native start --reset-cache
```

Stop any previous Metro process before restarting it on the same port.

### Android build fails

```
cd android
.\gradlew.bat clean
cd ..
npm install
npm run android
```

Cleaning and reinstalling dependencies should not be the first response to every failure. Read the actual Gradle error first, especially when the issue involves Java, Android SDK versions, dependency resolution, or native modules.

### App cannot connect to Metro on a USB device

```
adb devices
adb reverse tcp:8081 tcp:8081
```

Ensure Metro is running on your development machine and that the app is configured to use the correct development server.

## Important Notes

- Use `emulator -list-avds` to discover emulator names.
    
- Use `adb devices` to identify device IDs, commonly `emulator-5554`.
    
- Use `flutter devices` for Flutter and `npm run android` for React Native.
    
- React Native requires Node.js, the appropriate Java Development Kit, Android SDK tools, and project-compatible Gradle configuration.
    
- Keep Metro running during React Native development.
    
- Avoid wiping emulator data unless you intend to reset it.
    
- For production build failures, preserve the full error output and investigate the first meaningful error instead of repeatedly cleaning the project.