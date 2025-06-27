# ExHogaGrid

**ExHogaGrid**는 실시간으로 매수/매도 호가 데이터를 시각화하는 그리드 컴포넌트입니다. 업비트 WebSocket 데이터를 기반으로 시장의 호가 상태를 직관적으로 보여주며, 매도/매수 잔량과 가격 변동을 실시간으로 표시합니다.

***

### Key Features

* 실시간 호가 데이터 수신
* 매도/매수 데이터 시각화
* 가격 및 잔량 표시
* 가격 스케일링 및 호가 레벨 조정 지원
* 특정 가격 선택 및 하이라이트 기능
* 사용자 인터랙션 지원 (클릭 시 주문 가능)

***

### UI Components

| Component      | Description            |
| -------------- | ---------------------- |
| Ask Price Grid | 상단 영역, 매도 가격과 매도 잔량 표시 |
| Current Price  | 현재 거래가 표시              |
| Bid Price Grid | 하단 영역, 매수 가격과 매수 잔량 표시 |
| Price Column   | 각 호가의 가격               |
| Volume Column  | 각 호가의 잔량 (바 그래프 가능)    |

***

### Data Structure

#### WebSocket Orderbook Data Example

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

| Field      | Description |
| ---------- | ----------- |
| ask\_price | 매도 호가 가격    |
| bid\_price | 매수 호가 가격    |
| ask\_size  | 매도 잔량       |
| bid\_size  | 매수 잔량       |
| timestamp  | 데이터 수신 시간   |

***

### UI Layout Example

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

### Events & Callbacks

| Event Name             | Description               |
| ---------------------- | ------------------------- |
| onPriceSelected(price) | 사용자가 특정 가격 선택 시 호출        |
| onOrderbookUpdated()   | 새로운 orderbook 데이터 수신 시 호출 |

***

### Options & Settings

| Option           | Description                | Default |
| ---------------- | -------------------------- | ------- |
| depthCount       | 표시할 호가 레벨 수 (예: 5, 10, 15) | 15      |
| enableHighlight  | 가격 하이라이트 기능 활성화 여부         | true    |
| showVolumeBar    | 잔량 바 그래프 표시 여부             | true    |
| autoScrollCenter | 현재가를 중앙에 고정하여 스크롤 여부       | true    |
| theme            | UI 테마 (Light / Dark)       | Light   |

***

### Example Usage

```javascript
const hogaGrid = new ExHogaGrid();

hogaGrid.setMarket('KRW-BTC');
hogaGrid.subscribe();

// 특정 가격 하이라이트
hogaGrid.highlightPrice(45500000);

// 현재 선택된 가격 가져오기
const price = hogaGrid.getSelectedPrice();
console.log('선택된 가격:', price);
```

***

### Error Handling

* WebSocket 연결 실패 시 자동으로 재접속 시도
* 수신 데이터가 비정상인 경우 내부적으로 `reset()` 처리
* `onError()` 메서드를 통해 콘솔 출력 및 사용자 알림 제공

***

### Initialization & Lifecycle

1. `setMarket()`로 조회할 종목 설정
2. `subscribe()` 호출 → WebSocket 연결 및 실시간 데이터 수신 시작
3. 실시간 데이터에 따라 UI 자동 갱신
4. 필요 시 `unsubscribe()` 호출로 연결 해제 및 종료 처리

