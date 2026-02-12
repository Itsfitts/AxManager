# Reverse Shell Tutorial

AxManager now includes a reverse shell feature in its native starter. This allows you to gain a shell on the device with either System (UID 1000) or ADB (UID 2000) privileges.

## Ports
- **Port 1337**: Provides a shell with **System (UID 1000)** privileges. This is available only when AxManager is started using the system exploit.
- **Port 1338**: Provides a shell with **ADB (UID 2000)** privileges. This is available when AxManager is started via ADB.

## How to use

### Prerequisites
- AxManager must be activated using either the System Exploit or Wireless ADB.
- You must have a way to connect to the device's local ports (e.g., via `adb forward` or using a terminal app on the same device).

### Method 1: Connecting via ADB (from Computer)
If you want to access the shell from your computer:

1.  Forward the port to your computer:
    ```bash
    # For System shell
    adb forward tcp:1337 tcp:1337
    # For ADB shell
    adb forward tcp:1338 tcp:1338
    ```

2.  Connect using `nc` (Netcat):
    ```bash
    nc 127.0.0.1 1337
    ```

### Method 2: Connecting from the Device
If you are using a terminal app on the device (like Termux):

1.  Connect directly to localhost:
    ```bash
    nc 127.0.0.1 1337
    ```

## Safety Warning
The reverse shell server listens on `127.0.0.1` (localhost) only, meaning it is only accessible from within the device or via an ADB forward. However, any app on the device with network permissions could potentially connect to these ports. Use this feature only when needed for debugging.
