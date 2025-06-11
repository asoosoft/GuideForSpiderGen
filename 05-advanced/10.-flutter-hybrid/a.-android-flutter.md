# A. Android 앱 구축하기(flutter)

### 1. Android 사용 환경 설정

Android 앱을 개발하기 위해서는 환경설정이 필요합니다.\
아래의 환경 설정 가이드의  <sub>Android Studio 설치, JAVA JDK 설치, JAVA\_HOME 환경변수 등록, Gradle설치, 환경변수 등록</sub> 항목을 참고해 환경을 설정해주세요.

[환경설정 가이드](../../03-start-guide/04-mobile/a-android.md)



### 2. flutter SDK설치

> [flutter 공식 홈페이지](https://docs.flutter.dev/get-started/install)

플러터 공식 메뉴얼에 따라 설치를 진행해주세요.



### 3. flutter SDK 환경변수 설정

* 환경변수 설정: "고급 시스템 설정" 실행 -> 고급탭 (환경 변수)
* 시스템변수 Path 편집
* 새로  만들기 "C:\flutter\bin" 추가 (flutter SDK를 설치한 경로에  맞게 수정)

<figure><img src="../../.gitbook/assets/image.png" alt="환경변수-시스템변수-Path편집"><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

명령 프롬프트를 열어 flutter doctor 명령어를 실행하고 추가로 필요한 조건을 확인합니다.

```powershell
flutter doctor
```

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>



### 4. flutter 프로젝트 생성

안드로이드 스튜디오의 New Flutter Project...\
또는 명령 프롬프트에서 flutter 명령어로 프로젝트를 생성합니다.

```powershell
flutter create 프로젝트명
```



### 5. flutter 플러그인 설치

> 플러터 플러그인을 활용하여 기본 제공되는 기능 외 추가적인 기능을 쉽게 구현할 수  있습니다.
>
> [flutter 공식 패키지 저장소](https://pub.dev/)

```powershell
cd 프로젝트명
flutter pub add flutter_inappwebview
#스파이더젠을 출력하기 위해 필요한기능이 확장된 웹뷰 플러그인
flutter pub add asset_fill
#빌드된 스파이더젠 정적 리소스를 쉽게 에셋에 등록하기 위한 플러그인
flutter pub get
#pubspec에 add 명령으로 등록된 플러그인 설치
```



### 6. 스파이더젠 웹페이지 등록

> flutter에서 정적 리소스를 사용할때 리소스를 프로젝트 루트 assets  디렉터리에 위치하고\
> pubspec.yaml에 등록해야 빌드 결과물에 포함됩니다.

생성한 flutter 프로젝트의 최 상위 루트에 assets 폴더를 생성합니다.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

스파이더젠에서 Build Project 기능으로 미리 빌드한 bin 폴더의 자료를 붙여 넣습니다.

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

pubspec.yaml을 열어 assets 하위의  필요한 디렉터리 및 파일을 직접 등록할 수 있습니다.

```yaml
# The following section is specific to Flutter packages.
flutter:
  assets:
    - assets/ #flutter는 명시된 디렉토리의 1-depth까지만 인식합니다.
```

또는 설치해두었던 "asset\_fill" 플러그인을 명령 프롬프트에서  실행하여\
자동으로 assets의 하위 디렉터리를 추가할 수 있습니다.

```powershell
flutter pub run asset_fill
#플러그인을 실행하면 assets를 제외 이하의 디렉토리가 자동으로 pubspec.yaml에 포함됩니다.
```

#### **최종적으로 아래와 같이 pubspec.yaml의 assets 항목이 작성됩니다.**

```yaml
flutter:
  assets:
    - assets/ #asset_fill 플러그인은 assets/을 추가하지 않으므로 필요한경우직접 추가해야 합니다.
    - assets/Assets/
    - assets/Framework/
    - assets/Framework/afc/
    - assets/Framework/afc/asset/
    - assets/Framework/afc/component/
    - assets/Framework/afc/default/
    - assets/Framework/afc/event/
    - assets/Framework/afc/image/
    - assets/Framework/afc/layout/
    - assets/Framework/afc/library/
    - assets/Framework/afc/style/
    - assets/Library/
    - assets/Query/
    - assets/Source/
    - assets/Source/page/
    - assets/Template/
    - assets/Template/Theme/
```



### 7. flutter에 웹뷰 위젯 추가

원하는 위젯의 위치에 설치했던 플러그인 "InAppWebView" 위젯을 추가합니다.

```dart
class WebViewExample extends StatefulWidget {
  const WebViewExample({super.key});

  @override
  State<WebViewExample> createState() => _WebViewExampleState();
}

class _WebViewExampleState extends State<WebViewExample> {
final webViewKey = GlobalKey();

  final settings = InAppWebViewSettings(
    webViewAssetLoader: WebViewAssetLoader(//WebViewAssetLoader로 정적 웹페이지를 로드합니다.
      //CORS정책을 우회하기 위해 file 프로토콜 대신 가상 도메인으로 매핑합니다.
      domain: "my.custom.domain.com",//웹뷰를 여러개 사용시 도메인을 분리하여 사용할 수 있습니다.
      pathHandlers: [
        // 웹뷰에서 정적 리소스를 불러올 수 있도록 '/assets/' 경로를 매핑합니다.
        AssetsPathHandler(path: '/assets/'),
      ],
    ),
  );

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('InAppWebView Example')),
      body: SafeArea(
        child: InAppWebView(//InAppWebView 위젯을 생성합니다.
          key: webViewKey,
          initialUrlRequest: URLRequest(
            url: WebUri(
                'https://my.custom.domain.com/assets/flutter_assets/assets/index.html'),
          ),
          ///flutter는 빌드후 assets에 포함된 리소스는 "/assets/flutter_assets"에 위치합니다.
          ///스파이더젠의 index.html은 "assets/index.html"에 위치하므로
          ///최종위치는"/assets/flutter_assets/assets/index.html"에 존재합니다.
          ///InAppWebViewSettings의 domain을 수정했다면 그에 맞게 수정해야 합니다.
          initialSettings: settings,
        ),
      ),
    );
  }
}
```



### 8. Android 실행 및 확인

안드로이드 스튜디오에서 Run 'main.dart' 기능을  이용하거나\
명령 프롬프트에서 flutter 명령어로 앱을 실행합니다.

```powershell
flutter run
```

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>



### 9. (추가) 예제코드

### addJavaScriptHandler

<figure><img src="../../.gitbook/assets/image (16).png" alt="" width="375"><figcaption></figcaption></figure>

InAppWebView 위젯은 controller객체의 `addJavaScriptHandler` 메서드를  이용하여\
아래와 같이 웹뷰가 flutter InAppWebView의  콜백을 호출할 수 있습니다.

<pre class="language-dart"><code class="lang-dart"><strong>///flutter
</strong>InAppWebView(
  key: webViewKey,
  initialUrlRequest: URLRequest(
    url: WebUri(
      'https://my.custom.domain.com/assets/flutter_assets/assets/index.html'),
    ),
    onWebViewCreated: (controller) {
      controller.addJavaScriptHandler(
          handlerName: 'myHandler',//웹뷰에서 myHandler이름으로 호출하면
          callback: (args) {
            print(args);
            return {'result': '플러터에서 응답'};//{result:값}이라는 json객체를 반환함
          },
        );
      },
    initialSettings: settings,
 ),
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
            console.log("플러터 콜백 호출 성공"+response.result)//반환값{result:값}
            resultTextBox.setText(response.result)
        });
}
</code></pre>

