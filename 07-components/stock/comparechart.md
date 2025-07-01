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

<table data-header-hidden><thead><tr><th width="361"></th><th></th></tr></thead><tbody><tr><td><strong>이름</strong></td><td><strong>설명</strong></td></tr><tr><td><strong>색상 속성</strong></td><td></td></tr><tr><td><code>Text</code></td><td>차트 내 텍스트(레이블, 축 값, 날짜 등)에 적용되는 색상</td></tr><tr><td><code>Divide Line</code></td><td>메인 영역과 오른쪽 값 영역을 구분하는 기준선의 색상</td></tr><tr><td><code>Up</code></td><td>상승 시 표시되는 색상</td></tr><tr><td><code>Down</code></td><td>하락시 표시되는 색상</td></tr><tr><td><code>Dot</code></td><td>배경 점선(Grid Line)에 적용되는 색상</td></tr></tbody></table>

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

    const baseData = [
        ['20250701', 100, 110, 95, 105, 1000, 105000],
        ['20250702', 105, 115, 102, 110, 1200, 132000],
        ['20250703', 110, 120, 108, 115, 1500, 172500],
        ['20250704', 115, 125, 112, 118, 1700, 200600],
        ['20250705', 118, 130, 117, 128, 1900, 243200],
    ];

    const mapping = [0, 1, 2, 3, 4, 5, 6];

    // ✅ 기본 데이터 세팅
    this.CompareChart.setData([baseData], mapping);

    // ✅ 비교 데이터는 종가만 배열로
    const compareData = [205, 210, 215, 218, 228];

    // ✅ 비교 종목 추가
    this.CompareChart.addCompareData(['비교종목', compareData]);

    // ✅ 위치 및 크기 (옵션)
    this.CompareChart.setPos(50, 50);
    this.CompareChart.setSize(640, 400);
}
```

**3. 프로젝트 실행**

<figure><img src="../../.gitbook/assets/스크린샷 2025-07-01 094504.png" alt=""><figcaption></figcaption></figure>

* 설정한 데이터에 맞춰서 캔들 차트와 비교선의 레이아웃 생성



**4. 코드로 CompareChart 생성**

* 먼저 MainView.js 파일을 오픈
* onInitDone() 함수에서 아래와 같이 코드를 입력



* **예제 1**

```
    onInitDone() 
    {
        super.onInitDone();

        // CompareChart DOM 생성 (라이브러리에서 요구하는 구조)
        const chartDiv = $(CompareChart.CONTEXT.tag)
            .attr('id', 'CompareChart')
            .css({
                width: "100%",
                height: "500px"
            });

        chartDiv.appendTo(this.$ele);

        // CompareChart 인스턴스 생성 및 초기화
        const chart = new CompareChart();
        chart.init(chartDiv[0]);

        // 메인 데이터 세팅
        const mainData = [
            [
                ["20240701", 100, 110, 95, 105, 10000, 105],
                ["20240702", 105, 115, 100, 112, 15000, 112],
                ["20240703", 112, 118, 108, 115, 12000, 115],
                ["20240704", 115, 125, 110, 120, 17000, 120],
                ["20240705", 120, 130, 115, 128, 19000, 128],
                ["20240706", 128, 135, 120, 130, 16000, 130],
                ["20240707", 130, 140, 125, 138, 20000, 138]
            ],
            [105, 112, 115, 120, 128, 130, 138]
        ];

        chart.setData(mainData);

        // 비교 데이터 추가
        chart.addCompareData(["NAVER", [102, 108, 113, 119, 125, 127, 135]]);
        chart.addCompareData(["KAKAO", [98, 105, 110, 117, 123, 126, 132]]);
        chart.addCompareData(["SAMSUNG", [100, 107, 114, 118, 124, 129, 137]]);

        // 포지션 업데이트
        const width = chart.getElement().clientWidth;
        const height = chart.getElement().clientHeight;
        chart.updatePosition(width, height);

        chart.updateGraph();

        // 객체 저장
        this.chart = chart;
    }
