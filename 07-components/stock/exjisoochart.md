---
description: 지수를 표현하는 차트 컴포넌트로, 주식 시장에서 지수의 변동을 시각적으로 표현하는 데 사용됩니다
---

# EXJisooChart

<figure><img src="../../.gitbook/assets/image (70).png" alt="" width="563"><figcaption></figcaption></figure>

### Appearance

공통 Appearance 는 [**6. Global Properties**](<../../Guide for SpiderGen/06  SpiderGen Editor/04  Properties Pane/02 Appearence.md>) 속성을 참고

### Attribute

<table data-header-hidden><thead><tr><th width="361"></th><th></th></tr></thead><tbody><tr><td><strong>data 속성</strong></td><td></td></tr><tr><td><code>Title</code></td><td>차트 중앙 상단에 출력될 제목</td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="361"></th><th></th></tr></thead><tbody><tr><td><strong>color 속성</strong></td><td></td></tr><tr><td><code>Text</code></td><td>X, Y 축 눈금 라벨의 색상</td></tr><tr><td><code>Line</code></td><td>그래프의 외곽선 색상</td></tr><tr><td><code>Divide LIne</code></td><td>Y축과 그래프간 경계선 색상</td></tr><tr><td><code>LongTab Line</code></td><td>롱탭시 출력되는 크로스헤어선 색상</td></tr><tr><td><code>Start</code></td><td>그래프 그라데이션 색상 위쪽 색상</td></tr><tr><td><code>End</code></td><td>그래프 그라데이션 색상 아래 색상</td></tr><tr><td><code>Dot</code></td><td> 그래프 그리드 점선 격자 색상</td></tr></tbody></table>

***

### Example

**1. 프로젝트 생성**

* 프로젝트 트리뷰에서 Source > MainView.lay 파일을 클릭
* MainView의 레이아웃 파일이 오픈되면 컴포넌트 리스트에서 EXJisooChart 컴포넌트를 선택하고 드래그하여 레이아웃에 배치
* Class에서 ID를 jisoo로 입력



**2.데이터 설정**

* 먼저 MainView.js 파일을 오픈
* onInitDone() 함수에서 아래와 같이 코드를 입력

> setData 함수를 통해 설정할 배열의 아이템 구조는  `[날짜, 시가, 고가, 저가, 종가, 거래량, 거래대금]`형태로 이루어져 있고 `날짜, 종가` 값을 이용해 그래프를 출력하며 longtab시 `시가, 고가, 저가, 종가`를  이용해 롱탭 모달을 출력합니다.

```javascript
onInitDone() {
    super.onInitDone();

    const baseData = [
            [20261010, 0, 0, 0, 1200, 0, 0],
            [20251010, 0, 0, 0, 500, 0, 0],
            [20241010, 0, 0, 0, 200, 0, 0],
            [20231010, 0, 0, 0, 200, 0, 0],
            [20231009, 0, 0, 0, 400, 0, 0],
            [20231008, 0, 0, 0, 700, 0, 0],
            [20231007, 0, 0, 0, 600, 0, 0],
            [20231006, 0, 0, 0, 100, 0, 0],
            [20231005, 0, 0, 0, 600, 0, 0],
            [20231004, 0, 0, 0, 1000, 0, 0],
            [20231003, 0, 0, 0, 800, 0, 0],
            [20231002, 0, 0, 0, 1500, 0, 0],
            ...생략...
    ];
    this.jisoo.setData(baseData);
}
```



**3.결과확인**

<figure><img src="../../.gitbook/assets/image (71).png" alt="" width="563"><figcaption></figcaption></figure>

### 코드로 EXJisooView 생성

* 먼저 MainView.js 파일을 오픈
* onInitDone() 함수에서 아래와 같이 코드를 입력

```javascript
onInitDone() 
{
        super.onInitDone();
        
        //컴포넌트 생성
        const jisoo = new EXJisooChart();
        jisoo.init();
        
        //데이터 설정
        const baseData = [...생략...];
        jisoo.setData(baseData);
        
        //메서드 위임
        jisoo.setDelegator(this);//EXJisooChart의 callNextData는 화면에서 세팅된 데이터의 끝까지 확인한 경우에 다음 데이터 추가를 위해 호출됩니다
        
        this.addComponent(jisoo)//컴포넌트 삽입
}

async callNextData(nextIqryDate)//위임받은 callNextData를 재정의합니다
{
        try 
        {
                // 예시: 서버로부터 추가 데이터를 비동기적으로 가져오는 코드
                const response = await fetch(`https://api.asoosoft.com/data?date=${nextIqryDate`});
                const newData = await response.json();

                // 가져온 데이터를 차트에 추가
                if (newData && newData.length > 0) 
                {
                    this.jisoo.addNewData(newData);
                }
        } 
        catch (error) 
        {
                console.error("Error fetching additional data:", error);
        }
}
```

{% hint style="info" %}
**코드로 생성시 직접 컴포넌트 모듈을 불러와야 합니다.**

프로젝트 트리뷰에서 Framework > stock 우클릭 > Default Load Settings.. > Component > **EXJiSooChart** 선택(이벤트 사용시 **EXJiSooChartEvent** 선택)

![](<../../.gitbook/assets/image (1) (1).png>)
{% endhint %}

***

### Method

<details>

<summary>주요 메서드</summary>

1. `draw()` : 차트를 그립니다. 필요한 경우 차트를 다시 그리도록 호출합니다.
2. `resetData()` : 기존의 데이터를 제거하고 차트를 초기 상태로 되돌립니다.
3. `setColors(colors)` :  colors 객체를 통해 텍스트, 라인, 그라데이션 등의 색상을 지정할 수 있습니다.
4. `setData()` :  차트에 데이터를 설정하는 메서드 입니다.
5. `setDelegator(delegator)` : 차트의 delegator를 설정하는 메서드입니다. 데이터의 끝에 도달했을 때 추가 요청 메서드를 받을 객체를 지정합니다.
6. `setDivisionVal(divisionVal)` : 지수 차트 데이터를 나눗셈할 값을 설정하는 메서드입니다. 차트의 데이터 스케일을 조정할 때 사용됩니다.
7. `upDatePosition(pWidth, pHeight)` : 차트의 너비 및 높이를 업데이트하는 메서드입니다. 차트의 크기를 조정할 때 사용됩니다.
8. `setZoomEvent()` : 줌 이벤트를 설정하는 메서드입니다. 차트의 확대 및 축소 동작을 처리합니다.
9. `setMaxMin(pWidth, pHeight)` : 상하단 그래프의 최대 최소 값을 설정하는 메서드입니다. 차트의 데이터 범위를 조정합니다.

</details>