### postWebMessage

<figure><img src="../../.gitbook/assets/image (17).png" alt="" width="375"><figcaption></figcaption></figure>

InAppWebView 위젯은 controller객체의 `postWebMessage` 메서드를  이용하여\
아래와 같이 flutter가 웹뷰에게 메세지 이벤트를 트리거 할  수 있습니다.

<pre class="language-dart"><code class="lang-dart"><strong>///flutter
</strong>class _WebViewExampleState extends State&#x3C;WebViewExample> {
  InAppWebViewController? webViewController;
  final webViewKey = GlobalKey();
  final settings = InAppWebViewSettings(
    //생략
  );

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('InAppWebView Example')),
      body: Column(children: &#x3C;Widget>[
        InAppWebView(
          key: webViewKey,
          initialUrlRequest: URLRequest(
            url: WebUri(
                'https://my.custom.domain.com/assets/flutter_assets/assets/index.html'),
          ),
          onWebViewCreated: (controller) {
            webViewController = controller;
          },
          initialSettings: settings,
        ),
        TextButton(
          onPressed: () {
            webViewController?.postWebMessage(//postWebMessage 호출
                message:
                    WebMessage(data: "InAppWebView가 제공하는 postWebMessage 호출"));
          },
          child: const Text("InAppWebView가 제공하는 postWebMessage 호출"),
        ),
      ]),
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
		//예상 값 "InAppWebView가 제공하는 postWebMessage 호출"
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

### evaluateJavaScript

<figure><img src="../../.gitbook/assets/image (18).png" alt="" width="375"><figcaption></figcaption></figure>

InAppWebView 위젯은 controller객체의 `evaluateJavaScript` 메서드를  이용하여\
아래와 같이 flutter가 웹뷰 자바스크립트를 직접 호출할 수 있습니다.

<pre class="language-dart"><code class="lang-dart"><strong>///flutter
</strong>class _WebViewExampleState extends State&#x3C;WebViewExample> {
  InAppWebViewController? webViewController;
  final webViewKey = GlobalKey();
  final settings = InAppWebViewSettings(
    //생략
  );

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('InAppWebView Example')),
      body: Column(children: &#x3C;Widget>[
        InAppWebView(
          key: webViewKey,
          initialUrlRequest: URLRequest(
            url: WebUri(
                'https://my.custom.domain.com/assets/flutter_assets/assets/index.html'),
          ),
          onWebViewCreated: (controller) {
            webViewController = controller;
          },
          initialSettings: settings,
        ),
        TextButton(
          onPressed: () {
            webViewController?.evaluateJavascript(
              source: "window.postMessage('플러터에서 직접 웹뷰 이벤트 호출')");
            },//js기본 messege 이벤트를 활용
            child: const Text("플러터에서 직접 이벤트 호출"),
          ),
        TextButton(
          onPressed: () {
            webViewController?.evaluateJavascript(
              source: "webFunction('플러터에서 직접 웹뷰 함수 호출')");
            },//웹뷰에서 미리 정의한 전역함수 webFunction
            child: const Text("플러터에서 직접 웹뷰 함수 호출"),
          ),
      ]),
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

`android\app\src\main\kotlin\생성시_작성한_패키지_이름\MainActivity.kt`\
위치에 MainActivty.kt에서  `configureFlutterEngine`를 재정의하여\
네이티브 모듈을 직접 작성할 수  있습니다.

<pre class="language-kotlin"><code class="lang-kotlin"><strong>///android\app\src\main\kotlin\com\example\firstapp\MainActivity.kt
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
      appBar: AppBar(
        backgroundColor: Theme.of(context).colorScheme.inversePrimary,
        title: Text(widget.title),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: &#x3C;Widget>[
            TextButton(
              onPressed: getNativeMessage,
              child: const Text("플러터에서 네이티브 호출"),
            ),
          ],
        ),
      ),
    );
  }
}
</code></pre>



