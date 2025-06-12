# A. Android 앱 구축하기 로컬 서버 배포(flutter)

### 1. flutter SDK 설치

이 가이드에서는 Visual Studio Code를 이용해서 flutter 프로젝트를 설치 및 생성합니다.

> Use VS code to install 항목을 참고하실 수 있습니다.
>
> [flutter 공식 설치 메뉴얼](https://docs.flutter.dev/get-started/install)

#### 1.1 Visual Studio Code 설치 및 extension 설치

자신의 운영체제와  원하는 설치 방법을 선택해 설치합니다

> [Visual Studio Code 공식 다운로드 페이지](https://code.visualstudio.com/Download)

<figure><img src="../../.gitbook/assets/image (1).png" alt="" width="563"><figcaption></figcaption></figure>

Visual Studio Code를 실행하고 좌측 사이드 메뉴에서 Extension 항목을 찾거나 (ctrl+shift+X)로 항목을 전환하고 익스텐션 마켓플레이스에서 Flutter를 찾아 설치합니다.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

익스텐션이 설치된 후 최 상단 명령 팔레트를 선택하거나 (ctrl+shift+P)로 팔레트를 열고 `>Flutter: New Project` 명령을 찾아 선택하면 flutter SDK가 없을 경우 설치 안내 팝업이 우하단에 출력됩니다.

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

이후  팝업모달 안내에따라 Clone Flutter 를 눌러 SDK 설치 위치를 선택하고 설치합니다.

#### 1.2 flutter SDK 설치 확인

정상적으로 SDK가 설치되고 환경변수까지 등록했다면\
명령 프롬프트를 열어 아래의 명령어를 입력하여 정상적으로 설치되었는지 확인할  수 있습니다.

```powershell
flutter --version
```

만약 아래와 같이 출력되지 않는다면 직접 sdk를 환경변수에 설정할 수 있습니다.

<figure><img src="../../.gitbook/assets/image (5).png" alt="" width="563"><figcaption></figcaption></figure>

#### 1.3 flutter SDK 수동 설치 및  확인

정상적으로 SDK가 설치되지 않았다면 아래의 링크에서 다운로드 후 직접 환경변수를 설정해야합니다.

> [flutter 공식 설치 메뉴얼](https://docs.flutter.dev/get-started/install)
>
> 운영체제를 선택한뒤 Download and install 항목에서 직접 설치할 수 있습니다.

* 환경변수 설정: "고급 시스템 설정" 실행 -> 고급탭 (환경 변수)
* 시스템변수 Path 편집
* 새로  만들기 "C:\flutter\bin" 추가 (flutter SDK 설치 경로 하위  "bin" 디렉토리)

<figure><img src="../../.gitbook/assets/image (13).png" alt="환경변수-시스템변수-Path편집"><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

### 2. 안드로이드스튜디오 설치

> [Android Studio 공식 홈페이지](https://developer.android.com/studio?hl=ko)

공식 홈페이지에서 안드로이드 스튜디오를 설치후 Android Studio를 실행합니다\
좌측 상단 main menu 버튼을 누르고 Tools - **SDK manager** 를 열어 아래 항목을 선택 후 설치합니다.

* Android SDK Platform, API 35
* Android SDK Command-line Tools
* Android SDK Build-Tools
* Android SDK Platform-Tools
* Android Emulator



### 3. flutter 사용 환경 설정 확인

아래 명령어를 실행해서 현재 flutter를 사용할 수 있는지 최종 확인합니다.

```
flutter doctor
```

정상적으로 설정이 완료되었다면 아래와 같이 출력 됩니다.\
만약 필요한 설정이 있다면 안내대로 추가 설정을 진행해주세요.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption><p>chrom과visual studio는 다른애플리케이션을 만들기 위해 필요한 것이므로 무시하여도 됩니다.</p></figcaption></figure>



### 4. flutter 프로젝트 생성 및 플러그인 설치

Visual Studio Code에서 최 상단 명령 팔레트를 선택하거나 (ctrl+shift+P)로 팔레트를 열고 `>Flutter: New Project` - `Application`명령을 선택하면 이전과 달리 정상적으로 flutter 프로젝트를 생성할 수 있습니다.

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

이후 스파이더젠을 간편하게 웹뷰로 등록할 수 있도록 몇 가지 플러그인을 설치할 수 있습니다.

> 플러터 플러그인을 활용하여 기본 제공되는 기능 외 추가적인 기능을 쉽게 구현할 수  있습니다.
>
> [flutter 공식 패키지 저장소](https://pub.dev/)

```powershell
cd 프로젝트명
flutter pub add flutter_inappwebview
#스파이더젠을 출력하기 위해 필요한 기능이 확장된 웹뷰 플러그인
flutter pub add asset_fill
#빌드된 스파이더젠 정적 리소스를 쉽게 에셋에 등록하기 위한 플러그인
flutter pub get
#pubspec에 add 명령으로 등록된 플러그인 설치
```

추가적으로 flutter\_inappwebview를 android os에서 사용하기 위해서는\
android ndk버전이 "27.0.12077973" 이상이어야 합니다.

경고 발생시 `프로젝트이름\android\app\build.gradle.kts` 를 열어 아래와 같이 버전을 수정해주세요

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

### 5. 스파이더젠 웹페이지 등록

생성한 flutter 프로젝트의 최 상위 루트에 assets 폴더를 생성합니다.

> flutter에서 정적 리소스를 사용할때 리소스를 프로젝트 루트 assets 디렉터리에 위치하고\
> pubspec.yaml에 등록해야 빌드 결과물에 포함됩니다.

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption><p>www 디렉터리는 웹뷰 관레일 뿐 필요에따라 사용하지 않아도 됩니다.</p></figcaption></figure>

생성한 디렉터리에 스파이더젠을 빌드한(Build Project F7) 파일을 assets디렉토리로 옮깁니다.

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

이후 pubspec.yaml을 열어 assets 하위의  필요한 디렉터리 및 파일을 직접 등록할 수 있습니다.

```yaml
# The following section is specific to Flutter packages.
flutter:
  assets:
    - assets/www/ # flutter는 명시된 디렉토리의 1-depth까지만 인식합니다.
```

또는 설치해두었던 "asset\_fill" 플러그인을 명령 프롬프트에서  실행하여\
자동으로 assets의 하위 디렉터리를 추가할 수 있습니다.

```powershell
dart pub run asset_fill
# 플러그인을 실행하면 assets를 제외 이하의 디렉토리가 자동으로 pubspec.yaml에 포함됩니다.
```

#### **최종적으로 아래와 같이 pubspec.yaml의 assets 항목이 작성됩니다.**

```yaml
flutter:
  assets:
    - assets/www/
    - assets/www/Assets/
    - assets/www/Framework/
    - assets/www/Framework/afc/
    - assets/www/Framework/afc/asset/
    - assets/www/Framework/afc/component/
    - assets/www/Framework/afc/default/
    - assets/www/Framework/afc/event/
    - assets/www/Framework/afc/image/
    - assets/www/Framework/afc/layout/
    - assets/www/Framework/afc/library/
    - assets/www/Framework/afc/style/
    - assets/www/Library/
    - assets/www/Query/
    - assets/www/Source/
    - assets/www/Source/page/
    - assets/www/Template/
    - assets/www/Template/Theme/
```

### 6. flutter에 웹뷰 위젯 추가 및 로컬 서버 추가

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



### 7. Android 실행 및 확인

안드로이드 에뮬레이터가 실행된 상태거나 실제 안드로이드 디바이스를 pc와 연결한 상태에서 Visual Studio Code의 `프로젝트이름/lib/main.dart` 를 열고 Run and Debug의 Run (F5)을 눌러 실행하거나\
명령프롬프트 창에서 프로젝트 디렉터리로 이동해 아래와 같은 명령어를 입력하면 디버깅 모드로 플러터앱이 실행됩니다.

```powershell
flutter run
```

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

### 9. APK 빌드

앱 개발을 마치고 실제 APK를 생성하고 싶다면 명령 프롬프트 창에서 프로젝트 디렉터리로 이동해 아래와 같은 명령어를 입력하면 `\build\app\outputs\flutter-apk\app-release.apk` 위치에 apk가 생성됩니다.

```powershell
flutter build apk
```

### 8. (추가) 통신 예제 코드

### addJavaScriptHandler

<figure><img src="../../.gitbook/assets/image (16).png" alt="" width="375"><figcaption></figcaption></figure>

InAppWebView 위젯은 controller객체의 `addJavaScriptHandler` 메서드를  이용하여\
아래와 같이 웹뷰가 flutter InAppWebView의  콜백을 호출할 수 있습니다.

<pre class="language-dart"><code class="lang-dart"><strong>///flutter
</strong>class _MyAppState extends State&#x3C;MyApp> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text("InAppWebView LocalhostServer Example")),
      body: InAppWebView(
        initialUrlRequest: URLRequest(
          url: WebUri("http://localhost:8080/index.html"),
        ),
        onWebViewCreated: (controller) {
          controller.addJavaScriptHandler(
            handlerName: "myHandler",
            callback: (args) {
              return {'result': '플러터에서 응답 $args'};
            },
          );
        },
      ),
    );
  }
}

</code></pre>

자바스크립트에서는 window객체를 통해 flutter InAppWebView가 전달한\
`window.flutter_inappwebview.callHandler`를 호출해 플러터에서 정의한 콜백을 실행할 수  있습니다.

<pre class="language-javascript"><code class="lang-javascript"><strong>///웹뷰(스파이더젠)
</strong>onSubmitToFlutterButtonClick(comp, info, e)
{
        const inputText = this.inputField.getText();
        const resultTextBox = this.resultTextBox;

        if (!window.flutter_inappwebview) return;
        window.flutter_inappwebview.callHandler('myHandler', inputText)//handlerName
        .then(function(response) {
            resultTextBox.setText(response.result) //예상값 플러터에서 응답 [args]
        });
}
</code></pre>

### postWebMessage

<figure><img src="../../.gitbook/assets/image (17).png" alt="" width="375"><figcaption></figcaption></figure>

InAppWebView 위젯은 controller객체의 `postWebMessage` 메서드를  이용하여\
아래와 같이 flutter가 웹뷰에게 메세지 이벤트를 트리거 할  수 있습니다.

<pre class="language-dart"><code class="lang-dart"><strong>///flutter
</strong>class _MyAppState extends State&#x3C;MyApp> {
  late InAppWebViewController _inAppWebViewController;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text("InAppWebView LocalhostServer Example")),
      body: Column(
        children: &#x3C;Widget>[
          Expanded(
            child: InAppWebView(
              initialUrlRequest: URLRequest(
                url: WebUri("http://localhost:8080/index.html"),
              ),
              onWebViewCreated: (controller) {
                _inAppWebViewController = controller;//콜백외부에서 사용할 수 있도록 controller 저장
                controller.addJavaScriptHandler(
                  handlerName: "myHandler",
                  callback: (args) {
                    print(args);
                    return {'result': '플러터에서 응답 $args'};
                  },
                );
              },
            ),
          ),
          TextButton(
            onPressed: () {
              _inAppWebViewController.postWebMessage(
                //postWebMessage 호출
                message: WebMessage(data: "postWebMessage 호출됨!"),
              );
            },
            child: Text("postWebMessage 호출"),
          ),
        ],
      ),
    );
  }
}

