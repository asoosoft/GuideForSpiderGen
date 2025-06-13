# Flutter<-->Android 통신하기

### 직접 네이티브 코드 작성

<figure><img src="../../../.gitbook/assets/image (19).png" alt="" width="375"><figcaption></figcaption></figure>

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
