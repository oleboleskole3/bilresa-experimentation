# Docs:

Datasheet: available at <https://www.qorvo.com/products/p/QPG6200L#documents>

SDK: docs at <https://qorvo_sdk.gitlab.io/public/devkits/qpg6200-iot-sdk/QPG6200-IoT-SDK/2.0.1/sphinx/docs/QUICKSTART.html#install-the-sdk>

Platform tools / general info: <https://qorvo_sdk.gitlab.io/public/tools/packages/qorvo-platform-tools/index.html>

# SDK installation

Must be installed on Ubuntu, I used an Ubuntu docker container (`docker run -it ubuntu bash`)

```bash
git clone https://gitlab.com/qorvo_sdk/public/devkits/qpg6200-iot-sdk
```

Trying to install SDK gives errors, install script tries to install python 3.11, fixed by replacing all instances of "python3.11" with "python3" in `Scripts/bootstrap.sh` to use latest version of python.

Install script was unable to clone required submodules because I'm missing ssh access to gitlab, changed submodules to use https instead
```bash
git submodule set-url Components/ThirdParty/Matter/repo https://gitlab.com/qorvo_sdk/public/stacks/matter-sdk-qorvo.git
git submodule set-url Components/ThirdParty/OpenThread/ot-qorvo https://gitlab.com/qorvo_sdk/public/stacks/ot-qorvo.git
```

After these fixes I was successfully able to install the SDK
```bash
source ./Scripts/activate.sh
```

To download precompiled example binaries, enable git lfs
```bash
git lfs install
git lfs pull
```

# Compiling

cd into directory of example, then run make
```bash
cd Applications/Zigbee/Switch/
make -f Makefile.Switch_Zigbee_qpg6200 clean
make -f Makefile.Switch_Zigbee_qpg6200
```

Successful compilation!
```
+----------------+------------------------------+
|                | Switch_Zigbee_qpg6200.map    |
+----------------+------------------------------+
| Flash          |  426017/2011136 -    21.18 % |
| Flash+NVM+OTA  |  978977/2011136 -    48.68 % |
| Ram            |   46150/ 329728 -    14.00 % |
| Stack          |     512/ 329728 -     0.16 % |
| Heap           |  283066/ 329728 -    85.85 % |
| Ram+Heap+Stack |  329728/ 329728 -   100.00 % |
| ------         | ------                       |
| APP            | Flash:    974 / RAM:  4417   |
| BLE            | Flash:   1928 / RAM:   558   |
| MAC            | Flash:  29832 / RAM:  2892   |
| Matter         | Flash:      0 / RAM:     0   |
| OS/Libs        | Flash: 192970 / RAM: 34742   |
| Security       | Flash:   3745 / RAM:     5   |
| Thread         | Flash:      0 / RAM:     0   |
| Zigbee         | Flash: 197186 / RAM:   837   |
+----------------+------------------------------+
```

# Connecting to chip

Official SDK uses SEGGER J-Link to communicate. As I do not currently own any J-Link devices, this project will be put on hiatus until my J-Link arrives.

The chip is an ARM Cortex-M4

If we're lucky, secure boot on the QPG6200 is disabled. If not, re-flashing the device with custom firmware will most likely be impossible (unless someone figures out a bypass for the QPG6200 in the very near future (very unlikely)). In this situation, the included processor (QPG6200) *must* be removed/replaced before custom firmware is possible. This shouldn't be too bad, since the processor is on a seperate *propietary* IKEA network module, whose pinout can be replicated on a custom pcb.

## Alternative processors

In case secure boot is enabled, and the processor must be replaced, it will most likely be to one of the following:
- ESP32H2
- ESP32C5
- Something in the nRF52 series
