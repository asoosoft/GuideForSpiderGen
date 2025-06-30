# ExMiniHoga

<figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

EXMiniHoga는 호가와 거래량을 2열로 표시하는 호가 그리드 컴포넌트

이 컴포넌트는 주식 거래에서 호가 정보를 시각적으로 표현하는 데 사용

### Appearance

공통 Appearance 는 [**6. Global Properties**](<../../Guide for SpiderGen/06  SpiderGen Editor/04  Properties Pane/02 Appearence.md>) 속성을 참고

### Attribute

EXMiniHoga속성

<figure><img src="../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

**Data**

<table data-header-hidden><thead><tr><th width="361"></th><th></th></tr></thead><tbody><tr><td><strong>이름</strong></td><td><strong>설명</strong></td></tr><tr><td><strong>속성</strong></td><td></td></tr><tr><td><code>Current Price</code></td><td>매핑된 쿼리파일의 현재가의 필드명을 입력</td></tr><tr><td><code>Base Price</code></td><td>매핑된 쿼리파일의 기준가의 필드명을 입력</td></tr><tr><td><code>Bottom Row</code></td><td>호가를 하단에 표현될 로우의 개수를 지정</td></tr><tr><td><code>Quote Count</code></td><td>호가의 단계 설정</td></tr><tr><td><strong>색상 속성</strong></td><td></td></tr><tr><td><code>Up</code></td><td>호가 상승색 설정</td></tr><tr><td><code>Down</code></td><td>호가 하락색 설정</td></tr><tr><td><code>Steady</code></td><td>호가 보합색 설정</td></tr><tr><td><strong>바 스타일</strong></td><td></td></tr><tr><td><code>Size</code></td><td>호가 잔량을 표현하는 바의 높이를 지정</td></tr><tr><td><code>Ask Position</code></td><td>매도 잔량바의 위치를 지정</td></tr><tr><td><code>Bid Position</code></td><td>매수 잔량바의 위치를 지정</td></tr><tr><td><code>Ask Color</code></td><td>매도 잔량바의 색을 지정</td></tr><tr><td><code>Bid Color</code></td><td>매수 잔량바의 색을 지정</td></tr><tr><td><strong>옵션</strong></td><td></td></tr><tr><td><code>Hide Header</code></td><td>헤더 숨김 여부 옵션</td></tr><tr><td><code>Single Select</code></td><td>Ctrl 키를 누르고 선택해도 하나만 선택되는 옵션</td></tr><tr><td><code>Fullrow Select</code></td><td>특정 셀을 클릭해도 그 행 전체가 선택되는 옵션</td></tr><tr><td><code>Selectable</code></td><td>선택 가능 여부 옵션 플래그</td></tr><tr><td><code>Flexable Row</code></td><td>TR의 높이를 TABLE 높이에 풀로 맞추는 옵션</td></tr></tbody></table>

### Example

**1. 프로젝트 생성**

* 프로젝트 트리뷰에서 Source > MainView.lay 파일을 클릭
* MainView의 레이아웃 파일이 오픈되면 컴포넌트 리스트에서 EXMiniHoga 컴포넌트를 선택하고 드래그하여 레이아웃에 배치
* Class 에서 ID를 minihoga로 입력



**2. 데이터 설정**

* 먼저 MainView.js 파일을 오픈
* 상단의 파일탭에서 MainView.lay 탭을 더블 클릭하거나 우측의 프로젝트 트리에서 MainView.js 파일을 더블 클릭
* 모든 화면뷰는 onInitDone() 함수가 존재하며 이 함수는 화면이 생성될 때 딱 한번 실행
* onInitDone() 함수에서 레이블의 텍스트 내용을 아래와 같이 코드를 입력

