# ExTriangle

<figure><img src="../../.gitbook/assets/스크린샷 2025-06-27 164338.png" alt=""><figcaption></figcaption></figure>



업비트의 REST API와 WebSocket을 활용하여 종목 데이터, 캔들, 호가 등 다양한 데이터를 실시간으로 수집 및 표시하는 프레임워크.

***

### Appearance

공통 Appearance 는 [**6. Global Properties**](<../../Guide for SpiderGen/06  SpiderGen Editor/04  Properties Pane/02 Appearence.md>) 속성을 참고

### Attribute

EXTriangle 속성

<figure><img src="../../.gitbook/assets/스크린샷 2025-06-30 085048.png" alt=""><figcaption></figcaption></figure>

**Data**

<table data-header-hidden><thead><tr><th width="361"></th><th></th></tr></thead><tbody><tr><td><strong>이름</strong></td><td><strong>설명</strong></td></tr><tr><td><strong>색상 속성</strong></td><td></td></tr><tr><td><code>Use StockColor</code></td><td></td></tr><tr><td><code>Up Color</code></td><td>상승색 설정</td></tr><tr><td><code>Down Color</code></td><td>하락색 설정</td></tr><tr><td><code>Direction</code></td><td> 화살표의 방향, 굵기 설정</td></tr></tbody></table>

### Example

**1. 프로젝트 생성**

* 프로젝트 트리뷰에서 Source > MainView.lay 파일을 클릭
* MainView의 레이아웃 파일이 오픈되면 컴포넌트 리스트에서 EXTriangle 컴포넌트를 선택하고 드래그하여 레이아웃에 배치
* Class 에서 ID를triangle로 입력

**2. 데이터 설정**

* 먼저 MainView.js 파일을 오픈
* 상단의 파일탭에서 MainView.lay 탭을 더블 클릭하거나 우측의 프로젝트 트리에서 MainView.js 파일을 더블 클릭
* 모든 화면뷰는 onInitDone() 함수가 존재하며 이 함수는 화면이 생성될 때 딱 한번 실행
* onInitDone() 함수에서 레이블의 텍스트 내용을 아래와 같이 코드를 입력

```javascript
onInitDone()
{
	super.onInitDone()

}
```

**3. 프로젝트 실행**

* 설정한 데이터에 맞춰서 각 가격과 거래량, 평균가, 현재가가 표시

**5. 코드로&#x20;**_**EXSecureTextField**_**&#x20;생성**

* 먼저 MainView.js 파일을 오픈
* onInitDone() 함수에서 아래와 같이 코드를 입력

```javascript
onInitDone()
{
	super.onInitDone()
	

}
```