</code></pre>

자바스크립트에서는 window객체에 이벤트리스너를 등록해\
이벤트가 트리거되면 실행될 이벤트 핸들러를 등록할 수 있습니다.

<pre class="language-javascript"><code class="lang-javascript"><strong>///웹뷰(스파이더젠)
</strong>class TestView extends AView
{
	constructor()
	{
		super()
	}

	init(context, evtListener)
	{
		super.init(context, evtListener)
	}

	onInitDone()
	{
		super.onInitDone()
	}

	onMessageHandler=(event)=>
	{
	        this.resultTextBox.setText(event.data);
		//예상 값 "postWebMessage 호출됨"
	}

	onActiveDone(isFirst)
	{
		super.onActiveDone(isFirst)
        	window.addEventListener("message", this.onMessageHandler);
        	//윈도우 객체에 이벤트 등록
	}

    	onDeactiveDone()
    	{
        	super.onDeactiveDone()
        	window.removeEventListener("message",this.onMessageHandler);
        	//이벤트 클린업
    	}

}


</code></pre>

### evaluateJavaScript<sub>(runJavaScript, runJavaScriptReturningResult 등...)</sub>

<figure><img src="../../.gitbook/assets/image (18).png" alt="" width="375"><figcaption></figcaption></figure>

InAppWebView 위젯은 controller객체의 `evaluateJavaScript` 메서드를  이용하여\
아래와 같이 flutter가 웹뷰 자바스크립트를 직접 호출할 수 있습니다.

