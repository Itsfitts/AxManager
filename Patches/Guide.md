# Integration Guide for UID 1000 Support

This guide outlines the changes required to enable UID 1000 (system) support in Shizuku-based projects, as implemented in the Pascua28 variant.

## 1. Native Starter (starter.cpp)
The native starter must be modified to:
- Accept UID 1000 in its initial check.
- Daemonize properly using a double fork.
- Optionally start a reverse shell server for remote debugging.

**Key File:** `manager/src/main/jni/starter.cpp`

## 2. System Exploit (StarterActivity.kt)
The exploit targets `com.sdet.fotaagent` on Samsung devices. It involves:
- Starting the `com.sdet.fotaagent.Main` activity.
- Sending a broadcast with action `com.sdet.fotaagent.intent.CP_FILE`.
- Injecting the command to run the Shizuku native library via the `CP_LOC` extra.

**Key File:** `manager/src/main/java/moe/shizuku/manager/starter/StarterActivity.kt`

## 3. Permission Bypass
Since UID 1000 is a system user, it should be granted permission by default in the manager.
- Update `HomeViewModel.kt` and `RequestPermissionActivity.kt` to check if `Shizuku.getUid() == 1000`.

## 4. UI Changes
- Add a new card in the Home screen to trigger the system activation.
- Check for the existence of the `com.sdet.fotaagent` package before showing the option.

## 5. Reverse Shell Usage
The modified starter opens two ports:
- **Port 1337**: Provides a shell with UID 1000 (System).
- **Port 1338**: Provides a shell with UID 2000 (ADB).

To connect, use:
```bash
nc 127.0.0.1 1337
```
