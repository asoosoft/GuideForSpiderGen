# TextArea

![](https://wikidocs.net/images/page/24785/textarea-comp-00.png)

**텍스트에어리어(ATextArea)** 는 여러 줄의 텍스트를 입력할 수 있는 텍스트 입력기 컴포넌트입니다.\


> 텍스트에어리어는 다양한 속성과 옵션을 제공하여 텍스트의 표시 및 입력 방식을 제어할 수 있습니다.

### Attribute

![](https://wikidocs.net/images/page/24785/ta_Attribute.png)

**Data**

* **Text**\
  텍스트 값을 설정하는 속성입니다.
* **Placeholder**\
  텍스트 에어리어에 아무런 값이 입력되지 않았을 때 표시되는 플레이스홀더 텍스트를 설정하는 속성입니다.
* **Align**\
  텍스트의 정렬을 설정하는 속성입니다.
  * **`left`** : 텍스트를 좌측으로 정렬합니다.
  * **`center`** : 텍스트를 중앙으로 정렬합니다.
  * **`right`** : 텍스트를 우측으로 정렬합니다.
* **Alt**\
  텍스트 영역의 대체 텍스트를 설정하는 속성입니다.\
  주로 이미지가 로드되지 않을 때 대체 텍스트로 사용됩니다.
* **IME**\
  텍스트 입력 모드(국문/영문)를 설정하는 속성입니다. (IE 브라우저만 가능)
  * **`none`** : 입력 모드를 설정하지 않고 현재 로컬 상태를 그대로 사용합니다.
  * **`english`** : 영문 입력 모드로 설정합니다.
  * **`korean`** : 국문 입력 모드로 설정합니다.

### Example

텍스트 에어리어는 사용자로부터 긴 텍스트 입력을 받을 때 유용하며,\
예를 들어 메모장, 댓글 입력란, 설명 입력 필드 등 다양한 상황에서 활용될 수 있습니다.\
사용자는 텍스트를 입력하고, 필요에 따라 텍스트의 정렬이나 플레이스홀더를 설정하여 사용자 경험을 향상시킬 수 있습니다.

**1️⃣ 컴포넌트 배치**

**layout 파일을 오픈하고 아래 내용으로 컴포넌트를 배치합니다.**

| component  | id        | text | playcehold |
| ---------- | --------- | ---- | ---------- |
| ATextField | textField |      | 내용을 입력하세요. |
| ATextArea  | textarea  |      | -          |
| AButton    | button    | 추가   | -          |

![](https://wikidocs.net/images/page/24785/ta_ex1.png)

**2️⃣ 이벤트 설정**

**버튼에 클릭 이벤트를 설정하고 아래와 같이 작성합니다.**

```javascript
  
onButtonClick(comp, info, e) 
{ 
 
    let text = this.textField.getText(); 
 
    if(!text || txt.text < 1){ 
        AToast.show('추가할 내용을 입력하세요.');         
        return; 
    } 
 
    // 텍스트에어리어의 있던 기존의 텍스트에 
    // 텍스트필드에 입력한 텍스트 추가 
    this.textarea.setText( 
        this.textarea.getText() + '\n' + this.textField.getText() 
    ); 
 
    // 텍스트 추가 후 입력받는 텍스트필드 값 초기화 
    this.textField.setText(''); 
 
};  
 
```

**3️⃣ 실행**

**F5 키를 이용해서 빌드하고 실행합니다.**

1. 텍스트필드에 값을 입력하지 않고 추가 버튼을 클릭해서 메시지 토스트를 확인합니다.
2. 텍스트를 입력하고 추가 버튼을 클릭해 봅니다.\
   TextArea 컴포넌트 영역에 입력하는 텍스트가 잘 추가되는지 확인합니다.
3. 마지막으로 지금까지 입력된 내용 다음에 TextArea에 직접 입력을 해봅니다.
