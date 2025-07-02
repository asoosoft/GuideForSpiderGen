# EXCenterPivotView



<figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 103513.png" alt=""><figcaption></figcaption></figure>

그리드의 특정 중앙 열을 기준으로 고정한 상태에서 좌우 영역은 각각 독립적으로 가로 스크롤되며, 세로 스크롤 시에는 중앙과 좌우 영역이 동시에 연동되는 중앙 열 고정형 그리드 뷰 컴포넌트

***

### Appearance

공통 Appearance 는 [**6. Global Properties**](<../../Guide for SpiderGen/06  SpiderGen Editor/04  Properties Pane/02 Appearence.md>) 속성을 참고



Example

**1. 프로젝트 생성**

* 프로젝트 트리뷰에서 Source > MainView.lay 파일을 클릭
* MainView의 레이아웃 파일이 오픈되면 컴포넌트 리스트에서 EXCenterPivotView 컴포넌트를 선택하고 드래그하여 레이아웃에 배치
* Class 에서 ID를 pivotView로 입력

**2. 데이터 설정**

* 먼저 MainView.js 파일을 오픈
* 상단의 파일탭에서 MainView.lay 탭을 더블 클릭하거나 우측의 프로젝트 트리에서 MainView.js 파일을 더블 클릭
* 모든 화면뷰는 onInitDone() 함수가 존재하며 이 함수는 화면이 생성될 때 딱 한번 실행
* onInitDone() 함수에서 레이블의 텍스트 내용을 아래와 같이 코드를 입력



* addRow 예제

```javascript
onInitDone() {
    super.onInitDone();

    this.pivotView.leftGrid.addRow(['왼쪽1', '왼쪽2', '왼쪽3']);
    this.pivotView.pivotGrid.addRow(['중심']);
    this.pivotView.rightGrid.addRow(['오른쪽1', '오른쪽2', '오른쪽3']);

    this.pivotView.addRow(['L100', 'L200', 'L300'], ['Center-1'], ['R100', 'R200', 'R300']);
    this.pivotView.addRow(['L101', 'L201', 'L301'], ['Center-2'], ['R101', 'R201', 'R301']);
    this.pivotView.addRow(['L102', 'L202', 'L302'], ['Center-3'], ['R102', 'R202', 'R302']);
    this.pivotView.addRow(['L103', 'L203', 'L303'], ['Center-4'], ['R103', 'R203', 'R303']);
    this.pivotView.addRow(['L104', 'L204', 'L304'], ['Center-5'], ['R104', 'R204', 'R304']);
    this.pivotView.addRow(['L105', 'L205', 'L305'], ['Center-6'], ['R105', 'R205', 'R305']);

    this.pivotView.scrollViewLeft();
}

```



* prependRow 예제

```javascript
onInitDone() {
super.onInitDone();
    
    this.pivotView.leftGrid.prependRow(['왼쪽1', '왼쪽2', '왼쪽3']);
    this.pivotView.pivotGrid.prependRow(['중심']);
    this.pivotView.rightGrid.prependRow(['오른쪽1', '오른쪽2', '오른쪽3']);
    
    this.pivotView.prependRow(['L105', 'L205', 'L305'], ['Center-6'], ['R105', 'R205', 'R305']);
    this.pivotView.prependRow(['L104', 'L204', 'L304'], ['Center-5'], ['R104', 'R204', 'R304']);
    this.pivotView.prependRow(['L103', 'L203', 'L303'], ['Center-4'], ['R103', 'R203', 'R303']);
    this.pivotView.prependRow(['L102', 'L202', 'L302'], ['Center-3'], ['R102', 'R202', 'R302']);
    this.pivotView.prependRow(['L101', 'L201', 'L301'], ['Center-2'], ['R101', 'R201', 'R301']);
    this.pivotView.prependRow(['L100', 'L200', 'L300'], ['Center-1'], ['R100', 'R200', 'R300']);
    
    this.pivotView.scrollViewLeft();

}
```



**3. 프로젝트 실행**

* 설정한 데이터에 맞춰서 각 가격과 거래량, 평균가, 현재가가 표시
* 왼쪽부터 addRow, prependRow 사용예제

<div><figure><img src="../../.gitbook/assets/화면 녹화 중 2025-07-02 104331.gif" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/화면 녹화 중 2025-07-02 105402.gif" alt=""><figcaption></figcaption></figure></div>

**4. 코드로** EXCenterPivotView **생성**

* 먼저 MainView.js 파일을 오픈
* onInitDone() 함수에서 아래와 같이 코드를 입력



* addRow 예제

```javascript
onInitDone() {
    super.onInitDone();

    // CenterPivotView 생성
    const pivot = new EXCenterPivotView();
    pivot.createElement();
    this.addComponent(pivot);
    pivot.init();

    pivot.addRow(['L100', 'L200', 'L300'], ['Center1'], ['R100', 'R200', 'R300']);
    pivot.addRow(['L101', 'L201', 'L301'], ['Center2'], ['R101', 'R201', 'R301']);
    pivot.addRow(['L102', 'L202', 'L302'], ['Center3'], ['R102', 'R202', 'R302']);
    pivot.addRow(['L103', 'L203', 'L303'], ['Center4'], ['R103', 'R203', 'R303']);
    pivot.addRow(['L104', 'L204', 'L304'], ['Center5'], ['R104', 'R204', 'R304']);
    pivot.addRow(['L105', 'L205', 'L305'], ['Center6'], ['R105', 'R205', 'R305']);

    pivot.setPos(100, 100);
    pivot.scrollViewLeft();

    this.pivotView = pivot;
}

```



* prependRow 예제

```javascript
onInitDone() {
    super.onInitDone();
    
    // CenterPivotView 생성
    const pivot = new EXCenterPivotView();
    pivot.createElement();
    this.addComponent(pivot);
    pivot.init();
    
    pivot.prependRow(['L105', 'L205', 'L305'], ['Center6'], ['R105', 'R205', 'R305']);
    pivot.prependRow(['L104', 'L204', 'L304'], ['Center5'], ['R104', 'R204', 'R304']);
    pivot.prependRow(['L103', 'L203', 'L303'], ['Center4'], ['R103', 'R203', 'R303']);
    pivot.prependRow(['L102', 'L202', 'L302'], ['Center3'], ['R102', 'R202', 'R302']);
    pivot.prependRow(['L101', 'L201', 'L301'], ['Center2'], ['R101', 'R201', 'R301']);
    pivot.prependRow(['L100', 'L200', 'L300'], ['Center1'], ['R100', 'R200', 'R300']);
    
    pivot.setPos(100, 100);
    pivot.scrollViewLeft();
    
    this.pivotView = pivot;
}
```

<figure><img src="../../.gitbook/assets/화면 녹화 중 2025-07-02 104537.gif" alt=""><figcaption></figcaption></figure>

<mark style="color:red;">**Build 에러 발생 시**</mark>

1. _**프로젝트 트리뷰에서 Framework > afc 우클릭 > Default Load Settings.. > Component > AGrid.js + AGridEvent.js 체크**_
2. _**프로젝트 트리뷰에서 Framework > stock 우클릭 > Default Load Settings.. > Component > ExCenterPivotView.js + EXCenterPivotViewEvent.js 체크**_

<div><figure><img src="../../.gitbook/assets/스크린샷 2025-06-30 132154.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/스크린샷 2025-06-30 131803.png" alt=""><figcaption></figcaption></figure></div>
