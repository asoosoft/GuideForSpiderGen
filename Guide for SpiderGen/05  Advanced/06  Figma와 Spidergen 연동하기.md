# 06  Figma와 Spidergen 연동하기

### 1. 개발 목적

**<기존 개발 Process>**

![](https://wikidocs.net/images/page/276478/1.png)

**<개선된 Process>**

![](https://wikidocs.net/images/page/276478/2.png)

* 디자이너 측에서 작업한 결과물을 중간에 개발자가 수동으로 진행한 화면 작업에서 변환기를 통한 화면 작업으로 Process 를 개선하기 위함.

### 2. 화면 종류

**개발을 위한 Figma 화면은 Template, Component, Scene 세 종류로 구성됩니다.**

**1. Template**

![](https://wikidocs.net/images/page/276478/3.png)

* Asoo Soft 측에서 제공하는 Component 들의 기본 디자인 Set.
* SpiderGen 에서 Component로 인식할수 있는 구성된 화면. 타입별로 1개씩 존재.
* 각 컴포넌트의 상태별 디자인을 할수 있게 제공되어 있슴.(버튼 : Normal, Over, Down, Disable)

**2. Component**

![](https://wikidocs.net/images/page/276478/4.png)

* 컴포넌트 생성화면.
* Template 으로부터 컴포넌트들을 가져와서 화면구성에 필요한 모든 컴포넌트들을 생성하는 단계.

**3. Scene**

![](https://wikidocs.net/images/page/276478/5.png)

* 각 장면 생성 화면.
* Component 를 조합하여 각 장면을 완성하는 단계.

### 3. 작업 순서

위의 3단계를 포함한, 전체 단계는 총 6단계로 구성됩니다.

![](https://wikidocs.net/images/page/276478/6.png)

**1. Component 생성**

![](https://wikidocs.net/images/page/276478/7.png)

* Template 으로부터 필요한 Component 를 Copy\&Paste 한다음, 디자인 완성.(alt -drag 와 같은기능)
* 최상단의 이름은 Components 로 지정해야 함(하단 MetaMaker 와 연관)

**2. MetaMaker**

* Components 내의 이름이 중복되는경우, Lay 로 변환시 이름이 같은 다른 컴포넌트의 스타일이 적용되게 됨.
* MetaMaker 로 모든 컴포넌트의 이름을 Unique 하게 변경.
* Plugin - MetaMaker 실행후 Check 클릭
* 컴포넌트를 추가한 경우 무조건 실행하는것을 추천.
* 설치법
  * 하단 \<MetaMaker 설치법> 참조. 차후 Figma 플러그인으로 배포시 필요없는 과정.
* 사용법
  * Plugin-Development-MetaMaker 선택
  * Check 실행
  * 적용후 상태![](https://wikidocs.net/images/page/276478/8.png)

![](https://wikidocs.net/images/page/276478/9.png)

![](https://wikidocs.net/images/page/276478/91.png)

**3. Scene 생성**

생성한 Component 들을 Asset 메뉴에서 확인

![](https://wikidocs.net/images/page/276478/92.png)

* Asset 화면으로부터 사용할 컴포넌트들을 화면에 배치.
* Figma 의 Frame 은 SpiderGen 상에서 View 로 변환.
* Frame 내에 Auto Layout 이 켜지면 FlexLayout 으로 변환.
* \*\*\*\* 배치된 컴포넌트의 이름변경 불가(Component 에서 매칭되는 이름의 원본을 찾지 못해 에러가 발생) \*\*\*\*
* \*\*\* Scene 에서는 이미지 교체 불가능(Component 에있는 이미지만 export 되는 구조) \*\*\*
*

![](https://wikidocs.net/images/page/276478/93.png)

**4. Html 추출**

* html 추출은 Figma Plugin 중 Anima 를 사용하여 진행.

![](https://wikidocs.net/images/page/276478/94.png)

* Dev mode 활성화
* Component 혹은 Scene 선택
* Plugin 탭에서 Anima 선택
* Download 진행
* 다운로드된 파일은 각각 가독성있는 이름으로 변경.

**5. Lay 변환**

SpderGen 의 FigmaToLay 메뉴를 통해 추출된 Html 을 Lay 로 변환진행을 합니다.

1️⃣ 프로젝트 생성 or 열기

2️⃣ View - FigmaToLay 선택

3️⃣ ![](https://wikidocs.net/images/page/276478/95.png)

4️⃣ Load FigmaProject 클릭후 압축푼 폴더의 최상위 폴더 선택![](https://wikidocs.net/images/page/276478/96.png)

```
①	다운로드 받은 파일들을 선택해서 FigmaToLay 창에 드래그
②	리스트에서 Component 화면에 해당하는 파일 체크
③	Convert 클릭하여 변환 진행.
```

**5. Convert된 Lay 확인**

![](https://wikidocs.net/images/page/276478/97.png)

**6. PS. 한번 Convert 가 진행되면 다음번에도 Component 를 다시 드래그 해서 추가해야 하는가?**

1️⃣ 아니오.

* Convert 가 진행되면 Component 는 프로젝트 내로 복사되어 다음번 Convert 시 기본으로 참조되어, Scene 들만 추가하면 됨.
*

    ![](https://wikidocs.net/images/page/276478/98.png)

2️⃣ 그렇다면 Component 가 업데이트 된경우 어떻게 진행해야 하는가?

* 새로운 Component 를 추가후, 이를 Check 하고 진행하면 이후 Component 로 교체되어 적용됨.
* ![](https://wikidocs.net/images/page/276478/99.png)

### 4. MetaMaker 설치법

* PlugIn-Development-Import-Import Plugin from menifest 선택
* ![](https://wikidocs.net/images/page/276478/9a.png)
* 이후 파일 선택창에서 전달한 첨부 파일중에 MetaMaker 폴더의 Menifest.json 선택
* ![](https://wikidocs.net/images/page/276478/9a1.png)
* 이후 Plugin-Developmemt 에 MetaMaker 플러그인이 추가되어 사용가능합니다.
* ![](https://wikidocs.net/images/page/276478/9a2.png)

### 5 . 컴포넌트 리스트

**1. Button**

1️⃣Text Button

* ![](https://wikidocs.net/images/page/276478/9a3.png)
* 일반적인 텍스트로만 구성된 버튼.
* 텍스트는 Scene 에서 수정 가능.
* Normal, Over, Down, Diable 순 디자인.

2️⃣ Image Button

* ![](https://wikidocs.net/images/page/276478/9999.png)
* 텍스트 없이 이미지만 사용하는 버튼 **(상태별 이미지 변경 가능)**
* 적용법
  * Template 에서 ImageButton 을 Component 로 복사
  * ![](https://wikidocs.net/images/page/276478/9a4.png)
  * 이미지 Node 선택
  * ![](https://wikidocs.net/images/page/276478/9a5.png)
  * Fill 선택
  * image 선택
  * 파일 선택 하여 이미지 지정.

3️⃣ 복합 Button

* 텍스트와 이미지의 동시사용을 위해 디자인된 버튼.(상태별 이미지 변경 불가)
*

    ![](https://wikidocs.net/images/page/276478/9a6.png)
* 이미지가 좌측에 배치된 버튼
*

    ![](https://wikidocs.net/images/page/276478/9a7.png)
* 이미지가 상단에 배치된 버튼

**2. Label**

1️⃣ ![](https://wikidocs.net/images/page/276478/9a8.png)

2️⃣ 간단한 텍스트를 표시할때 사용되는 컴포넌트.

3️⃣Scene 에서 텍스트 수정이 가능.

* 아이콘 추가시 사용되는 Template

**3. TextField**

1️⃣ ![](https://wikidocs.net/images/page/276478/9a9.png)

2️⃣ 텍스트 입력에 사용되는 컴포넌트

3️⃣아이콘 표현이 필요한경우 아래의 컴포넌트 디자인 사용

**4. TextArea**

1️⃣ ![](https://wikidocs.net/images/page/276478/9b1.png)

2️⃣ 긴 분량의 텍스트 입력에 사용되는 컴포넌트

**5. TextBox**

1️⃣ ![](https://wikidocs.net/images/page/276478/9b2.png)

2️⃣ 긴분량의 텍스트 출력에 사용되는 컴포넌트.

**6. Image**

1️⃣ ![](https://wikidocs.net/images/page/276478/9b3.png)

2️⃣이미지 출력에 사용되는 컴포넌트.

**7. CheckBox**

1️⃣![](https://wikidocs.net/images/page/276478/9b4.png)

2️⃣ 체크 상태 표시에 사용되는 컴포넌트.

3️⃣ UnCheck - Check 상태 순으로 디자인.

**8. RadioButton**

1️⃣![](https://wikidocs.net/images/page/276478/9b5.png)

2️⃣ 여러 항목중 1개만 선택되어야 할때 사용되는 컴포넌트.

3️⃣ UnCheck - Check 상태순으로 디자인.

**9. SwitchButton**

1️⃣![](https://wikidocs.net/images/page/276478/9b6.png)

2️⃣ on/off 상태를 표현할때 사용되는 컴포넌트.

3️⃣ On-Off 순으로 디자인.

**10. DropBox**

1️⃣![](https://wikidocs.net/images/page/276478/9b7.png)

2️⃣ 여러항목 리스트중에서 하나를 선택할때 사용되는 컴포넌트.

3️⃣ 항목 리스트 UI 는 자체로 만든 UI 가 사용되어 적용됨.

**11. SelectBox**

1️⃣![](https://wikidocs.net/images/page/276478/9b8.png)

2️⃣ 기능은 DorpBox 와 동일.

3️⃣ 항목 리스트 UI 는 OS 에서 제공되는 UI 가 사용되어 적용됨.

**12. FileUploader**

1️⃣ ![](https://wikidocs.net/images/page/276478/9b9.png)

2️⃣ 파일 업로드시 파일을 선택하기 위한 컴포넌트.

**13. CalendarPicker**

1️⃣ ![](https://wikidocs.net/images/page/276478/9c1.png)

2️⃣ 날짜를 선택할때 사용되는 컴포넌트

3️⃣ Over - Down - Disable 순으로 디자인.

**14. Progress**

1️⃣![](https://wikidocs.net/images/page/276478/9c2.png)

2️⃣ 어떤 작업의 진행상태를 표시할때 사용되는 컴포넌트

**15. TabView**

1️⃣ Tab별로 화면을 분할할때 사용되는 컴포넌트

2️⃣ 탭이 선택되었을때의 디자인은 우측의 TabSelect 을통해서 진행.

**16. Grid**

![](https://wikidocs.net/images/page/276478/9c3.png)

1️⃣ ![](https://wikidocs.net/images/page/276478/9c4.png)

2️⃣ Table 을 표현할때 사용되는 컴포넌트.

3️⃣ 각 Row 및 각각 Cell 의 색상 설정 가능.

4️⃣ Cell 이 선택되었을때 디자인은 하단의 Selected 를 통해서 진행

**17. WebView**

1️⃣ ![](https://wikidocs.net/images/page/276478/9c5.png)

2️⃣ 화면내에서 web 화면을 표현할떄 사용되는 컴포넌트

3️⃣ 실행시 웹을 띄우기 위한 빈 공간으로 표현됨.

**18. ListView**

1️⃣ ![](https://wikidocs.net/images/page/276478/9c6.png)

2️⃣ 리스트 항목을 위해 사용되는 컴포넌트.

3️⃣ 실행시 리스트를 띄우기 위한 빈 공간으로 표현됨.

**19. SlideView**

1️⃣![](https://wikidocs.net/images/page/276478/9c7.png)

2️⃣ lay 로 구성된 하면들을 Swipe 를 통해 슬라이드 처럼 보기 위한 컴포넌트.

3️⃣ 실행시 슬라이드를 띄우기 위한 빈 공간으로 표현됨.

// todo\
상태유무에 따른 컴포넌트 수정 범위
