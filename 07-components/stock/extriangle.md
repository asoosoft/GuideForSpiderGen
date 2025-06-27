# ExTriangle

```markdown
# ExTriangle 사용 가이드

## 목차
- 프로젝트 구조
- 앱 구조 및 라이프사이클
- 서버 연결 (REST & WebSocket)
- MainView 동작
- TestView 예제
- 다크모드 및 더미 데이터 모드
- 위젯 시스템

## 프로젝트 구조

```

/Framework\
└── afc\
└── stock\
/Source\
└── Define.js\
└── MainView.lay\
└── Widget\
/Source/Widget\
└── ItemInfo/\
└── ItemList/\
└── Chart/\
└── Hoga/\
└── Order/\
└── Trades/

````

## 앱 구조 및 라이프사이클

### SpiderWTSApp (AApplication 상속)

### 초기화 메서드
- onReady() : 앱 시작 시 서버 연결 및 설정
- initRestServer() : REST 서버 초기화
- connectSocketServer() : WebSocket 서버 연결

### 종목 관리
- setItemInfo(marketCode) : 현재 종목 설정
- getItemInfo(key) : 현재 종목 정보 반환

### 페이지 로딩
- displayMainPage() : 메인 페이지 로드

### 연결 상태 콜백
- onConnected(success) : 연결 성공/실패 처리
- 재연결 로직 포함 (최대 RE_CONNECT_CNT 만큼)

## 서버 연결 (REST & WebSocket)

### REST 서버 연결

```javascript
this.qmRest = new RestQueryManager('REST');
this.qmRest.setNetworkIo(new UbHttpIO(this.qmRest));
this.qmRest.startManager(Define.SERVER_ADDR_REST);
this.qmRest.setTimeout(Define.TIMEOUT_SEC);
````

* QueryManager를 통해 서버와 통신
* UBREST01, UBREST02 등 프로세스 이름으로 호출

#### WebSocket 연결

```javascript
this.qmReal = new RealQueryManager();
const nio = new UbWebsocketIO(this.qmReal, true);
nio.enableRetry(5);
this.qmReal.setNetworkIo(nio);
this.qmReal.startManager(Define.SERVER_ADDR_WEBSOCKET);
```

* 실시간 데이터 수신
* 연결 상태 감지 및 재시도 로직 포함

### MainView 동작

#### 주요 동작 흐름

* 종목 리스트 조회 (UBREST01)
* 위젯 로드
* 더미 데이터 모드 및 다크모드 지원

#### 종목 리스트 조회 예제

```javascript
send_UBREST01() {
    return new Promise((resolve, reject) => {
        theApp.qmRest.sendProcessByName('UBREST01', 'MainView', null,
            (queryData) => {
                const inBlock1 = queryData.getBlockData('InBlock1')[0];
                inBlock1['isDetails'] = true;
                queryData.printQueryData();
            },
            (queryData) => {
                const result = queryData.getBlockData('OutBlock1');
                resolve(result);
            }
        );
    });
}
```

#### 위젯 로드

```javascript
loadWidget() {
    theApp.widgetManager.loadWidget('ItemInfo', this.ItemInfoView);
    theApp.widgetManager.loadWidget('ItemList', this.ItemListView);
    theApp.widgetManager.loadWidget('Chart', this.ChartView);
    theApp.widgetManager.loadWidget('Hoga', this.HogaView);
    theApp.widgetManager.loadWidget('Order', this.OrderView);
    theApp.widgetManager.loadWidget('Trades', this.TradesView);
}
```

#### 프레임 방식으로 위젯 다중 오픈

```javascript
openTradesAsFrame() {
    let tot = 0;
    for (let i = 0; i < 3; i++) {
        for (let j = 0; j < 6; j++) {
            tot++;
            setTimeout(async () => {
                let frm = new AFrameWnd(i + '_' + j + '_');
                await frm.open("Source/Widget/Trades/TradesView.lay", null, i + '_' + j + '_', j * 300, i * 500 + 200, 300, 500);
                frm.maxBtn.hide();
                frm.minBtn.hide();
            }, 200 * tot);
        }
    }
}
```

### TestView 예제

#### REST API 호출 예시

**종목 조회 (UBREST01)**

```javascript
onAButton1Click() {
    theApp.qmRest.sendProcessByName('UBREST01', this.getContainerId(), null,
        (queryData) => {
            const inBlock1 = queryData.getBlockData('InBlock1')[0];
            inBlock1['isDetails'] = true;
            queryData.printQueryData();
        },
        (queryData) => {
            const OutBlock1 = queryData.getBlockData('OutBlock1');
            console.log(OutBlock1);
        }
    );
}
```

**캔들 조회 (UBREST02)**

```javascript
onAButton2Click() {
    theApp.qmRest.sendProcessByName('UBREST02', this.getContainerId(), null,
        (queryData) => {
            const inBlock1 = queryData.getBlockData('InBlock1')[0];
            inBlock1['type'] = 1;
            inBlock1['market'] = 'KRW-BTC';
            queryData.printQueryData();
        },
        (queryData) => {
            const OutBlock1 = queryData.getBlockData('OutBlock1');
            console.log(OutBlock1);
        }
    );
}
```

**체결 조회 (UBREST03)**

**호가 조회 (UBREST04)**

**주문 조회 (UBREST05)**

* 모두 위와 동일한 방식으로 사용 가능

### 다크모드 및 더미 데이터 모드

#### 다크모드 전환

```javascript
onAModeChange(comp) {
    const val = comp.getValue();
    if (val) {
        document.body.classList.add('dark');
        comp.addClass('switch_nightmode_off');
        comp.removeClass('switch_nightmode_on');
    } else {
        document.body.classList.remove('dark');
        comp.addClass('switch_nightmode_on');
        comp.removeClass('switch_nightmode_off');
    }
}
```

#### 더미 데이터 모드

```javascript
if (val) {
    theApp.qmReal.startDummyMode();
    this.enableAniFrame('TradesView', true);
    this.enableAniFrame('ItemListView', true);
} else {
    theApp.qmReal.stopDummyData();
    this.enableAniFrame('TradesView', false);
    this.enableAniFrame('ItemListView', false);
}
```

* onDummyChange() 호출 시 더미 데이터 시작/종료 가능

### 위젯 시스템

* 각 화면은 독립적인 위젯으로 구성됨
* WidgetManager를 통해 동적으로 로드 및 제어

```javascript
theApp.widgetManager.loadWidget('Chart', this.ChartView);
```

* 프레임 모드로 다중창 띄우기 가능
* 예) 호가창, 체결창을 여러 개 띄워서 모니터링 가능

### 결론

* REST와 WebSocket을 동시에 활용한 하이브리드 구조
* 위젯 단위 모듈화로 확장성 높음
* 다크모드, 더미 데이터, 다중 프레임 등 사용자 편의 기능 지원
