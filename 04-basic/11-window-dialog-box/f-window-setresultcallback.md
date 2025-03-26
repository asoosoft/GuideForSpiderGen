# F. Window setResultCallback

**setResultCallback** 메서드는 스파이더젠에서 윈도우가 닫힌 후 특정 작업을 수행하기 위해 콜백 함수를 설정하는 기능을 제공함.\
이 메서드를 사용하면 윈도우가 닫힐 때 원하는 동작을 정의할 수 있으며, 닫힐 때 전달된 결과값과 데이터를 콜백 함수로 받을 수 있음.

***

### 1. 컴포넌트 배치

* View에 아래와 같이 컴포넌트들을 배치함.

| component | id      | text |
| --------- | ------- | ---- |
| AButton   |         | X    |
| ATextArea | txtData |      |
| AButton   |         | 내용추가 |

![](../../.gitbook/assets/WindowsetResultCallback01.png)

***

### 2. 멤버 변수 추가

* DataWindow 클래스에 멤버 변수를 추가함.

```javascript
class DataWindow extends AView {
    constructor() {
        super();
        this.data = null;
    }
}
```

***

### 3.버튼 이벤트 연결

* **'X' 버튼 이벤트**

버튼 클릭 시 동작할 이벤트 함수를 아래와 같이 작성함.

```javascript
onXClick(comp, info, e) {
    this.getContainer().close(1, this.data);
}
```

* **'내용추가' 버튼 이벤트**

버튼 클릭 시 동작할 이벤트 함수를 아래와 같이 작성함.

```javascript
onAddClick(comp, info, e) {
    this.data = this.txtData.getText();
}
```

***

### 4. 데이터 세팅

* 윈도우가 활성화될 때, 다른 화면(예: MainView)에서 전달한 데이터를 아래와 같이 세팅함.

```javascript
onActiveDone(isFirst) {
    super.onActiveDone(isFirst);
    let gData = this.getContainer().getData();
    if (gData) {
        this.data = gData;
        this.txtData.setText(this.data);
    }
}
```

> getContainer().getData() : 다른 화면(예: MainView)에서 wnd.setData(...)로 보낸 데이터를 수신함.

***

### 5. 다른 화면에서 윈도우 열기 & 콜백 처리

* 메인 화면에 **setResultCallback** 버튼을 추가한 후, 클릭 이벤트를 설정하여 DataWindow를 모달로 열고, 닫힐 때 받은 데이터를 Label에 출력함.

```javascript
onSetResultCallbackClick(comp, info, e) {
    const wnd = new AWindow('callback-window');
    const self = this;
    // url, parent, width, height 순서대로 지정함.
    wnd.openAsDialog('Source/DataWindow.lay', this.getContainer(), 400, 400);
    
    // 윈도우에 데이터를 전송(설정)
    wnd.setData('MainView에서 DataWindow에 텍스트를 전달합니다.');
    
    // 윈도우가 Close 될 때 자동 호출되는 함수 정의
    wnd.setResultCallback(function (result, data) {
        self.text.setData(data);
    });
}
```

> wnd.setData(...) : 열리는 윈도우에 데이터를 미리 전달\
> wnd.setResultCallback(...) : 윈도우가 닫힐 때 자동 호출되는 함수 정의\
> result, data : close() 시점에 전달한 인자

***

### 6. 컴포넌트 배치 (Label 추가)

* 메인 화면에 Label 컴포넌트를 추가하고, id를 **text** 로 설정함.
* 구분을 위해 Label 에 텍스트 추가(예 :내용 전달 받는 곳)

![](../../.gitbook/assets/WindowsetResultCallback03.png)

***

### 7. 실행 후 동작 확인

* **setResultCallback** 버튼을 클릭하여 DataWindow를 열음.
* 텍스트 영역에 내용을 입력하고 **내용추가** 버튼을 눌러 this.data에 저장함.
* **X** 버튼을 눌러 윈도우를 닫음.
* 메인 화면의 Label(text)에 입력했던 내용이 표시되는지 확인함.

![](../../.gitbook/assets/WindowsetResultCallback02.png)
