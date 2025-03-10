![](https://wikidocs.net/images/page/24836/tabview-comp-00.png) 


**탭뷰(TabView)** 는 사용자가 여러 개의 탭을 통해 다양한 콘텐츠를 표시할 수 있는 UI 컴포넌트입니다.
>사용자는 탭을 클릭하여 서로 다른 콘텐츠를 쉽게 전환할 수 있습니다. TabView는 다음과 같은 속성과 메서드를 제공합니다

## Appearance

![](https://wikidocs.net/images/page/24836/tabview-comp-01.png)


**Tab**

* **Width** 탭의 가로 사이즈를 지정하는 속성입니다.
* **Height** 탭의 높이를 지정하는 속성입니다.
* **Hidden**  탭의 name UI를 숨기는 속성입니다.
* **Select History** 탭 전환 시 사용자의 탭 선택 기록을 저장하는 속성입니다.

**Items**

* **Selct** 탭뷰 중 기본적으로 선택될 탭아이디를 설정하는 속성입니다.
* **edit** 탭의 설정 내용을 수정하는 속성입니다.
* **del** 선택한 탭을 삭제합니다.
* **add** 탭뷰를 추가하는 속성입니다.

![](https://wikidocs.net/images/page/24836/tabview-ex-02.png)

   >* **ID** 탭을 구분하기 위한 ID 입니다.
   * **Name** 탭에 표시될 텍스트 입니다.
   * **URL** 탭과 매칭될 탭뷰의 URL 입니다.




## Example

#### 1. 컴포넌트를 추가 합니다.

| component	 | id |
| -------- | -------- |
| ATabView     | mainTabView     |

#### 2. 폴더를 생성합니다.

* 새로운 폴더를 생성해서 화면을 추가합니다
* Views 폴더에 tView1, tView2, tView3 이름으로 3개의 뷰를 추가합니다.

![](https://wikidocs.net/images/page/24836/tabview-comp-07.png)

#### 3. 배경색을 변경합니다.
* 추가한 화면의 색을 각각 다르게 설정합니다.
* MainView의 tabView 컴포넌트 Appearance > Items에 위에서 생성한 tView를 추가하고 Select에 tab1을 추가합니다.

* Url은 CopyUrl 을 사용해서 복사할 수 있습니다.

![](https://wikidocs.net/images/page/24836/d886c56b-0525-4ff6-8ee2-8830f8950b39.png)

| id  | name | url  |
| -------- | -------- | -------- |
| tab1     | TAB1     | Source/Views/tView1.lay     |
| tab2     | TAB2     | Source/Views/tView2.lay     |
| tab3     | TAB3     | Source/Views/tView3.lay     |



* JavaScript로 작성시 MainView.js 파일에 아래 코드를 참고해서 작성합니다.

```
	onInitDone()
	{
		super.onInitDone()

		    // 탭 추가
           this.tabView.addTab('Tab 1', 'Source/Views/tView1.lay', 'tab1');
           this.tabView.addTab('Tab 2', 'Source/Views/tView2.lay', 'tab2');
           this.tabView.addTab('Tab 3', 'Source/Views/tView3.lay', 'tab3');

           this.tabView.selectTabById('tab1')
        
    } 
```

![](https://wikidocs.net/images/page/24836/tabview-ex-03.png)

#### 4.빌드를 실행 합니다.

* 상단에 있는 TAB UI를 클릭해서 탭을 이동합니다.

![](https://wikidocs.net/images/page/24836/tabview-comp-04.png)
![](https://wikidocs.net/images/page/24836/tabview-comp-05.png)
![](https://wikidocs.net/images/page/24836/tabview-comp-06.png)

## 다음 예제는 JavaScript를 사용하여 탭뷰(TabView)를 만듭니다.

#### 1. Framework를 추가합니다.

* Framework의 afc에서 ATabView/ATabViewEent를 추가합니다.

>컴포넌트를 코드로 추가할 때는 컴포넌트(componet)와 이벤트(event)를 둘 다 추가해야 합니다.

![](https://wikidocs.net/images/page/24836/tabview-comp-08.png)

#### 2.  폴더를 생성합니다.


* 새로운 폴더를 생성해서 화면을 추가합니다
* Views 폴더에 tView1, tView2, tView3 이름으로 3개의 뷰를 추가합니다.

![](https://wikidocs.net/images/page/24836/tabview-comp-07.png)

#### 3. 배경색을 변경합니다.
* 추가한 화면의 색을 각각 다르게 설정합니다.

#### 4.코드를 추가합니다.
* 메인 화면에 아래의 코드를 추가합니다.

```
onInitDone() {
        super.onInitDone()
        // ATabView 객체 생성
        const tabView = new ATabView();
        tabView.init();// 탭 뷰 초기화
        tabView.setSize('100%', '100%');// 탭 뷰 크기 설정 (전체 화면 크기)
        tabView.setPos(0, 0);// 탭 뷰 위치 설정 (좌상단 위치로 설정)




        // 탭 추가: 탭 이름, 해당 탭에 로드될 레이아웃 파일 경로, 탭의 고유 ID
        tabView.addTab('Tab 1', 'Source/Views/tView1.lay', 'tab1');
        tabView.addTab('Tab 2', 'Source/Views/tView2.lay', 'tab2');
        tabView.addTab('Tab 3', 'Source/Views/tView3.lay', 'tab3');
        // 첫 번째 탭(tab1)을 선택하여 표시
        tabView.selectTabById('tab1')
        // 탭 뷰를 부모 컨테이너에 추가하여 화면에 표시
        this.getContainer().addComponent(tabView);

    }
```

#### 5.빌드를 실행 합니다.


![](https://wikidocs.net/images/page/24836/tabview-comp-04.png)
![](https://wikidocs.net/images/page/24836/tabview-comp-05.png)
![](https://wikidocs.net/images/page/24836/tabview-comp-06.png)