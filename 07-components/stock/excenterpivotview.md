# ExCenterPivotView

<figure><img src="../../.gitbook/assets/스크린샷 2025-06-27 164426.png" alt=""><figcaption></figcaption></figure>



트레이딩 화면의 중심에 위치하는 주요 UI 컴포넌트.&#x20;



현재 선택된 종목의 핵심 정보(현재가, 변동률, 거래량 등)를 표시하며, 타 위젯들과 상태를 연동하여 트레이딩 화면의 중심 역할.

***

### Appearance

공통 Appearance 는 [**6. Global Properties**](<../../Guide for SpiderGen/06  SpiderGen Editor/04  Properties Pane/02 Appearence.md>) 속성을 참고



Example

**1. 프로젝트 생성**

* 프로젝트 트리뷰에서 Source > MainView.lay 파일을 클릭
* MainView의 레이아웃 파일이 오픈되면 컴포넌트 리스트에서 EXCenterPivotView 컴포넌트를 선택하고 드래그하여 레이아웃에 배치
* Class 에서 ID를centerpivotview로 입력



**2. 데이터 설정**

* 먼저 MainView.js 파일을 오픈
* 상단의 파일탭에서 MainView.lay 탭을 더블 클릭하거나 우측의 프로젝트 트리에서 MainView.js 파일을 더블 클릭
* 모든 화면뷰는 onInitDone() 함수가 존재하며 이 함수는 화면이 생성될 때 딱 한번 실행
* onInitDone() 함수에서 레이블의 텍스트 내용을 아래와 같이 코드를 입력

```javascript
onInitDone()
{

}
```

**3. 프로젝트 실행**

* 설정한 데이터에 맞춰서 각 가격과 거래량, 평균가, 현재가가 표시

**4. 코드로** EXCenterPivotView **생성**

* 먼저 MainView.js 파일을 오픈
* onInitDone() 함수에서 아래와 같이 코드를 입력

```javascript
onInitDone() {
    super.onInitDone();

    const pivotView = new EXCenterPivotView();

    // ✅ DOM 생성
    pivotView.createElement();

    // ✅ 화면에 추가 (이게 있어야 내부 스크롤 영역도 생성됨)
    this.addComponent(pivotView);

    // ✅ 초기화
    pivotView.init();

    // ✅ 그리드 헤더 설정
    pivotView.leftGrid.setHeader(['Left1', 'Left2', 'Left3']);
    pivotView.pivotGrid.setHeader(['Pivot']);
    pivotView.rightGrid.setHeader(['Right1', 'Right2', 'Right3']);

    // ✅ 데이터 추가
    pivotView.addRow(
        ['100', '200', '300'],
        ['Center'],
        ['400', '500', '600']
    );

    // ✅ 스크롤 동기화
    pivotView.scrollViewLeft();
}

```

<figure><img src="../../.gitbook/assets/스크린샷 2025-06-30 110253.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
<mark style="color:red;">**Build 에러 발생 시**</mark>

_**프로젝트 트리뷰에서 Framework > stock 우클릭 > Default Load Settings.. > Component > ExCenterPivotView.js 체크**_

<img src="../../.gitbook/assets/스크린샷 2025-06-30 092905.png" alt="" data-size="original">
{% endhint %}
