# B. 웹뷰 가상 도메인 맵핑(Android)

{% hint style="warning" %}
이 방법은 Android에서만 사용할 수 있습니다.
{% endhint %}

### 1. flutter 개발 환경 구축

flutter 앱을 개발하기 위해서는 환경설정이 필요합니다.\
아래의 환경 설정을 참고해서 진행 해주세요.

[환경설정 가이드](../01.-flutter.md)



### 2. flutter에 웹뷰 위젯 추가

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
    webViewAssetLoader: WebViewAssetLoader(//WebViewAssetLoader로 로컬 웹페이지를 로드합니다.
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
                'https://my.custom.domain.com/assets/flutter_assets/assets/www/index.html'),
          ),
          ///flutter는 빌드후 assets에 포함된 리소스는 "/assets/flutter_assets"에 위치합니다.
          ///스파이더젠의 index.html은 "assets/www/index.html"에 위치하므로
          ///최종위치는"/assets/flutter_assets/assets/www/index.html"에 존재합니다.
          ///InAppWebViewSettings의 domain을 수정했다면 그에 맞게 수정해야 합니다.
          initialSettings: settings,
        ),
      ),
    );
  }
}
```



### 3. Flutter<-->WebView 통신하기

> 빌드하고 싶은 플랫폼 운영체제와 방법에따라\
> 하위 페이지 링크에서 웹뷰와  통신하는 방법을 알아보세요
>
> > [03. Flutter<-->WebView 통신하기](../03.-flutter-less-than-greater-than-webview/)
>
> > [A. Flutter<-->Android 통신하기](../03.-flutter-less-than-greater-than-webview/a.-flutter-less-than-greater-than-android.md)
