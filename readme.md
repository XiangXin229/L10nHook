1、在 Visual Studio 中打开‌：

​    关闭当前解决方案。
​    使用 ‌“文件” -> “打开” -> “文件夹”‌ 打开项目根目录。
​    Visual Studio 会自动检测到 CMakePresets.json。
​    在顶部工具栏的配置下拉菜单中，你现在应该能看到 ‌x64-debug‌ 和 ‌Win32 (x86) Debug‌ 两个选项。
​    选择所需架构，VS 会自动运行 CMake 配置，生成所需构建环境。

2、使用对应架构的批处理可以生成VS解决方案

3、使用 Ninja、MinGW Makefiles 等非 IDE 生成器编译x86架构

方案 A：使用 Visual Studio 开发者命令提示符

在开始菜单中找到 ‌"x86 Native Tools Command Prompt for VS 20xx"‌ 并打开。
在该命令行窗口中执行：

```bat
mkdir build
cd build
cmake -G "Ninja" ..  # 或者 -G "NMake Makefiles"
cmake --build . --config Release
```

因为环境已经是 x86 模式，CMake 检测到的指针大小将是 4 字节，从而自动将 HOOK_TARGET_ARCH 设置为 x86。

方案 B：手动调用 vcvarsall.bat (如果在普通 CMD/PowerShell 中)

```bat
# 1. 初始化 x86 编译环境 (路径根据你的 VS 安装位置可能不同)
call "C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Auxiliary\Build\vcvarsall.bat" x86

# 2. 配置和编译
mkdir build
cd build
cmake -G "Ninja" ..
cmake --build . --config Release
```