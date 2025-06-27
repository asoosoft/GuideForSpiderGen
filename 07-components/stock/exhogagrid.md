# ExHogaGrid

```markdown
# ExHogaGrid 사용 가이드

## 목차
- 프로젝트 구조
- 클래스 개요
- 주요 메서드 및 기능
- 데이터 처리 방식
- 주요 이벤트
- 예제 코드
- 결론

## 프로젝트 구조

```

/Source/Widget/Hoga/\
└── ExHogaGrid.js\
└── HogaView.lay

````

## 클래스 개요

### ExHogaGrid (AComponent 상속)

- 호가창 전용 그리드 컴포넌트
- 실시간 호가 데이터 표시
- WebSocket 실시간 수신 지원
- 대기 매수/매도 잔량, 현재가 강조 표시

## 주요 메서드 및 기능

### 초기화 및 설정

```javascript
initComp()
````

* 컴포넌트 초기화
* 내부 구조 및 UI 세팅

```javascript
setMarket(market)
```

* 현재 종목 설정
* 예) 'KRW-BTC'

```javascript
setDepth(depth)
```

* 호가 단수 설정
* 기본값 15호가

#### 데이터 핸들링

```javascript
setData(hogaData)
```

* 외부에서 수신한 호가 데이터 적용

```javascript
updateHoga(hogaData)
```

* 실시간으로 변경된 데이터 반영

```javascript
clearData()
```

* 현재 데이터 초기화

#### 시각적 효과

```javascript
highlightPrice(price)
```

* 특정 가격 강조 표시 (현재가 등)

```javascript
setTheme(darkMode)
```

* 다크모드 적용 여부 설정

### 데이터 처리 방식

#### 데이터 구조 예시 (호가 데이터)

```json
{
  "market": "KRW-BTC",
  "asks": [
    {"price": 50000000, "size": 0.5},
    ...
  ],
  "bids": [
    {"price": 49900000, "size": 0.7},
    ...
  ],
  "trade_price": 49950000
}
```

* asks : 매도호가 (상단)
* bids : 매수호가 (하단)
* trade\_price : 현재가

### 주요 이벤트

| 이벤트           | 설명              |
| ------------- | --------------- |
| onHogaClick   | 사용자가 특정 호가 선택 시 |
| onDataUpdated | 호가 데이터 갱신 완료 시  |

#### 이벤트 등록 예시

```javascript
this.hogaGrid.setEventListener({
    onHogaClick: (price, size, type) => {
        console.log('Clicked Price:', price);
    },
    onDataUpdated: () => {
        console.log('Hoga Updated');
    }
});
```

### 예제 코드

```javascript
this.hogaGrid.setMarket('KRW-BTC');
this.hogaGrid.setDepth(15);

theApp.qmReal.setRealCallback('UBHOGA', (queryData) => {
    const hogaData = queryData.getBlockData('OutBlock1')[0];
    this.hogaGrid.updateHoga(hogaData);
});
```

* setMarket() : 종목 지정
* setDepth() : 호가 단수 지정
* setRealCallback() : 실시간 데이터 수신
* updateHoga() : 수신 데이터 UI 반영

### 결론

* ExHogaGrid는 실시간 호가 데이터 시각화에 최적화된 컴포넌트
* WebSocket 연동으로 빠른 데이터 반영
* 클릭 이벤트, 테마 지원, 데이터 클리어 기능 포함
* 다중 종목, 다중 프레임에도 활용 가능
