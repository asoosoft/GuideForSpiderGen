# (활용) Firebase 네이티브 푸시알림

{% hint style="success" %}
이 방법은 Android/IOS 모두 사용할 수 있습니다.
{% endhint %}

> 네이티브 푸시를 통해 앱이 완전히 종료된 상태더라도 서버 신호를 통해 필요한 정보를 기기에게 전달할 수 있습니다.

### 1. 시스템 환경변수 설정

이전 개발 환경 설정 단계 외에 "flutterfire\_cli" dart 전역  플러그인을 사용하기 위해 추가적인 시스템 변수 설정이 필요합니다.

* 환경 변수 설정: "고급 시스템 설정" 실행 -> 고급 탭 (환경 변수)
* 시스템 변수 Path 편집
* 새로  만들기 "C:\Users\사용자명\AppData\Local\Pub\Cache\bin" 추가

<figure><img src="../../.gitbook/assets/image (13) (1) (1) (1) (1) (1).png" alt="환경변수-시스템변수-Path편집"><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/스크린샷 2025-09-23 165041.png" alt=""><figcaption></figcaption></figure>



### 2. Firebase 및 서비스 등록

Firebase에 앱을등록하면 네이티브 푸시 알림 서비스를 별도로 관리할 필요 없이 android, ios의 통합 관리할 수 있습니다. (다만,  FCM, APNs 등... 기능 사용의 경우 각각의 개발자 프로그램에 직접 등록 해야 함)

### 2.1 개발자 등록 및 푸시 서비스 설정

**만약 Android 앱 푸시를 구현하고 싶다면...**

