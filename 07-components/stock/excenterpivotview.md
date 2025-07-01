# ExCenterPivotView

트레이딩 화면의 중심에 위치하는 주요 UI 컴포넌트.&#x20;



현재 선택된 종목의 핵심 정보(현재가, 변동률, 거래량 등)를 표시하며, 타 위젯들과 상태를 연동하여 트레이딩 화면의 중심 역할.

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

```javascript
onInitDone() {
    super.onInitDone();

    // 배치한 컴포넌트 이름 기준 (ex: pivotView)
    // 만약 컴포넌트 이름이 다르면 수정하세요.

    // 🔸 왼쪽 그리드 데이터
    this.pivotView.leftGrid.setData([
        ['왼쪽1', '왼쪽2', '왼쪽3'], // 👉 헤더
        ['L100', 'L200', 'L300'],    // 👉 데이터
        ['L101', 'L201', 'L301']
    ]);

    // 🔸 피벗(중앙) 그리드 데이터
    this.pivotView.pivotGrid.setData([
        ['중심'],      // 👉 헤더
        ['Center-1'], // 👉 데이터
        ['Center-2']
    ]);

    // 🔸 오른쪽 그리드 데이터
    this.pivotView.rightGrid.setData([
        ['오른쪽1', '오른쪽2', '오른쪽3'], // 👉 헤더
        ['R100', 'R200', 'R300'],         // 👉 데이터
        ['R101', 'R201', 'R301']
    ]);

    // 🔸 스크롤 초기화 (왼쪽 기준 정렬)
    this.pivotView.scrollViewLeft();
}
```

**3. 프로젝트 실행**

* 설정한 데이터에 맞춰서 각 가격과 거래량, 평균가, 현재가가 표시

<figure><img src="../../.gitbook/assets/스크린샷 2025-06-30 132530.png" alt=""><figcaption></figcaption></figure>

**4. 코드로** EXCenterPivotView **생성**

* 먼저 MainView.js 파일을 오픈
* onInitDone() 함수에서 아래와 같이 코드를 입력

```
onInitDone() {
    super.onInitDone();

    const pivot = new EXCenterPivotView();
    pivot.createElement();
    this.addComponent(pivot);
    pivot.init();

    // 🔸 왼쪽 그리드
    pivot.leftGrid.setData([
        ['왼쪽1', '왼쪽2', '왼쪽3'],   // 헤더
        ['L100', 'L200', 'L300'],      // 데이터
        ['L101', 'L201', 'L301']
    ]);

    // 🔸 중앙 피벗 그리드
    pivot.pivotGrid.setData([
        ['중심'], 
        ['Center1'], 
        ['Center2']
    ]);

    // 🔸 오른쪽 그리드
    pivot.rightGrid.setData([
        ['오른쪽1', '오른쪽2', '오른쪽3'],
        ['R100', 'R200', 'R300'],
        ['R101', 'R201', 'R301']
    ]);

    pivot.setPos(100, 100);
    pivot.scrollViewLeft();

    this.pivotView = pivot;
}
```

<figure><img src="../../.gitbook/assets/스크린샷 2025-06-30 131431.png" alt=""><figcaption></figcaption></figure>

<mark style="color:red;">**Build 에러 발생 시**</mark>

1. _**프로젝트 트리뷰에서 Framework > afc 우클릭 > Default Load Settings.. > Component > AGrid.js + AGridEvent.js 체크**_
2. _**프로젝트 트리뷰에서 Framework > stock 우클릭 > Default Load Settings.. > Component > ExCenterPivotView.js + EXCenterPivotViewEvent.js 체크**_

<div><figure><img src="../../.gitbook/assets/스크린샷 2025-06-30 132154.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/스크린샷 2025-06-30 131803.png" alt=""><figcaption></figcaption></figure></div>
