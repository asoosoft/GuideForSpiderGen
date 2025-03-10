# 1. 코르도바 세팅(안드로이드 스튜디오 필요)


-----

아래 설정들을 진행시켜줍니다.

**1. node js 설치**

[](https://nodejs.org/en)

**2.  cordova 설치**

cmd창에서 진행

> `npm install -g cordova`

**3. cordova 프로젝트 생성**

원하는 경로로 이동 후 cmd창에서 해당 명령어 실행

> `cordova create myapp`

기본적으로 웹 플랫폼만 추가됨

**4. cordova 플랫폼 추가(안드로이드 생성)**

cmd창에서 해당위치로 이동: cd 사용자가 설정한 경로\myapp
안드로이드 플랫폼 추가 : cordova platform add android

**5. JAVA JDK(1.8) 설치**

다운로드 : [](https://www.oracle.com/java/technologies/javase-downloads.html)
jdk-8u251-windows-x64.exe 다운로드 및 설치

**6. JAVA_HOME 환경변수 등록**

* 환경변수 설정: "고급 시스템 설정" 실행 -> 고급탭(환경 변수)
* 시스템변수 새로만들기: JAVA_HOME / 설치한 JDK 경로 추가
* 시스템변수 Path: "%JAVA_HOME%\bin" 추가
 
![](https://wikidocs.net/images/page/277125/%EC%BA%A1%EC%B2%98.PNG)

![](https://wikidocs.net/images/page/277125/%EC%BA%A1%EC%B2%982.PNG)
 
 
**7. Gradle설치, 환경변수 등록**

* 환경변수 설정: "고급 시스템 설정" 실행 -> 고급탭(환경 변수)
* 다운로드 : [](gradle.org/releases/)
* 특정 폴더에 넣고 그 폴더경로를 환경변수에 등록
* 커맨드창 껏다 켜야 적용됨

![](https://wikidocs.net/images/page/277125/%EC%BA%A1%EC%B2%98_kj05zSj.PNG)

![](https://wikidocs.net/images/page/277125/%EC%BA%A1%EC%B2%981.PNG)

**8. JS 통신을 위한 코르도바 플러그인 설치하기**

하이브리드앱을 구축하기 위해 아래 명령어를 입력해줍니다.

> `cordova platform add android`

# 2. 스파이더젠 설정


-----

File - Properties - Build 에서 아래와 같이 설정합니다.

![](https://wikidocs.net/images/page/277125/%EC%8A%A4%ED%8C%8C%EC%9D%B4%EB%8D%94%EC%A0%A0%EC%84%A4%EC%A0%95.PNG)

프로젝트 트리에서 Bridge 폴더가 추가된것을 확인 할 수 있습니다.

![](https://wikidocs.net/images/page/277125/%EC%8A%A4%ED%8C%8C%EC%9D%B4%EB%8D%94%EC%A0%A0%EC%84%A4%EC%A0%952.PNG)

마지막으로 Android환경으로 테스트 하기 위해 Bridge/ios 폴더안의 파일을 지우고 사용자의 프로젝트 경로\myapp\platforms\android\platform_www에 있는 plugins폴더,cordova.js, cordova_plugins.js 세개를 Bridge/android 경로에 export 해줍니다.
# 3. 코르도바 웹뷰


-----

**코르도바 웹뷰로 스파이더젠 lay파일을 띄워보고 js와 통신하는법을 알아보고자 합니다.**

먼저 스파이더젠에서 아래와 같이 세팅해줍니다.
MainView.lay에 button과 textbox 컴포넌트를 만들어주고 각각의 컴포넌트 아이디를 deviceBtn, textbox로 만들어줍니다. 그리고 버튼에는 click 이벤트로 onDeviceBtnClick를 등록해줍니다.(위치는 편하신대로 설정하셔도 됩니다.)

![](https://wikidocs.net/images/page/277125/%EB%A0%88%EC%9D%B4.PNG)

lay의 구성이 끝났다면 MainView.js의 onDeviceBtnClick 함수에 아래와 같이 코드를 입력해줍니다.

```
cordova.exec((result)=>{
    this.textbox.setText(JSON.stringify(result));
},null,"Device","getDeviceInfo",[])
```

그리고 F7을 눌러 빌드하고 bin파일을 코르도바 웹뷰의 기본경로인 유저의 프로젝트 설정경로\myapp\platforms\android\app\src\main\assets\www 에 붙여넣기 합니다.

안드로이드 스튜디오를 실행해서 Run을 눌러줍니다.(사용자의 기기를 연결해서 진행해도 되지만 가상 기기를 만들어 진행할수 있음,아래 이미지는 가상기기)

![](https://wikidocs.net/images/page/277125/%EA%B0%80%EC%83%81%ED%8F%B0.PNG)

위 이미지와 같이 성공적으로 실행이 됐다면 버튼을 눌러 textbox가 바뀌는것을 확인합니다.

![](https://wikidocs.net/images/page/277125/%EC%BA%A1%EC%B2%98_9eFlZfD.PNG)

이상으로 기본적인 하이브리드앱 구축을 끝마칩니다.