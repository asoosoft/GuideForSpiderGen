# SwitchButton

![](../../.gitbook/assets/switchbtn-comp-00.png)

\
\*\*스위치 버튼 (SwitchButton)\*\* 는 사용자가 on/off 상태를 전환할 수 있는 컴포넌트입니다.\
\>SwitchButton 요소를 사용하여 클릭이 가능한 스위치 버튼(SwitchButton) 을 만듭니다.\
사용자가 스위치 버튼(SwitchButton) 을 클릭하면 on/off 상태에 설정해둔 이벤트가 트리거 됩니다.

### 스위치 버튼(SwitchButton) 만들기 

UI 또는 JavaScript 로 스위치 버튼(SwitchButton)을 만들 수 있습니다.\


### Appearance

![](../../.gitbook/assets/switchbtn-ex-002.png)

**style**

* **default** 스위치 버튼의(SwitchButton) on/off 상태의 스타일을 지정합니다\

* **On** 스위치 버튼이(SwitchButton) On상태일때 스타일을 지정합니다.\

* **Off** 스위치 버튼이(SwitchButton) Off상태일때 스타일을 지정합니다.\


**Data**

* **Text**텍스트를 작성하는 공간입니다.
* **H-Align**텍스트의 수평 정렬을 설정하는 속성입니다.
* **v-Align**텍스트의 수직 정렬을 설정하는 속성입니다.
* **text-Align**텍스트 콘텐츠의 정렬을 설정하는 속성입니다일반적으로 H-Align과 유사한 기능을 제공하며, 텍스트가 포함된 요소 내에서의 정렬을 지정합니다.

### Example

스위치 버튼(SwitchButton)은 사용자가 On과 Off 상태를 전환할 수 있도록 설계된 UI 요소입니다. 주로 설정 페이지, 기능 활성화/비활성화, 또는 간단한 사용자 선택을 요구하는 상황에서 사용됩니다.

**1.컴포넌트를 배치합니다.**

| component     | id      | text       |
| ------------- | ------- | ---------- |
| ATextBox      | textBox | 1번 텍스트입니다. |
| ASwitchButton | switch  |            |

![](../../.gitbook/assets/switchbtn-ex-01.png)

**2. 이벤트 연결**

* 확인 버튼에 Click 이벤트 설정하고 설정한 함수 내용은 아래와 같이 수정합니다.

```
	onASwitchButton1Change(comp, info, e)
	{

        if(!this.switch.getValue())
        {
            this.textBox.setText("1번 텍스트입니다.");

        } else 
        {
            this.textBox.setText("2번 텍스트입니다.");
        }

	}
```

**3.빌드실행 합니다.**

* 스위치 버튼을 좌측 스위치 상태에서 버튼 클릭 메시지 확인. 우측 상태로 스위칭하고 메시지를 확인합니다.

![](../../.gitbook/assets/switchbtn-ex-02.png)

### 다음 예제는 JavaScript를 사용하여 스위치 버튼(SwitchButton)을 만듭니다.

**1. Framework를 추가합니다.**

* Framework의 afc에 에서 ASwitchButton/ATextBox/ASwitchButtonEvent/ATextBoxEvent를 추가합니다.

> 컴포넌트를 코드로 추가할 때는 컴포넌트(componet)와 이벤트(event)를 둘 다 추가해야 합니다.

![](../../.gitbook/assets/switchbutton-ex-05.png)

**2.코드를 추가합니다.**

```
    onInitDone() {
        super.onInitDone();
        this.createSwitchButton();
    }

    createSwitchButton() {
        // 스위치 버튼 생성 및 초기화
        this.switchButton = new ASwitchButton(); // switchButton 생성
        this.switchButton.init(); // switchButton 초기화

        // 스위치 버튼 설정
        this.switchButton.setSize(100, 50);
        this.switchButton.setPos(50, 50);
        this.switchButton.setSwitchOnStyle({ backgroundColor: 'green' });
        this.switchButton.setSwitchOffStyle({ backgroundColor: 'red' });
        

        // 스위치 버튼을 메인 뷰에 추가
        this.addComponent(this.switchButton);
        

        // 스위치 버튼의 상태 변경 이벤트 리스너 추가
        this.switchButton.addEventListener('change', this,'onASwitchButtonChange');


        // 텍스트 박스 생성 및 초기화
        this.textBox = new ATextBox();
        this.textBox.init();
        this.textBox.setSize(200, 30);
        this.textBox.setPos(50, 120);
        this.textBox.setText("1번 텍스트입니다.");

        // 텍스트 박스를 메인 뷰에 추가
        this.addComponent(this.textBox);
    }

    onActiveDone(isFirst) {
        super.onActiveDone(isFirst);
        
    }

    onASwitchButtonChange(comp, info, e) {
        
        if (!this.switchButton.getValue()) {
            this.textBox.setText("1번 텍스트입니다.");
        } else {
            this.textBox.setText("2번 텍스트입니다.");
        }
    }

```

**3.빌드실행 합니다.**

* 버튼을 눌러서 내용이 바뀌는지 확인합니다

![](../../.gitbook/assets/switchbtn-ex-01.png) ![](../../.gitbook/assets/switchbtn-ex-02.png)
