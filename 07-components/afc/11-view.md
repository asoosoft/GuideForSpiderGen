# View

![](../../.gitbook/assets/스크린샷_2025-01-23_111628.png)

화면 구성을 위한 기본 단위로, 다른 컴포넌트를 자식으로 포함할 수 있는 컴포넌트.

AView는 자식 컴포넌트(버튼, 라벨 등)를 포함하고, 이들의 배치와 스타일을 조정.

AView의 크기나 위치 변경 시, 자식 컴포넌트의 위치와 크기를 자동으로 조정.

자식 컴포넌트에서 발생한 이벤트를 감지하고 적절히 처리.

AView는 자식 컴포넌트에 공통 속성과 스타일을 손쉽게 전달.

### Attribute

* Load Url![](../../.gitbook/assets/스크린샷_2025-01-23_135819.png)

뷰 컴포넌트에 로드할 레이아웃 파일(.lay)의 경로를 설정하는 속성.

이 속성을 통해 특정 레이아웃 파일을 뷰에 로드하여 화면에 표시.

### Example

#### 1. 화면에 컴포넌트 및 이벤트 생성

* 컴포넌트에서 View 생성.

![](../../.gitbook/assets/create_view.png)

* Event에서 Click 선택 후 확인

![](../../.gitbook/assets/view_event.png)

*   이벤트 함수 생성

    ```
    onAViewClick(comp, info, e){
      alert("hello world");
    }
    ```
* Run Project 실행 후 View 클릭![](../../.gitbook/assets/run_prj.png)

***

#### 2. 코드로 컴포넌트 및 이벤트 생성

* 컴포넌트 생성 코드

***

```
onInitDone() {

	super.onInitDone()

	// AView 인스턴스 생성
	const myView = new  AView();
	myView.init(); // 초기화

	// 컴포넌트 속성 설정
	myView.setWidth(400);
	myView.setHeight(200);

	// 부모 컴포넌트에 추가
	this.addComponent(myView);

}
```

* 이벤트 생성 코드

***

```
onInitDone() {
	super.onInitDone();

	// AView 인스턴스 생성
	const myView = new  AView();
	myView.init(); // 초기화

	// 컴포넌트 속성 설정
	myView.setWidth(400);
	myView.setHeight(200);

	// 부모 컴포넌트에 추가
	this.addComponent(myView);
	// 이벤트 리스너 추가
	myView.addEventListener('click', this, 'onMyViewClick');
}

// 클릭 이벤트 핸들러
onMyViewClick(comp, info, e) {
	alert('View가 클릭되었습니다.');
	// 클릭 시 실행할 작업
}
```

* 실행 결과

![](../../.gitbook/assets/스크린샷_2025-02-18_131044.png)

***

#### 3. 클릭 이벤트.

*   mainView.lay에 AButton 및 ALabel 추가

    ***

| component | ID        | Text         |
| --------- | --------- | ------------ |
| AView     | mainView  |              |
| AButton   | btnChange | Change Text  |
| ALabel    | lblText   | Initial Text |

![](../../.gitbook/assets/스크린샷_2025-01-23_170927.png)

* MainView.js에 코드 생성

***

```
class  MainView  extends  AView
{
	constructor()
	{
		super();
	}  

	init(context, evtListener)
	{
		super.init(context, evtListener);
	}

	onInitDone()
	{
		super.onInitDone();

	// 버튼에 클릭 이벤트 리스너 추가
		this.btnChange.addEventListener('click', this, 			'onBtnChangeClick');
	}

	// 버튼 클릭 이벤트 핸들러
		onBtnChangeClick(comp, info, e)
	{
	// 레이블의 텍스트를 변경
		this.lblText.setText('Text Changed!');
	}
}
```

* 실행 결과

![](../../.gitbook/assets/스크린샷_2025-01-23_164941.png) ![](../../.gitbook/assets/스크린샷_2025-01-23_164926.png)

#### 4. 코드로 컴포넌트 추가

* Project > Framework > afc 마우스 우클릭 > Default Load Settings![](../../.gitbook/assets/스크린샷_2025-02-18_132513.png)



* AButton.js, ALabel.js 선택

![](../../.gitbook/assets/스크린샷_2025-02-18_132854.png)![](../../.gitbook/assets/스크린샷_2025-02-18_132907.png)



* 창닫기 > 변경사항 적용 Yes

![](../../.gitbook/assets/스크린샷_2025-02-18_132942.png)



* MainView.js에 코드 생성

```
    onInitDone() {
	    super.onInitDone();
	    
	    // AView 인스턴스 생성
	    var dynamicView = new  AView();
	    dynamicView.init(); // 뷰 초기화
	    dynamicView.setSize(400, 300); // 뷰의 크기 설정
	    dynamicView.setPos(50, 50); // 뷰의 위치 설정
	    // 뷰의 배경색을 파란색으로 설정
	    dynamicView.setStyle('background-color', 'blue');
	    
	    // AButton 인스턴스 생성
	    const button = new  AButton();
	    button.init(); // 버튼 초기화
	    button.setText('Hello World'); // 버튼의 텍스트 설정
	    button.setSize(100, 40); // 버튼의 크기 설정
	    button.setPos(150, 130); // 버튼의 위치 설정
	    
	    // AView에 버튼 추가
	    dynamicView.addComponent(button, false, null);
	    
	    // MainView에 동적으로 생성한 AView 추가
	    this.addComponent(dynamicView, false, null);
    } 
```

* Build 및 실행

![](../../.gitbook/assets/스크린샷_2025-01-23_174659.png)
