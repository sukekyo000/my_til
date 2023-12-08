
# Flutter×iOS×Firebase環境まとめ

## Firebaseプロジェクトの切り分け
1. `flutterfire configure`で生成される「firebase_app_id_file.json」と「GoogleService-Info.plist」を取得する
2. dev・local・prod切り分けのために「firebase_app_id_file_(flavor).json」を「ios/」直下に3つのファイルを作成
3. dev・local・prod切り分けのために「GoogleService-Info-(flavor).plist」を「ios/Runner/」直下に3つのファイルを作成
4. `open ios/Runner.xcworkspace`で Xcodeを開き、Build Phasesに移動
5. 「+」から「New Run Script Phase」を選択
6. 下記のスクリプトを追加
```
cp -f ${SRCROOT}/Runner/GoogleService-Info-${FIREBASE_PREFIX}.plist ${SRCROOT}/Runner/GoogleService-Info.plist
cp -f ${SRCROOT}/firebase_app_id_file_${FIREBASE_PREFIX}.json ${SRCROOT}/firebase_app_id_file.json
```
7. Output Filesに下記を追加
```
${SRCROOT}/Runner/GoogleService-Info.plist
${SRCROOT}/firebase_app_id_file.json
```
8. ios/.gitignoreに下記を追加
```
Runner/GoogleService-Info.plist
firebase_app_id_file.json
```