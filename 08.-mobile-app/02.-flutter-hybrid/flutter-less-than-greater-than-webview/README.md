# (활용) Flutter<-->WebView 통신하기

> 이  가이드에서는 **플러터와 웹뷰(스파이더) 간 통신**하는 방법 3가지를 소개합니다.
>
> 웹뷰 구현 방식(로컬  서버  배포/웹뷰 가상 도메인 매핑)에 **상관없이** 필요한 방식 중 하나를 선택해 웹뷰와 플러터 간 통신을 구현해보세요.

### 1.addJavaScriptHandler

<figure><img src="../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

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
<strong>        onWebViewCreated: (controller) {
</strong><strong>          controller.addJavaScriptHandler(
</strong><strong>            handlerName: "myHandler",
</strong><strong>            callback: (args) {
</strong><strong>              return {'result': '플러터에서 응답 $args'};
</strong><strong>            },
</strong><strong>          );
</strong><strong>        },
</strong>      ),
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

### 2.postWebMessage

<figure><img src="../../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

InAppWebView 위젯은 controller객체의 `postWebMessage` 메서드를  이용하여\
아래와 같이 flutter가 웹뷰에게 메세지 이벤트를 트리거 할  수 있습니다.

<pre class="language-dart"><code class="lang-dart"><strong>///flutter
</strong>class _MyAppState extends State&#x3C;MyApp> {
<strong>  late InAppWebViewController _inAppWebViewController;
</strong>
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
<strong>              onWebViewCreated: (controller) {
</strong><strong>                _inAppWebViewController = controller;//콜백외부에서 사용할 수 있도록 controller 저장
</strong><strong>              },
</strong>            ),
          ),
          TextButton(
            onPressed: () {
<strong>              _inAppWebViewController.postWebMessage(
</strong><strong>                //postWebMessage 호출
</strong><strong>                message: WebMessage(data: "postWebMessage 호출됨!"),
</strong><strong>              );
</strong>            },
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

### 3.evaluateJavaScript<sub>(runJavaScript, runJavaScriptReturningResult 등...)</sub>

<figure><img src="../../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

InAppWebView 위젯은 controller객체의 `evaluateJavaScript` 메서드를  이용하여\
아래와 같이 flutter가 웹뷰 자바스크립트를 직접 사용할 수 있습니다.

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
<strong>              onWebViewCreated: (controller) {
</strong><strong>                _inAppWebViewController = controller;
</strong><strong>              },
</strong>            ),
          ),
          TextButton(
            onPressed: () {
<strong>              _inAppWebViewController.evaluateJavascript(
</strong><strong>                source: "window.postMessage('플러터에서 직접 웹뷰 이벤트 호출')",
</strong><strong>              );
</strong>            },
            child: Text("직접 웹뷰 이벤트 호출"),
          ),
          TextButton(
            onPressed: () {
<strong>              _inAppWebViewController.evaluateJavascript(
</strong><strong>                source: "webFunction('플러터에서 직접 웹뷰 함수 호출')",
</strong>              );
            },
            child: Text("직접 웹뷰 함수 호출"),
          ),
        ],
      ),
    );
  }
}
</code></pre>

직접 flutter의 InAppWebView가 자바스크립트 코드를 실행해서 웹뷰의 함수나 이벤트를 호출 하지만 \
스파이더젠 생명주기와는 별도의 컨텍스트에서 동작하므로 \
전역 함수나 window객체에 이벤트를 등록해야만 실행할 수 있습니다.

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

### 4. Flutter <--> Native

> 빌드하고 싶은 플랫폼에따라\
> 하위 페이지 링크에서 네이티브와 통신하는 방법을 추가로알아보세요
>
> > [A. Flutter<-->Android 통신하기](a.-flutter-less-than-greater-than-android.md)
>
> > [B. Flutter<-->IOS통신하기](b.-flutter-less-than-greater-than-ios.md)
