# CandleChart

<figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 112359.png" alt=""><figcaption></figcaption></figure>

금융 데이터(주식, 코인, 선물 등)의 시세 변동을 시각화하는 대표적인 차트.

**시가(Open), 고가(High), 저가(Low), 종가(Close)** 네 가지 가격 정보를 시각적으로 보여주는  역할.

각 캔들은 선택한 시간 단위(일, 주, 월, 분, 틱) 동안의 가격 변동을 시각적으로 제공.

일봉 차트에서는 하나의 캔들이 하루 동안의 시가(Open), 고가(High), 저가(Low), 종가(Close)를 의미.

### Appearance

공통 Appearance 는 [**6. Global Properties**](<../../Guide for SpiderGen/06  SpiderGen Editor/04  Properties Pane/02 Appearence.md>) 속성을 참고

#### Attribute

CandleChart 속성

<figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 144258.png" alt=""><figcaption></figcaption></figure>

**Data**

<table data-header-hidden><thead><tr><th width="361"></th><th></th></tr></thead><tbody><tr><td><strong>이름</strong></td><td><strong>설명</strong></td></tr><tr><td><code>Mode</code></td><td>차트 타입 선택(Candle, Line)</td></tr><tr><td><code>Intervals</code></td><td><p>데이터가 집계되는 시간 단위</p><ul><li><code>CandleChart.INTERVALS_MONTH</code> — 월봉</li><li><code>CandleChart.INTERVALS_WEEK</code> — 주봉</li><li><code>CandleChart.INTERVALS_DAY</code> — 일봉</li><li><code>CandleChart.INTERVALS_MINUTE</code> — 분봉</li><li><code>CandleChart.INTERVALS_TICK</code> — 틱 차트 (거래 단위)</li></ul><p></p><ul><li>ex) candleChart.setIntervals(CandleChart.INTERVALS_DAY); // 일봉 차트</li></ul></td></tr><tr><td><code>Indicator</code></td><td><p>차트 하단에 보조 지표 표시</p><ul><li><code>CandleChart.INDICATOR_VOLUME</code> — 거래량</li><li><code>CandleChart.INDICATOR_OBV</code> — OBV</li><li><code>CandleChart.INDICATOR_MACD</code> — MACD</li><li><code>CandleChart.INDICATOR_SLOW</code> — Slow Stochastic</li><li><code>CandleChart.INDICATOR_FAST</code> — Fast Stochastic</li><li><code>CandleChart.INDICATOR_DISPARITY</code> — 이격도</li><li><code>CandleChart.INDICATOR_RSI</code> — RSI</li><li><code>CandleChart.INDICATOR_EMPTY</code> — 보조 지표 없음</li></ul><p></p><ul><li>ex) candleChart.setIndicator(CandleChart.INDICATOR_MACD); // MACD 보조지표 표시</li></ul></td></tr><tr><td><code>updateRefVal</code></td><td><p><strong>실시간 데이터 갱신 주기</strong>를 설정하는 값</p><ul><li>단위는 밀리초(ms)</li></ul><ul><li>예를 들어 <code>1000</code>을 넣으면 <strong>1초마다 데이터 갱신</strong>을 의미.</li><li><code>Intervals</code>가 <code>Minute</code>나 <code>Tick</code>일 때만 유효.</li></ul></td></tr></tbody></table>



**Mode**

* Candle

<figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 160032.png" alt=""><figcaption></figcaption></figure>

* Line

<figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 160119.png" alt=""><figcaption></figcaption></figure>



**Intervals**

* Month

<figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 160032 (1).png" alt=""><figcaption></figcaption></figure>

* Week

<figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 160218.png" alt=""><figcaption></figcaption></figure>

* Day

<figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 160305.png" alt=""><figcaption></figcaption></figure>

* Minute

<figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 160346.png" alt=""><figcaption></figcaption></figure>

* Tick

<figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 160403.png" alt=""><figcaption></figcaption></figure>



**Indicator**

* Volume

<figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 160519.png" alt=""><figcaption></figcaption></figure>

* OBV

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* MACD

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* Slow

<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* Fast

<figure><img src="../../.gitbook/assets/image (5) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* Disparity

<figure><img src="../../.gitbook/assets/image (6) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* RSI

<figure><img src="../../.gitbook/assets/image (7) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* EMPTY

<figure><img src="../../.gitbook/assets/image (8) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>



**Color**

<table data-header-hidden><thead><tr><th width="361"></th><th></th></tr></thead><tbody><tr><td><strong>이름</strong></td><td><strong>설명</strong></td></tr><tr><td><code>Text</code></td><td>차트 내 일반 텍스트 색상 (날짜, 가격 등)</td></tr><tr><td><code>Up</code></td><td>상승 봉의 색상</td></tr><tr><td><code>Divide Line</code></td><td>차트 영역을 구분하는 선 색상</td></tr><tr><td><code>Down</code></td><td>하락 봉의 색상</td></tr><tr><td><code>Longtab Line</code></td><td>롱탭(혹은 마우스 오버) 시 나타나는 세로/가로 선 색상</td></tr><tr><td><code>Dot</code></td><td>배경의 점선 라인 (격자) 색상</td></tr><tr><td><code>LineMode Line</code></td><td>라인 차트 모드일 때 라인 색상</td></tr><tr><td><code>Volume</code></td><td>거래량 막대 색상</td></tr></tbody></table>

**Current Price Color**

<table data-header-hidden><thead><tr><th width="361"></th><th></th></tr></thead><tbody><tr><td><strong>이름</strong></td><td><strong>설명</strong></td></tr><tr><td><code>Up Bg</code></td><td>상승 상태의 현재가 배경색</td></tr><tr><td><code>Up Text</code></td><td>상승 상태의 현재가 텍스트 색</td></tr><tr><td><code>Down Bg</code></td><td>하락 상태의 현재가 배경색</td></tr><tr><td><code>Down Text</code></td><td>하락 상태의 현재가 텍스트 색</td></tr></tbody></table>

**Option**

<table data-header-hidden><thead><tr><th width="361"></th><th></th></tr></thead><tbody><tr><td><strong>이름</strong></td><td><strong>설명</strong></td></tr><tr><td><code>Touch Event</code></td><td>터치 이벤트 활성화</td></tr></tbody></table>



#### Example

**1. 프로젝트 생성**

* 프로젝트 트리뷰에서 Source > MainView.lay 파일을 클릭
* MainView의 레이아웃 파일이 오픈되면 컴포넌트 리스트에서 CandleChart 컴포넌트를 선택하고 드래그하여 레이아웃에 배치
* Class에서 ID를 CandleChart 로 입력

**2. 데이터 설정**

* 먼저 MainView.js 파일을 오픈
* 상단의 파일탭에서 MainView.lay 탭을 더블 클릭하거나 우측의 프로젝트 트리에서 MainView.js 파일을 더블 클릭
* 모든 화면뷰는 onInitDone() 함수가 존재하며 이 함수는 화면이 생성될 때 딱 한번 실행
* onInitDone() 함수에서 레이블의 텍스트 내용을 아래와 같이 코드를 입력

