# Accordion

![](../../.gitbook/assets/accor.png)

**아코디언(Accordion)** 는 여러 개의 패널을 포함하여 각 패널을 확장하거나 축소할 수 있는 인터페이스를 제공하는 컴포넌트입니다.\


아코디언 컴포넌트는 공간을 절약하면서도 많은 정보를 표시할 수 있는 유용한 방법을 제공합니다.\


사용자는 각 패널의 헤더를 클릭하여 해당 패널의 내용을 확장하거나 축소할 수 있습니다.

### Attribute

![](../../.gitbook/assets/ac_Attribute.png)

**1️⃣ Items**

* **Item Height**\
  각 아이템의 높이를 설정하는 속성입니다.
* **add**\
  새로운 아이템을 추가하는 기능입니다.
  * **`Title`**: 아이템의 제목을 설정합니다.
  * **`URL`:** 아이템과 연결될 URL을 설정합니다.
* **edit**\
  기존 아이템의 설정 내용을 수정하는 기능입니다.
* **del**\
  선택한 아이템을 삭제하는 기능입니다.
* **up**\
  선택한 아이템의 순서를 한 단계 위로 이동합니다.
* **down**\
  선택한 아이템의 순서를 한 단계 아래로 이동합니다.

**2️⃣ Option**

* **Show item on inserting**\
  아이템을 추가할 때 메뉴를 모두 보여주는 옵션입니다.
* **Single Show**\
  한 번에 하나의 메뉴만 보여주는 옵션입니다.
* **no animation**\
  애니메이션 효과를 제거하는 옵션입니다.
* **No Toggle**\
  토글 기능을 제거하는 옵션입니다.

### Example

AAccordion 컴포넌트는 사용자가 많은 정보를 효율적으로 탐색할 수 있도록 도와주는 유용한 도구입니다.\


이를 통해 복잡한 사용자 인터페이스를 간결하고 직관적으로 설계할 수 있습니다.

**1️⃣ 레이아웃에서 생성**\


**1️⃣-1️⃣ 레이아웃에서 아이템을 추가한 경우**

![](../../.gitbook/assets/ac_add.png)

**<사진 Accordion 컴포넌트의 속성에서 레이아웃 추가 >**



```javascript

onInitDone()
{
	// Accordion 초기 설정

	// 패딩 설정
	this.accordionID.setMenuPadding(10, 20);
	// UP 아이콘 설정
	this.accordionID.setMenuUpIcon('asset/icon/up.png');
}

```

\


**1️⃣-2️⃣ 코드에서 아이템을 추가한 경우**

```javascript

onInitDone()
{
	// Accordion 초기 설정

	// 패딩 설정
	this.accordionID.setMenuPadding(10, 20);
	// UP 아이콘 설정
	this.accordionID.setMenuUpIcon('asset/icon/up.png');

	// 아이템 추가 
	accordionID.insertItem('Item 1', 'Source/Views/Item1.lay'); 
	accordionID.insertItem('Item 2', 'Source/Views/Item2.lay');
}

```

\
\


**2️⃣ 코드에서 생성**\


```javascript

onInitDone()
{
	// 사용자 함수 불러오기
	this.createAccordion()
}

createAccordion()
{
	// AAccordion 생성
	const accordion = new AAccordion();

	// 아코디언 초기화
	accordion.init();

	// 아코디언 옵션 설정
	accordion.setAccordionOption({ 
		isSingleShow: true, // 한 번에 하나의 메뉴만 펼치기
		isAnimation: true, // 애니메이션 효과 사용 
		isShowToggle: true // 펼쳐진 항목 다시 클릭 시 숨기기 
	});

	// 아코디언 아이템 추가
	accordion.insertItem('Item 1', 'Source/Views/Item1.lay', true); 
	accordion.insertItem('Item 2', 'Source/Views/Item2.lay', false); 

	// 아코디언을 특정 컨테이너에 추가
	// jQuery 객체를 사용하여 추가 
	this.view.$ele.append(accordion.$ele); 

	// 아코디언의 선택 이벤트 설정
	accordion.addEventListener('select', function(comp, info, e) { 
		alert('선택된 아이템: ' + info.innerText); 
	});
}

```

**결과화면**

![](../../.gitbook/assets/ac_res.png)
