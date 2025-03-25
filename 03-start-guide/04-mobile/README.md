# 04  빌드 및 실행(Mobile)

**SpiderGen 프로젝트는 하나의 소스로 안드로이드, iOS 모두에서 사용**

사용하기 위해서는 우선 Cordova를 설치하고 플랫폼을 추가

### 1. Android에서 실행

안드로이드 스튜디오에서 실행하기 위해서 먼저 설치 진행

> [안드로이드 스튜디오 설치](https://developer.android.com/studio?hl=ko)

설치 후 Android Studio 실행 후 \[File > Open] 선택 ➡️\
cordova 폴더의 안드로이드 프로젝트 오픈

### 2. iOS에서 실행

iOS에서 실행하기 위해선 macOS 환경과 XCode 설치 필요

> [XCode 설치](https://apps.apple.com/kr/app/xcode/id497799835)

설치 후 XCode 실행 후 \[File > Open]선택 ➡️\
cordova폴더의 prj파일 오픈

### cordova 플러그인

프로젝트를 진행하다보면 HTML만으론 불가능한 네이티브 기능이 필요

> 기기의 진동, 벨소리, 앱 이름, 버전 등은 네이티브에서만 실행 가능
>
> 스파이더젠과 네이티브를 이어주는 브릿지 역할 ➡️ cordova

스파이더젠에서 cordova 함수를 통해 네이티브로 요청 ➡️\
네이티브에서 받은 요청에 따라 수행 후 다시 웹브라우저로 값 리턴

> 모바일에서 어떤 작업을 수행할 것인지에 따라 직접 플러그인 생성

자세한 사용 예시는 [동영상 강좌](https://www.youtube.com/watch?v=Cu9fOuyX6RE\&ab_channel=%ED%99%A9%EC%95%84%EC%88%98)를 통해 확인

### 스파이더젠과 함께 cordova 사용법

#### 스파이더젠

스파이더젠 프로젝트에서 버튼 클릭 이벤트함수에 아래와 같이 작성

🔽cordova.exec 함수가 cordova를 통해 모바일로 기능을 요청하는 함수

```js

    constructor() {
        super()
         // 현재 상태를 저장할 변수
        this.isLandscape = false;
    }


   onButtonClick(comp, info, e) {

        // landscape ↔ portrait 토글
        let orientation = this.isLandscape ? "portrait" : "landscape";

        cordova.exec(
            function () {
                alert("화면 방향이 " + orientation + "로 변경되었습니다.");
            },
            function (error) {
                alert("오류 발생: " + error);
            },
            "CDVOrientation",
            "screenOrientation",
            ["set", orientation]
        );

        // 상태 변경
        this.isLandscape = !this.isLandscape;
    }

```

🔽 cordova.exec 의 각 파라미터

```js
cordova.exec(
		<성공 시 함수>, 
		<실패 시 함수>, 
		<플러그인 이름>, <행동 이름>, [<인수>]
	);
```

***

#### Android

Android Studio를 실행하여 cordova 폴더의 안드로이드 프로젝트 오픈

```java
@Override
    public boolean execute(String action, JSONArray args, CallbackContext callbackContext) throws JSONException {
        if (action.equals("screenOrientation")) {
            return routeScreenOrientation(args, callbackContext);
        }
        else if (action.equals("sampleMethod")) {
            String message = args.getString(0);
            this.sampleMethod(message, callbackContext);
            return true;
        }
        return false;
    }
```

* **screenOrientation**: 화면의 방향을 정하는 플러그인
* **sampleMethod**: 샘플 플러그인

스파이더젠에서 sampleMethod을 요청했으므로 action이 sampleMethod인 곳 내부가 실행

내부에선 **args**로 부터 **message**를 받아오고 **sampleMethod함수**를 실행

**args**에는 스파이더젠에서 **배열로 보냈던 인수가 차례대로 저장** ➡️\
**get() 함수를 사용하여 원하는 위치의 인수를 얻어옴**

\


🔽 sampleMethod 함수

콜백 함수를 실행해주는 내용 확인

```java
private void sampleMethod(String message, CallbackContext callbackContext) {
    if (message != null && message.length() > 0) {
	    // 성공 시
        callbackContext.success(message);
    } else {
	    // 실패 시
        callbackContext.error("Expected one non-empty string argument.");
    }
}
```

> 이 함수를 사용하여 받은 message를 다시 스파이더젠으로 리턴
>
> 스파이더젠 프로젝트에서 작성했던 콜백함수가 호출되어 alert으로 message가 뜸

\


**플러그인을 추가하기 원한다면?**\


1️⃣ sampleMethod 아래에 새로운 else if 문을 사용하여 원하는 이름을 만듬\
2️⃣ 스파이더젠에서 cordova.exec를 통해 새로 만든 이름으로 호출

***

#### iOS

XCode를 실행해여 cordova 폴더의 iOS 프로젝트를 오픈

```c
    - (void) sampleMethod:(CDVInvokedUrlCommand *)command
    {
         CDVPluginResult* pluginResult = nil;
        NSString* message = [command.arguments objectAtIndex:0];
        if (message != nil) {
		        // 성공 시
                pluginResult = [CDVPluginResult resultWithStatus:CDVCommandStatus_OK messageAsString:message];
            } else {
	            // 실패 시
                pluginResult = [CDVPluginResult resultWithStatus:CDVCommandStatus_ERROR messageAsString:@"Arg was null"];
            }
        [self.commandDelegate sendPluginResult:pluginResult callbackId:command.callbackId];
    }
```

* **screenOrientation**: 화면의 방향을 정하는 플러그인
* **sampleMethod**: 샘플 플러그인

스파이더젠에서 **sampleMethod** 요청 ➡️ **sampleMethod 함수** 실행

내부에서 **command.arguments**로 부터 **message**를 받아오고 **sampleMethod함수**를 실행

**command.arguments**에 스파이더젠에서 배열로 보냈던 인수가 차례대로 저장 ➡️ **objectAtIndex 함수**를 사용하여 원하는 위치의 인수를 얻음

> 이 함수를 사용하여 받은 message를 다시 스파이더젠으로 리턴
>
> 스파이더젠 프로젝트에서 작성했던 콜백함수가 호출되어 alert으로 message가 뜸

\


**플러그인을 추가하기 원한다면?**\


1️⃣ **sampleMethod** 아래에 새로운 함수를 추가하여 원하는 이름을 만듬\
2️⃣ 스파이더젠에서 cordova.exec를 통해 새로 만든 이름으로 호출
