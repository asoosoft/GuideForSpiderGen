# ExCenterPivotView

아래는 주신 내용을 기반으로 메서드 설명을 제외하고 정리한 **ExCenterPivotView 매뉴얼**입니다.

***

## ExCenterPivotView Manual

### Overview

**ExCenterPivotView**는 트레이딩 화면의 중심에 위치하는 주요 UI 컴포넌트입니다. 현재 선택된 종목의 핵심 정보(현재가, 변동률, 거래량 등)를 표시하며, 타 위젯들과 상태를 연동하여 트레이딩 화면의 중심 역할을 합니다.

***

### Key Features

* 현재 선택 종목의 주요 정보 표시
* 실시간 시세 갱신
* 종목 변경 및 검색 기능 지원
* 타 위젯과의 상태 동기화
* 다크/라이트 테마 변경 지원

***

### UI Components

| Component        | Description          |
| ---------------- | -------------------- |
| Market Name      | 현재 선택된 종목명           |
| Current Price    | 현재 거래 가격             |
| Change Info      | 전일 대비 금액 및 등락률       |
| Opening Price    | 시가                   |
| High Price       | 고가                   |
| Low Price        | 저가                   |
| Volume           | 24시간 거래량             |
| Search Box       | 종목 검색 및 변경           |
| Status Indicator | 연결 상태 및 데이터 수신 상태 표시 |

***

### Data Structure

#### WebSocket Ticker Data Example

```json
{
  "type": "ticker",
  "code": "KRW-BTC",
  "trade_price": 45500000,
  "change_rate": 0.0215,
  "change_price": 960000,
  "signed_change_price": 960000,
  "acc_trade_volume_24h": 25.32,
  "high_price": 47000000,
  "low_price": 45000000,
  "opening_price": 45200000,
  "timestamp": 1656789123456
}
```

| Field                   | Description |
| ----------------------- | ----------- |
| code                    | 종목 코드       |
| trade\_price            | 현재가         |
| change\_rate            | 전일 대비 등락률   |
| change\_price           | 전일 대비 금액    |
| signed\_change\_price   | 절대 변화 금액    |
| acc\_trade\_volume\_24h | 24시간 거래량    |
| high\_price             | 고가          |
| low\_price              | 저가          |
| opening\_price          | 시가          |
| timestamp               | 데이터 수신 시간   |

***

### UI Layout Example

```
┌─────────────────────────────────────┐
│   [ 종목명 ]  KRW-BTC                │
│─────────────────────────────────────│
│   현재가      45,500,000 KRW         │
│   전일대비    +960,000 (+2.15%)      │
│─────────────────────────────────────│
│   시가   45,200,000                  │
│   고가   47,000,000                  │
│   저가   45,000,000                  │
│─────────────────────────────────────│
│   거래량  25.32 BTC                  │
│─────────────────────────────────────│
│   [ 검색 ] BTC 입력 시 자동완성      │
└─────────────────────────────────────┘
```

***

### Events & Callbacks

| Event Name              | Description              |
| ----------------------- | ------------------------ |
| onMarketChanged(market) | 종목이 변경될 때 호출             |
| onTickerUpdated(ticker) | 실시간 현재가 데이터 수신 시 호출      |
| onSummaryUpdated(data)  | 거래량, 시가, 고가, 저가 데이터 갱신 시 |

***

### Options & Settings

| Option        | Description            | Default |
| ------------- | ---------------------- | ------- |
| autoHighlight | 가격 변동 시 하이라이트 효과 적용 여부 | true    |
| enableSearch  | 종목 검색 기능 활성화 여부        | true    |
| showSummary   | 시가, 고가, 저가, 거래량 표시 여부  | true    |
| theme         | UI 테마 (light / dark)   | light   |

***

### Example Usage

```javascript
const pivot = new ExCenterPivotView();

pivot.setMarket('KRW-BTC');
pivot.subscribe();

// 다크 테마 적용
pivot.applyTheme('dark');

// 현재가 하이라이트 효과
pivot.highlight();
```

***

### Error Handling

* WebSocket 데이터 미수신 시 자동으로 `reset()` 처리 가능
* 종목 코드 오류 시 내부적으로 `onMarketChanged()` 재호출
* 네트워크 장애 발생 시 자동 재연결 로직 포함

***

### Initialization & Lifecycle

1. `setMarket()` 호출 → 종목 설정
2. `subscribe()` 호출 → 실시간 데이터 수신 시작
3. 종목 및 가격 변동에 따라 UI 자동 업데이트
4. 종료 시 `unsubscribe()` 호출로 데이터 수신 종
