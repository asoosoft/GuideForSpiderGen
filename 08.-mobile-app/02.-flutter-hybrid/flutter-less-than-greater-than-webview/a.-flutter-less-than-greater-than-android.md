# A. Flutter<-->Android 통신하기

### 직접 네이티브 코드 작성

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

`android\app\src\main\kotlin\프로젝트_이름\MainActivity.kt`\
위치에 MainActivty.kt에서  configureFlutterEngine 메서드를 재정의하여\
네이티브 모듈을 직접 작성하고 등록할 수 있습니다.

<pre class="language-kotlin"><code class="lang-kotlin"><strong>///android\app\src\main\kotlin\com\example\프로젝트_이름\MainActivity.kt
</strong>package com.example.firstapp

import io.flutter.embedding.android.FlutterActivity
import io.flutter.embedding.engine.FlutterEngine
import io.flutter.plugin.common.MethodChannel

class MainActivity: FlutterActivity(){
    private val CHANNEL = "samples.flutter.dev/native" //호출할 MethodChannel 이름
    
<strong>    override fun configureFlutterEngine(flutterEngine: FlutterEngine) {
</strong>        super.configureFlutterEngine(flutterEngine)
<strong>        MethodChannel(flutterEngine.dartExecutor.binaryMessenger, CHANNEL)
</strong>            .setMethodCallHandler { call, result ->
                if (call.method == "getMessage") { //호출할 method 이름
                    val args = call.arguments as? Map&#x3C;String, Any> ?: ""
                    result.success("Hello from Android Native!"+args)
                } else {
                    result.notImplemented()
                }
            }
    }
}
</code></pre>

MainActivity.kt에서 정의한 채널 이름과 메서드 이름을 MethodChannel와 invokeMethod를이용해서 아래와 같이 호출할 수 있습니다.

<pre class="language-dart"><code class="lang-dart"><strong>///flutter
</strong>class _MyHomePageState extends State&#x3C;MyHomePage> {

  Future&#x3C;void> getNativeMessage() async {
<strong>    const platform = MethodChannel('samples.flutter.dev/native');
</strong>    try {
      final args = {'key': 'value'}; // 네이티브로 전달할 인자 (Map 형태)
      final result = await platform.invokeMethod('getMessage', args);
<strong>      print(result);// "Hello from Android Native!{key: value}" 출력 예상
</strong>    } on PlatformException catch (e) {
      print(e.message);
    }
  }

  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text("Flutter - Android Native Communication")),
      body: Column(
        children: &#x3C;Widget>[
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
