# A  Modal Modeless Window

Modal 윈도우는 사용자가 해당 윈도우를 닫기 전까지 다른 작업을 할 수 없도록 제한함.\
사용자에게 중요한 정보를 전달하거나 입력을 받을 때 주로 사용함.\
Modal 윈도우가 열리면 사용자는 이 윈도우와의 상호작용이 완료될 때까지 다른 UI 요소와 상호작용할 수 없음.

Modeless 윈도우는 사용자가 해당 윈도우를 열어둔 상태에서도 다른 작업을 계속할 수 있음.\
보조적인 정보를 제공하거나 추가적인 기능을 제공할 때 유용함.\
Modeless 윈도우는 사용자가 다른 UI 요소와 상호작용할 수 있도록 허용하며, open 메서드를 사용해 생성할 수 있음.

***

### 1. Framework 추가

* 프로젝트 시작 전에 필요한 기능들을 준비함.
  * 메시지(알림창)를 간단히 띄우기 위해 afc 폴더에 **AToast.js** 파일을 추가함.
  * 이후 코드에서 `AToast.show("메시지")` 처럼 바로 알림창을 표시할 수 있음.

![](https://wikidocs.net/images/page/24886/Window01.png)

***

### 2. 컴포넌트 배치 (Modeless 창)

* View에 아래와 같이 버튼 두 개를 배치함.

| component | text                   |
| --------- | ---------------------- |
| AButton   | Window Open (modeless) |
| AButton   | Click!!!!              |

![](https://wikidocs.net/images/page/24886/Window0001.png)

* Window로 사용할 새로운 View(예: WindowView)를 생성함.
* 생성한 View에 배경 색상을 설정함.
* "닫기" 텍스트의 버튼 컴포넌트를 추가함.
* 닫기 버튼에 Click 이벤트를 연결한 후 아래 코드를 작성함.

![](https://wikidocs.net/images/page/24886/Window0003.png)

```js
onAButtonClick(comp, info, e) {
    this.getContainer().close();
}
```

***

### 3. 버튼 이벤트 연결

* **Window Open (modeless) 버튼 이벤트 연결**

```
onWindowOpenmodelessClick(comp, info, e) {
// 윈도우 생성함.
const wnd = new AWindow();
// 윈도우 오픈: viewUrl, parent, left, top, width, height 순서대로 지정함.
wnd.open('Source/WinView.lay', this.getContainer(), 50, 250, 200, 200);
}
```

* **new AWindow()** 를 통해 윈도우 인스턴스를 생성함.
* **open()** 메서드를 호출하여 화면을 띄움.
* **Click!!!! 버튼 이벤트 연결**

```

onClickItClick(comp, info, e) {
AToast.show("Click!!!!");
  }
```

* **Window Open (Modal) 버튼 이벤트 연결**

```
  onWindowOpenModalClick(comp, info, e) {
      // 윈도우 생성함.
      const wnd = new AWindow();
      // 모달 옵션 설정함.
      wnd.setWindowOption({
          isModal: true,
          modalBgOption: 'light'
      });
      // 윈도우 오픈: viewUrl, parent, left, top, width, height 순서대로 지정함.
      wnd.openAsDialog('Source/WinView.lay', this.getContainer(), 300, 300);
  }
```

* **setWindowOption()** 을 통해 모달 옵션(배경, 모달 여부 등)을 설정함.
* **openAsDialog()** 호출 시, 모달 창이 열려 기존 화면 조작이 차단됨.

***

### 4. 빌드 및 실행 (Modeless)

* 프로젝트를 빌드 후 실행함.
* **"Window Open (modeless)"** 버튼을 클릭하면 새로운 윈도우가 열림.
* **"Click!!!!"** 버튼을 클릭하면 "Click!!!!" 알림창이 표시됨.
* 윈도우 안의 **"닫기"** 버튼을 클릭하면 창이 닫힘.

![](https://wikidocs.net/images/page/24886/Window0002.png)\
![](https://wikidocs.net/images/page/24886/Window0004.png)

***

### 5. 컴포넌트 배치 (Modal 창 추가)

* View에 새로운 **AButton** 컴포넌트를 추가함.
* 추가한 버튼의 텍스트를 **"Window Open (Modal)"** 로 설정함.
* 최종적으로 View에 배치된 버튼 목록은 아래와 같음.

| component | text                   |
| --------- | ---------------------- |
| AButton   | Window Open (modeless) |
| AButton   | Window Open (Modal)    |
| AButton   | Click!!!!              |

***

### 6. 빌드 및 실행 (Modal)

* 프로젝트를 빌드 후 실행함.
* **"Window Open (Modal)"** 버튼을 클릭하면 모달 창이 열림.
* 모달 창이 활성화된 동안에는 기존 화면의 다른 컴포넌트(예: **"Click!!!!"** 버튼)의 조작이 차단됨.

![](https://wikidocs.net/images/page/24886/Window0005.png)