<pre class="language-dart"><code class="lang-dart"><strong>///flutter
</strong>class _MyAppState extends State&#x3C;MyApp> {
  late InAppWebViewController _inAppWebViewController;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text("InAppWebView LocalhostServer Example")),
      body: Column(
        children: &#x3C;Widget>[
          Expanded(
            child: InAppWebView(
              initialUrlRequest: URLRequest(
                url: WebUri("http://localhost:8080/index.html"),
              ),
              onWebViewCreated: (controller) {
                _inAppWebViewController = controller;
              },
            ),
          ),
          TextButton(
            onPressed: () {
              _inAppWebViewController.evaluateJavascript(
                source: "window.postMessage('플러터에서 직접 웹뷰 이벤트 호출')",
              );
            },
            child: Text("직접 웹뷰 이벤트 호출"),
          ),
          TextButton(
            onPressed: () {
              _inAppWebViewController.evaluateJavascript(
                source: "webFunction('플러터에서 직접 웹뷰 함수 호출')",
              );
            },
            child: Text("직접 웹뷰 함수 호출"),
          ),
        ],
      ),
    );
  }
}
</code></pre>

직접 flutter가 자바스크립트 코드를 실행해서 웹뷰의 함수나 이벤트를 호출 하지만 \
스파이더젠 생명주기와는 별도의 컨텍스트에서 동작하므로 \
전역 함수나 window객체에 이벤트를 등록해야만 실행할  수 있습니다.

