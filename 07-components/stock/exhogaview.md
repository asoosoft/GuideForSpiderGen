---
description: >-
  호가창을 출력하는 ExHogaGrid 컴포넌트와 추가적인 UI 요소나 기능을 포함할 수 있는 공간을 제공하는 AView를 포함하여 레이아웃을
  관리하는 역할을 하는 컨테이너 컴포넌트
---

# ExHogaView

> 이 컴포넌트가 담고 있는\
> [ExHogaGrid 예제 보러가기](exhogagrid.md)

<figure><img src="../../.gitbook/assets/image (62).png" alt="" width="516"><figcaption></figcaption></figure>

### Appearance

공통 Appearance 는 [**6. Global Properties**](https://asoosoft.gitbook.io/guideforspidergen/06-spidergen-editor/04-properties-pane/02-appearence) 속성을 참고

### Attribute

<table data-header-hidden><thead><tr><th width="361"></th><th></th></tr></thead><tbody><tr><td><strong>정보 속성</strong></td><td></td></tr><tr><td><code>Show Count</code></td><td>보여줄 호가 셀 만큼의 호가 뷰 높이 설정</td></tr></tbody></table>

***

### Example

#### 1. 프로젝트 생성

* 프로젝트 트리뷰에서 `Source > MainView.lay` 파일을 클릭.
* MainView의 레이아웃 파일이 오픈되면 컴포넌트 리스트에서 **EXHogaView** 컴포넌트를 선택하고 드래그하여 레이아웃에 배치.
* Class에서 ID를 **hogaView**로 입력.

***

#### 2. 보여줄 호가 갯수 설정

```javascript
onInitDone()
{
	super.onInitDone()
	
	hogaView.setShowCount(8);	//보여줄 호가 셀 갯수
    	hogaView.scrollToQuoteCenter();	//스크롤 중앙 정렬
}
```

<figure><img src="../../.gitbook/assets/image (61).png" alt="" width="375"><figcaption></figcaption></figure>

3\. 자식 AView를 활용한 ui 사용

<figure><img src="../../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

***

### 코드로 EXHogaView 생성

onInitDone() 함수에서 아래와 같이 코드를 입력

```javascript
onInitDone() {
    super.onInitDone();

    //EXHogaView 생성
    const exHogaView = new EXHogaView();
    exHogaView.init();

    // 자동 리사이즈 비활성화
    exHogaView.setAutoResizeChildren(false);

    // 위치 및 크기 설정
    exHogaView.setPos(50, 50);
    exHogaView.setSize(450, 600);

    this.addComponent(exHogaView);
}
```

{% hint style="info" %}
**코드로 생성시 직접 컴포넌트 모듈을 불러와야 합니다.**

프로젝트 트리뷰에서 Framework > stock 우클릭 > Default Load Settings.. > Component > **ExHogaView**, **ExHogaGrid** 선택(이벤트 사용시 **EXHogaGridEvent**와 **EXHogaViewEvent**도 선택)

![](<../../.gitbook/assets/image (72).png>)
{% endhint %}

***

### Method

<details>

<summary>주요메서드</summary>

1. `updatePosition(pWidth, pHeight)` : 사이즈가 변경될 때 호출되는 함수로, 부모 뷰의 넓이와 높이를 인자로 받아 뷰 컴포넌트의 위치나 사이즈를 갱신합니다
2. `setShowCount(cnt)` : 현재 뷰에서 보여줄 호가의 개수를 지정합니다.
3. `scrollToQuoteCenter()` : 호가가 중간에 위치하도록 스크롤 위치를 변경합니다.
4. `getShowCount()` : 현재 뷰에서 보여줄 호가의 개수를 반환합니다.
5. `setAutoResizeChildren(isAuto)` : 자식들의 위치와 높이를 자동으로 변경할지 여부를 지정합니다.
6. `getAutoResizeChildren()` : 자식들의 위치와 높이 자동 변경 여부를 반환합니다.
7. `onRowCountChange()` : 호가 그리드의 행 개수가 변경될 때 호출되는 함수입니다.

</details>

