# CandleChart

<figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 112359.png" alt=""><figcaption></figcaption></figure>

#### Appearance

공통 Appearance 는 **6. Global Properties** 속성을 참고

#### Attribute

CandleChart 속성

<figure><img src="../../.gitbook/assets/스크린샷 2025-07-02 112736.png" alt=""><figcaption></figcaption></figure>



**Data**

<table data-header-hidden><thead><tr><th width="361"></th><th></th></tr></thead><tbody><tr><td><strong>이름</strong></td><td><strong>설명</strong></td></tr><tr><td><code>Mode</code></td><td>차트 타입 선택</td></tr><tr><td><code>Intervals</code></td><td><p>데이터의 시간 간격 선택</p><p> <code>CandleChart.INTERVALS_*</code> 값과 매칭</p></td></tr><tr><td><code>Indicator</code></td><td><p>하단 보조 지표 선택 </p><p><code>CandleChart.INDICATOR_*</code> 값 활용</p></td></tr></tbody></table>

**Color**

<table data-header-hidden><thead><tr><th width="361"></th><th></th></tr></thead><tbody><tr><td><strong>이름</strong></td><td><strong>설명</strong></td></tr><tr><td><code>Text</code></td><td>차트 내 일반 텍스트 색상 (날짜, 가격 등)</td></tr><tr><td><code>Up</code></td><td>상승 봉의 색상</td></tr><tr><td><code>Divide Line</code></td><td>차트 영역을 구분하는 선 색상</td></tr><tr><td><code>Down</code></td><td>하락 봉의 색상</td></tr><tr><td><code>Longtab Line</code></td><td>롱탭(혹은 마우스 오버) 시 나타나는 세로/가로 선 색상</td></tr><tr><td><code>Dot</code></td><td>배경의 점선 라인 (격자) 색상</td></tr><tr><td><code>LineMode Line</code></td><td>라인 차트 모드일 때 라인 색상</td></tr><tr><td><code>Volume</code></td><td>거래량 막대 색상</td></tr></tbody></table>

**Current Price Color**

<table data-header-hidden><thead><tr><th width="361"></th><th></th></tr></thead><tbody><tr><td><strong>이름</strong></td><td><strong>설명</strong></td></tr><tr><td><code>Up Bg</code></td><td>상승 상태의 현재가 배경색</td></tr><tr><td><code>Up Text</code></td><td>상승 상태의 현재가 텍스트 색</td></tr><tr><td><code>Down Bg</code></td><td>하락 상태의 현재가 배경색</td></tr><tr><td><code>Down Text</code></td><td>하락 상태의 현재가 텍스트 색</td></tr></tbody></table>

**Option**

<table data-header-hidden><thead><tr><th width="361"></th><th></th></tr></thead><tbody><tr><td><strong>이름</strong></td><td><strong>설명</strong></td></tr><tr><td><code>Touch Event</code></td><td>터치 이벤트 활성화</td></tr></tbody></table>



#### Example

**1. 프로젝트 생성**

* 프로젝트 트리뷰에서 Source > MainView.lay 파일을 클릭
* MainView의 레이아웃 파일이 오픈되면 컴포넌트 리스트에서 CandleChart 컴포넌트를 선택하고 드래그하여 레이아웃에 배치
* Class에서 ID를 CandleChart 로 입력

**2. 데이터 설정**

* 먼저 MainView.js 파일을 오픈
* 상단의 파일탭에서 MainView.lay 탭을 더블 클릭하거나 우측의 프로젝트 트리에서 MainView.js 파일을 더블 클릭
* 모든 화면뷰는 onInitDone() 함수가 존재하며 이 함수는 화면이 생성될 때 딱 한번 실행
* onInitDone() 함수에서 레이블의 텍스트 내용을 아래와 같이 코드를 입력

```javascript
onInitDone() {
    super.onInitDone();


}
```

**3. 프로젝트 실행**

* 설정한 데이터에 맞춰서 상승, 하향 화살표가 표시



**4. 코드로** CandleChart **생성**

* 먼저 MainView.js 파일을 오픈
* onInitDone() 함수에서 아래와 같이 코드를 입력

```javascript
onInitDone() {
    super.onInitDone();


}

```
