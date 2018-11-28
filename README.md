# vscode_nrf52840_templete

Develop nrf52840 with vscode

# Tutorial

## 1. Install required tools

### Required Tools

- Visual Studio Code
- linux-arm-none-eabi (vscode extension)
- NRF5X Command Line Tools
- Segger Jlink Tools
- Cortex-Debug (vscode extension)
- Nordic SDK v15.2.0
  
---

## *On Linux (Ubuntu 16.04 tested)*

### Step 1. Install visual studio code

1.  Download the .deb file from https://code.visualstudio.com/

2. Install the .deb package through command line:

   ```bash
   sudo apt install ./<file>.deb
   
   # If you're on an older Linux distribution, you will need to run this instead:
   # sudo dpkg -i <file>.deb
   # sudo apt-get install -f # Install dependencies
   ```

### Step 2. Install vscode extension --- linux-arm-none-eabi 

`linux-arm-none-eabi` is the GNU embedded toolchain for arm.  It's a ready-to-use, open source suite of tools for C, C++ and Assembly programming targeting Arm Cortex-M and Cortex-R family of processors.

1. In Visual Studio Code goto extensions (shift+ctrl+x), search for `metalcode-eu`, choose `linux-arm-none-eabi` and click install.

2. Add GNU tools to PATH: 

    2.1  Open .bashrc or .zshrc (depends on your system)

    ```bash
    gedit ~/.bashrc
    ```

    2.2  Add path to .bashrc. The default extension path is ~/.vscode/extensions/metalcode-eu.linux-arm-none-eabi-0.1.2, so add following lines in the end of .bashrc:

    ```bash
    # VSCODE Extension --- linux-arm-none-eabi-0.1.2
    export GNU_TOOLS="/home/chengbang/.vscode/extensions/metalcode-eu.linux-arm-none-eabi-0.1.2/bin"
    export GNU_INCLUDE_PATH="/home/chengbang/.vscode/extensions/metalcode-eu.linux-arm-none-eabi-0.1.2/lib/gcc/arm-none-eabi/7.3.1/include"
    ```

    *Note: The path needs to be modified based on your extension version.*

### Step 3. Install Segger Jlink Tools
1. Download Jlink software pack (Jlink_Linux_V640_X86_64.deb)from https://www.segger.com/downloads/jlink/
2. Install .deb file through command line. 
   ```bash
   sudo apt install Jlink_Linux_V640_X86_64.deb
   ```
   The default install path is: `/opt/SEGGER/JLink`

### Step 4. Install NRF5X Command Line Tools
1. Download nrf5x command line tools from http://infocenter.nordicsemi.com/index.jsp?topic=%2Fcom.nordic.infocenter.tools%2Fdita%2Ftools%2Fnrf5x_command_line_tools%2Fnrf5x_installation.html
2. Extract the .tar archive anywhere on your filesystem.
3. Add to PATH. 
   Add following lines in the end of .bashrc:
   ```bash
    # NRF52 Command Line Tools
    export PATH="<Install path>/nrf_command_line_tools/mergehex:$PATH"
    export PATH="<Install path>/nrf_command_line_tools/nrfjprog:$PATH"
   ```
   
### Step 5. Install Cortex-Debug (vscode extension)
Debugging support for ARM Cortex-M Microcontrollers.

1. Launch VS Code Quick Open (Ctrl+P), paste the following command, and press enter.
   ```bash
   ext install marus25.cortex-debug
   ```
2. Configure the Jlink path.
In vscode, click `File->Preference->Settings->Extensions->Cortex-Debug-Configuration->Jlink GDBServer Path->Edit in settings.json`
3. Modify the user_settings of .json file in the right window:
   ```json
   {
       "cortex-debug.JLinkGDBServerPath": "/opt/SEGGER/JLink/JLinkGDBServerCLExe",
       "cortex-debug.armToolchainPath": "${env:GNU_TOOLS}"
   }
   ```
`Note: /opt/SEGGER is the default install path of Jlink Tools.`
### Step 6. Install Nordic SDK 15.2.0
1. To download the SDK, go to https://www.nordicsemi.com/eng/Products/Bluetooth-low-energy/nRF5-SDK
2. Download the repository file nRF5_SDK_x.x.x_xxxxxxx.zip (for example, nRF5_SDK_v15.2.0_9412b96.zip)
3. Extract the zip file to the directory that you want to use to work with the SDK.(for example, ~/NRF5_SDK)
4. Add to PATH.
   Add following lines in the end of .bashrc:
   ```bash
   export NRF_SDK="<Install path>/nRF5_SDK_15.2.0_9412b96"
   ```
5. Change the gcc path of sdk.
   Modify `$NRF_SDK/components/toolchain/gcc/Makefile.posix`.
   ```bash
   GNU_INSTALL_ROOT ?= ~/.vscode/extensions/metalcode-eu.linux-arm-none-eabi-0.1.2/bin/
   GNU_VERSION ?= 7.3.1
   GNU_PREFIX ?= arm-none-eabi
   ```
---

## *On Windows (Win10 64bit tested)*

*Note: Only describe different part with linux version.*

### Step 1. Install Visual Studio Code

Install windows version.

### Step 2. Install vscode extension --- windows-arm-none-eabi
1. In Visual Studio Code goto extensions (shift+ctrl+x), search for `metalcode-eu`, choose `windows-arm-none-eabi` and click install.

2. Add GNU tools to  PATH: 

### Step 3. Install Segger Jlink Tools

Install windows version.

### Step 4. Install NRF5X Command Line Tools
1. Download nrf5x command line tools from http://infocenter.nordicsemi.com/index.jsp?topic=%2Fcom.nordic.infocenter.tools%2Fdita%2Ftools%2Fnrf5x_command_line_tools%2Fnrf5x_installation.html
2. Run the installer and follow the given instructions.
3. Define the environment variables to the extracted directory to access the commands from anywhere in the command line.

### Step 5. Install Cortex-Debug (vscode extension)
Modify the JLink GDB Server path and GNU tools path in windows.

### Step 6. Install Nordic SDK 15.2.0

1. Set environment variables of install path.
2. Change the gcc path of sdk.
   Modify `$NRF_SDK/components/toolchain/gcc/Makefile.windows` and set the real path of your system.

---

## 2. Clone the templete project.

The templete project contains the whole configration of vscode project(.vscode folder):
1. Task: `build firmware`, `clean firmware`, `flash firmware`, `flash softdevice`, `erase flash`. --- $PROJ_PATH/PCA10056/s140/.vscode/tasks.json
2. Makefile --- $PROJ_PATH/pca10056/s140/armgcc/Makefile
   The makefile is based on the PATH or environment variables. So do not need to change it if you set PATH correctly as mentioned before.
3. Cortex-Debug confirguation --- $PROJ_PATH/PCA10056/s140/.vscode/launch.json
   