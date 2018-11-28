# vscode_nrf52840_templete

Develop nrf52840 with vscode

# Tutorial

## 1. Linux

### Required Tools

- Visual Studio Code
- linux-arm-none-eabi (vscode extension)
- NRF5X Command Line Tools
- 

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

2. Add GNU tools to  PATH: 

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

    Note: The path needs to be modified based on your extension version.

### Step 3. Install Segger Jlink Tools


   

   