# ExHogaGrid

`ExHogaGrid`는 실시간으로 매수/매도 호가 데이터를 표시하는 그리드 컴포넌트입니다. 업비트 WebSocket 데이터를 기반으로 시장의 호가 상태를 시각화합니다.

***

## 기능

* 실시간 호가 데이터 수신
* 매도/매수 구분 시각화
* 가격 및 잔량 표시
* 주문 단위와 가격 스케일링 지원
* 사용자 인터랙션 지원 (클릭 시 주문 가능)

***

## 주요 구성 요소

| 항목    | 설명                        |
| ----- | ------------------------- |
| 매도 호가 | 상단 영역, 매도 가격 및 잔량         |
| 현재가   | 중앙 영역, 현재 거래가격            |
| 매수 호가 | 하단 영역, 매수 가격 및 잔량         |
| 가격 컬럼 | 각 호가의 가격 표시               |
| 잔량 컬럼 | 각 호가의 잔량 표시 (바 그래프 포함 가능) |

***

## 클래스 메서드

### 초기화 관련

#### init(context, evtListener)

* 그리드 초기화
* 이벤트 리스너 및 데이터 바인딩 설정

#### setMarket(market)

* 현재 조회할 마켓 설정
* 예: `KRW-BTC`

### 데이터 관련

#### subscribe()

* 현재 설정된 market에 대해 WebSocket 실시간 데이터 구독 시작
* 연결되는 데이터 타입: `orderbook`

#### unsubscribe()

* 현재 market의 WebSocket 구독 해제

#### updateOrderbook(orderbookData)

* 수신된 orderbook 데이터를 그리드에 업데이트
* 가격과 잔량 기준으로 상단 매도/하단 매수 자동 정렬

### UI 및 스타일

#### applyTheme(theme)

* 테마 적용 (Light/Dark 모드 지원)

#### highlightPrice(price)

* 특정 가격 하이라이트 (예: 선택된 주문가)

#### reset()

* 그리드 데이터 초기화

### 유틸리티 메서드

#### getSelectedPrice()

* 현재 선택된 가격 반환

#### setDepthCount(count)

* 호가 레벨 설정 (기본 15레벨)
* 예: 5레벨, 10레벨, 15레벨

***

## 데이터 구조

### WebSocket orderbook 데이터 예시

```json
{
  "type": "orderbook",
  "code": "KRW-BTC",
  "orderbook_units": [
    {
      "ask_price": 45600000,
      "bid_price": 45550000,
      "ask_size": 1.25,
      "bid_size": 0.85
    }
  ],
  "timestamp": 1656789123456
}
```

| 필드         | 설명       |
| ---------- | -------- |
| ask\_price | 매도 호가 가격 |
| bid\_price | 매수 호가 가격 |
| ask\_size  | 매도 잔량    |
| bid\_size  | 매수 잔량    |

***

## UI 구조 예시

```
┌───────────────────────────────┐
│          매도 호가 (상단)       │
│-------------------------------│
│   가격   |   매도 잔량          │
│   가격   |   매도 잔량          │
│   가격   |   매도 잔량          │
├───────────────────────────────┤
│          현재가                │
├───────────────────────────────┤
│          매수 호가 (하단)       │
│-------------------------------│
│   가격   |   매수 잔량          │
│   가격   |   매수 잔량          │
│   가격   |   매수 잔량          │
└───────────────────────────────┘
```

***

## 이벤트 및 콜백

| 이벤트 이름                | 설명                     |
| --------------------- | ---------------------- |
| onHogaSelected(price) | 호가 가격 선택 시 호출          |
| onOrderbookUpdate()   | 새로운 orderbook 데이터 수신 시 |

***

## 설정 옵션

| 옵션               | 설명               | 기본값  |
| ---------------- | ---------------- | ---- |
| depthCount       | 호가 레벨 수          | 15   |
| enableHighlight  | 가격 하이라이트 사용 여부   | true |
| showVolumeBar    | 잔량 바 그래프 표시 여부   | true |
| autoScrollCenter | 현재가를 중앙에 고정할지 여부 | true |

***

## 사용 예제

```javascript
const hogaGrid = new ExHogaGrid();

hogaGrid.setMarket('KRW-BTC');
hogaGrid.subscribe();

// 특정 가격 선택 시
hogaGrid.highlightPrice(45500000);

// 현재 선택된 가격 얻기
const price = hogaGrid.getSelectedPrice();
console.log('선택된 가격:', price);
```

***

## 오류 처리 및 예외

* WebSocket 연결 실패 시 자동 재접속 시도
* 수신 데이터가 비정상인 경우 `reset()` 호출
* `onError()` 메서드 내부에서 콘솔 및 사용자 알림

***

## 초기화 및 종료 순서

1. `setMarket()` 호출
2. `subscribe()`로 WebSocket 연결 및 데이터 수신
3. 종료 시 `unsubscribe()`로 연결 해제