> **Firebase Cloud Messaging(FCM) 설정**
>
> > [Firebase 콘솔](https://console.firebase.google.com/?authuser=1)
> >
> > FCM은 Firebase 등록 과정 만으로 사용할 수 있습니다.
> >
> > 1. 생성된 프로젝트 개요 페이지에서 안드로이드 아이콘(Android)을 클릭합니다.
> > 2. 앱의 \*\*패키지 이름(Package name)\*\*을 입력하고, 앱 닉네임과 디버그 서명 인증서(SHA-1)는 선택적으로 입력합니다.

**또는 IOS 앱 푸시를 구현하고 싶다면...**

> **Apple Developer Program 등록**
>
> > [Apple Developer Program](https://www.google.com/search?q=https://developer.apple.com/account/\&authuser=1)
> >
> > 애플 앱스토어에 앱을 배포하고 APNs를 포함한 애플의 여러 개발자 서비스를 이용하기 위해 필수입니다.
>
> **Apple Push Notification service(APNs) 설정**
>
> > 1. &#x20;[Apple Developer Program](https://www.google.com/search?q=https://developer.apple.com/account/\&authuser=1) 웹사이트에 로그인합니다.
> > 2. 상단 메뉴에서 '계정'을 클릭합니다.
> > 3. '프로그램 리소스' - '인증서, ID 및 프로파일' - '키'를 클릭합니다.
> > 4. 우측 상단의 파란색 '+' 버튼을 클릭합니다.
> > 5. 키 이름(예: `FCM_APNs_Key`)을 입력하고, 'Apple Push Notifications service (APNs)' 체크박스를 활성화합니다.
> > 6. 키 생성 및 다운로드: 계속 진행하면 키가 생성됩니다. 이때만 다운로드할 수 있으므로, 반드시 `.p8` 파일을 안전한 곳에 보관해야 합니다. 또한, 키와 함께 제공되는 '**Key ID**'를 복사해 둡니다.

### 2.2 Firebase 앱 등록

#### . Firebase 프로젝트 생성

1. Google 계정으로 [Firebase 콘솔](https://console.firebase.google.com/?authuser=1)에 접속하여 새로운 프로젝트를 만듭니다.
2. "프로젝트 추가" 버튼을 누르고, 프로젝트 이름을 입력합니다.

#### 2. 클라이언트 앱 등록

<sub>**안드로이드(Android) 앱**</sub>

> 1. 생성된 프로젝트 개요 페이지에서 안드로이드 아이콘(Android)을 클릭합니다.
> 2. 앱의 패키지 이름(Package name)을 입력하고, 앱 닉네임과 디버그 서명 인증서(SHA-1)는 선택적으로 입력합니다.

<sub>**iOS 앱**</sub>

> **Firebase 앱등록**
>
> 1. 프로젝트 개요 페이지에서 iOS 아이콘을 클릭합니다.
> 2. 앱의 번들 ID(Bundle ID)를 입력하고, 앱 닉네임과 앱스토어 ID는 선택적으로 입력합니다.
>
> **Firebase 클라우드 메세징 서비스 등록**
>
> 1. 앱이 등록된 [Firebase 콘솔](https://console.firebase.google.com/?authuser=1)로 이동합니다.
> 2. 좌측 상단의 톱니바퀴 아이콘을 클릭하고, '**프로젝트 설정**'으로 들어갑니다.
> 3. 상단 탭에서 '**클라우드 메시징**'을 선택합니다.
> 4. Apple 앱 구성 섹션에서 '**APNs 인증 키**' 영역을 찾습니다.
> 5. Key ID, team ID 정보 입력 및 `.p8` 파일 업로드



### 3. flutter 및 npm 플러그인 설치

쉽게 플러터에 fcm을 사용하려면 추가적인 플러그인과 라이브러리가 필요합니다.

```powershell
cd 프로젝트이름
#프로젝트 디렉토리로 이동
flutter pub add firebase_core
#파이어베이스 sdk 기본 플러그인
flutter pub add firebase_messaging
#파이어베이스 메세지 기능을 위한 플러그인
npm install -g firebase-tools
#firebase_cli를 사용하기 위한 npm 라이브러리
dart pub global activate flutterfire_cli
#플러터용 firebase_cli 사용하기 위한 플러그인
firebase login
#파이어 베이스 로그인
flutterfire configure
#파이어 베이스 프로젝트에 맞게 자동으로 프로젝트 종속성 설정
```

{% hint style="warning" %}
**Android**에서 firebase\_messaging를 사용하기 위해서는 android sdk버전이 23 이상이어야 합니다.

> The plugin 'firebase\_messaging' requires a higher Android SDK version.

위 오류 발생시 `프로젝트이름\android\app\build.gradle.kts` 를 열어 보유중인  SDK 버전 중 **23이상**을 아래와 같이 수정합니다.

![](<../../.gitbook/assets/image (251).png>)
{% endhint %}

{% hint style="warning" %}
**IOS**에서 firebase\_messaging를 사용하기 위해서는 sdk버전이 12.2.0 이상이어야 합니다.

> firebase\_messaging: Using Firebase SDK version '12.2.0' defined in 'firebase\_core'

위 오류 발생시 `프로젝트이름\ios\podfile` 을 열어 xcode에 설치된 SDK 버전 중 **12이상**으로 아래와 같이 버전을 수정합니다.

![](<../../.gitbook/assets/image (250).png>)

저장후 아래 코드를 터미널에서 실행합니다.

```bash
cd ios //ios 네이티브 코드 디렉토리로 이동합니다
pod install //수정된 podfile로 다시 설치합니다
```
{% endhint %}



### 4. flutter에 웹뷰 위젯 추가 및 로컬 서버 추가

`프로젝트이름/lib/main.dart` 에서 `FirebaseMessaging.instance`로 런타임에서 권한을 얻고 포어그라운드는 `FirebaseMessaging.onMessage`로 백그라운드는 `FirebaseMessaging.onBackgroundMessage`로 Firebase신호가올때 처리할 기능을 구현합니다.

<pre class="language-dart"><code class="lang-dart"><strong>/// lib\main.dart
</strong>import 'package:firebase_core/firebase_core.dart';
import 'package:firebase_messaging/firebase_messaging.dart';
import 'package:flutter/material.dart';
import 'package:flutter_jewel_market/external_web_view.dart';

final webViewKey = GlobalKey&#x3C;ExternalWebViewState>(); //하위 위젯에 접근하기 위해 위젯 키저장

Future&#x3C;void> main() async {
  WidgetsFlutterBinding.ensureInitialized(); //비동기 main과 네이티브가 동기화하기 위한 초기화
  await Firebase.initializeApp(); //firebase sdk 초기화

  // 알림 런타임 권한 요청
  NotificationSettings settings = await FirebaseMessaging.instance
      .requestPermission(
        alert: true,
        announcement: false,
        badge: true,
        carPlay: false,
        criticalAlert: false,
        provisional: false,
        sound: true,
      );

  if (settings.authorizationStatus == AuthorizationStatus.authorized) {
    debugPrint('사용자가 알림 권한을 허용했습니다.');
  } else if (settings.authorizationStatus == AuthorizationStatus.denied) {
    debugPrint('사용자가 알림 권한을 거부했습니다.');
  }

  // 포어그라운드 메시지 리스너 설정
  FirebaseMessaging.onMessage.listen((RemoteMessage message) {
    // GlobalKey를 사용해 _ExternalWebViewState의 메서드를 호출합니다.
    webViewKey.currentState?.handleFCMMessage(message);
    debugPrint('포어그라운드 메시지 처리: ${message.data}');
  });

  // 백그라운드 메세지 핸들러 등록
  FirebaseMessaging.onBackgroundMessage(_firebaseMessagingBackgroundHandler);

  runApp(MyApp());
}

//백그라운드에서 메세지가 오면 main 대신 이 함수가 진입점 역할을 합니다.
@pragma('vm:entry-point')
Future&#x3C;void> _firebaseMessagingBackgroundHandler(RemoteMessage message) async {
  webViewKey.currentState?.handleFCMMessage(message);
  debugPrint('백그라운드 메시지 처리: ${message.data}');
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        backgroundColor: Colors.white,
        appBar: null,
        body: SafeArea(child: ExternalWebView(key: webViewKey)),
      ),
    );
  }
}

