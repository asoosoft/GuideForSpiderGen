# A. Android 앱 구축하기 로컬 서버 배포(flutter)

### 1. Android 개발 환경 구축

Android 앱을 개발하기 위해서는 환경설정이 필요합니다.\
아래의 환경 설정을 참고해서 진행 해주세요.

[환경설정 가이드](./)

### 2. flutter에 웹뷰 위젯 추가 및 로컬 서버 추가

`프로젝트이름/lib/main.dar` 에서 InAppLocalhostServer를 생성해 로컬서버를 배포하고 원하는 위젯의 위치에 설치했던 플러그인 "InAppWebView" 위젯을 추가합니다.

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
      body: InAppWebView( //InAppWebView를 생성하고 로컬서버를 출력
        initialUrlRequest: URLRequest(
          url: WebUri("http://localhost:8080/index.html"),
        )
      ),
    );
  }
}
</code></pre>

