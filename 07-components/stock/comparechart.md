# CompareChart

<figure><img src="../../.gitbook/assets/스크린샷 2025-06-30 163703.png" alt=""><figcaption></figcaption></figure>

업비트의 REST API와 WebSocket을 활용하여 종목 데이터, 캔들, 호가 등 다양한 데이터를 실시간으로 수집 및 표시하는 프레임워크.

***

### Appearance

공통 Appearance 는 [**6. Global Properties**](<../../Guide for SpiderGen/06  SpiderGen Editor/04  Properties Pane/02 Appearence.md>) 속성을 참고

### Attribute

CompareChart 속성

<figure><img src="../../.gitbook/assets/스크린샷 2025-06-30 163755.png" alt=""><figcaption></figcaption></figure>

**Data**

<table data-header-hidden><thead><tr><th width="361"></th><th></th></tr></thead><tbody><tr><td><strong>이름</strong></td><td><strong>설명</strong></td></tr><tr><td><strong>색상 속성</strong></td><td></td></tr><tr><td><code>Text</code></td><td></td></tr><tr><td><code>Divide Line</code></td><td></td></tr><tr><td><code>Up</code></td><td></td></tr><tr><td><code>Down</code></td><td> </td></tr><tr><td><code>Dot</code></td><td></td></tr></tbody></table>

### Example

**1. 프로젝트 생성**

* 프로젝트 트리뷰에서 Source > MainView.lay 파일을 클릭
* MainView의 레이아웃 파일이 오픈되면 컴포넌트 리스트에서 CompareChart 컴포넌트를 선택하고 드래그하여 레이아웃에 배치
* Class에서 ID를 CompareChart 로 입력

**2. 데이터 설정**

* 먼저 MainView.js 파일을 오픈
* 상단의 파일탭에서 MainView.lay 탭을 더블 클릭하거나 우측의 프로젝트 트리에서 MainView.js 파일을 더블 클릭
* 모든 화면뷰는 onInitDone() 함수가 존재하며 이 함수는 화면이 생성될 때 딱 한번 실행
* onInitDone() 함수에서 레이블의 텍스트 내용을 아래와 같이 코드를 입력

```javascript
onInitDone() {
    super.onInitDone();


}
```

**3. 프로젝트 실행**

* 설정한 데이터에 맞춰서 상승, 하향 화살표가 표시

**4. 코드로** EXTriangle **생성**

* 먼저 MainView.js 파일을 오픈
* onInitDone() 함수에서 아래와 같이 코드를 입력

```javascript
onInitDone() {
    super.onInitDone();

    // 1. CompareChart 객체 생성
    this.compareChart = new CompareChart();

    // 2. 차트를 붙일 부모 DOM 엘리먼트 선택 (예: id가 'chartArea'인 div)
    const parentDiv = document.getElementById('chartArea');

    // 3. 차트 초기화
    this.compareChart.init(parentDiv, null);

    // 4. 데이터 세팅
    const mainData = [
        // 날짜, 시가, 고가, 저가, 종가, 거래량, 체결가
        ["20250101", 100, 110, 95, 105, 1000, 105],
        ["20250102", 105, 115, 102, 110, 1500, 110],
        ["20250103", 110, 120, 108, 115, 1800, 115],
        ["20250104", 115, 125, 112, 120, 2000, 120],
        ["20250105", 120, 130, 118, 125, 2200, 125],
        ["20250106", 125, 135, 122, 130, 2500, 130],
    ];

    // 5. 메인 데이터 세팅
    this.compareChart.setData([mainData]);

    // 6. 비교 데이터 추가 (optional)
    const compareData = [
        95,  // 날짜 기준 동일
        [105, 110, 115, 118, 122, 127], // 예시 종가 데이터
    ];
    this.compareChart.addCompareData(compareData);

    // 필요시 확대/축소 등 추가 설정 가능
    // this.compareChart.zoomInOut();

    console.log("CompareChart 초기화 완료");
}


```
