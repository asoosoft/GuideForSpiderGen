# FlexLayout

![](../../.gitbook/assets/flexlayout-comp-01.png)

컴포넌트 배열과 정렬을 위해 사용하는 레이아웃 컴포넌트.

### Attribute

![](../../.gitbook/assets/스크린샷_2025-01-24_105017.png)

#### 1. Direction

| Direction      | 자식 요소의 방향성을 설정하는 속성           |
| -------------- | ----------------------------- |
| row            | 기본값. 자식 요소를 수평 방향(좌->우)으로 배치. |
| row-reverse    | 자식 요소를 수평 방향(우->좌)으로 배치.      |
| column         | 자식 요소를 수직 방향(상->하)으로 배치.      |
| column-reverse | 자식 요소를 수직 방향(하->상)으로 배치.      |

* row 예시화면

![](../../.gitbook/assets/dir-row.png)



* row-reverse 예시화면

![](../../.gitbook/assets/dir-rowreverse.png)



* column 예시화면

![](../../.gitbook/assets/dir-column.png)



* column-reverse 예시화면

![](../../.gitbook/assets/dir-columreverse.png)

#### 2. Wrap

| Wrap         | 자식 요소의 줄넘김 처리를 설정하는 속성      |
| ------------ | --------------------------- |
| nowrap       | 기본값. 자식 요소를 한 줄에 모두 배치.     |
| wrap         | 자식 요소가 적정 길이보다 길면 다음 줄에 배치. |
| wrap-reverse | wrap과 같으나 역방향으로 배치.         |

* wrap 예시화면

![](../../.gitbook/assets/wrap.png)

* wrap-reverse 예시화면

![](../../.gitbook/assets/wrap-reverse.png)

#### 3. Justify Content

| Justify Content | 자식 요소의 수평 방향 정렬 속성       |
| --------------- | ------------------------ |
| flex-start      | 자식 요소를 수평 방향의 시작점에 배치.   |
| center          | 자식 요소를 수평 방향의 중앙에 배치.    |
| flex-end        | 자식 요소를 수평 방향의 끝점에 배치.    |
| space-between   | 자식 요소를 양쪽 끝에 맞춰 정렬.      |
| space-around    | 자식 요소 전후에 일정한 간격을 두고 정렬. |
| space-evenly    | 자식 요소 사이에 동일한 간격을 두고 정렬. |

* center 예시화면

![](../../.gitbook/assets/just-center.png)



* flex-end 예시화면

![](../../.gitbook/assets/just-flexend.png)



* space-between 예시화면

![](../../.gitbook/assets/just-spacebetw.png)



* space-around 예시화면

![](../../.gitbook/assets/just-spacearound.png)



* space-evenly 예시화면

![](../../.gitbook/assets/just-spaceeven.png)



#### 4. Align Items

| Align Items | 자식 요소의 수직 방향 정렬 속성.          |
| ----------- | ---------------------------- |
| stretch     | 자식 요소를 수직 방향의 시작점에서 끝점까지 늘림. |
| flex-start  | 자식 요소를 수직 방향의 시작점에 배치.       |
| center      | 자식 요소를 수직 방향의 중간점에 배치.       |
| flex-end    | 자식 요소를 수직 방향의 끝점에 배치.        |
| base-line   | 자식 요소를 수직 방향의 베이스라인에 배치.     |

* stretch 예시화면

![](../../.gitbook/assets/align-stretch.png)



* center 예시화면

![](../../.gitbook/assets/align-center.png)



* flex-end 예시화면

![](../../.gitbook/assets/align-flexend.png)



* baseline 예시화면

![](../../.gitbook/assets/align-baseline.png)



#### 5. Align Content

| Align Content | 자식 요소들의 수직 공간 분배를 제어하는 속성.(Wrap 속성을 wrap이나 wrap-reverse를 설정해야 적용) |
| ------------- | ----------------------------------------------------------------- |
| flex-start    | 자식 요소를 컨테이너의 시작점에 배치.                                             |
| center        | 자식 요소를 컨테이너의 중앙에 배치.                                              |
| flex-end      | 자식 요소를 컨테이너의 끝점에 배치.                                              |
| stretch       | 자식 요소를 컨테이너의 높이에 맞춰 늘리는 옵션.                                       |
| space-between | 자식 요소 사이에 동일한 간격을 배치.                                             |
| space-around  | 자식 요소의 주위에 동일한 간격을 배치.                                            |

* center 예시화면

![](../../.gitbook/assets/contend-center.png)



* flex-end 예시화면

![](../../.gitbook/assets/content-flexend.png)



* stretch 예시화면

![](<../../.gitbook/assets/align-stretch (1).png>)



* space-around 예시화면

![](../../.gitbook/assets/content-spacearound.png)

### Example

#### 화면에 컴포넌트 생성

![](../../.gitbook/assets/스크린샷_2025-01-24_165601.png)

#### 코드로 컴포넌트 생성

* Framework > afc > Default Load Settings

![](../../.gitbook/assets/스크린샷_2025-02-18_143530.png)

* AFlexLayout.js 선택 > 창닫기

![](../../.gitbook/assets/스크린샷_2025-02-18_143542.png)

* 변경된 정보를 저장하시겠습니까> -> Yes

![](../../.gitbook/assets/스크린샷_2025-02-18_143555.png)

* js에 코드 추가

```
onInitDone() {
	    super.onInitDone()
	    
	    // FlexLayout 인스턴스 생성
	    const flexLayout = new  AFlexLayout();
	    flexLayout.init(); // 초기화
	    
	    // FlexLayout 설정
	    flexLayout.getElement().style.backgroundColor = 'blue';
	    flexLayout.getElement().style.width = '400px'; // 또는 원하는 크기
	    flexLayout.getElement().style.height = '100px'; // 또는 원하는 크기
	    
	    // 부모 레이아웃에 FlexLayout 추가
	    this.getContainer().addComponent(flexLayout);
    }
```

* 실행 결과

![](../../.gitbook/assets/스크린샷_2025-02-18_143612.png)

#### FlaxLayout 전용 기능

* FlexLayout 컴포넌트에서 마우스 우클릭 -> Flex Layout Property

![](../../.gitbook/assets/스크린샷_2025-01-24_113534.png)

* 기능

![](../../.gitbook/assets/스크린샷_2025-01-24_113709.png)

| 속성      | 설명                                                     |
| ------- | ------------------------------------------------------ |
| gap     | 자식 요소들 사이의 간격을 설정하는 데 사용.                              |
| order   | 각 자식 요소의 배치 순서를 제어하는 데 사용.                             |
| grow    | 자식 요소가 Flex 컨테이너 내에서 가용 공간을 어떻게 나누어 가질지를 결정하는 데 사용.    |
| shrink  | 자식 요소가 Flex 컨테이너의 크기가 줄어들 때, 얼마나 줄어들 수 있는지를 결정하는 데 사용. |
| align   | 각 자식 요소의 정렬 방식을 제어하는 데 사용.                             |
| basis   | 자식 요소의 기본 크기를 설정하는 데 사용.                               |
| padding | 자식 요소의 콘텐츠와 요소의 경계 사이의 내부 여백을 설정.                      |
| margin  | 자식 요소의 경계와 다른 요소 또는 컨테이너 경계 사이의 외부 여백을 설정.             |