```

<figure><img src="../../.gitbook/assets/스크린샷 2025-07-01 100532.png" alt=""><figcaption></figcaption></figure>





* **예제 2**

```javascript
onInitDone() {
    super.onInitDone();

    // [1] 차트용 DOM 생성
    const chartDiv = $(CompareChart.CONTEXT.tag).css({
        width: "100%",
        height: "500px",
        border: "1px solid #ccc"
    });

    chartDiv.appendTo(this.$ele); // 현재 화면에 붙이기

    // [2] CompareChart 인스턴스 생성
    this.compareChart = new CompareChart();

    // [3] 차트 초기화
    this.compareChart.init(chartDiv[0]);

    // [4] 메인 데이터 세팅
    const mainData = [
        [
            ["20240101", 100, 110, 90, 105, 10000, 105],
            ["20240102", 105, 115, 95, 110, 15000, 110],
            ["20240103", 110, 120, 100, 115, 13000, 115],
            ["20240104", 115, 125, 105, 120, 14000, 120],
            ["20240105", 120, 130, 110, 125, 16000, 125],
            ["20240106", 125, 135, 115, 130, 17000, 130],
            ["20240107", 130, 140, 120, 135, 18000, 135]
        ],
        [105, 110, 115, 120, 125, 130, 135]
    ];

    this.compareChart.setData(mainData);

    // [5] 비교 데이터 세팅
    const compareData = ["비교종목", [100, 107, 112, 118, 123, 128, 133]];
    this.compareChart.addCompareData(compareData);

    // [6] 포지션 업데이트
    const width = chartDiv.width();
    const height = chartDiv.height();
    this.compareChart.updatePosition(width, height);

    // [7] === 상호작용 기능 추가 ===

    // (1) 윈도우 크기 변경 시 리사이즈 대응
    $(window).on('resize', () => {
        const w = chartDiv.width();
        const h = chartDiv.height();
        this.compareChart.updatePosition(w, h);
    });

    // (2) 종목 추가 버튼
    const addBtn = $('<button>종목 추가</button>').css({
        position: 'absolute',
        top: '10px',
        left: '10px',
        zIndex: 1000
    }).appendTo(this.$ele);

    addBtn.on('click', () => {
        const randomData = [
            "비교" + (this.compareChart.lineData.length),
            Array.from({ length: 7 }, (_, i) => 90 + Math.random() * 50)
        ];
        this.compareChart.addCompareData(randomData);
    });

    // (3) 스크롤 버튼
    const scrollLeftBtn = $('<button>← Left</button>').css({
        position: 'absolute',
        top: '50px',
        left: '10px',
        zIndex: 1000
    }).appendTo(this.$ele);

    scrollLeftBtn.on('click', () => {
        this.compareChart.scrollRToL(1);
    });

    const scrollRightBtn = $('<button>Right →</button>').css({
        position: 'absolute',
        top: '90px',
        left: '10px',
        zIndex: 1000
    }).appendTo(this.$ele);

    scrollRightBtn.on('click', () => {
        this.compareChart.scrollLToR(1);
    });

    // (4) 줌 인 / 줌 아웃 버튼
    const zoomInBtn = $('<button>Zoom +</button>').css({
        position: 'absolute',
        top: '130px',
        left: '10px',
        zIndex: 1000
    }).appendTo(this.$ele);

    zoomInBtn.on('click', () => {
        this.compareChart.rateVal += 0.1;
        this.compareChart.zoomState = 1;
        this.compareChart.zoomInOut();
    });

    const zoomOutBtn = $('<button>Zoom -</button>').css({
        position: 'absolute',
        top: '170px',
        left: '10px',
        zIndex: 1000
    }).appendTo(this.$ele);

    zoomOutBtn.on('click', () => {
        this.compareChart.rateVal -= 0.1;
        this.compareChart.zoomState = 2;
        this.compareChart.zoomInOut();
    });

    // === 초기 그리기 ===
    this.compareChart.updateGraph();
}
```

<figure><img src="../../.gitbook/assets/스크린샷 2025-07-01 100646.png" alt=""><figcaption></figcaption></figure>





<mark style="color:red;">**Build 에러 발생 시**</mark>

1. _**프로젝트 트리뷰에서 Framework > afc 우클릭 > Default Load Settings.. > library + Component > ADataMask.js + AToast.js 체크**_
2. _**프로젝트 트리뷰에서 Framework > stock우클릭 > Default Load Settings.. > Component > CompareChart.js 체크**_

<div><figure><img src="../../.gitbook/assets/스크린샷 2025-07-01 084622.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/스크린샷 2025-07-01 084631.png" alt=""><figcaption></figcaption></figure></div>
