# CalendarPicker

![](../../.gitbook/assets/cp.png)

**캘린더 피커(ACalendarPicker)** 는 날짜를 선택하고 표시할 수 있는 컴포넌트입니다.\


> 캘린더 피커는 사용자가 날짜를 입력하거나 선택할 수 있도록 지원하며, 달력 인터페이스를 통해 직관적인 날짜 선택 기능을 제공합니다.\
>

캘린더 피커는 두 가지 주요 영역으로 나뉩니다.\
1️⃣ 직접 날짜를 입력할 수 있는 입력 필드\
2️⃣ 달력 아이콘을 클릭했을 때 나타나는 달력 팝업

### Attribute

![](../../.gitbook/assets/cp_Attribute.png)

**Data**

* **From Year**\
  사용자가 선택할 수 있는 최소 연도를 설정하는 속성입니다.\
  이 속성을 통해 달력에서 선택 가능한 연도의 범위를 제한할 수 있습니다.
* **To Year**\
  사용자가 선택할 수 있는 최대 연도를 설정하는 속성입니다.\
  이 속성을 통해 달력에서 선택 가능한 연도의 범위를 제한할 수 있습니다.
* **Format**\
  날짜가 표시되는 형식을 설정하는 속성입니다.\
  예를 들어, "YYYY-MM-DD", "MM/DD/YYYY" 등의 형식으로 날짜를 표시할 수 있습니다.
* **Day Mode**\
  달력의 일별 모드를 설정하는 속성입니다.\
  이 모드를 통해 사용자가 일 단위 또는 달 단위로 날짜를 선택할 수 있도록 설정합니다.
  * **`Day`**: 달력을 일 단위로 설정합니다.
  * **`Month`**: 달력을 월 단위로 설정합니다.
* **Align**\
  텍스트의 정렬을 설정하는 속성입니다.\
  날짜 텍스트가 입력 필드 내에서 어떻게 정렬될지를 결정합니다.
  * **`left`**: 텍스트를 좌측으로 정렬합니다.
  * **`center`**: 텍스트를 중앙으로 정렬합니다.
  * **`right`**: 텍스트를 우측으로 정렬합니다.

### Example

**1️⃣ 레이아웃에서 생성**

```javascript

onInitDone() 
{ 
	super.onInitDone(); 
	// ACalendarPicker 초기 설정 
	this.calendarPicker.setDate(
		{ 
			year: 2023, 
			month: 10, 
			day: 15 
		}
	); 
	
	// 캘린더 아이콘을 우측에 배치
	this.calendarPicker.setCalendarIconRight();
}

// 캘린더 피커에 체인지 이벤트 추가
onCalendarPickerChange(comp, info, e)
{
	const selectedDate = comp.getDateString();
	alert("선택된 날짜: " + selectedDate);
}

```

\


**2️⃣ 코드에서 생성**

```javascript

onInitDone()
{
	super.onInitDone()

	// 사용자 함수 불러오기
	this.createCalendarPicker();
}

// 사용자 함수 생성
createCalendarPicker()
{
	// 캘린더피커 생성
	const calendarPicker = new ACalendarPicker();

	// 캘린더피커 초기화
	calendarPicker.init();
	
	// 캘린더피커 속성 설정
	
    // 캘린더피커의 초기 날짜 설정
	calendarPicker.setDate(
		{ 
			year: 2023, 
			month: 10, 
			day: 15 
		}
	); 
	
	// 캘린더 아이콘을 우측에 배치
	calendarPicker.setCalendarIconRight();
	
	// 프로그래스를 특정 컨테이너에 추가
	// 스파이더젠에서는 컴포넌트의 jQuery 객체를 사용하여 
	// DOM 조작을 수행합니다.
	this.view.$ele.append(calendarPicker.$ele);

	// 캘린더피커의 날짜 변경 이벤트 설정 
	calendarPicker.addEventListener('change', function(e) {
		 let selectedDate = calendarPicker.getDateString(); 
	 	 alert("선택된 날짜: " + selectedDate); 
	 	}
 	);
}

```
