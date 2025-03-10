스파이더젠에서 제공하는 윈도우는 다양한 옵션을 설정해서 오픈할 수 있음.  
앞에서 예제로 보였던 Modal 윈도우도 내부적으로 이 옵션들을 설정하여 오픈하는 방식임.

---

## 1. 윈도우 옵션 설정
* 윈도우를 오픈할 때 다양한 옵션들을 설정할 수 있음.  
* 아래 코드는 설정 가능한 옵션들의 예시임.

```js
wnd.setWindowOption({
    isModal: true,               // 모달로 띄울지 여부 (true: 모달, false: 모달 아님)
    isCenter: true,              // 윈도우를 자동으로 중앙 정렬할지 여부
    isFocusLostClose: false,     // 모달인 경우 포커스를 잃을 때 창을 닫을지 여부
    isFocusLostHide: false,      // 모달인 경우 포커스를 잃을 때 창을 숨길지 여부
    modalBgOption: 'dark',       // 모달인 경우 배경의 어둡기 정도 ('none', 'light', 'dark')
    overflow: 'hidden',          // 윈도우의 오버플로우 설정 ('hidden', 'auto', 'visible', 'scroll')
    dragHandle: null,            // 드래그 핸들이 될 클래스명이나 아이디 (예: '.windowHandle' or '#windowHandle')
    isResizable: true,           // 윈도우 창을 리사이즈 가능하게 할지 여부
    isDraggable: true,           // 윈도우 창을 드래그로 움직이게 할지 여부
    inParent: false,             // 부모 컨테이너 안에 창을 띄울 경우, 항상 부모보다 위에 보이게 할지 여부
    focusOnInit: true,           // 초기화될 때 자동으로 윈도우의 첫 번째 컴포넌트에 포커스를 줄지 여부
    activePropagation: true      // 윈도우가 닫힐 때 활성화되는 컨테이너의 active 호출 여부
});
```

---

## 2. 컴포넌트 배치 
* View에 새로운 **AButton** 컴포넌트를 추가함.  
* 추가한 버튼의 텍스트를 **"Window Option"** 으로 설정함.

---

## 3. 버튼 이벤트 연결
* **"Window Option"** 버튼의 Click 이벤트 함수를 다음과 같이 작성함.

```
function MainView:onAButton4Click(comp, info, e) 
{ 
    const wnd = new AWindow('option-window'); 

    // 윈도우의 옵션을 설정한다.
    wnd.setWindowOption({ 
        isModal : true,             // 모달 여부 
        isCenter : true,             // 화면 가운데 위치 여부 
        isFocusLostClose : true,     // 윈도우 밖의 화면 클릭 시 닫히는 여부 
        modalBgOption : 'light'       // 배경 옵션 설정
    }); 

    // url, parent, top, left, width, height 순서대로 지정함.
    wnd.open('Source/Views/WinView.lay', this.getContainer(), 0, 0, 300, 300); 
};
```

---

## 4. 빌드 및 실행 (Window Option 테스트)
* 프로젝트를 빌드 후 실행함.  
* **"Window Option"** 버튼을 클릭하여 윈도우를 열어봄.  
* isModal, isCenter, modalBgOption 등 옵션 값을 변경하면서 동작 방식을 확인함.
  - isFocusLostClose가 true일 경우, 윈도우 밖을 클릭하면 창이 닫힘.
  - modalBgOption이 light일 경우, 창 뒤로 밝은 투명 배경이 적용됨.