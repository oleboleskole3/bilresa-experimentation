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


