# FlowOneLine

![](../../.gitbook/assets/스크린샷_2025-01-24_132216.png)

직선을 그리는 컴포넌트.

다양한 속성과 메서드를 통해 직선의 스타일과 방향을 설정.

기본적으로 직선을 그리며, 컴포넌트의 사이즈 정보가 변경될 때 자동으로 직선을 다시 그림.

직선의 양 끝에 화살표를 추가할 수 있으며, 화살표의 위치를 시작점, 끝점, 또는 양쪽 모두로 설정.

직선의 방향을 가로(수평) 또는 세로(수직)로 지정.

직선의 색상과 두께를 설정할 수 있어, 다양한 스타일의 직선을 표현.

### Attribute

#### Type

| Direction | 설명             |
| --------- | -------------- |
| horizon   | 직선을 수평 방향으로 설정 |
| vertical  | 직선을 수직 방향으로 설정 |

![](../../.gitbook/assets/스크린샷_2025-01-24_133326.png)

![](../../.gitbook/assets/스크린샷_2025-01-24_133407.png)

#### Arrow

| Arrow | 설명                               |
| ----- | -------------------------------- |
| Use   | 직선의 양 끝에 화살표를 추가하여 방향성을 나타내는 기능. |
| start | 직선의 시작 부분에 화살표를 추가하는 기능.         |
| end   | 직선의 끝 부분에 화살표를 추가하는 기능.          |
| both  | 직선의 양 끝에 화살표를 추가하는 기능.           |

![](../../.gitbook/assets/스크린샷_2025-01-24_134046.png) ![](../../.gitbook/assets/스크린샷_2025-01-24_134055.png) ![](../../.gitbook/assets/스크린샷_2025-01-24_134105.png)

#### Stroke Width

| 기능           | 설명                   |
| ------------ | -------------------- |
| Stroke Width | 직선의 두께를 설정하는 기능을 제공. |
| Line Color   | 직선의 색상을 설정.          |

![](../../.gitbook/assets/스크린샷_2025-01-24_134635.png) ![](../../.gitbook/assets/스크린샷_2025-01-24_134719.png)

### Example

#### 1. 화면에 컴포넌트 생성

![](../../.gitbook/assets/스크린샷_2025-01-24_164833.png)

#### 코드로 컴포넌트 및 이벤트 생성

* Practice > Framework > afc > Default Load Settings

![](../../.gitbook/assets/스크린샷_2025-02-18_150347.png)

* AFlowOneLine.js + AFlowOneLineEvent.js + compEx.css 선택

![](../../.gitbook/assets/스크린샷_2025-02-18_150424.png)

* 창닫기 > 변경된 정보를 저장하시겠습니까? Yes

![](../../.gitbook/assets/스크린샷_2025-02-18_150533.png)

* js에 코드 생성

```
    
onInitDone() {

	super.onInitDone();

	// AFlowOneLine 인스턴스 생성
	const flowLine = new  AFlowOneLine();
	flowLine.init(); // 초기화

	// AFlowOneLine 설정
	flowLine.setLineColor('green'); // 직선 색상 설정
	flowLine.setStrokeWidth(5); // 직선 두께 설정
	flowLine.setDirect('vertical'); // 직선 방향 설정 (세로)
	flowLine.setArrow(true); // 화살표 사용 여부 설정

	// 스타일을 통해 중앙에 배치
	const flowLineElement = flowLine.getElement();
	flowLineElement.style.position = 'absolute';
	flowLineElement.style.top = '50%';
	flowLineElement.style.left = '50%';
	flowLineElement.style.transform = 'translate(-50%, -50%)';

	// 클릭 이벤트 리스너 추가
	flowLine.addEventListener('click', this, 'onFlowLineClick');

	// AFlowOneLine을 부모 레이아웃에 추가
	this.getContainer().addComponent(flowLine);
	}

	// 클릭 이벤트 핸들러
	onFlowLineClick(comp, info, e) {
		alert('Flow line clicked!');
	}

```

* 실행 결과

![](../../.gitbook/assets/스크린샷_2025-02-18_150247.png)