```javascript
onInitDone()
{
	super.onInitDone()
	this.minihoga.setData([{
           ask_hoga20: 4000, ask_remain20: 1000,
           ask_hoga19: 3900, ask_remain19: 2000,
           ask_hoga18: 3800, ask_remain18: 2000,
           ask_hoga17: 3700, ask_remain17: 2000,
           ask_hoga16: 3600, ask_remain16: 2000,
           ask_hoga15: 3500, ask_remain15: 2000,
           ask_hoga14: 3400, ask_remain14: 2000,
           ask_hoga13: 3300, ask_remain13: 2000,
           ask_hoga12: 3200, ask_remain12: 2000,
           ask_hoga11: 3100, ask_remain11: 2000,
           ask_hoga10: 3000, ask_remain10: 1000,
           ask_hoga9: 2900, ask_remain9: 2000,
           ask_hoga8: 2800, ask_remain8: 2000,
           ask_hoga7: 2700, ask_remain7: 2000,
           ask_hoga6: 2600, ask_remain6: 2000,
           ask_hoga5: 2500, ask_remain5: 2000,
           ask_hoga4: 2400, ask_remain4: 2000,
           ask_hoga3: 2300, ask_remain3: 2000,
           ask_hoga2: 2200, ask_remain2: 2000,
           ask_hoga1: 2100, ask_remain1: 2000,
       }]);
       // <- 데이터를 Array로 변경해서 사용도 가능
       // ex )
       //    this.minihoga.setData([[
       //         461679,62000,null,
       //         197778,61900, 
       //         108156,61800, 
       //         112935,61700, 
       //         null,61000, 26216,
       // .....
       

       // 기준가
       this.minihoga.setBasePrice(3200);

       // 현재가
       this.minihoga.setCurrentPrice(2700);
}
```

**3. 프로젝트 실행**

* 입력한 데이터인 호가(기준가 대비 색상 및 현재가에 테두리)와 잔량이 표시됨

<figure><img src="../../.gitbook/assets/image (48).png" alt=""><figcaption><p>&#x3C;EXMiniHoga 컴포넌트></p></figcaption></figure>

**5. 코드로** EXMiniHoga **생성**

* 먼저 MainView.js 파일을 오픈
* onInitDone() 함수에서 아래와 같이 코드를 입력

```javascript
onInitDone()
{
	super.onInitDone()
	
	// EXMiniHoga 인스턴스 생성
        const exMiniHoga = new EXMiniHoga();

        // 컴포넌트 초기화
        exMiniHoga.init();

        // 현재가와 기준가 설정
        exMiniHoga.setCurrentPrice(2300);
        exMiniHoga.setBasePrice(2500);

        // 호가 데이터 설정
        var hogaData = [{
            ask_hoga20: 4000, ask_remain20: 1000,
            ask_hoga19: 3900, ask_remain19: 2000,
            ask_hoga18: 3800, ask_remain18: 2000,
            ask_hoga17: 3700, ask_remain17: 2000,
            ask_hoga16: 3600, ask_remain16: 2000,
            ask_hoga15: 3500, ask_remain15: 2000,
            ask_hoga14: 3400, ask_remain14: 2000,
            ask_hoga13: 3300, ask_remain13: 2000,
            ask_hoga12: 3200, ask_remain12: 2000,
            ask_hoga11: 3100, ask_remain11: 2000,
            ask_hoga10: 3000, ask_remain10: 1000,
            ask_hoga9: 2900, ask_remain9: 2000,
            ask_hoga8: 2800, ask_remain8: 2000,
            ask_hoga7: 2700, ask_remain7: 2000,
            ask_hoga6: 2600, ask_remain6: 2000,
            ask_hoga5: 2500, ask_remain5: 2000,
            ask_hoga4: 2400, ask_remain4: 2000,
            ask_hoga3: 2300, ask_remain3: 2000,
            ask_hoga2: 2200, ask_remain2: 2000,
            ask_hoga1: 2100, ask_remain1: 2000,
        }];
        exMiniHoga.setData(hogaData);

        // 상승, 하락, 보합 색상 설정
        exMiniHoga.setUpColor("#ff0000"); // 예: 빨간색
        exMiniHoga.setDownColor("#0000ff"); // 예: 파란색
        exMiniHoga.setSteadyColor("#00ff00"); // 예: 초록색

        // 생성된 EXMiniHoga 컴포넌트를 원하는 위치에 추가
        this.addComponent(exMiniHoga); // 레이아웃에 exMiniHoga 추가
        exMiniHoga.setPos(100,100);
}
```

{% hint style="info" %}
<mark style="color:red;">**Build 에러발생시**</mark>

_**프로젝트 트리뷰에서 Framework > stock 우클릭 > Default Load Settings.. > Component > EXMiniHoga.js 체크**_

![](<../../.gitbook/assets/image (49).png>)
{% endhint %}