```javascript
onInitDone() {
    super.onInitDone();

    // CandleChart 생성
    // 화면에 배치된 CandleChart 컴포넌트 찾기
    const candleChart = this.candleChart;

    // 차트 옵션 설정
    candleChart.setMode(CandleChart.MODE_CANDLE);             // 캔들 차트
    candleChart.setIntervals(CandleChart.INTERVALS_DAY);      // 일봉 기준
    candleChart.setIndicator(CandleChart.INDICATOR_VOLUME);   // 거래량 보조지표
    candleChart.setMAInfo([5, 20, 60]);                        // 이동평균선 설정

    // 데이터 정의
    const data = [
        [20140417,1376000,1380000,1368000,1372000,54664,1371400],
        [20140416,1370000,1392000,1363000,1380000,186171,1373000],
        [20140415,1386000,1387000,1369000,1370000,219396,1371200],
        [20140414,1365000,1386000,1365000,1370000,211720,1376000],
        [20140411,1362000,1368000,1359000,1365000,213187,1381400],
        [20140410,1369000,1380000,1360000,1380000,199984,1384400],
        [20140409,1394000,1395000,1364000,1371000,321232,1386400],
        [20140408,1387000,1399000,1375000,1394000,212164,1383600],
        [20140407,1397000,1397000,1374000,1397000,215235,1372600],
        [20140404,1377000,1397000,1377000,1380000,368007,1361800],
        [20140403,1351000,1395000,1351000,1390000,381976,1352800],
        [20140402,1350000,1357000,1343000,1357000,262001,1341400],
        [20140401,1345000,1345000,1331000,1339000,221620,1327000],
        [20140331,1345000,1345000,1322000,1343000,265197,1308600],
        [20140328,1320000,1338000,1320000,1335000,212974,1294600],
        [20140327,1290000,1333000,1285000,1333000,417557,1282200],
        [20140326,1269000,1290000,1248000,1285000,348894,1268000],
        [20140325,1269000,1270000,1241000,1247000,272500,1264800],
        [20140324,1260000,1274000,1259000,1273000,141478,1271000],
        [20140321,1269000,1273000,1262000,1273000,166426,1269600],
        [20140320,1270000,1272000,1262000,1262000,118788,1270000],
        [20140319,1280000,1285000,1268000,1269000,152771,1275600],
        [20140318,1270000,1283000,1266000,1278000,220912,1280600],
        [20140317,1275000,1276000,1258000,1266000,176400,1289400],
        [20140314,1270000,1285000,1270000,1275000,216736,1300200],
        [20140313,1294000,1313000,1290000,1290000,235004,1313000],
        [20140312,1320000,1320000,1293000,1294000,251585,1320200],
        [20140311,1320000,1327000,1309000,1322000,181596,1327400],
        [20140310,1320000,1330000,1317000,1320000,173152,1326000],
        [20140307,1339000,1339000,1329000,1339000,150973,1327000],
        [20140306,1329000,1329000,1310000,1326000,172335,1329000],
        [20140305,1335000,1341000,1330000,1330000,149830,1332000],
        [20140304,1320000,1329000,1315000,1315000,158003,1334400],
        [20140303,1336000,1340000,1321000,1325000,242083,1338200],
        [20140228,1337000,1349000,1332000,1349000,284647,1338800],
        [20140227,1335000,1342000,1330000,1341000,157827,1335000],
        [20140226,1337000,1343000,1325000,1342000,258361,1324000],
        [20140225,1332000,1340000,1326000,1334000,175706,1313600],
        [20140224,1334000,1345000,1321000,1328000,148501,1305800],
        [20140221,1333000,1333000,1300000,1330000,286924,1297200],
        [20140220,1290000,1296000,1281000,1286000,190866,1291400]
    ];

    candleChart.setData(data);
}
```

**3. 프로젝트 실행**

* 설정한 데이터에 맞춰 차트가 정상적으로 렌더링
* 사용자 인터랙션(확대/축소 및 스크롤) 기능 정상적으로 작동 확인

<figure><img src="../../.gitbook/assets/화면 녹화 중 2025-07-02 162357.gif" alt=""><figcaption></figcaption></figure>

**4. 코드로** CandleChart **생성**

* 먼저 MainView.js 파일을 오픈
* onInitDone() 함수에서 아래와 같이 코드를 입력

