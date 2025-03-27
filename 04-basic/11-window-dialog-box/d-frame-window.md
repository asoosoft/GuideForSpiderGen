# D. Frame Window

**Frame Window**는 상단에 타이틀바와 최대화, 최소화, 닫기 버튼을 가지고 있으며, 하단에는 상태바를 포함하고 있음.

***

### 1. Framework 추가

* 프로젝트 시작 전에 필요한 Framework를 준비함.
  * afc 폴더에 **AFrameWnd.js** 컴포넌트를 추가함.

![](../../.gitbook/assets/Window004.png)

***

### 2. 컴포넌트 배치

* View에 새로운 **AButton** 컴포넌트를 추가함.
* 추가한 버튼의 텍스트를 **"Frame Window"** 로 설정함.

***

### 3. 버튼 이벤트 연결

* **"Frame Window"** 버튼의 Click 이벤트 함수를 아래와 같이 작성함.

```javascript
onFrameWindowClick(comp, info, e) {
    const wnd = new AFrameWnd('frame window');
    wnd.open('Source/WinView.lay', this.getContainer(), 0, 0, 100, 300);
}
```

***

### 4. 빌드 및 실행 (Frame Window 테스트)

* 프로젝트를 빌드 후 실행함.
* 메인 화면에서 **Frame Window** 버튼을 클릭하면, 상단에 프레임과 타이틀이 표시되는 윈도우가 열림.
* 윈도우 프레임 부분을 마우스 오른쪽 버튼으로 드래그하면 창을 이동할 수 있음.
* 프레임 우측에 있는 최소화, 최대화, 닫기 버튼을 각각 클릭하여 기능을 확인함.

![](../../.gitbook/assets/Frame_Window.png)
