# WebView

![](../../.gitbook/assets/webview-comp-00.png)

HTML, CSS, JavaScript로 작성된 웹 콘텐츠를 로드하고 표시할 수 있는 **웹뷰 컴포넌트.**

### Data

![](https://wikidocs.net/images/page/24840/webview-ex-001.png)\


**`Load Url`** : 웹뷰에 로드할 Url 주소를 설정하는 속성.\


### Example

> #### 웹뷰에 스파이더젠 홈페이지 로드하기

#### 1. 툴을 이용하는 방법

**1-1. WebView 컴포넌트 추가 후, `Load Url`에 URI 를 입력**

![](../../.gitbook/assets/스크린샷_2025-01-23_163212.png)

#### 2. 코드로 추가하는 방법

```js
//웹뷰 컴포넌트를 생성
const webView = new AWebView(); 

// 초기화
webView.init()

// 웹뷰를 메인 뷰에 추가 
this.addComponent(webView); 

// 웹뷰에 로드할 URI를 설정
webView.setUrl('https://www.spidergen.com');
```
