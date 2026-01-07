---
description: 호가 데이터를 배열 또는 객체 형태로 입력하여 매도/매수 호가를 시각화하는 그리드 컴포넌트
---

# EXHogaGrid

<figure><img src="../../.gitbook/assets/스크린샷 2025-06-27 164531.png" alt="" width="563"><figcaption></figcaption></figure>

### Appearance

공통 Appearance 는 [**6. Global Properties**](<../../Guide for SpiderGen/06  SpiderGen Editor/04  Properties Pane/02 Appearence.md>) 속성을 참고

### Attribute

<figure><img src="../../.gitbook/assets/스크린샷 2025-06-30 082052.png" alt=""><figcaption></figcaption></figure>

<table data-header-hidden><thead><tr><th width="361"></th><th></th></tr></thead><tbody><tr><td><strong>데이터</strong> <strong>속성</strong></td><td></td></tr><tr><td><code>Current Price</code></td><td>현재가 입력</td></tr><tr><td><code>Base Price</code></td><td>기준가 입력</td></tr><tr><td><code>Bottom Row</code></td><td>호가를 하단에 표현될 로우의 개수를 지정</td></tr><tr><td><code>Quote Count</code></td><td>호가의 단계 설정</td></tr><tr><td><strong>가격 색상 속성</strong></td><td></td></tr><tr><td><code>Up</code></td><td>호가 상승색 설정</td></tr><tr><td><code>Down</code></td><td>호가 하락색 설정</td></tr><tr><td><code>Steady</code></td><td>호가 보합색 설정</td></tr><tr><td><strong>바 스타일</strong></td><td></td></tr><tr><td><code>Size</code></td><td>호가 잔량을 표현하는 바 크기 지정</td></tr><tr><td><code>Ask Position</code></td><td>매도 잔량바의 위치를 지정</td></tr><tr><td><code>Bid Position</code></td><td>매수 잔량바의 위치를 지정</td></tr><tr><td><code>Ask Color</code></td><td>매도 잔량바의 색을 지정</td></tr><tr><td><code>Bid Color</code></td><td>매수 잔량바의 색을 지정</td></tr><tr><td><strong>옵션</strong></td><td></td></tr><tr><td><code>Hide Header</code></td><td>헤더 숨김 여부 옵션</td></tr><tr><td><code>Single Select</code></td><td>Ctrl 키를 누르고 선택해도 하나만 선택되는 옵션</td></tr><tr><td><code>Fullrow Select</code></td><td>특정 셀을 클릭해도 그 행 전체가 선택되는 옵션</td></tr><tr><td><code>Selectable</code></td><td>선택 가능 여부 옵션 플래그</td></tr><tr><td><code>Flexable Row</code></td><td>TR의 높이를 TABLE 높이에 풀로 맞추는 옵션</td></tr></tbody></table>

***

### Example

> ExHogaGrid는 AGrid를 확장하여 호가창에 적합한 형태의 그리드를 생성하므로\
> AGrid와 같은 메서드를 활용할 수 있습니다.



**1. 프로젝트 생성**

* 프로젝트 트리뷰에서 Source > MainView.lay 파일을 클릭
* MainView의 레이아웃 파일이 오픈되면 컴포넌트 리스트에서 EXHogaGrid 컴포넌트를 선택하고 드래그하여 레이아웃에 배치
* 컴포넌트의 Class - Identity 에서 ID를 hogagrid로 입력



**2.데이터 설정**

* 먼저 MainView.js 파일을 오픈
* onInitDone() 함수에서 아래와 같이 코드를 입력

{% columns %}
{% column %}
#### <sub>배열 형태 예시</sub>

```javascript
onInitDone()
{
    super.onInitDone()
    this.hogagrid.setData([[
        461679, 62000, null, // 매도 잔량, 호가 시작
        197778, 61900, 
        108156, 61800, 
        112935, 61700, 
        113625, 61600, 
        333086, 61500, 
        286942, 61400, 
        210827, 61300, 
        253941, 61200, 
        243625, 61100, 
        null, 61000, 26216, // 매수 호가, 잔량 시작
        60900, 191373,
        60800, 48972,
        60700, 72411,
        60600, 101422,
        60500, 108568,
        60400, 146241,
        60300, 277847,
        60200, 230109,
        60100, 205014,
        2322594, null, 1408173 // 총 매도 잔량, 중앙값, 총 매수 잔량
    ]])
}
```
{% endcolumn %}

