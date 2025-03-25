

`AMessageBox.YES_NO`와 `AMessageBox.YES_NO_CANCEL`은 세 가지 버튼을 제공하는 메시지 박스 타입임.  
이 타입은 "YES", "NO", "CANCEL" 버튼을 제공하며, 사용자가 세 가지 선택지 중 하나를 선택해야 하는 상황에 유용함.  
예를 들어, 사용자가 작업을 저장할지, 저장하지 않고 진행할지, 아니면 작업을 취소할지를 묻는 경우에 사용할 수 있음.

---

## 1. Framework 추가

* 프로젝트를 시작하기 전에 필요한 기능들을 준비함.
  * MessageBox를 사용하기 위해 `afc` 폴더에 **AMessageBox.js** 파일을 추가함.
  * 메시지(알림창)를 간단히 띄우기 위해 `afc` 폴더에 **AToast.js** 파일을 추가함.
  * 이후 코드에서 `AToast.show("메시지")`처럼 바로 알림창을 표시할 수 있음.

![](https://wikidocs.net/images/page/275963/MessageBox.png)

---

## 2. 컴포넌트 배치

* View에 아래와 같이 컴포넌트들을 배치함.

| component | text          |
| --------- | ------------- |
| AButton   | YES_NO        |
| AButton   | YES_NO_CANCEL |

![](https://wikidocs.net/images/page/275963/YES_NO_CANCELMessageBox01.png)

---

## 3. 버튼 이벤트 연결 

* **YES_NO** 버튼의 Click 이벤트 함수를 아래와 같이 작성함.

```javascript
onYES_NOClick(comp, info, e) {
    let msgBox = new AMessageBox();
    msgBox.openBox(
        null,                          // 부모 컨테이너 (null: 최상위)
        "선택",                       // 제목 (MessageBox의 타이틀)
        "변경 사항을 저장하시겠습니까?", // 내용 (표시될 메시지)
        AMessageBox.YES_NO,            // 버튼 타입
        function (result) {            // 콜백 함수
            if (result === 0) {
                AToast.show("YES 버튼이 눌렸습니다.");
            } else if (result === 1) {
                AToast.show("NO 버튼이 눌렸습니다.");
            }
        }
    );
}
```

* **YES_NO_CANCEL** 버튼의 Click 이벤트 함수를 아래와 같이 작성함.

```javascript
onYES_NO_CANCELClick(comp, info, e) {
    const msgBox = new AMessageBox();
    msgBox.openBox(
        null,                        // 부모 컨테이너 (null: 최상위)
        "알림",                     // 제목 (MessageBox의 타이틀)
        "저장을 완료했습니다.",       // 내용 (표시될 메시지)
        AMessageBox.YES_NO_CANCEL,    // 버튼 타입 (YES, NO, CANCEL 버튼 표시)
        function (result) {           // 콜백 함수 (버튼 클릭 시 실행)
            if (result === 0) {
                AToast.show("YES 버튼이 눌렸습니다.");
            } else if (result === 1) {
                AToast.show("NO 버튼이 눌렸습니다.");
            } else if (result === 2) {
                AToast.show("CANCEL 버튼이 눌렸습니다.");
            }
        }
    );
}
```

---

## 4. 빌드 및 실행

* 프로젝트를 빌드 후 실행함.
* 각 버튼(YES_NO, YES_NO_CANCEL)을 클릭하여 출력되는 메시지 박스와 알림창을 확인함.

![](https://wikidocs.net/images/page/275963/YES_NO_CANCELMessageBox02.png)  
![](https://wikidocs.net/images/page/275963/YES_NO_CANCELMessageBox03.png)