</code></pre>

<pre class="language-dart"><code class="lang-dart"><strong>/// lib\external_web_view.dart
</strong>import 'dart:convert';

import 'package:firebase_messaging/firebase_messaging.dart';
import 'package:flutter/material.dart';
import 'package:flutter_inappwebview/flutter_inappwebview.dart';

class ExternalWebView extends StatefulWidget {
  const ExternalWebView({super.key});

  @override
  State&#x3C;ExternalWebView> createState() => ExternalWebViewState();
}

class ExternalWebViewState extends State&#x3C;ExternalWebView>
    with WidgetsBindingObserver {
  final String uri = "http://웹뷰에 띄울 주소";
  late InAppWebViewController webViewController;

  //fcm 신호가 오는경우 main에서 호출할 웹뷰 핸들러
  void handleFCMMessage(RemoteMessage message) {
    final data = message.data;
    final jsonData = jsonEncode(data);
    webViewController.evaluateJavascript(
      source://웹뷰에서 사용할 실행문
          '''
      console.log("push");
      const pushData = JSON.parse('$jsonData');
      window.dispatchEvent(new CustomEvent("push", { detail: { pushType:pushType, pushData: pushData } }));
    ''',
    );
  }

  @override
  Widget build(BuildContext context) {
    return InAppWebView(
        initialUrlRequest: URLRequest(url: WebUri(uri)),
        onWebViewCreated: (controller) {
          webViewController = controller;
        },
    );
  }
}
</code></pre>

### 5. 네이티브 권한 허가

네이티브 푸시 알림은 추가적인 알림 권한이 필요합니다.

> **Android의 경우** `android\app\src\main\AndroidManifest.xml`를 열어 아래와 같이 추가합니다.
>
> <pre class="language-xml"><code class="lang-xml">&#x3C;manifest xmlns:android="http://schemas.android.com/apk/res/android">
>     &#x3C;!-- POST_NOTIFICATIONS 권한과 런타임 권한 체크 후 알림센터 알림이 발생함 -->
> <strong>    &#x3C;uses-permission android:name="android.permission.POST_NOTIFICATIONS"/>
> </strong>    ... 생략 ...
>     &#x3C;application
>         ... 생략 ...
> </code></pre>

> **IOS의 경우** `ios\Runner\info.plist`를 열어 아래와 같이 추가합니다
>
> ```xml
> <?xml version="1.0" encoding="UTF-8"?>
> <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
> <plist version="1.0">
> <dict>
> 	<key>CADisableMinimumFrameDurationOnPhone</key>
> 	<true/>
> 	... 생략 ...
> ```
>
>
>
> 추가적으로  xcode를 열어 Signing & Capabilities에 아래와 같이 추가합니다.
>
> ![](<../../.gitbook/assets/스크린샷 2025-09-24 오후 4.11.03 (2).png>)![](<../../.gitbook/assets/image (247).png>)![](<../../.gitbook/assets/스크린샷 2025-09-24 오후 4.14.27 (1).png>)