{% column %}
#### <sub>객체 형태 예시</sub>

```javascript
onInitDone()
{
    super.onInitDone()
    this.hogagrid.setData([{
        ask_price9: 461679, ask_remain9: 62000, null_0: null, // 매도 잔량, 호가시작
        ask_price8: 197778, ask_remain8: 61900,
        ask_price7: 108156, ask_remain7: 61800,
        ask_price6: 112935, ask_remain6: 61700,
        ask_price5: 113625, ask_remain5: 61600,
        ask_price4: 333086, ask_remain4: 61500,
        ask_price3: 286942, ask_remain3: 61400,
        ask_price2: 210827, ask_remain2: 61300,
        ask_price1: 253941, ask_remain1: 61200,
        ask_price0: 243625, ask_remain0: 61100,
        null_1:null, bid_price0: 61000, bid_remain0: 26216, // 매수 호가, 잔량 시작
        bid_price1: 60900, bid_remain1: 191373,
        bid_price2: 60800, bid_remain2: 48972,
        bid_price3: 60700, bid_remain3: 72411,
        bid_price4: 60600, bid_remain4: 101422,
        bid_price5: 60500, bid_remain5: 108568,
        bid_price6: 60400, bid_remain6: 146241,
        bid_price7: 60300, bid_remain7: 277847,
        bid_price8: 60200, bid_remain8: 230109,
        bid_price9: 60100, bid_remain9: 205014,
        total_ask_remain:2322594, null_2: null, total_bid_remain:1408173 // 총 매도 잔량, 중앙값, 총 매수 잔량
    ]})
}
```
{% endcolumn %}
{% endcolumns %}

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="" width="157"><figcaption><p>이해를 돕기 위한 차트 예시</p></figcaption></figure>
{% endcolumn %}

{% column %}


<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>실제 출력 화면</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

**3.  기준가 설정**

기준가 보다 낮은 가격은 파란색 높은 가격은 빨간색으로 표시됩니다.(기본색일 경우)

```javascript
this.hogagrid.setBasePrice(60400)
```

<figure><img src="../../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

**4. 현재가 설정**

현재가로 지정한 가격에 일치하는 가격이 있다면 셀이 하이라이트 됩니다.

```javascript
this.hogagrid.setCurrentPrice(61100)
```

<figure><img src="../../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

***

### 코드로 ExHogaGrid  생성

* 먼저 MainView.js 파일을 오픈
* onInitDone() 함수에서 아래와 같이 코드를 입력

```javascript
onInitDone() 
{
    super.onInitDone();
    
    // EXHogaGrid 인스턴스 생성 및 초기화
    const hogaGrid = new EXHogaGrid();
    hogaGrid.init();
    
    // 컨테이너에 hogaGrid 추가
    this.getContainer().addComponent(hogaGrid);
    
    //예시 데이터 정의 및 설정
    const dataObj = {...생략...}
    hogaGrid.setData([dataObj]);        //데이터 설정
    hogaGrid.setBasePrice(60400);        //기준가 설정
    hogaGrid.setCurrentPrice(60100);        //현재가 설정
    
    //이벤트 리스너 및 델리게이터 설정
    //AGrid와 동일한 방식으로 select 이벤트 등록 가능
    hogaGrid.addEventListener('select', this, 'onGridSelect');
    //hogaGrid의 메서드를 this객체에 위임(quoteCount또는 bottomRowCount를 변경하면 onRowCountChange 메서드가 호출됨)
    hogaGrid.setDelegator(this);
}

onGridSelect(comp, _info, _e) 
{
    //QuoteCount 값을 변경
    comp.setQuoteCount(comp.getQuoteCount()-1);
}

//setDelegator로 메서드를 위임받은 상태에서 QuoteCount이 변경되면 "onRowCountChange"이 호출됨
onRowCountChange()
{
    console.log("QuoteCount 갯수: ", this.hogaGrid.getQuoteCount());
}
```

