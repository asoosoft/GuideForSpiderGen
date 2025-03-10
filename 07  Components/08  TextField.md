![](https://wikidocs.net/images/page/24782/tf.png) 

**텍스트필드(ATextField)** 는 사용자가 문자를 입력할 수 있는 기본적인 입력 컴포넌트입니다. <br />
>텍스트필드는 다양한 속성과 옵션을 제공하여 사용자 입력을 제어하고, 입력된 데이터를 처리할 수 있도록 합니다.

## Attribute

![](https://wikidocs.net/images/page/24782/tf_Attribute.png)

#### **1️⃣ Data**

-   **Text**   
    텍스트 필드에 입력된 텍스트 값을 설정하거나 가져오는 속성입니다.
    
-   **Placeholder**   
    텍스트 필드에 아무런 값이 입력되지 않았을 때 표시되는 플레이스홀더 텍스트를 설정하는 속성입니다.
    
- **Data Type**<br />
      텍스트 필드의 데이터 타입을 설정하는 속성입니다.
      
	-   **`text`** : 일반 텍스트 입력이 가능합니다.
	-   **`search`** : 검색 필드로, 특정 브라우저에서 클리어 버튼이 노출됩니다.
	-   **`password`** : 입력 내용을 숨김 처리하여 비밀번호 입력에 사용됩니다.
	-   **`number`** : 숫자만 입력이 가능합니다.
	-   **`email`** : 이메일 주소 형식으로만 입력이 가능합니다.
	-   **`tel`** : 전화번호 형식으로 입력이 가능합니다.
	-   **`file`** : 파일 입력이 가능합니다.
	
	
 - **Align**<br />
      텍스트의 정렬을 설정하는 속성입니다.
      
	-   **`left`** : 텍스트를 좌측으로 정렬합니다.
	-   **`center`** : 텍스트를 중앙으로 정렬합니다.
	-   **`right`** : 텍스트를 우측으로 정렬합니다.

  - **MaxLength**<br />
      입력 가능한 텍스트의 최대 길이를 설정하는 속성입니다.

  - **IME**<br />
      텍스트 입력 모드(국문/영문)를 설정하는 속성입니다. (IE 브라우저만 가능)
      
	-   **`none`** : 입력 모드를 설정하지 않고 현재 로컬 상태를 그대로 사용합니다.
	-   **`english`** : 영문 입력 모드로 설정합니다.
	-   **`korean`** : 국문 입력 모드로 설정합니다.

----------

#### **2️⃣ Option**

-   **TimerChange**   
    기본 0.2초마다 change 이벤트가 발생하게 만드는 옵션입니다.
    -모바일에서 텍스트 입력시, 변경 이벤트 발생하는 용도.
    
-   **FocusSelection**   
    포커스 될 때 셀렉션(블락) 영역을 잡아주는 옵션입니다.
    
- **AutoTab**<br />
      값만큼 입력하는 경우 다음 탭으로 자동 이동시켜주는 옵션입니다.


## Example

  텍스트필드에 입력된 값을 다른 컴포넌트에 표시하거나, 특정 조건에 따라 동작을 수행하도록 이벤트를 설정할 수 있습니다.

 #### .js를 사용해 **Attribute 내용**을 설정하는 경우
 
```javascript
onInitDone()
{
	super.onInitDone()

	// 예시 1. 기본 텍스트 설정
	this.textFieldId.setText('기본 텍스트 설정');
	
	// 예시 2. 플레이스홀더 설정
	this.textFieldId.setPlaceholder('여기에 입력하세요');
	
	// 예시 3. 숫자 입력 전용 텍스트필드
	this.textFieldId.setDataType('number');
	
	// 예시 4. 최대 입력 길이 설정
	this.textFieldId.setMaxLength(10);
	
	// 예시 5. 포커스 시 텍스트 자동 선택
	this.textFieldId.setOption('FocusSelection', true);
}
```

-----------

#### 예시 1️⃣

![](https://wikidocs.net/images/page/24782/tf_ex1.png)
<br />

1️⃣ **컴포넌트 생성**<br>
> ATextField 컴포넌트를 생성한 후 생성한 ATextField를 클릭

2️⃣ **이벤트**<br>
> ① Class Pane > Event에서 change 우측 빈 공간 더블클릭
>
> ② 함수명 지정 (또는 기본 함수명 사용) 후 확인 클릭<br>
> 
> ③ 함수 안에 밑의 예제 코드를 작성합니다.<br>
```javascript
	onATextField1Change(comp, info, e)
	{
		let text =  this.textfield.getText();
		console.log(text);
	}
```
![](https://wikidocs.net/images/page/24782/tf_ex1_result.png)

텍스트필드의 값이 변할 때마다 텍스트를 받아와 이를 콘솔에 출력

-----------

#### 예시 2️⃣ <br />

> 위 예시 1에서 이어지는 예시 입니다.

![](https://wikidocs.net/images/page/24782/tf_ex2.png)

1️⃣ **컴포넌트 추가**<br>
> 위 예시에서 AButton 컴포넌트를 추가합니다.

2️⃣ **이벤트 설정**<br>
> 생성한 AButton 컴포넌트를 클릭한 후 Click Event를 설정합니다.

3️⃣ **코드 작성**<br>
> 다음과 같이 예제 코드를 작성합니다.

```javascript
	onResetClick(comp, info, e)
	{
		// reset() 함수 사용예시
		this.textfield.reset();
	}
``` 
4️⃣ **결과**

> 결과화면에서 텍스트필드에 값을 입력 후 버튼을 누르면 텍스트필드에 입력한 값이 지워지는 결과를 볼 수 있습니다.