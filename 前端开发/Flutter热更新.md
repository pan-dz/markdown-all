
# Flutter 热更新（Code Push）

Flutter 官方不支持热更新，但有以下开源/商业方案可实现动态下发和热更新能力。

---

## 1. Shorebird（推荐）

- **GitHub**：https://github.com/shorebirdtech/shorebird
- **文档**：https://docs.shorebird.dev
- **简介**：目前最主流的 Flutter 热更新方案，支持 Android 和 iOS，可以在不经过应用商店审核的情况下，将新的 Dart 代码推送给用户。
- **特点**：
  - 支持 Android、iOS
  - 仅限 Dart 代码更新（不支持原生代码、资源文件更新）
  - 提供命令行工具和控制台
  - 有免费套餐，也有付费计划

### 快速上手

```bash
# 安装 shorebird CLI
curl --proto '=https' --tlsv1.2 https://raw.githubusercontent.com/shorebirdtech/install/main/install.sh -sSf | bash

# 登录
shorebird login

# 在 Flutter 项目中初始化
shorebird init

# 发布 release（首次提交应用商店的版本）
shorebird release android
shorebird release ios

# 发布热更新 patch（后续无需重新上架）
shorebird patch android
shorebird patch ios
```

---

## 2. Fair（58同城开源）

- **GitHub**：https://github.com/wuba/fair
- **文档**：https://fair.58.com
- **简介**：58同城开源的 Flutter 动态化框架，通过将 Dart 源码转换为 bundle 文件，实现 Widget 树和 State 的动态更新。
- **特点**：
  - 支持 UI 动态下发（Widget 级别）
  - 支持 JS 分发，类似 React Native 的动态更新
  - UI 渲染无损，像素级还原
  - 支持整页替换或部分替换

### 快速上手

```yaml
# pubspec.yaml
dependencies:
  fair: 3.2.1

dev_dependencies:
  build_runner: ^2.0.0
  fair_compiler: ^1.7.0

dependency_overrides:
  fair_version:
    path: ../fair/flutter_version/flutter_3_7_0
```

```dart
// 入口包裹 FairApp
void main() {
  WidgetsFlutterBinding.ensureInitialized();
  FairApp.runApplication(_getApp());
}

dynamic _getApp() => FairApp(
  child: MaterialApp(
    home: FairWidget(
      name: 'DynamicWidget',
      path: 'assets/bundle/lib_src_page_dynamic_widget.fair.json',
      data: {"fairProps": json.encode({})}
    ),
  ),
);
```

---

## 方案对比

| 方案 | 更新粒度 | 平台支持 | 是否开源 | 适用场景 |
|------|---------|---------|---------|---------|
| Shorebird | Dart 代码 | Android / iOS | 部分开源 | 修复 Bug、更新逻辑 |
| Fair | Widget UI + JS | Android / iOS / Web | 开源 | 动态更新页面 UI |

---

## 注意事项

- **iOS** 审核政策：Apple App Store 禁止下载可执行代码，Shorebird 的 iOS 实现通过解释器方式合规运行。
- **Android** 限制相对宽松，热更新方案更易实施。
- 热更新只适合更新**业务逻辑和 UI**，涉及原生插件、Flutter 引擎升级时仍需重新发版。
