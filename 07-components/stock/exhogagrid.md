# ExHogaGrid

<figure><img src="../../.gitbook/assets/스크린샷 2025-06-27 164531.png" alt=""><figcaption></figcaption></figure>

호가 데이터를 배열 또는 객체 형태로 입력하여 매도/매수 호가를 시각화하는 그리드 컴포넌트.

***

### Appearance

공통 Appearance 는 [**6. Global Properties**](<../../Guide for SpiderGen/06  SpiderGen Editor/04  Properties Pane/02 Appearence.md>) 속성을 참고

### Attribute

EXHogaGrid 속성

<figure><img src="../../.gitbook/assets/스크린샷 2025-06-30 082052.png" alt=""><figcaption></figcaption></figure>

**Data**

<table data-header-hidden><thead><tr><th width="361"></th><th></th></tr></thead><tbody><tr><td><strong>이름</strong></td><td><strong>설명</strong></td></tr><tr><td><strong>속성</strong></td><td></td></tr><tr><td><code>Current Price</code></td><td>매핑된 쿼리파일의 현재값의 필드명을 입력</td></tr><tr><td><code>Base Price</code></td><td>매핑된 쿼리파일의 기본값의 필드명을 입력</td></tr><tr><td><code>Bottom Row</code></td><td>호가를 하단에 표현될 로우의 개수를 지정</td></tr><tr><td><code>Quote Count</code></td><td>호가의 단계 설정</td></tr><tr><td><strong>색상 속성</strong></td><td></td></tr><tr><td><code>Up</code></td><td>호가 상승색 설정</td></tr><tr><td><code>Down</code></td><td>호가 하락색 설정</td></tr><tr><td><code>Steady</code></td><td>호가 보합색 설정</td></tr><tr><td><strong>바 스타일</strong></td><td></td></tr><tr><td><code>Size</code></td><td>호가 잔량을 표현하는 바의 높이를 지정</td></tr><tr><td><code>Ask Position</code></td><td>매도 잔량바의 위치를 지정</td></tr><tr><td><code>Bid Position</code></td><td>매수 잔량바의 위치를 지정</td></tr><tr><td><code>Ask Color</code></td><td>매도 잔량바의 색을 지정</td></tr><tr><td><code>Bid Color</code></td><td>매수 잔량바의 색을 지정</td></tr><tr><td><strong>옵션</strong></td><td></td></tr><tr><td><code>Hide Header</code></td><td>헤더 숨김 여부 옵션</td></tr><tr><td><code>Single Select</code></td><td>Ctrl 키를 누르고 선택해도 하나만 선택되는 옵션</td></tr><tr><td><code>Fullrow Select</code></td><td>특정 셀을 클릭해도 그 행 전체가 선택되는 옵션</td></tr><tr><td><code>Selectable</code></td><td>선택 가능 여부 옵션 플래그</td></tr><tr><td><code>Flexable Row</code></td><td>TR의 높이를 TABLE 높이에 풀로 맞추는 옵션</td></tr></tbody></table>

### Example

**1. 프로젝트 생성**

* 프로젝트 트리뷰에서 Source > MainView.lay 파일을 클릭
* MainView의 레이아웃 파일이 오픈되면 컴포넌트 리스트에서 EXHogaGrid 컴포넌트를 선택하고 드래그하여 레이아웃에 배치
* Class 에서 ID를hogagrid로 입력



**2. 데이터 설정**

* 먼저 MainView.js 파일을 오픈
* 상단의 파일탭에서 MainView.lay 탭을 더블 클릭하거나 우측의 프로젝트 트리에서 MainView.js 파일을 더블 클릭
* 모든 화면뷰는 onInitDone() 함수가 존재하며 이 함수는 화면이 생성될 때 딱 한번 실행
* onInitDone() 함수에서 레이블의 텍스트 내용을 아래와 같이 코드를 입력

```javascript
onInitDone()
{

}
```

**3. 프로젝트 실행**

* 설정한 데이터에 맞춰서 각 가격과 거래량, 평균가, 현재가가 표시

**5. 코드로** EXHogaGrid **생성**

* 먼저 MainView.js 파일을 오픈
* onInitDone() 함수에서 아래와 같이 코드를 입력

```javascript
onInitDone() {
    super.onInitDone();

    const exHogaGrid = new EXHogaGrid();

    exHogaGrid.init();

    // 기준가 및 현재가 설정
    exHogaGrid.setBasePrice(3200);
    exHogaGrid.setCurrentPrice(3100);

    // 데이터 설정
    const hogaData = [
        { askSize: 1000, askPrice: 4000, bidPrice: '', bidSize: '' },
        { askSize: 900,  askPrice: 3900, bidPrice: '', bidSize: '' },
        ...
        { askSize: '', askPrice: '', bidPrice: 3100, bidSize: 1200 },
        { askSize: '', askPrice: '', bidPrice: 3000, bidSize: 1300 },
    ];

    exHogaGrid.setData(hogaData);

    // 색상 설정
    exHogaGrid.setUpColor("#ff0000");     // 빨강
    exHogaGrid.setDownColor("#0000ff");   // 파랑
    exHogaGrid.setSteadyColor("#00ff00"); // 초록

    // 레이아웃에 추가
    this.addComponent(exHogaGrid);
    exHogaGrid.setPos(100, 300);
}

```

{% hint style="info" %}
<mark style="color:red;">**Build 에러 발생 시**</mark>

_**프로젝트 트리뷰에서 Framework > stock 우클릭 > Default Load Settings.. > Component > EXHogaGrid.js 체크**_

<img src="../../.gitbook/assets/스크린샷 2025-06-30 084359.png" alt="" data-size="original">
{% endhint %}