{% hint style="info" %}
**코드로 생성시 직접 컴포넌트 모듈을 불러와야 합니다.**

프로젝트 트리뷰에서 Framework > stock 우클릭 > Default Load Settings.. > Component > **EXHogaGrid** 선택 (이벤트 사용시  **EXHogaGridEvent** 선택)

![](<../../.gitbook/assets/image (73).png>)
{% endhint %}

***

### Method

<details>

<summary>주요 메서드</summary>

1\. `setData(dataArr)`: 호가 관련 데이터를 그리드에 표현합니다.

2.`setBasePrice(basePrice)`: 기본가를 설정합니다.

3.`setCurrentPrice` : 현재가를 설정합니다.

</details>

<details>

<summary>그 외</summary>

1\. `setUpColor(color)`: 호가 상승색을 설정합니다.

2\. `setDownColor(color)`: 호가 하락색을 설정합니다.

3\. `setSteadyColor(color)`: 호가 보합색을 설정합니다.

4\. `getUpColor()`: 호가 상승색을 반환합니다.

5\. `getDownColor()`: 호가 하락색을 반환합니다.

6\. `getSteadyColor()`: 호가 보합색을 반환합니다.

7\. `setRateMode(enable)`: 호가 우측의 등락률 표현 여부를 지정합니다.

8\. `getRateMode()`: 호가 우측의 등락률 표현 여부를 반환합니다.

9\. `selectCurrentCell(mapCell)`: 현재가의 상승, 하락, 보합에 따라 셀에 클래스를 지정합니다.

10\. `setCurrentPriceStyleArr(styleArr)`: 현재가에 해당하는 셀에 추가할 상승, 하락, 보합의 클래스 목록을 지정합니다.

11\. `setDecimal(exp)`: 호가의 소수점 아래 자리수를 지정합니다.

12\. `initBar()`: 호가 잔량을 표현하는 바를 초기화합니다.

13\. `setBarSize(barSize)`: 호가 잔량을 표현하는 바의 높이를 지정합니다.

14\. `getBarSize()`: 호가 잔량을 표현하는 바의 높이를 반환합니다.

15\. `setAskBarBgImg(bgImage)`: 매도 잔량바의 Background-image를 지정합니다.

16\. `getAskBarBgImg()`: 매도 잔량바의 Background-image를 반환합니다.

17\. `setBidBarBgImg(bgImage)`: 매수 잔량바의 Background-image를 지정합니다.

18\. `getBidBarBgImg()`: 매수 잔량바의 Background-image를 반환합니다.

19\. `setAskBarPositionX(pos)`: 매도 잔량바의 시작 위치 x 값을 지정합니다.

20\. `getAskBarPositionX()`: 매도 잔량바의 시작 위치 x 값을 반환합니다.

21\. `setAskBarPositionY(pos)`: 매도 잔량바의 시작 위치 y 값을 지정합니다.

22\. `getAskBarPositionY()`: 매도 잔량바의 시작 위치 y 값을 반환합니다.

23\. `setBidBarPositionX(pos)`: 매수 잔량바의 시작 위치 x 값을 지정합니다.

24\. `getBidBarPositionX()`: 매수 잔량바의 시작 위치 x 값을 반환합니다.

25\. `setBidBarPositionY(pos)`: 매수 잔량바의 시작 위치 y 값을 지정합니다.

26\. `getBidBarPositionY()`: 매수 잔량바의 시작 위치 y 값을 반환합니다.

27\. `setBottomRowCount(btmRowCnt)`: 호가를 하단에 표현될 로우의 개수를 지정합니다.

28\. `getBottomRowCount()`: 호가를 하단에 표현된 로우의 개수를 반환합니다.

29\. `setQuoteCount(cnt)`: 호가의 단계를 지정합니다.

30\. `getQuoteCount()`: 호가의 단계를 반환합니다.

31\. `setDelegator(delegator)`:   메서드 위임 객체를 지정합니다.(quoteCount, bottomRowCount 변경시 onRowCountChange메서드호출됨)

32\. `toggleRateMode()`: 호가 우측에 등락률을 표현하거나 제거합니다.

</details>
