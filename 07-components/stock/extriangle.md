# ExTriangle

<figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 100558.png" alt=""><figcaption></figcaption></figure>

업비트의 REST API와 WebSocket을 활용하여 종목 데이터, 캔들, 호가 등 다양한 데이터를 실시간으로 수집 및 표시하는 프레임워크.

상한, 상승, 보합, 하한, 하락을 표시하는 컴포넌트

***

### Appearance

공통 Appearance 는 [**6. Global Properties**](<../../Guide for SpiderGen/06  SpiderGen Editor/04  Properties Pane/02 Appearence.md>) 속성을 참고

### Attribute

EXTriangle 속성

<figure><img src="../../.gitbook/assets/스크린샷 2025-06-30 085048.png" alt=""><figcaption></figcaption></figure>

**Data**

<table data-header-hidden><thead><tr><th width="361"></th><th></th></tr></thead><tbody><tr><td><strong>이름</strong></td><td><strong>설명</strong></td></tr><tr><td><strong>색상 속성</strong></td><td></td></tr><tr><td><code>Use StockColor</code></td><td>stock 프레임워크의 기본 색상 사용 (<code>StockColor.UP_COLOR</code>, <code>StockColor.DOWN_COLOR</code>)</td></tr><tr><td><code>Up Color</code></td><td>상승 시 색상</td></tr><tr><td><code>Down Color</code></td><td>하락 시 색상</td></tr><tr><td><code>Direction</code></td><td>화살표 방향만 설정 가능. <strong>굵기 설정은 없음</strong></td></tr></tbody></table>



* Direction

<div><figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 084535.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 084611.png" alt=""><figcaption></figcaption></figure></div>

<div><figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 084618 (1).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 084625.png" alt=""><figcaption></figcaption></figure></div>

<div><figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 084633.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 084642.png" alt=""><figcaption></figcaption></figure></div>

### Example

**1. 프로젝트 생성**

* 프로젝트 트리뷰에서 Source > MainView.lay 파일을 클릭
* MainView의 레이아웃 파일이 오픈되면 컴포넌트 리스트에서 EXTriangle 컴포넌트를 선택하고 드래그하여 레이아웃에 배치
* Class에서 ID를 triangle로 입력

**2. 데이터 설정**

* 먼저 MainView.js 파일을 오픈
* 상단의 파일탭에서 MainView.lay 탭을 더블 클릭하거나 우측의 프로젝트 트리에서 MainView.js 파일을 더블 클릭
* 모든 화면뷰는 onInitDone() 함수가 존재하며 이 함수는 화면이 생성될 때 딱 한번 실행
* onInitDone() 함수에서 레이블의 텍스트 내용을 아래와 같이 코드를 입력

```javascript
onInitDone() {
    super.onInitDone();

    this.triangle.setUpDownColor('#FF0000', '#0000FF');
    triangle.setData(1); // 상한
    // 🔺 모양 변경 테스트
    // triangle.setData(2); // 상승
    // triangle.setData(3); // 보합
    // triangle.setData(4); // 하한
    // triangle.setData(5); // 하락
    
    this.triangle.setPos(100, 100);
}
```

**3. 프로젝트 실행**

* 설정한 데이터에 맞춰서 **상한, 상승, 보합, 하한, 하락 상태**가 화면에 표시.



* 왼쪽부터 상한-상승-보합-하한-하락

<div><figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 094257.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 094341.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 094712.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 094757.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 094830.png" alt=""><figcaption></figcaption></figure></div>



**4. 코드로** EXTriangle **생성**

* 먼저 MainView.js 파일을 오픈
* onInitDone() 함수에서 아래와 같이 코드를 입력

```javascript
onInitDone() {
    super.onInitDone();

    const exTriangle = new EXTriangle();
    exTriangle.init();

    // 색상 설정
    exTriangle.setUpDownColor('#ff0000', '#0000ff');
    // 방향 설정
    exTriangle.setData(1); // 상한
    // exTriangle.setData(2); // 상승
    // exTriangle.setData(3); // 보합
    // exTriangle.setData(4); // 하한
    // exTriangle.setData(5); // 하락

    this.addComponent(exTriangle);
    exTriangle.setPos(100, 100);
}
```



* 왼쪽부터 상한-상승-보합-하한-하락

<div><figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 094257 (2).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 094341 (2).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 094712 (2).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 094757 (2).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 094830 (2).png" alt=""><figcaption></figcaption></figure></div>

