# B. iOS 앱 구축하기

## 1. 환경 설정

***

`환경 설정은 다음의 순서대로 진행해야 합니다.`

### 1. Xcode 설치

iOS 앱 개발을 위해 Xcode가 필요합니다. Xcode는 macOS에서만 사용할 수 있는 iOS 앱 개발을 위한 공식 IDE입니다.(iOS 앱을 테스트하거나 배포하려면 Apple Developer 계정이 필요합니다.)

> `Mac App Store를 열고 Xcode를 검색하여 설치합니다`.

### 2. Node js 설치

Node js 를 설치합니다.

> [node js 공식 홈페이지](https://nodejs.org/en/)

### 3. Cordova 설치

cmd 에서 아래의 단계를 순서대로 진행합니다.

> `npm i -g cordova`

(npm을 사용하여 Cordova를 전역 설치합니다.)

> `cordova -v`

(설치가 정상적으로 완료되면 Cordova의 버전이 출력됩니다.)

> `cordova create MyApp`

(MyApp이라는 새로운 Cordova 프로젝트 폴더를 생성합니다.)

> `cd MyApp`

(생성된 프로젝트 폴더인 MyApp/으로 이동합니다.)

> `cordova platform add ios`

(Cordova 프로젝트에 iOS 플랫폼을 추가합니다.)

### 4. SpiderGen cordova export

경로에 생성된 Android 폴더를 스파이더젠 프로젝트 Assets 폴더에 복사합니다.

![](../../.gitbook/assets/asset_settings.png)

## 2. SpiderGen 프로젝트 만들기

***

### 1. 예제 코드 추가

SpiderGen 프로젝트의 js파일에 예제 코드를 추가합니다. 예를 들어 Button 컴포넌트와 id가TextBox01인 TextBox 컴포넌트 추가 후 Button의 click Event 설정에 예제 코드를 추가합니다.

```

	onButtonClick(comp, info, e)
	{

       this.TextBox01.steText("기능이 동작합니다");

	}
```

그리고 F7을 눌러 빌드하고 bin파일을 생성합니다.

### 2. Cordova 앱 빌드 및 실행

iOS 앱을 빌드하고 실행합니다. 이 단계에서는 **Xcode가** 필요합니다.

![](../../.gitbook/assets/MyAppSettings.png)

Staging 폴더의 www 경로에 SpiderGen 프로젝트에서 만든 bin 폴더안에 있는 파일을 복사합니다. (기존www 경로의 index 파일은 삭제합니다)

IOS는 파일프로토콜을 기본 지원하지 않으므로 localhost로 동작하도록 해야합니다.\
그러므로 Staging/config.xml 파일에 아래 옵션을 추가해줘야 동작합니다.

```
<preference name="WKWebViewOnly" value="true" />
<preference name="scheme" value="app" />
<preference name="hostname" value="localhost" />
```

### 3. Xcode에서 프로젝트를 실행합니다.

Menu에 진입 후 File -> Open 생성해두었던`MyApp/platforms/ios` 경로를 를 선택하여 파일을 오픈합니다.

![](../../.gitbook/assets/androidwhite1.png)

### 4. 버튼을 눌러 정상 동작을 확인합니다.

![](../../.gitbook/assets/androidwhite2.png)

### 5. app 파일 생성

프로젝트를 run 했다면 app 파일이 생성됩니다.\
(프로젝트 이름이 MyApp 라면 아래의 경로에 생성)\
MyApp/platforms/ios/build/emulator/MyApp.app

이 경로에 .app 파일이 생성되며, 이를 Xcode를 통해 .ipa 파일로 변환할 수 있습니다.

### 6. Plugin

프로젝트를 진행하다보면 HTML만으론 불가능한 네이티브 기능이 필요합니다.

기기의 진동, 벨소리, 앱 이름, 버전 등은 네이티브에서만 실행 가능합니다.

> 스파이더젠과 네이티브를 이어주는 브릿지 역할 ➡️ cordova

> 스파이더젠에서 cordova 함수를 통해 네이티브로 요청 ➡️

> 네이티브에서 받은 요청에 따라 수행 후 다시 웹브라우저로 값 리턴

필요한 플러그인이 있다면 [cordova 공식 페이지](https://cordova.apache.org/)에서 찾아볼 수 있습니다.

[스파이더젠 프로젝트 iOS 코르도바 플러그인 사용방법](../../08.-mobile-app/09-cordova-hybrid/b-ios-cordova.md)
