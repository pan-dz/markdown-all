### vscode在连接模拟器的时候总是报错超时（用xcode打开ios目录，会发现有俩个报错，截图ai搜索xcode 在编译的时候报错）
### Failed to launch iOS Simulator: Error: Emulator didn't connect within 60 seconds
<p>
原因：这是 Flutter 项目中常见的 CocoaPods 依赖问题；
<br />
解决方案：清理和重新安装 Pods（vscode无法热更新）
</p>

```
flutter clean

flutter pub get

cd ios

pod install
```

<p>
解决方案：vscode配置flutter sdk路径
</p>

```
# 查找flutter路径
which flutter

# vscode编辑路径 Cmd+Shift+P
# 输入 "Preferences: Open Settings (JSON)"

"dart.flutterSdkPath": "/Users/dengzhipan/my-software/flutter",

```


