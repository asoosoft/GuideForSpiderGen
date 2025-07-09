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

    this.dataArr = 
    [
      [ "005930", "삼성전자", "001" ], 
      [ "003550", "LG", "002" ], 
      [ "005380", "현대자동차", "003" ],
    ];
  
    //데이터 설정시 변경 이벤트 발생여부
    const isReport = true;
    // setItemInfo(dataArr) -> EXItemView에 하나의 데이터 설정
    this.itemView.setItemInfo(this.dataArr[0], isReport);
}
```

<figure><img src="../../.gitbook/assets/image (92).png" alt=""><figcaption></figcaption></figure>

* 배치한 EXItemView 의 레이아웃을 위 사진과 같이 일부 변형해서 사용
* 위 데이터 예제와 같이 설정한 데이터에 맞춰 ALabel 컴포넌트의 아이디를 각각 name, code로 변경



```javascript

onOpenDrop(comp, info, e)
{
    // EXItemView의 openDrop 함수를 dropBtn 아이디를 가진 AButton 컴포넌트의 클릭이벤트에 설정
    // => openDrop(itemArr)
    this.itemView.openDrop(this.Data);
}

// EXItemView의 Change 이벤트 지정
onItemViewChange(comp, info, e)
{
    // setItemInfo(itemInfo, isReport) 호출시 isReport 값이 true 인 경우 change 이벤트 발생
    // 또는 위 openDrop으로 연 데이터 리스트에서 아이템을 선택시 change 이벤트 발생
    // 각 ALabel 컴포넌트에 선택한 데이터의 코드와 이름이 들어가게 함
    this.code.setText(info[0]);
    this.name.setText(info[1]);
}
```



**3. 프로젝트 실행**

* 드롭버튼을 클릭해 실행결과 확인

<figure><img src="../../.gitbook/assets/image (93).png" alt=""><figcaption><p>&#x3C;drop버튼 클릭 시></p></figcaption></figure>



<figure><img src="../../.gitbook/assets/image (94).png" alt=""><figcaption><p>&#x3C;아이템 선택 시></p></figcaption></figure>

