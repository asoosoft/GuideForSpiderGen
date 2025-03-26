# B. iOS 앱 구축하기(cordova)

## 1. iOS 사용 환경 설정

iOS 앱을 개발하기 위해서는 환경설정이 필요합니다. 아래의 환경 설정을 참고해서 진행 해주세요.

[환경설정 가이드](https://wikidocs.net/278960)

## 2. 스파이더젠에서 cordova 플러그인 사용법

**Cordova Plugin 설치**

cmd 창에서 프로젝트 경로에 진입 후 Plugin을 설치합니다

`cordova plugin add cordova-plugin-screen-orientation`

![](../../../.gitbook/assets/cordova.png)

> [cordova 공식 홈페이지](https://cordova.apache.org/plugins/)

## 3. 예제 코드 추가

**01. 이밴트 생성**

스파이더젠 프로젝트에서 버튼을 생성해서 클릭 이벤트함수에 아래와 같이 작성합니다.

🔽cordova.exec 함수가 cordova를 통해 모바일로 기능을 요청합니다.

```

    onButtonClick(comp, info, e)
    {

       if (!this.isClicked) {
            this.isClicked = false; // 초기값 설정
        }

        if (this.isClicked) {
            this.box.setText("다시 한번 버튼을 눌러보세요!");
        } else {
            this.box.setText("버튼이 정상 동작 합니다.");
        }

        this.isClicked = !this.isClicked;


    }
```

🔽 cordova.exec 의 각 파라미터 입니다.

```
cordova.exec(
        <성공 시 함수>, 
        <실패 시 함수>, 
        <플러그인 이름>, <행동 이름>, [<인수>]
    );
```

`MyApp\platforms`

위 경로에 있는 ios 폴더를 스파이더젠의 Assets 폴더에 export 합니다.

![](../../../.gitbook/assets/002.png)

**02. bin파일 생성**

F7을 눌러 빌드하고 bin파일을 생성합니다.

(open folder 기능을 이용해서 프로젝트 폴더로 쉽게 이동할 수 있습니다.)

![](<../../../.gitbook/assets/build (1).png>)

`MyApp\platforms\ios\app\src\main\assets\www`

위 경로에 있는 파일을 삭제 후 스파이더젠 프로젝트 bin 폴더안에 있는 파일을 export 합니다.

**03. Xcode 실행**

Menu에 진입 후 File -> Open 생성해두었던 `MyApp\platforms\ios` 를 선택하여 파일을 오픈합니다.

**04. Cordova 설정**

`내용 수정필요`

위 경로에 있는 index.html 파일에 아래 내용을 추가합니다.

`내용 수정필요`

**05. Xcode에서 프로젝트를 실행합니다.**

Staging 폴더의 www 경로에 있는 파일을 삭제 후 스파이더젠 프로젝트 bin 폴더안에 있는 파일을 export 합니다.

IOS는 파일프로토콜을 기본 지원하지 않으므로 localhost로 동작하도록 해야합니다. 그러므로 Staging/config.xml 파일에 아래 옵션을 추가해줘야 동작합니다.

```
<preference name="WKWebViewOnly" value="true" />
<preference name="scheme" value="app" />
<preference name="hostname" value="localhost" />
```

**06. 버튼을 눌러 정상 동작을 확인합니다.**
