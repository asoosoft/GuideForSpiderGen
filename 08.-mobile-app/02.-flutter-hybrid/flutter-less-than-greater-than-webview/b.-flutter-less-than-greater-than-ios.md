# B. Flutter<-->IOS통신하기

### 직접 네이티브 코드 작성

<figure><img src="../../../.gitbook/assets/image (6) (1) (1) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

`ios\Runner\AppDelegate.swift` 위치의 AppDelegate.swif에서 application 메서드를 재정의하여\
네이티브 모듈을 직접 작성하고  등록할 수  있습니다.

<pre class="language-kotlin"><code class="lang-kotlin"><strong>///ios\Runner\AppDelegate.swift
</strong>import Flutter
import UIKit

@main
@objc class AppDelegate: FlutterAppDelegate {
<strong>  override func application(
</strong>    _ application: UIApplication,
    didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?
  ) -> Bool {
    let controller: FlutterViewController = window?.rootViewController as! FlutterViewController

    let messageChannel = FlutterMethodChannel(
      name: "samples.flutter.dev/message", //호출할 MethodChannel 이름
      binaryMessenger: controller.binaryMessenger
    )

    messageChannel.setMethodCallHandler { (call, result) in
      if call.method == "printMessage" { //호출할 method 이름
        if let message = call.arguments as? String {
          print("Received from Flutter: \(message)")
          result("Received!")  // 플러터로 반환할 메시지
        } else {
          result(FlutterError(code: "INVALID_ARGUMENT", message: "No message received", details: nil))
        }
      } else {
        result(FlutterMethodNotImplemented)
      }
    }

    GeneratedPluginRegistrant.register(with: self)
    return super.application(application, didFinishLaunchingWithOptions: launchOptions)
  }
}
</code></pre>

AppDelegate.swift에서 정의한 채널 이름과 메서드 이름을 MethodChannel와 invokeMethod를 이용해서 아래와 같이 호출할 수 있습니다.

<pre class="language-dart"><code class="lang-dart"><strong>///flutter
</strong>class _MyHomePageState extends State&#x3C;MyHomePage> {
<strong>  static const MethodChannel platform = MethodChannel('samples.flutter.dev/message');
</strong>  
  Future&#x3C;void> sendMessage() async {
    try {
<strong>      final String response = await platform.invokeMethod('printMessage', "Hello from Flutter!");
</strong>      print("Received from iOS: $response");
    } on PlatformException catch (e) {
      print("Error: ${e.message}");
    }
  }
  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text("Flutter - iOS Native Communication")),
      body: Column(
        children: &#x3C;Widget>[
          TextButton(
            onPressed: sendMessage,
            child: const Text("플러터에서 네이티브 호출"),
          ),
        ],
      ),
    );
  }
}
</code></pre>
