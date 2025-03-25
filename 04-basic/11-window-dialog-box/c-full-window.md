# C  Full Window

윈도우는 애플리케이션 내에서 추가 정보를 보여주거나 별도의 작업을 수행할 수 있는 UI 요소임.\
Full Window 기능은 일반적인 윈도우 오픈 방식과 동일하게 동작하지만, 윈도우의 크기를 픽셀이 아닌 `%` 단위로 설정하여 부모 컨테이너의 전체 영역을 채우도록 하는 기능임.

***

### 1. 컴포넌트 배치

* View에 새로운 **AButton** 컴포넌트를 추가함.
* 추가한 버튼의 텍스트를 **"Full Size Window"** 로 설정함.

***

### 2. 버튼 이벤트 연결

* **"Full Size Window"** 버튼의 Click 이벤트 함수를 아래와 같이 작성함.

```javascript
onFullSizeWindowClick(comp, info, e) {
    // AWindow 인스턴스 생성
    const wnd = new AWindow();

    // 윈도우 오픈: viewUrl, parent, left, top, width, height
    // 좌측 상단(0, 0)에서 시작하며, 폭과 높이를 각각 '100%'로 지정하여 전체 화면을 채움
    wnd.open('Source/FullWinView.lay', this.getContainer(), 0, 0, '100%', '100%');
}
```

***

### 3. 화면 생성 및 구성

* **Full Size Window View**의 화면으로 사용할 View를 추가 생성함.
* 전체 화면에 어울리는 배경색을 지정함.
* 사용자가 **Full Size Window**를 종료할 수 있도록 “닫기” 버튼 컴포넌트를 추가함.
* “닫기” 버튼의 Click 이벤트에 아래와 같이 코드를 작성

```javascript
onAButtonClick(comp, info, e) {
    this.getContainer().close();
}
```

***

### 4. 빌드 및 실행 (Full Size Window)

* 프로젝트를 빌드 후 실행함.
* 메인 화면에서 **Full Size Window** 버튼을 클릭하면, 전체 화면을 채우는 Full Size Window가 표시됨.
* Full Size Window 내부의 **닫기** 버튼을 클릭하면, 윈도우가 정상적으로 종료됨.

![](https://wikidocs.net/images/page/24899/Full_Size_Window.png)
