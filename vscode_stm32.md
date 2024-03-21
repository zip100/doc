# 安装 Vscode
[[官网]](https://code.visualstudio.com/) 微软开发的代码编辑器

# 安装 OpenOCD
> [[官网]](https://openocd.org/pages/getting-openocd.html) 烧录和调试工具

# 安装 ToolChain
> [[官网]](https://developer.arm.com/Tools%20and%20Software/GNU%20Toolchain) 编译和调试工具链

# 安装三个 vs 插件
* STM32 VS code extension (STM32 支持插件)
* C/C++ extension pack（语言支持）
* cortext-debug （调试支持）


# 配置编辑器 (setting.json)
 ```json
    {
        "cortex-debug.gdbPath": "C:\\ST\\STM32CubeIDE_1.15.0\\STM32CubeIDE\\plugins\\com.st.stm32cube.ide.mcu.externaltools.gnu-tools-for-stm32.12.3.rel1.win32_1.0.100.202403111256\\tools\\bin\\arm-none-eabi-gdb.exe",
        "cortex-debug.openocdPath.windows": "C:\\openocd\\bin\\openocd.exe",
        "cortex-debug.armToolchainPath.windows": "C:\\Program Files (x86)\\Arm GNU Toolchain arm-none-eabi\\13.2 Rel1\\bin",
    }
 ```


# 把 OpenOCD 和 ToolChain 的 bin 目录加入环境变量

# 烧录命令
```
Openocd -f 'C:\openocd\openocd\scripts\interface\cmsis-dap.cfg' -f 'C:\openocd\openocd\scripts\target\stm32f7x.cfg' -c "program D:\\STM32\\Projects\\beep\\build\\debug\\build\\beep.elf verify reset exit"
```

```json
{
      "name": "Cortex debug",
      "type": "cortex-debug",
      "request": "launch",
      "servertype": "openocd",
      "cwd": "${workspaceFolder}",
      "interface": "swd",
      "executable": "build/debug/build/beep.elf",
      "svdFile": "${command:vscode-embedded.st.svd}/STM32F767.svd",
      "runToEntryPoint": "main",
      "configFiles": [
         "C:/openocd/openocd/scripts/interface/cmsis-dap.cfg",
         "C:/openocd/openocd/scripts/target/stm32f7x.cfg"
      ],
      "showDevDebugOutput": "raw",
      "preLaunchTask": "Build",
   }
```

# 使用 CubeIDE 创建 STM32 项目

# 然后在 Vscode -> STM32 -> Import Project
