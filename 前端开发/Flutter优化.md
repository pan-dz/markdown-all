
### 包体积大小分析命令
flutter build apk --release --target-platform android-arm64 --analyze-size

flutter build apk --release --flavor prod --dart-define=APP_ENV=prod --target-platform android-arm64 --analyze-size