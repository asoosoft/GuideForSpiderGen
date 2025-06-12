# Flutter<-->WebView 통신하기

### 1.addJavaScriptHandler

<figure><img src="../../../.gitbook/assets/image (16).png" alt="" width="375"><figcaption></figcaption></figure>

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

### 2.postWebMessage

<figure><img src="../../../.gitbook/assets/image (17).png" alt="" width="375"><figcaption></figcaption></figure>

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

### 3.evaluateJavaScript<sub>(runJavaScript, runJavaScriptReturningResult 등...)</sub>

<figure><img src="../../../.gitbook/assets/image (18).png" alt="" width="375"><figcaption></figcaption></figure>

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
