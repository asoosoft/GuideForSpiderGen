# 03. Container 를 사용한 컴포넌트 배치

### View

스파이더젠에서 View는 사용자 인터페이스의 기본 구성 요소로, **다양한 UI 컴포넌트를 배치하고 관리**할 수 있는 컨테이너 역할을 함. View는 레이아웃 파일(.lay)을 통해 정의되며, 다양한 속성과 메서드를 통해 동적으로 UI를 구성할 수 있음.

> 사용 예시

![](../../.gitbook/assets/View02.png)

#### 언제 사용할까?

**✅ View는 UI의 특정 화면을 구성할 때 사용**

**✅ 복잡한 UI를 모듈화하고, View 간의 상호작용을 통해 동적인 화면 전환을 구현할 때 사용**

**✅ 화면 크기, 테마 변경, 반응형 디자인 등 다양한 환경에 맞춰 유연하게 관리할 때 사용**

> 자세한 구현은 링크 참조[ View](../../07-components/afc/11-view.md)

### GridLayout

스파이더젠의 GridLayout은 화면의 영역을 구분하기 위해 사용되는 컴포넌트입니다. 이 레이아웃은 행(Row)과 열(Col)로 구성되어 있으며, **각 셀(Cell)에 다양한 UI 컴포넌트를 배치**할 수 있음. GridLayout을 사용하면 **복잡한 레이아웃을 쉽게 관리**하고 구성할 수 있음.

> 사용 예시

![](../../.gitbook/assets/GridLayout02.png)

> 응용 예시

![](../../.gitbook/assets/GridLayout01.png)

#### 언제 사용할까?

**✅ 웹 페이지 전체 레이아웃을 구성할 때 사용**

**✅ 정확한 행(Row)과 열(Column) 배치가 필요한 경우 사용**

**✅ 복잡한 UI를 만들 때 사용**

> 자세한 구현은 링크 참조 [GridLayout](../../07-components/afc/20-gridlayout.md)

### FlexLayout

스파이더젠의 FlexLayout은 컴포넌트 배열과 **정렬을 유연하게 관리**할 수 있는 레이아웃 컴포넌트. FlexLayout을 사용하면 다양한 UI 요소를 손쉽게 배치하고 정렬할 수 있음.

> 사용 예시

![](../../.gitbook/assets/FlexLayout_01.png)

> 응용 예시

![](../../.gitbook/assets/FlexLayout02.png)

#### 언제 사용할까?

**✅ 한 줄(Row) 또는 한 열(Column) 정렬이 필요할 때 사용**

**✅ 반응형 웹에서 유동적인 정렬이 필요할 때 사용**

**✅ 버튼 그룹, 네비게이션 바, 카드 레이아웃 등을 만들 때 사용**

> 자세한 구현은 링크 참조 [FlexLayout](../../07-components/afc/23-flexlayout.md)

### Vertical

스파이더젠에서 Vertical은 주로 레이아웃이나**컴포넌트의 방향성을 설정** 할 때 사용되는 속성. 여러 컴포넌트에서 이 속성을 통해 자식 요소들이 **수직 방향으로 배치**되도록 설정할 수 있음. 예를 들어, FlexLayout이나 SlideView와 같은 컴포넌트에서 Vertical 속성을 사용하여 자식 요소들이 위에서 아래로 배치되도록 할 수 있음.

> 사용 예시

![](../../.gitbook/assets/Vertical02.png)

> 응용 예시

![](../../.gitbook/assets/Vertical001.png)

#### 언제 사용할까?

**✅ 요소를 왼쪽, 오른쪽, 가운데 정렬해야 할 때 사용**

**✅ 네비게이션 바를 가로로 정렬할 때 사용**

**✅ 버튼을 가로로 정렬할 때 사용**

**✅ 카드형 UI를 가로로 배치할 때 사용**

> 자세한 구현은 링크 참조 [Vertical](<../07  Components/39 Vertical.md>)

### Horizontal

스파이더젠에서 Horizontal은 주로 레이아웃이나 컴포넌트의 방향성을 설정할 때 사용되는 속성. 여러 컴포넌트에서 이 속성을 통해 자식 요소들이 **수평 방향으로 배치**되도록 설정할 수 있음. 예를 들어, FlexLayout이나 SlideView와 같은 컴포넌트에서 Horizontal 속성을 사용하여 자식 요소들이 왼쪽에서 오른쪽으로 배치되도록 할 수 있음.

> 사용 예시

![](../../.gitbook/assets/Horizontal.png)

> 응용 예시

![](../../.gitbook/assets/Horizontal02.png)

#### 언제 사용할까?

**✅ 폼 입력 필드를 세로로 배치해야 할 때 사용**

**✅ 버튼 그룹을 세로로 정렬해야 할 때 사용**

**✅ 페이지 내 요소를 세로 중앙 정렬할 때 사용**

\*\*✅ 플렉스 컨테이너 안에서 텍스트 또는 아이콘을 세로로 정렬할 때 \*\*

> 자세한 구현은 링크 참조 [Horizontal](<../07  Components/40 Horizontal.md>)
