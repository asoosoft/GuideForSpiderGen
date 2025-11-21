# Spacer

![](../../.gitbook/assets/spacer.png)

주로 레이아웃에서 공간을 확보하거나 다른 컴포넌트 간의 간격을 조정하는 데 사용.<br>

Spacer 컴포넌트는 자체적으로는 기능을 수행하지 않음.

### Example

* &#x20;**레이아웃에서 생성**

① Spacer 컴포넌트를 클릭한 후 Placement Pane > Size에서 설정

② Spacer 컴포넌트에 ID를 부여한 후 js에서 밑 코드 작성

```javascript
// 2. js에서 Spacer 설정하기
// 너비 100%, 높이 50px로 설정
this.spacer.setSize('50px', '50px');
// 위치 설정
this.spacer.setPosition('left: 0px, top: 0px');
```

\
<br>

* **코드에서 생성**

```javascript

onInitDone()
{
	// 스페이서 생성
	const spacer = new ASpacer();
	
	// 스페이서 속성 설정
	spacer.setSize('100%', '50px');
	spacer.setPosition('left: 0px, top: 0px');

	// 레이아웃에 스페이서 넣기
	// 스파이더젠에서는 컴포넌트의 jQuery 객체를 사용하여 
	// DOM 조작을 수행합니다.
	this.view.$ele.append(spacer.$ele);
	
}

```

![](../../.gitbook/assets/spacer2.png)
