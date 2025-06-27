# ExTriangle

<figure><img src="../../.gitbook/assets/스크린샷 2025-06-27 164338.png" alt=""><figcaption></figcaption></figure>



**ExTriangle**은 업비트의 REST API와 WebSocket을 활용하여 종목 데이터, 캔들, 호가 등 다양한 데이터를 실시간으로 수집 및 표시하는 프레임워크입니다.

이 매뉴얼은 주요 클래스인 `SpiderWTSApp`, `MainView`, `TestView`의 구조와 동작을 기반으로 작성되었습니다.

***

### SpiderWTSApp

#### Role

* 애플리케이션 초기화
* 업비트 REST API 및 WebSocket 서버 연결
* 종목 정보 관리
* 메인 페이지 로드 및 오류 처리
* 서버 연결 상태 관리 및 재접속 처리

***

### MainView

#### Role

* 초기 종목 데이터 조회 및 로드
* 화면 UI 구성 및 위젯 초기화
* 다크 모드, 더미 데이터(Speed Booster) 모드 지원
* 사용자 인터랙션에 따라 위젯 동적 생성 및 제거

#### Features

* 종목 리스트 조회 및 현재 종목 선택
* 주요 거래 위젯 로드 (ItemInfo, ItemList, Chart, Hoga, Order, Trades)
* 다크 모드 토글
* 더미 데이터 모드 지원
* Trades, ItemList를 다중 프레임으로 띄우기 및 종료 기능

***

### TestView

#### Role

* REST API 테스트 기능 제공
* 종목 조회, 캔들 조회, 체결 조회, 호가 조회, 현재가 조회 등의 기능 수행
* 데이터 확인 및 콘솔 로그 출력용 뷰
* 추가 테스트 기능 확장 가능

***

### Status & Mode

#### Speed Booster (Dummy Data Mode)

* 서버로부터 실제 데이터를 수신하지 않고 가상의 더미 데이터를 생성하여 UI 동작을 테스트합니다.
* TradesView와 ItemListView에서 애니메이션 프레임 적용 가능
* 다중 창 모드와 연동 가능

#### Night Mode (다크 모드)

* 화면 테마를 어두운 모드로 전환합니다.
* `body` 태그에 `dark` 클래스가 추가되어 동작합니다.

***

### File & Class Structure

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

### Error Handling

* `onError()` 메서드를 통해 전역 오류를 감지합니다.
* 오류 발생 시 콘솔 로그 출력 및 사용자에게 오류 표시
* 네트워크 오류 발생 시 설정된 최대 재접속 횟수까지 자동 재연결 시도

***

### Initialization & Execution Flow

1. **SpiderWTSApp.onReady()**\
   → REST 서버와 WebSocket 서버 연결 시도
2. **connectSocketServer()**\
   → 서버 연결 성공 시 **displayMainPage()** 호출
3. **MainView**\
   → 종목 리스트 조회 후 초기 종목 설정 및 주요 거래 위젯 로드
4. **실시간 데이터 반영**\
   → WebSocket을 통한 실시간 데이터 수신 및 UI 업데이트

