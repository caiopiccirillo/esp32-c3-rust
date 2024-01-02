# ESP32-C3 with Rust

A small experiment with ESP32-C3 and Rust

## Setup

### Install Rust

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

### WSL2 integration

1. Install the following packages:

* [USBIPD](https://github.com/dorssel/usbipd-win)

2. Run the following commands on WSL2:

```bash
sudo apt install linux-tools-generic hwdata
sudo update-alternatives --install /usr/local/bin/usbip usbip /usr/lib/linux-tools/*-generic/usbip 20
```

3. Plug the ESP32-C3 board and run the following command on PowerShell as administrator:

```powershell
usbipd list
```

Output:


```powershell
Connected:
BUSID  VID:PID    DEVICE                                                        STATE
1-2    303a:1001  Dispositivo Serial USB (COM5), USB JTAG/serial debug unit     Not shared
1-3    056a:0375  Wacom Tablet                                                  Not shared
1-4    0cf3:e007  Qualcomm QCA61x4A Bluetooth                                   Not shared
1-12   0bda:568a  Integrated Webcam                                             Not shared

Persisted:
GUID                                  DEVICE
````

4. Get the BUSID of the ESP32-C3 board (in this case is 1-2) and run the following command on PowerShell as administrator:

```powershell
usbipd bind --busid 1-2
usbipd attach --wsl --busid 1-2
```

5. The device should be available on WSL2:

```bash
ls /dev/ttyACM*
```

## Build

```bash
cargo build
```

## Flash and monitor serial

```bash
cargo run
```
