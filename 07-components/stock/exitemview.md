---
description: 종목 선택을 위한 뷰 컴포넌트
---

# EXItemView

<figure><img src="../../.gitbook/assets/image (90).png" alt=""><figcaption><p>&#x3C;EXItemView 컴포넌트></p></figcaption></figure>

이 컴포넌트는 사용자가 특정 종목을 선택하고, 그에 따른 정보를 표시하거나 조작할 수 있도록 도움

&#x20;EXItemView는 다양한 속성과 메서드를 제공하여 <mark style="color:red;">종목 데이터를 관리하고 사용자 인터페이스와 상호작용</mark> 할 수 있음

<figure><img src="../../.gitbook/assets/image (91).png" alt=""><figcaption><p>&#x3C;EXItemView의 기본 트리 구조></p></figcaption></figure>

{% hint style="warning" %}
**EXItemView의 레이아웃은 사용자들이 많이 사용하는 구성으로 짜여있으며 이는 삭제하고 사용해도 무방**
{% endhint %}

### Appearance

공통 Appearance 는 [**6. Global Properties**](<../../Guide for SpiderGen/06  SpiderGen Editor/04  Properties Pane/02 Appearence.md>) 속성을 참고

### Attribute

<mark style="color:red;">EXItemView의 Attribute는 사용하지 않습니다.</mark>



### Example

**1. 프로젝트 생성**

* 프로젝트 트리뷰에서 Source > MainView.lay 파일을 클릭
* MainView의 레이아웃 파일이 오픈되면 컴포넌트 리스트에서 EXItemView 컴포넌트를 선택하고 드래그하여 레이아웃에 배치
* Class 에서 ID를 itemView로 입력
* 배치한 EXItemView에 속한 컴포넌트를 그대로 사용하는 예제 진행



**2. 데이터 설정**

* 먼저 MainView.js 파일을 오픈
* 상단의 파일탭에서 MainView.lay 탭을 더블 클릭하거나 우측의 프로젝트 트리에서 MainView.js 파일을 더블 클릭
* 예시와 같이 임시 데이터 설정

```javascript
init(context, evtListener)
{
    super.init(context, evtListener)  

    this.Data = 
    [
      [ "005930", "삼성전자", "001" ], 
      [ "003550", "LG", "002" ], 
      [ "005380", "현대자동차", "003" ],
    ];
  
    // setItemInfo(dataArr) -> EXItemView에 데이터 설정
    this.itemView.setItemInfo(this.Data);            
}
```

<figure><img src="../../.gitbook/assets/image (92).png" alt=""><figcaption></figcaption></figure>

*



**3. 프로젝트 실행**

* 설정한 데이터에 맞춰서 상승인지 하락인지에 따라 봉 생성

<div data-full-width="false"><figure><img src="../../.gitbook/assets/image (52).png" alt=""><figcaption><p>ex) [1000, 2000, 900, 1400]</p></figcaption></figure> <figure><img src="../../.gitbook/assets/image (55).png" alt=""><figcaption><p>ex) [1500, 2000, 700, 900]</p></figcaption></figure></div>

**5. 코드로 EXBong 생성**

* 먼저 MainView.js 파일을 오픈
* onInitDone() 함수에서 아래와 같이 코드를 입력

```javascript
onInitDone()
{
	super.onInitDone()
	
	// EXBong 인스턴스 생성
        const exBong = new EXBong();

        // 컴포넌트 초기화
        exBong.init();

        // 상승 색상 설정
        exBong.setUpColor("#ff0000"); // 예: 빨간색

        // 하락 색상 설정
        exBong.setDownColor("#0000ff"); // 예: 파란색

        // 방향 설정 (세로 방향)
        exBong.setDirection(true);

        // 시가, 고가, 저가, 종가 데이터 설정
        let valueArr = [55, 100, 0, 25];
        let prdyvrss = 5; // 전일대비 등락구분값 예시
        exBong.setData(valueArr, prdyvrss);

        // 생성된 EXBong 컴포넌트를 원하는 위치에 추가
        this.addComponent(exBong); // 레이아웃에 EXBong 추가
	exBong.setPos(100,100); // 원하는 위치에 배치
}
```

<div><figure><img src="../../.gitbook/assets/image (56).png" alt=""><figcaption><p>[55, 100, 0, 25]</p></figcaption></figure> <figure><img src="../../.gitbook/assets/image (57).png" alt=""><figcaption><p>[55, 100, 0, 75]</p></figcaption></figure></div>
