# DiPlay P170 Nissan Bluetooth build

This source tree is modified for Nissan P170/HSAE BluetoothService.

Changes:
- Reads paired phones from `com.hsae.bluetoothservice` / `IBluetoothManager.getPairedDevices()` when Android `bondedDevices` is empty.
- Calls the OEM `connect(name, mac)`, `connectA2dp(mac)`, and `connectHfp(mac)` before DiPlay opens its iAP2 RFCOMM socket.
- Keeps the normal Android Bluetooth path for non-P170 devices.
- Mirrors the HSAE `BluetoothDevice` Parcelable used by the vendor service.

Important: this environment cannot download Gradle 9.5, so an APK was not compiled here. Build the `mobile` release APK with the repository's `./gradlew` on a machine with Android SDK/Gradle network access.

Expected build command:

    ./gradlew :mobile:assembleRelease

The release signing configuration in `mobile/build.gradle.kts` expects the normal environment variables for the project's signing key. For a local test APK, use:

    ./gradlew :mobile:assembleDebug

Install the generated APK, pair the iPhone with the Nissan OEM Bluetooth first, then open DiPlay -> Wireless CarPlay -> choose iPhone.