<pre class="language-javascript"><code class="lang-javascript"><strong>///웹뷰(스파이더젠)
</strong>class TestView extends AView
{
	constructor()
	{
		super()
	}

	init(context, evtListener)
	{
		super.init(context, evtListener)
	}

	onInitDone()
	{
		super.onInitDone()
        	const resultTextBox = this.resultTextBox;
        	window.webFunction = function(message)//전역 함수 등록
        	{
            		console.log("전역함수 호출됨")
            		resultTextBox.setText(message);
        	}
	}

	onMessageHandler=(event)=>
	{
	        this.resultTextBox.setText(event.data);
		//예상 값{data: "플러터에서 직접 웹뷰 이벤트 호출"}
	}

	onActiveDone(isFirst)
	{
		super.onActiveDone(isFirst)
        	window.addEventListener("message", this.onMessageHandler);
	}

    	onDeactiveDone()
    	{
        	super.onDeactiveDone()
        	window.removeEventListener("message",this.onMessageHandler);
    	}

}
</code></pre>

### 직접 네이티브 코드 작성

<figure><img src="../../.gitbook/assets/image (19).png" alt="" width="375"><figcaption></figcaption></figure>

`android\app\src\main\kotlin\프로젝트_이름\MainActivity.kt`\
위치에 MainActivty.kt에서  `configureFlutterEngine`를 재정의하여\
네이티브 모듈을 직접 작성할 수  있습니다.

<pre class="language-kotlin"><code class="lang-kotlin"><strong>///android\app\src\main\kotlin\com\example\프로젝트_이름\MainActivity.kt
</strong>package com.example.firstapp

import io.flutter.embedding.android.FlutterActivity
import io.flutter.embedding.engine.FlutterEngine
import io.flutter.plugin.common.MethodChannel

class MainActivity: FlutterActivity(){
    private val CHANNEL = "samples.flutter.dev/native"//호출할 패키지 이름
    
    override fun configureFlutterEngine(flutterEngine: FlutterEngine) {
        super.configureFlutterEngine(flutterEngine)
        MethodChannel(flutterEngine.dartExecutor.binaryMessenger, CHANNEL)
            .setMethodCallHandler { call, result ->
                if (call.method == "getMessage") {//호출할 메서드 이름
                    val args = call.arguments as? Map&#x3C;String, Any> ?: ""
                    result.success("Hello from Android Native!"+args)
                } else {
                    result.notImplemented()
                }
            }
    }
}
</code></pre>

MainActivity.kt에서 정의한 패키지 이름과  메서드 이름을 이용해서 아래와 같이 호출할 수 있습니다.

<pre class="language-dart"><code class="lang-dart"><strong>//flutter
</strong>class _MyHomePageState extends State&#x3C;MyHomePage> {

  Future&#x3C;void> getNativeMessage() async {
    const platform = MethodChannel('samples.flutter.dev/native');
    try {
      final args = {'key': 'value'}; // 네이티브로 전달할 인자 (Map 형태)
      final result = await platform.invokeMethod('getMessage', args);
      log(result.toString()); // "Hello from Android Native!{key: value}" 출력 예상
      print(result);
    } on PlatformException catch (e) {
      log("Failed to get message: '${e.message}'.");
      print(e.message);
    }
  }

  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text("InAppWebView LocalhostServer Example")),
      body: Column(
        children: &#x3C;Widget>[
          Expanded(
            child: InAppWebView(
              initialUrlRequest: URLRequest(
                url: WebUri("http://localhost:8080/index.html"),
              ),
              onWebViewCreated: (controller) {
                _inAppWebViewController = controller;
                controller.addJavaScriptHandler(
                  handlerName: "myHandler",
                  callback: (args) {
                    print(args);
                    return {'result': '플러터에서 응답 $args'};
                  },
                );
              },
            ),
          ),
          TextButton(
            onPressed: getNativeMessage,
            child: const Text("플러터에서 네이티브 호출"),
          ),
        ],
      ),
    );
  }
}
</code></pre>

