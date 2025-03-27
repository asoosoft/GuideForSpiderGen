# GridLayout

![](../../.gitbook/assets/gridlayout-comp-00.png)

GridLayout은 화면의 영역을 구분하기 위해 사용되는 그리드 기반의 레이아웃 컴포넌트.

### Property

#### 주요 속성

* **Rows**: 현재 로우의 총 개수
* **Cols**: 현재 컬럼의 총 개수
* **Cell Height**: 선택한 셀의 높이를 설정하는 속성
* **Cell Width**: 선택한 셀의 넓이를 설정하는 속성
* **Cell Padding**: 선택한 셀의 패딩을 설정하는 속성
* **Cell Color**: 선택한 셀의 배경색을 설정하는 속성

### Cell Borders

* 선택된 셀의 **top line**만 설정
* 선택된 셀의 **horizontal middle line**만 설정
* 선택된 셀의 **bottom line**만 설정
* 선택된 셀의 **left line**만 설정
* 선택된 셀의 **vertical middle line**만 설정
* 선택된 셀의 **right line**만 설정
* **All**: 선택된 셀의 모든 border를 설정
* **OutLine**: 선택된 셀의 테두리 line만 설정
* **Clear**: 선택된 셀에 적용된 border를 초기화

### Cell Context Menu

* **Merge**: 현재 선택한 셀들을 하나의 셀로 합병
* **Split**: Merge된 셀을 원래의 셀들로 분리
* **Insert Row**: 현재 선택한 셀 앞에 Row를 추가
* **Delete Row**: 현재 선택한 셀의 Row를 삭제
* **Insert Col**: 현재 선택한 셀 앞에 Column을 추가
* **Delete Col**: 현재 선택한 셀을 삭제
* **Col H-Align**: 선택한 셀 내의 element를 가로 정렬
  * **center**: 중앙 정렬
  * **left**: 좌측 정렬
  * **right**: 우측 정렬
  * **justify**: 셀 내의 element를 넓이에 맞게 사이즈 조정
* **Col V-Align**: 선택한 셀 내의 element를 세로 정렬
  * **middle**: 세로 중앙 정렬
  * **top**: 맨 상단 정렬
  * **bottom**: 맨 하단 정렬
  * **baseline**: 기준선에 맞춰 정렬

### Example

#### 1. 컴포넌트 추가

* Component ui를 사용해서 GridLayout 컴포넌트를 화면에 추가함.
* GridLayout 컴포넌트를 선택한 후 오른쪽 클릭 → Grid Layout Property를 선택함.

![](../../.gitbook/assets/GridLayout001.png)

* Cell Height & Width를 동일하게 설정함
* GridLayout Property 다이얼로그에서 다음과 같이 속성을 설정Rows: 3, Cols: 2
* 맨 위에 있는 붙어있는 두 셀을 선택한 뒤 우클릭 후 Merge선택 (병합)
* 맨 아래에 있는 붙어있는 두 셀을 선택한 뒤 우클릭 후 Merge선택 (병합)

![](../../.gitbook/assets/GridLayout04.png) ![](../../.gitbook/assets/GridLayout06.png)

* AView 컴포넌트를 화면에 추가 후 각각 다른 색상을 설정
* GridLayout에 AView를 드래그앤드롭으로 추가함

![](../../.gitbook/assets/GridLayout07.png)

#### 2. 프로젝트 실행

* 프로젝트를 빌드하고 실행.
* 페이지를 늘리고 줄여보면서 화면의 변화를 확인.
