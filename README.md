# ofxAutoCam

## Introduction

openFrameworksのofCamera関数を拡張したものです。

また、 @rhizomatiks が開発したDynamic VR Displayの技術もこのアドオンを使うことにより、再現できます。



## Notice

* openFrameworks 0.9.8 Windows版のみ対応しております。 (openFrameworks 0.10.0 Windows版の対応は、ofxCvが0.10.0に対応すれば対応するはずです)
* macOSや、Linuxには公式には対応しておりません。
* 自作アドオンを他のアドオンと区別するためにofxのあとにMb21mlとつけています。



##Dependency

ofxOpenCv

ofxCv

ofxSpout2 (Dynamic VR Displayの投影用映像を送信するために使います。)



## Instruction

### Setup

#### Basic

1. ofxOpenCv, ofxCv, そしてこのアドオンをダウンロードして、Addonフォルダに入れます。
2. openFrameworksのProject GeneratorのAddon欄にofxOpenCv, ofxCv, ofxMb21mlAutoCamを入れて、プロジェクトを生成します。



#### Dynamic VR Display

1. ofxOpenCv, ofxCv, ofxSpout2, そしてこのアドオンをダウンロードして、Addonフォルダに入れます。
2. openFrameworksのProject GeneratorのAddon欄にofxOpenCv, ofxCv, ofxSpout2, ofxMb21mlAutoCamを入れて、プロジェクトを生成します。



### Integrate

#### Basic

1. ofxMb21mlAutoCam.hをincludeさせます。

   > Reference
   >
   > ```c++
   > #include "ofxMb21mlAutoCam.h"
   > ```
   >
   > ofApp.h

2. アドオンをヘッダーで定義します。

   > Reference
   >
   > ```c++
   > ofxAutoCam autocam;
   > ```
   >
   > ofApp.h

3. Setup関数を使用してセットアップを行います。

   > Reference
   >
   > ```c++
   > setup("プロジェクト名", フレームレート制限値, ディスプレイモード (Basic: 1, Dynamic VR Display: 2), ディスプレイ幅, ディスプレイ高);
   > ```
   >
   > ofApp.cpp

   

   > Example
   >
   > ```c++
   > autocam.setup("Project X", 60, 1, 1920, 1080);
   > ```
   >
   > ofApp.cpp

4. Update関数を挿入します。

   > Reference
   >
   > ```c++
   > //--------------------------------------------------------------
   > void ofApp::update(){
   > 	autocam.update();
   > }
   > ```
   >
   > ofApp.cpp

5. 描画する範囲を囲います。

   > Reference
   >
   > ```c++
   > autocam.begin();
   > //描画
   > autocam.end();
   > ```
   >
   > ofApp.cpp

6. カメラの動作の設定を行ってください。

   カメラの切り替え効果をカットにする場合は

   ```c++
   autocam.SetTransCut();
   ```

   と挿入してください。

   

   カメラの切り替え効果をモーフィングにする場合は

   ```c++
   autocam.SetTransVR(スピード);
   ```

   と挿入してください。なお、括弧内のスピードは、必要に応じて数字を入力してください。

   

   現実のカメラを動かす場合は、

   ```c++
   autocam.vcam(位置X, 位置Y, 位置Z, 目線X, 目線Y, 目線Z);
   ```

   と挿入してください。 (今後変更予定) 必要に応じて、モーションキャプチャーデバイスと連携を作成してください。

   

   仮想のカメラを動かす場合は、

   ```c++
   autocam.vcam(位置X, 位置Y, 位置Z, 目線X, 目線Y, 目線Z);
   ```

   と挿入してください。

   

#### Dynamic VR Display

1. ofxMb21mlAutoCam.hをincludeさせます。

   > Reference
   >
   > ```c++
   > #include "ofxMb21mlAutoCam.h"
   > ```
   >
   > ofApp.h

2. アドオンをヘッダーで定義します。

   > Reference
   >
   > ```c++
   > ofxAutoCam autocam;
   > ```
   >
   > ofApp.h

3. Setup関数を使用してセットアップを行います。

   > Reference
   >
   > ```c++
   > setup("プロジェクト名", フレームレート制限値, ディスプレイモード (Basic: 1, Dynamic VR Display: 2), ディスプレイ幅, ディスプレイ高);
   > ```
   >
   > ofApp.cpp

   

   > Example
   >
   > ```c++
   > autocam.setup("Project X", 60, 2, 1920, 1080);
   > ```
   >
   > ofApp.cpp

4. Update関数を挿入します。

   > Reference
   >
   > ```c++
   > //--------------------------------------------------------------
   > void ofApp::update(){
   > 	autocam.update();
   > }
   > ```
   >
   > ofApp.cpp

5. 描画する範囲を囲います。

   > Reference
   >
   > ```c++
   > autocam.begin();
   > //描画
   > autocam.end();
   > ```
   >
   > ofApp.cpp

6. Dynamic VR Displayの設定を行います。

   Update関数内に挿入することをおすすめします。

   > Reference
   >
   > ```c++
   > autocam.dvd(ディスプレイNo, 画面の縦横のサイズ (ofVec2f形式), 左上 (ofVec3f形式), 右上 (ofVec3f形式), 右下 (ofVec3f形式), 左下 (ofVec3f形式));
   > ```
   >
   > ofApp.cpp

7. カメラの動作の設定を行ってください。

   カメラの切り替え効果をカットにする場合は

   ```c++
   autocam.SetTransCut();
   ```

   と挿入してください。

   

   カメラの切り替え効果をモーフィングにする場合は

   ```c++
   autocam.SetTransVR(スピード);
   ```

   と挿入してください。なお、括弧内のスピードは、必要に応じて数字を入力してください。

   

   現実のカメラを動かす場合は、

   ```c++
   autocam.vcam(位置X, 位置Y, 位置Z, 目線X, 目線Y, 目線Z);
   ```

   と挿入してください。 (今後変更予定) 必要に応じて、モーションキャプチャーデバイスと連携を作成してください。

   

   仮想のカメラを動かす場合は、

   ```c++
   autocam.vcam(位置X, 位置Y, 位置Z, 目線X, 目線Y, 目線Z);
   ```

   と挿入してください。
