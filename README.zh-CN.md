# gimi_arm64（中文说明）

**面向 Android ARM64 的 3dmigoto 模型导入器：非破坏性 Vulkan 与 OpenGL ES 图形钩子**

gimi_arm64 是 GIMI（基于 3dmigoto）的 Android ARM64 移植版。它可以在游戏图形管线中替换 3D 模型、纹理并应用着色器修复（例如 `Orfix.ini` 和 `Txfix.ini`），无需修改 APK、获取 root 或改写游戏文件。

## 工作原理

项目通过 Android Vulkan 隐式层和 EGL 分发器拦截渲染调用，在内存中匹配资源哈希并替换顶点/索引缓冲区、纹理和着色器。原始游戏文件保持不变，支持 Vulkan 1.3 与 OpenGL ES 3.2。

## 功能

- 无需 root，在用户空间运行
- Vulkan 与 OpenGL ES 图形拦截
- 兼容 3dmigoto `.ini` 模组配置
- 支持 Orfix/Txfix 着色器修复
- 支持 ASTC、ETC2 和 RGBA8 纹理
- 启动器内置模组搜索、扫描、启用和停用

## 使用方法

1. 安装并启动 Shizuku，通过无线调试授权 GIMI 启动器；也可以使用电脑执行：
   ```bash
   adb shell pm grant com.gimi.launcher android.permission.WRITE_SECURE_SETTINGS
   ```
2. 在设备上创建 `/sdcard/GIMI/Mods/`，将每个 3dmigoto 模组放入独立子目录。
3. 在启动器的“模组管理”中扫描并选择模组，在控制台选择游戏版本后点击“注入 Vulkan 层并启动”。

## 从源码构建

需要 Android NDK r26 或更高版本：

```bash
./gradlew assembleDebug
```

也可以在 Termux 或轻量命令行环境执行 `bash build_termux.sh`。脚本会编译 `libgimi_arm64.so`、打包并签名 APK。

## 参与贡献

原生代码使用 C++20。请只在 Vulkan 层或 EGL 分发器边界进行拦截，不要修改游戏代码段。提交信息请使用结构化格式，例如 `feat(subsystem): 描述` 或 `fix(subsystem): 描述`。

## 许可证

本项目采用 MIT 许可证，详见 LICENSE 文件。
