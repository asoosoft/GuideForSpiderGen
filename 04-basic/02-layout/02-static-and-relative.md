# 02  Static & Relative

Static, Relative는 컴포넌트의 위치와 배열을 설정하는 데 중요한 역할.

### Static

컴포넌트의 기본 위치 설정 방식으로, 컴포넌트가 문서의 일반적인 흐름에 따라 배치.

Static으로 설정된 컴포넌트는 다른 요소에 의해 밀려나거나 겹쳐지지 않으며, 일반적인 문서 흐름에 따라 배치.

Static 위치는 기본값으로, 특별한 위치 지정이 필요하지 않은 경우에 사용.

### Relative

컴포넌트의 위치를 부모 요소나 이전 위치를 기준으로 상대적으로 설정하는 방식.

Relative로 설정된 컴포넌트는 기본 위치에서 지정된 오프셋만큼 이동할 수 있으며, 다른 요소의 배치에 영향을 주지 않음.

Relative 위치는 컴포넌트를 기존 위치에서 약간 조정해야 할 때 유용.

### Static, Relative 차이

#### Static

| Component | Position                        | Size                               | Layout           |
| --------- | ------------------------------- | ---------------------------------- | ---------------- |
| AButton   | <p>Left: 0<br>Top: 0</p>        | <p>Width: 80px<br>Height: 22px</p> | Position: static |
| AButton   | <p>Left: 0<br>Top: 20px</p>     | <p>Width: 80px<br>Height: 22px</p> | Position: static |
| AButton   | <p>Left: 100px<br>Top: 50px</p> | <p>Width: 80px<br>Height: 22px</p> | Position: static |

![](https://wikidocs.net/images/page/276192/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-14_142513.png)

* 기본값으로, 컴포넌트는 문서의 일반적인 흐름에 따라 배치.
* static으로 설정된 컴포넌트는 상위 요소의 위치나 다른 요소의 위치에 영향을 받지 않고, 일반적인 문서 흐름에 따라 배치.
* top, right, bottom, left와 같은 위치 속성은 static 요소에 적용되지 않음.

#### Relative

| Component | Position                        | Size                               | Layout             |
| --------- | ------------------------------- | ---------------------------------- | ------------------ |
| AButton   | <p>Left: 0<br>Top: 0</p>        | <p>Width: 80px<br>Height: 22px</p> | Position: relative |
| AButton   | <p>Left: 0<br>Top: 20px</p>     | <p>Width: 80px<br>Height: 22px</p> | Position: relative |
| AButton   | <p>Left: 100px<br>Top: 50px</p> | <p>Width: 80px<br>Height: 22px</p> | Position: relative |

![](https://wikidocs.net/images/page/276192/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-14_142052.png)

* 기본적으로 static과 같은 위치에 배치되지만, top, right, bottom, left 속성을 사용하여 자신의 원래 위치에서 상대적으로 이동.
* 컴포넌트는 자신의 원래 위치를 기준으로 이동하며, 다른 요소의 배치에는 영향을 주지 않음.

### 예제

#### 1. AView 컴포넌트 생성

| Component | Position                        | Size                                            | Layout                                      |
| --------- | ------------------------------- | ----------------------------------------------- | ------------------------------------------- |
| AView     | <p>Left: 0<br>Top: 0</p>        | <p>Width: 100%<br>Height: 100px</p>             | Position: absolute                          |
| AView     | <p>Left: 0<br>Top: 100px</p>    | <p>Width: 20%<br>Height:<br>Stretch - 100px</p> | <p>Position: absolute<br>Display: block</p> |
| AView     | <p>Top: 100px<br>Right: 0px</p> | <p>Width: 80%<br>Height:<br>Stretch - 100px</p> | <p>Position: absolute<br>Display: block</p> |
| AView     | <p>Left: 0<br>Bottom: 0</p>     | <p>Width: 100%<br>Height: 100px</p>             | Position: absolute                          |

![](https://wikidocs.net/images/page/276192/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-17_090403.png)

#### 2. 1에서 만든 AView를 부모로 AButton 컴포넌트 생성하고 relative, static 활용

**relative**

| Component | Position                     | Size                                | Layout             |
| --------- | ---------------------------- | ----------------------------------- | ------------------ |
| AButton   | <p>Left: 0<br>Top: 0</p>     | <p>Width: 200px<br>Height: 100%</p> | Position: relative |
| AButton   | <p>Left: 180px<br>Top: 0</p> | <p>Width: 200px<br>Height: 100%</p> | Position: relative |
| AButton   | <p>Left: 390px<br>Top: 0</p> | <p>Width: 200px<br>Height: 100%</p> | Position: relative |

![](https://wikidocs.net/images/page/276192/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-17_090628.png)

* relative는 다른 컴포넌트의 위치에 따라 배치에 영향.

**static**

| Component | Margin                                        | Size                                            | Layout                                           |
| --------- | --------------------------------------------- | ----------------------------------------------- | ------------------------------------------------ |
| AButton   | <p>Left: 10%<br>Top: 10px<br>Bottom: 50px</p> | <p>Width: 80%<br>Height: 150px</p>              | <p>Position: static<br>Display: inline-block</p> |
| AButton   | <p>Left: 10%<br>Bottom: 50px</p>              | <p>Width: 80%<br>Height:<br>Stretch - 100px</p> | <p>Position: static<br>Display: inline-block</p> |
| AButton   | <p>Left: 10%<br>Bottom: 50px</p>              | <p>Width: 80%<br>Height:<br>Stretch - 100px</p> | <p>Position: static<br>Display: inline-block</p> |
| AButton   | <p>Left: 10%<br>Bottom: 50px</p>              | <p>Width: 80%<br>Height: 100px</p>              | <p>Position: static<br>Display: inline-block</p> |

![](https://wikidocs.net/images/page/276192/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-17_090651.png)

* static으로 설정한 요소들은 Position 값에 영향을 받지 않기 때문에 Margin을 활용하여 컴포넌트 배치.

#### 3. AButton 컴포넌트에 이미지 생성

| Component | Size                                | Layout           | Margin       | Border      |
| --------- | ----------------------------------- | ---------------- | ------------ | ----------- |
| AButton   | <p>Width: 100%<br>Height: 100px</p> | Position: static | Bottom: 10px | Round: 10px |

**이미지 첨부 방법**

* Assets 폴더 우클릭 > New Folder > 이름 img로 설정 후 OK > img 폴더 우클릭 > Add existing files 클릭 > 이미지 첨부![](https://wikidocs.net/images/page/276192/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-14_150434.png)
* Attribute > Data > icon 옆 오른쪽 박스 클릭

![](https://wikidocs.net/images/page/276192/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-14_150707.png)

* Image Picker > show all 클릭 > Add existing files로 추가한 이미지 선택

![](https://wikidocs.net/images/page/276192/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-14_150814.png)

![](https://wikidocs.net/images/page/276192/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-17_092142.png)

### 참조

* [https://www.youtube.com/watch?v=OBgK6fw8qtY](https://www.youtube.com/watch?v=OBgK6fw8qtY)
* [https://www.youtube.com/watch?v=ZmCWQovYUfo](https://www.youtube.com/watch?v=ZmCWQovYUfo)
