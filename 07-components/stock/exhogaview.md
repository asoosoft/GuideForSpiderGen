---
description: ket API를 통해 종목의 매도/매수 호가 데이터를 실시간으로 받아 사용자에게 직관적으로 보여줍니다.
---

# ExHogaView

주식 및 가상자산 거래 시스템에서 실시간 호가 정보를 시각적으로 표시하는 컴포넌트.

\
업비트와 같은 거래소의 REST API 및 WebSocket API를 통해 종목의 매도/매수 호가 데이터를 실시간으로 받아 사용자에게 직관적으로 보여줌.

### Appearance

* 공통 Appearance는\
  **6. Global Properties** 속성을 참고.

### Attribute

| Data          | 설명 |
| ------------- | -- |
| Current Price |    |
| Base Price    |    |
| Bottom Row    |    |
| Quote Count   |    |

| Price Color | 설명 |
| ----------- | -- |
| Up          |    |
| Down        |    |
| Steady      |    |

| Bar Style    | 설명 |
| ------------ | -- |
| Size         |    |
| Ask Position |    |
| Bid Position |    |
| Ask Color    |    |
| Bid Color    |    |

| Option         | 설명 |
| -------------- | -- |
| Hide Header    |    |
| Single Select  |    |
| Fullrow Select |    |
| Selectable     |    |
| Flexable Row   |    |

### Example

#### 1. 프로젝트 생성

* 프로젝트 트리뷰에서 `Source > MainView.lay` 파일을 클릭.
* MainView의 레이아웃 파일이 오픈되면 컴포넌트 리스트에서 **EXHogaView** 컴포넌트를 선택하고 드래그하여 레이아웃에 배치.
* Class에서 ID를 **hogaView**로 입력.

***

#### 2. 데이터 설정

MainView.js 파일을 열고 onInitDone() 함수에 아래와 같이 작성.

```javascript
onInitDone() {
    super.onInitDone();

    const hogaView = new EXHogaView();
    hogaView.createElement();
    this.addComponent(hogaView);
    hogaView.init();

    // 표시할 호가 단계 수 설정
    hogaView.setShowCount(10);

    // 자동 리사이즈 여부 설정
    hogaView.setAutoResizeChildren(true);

    // 위치 설정
    hogaView.setPos(100, 100);

    // 크기 설정 (필요시)
    hogaView.setSize(400, 500);
}
```

***

#### 3. 프로젝트 실행

* 설정한 호가 데이터에 따라 실시간으로 호가 정보가 표시.
* 업비트의 WebSocket API와 연동하여 실시간으로 매도/매수 잔량이 업데이트.
* 중앙 정렬 기능과 자동 크기 조절 기능이 적용.

***

#### 4. 코드로 EXHogaView 생성

MainView.js 파일 내에서 아래와 같이 작성.

```javascript
onInitDone() {
    super.onInitDone();

    const exHogaView = new EXHogaView();
    exHogaView.createElement();
    exHogaView.init();

    // 호가 단계 설정
    exHogaView.setShowCount(15);

    // 자동 리사이즈 비활성화
    exHogaView.setAutoResizeChildren(false);

    // 위치 및 크기 설정
    exHogaView.setPos(50, 50);
    exHogaView.setSize(450, 600);

    this.addComponent(exHogaView);
}
```

***
