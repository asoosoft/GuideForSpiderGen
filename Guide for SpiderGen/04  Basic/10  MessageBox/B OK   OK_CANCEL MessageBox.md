# B OK   OK\_CANCEL MessageBox

`AMessageBox.OK`는 단일 버튼 메시지 박스 타입으로, 오직 "OK" 버튼만 제공함.\
이 타입은 사용자가 정보를 단순히 확인한 후 진행할 때 유용함.\
반면, `AMessageBox.OK_CANCEL`은 두 개의 버튼, "OK"와 "CANCEL"을 제공하는 메시지 박스 타입임.\
이 타입은 사용자가 제시된 선택지 중 하나를 선택하여 진행 여부를 결정해야 하는 상황에 적합함.

***

### 1. Framework 추가

* 프로젝트를 시작하기 전에 필요한 기능들을 준비함.
  * MessageBox를 사용하기 위해 `AMessageBox.js` 파일을 afc 폴더에 추가함.
  * 메시지(알림창)를 간단히 띄우기 위해 afc 폴더에 `AToast.js` 파일을 추가함.
  * 이후 코드에서 `AToast.show("메시지")`처럼 바로 알림창을 표시할 수 있음.

![](https://wikidocs.net/images/page/275962/MessageBox.png)

***

### 2. 컴포넌트 배치

* View에 아래와 같이 버튼들을 배치함.

| component | text       |
| --------- | ---------- |
| AButton   | OK         |
| AButton   | OK\_CANCEL |

![](https://wikidocs.net/images/page/275962/OKMessageBox01.png)

***

### 3. 버튼 이벤트 연결

* **OK** 버튼의 Click 이벤트 함수를 아래와 같이 작성함.

```javascript
onOKClick(comp, info, e) {
    let msgBox = new AMessageBox();
    msgBox.openBox(
        null,                     // 부모 컨테이너 (null: 최상위)
        "확인",                  // 제목 (MessageBox의 타이틀)
        "작업이 완료되었습니다.",  // 내용 (표시될 메시지)
        AMessageBox.OK,           // 버튼 타입 (OK 버튼만 표시)
        function (result) {
            if (result === 0) {
                AToast.show("OK 버튼이 눌렸습니다.");
            }
        }
    );
}
```

* **OK\_CANCEL** 버튼의 Click 이벤트 함수를 아래와 같이 작성함.

```javascript
onOK_CANCELClick(comp, info, e) {
    let msgBox = new AMessageBox();
    msgBox.openBox(
        null,                         // 부모 컨테이너 (null: 최상위)
        "확인 취소",                  // 제목 (MessageBox의 타이틀)
        "이 작업을 진행하시겠습니까?",  // 내용 (표시될 메시지)
        AMessageBox.OK_CANCEL,        // 버튼 타입 (OK와 CANCEL 버튼 표시)
        function (result) {           // 콜백 함수 (버튼 클릭 시 실행)
            if (result === 0) {
                AToast.show("OK 버튼이 눌렸습니다.");
            } else if (result === 1) {
                AToast.show("CANCEL 버튼이 눌렸습니다.");
            }
        }
    );
}
```

***

### 4. 빌드 및 실행

* 프로젝트를 빌드 후 실행함.
* 각 버튼(OK, OK\_CANCEL)을 클릭하여 출력되는 메시지 박스와 알림창을 확인함.

![](https://wikidocs.net/images/page/275962/OKMessageBox02.png)

![](https://wikidocs.net/images/page/275962/OKMessageBox03.png)
