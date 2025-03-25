# 34  Progress

![](https://wikidocs.net/images/page/24858/progress.png)

**프로그래스(AProgress)** 는 진행 상황을 시각적으로 표시하는 데 사용되는 컴포넌트입니다.\


프로그래스는 작업의 완료 비율을 나타내는 데 유용하며, 사용자에게 현재 진행 상태를 알려주는 역할을 합니다.

### Example

AProgress 컴포넌트는 파일 업로드, 다운로드 진행 상황, 작업 처리 상태 등을 사용자에게 시각적으로 알릴 때 유용하게 사용됩니다.\


프로그레스 바의 값을 동적으로 업데이트하여 사용자에게 실시간으로 진행 상황을 보여줄 수 있습니다.

**1️⃣ 레이아웃에서 생성**

![](https://wikidocs.net/images/page/24858/pg_res1.png)

```js
class  MainView  extends  AView
{
	constructor()
	{
		super()

		// 프로그래스 값 변수
		this.progressVal = 0;
	}

	init(context, evtListener)
	{
		super.init(context, evtListener)
		
		// 초기 프로그레스 값을 설정
		this.progressID.setValue(progressVal); 
	}

	// 버튼 클릭 이벤트 함수 추가
	// 버튼을 클릭할 때 마다 프로그레스 값을 증가시키는 로직
	onButtonClick(comp, info, e) {  
		if(progressVal < 100) { 
			this.progressVal += 10; // 10%씩 증가 
			// 프로그래스 바 업데이트
			this.progressID.setValue(progressVal);  
		} 
	}
}
```

***

**2️⃣ 코드에서 생성**

![](https://wikidocs.net/images/page/24858/pg_res2.png)

```javascript

onInitDone()
{
	super.onInitDone()

	// 사용자 함수 불러오기
	this.createProgress();
}

// 사용자 함수 생성
createProgress()
{
	// 프로그래스 생성
	const progress = new AProgress();

	// 체크박스 초기화
	progress.init();
	
	// 프로그래스 속성 설정
	
    // 프로그래스의 값 설정
	progress.setValue(50); 
	
	// 프로그래스를 특정 컨테이너에 추가
	// 스파이더젠에서는 컴포넌트의 jQuery 객체를 사용하여 
	// DOM 조작을 수행합니다.
	this.view.$ele.append(progress.$ele);
}

```
