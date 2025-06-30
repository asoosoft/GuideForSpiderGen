# ExBong

EXBong 컴포넌트는 봉 차트를 표현하는 컴포넌트

주로 금융 데이터에서 시가, 고가, 저가, 종가와 같은 정보를 시각적으로 표현하는 데 사용

### Appearance

공통 Appearance 는 [**6. Global Properties**](<../../Guide for SpiderGen/06  SpiderGen Editor/04  Properties Pane/02 Appearence.md>) 속성을 참고

### Attribute

EXBong 속성

<p align="center"><img src="../../.gitbook/assets/image (41).png" alt=""></p>

**Data**

ExBong 컴포넌트의 시각적 표현을 설정하는 속성

| **이름**       | **설명**                                           |
| ------------ | ------------------------------------------------ |
| `Up Color`   | 상승 시 봉의 색상을 설정하는 속성                              |
| `Down Color` | 하락 시 봉의 색상을 설정하는 속성                              |
| `Direction`  | <p>봉의 방향을 설정하는 속성<br>portrait: 세로 방향 (기본 설정)</p> |

### Example

**1. 프로젝트 생성**

* 프로젝트 트리뷰에서 Source > MainView.lay 파일을 클릭
* MainView의 레이아웃 파일이 오픈되면 컴포넌트 리스트에서 EXBong 컴포넌트를 선택하고 드래그하여 레이아웃에 배치
* Class 에서 ID를 bong1로 입력



**2. 데이터 설정**

* 먼저 MainView.js 파일을 오픈
* 상단의 파일탭에서 MainView.lay 탭을 더블 클릭하거나 우측의 프로젝트 트리에서 MainView.js 파일을 더블 클릭
* 모든 화면뷰는 onInitDone() 함수가 존재하며 이 함수는 화면이 생성될 때 딱 한번 실행
* onInitDone() 함수에서 레이블의 텍스트 내용을 아래와 같이 코드를 입력

```javascript
onInitDone()
{
	super.onInitDone()
	// valueArr = [시가, 고가, 저가, 종가]
	
	this.bong1.setData([10000, 20000, 9000, 9000]);
	// this.bong1.setData(valueArr);
}
```

**3. 프로젝트 실행**

* 설정한 데이터에 맞춰서 상승인지 하락인지에 따라 봉 생성

<div data-full-width="false"><figure><img src="../../.gitbook/assets/image (52).png" alt=""><figcaption><p>ex) [1000, 2000, 900, 1400]</p></figcaption></figure> <figure><img src="../../.gitbook/assets/image (55).png" alt=""><figcaption><p>ex) [1500, 2000, 700, 900]</p></figcaption></figure></div>

**5. 코드로 EXBong 생성**

* 먼저 MainView.js 파일을 오픈
* onInitDone() 함수에서 아래와 같이 코드를 입력

```javascript
onInitDone()
{
	super.onInitDone()
	
	// EXBong 인스턴스 생성
        const exBong = new EXBong();

        // 컴포넌트 초기화
        exBong.init();

        // 상승 색상 설정
        exBong.setUpColor("#ff0000"); // 예: 빨간색

        // 하락 색상 설정
        exBong.setDownColor("#0000ff"); // 예: 파란색

        // 방향 설정 (세로 방향)
        exBong.setDirection(true);

        // 시가, 고가, 저가, 종가 데이터 설정
        let valueArr = [55, 100, 0, 25];
        let prdyvrss = 5; // 전일대비 등락구분값 예시
        exBong.setData(valueArr, prdyvrss);

        // 생성된 EXBong 컴포넌트를 원하는 위치에 추가
        this.addComponent(exBong); // 레이아웃에 EXBong 추가
	exBong.setPos(100,100); // 원하는 위치에 배치
}
```

<div><figure><img src="../../.gitbook/assets/image (56).png" alt=""><figcaption><p>[55, 100, 0, 25]</p></figcaption></figure> <figure><img src="../../.gitbook/assets/image (57).png" alt=""><figcaption><p>[55, 100, 0, 75]</p></figcaption></figure></div>
