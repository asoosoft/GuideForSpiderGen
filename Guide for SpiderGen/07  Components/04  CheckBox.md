# CheckBox

![](../../.gitbook/assets/checkBox.png)

**체크박스(ACheckBox)** 는 사용자가 선택할 수 있는 옵션을 제공하는 컴포넌트입니다.\


> 체크박스는 여러 개의 옵션 중에서 하나 이상을 선택할 수 있도록 하며, 각 체크박스는 개별적으로 선택되거나 해제될 수 있습니다.

### Attribute

![](../../.gitbook/assets/checkBox_Attribute.png)

**1️⃣ Data**

* **Text**\
  체크박스의 텍스트를 설정하는 속성입니다.
* **Align**\
  텍스트 정렬을 설정하는 속성입니다.
  * **`left`** : 텍스트를 좌측으로 정렬합니다.
  * **`center`** : 텍스트를 중앙으로 정렬합니다.
  * **`right`** : 텍스트를 우측으로 정렬합니다.
* **Check Pos**\
  체크박스의 위치를 텍스트 기준으로 설정합니다.
  * **`left`** : 체크박스를 텍스트 좌측에 위치시킵니다.
  * **`right`** : 체크박스를 텍스트 우측에 위치시킵니다.

***

**2️⃣ Value**

* **`Check`** : 체크 상태의 값을 설정합니다.
* **`Uncheck`** : 체크 해제 상태의 값을 설정합니다.
* **`setcheck`** : 기본값을 체크 상태로 설정합니다.

### Example

> 1번 예제

**1️⃣ 컴포넌트 배치**

**layout에 다음 내용을 참고해서 컴포넌트를 배치합니다.**

| component | id       | text | value |
| --------- | -------- | ---- | ----- |
| ALabel    | label    | 체크값  |       |
| AButton   | button   | 확인   |       |
| ACheckBox | checkBox | 사과   | 200   |

![](../../.gitbook/assets/checkBox_ex1_re.png)

**2️⃣ 클릭 이벤트 설정**

**버튼 컴포넌트에 클릭 이벤트를 설정합니다.**

```javascript

onButtonClick(comp, info, e)
{
	const checkBox_value = this.checkBox.getValue();

	// 체크박스가 체크된 상태일 때
	if (this.checkBox.isChecked) {
		this.label.setText(checkBox_value);
	}
}

```

**3️⃣ 실행**

**F5 키를 누르거나 Build > Run Project를 실행합니다.**

* 실행된 화면에서 체크박스를 선택하고 확인버튼을 클릭합니다.
* 레이블에 선택된 체크박스의 Value 값을 출력하는걸 확인합니다.

![](../../.gitbook/assets/checkBox_result_re.png)

> 2번 예제
>
> 체크박스에 직접 이벤트를 주는 경우

```javascript

// 체크박스 클릭 이벤트
onCheckBoxChange(comp, info, e)
{
	this.label.setText(comp.getValue());
}

```

> 3번 예제
>
> 체크박스를 코드로 만드는 경우

```javascript

onInitDone()
{
	super.onInitDone()

	// 사용자 함수 불러오기
	this.createCheckBox();
}

// 사용자 함수 생성
createCheckBox()
{
	// 체크박스 생성
	const checkBox = new ACheckBox();

	// 체크박스 초기화
	checkBox.init();
	
	// 체크박스 속성 설정

	// 체크박스 옆에 표시될 텍스트 설정
	checkBox.setText("동의합니다");  
    // 체크박스의 값 설정
	checkBox.setValue("agree"); 
	// 기본적으로 체크 상태로 설정
	checkBox.setCheck(true);  

	// 체크박스의 정렬 설정
	
	// 체크박스를 텍스트의 왼쪽에 위치
	checkBox.setCheckAlign("left");  
	
	// 체크박스를 특정 컨테이너에 추가
	// 스파이더젠에서는 컴포넌트의 jQuery 객체를 사용하여 
	// DOM 조작을 수행합니다.
	this.view.$ele.append(checkBox.$ele);

	// 체크박스의 클릭 이벤트 설정
	checkBox.addEventListener('click',  function(e)  {
		if  (checkBox.getCheck())  {
			alert("체크박스가 선택되었습니다.");
		}  else  {
			alert("체크박스가 선택 해제되었습니다.");
		}
	});
}

```
