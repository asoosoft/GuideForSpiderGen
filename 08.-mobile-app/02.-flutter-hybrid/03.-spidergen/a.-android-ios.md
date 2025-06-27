# A. 로컬 서버로 웹뷰 연결(Android/IOS)

{% hint style="success" %}
이 방법은 Android/IOS 모두 사용할 수 있습니다.
{% endhint %}

### 1. flutter 개발 환경 구축

flutter 앱을 개발하기 위해서는 환경설정이 필요합니다.\
아래의 환경 설정을 참고해서 진행 해주세요.

[환경설정 가이드](../01..md)



### 2. flutter에 웹뷰 위젯 추가 및 로컬 서버 추가

`프로젝트이름/lib/main.dart` 에서 InAppLocalhostServer를 생성해 로컬 서버를 배포하고\
원하는 위젯의 위치에 설치했던 플러그인 "InAppWebView" 위젯을 추가합니다.

<pre class="language-dart"><code class="lang-dart"><strong>/// lib\main.dart
</strong>import 'package:flutter/material.dart';
import 'package:flutter_inappwebview/flutter_inappwebview.dart';

//로컬 서버를 생성하기 위해 InAppLocalhostServer객체를 생성하고
//pubspec.yaml의 assets에 등록한 'assets/www'을 루트로 인식하게 합니다.
final InAppLocalhostServer localhostServer = InAppLocalhostServer(
  documentRoot: 'assets/www',
); 

Future&#x3C;void> main() async {//InAppLocalhostServer가 시작될때까지 기다리기위해 Future를 사용합니다
  // main()이 비동기로 실행될때 함께 동작하는 네이티브 코드들의 실행 타이밍이 예상과 다르게 될 수 있으므로
  // 이를 방지하기 위해 반드시 ensureInitialized()로 초기화해야 합니다.
  WidgetsFlutterBinding.ensureInitialized();
  await localhostServer.start();//로컬 서버 시작
  runApp(MaterialApp(home: const MyApp()));
}

class MyApp extends StatefulWidget {
  const MyApp({super.key});
  @override
  State&#x3C;MyApp> createState() => _MyAppState();
}

class _MyAppState extends State&#x3C;MyApp> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text("InAppWebView LocalhostServer Example")),
      body: InAppWebView( //InAppWebView를 생성
        initialUrlRequest: URLRequest(
          url: WebUri("http://localhost:8080/index.html"),
        )
      ),
    );
  }
}
</code></pre>



### 3. 네이티브 권한 허가

로컬 서버를 띄워서 페이지를 배포하고 웹뷰에 웹페이지를 출력하는 경우 권한이 필요합니다.

> **Android의 경우** `android\app\src\main\AndroidManifest.xml`를 열어 아래와 같이 추가합니다
>
> <pre class="language-xml"><code class="lang-xml">&#x3C;manifest xmlns:android="http://schemas.android.com/apk/res/android">
>     &#x3C;!-- 인터넷 연결을 허용합니다 -->
> <strong>    &#x3C;uses-permission android:name="android.permission.INTERNET"/>
> </strong>    ... 생략 ...
>     &#x3C;application
>         ... 생략 ...
> <strong>        android:usesCleartextTraffic="true"> &#x3C;!-- http 접근을 허용합니다 -->
> </strong>        ... 생략 ...
> </code></pre>

> **IOS의 경우** `ios\Runner\info.plist`를 열어 아래와 같이 추가합니다
>
> <pre class="language-xml"><code class="lang-xml">&#x3C;?xml version="1.0" encoding="UTF-8"?>
> &#x3C;!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
> &#x3C;plist version="1.0">
>     &#x3C;dict>
>         &#x3C;!-- 웹뷰에서 http 접근을 허용합니다 -->
> <strong>        &#x3C;key>NSAppTransportSecurity&#x3C;/key>
> </strong><strong>        &#x3C;dict>
> </strong><strong>            &#x3C;key>NSAllowsArbitraryLoadsInWebContent&#x3C;/key>
> </strong><strong>            &#x3C;true />
> </strong><strong>        &#x3C;/dict>
> </strong>        ... 생략 ...
> </code></pre>



### 4. Flutter<-->WebView 통신하기

> 빌드하고 싶은 플랫폼 운영체제와 방법에 따라\
> 하위 페이지 링크에서 웹뷰와  통신하는 방법을 알아보세요
>
> > [(활용) Flutter<-->WebView 통신하기](../flutter-less-than-greater-than-webview/)
> >
> > > [A. Flutter<-->Android 통신하기](../flutter-less-than-greater-than-webview/a.-flutter-less-than-greater-than-android.md)
> >
> > > [B. Flutter<-->IOS통신하기](../flutter-less-than-greater-than-webview/b.-flutter-less-than-greater-than-ios.md)
