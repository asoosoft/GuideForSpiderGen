---
description: 지수를 표현하는 차트 컴포넌트로, 주식 시장에서 지수의 변동을 시각적으로 표현하는 데 사용됩니다
---

# EXJisooChart

<figure><img src="../../.gitbook/assets/image (70).png" alt="" width="563"><figcaption></figcaption></figure>

### Appearance

공통 Appearance 는 [**6. Global Properties**](<../../Guide for SpiderGen/06  SpiderGen Editor/04  Properties Pane/02 Appearence.md>) 속성을 참고

### Attribute

<figure><img src="../../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>

<table data-header-hidden><thead><tr><th width="361"></th><th></th></tr></thead><tbody><tr><td><strong>Data 속성</strong></td><td></td></tr><tr><td><code>Title</code></td><td>차트 중앙 상단에 출력될 제목</td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="361"></th><th></th></tr></thead><tbody><tr><td><strong>Color 속성</strong></td><td></td></tr><tr><td><code>Text</code></td><td>X, Y 축 눈금 라벨의 색상</td></tr><tr><td><code>Line</code></td><td>그래프의 외곽선 색상</td></tr><tr><td><code>Divide LIne</code></td><td>Y축과 그래프간 경계선 색상</td></tr><tr><td><code>LongTab Line</code></td><td>롱탭시 출력되는 크로스헤어선 색상</td></tr><tr><td><code>Start</code></td><td>그래프 그라데이션 색상 위쪽 색상</td></tr><tr><td><code>End</code></td><td>그래프 그라데이션 색상 아래쪽 색상</td></tr><tr><td><code>Dot</code></td><td> 그래프 그리드 점선 격자 색상</td></tr></tbody></table>

***

### Example

**1. 프로젝트 생성**

* 프로젝트 트리뷰에서 Source > MainView.lay 파일을 클릭
* MainView의 레이아웃 파일이 오픈되면 컴포넌트 리스트에서 EXJisooChart 컴포넌트를 선택하고 드래그하여 레이아웃에 배치
* Class에서 ID를 jisoo로 입력



**2.데이터 설정**

* 먼저 MainView.js 파일을 오픈
* onInitDone() 함수에서 아래와 같이 코드를 입력

> setData(dataArr, KeyArr) 함수를 통해 설정할 배열의 아이템 구조는 기본적으로 `[날짜, 시가, 고가, 저가, 종가, 거래량, 거래대금]`형태로 이루어져 있고 `날짜, 종가` 값을 이용해 그래프를 출력하며 longtab시 `시가, 고가, 저가, 종가`를  이용해 롱탭 모달을 출력합니다.

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

### 코드로 EXJisooChart 생성

* 먼저 MainView.js 파일을 오픈
* onInitDone() 함수에서 아래와 같이 코드를 입력

```javascript
onInitDone() 
{
    super.onInitDone();
    
    //컴포넌트 생성
    this.jisoo = new EXJisooChart();//view 내에서 호출하기 위해 멤버 변수로 참조를 저장합니다.
    this.jisoo.init();
    
    //데이터 설정
    const baseData = [...생략...];
    this.jisoo.setData(baseData);
    
    //메서드 위임
    this.jisoo.setDelegator(this);//EXJisooChart의 callNextData는 화면에서 세팅된 데이터의 끝까지 확인한 경우에 다음 데이터 추가를 위해 호출됩니다
    
    this.addComponent(this.jisoo);//컴포넌트 삽입
}

callNextData(nextIqryDate)//위임받은 callNextData를 재정의합니다.
{
    let randomDataArr = [];
    for(let i=1; i<100; i++) 
        randomDataArr.push(this.createRandomDataArr(nextIqryDate));
    //setQueryData(dataArr,kerArr) 메서드로 data 배열 뒤쪽에 추가 값을 저장합니다.(현재 스파이더젠 버전에서 권장하는 방식)
    this.jisoo.setQueryData(randomDataArr, Object.keys(randomDataArr[0]));
    this.jisoo.nextIqryDate = randomDataArr[0][0]-1;//다음 호출에서 사용할 nextIqryDate 저장
}

//이해를 돕기 위한 랜덤 배열을 생성하는 함수입니다(실제로는 통신 값을 이용)
createRandomDataArr(lastDate)
{
    return [parseInt(lastDate)-1,0,0,0,Math.floor(Math.random()*1500),0,0];
}

onActiveDone(isFirst) 
{
    super.onActiveDone(isFirst);

    let currentDate = this.jisoo.data[0][0];
    //새로고침 타이머
    if (this.refreshTimer) return;
    this.refreshTimer = setInterval(()=>
    {
        currentDate ++;
        //addNewData(dataArr,keyArr)로 data 배열 앞쪽에 값을 추가합니다.
        this.jisoo.addNewData(this.createRandomDataArr(currentDate));
    },1000);
}

onDeactiveDone()
{
    //새로고침 타이머 클린업
    if (!this.refreshTimer) return;
    clearInterval(this.refreshTimer);
}
```

{% hint style="info" %}
**코드로 생성시 직접 컴포넌트 모듈을 불러와야 합니다.**

프로젝트 트리뷰에서 Framework > stock 우클릭 > Default Load Settings.. > Component > **EXJiSooChart** 선택(이벤트 사용시 **EXJiSooChartEvent** 선택)

![](<../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png>)
{% endhint %}

***

### Method

<details>

<summary>주요 메서드</summary>

1. `setData(dataArr, KeyArr)` :  차트에 데이터를 설정하는 메서드 입니다.
2. `addNewData(dataArr,keyArr)` : 차트에 새로운 데이터를 추가합니다. newData는 시간과 값의 배열입니다.
3. `setDelegator(delegator)` : 차트의 delegator를 설정하는 메서드입니다. 데이터의 끝에 도달했을 때 추가 요청 메서드를 받을 객체를 지정합니다.
4. `resetData()` : 기존의 데이터를 제거하고 차트를 초기 상태로 되돌립니다.
5. `draw()` : 차트를 그립니다. 필요한 경우 차트를 다시 그리도록 호출합니다.
6. `setDivisionVal(divisionVal)` : 지수 차트 데이터를 나눗셈할 값을 설정하는 메서드입니다. 차트의 데이터 스케일을 조정할 때 사용됩니다.
7. `setMaxMin(pWidth, pHeight)` : 상하단 그래프의 최대 최소 값을 설정하는 메서드입니다. 차트의 데이터 범위를 조정합니다.
8. `upDatePosition(pWidth, pHeight)` : 차트의 너비 및 높이를 업데이트하는 메서드입니다. 차트의 크기를 조정할 때 사용됩니다.
9. `setZoomEvent()` : 줌 이벤트를 설정하는 메서드입니다. 차트의 확대 및 축소 동작을 처리합니다.
10. `setColors(colors)` :  colors 객체를 통해 텍스트, 라인, 그라데이션 등의 색상을 지정할 수 있습니다.

</details>
