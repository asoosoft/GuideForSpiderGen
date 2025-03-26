# 01. Position & Layout

스파이더젠에서 Position & Layout은 컴포넌트의 위치와 배열을 설정하는 중요한 요소.

이를 통해 사용자 인터페이스의 구조와 디자인을 정의.

### Position

컴포넌트의 위치와 크기를 설정하는 데 사용.

이는 컴포넌트가 부모 컨테이너 내에서 어디에 배치될지를 결정.

position 속성은 주로 픽셀(px) 단위로 설정되며, 컴포넌트의 left, top, right, bottom 등의 속성을 통해 구체적인 위치를 지정.

예를 들어, left: 20px, top: 50px와 같이 설정하면 컴포넌트가 부모 컨테이너의 왼쪽에서 20픽셀, 위쪽에서 50픽셀 떨어진 위치에 배치.

### Layout

layout은 여러 컴포넌트를 어떻게 배열하고 정렬할지를 정의하는 방식.

스파이더젠에서는 FlexLayout과 GridLayout 같은 다양한 레이아웃 컴포넌트를 제공하여 복잡한 UI 구조를 쉽게 구성.

### View

스파이더젠의 메뉴바에 있는 "View"는 사용자 인터페이스의 다양한 요소를 관리하고 조정하는 데 사용되는 기능을 제공.

이 메뉴는 주로 개발 환경에서 작업할 때 필요한 다양한 뷰를 열거나 닫는 데 사용.

#### View 구성 요소

**1. Component (Ctrl + 1)**

스파이더젠에서 UI를 구성하는 기본 단위.

버튼, 레이블, 차트 등 다양한 형태의 컴포넌트가 있으며, 각 컴포넌트는 특정한 기능과 속성을 가짐.

컴포넌트는 프로젝트 내에서 시각적 요소를 구성하고 사용자와 상호작용이 가능.

![](../../.gitbook/assets/스크린샷_2025-02-14_110453.png)

**2. Project (Ctrl + 2)**

스파이더젠에서 개발하는 애플리케이션의 전체 구조를 의미.

여러 개의 뷰, 레이아웃, 컴포넌트, 그리고 관련된 소스 코드 파일들로 구성.

개발자가 애플리케이션의 기능을 구현하고 관리하는 기본 단위.

![](../../.gitbook/assets/스크린샷_2025-02-14_110821.png)

**3. Placement (Ctrl + 3)**

컴포넌트가 레이아웃 내에서 어떻게 배치되는지를 정의.

컴포넌트의 위치와 크기를 설정하는 데 사용되며, 픽셀 단위로 위치를 지정하거나 레이아웃의 특정 규칙에 따라 배치.

UI 디자인의 시각적 배치를 조정하는 데 중요한 역할.

![](../../.gitbook/assets/스크린샷_2025-02-14_110714.png)

**4. Class (Ctrl + 4)**

스파이더젠에서 컴포넌트의 동작을 정의하는 코드 구조.

각 컴포넌트는 특정 클래스에 의해 제어되며, 클래스는 컴포넌트의 속성, 메서드, 이벤트 핸들러 등을 포함.

컴포넌트의 기능을 확장하고 사용자 정의 동작을 구현하는 데 사용.

![](../../.gitbook/assets/스크린샷_2025-02-14_110909.png)

**5. Appearance (Ctrl + 5)**

컴포넌트의 시각적 속성을 정의하는 요소.

색상, 글꼴, 테두리, 배경 등 컴포넌트의 외형을 설정하는 다양한 속성을 포함.

컴포넌트의 스타일을 조정하고, 전체 UI의 일관성을 유지.

![](../../.gitbook/assets/스크린샷_2025-02-14_110942.png)

**6. Attribute (Ctrl + 6)**

컴포넌트의 특정 속성을 설정하는 데 사용되는 값.

각 컴포넌트는 고유한 속성 집합을 가지며, 이러한 속성은 컴포넌트의 동작과 외형을 제어.

버튼 컴포넌트의 텍스트, 색상, 크기 등을 설정할 수 있는 속성이 Attribute에 해당.

![](../../.gitbook/assets/스크린샷_2025-02-14_111039.png)

### Position & Layout 예제

#### 1. ALabel 생성

| Component | Position                       | Layout             | Size                               |
| --------- | ------------------------------ | ------------------ | ---------------------------------- |
| ALabel    | <p>Left: 20px<br>Top: 30px</p> | Position: absolute | <p>width: auto<br>height: auto</p> |

![](../../.gitbook/assets/스크린샷_2025-02-14_102917.png)

#### 2. ATextField 생성

| Component  | Position                        | Layout             | Size                                            |
| ---------- | ------------------------------- | ------------------ | ----------------------------------------------- |
| ATextField | <p>Left: 110px<br>Top: 30px</p> | Position: absolute | <p>width:<br>stretch: 120px<br>height: 30px</p> |

![](../../.gitbook/assets/스크린샷_2025-02-14_102957.png)

#### 3. AButton 생성

| Component | Position                        | Layout             | Size                               |
| --------- | ------------------------------- | ------------------ | ---------------------------------- |
| AButton   | <p>Right: 20px<br>Top: 25px</p> | Position: absolute | <p>width: 80px<br>height: 30px</p> |

![](../../.gitbook/assets/스크린샷_2025-02-14_103036.png)

#### 4. AGrid 생성

| Component | Position                       | Layout             | Size                                                        |
| --------- | ------------------------------ | ------------------ | ----------------------------------------------------------- |
| AGrid     | <p>Left: 20px<br>Top: 80px</p> | Position: absolute | <p>width:<br>stretch: 20px<br>height:<br>stretch: 100px</p> |

![](../../.gitbook/assets/스크린샷_2025-02-14_103057.png)

#### 5. AView 생성

| Component | Position                        | Layout             | Size                                |
| --------- | ------------------------------- | ------------------ | ----------------------------------- |
| AView     | <p>Bottom: 30px<br>center X</p> | Position: absolute | <p>width: 170px<br>height: 40px</p> |

![](../../.gitbook/assets/스크린샷_2025-02-14_103212.png)

#### 6. AView를 부모 컨테이너로 AButton 2개 생성

| Component | Position                  | Layout             | Size                               |
| --------- | ------------------------- | ------------------ | ---------------------------------- |
| AButton   | <p>Left: 0<br>Top: 0</p>  | Position: absolute | <p>width: 80px<br>height: 100%</p> |
| AButton   | <p>Right: 0<br>Top: 0</p> | Position: absolute | <p>width: 80px<br>height: 100%</p> |

![](../../.gitbook/assets/스크린샷_2025-02-14_103303.png)

#### 7. 실행

![](../../.gitbook/assets/스크린샷_2025-02-14_103349.png)

[참조: 유튜브](https://www.youtube.com/watch?v=5imOh3KAvW0)
