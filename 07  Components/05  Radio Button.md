# 05  Radio Button

![](https://wikidocs.net/images/page/24700/RadioButton.png)

사용자가 여러 옵션 중 하나를 선택할 수 있도록 하는 **라디오 버튼 컴포넌트**

> `ARadioGroup` 내에 배치되어 그룹으로 관리되며, 그룹 내에서 하나의 버튼만 선택 가능.

### Data

![](https://wikidocs.net/images/page/24701/RadioButton_Attribute.png)

| Data        | 설명                                     |
| ----------- | -------------------------------------- |
| `Text`      | 라디오버튼의 텍스트를 설정                         |
| `Align`     | 라디오버튼의 텍스트 정렬을 설정(left, center, right) |
| `Check Pos` | 라디오버튼의 체크 위치를 설정(left, right)          |
| `Value`     | 라디오버튼의 보유값을 설정                         |

### Example

> #### 남자,여자 라디오 버튼을 추가하고, 클릭 된 버튼의 텍스트 값을 화면에 출력하기

#### \[1. 툴을 이용하는 방법]

**1-1. RadioGroup 을 추가**

![](https://wikidocs.net/images/page/24700/%ED%99%94%EB%A9%B4_%EC%BA%A1%EC%B2%98_2025-01-23_091408.png)

![](https://wikidocs.net/images/page/24700/%ED%99%94%EB%A9%B4_%EC%BA%A1%EC%B2%98_2025-01-23_091347.png)

**1-2. RadioGroup 내 라디오버튼을 각각 추가 후 Label 추가**

![](https://wikidocs.net/images/page/24700/%ED%99%94%EB%A9%B4_%EC%BA%A1%EC%B2%98_2025-01-23_092415_YBg4s7F.png)

`Label id = lbl001`

**1-3. 각 라디오버튼에 클릭 이벤트 설정**

![](https://wikidocs.net/images/page/24700/%ED%99%94%EB%A9%B4_%EC%BA%A1%EC%B2%98_2025-01-23_095038.png)

`함수명 = onARadioButtonsClick`

```js
 onARadioButtonsClick(comp, info, e) 
{ 
    //선택되었을 경우 
    if(comp.getSelect()) 
    { 
        this.lbl001.setText(comp.getText());     
    }     
}; 
 
```

**1-4. 실행 후 결과 확인**

![](https://wikidocs.net/images/page/24700/%ED%99%94%EB%A9%B4_%EC%BA%A1%EC%B2%98_2025-01-23_100152.png)

#### \[2. 코드로 추가하는 방법]

```js
// 라디오 그룹 생성 
const radioGroup = new ARadioGroup();
this.addComponent(radioGroup); 

// 남자 라디오 버튼 생성 
const maleRadio = new ARadioButton(); 
maleRadio.setText("남자"); 
radioGroup.addComponent(maleRadio); 

// 여자 라디오 버튼 생성 
const femaleRadio = new ARadioButton(); 
femaleRadio.setText("여자"); 
radioGroup.addComponent(femaleRadio); 

// 라벨 생성 
const label = new ALabel(); 
label.setText("선택된 성별: "); 
this.addComponent(label); 

// 라디오 버튼 클릭 이벤트 설정 
onRadioButtonClick(comp, info, e) {
	if (comp.getSelect()) { 
		label.setText("선택된 성별: " + comp.getText()); 
		} 
	} 

// 이벤트 함수 매핑 
maleRadio.addEventListener('click', onRadioButtonClick);
femaleRadio.addEventListener('click', onRadioButtonClick); 

```
