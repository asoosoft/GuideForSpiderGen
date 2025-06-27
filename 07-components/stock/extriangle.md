# ExTriangle

ExTriangle은 업비트의 REST API와 WebSocket을 활용하여 종목 데이터, 캔들, 호가 등 다양한 데이터를 실시간으로 수집 및 표시하는 프레임워크입니다. 본 메뉴얼은 `SpiderWTSApp`, `MainView`, `TestView`의 코드 구조를 기반으로 작성되었습니다.

***

## SpiderWTSApp

### 역할

* 어플리케이션의 초기화, REST 서버 및 WebSocket 서버 연결
* 종목 정보 관리
* 메인 페이지 로드 및 오류 처리

### 주요 메서드

#### onReady()

* 앱 초기화
* REST 서버와 WebSocket 서버 연결 시도

#### initRestServer()

* 업비트 REST 서버 초기화
* `UbHttpIO`를 이용하여 통신

#### connectSocketServer()

* WebSocket 서버 연결
* 연결 상태에 따른 콜백 처리

#### setItemInfo(marketCode)

* 현재 선택한 종목 정보 설정
* 종목 코드가 다르면 `widgetManager.updateMarket()` 실행

#### getItemInfo(key)

* 현재 선택한 종목 정보 반환
* key가 없으면 전체 itemInfo 반환

#### onConnected(success)

* 서버 연결 성공/실패에 따른 동작
* 재접속 로직 포함

#### displayMainPage()

* 메인 페이지 레이아웃 로드
* `WidgetManager` 초기화 및 위젯 로드

#### onError(message, url, lineNumber, colNumber, error)

* 오류 발생 시 로그 출력 및 처리

***

## MainView

### 역할

* 초기 종목 데이터 로드
* 위젯 구성 및 화면 초기화
* 다크 모드, 더미 데이터 모드 지원

### 주요 메서드

#### init()

* UI 초기화
* 10초 후 상태 표시 변경 (데이터 수집중 → Speed Booster)
* 종목 리스트 조회 및 위젯 로드

#### send\_UBREST01()

* 종목 리스트 조회 API
* `UBREST01` 호출
* 결과는 `OutBlock1`

#### loadWidget()

* 주요 위젯 로드
  * ItemInfo
  * ItemList
  * Chart
  * Hoga
  * Order
  * Trades

#### openItemListAsFrame()

* `ItemList` 위젯을 별도의 다중 프레임으로 생성

#### openTradesAsFrame()

* `Trades` 위젯을 별도의 다중 프레임으로 생성

#### closeTestFrames()

* 다중 프레임으로 띄운 ItemList/Trades 뷰를 닫음

#### onAModeChange(comp)

* 다크 모드 토글
* body에 `dark` 클래스 추가 및 제거

#### enableAniFrame(viewId, enable)

* 특정 뷰에 대해 애니메이션 프레임 켜기/끄기

#### onDummyChange(comp)

* 더미 데이터 모드 토글
* Trades, ItemList 뷰에 애니메이션 프레임 적용
* 다중창 생성 및 닫기

***

## TestView

### 역할

* 각종 REST API 테스트
* 데이터 확인 및 로그 출력

### 주요 메서드

#### onAButton1Click()

* 종목 조회
* `UBREST01` 호출

#### onAButton2Click()

* 캔들 조회
* `UBREST02` 호출
* 인자:
  * type: 1 (기본)
  * market: 'KRW-BTC'

#### onAButton3Click()

* 체결 조회
* `UBREST03` 호출
* 인자:
  * market: 'KRW-BTC'
  * count: 50

#### onAButton4Click()

* 호가 조회
* `UBREST04` 호출
* 인자:
  * market: 'KRW-BTC'

#### onAButton5Click()

* 현재가 조회
* `UBREST05` 호출
* 인자:
  * market: 'KRW-BTC'

#### onAButton6Click() \~ onAButton8Click()

* 예약된 추가 기능 (미구현)

***

## API 명세

| API 이름   | 설명     | 입력값 예시        | 반환 블록     |
| -------- | ------ | ------------- | --------- |
| UBREST01 | 종목 조회  | 없음            | OutBlock1 |
| UBREST02 | 캔들 조회  | type, market  | OutBlock1 |
| UBREST03 | 체결 조회  | market, count | OutBlock1 |
| UBREST04 | 호가 조회  | market        | OutBlock1 |
| UBREST05 | 현재가 조회 | market        | OutBlock1 |

***

## 상태 및 모드

### Speed Booster (더미 데이터 모드)

* 수신 데이터 없이 가상의 데이터를 생성하여 화면을 테스트할 수 있음
* TradesView, ItemListView에 애니메이션 적용
* 다중 창 모드와 연동 가능

### 다크 모드 (Night Mode)

* 화면을 어두운 테마로 전환
* CSS class인 `dark`를 body에 적용하여 동작

***

## 파일 및 클래스 구조

```
/Source/
    Define.js
    Widget/
        WidgetManager.js
        ItemInfo/
        ItemList/
        Chart/
        Hoga/
        Order/
        Trades/
    MainView.lay
    MainView.js
    TestView.js

/Framework/
    afc/
        component/
            AIndicator.js
    stock/
        component/
            EXItemView.js
```

***

## 오류 처리

* `onError()` 메서드를 통해 전역 오류를 캐치하고 콘솔에 로그 출력
* 네트워크 오류 발생 시 재접속 시도 (최대 시도 횟수 설정 가능)

***

## 초기화 및 실행 순서

1. `SpiderWTSApp.onReady()`
   * REST, WebSocket 서버 연결
2. `connectSocketServer()`에서 연결 성공 시 `displayMainPage()` 호출
3. `MainView`에서 종목 조회 후 위젯 로드
4. 실시간 데이터 반영 및 UI 업데이트