```javascript
onInitDone() {
    super.onInitDone();

    // CandleChart 생성
    const candleChart = new CandleChart();
    candleChart.init();

    // 차트 옵션 설정
    candleChart.setMode(CandleChart.MODE_CANDLE);             // 캔들 차트
    candleChart.setIntervals(CandleChart.INTERVALS_DAY);      // 일봉 기준
    candleChart.setIndicator(CandleChart.INDICATOR_VOLUME);   // 거래량 보조지표
    candleChart.setMAInfo([3, 4, 17]);                        // 이동평균선 설정

    // 화면에 추가
    this.addComponent(candleChart);
    candleChart.setSize(800, 600);    // 크기 설정
    candleChart.setPos(100, 100);     // 위치 설정

    // 데이터 정의
    const data = [
        [20140417,1376000,1380000,1368000,1372000,54664,1371400],
        [20140416,1370000,1392000,1363000,1380000,186171,1373000],
        [20140415,1386000,1387000,1369000,1370000,219396,1371200],
        [20140414,1365000,1386000,1365000,1370000,211720,1376000],
        [20140411,1362000,1368000,1359000,1365000,213187,1381400],
        [20140410,1369000,1380000,1360000,1380000,199984,1384400],
        [20140409,1394000,1395000,1364000,1371000,321232,1386400],
        [20140408,1387000,1399000,1375000,1394000,212164,1383600],
        [20140407,1397000,1397000,1374000,1397000,215235,1372600],
        [20140404,1377000,1397000,1377000,1380000,368007,1361800],
        [20140403,1351000,1395000,1351000,1390000,381976,1352800],
        [20140402,1350000,1357000,1343000,1357000,262001,1341400],
        [20140401,1345000,1345000,1331000,1339000,221620,1327000],
        [20140331,1345000,1345000,1322000,1343000,265197,1308600],
        [20140328,1320000,1338000,1320000,1335000,212974,1294600],
        [20140327,1290000,1333000,1285000,1333000,417557,1282200],
        [20140326,1269000,1290000,1248000,1285000,348894,1268000],
        [20140325,1269000,1270000,1241000,1247000,272500,1264800],
        [20140324,1260000,1274000,1259000,1273000,141478,1271000],
        [20140321,1269000,1273000,1262000,1273000,166426,1269600],
        [20140320,1270000,1272000,1262000,1262000,118788,1270000],
        [20140319,1280000,1285000,1268000,1269000,152771,1275600],
        [20140318,1270000,1283000,1266000,1278000,220912,1280600],
        [20140317,1275000,1276000,1258000,1266000,176400,1289400],
        [20140314,1270000,1285000,1270000,1275000,216736,1300200],
        [20140313,1294000,1313000,1290000,1290000,235004,1313000],
        [20140312,1320000,1320000,1293000,1294000,251585,1320200],
        [20140311,1320000,1327000,1309000,1322000,181596,1327400],
        [20140310,1320000,1330000,1317000,1320000,173152,1326000],
        [20140307,1339000,1339000,1329000,1339000,150973,1327000],
        [20140306,1329000,1329000,1310000,1326000,172335,1329000],
        [20140305,1335000,1341000,1330000,1330000,149830,1332000],
        [20140304,1320000,1329000,1315000,1315000,158003,1334400],
        [20140303,1336000,1340000,1321000,1325000,242083,1338200],
        [20140228,1337000,1349000,1332000,1349000,284647,1338800],
        [20140227,1335000,1342000,1330000,1341000,157827,1335000],
        [20140226,1337000,1343000,1325000,1342000,258361,1324000],
        [20140225,1332000,1340000,1326000,1334000,175706,1313600],
        [20140224,1334000,1345000,1321000,1328000,148501,1305800],
        [20140221,1333000,1333000,1300000,1330000,286924,1297200],
        [20140220,1290000,1296000,1281000,1286000,190866,1291400]
    ];

    candleChart.setData(data);
}

```

<figure><img src="../../.gitbook/assets/화면 녹화 중 2025-07-02 162525.gif" alt=""><figcaption></figcaption></figure>

<mark style="color:red;">**Build 에러 발생 시**</mark>

1. _**프로젝트 트리뷰에서 Framework > afc 우클릭 > Default Load Settings.. > Component > ADataMask.js 체크**_
2. _**프로젝트 트리뷰에서 Framework > stock 우클릭 > Default Load Settings.. > Component > CandleChart.js + CandleChartEvent.js 체크**_

<div><figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 142053.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 142215.png" alt=""><figcaption></figcaption></figure></div>
