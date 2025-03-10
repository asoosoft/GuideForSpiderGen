# 03  Button

![](https://wikidocs.net/images/page/24562/btn-comp-00.png)

사용자와의 상호작용을 처리하는 데 사용 및 클릭 이벤트를 통해 특정 기능을 수행하는 **버튼 컴포넌트**

![](https://wikidocs.net/images/page/24562/1.png)

### Data

* **Text** 버튼의 텍스트를 설정하는 속성.
* **Align** 텍스트의 정렬을 설정하는 속성.

| Align    | 설명               |
| -------- | ---------------- |
| `left`   | 버튼 텍스트 좌측 정렬     |
| `center` | 버튼 텍스트 텍스트 중앙 정렬 |
| `right`  | 버튼 텍스트 우측 정렬     |

* **Icon** : 버튼에 아이콘을 삽입하는 속성.

| Icon            | 설명                |
| --------------- | ----------------- |
| `After Text`    | 아이콘이 텍스트 다음에 위치   |
| `New Line Text` | 아이콘과 텍스트를 위아래로 위치 |

![](https://wikidocs.net/images/page/24562/%ED%99%94%EB%A9%B4_%EC%BA%A1%EC%B2%98_2025-01-22_161501.png)\
`기본`

![](https://wikidocs.net/images/page/24562/%ED%99%94%EB%A9%B4_%EC%BA%A1%EC%B2%98_2025-01-22_161544.png)\
`✅After Text`

![](https://wikidocs.net/images/page/24562/%ED%99%94%EB%A9%B4_%EC%BA%A1%EC%B2%98_2025-01-22_161610.png)\
`✅New Line Text`

![](https://wikidocs.net/images/page/24562/%ED%99%94%EB%A9%B4_%EC%BA%A1%EC%B2%98_2025-01-22_161633.png)\
`✅After Text ✅New Line Text`

### Option

#### Fast Click

버튼을 연속으로 빠르게 클릭할 수 있도록 설정.

> 일반적으로 클릭 이벤트가 발생한 후 버튼이 비활성화되거나 딜레이가 생기는 경우가 있는데, Fast Click 옵션을 사용하면 이러한 딜레이 없이 연속 클릭이 가능.

#### Tool Button

버튼을 툴 버튼으로 설정.

> 툴 버튼은 default, down, over, disable의 네 가지 상태에 따라 버튼의 이미지를 변경. 버튼의 가로 크기의 4배로 이미지를 이어붙여서 버튼의 백그라운드 이미지로 지정하면, 각 상태에 맞는 이미지가 자동으로 변경 됨.

#### Check Button

버튼을 체크박스처럼 사용할 수 있도록 설정.

> 이 옵션을 활성화하면 버튼이 선택되거나 선택 해제될 수 있으며, `setCheck()` 및 `getCheck()` 메서드를 사용하여 버튼의 체크 상태를 제어 가능.

#### Down State

버튼이 눌렸을 때의 상태를 자동으로 조절.

> 버튼이 눌린 상태일 때 배경색의 밝기를 조절하여 시각적으로 눌린 느낌을 제공. 이 옵션을 체크 해제하면 스타일을 넣지 않으면 버튼이 눌린 상태여도 아무런 변화가 없음.

### Style

![](https://wikidocs.net/images/page/24562/2.png)

| Style     | 설명                             |
| --------- | ------------------------------ |
| `Over`    | 버튼에 마우스 오버(호버) 시 스타일을 설정하는 속성. |
| `Down`    | 버튼의 마우스 다운(클릭) 시 스타일을 설정하는 속성. |
| `Disable` | 버튼 비활성 시 스타일을 설정하는 속성.         |

### Example

> #### 버튼을 추가하고, 클릭 시 토스트 창 출력 이벤트 생성하기

#### 1. 툴을 이용하여 추가하는 방법

**1-1. 버튼 컴포넌트를 추가하고, ID를 할당**

![](https://wikidocs.net/images/page/24562/%ED%99%94%EB%A9%B4_%EC%BA%A1%EC%B2%98_2025-01-22_163749.png)\
`Component -> Button`\
![](https://wikidocs.net/images/page/24562/2_1Kcg0W6.png)\
`Identify -> ID -> btn001 입력`

**1-2. Click 이벤트를 설정.**

![](https://wikidocs.net/images/page/24562/3.png)\
`방법 1 : 버튼을 오른쪽 클릭후 Add Event 선택하여 이벤트 추가.`\
`방법 2 : 캡처 화면과 같이 Event -> click 이벤트 리스트 우측 영역을 클릭 후 이벤트 추가.`

**1-3. 버튼이 클릭 될 시 발생할 코드를 작성.**

```js
onBtn001Click(comp, info, e)
{
    AToast.show('Hello Button!');
};
```

```
// 버튼 클릭 시 'Hello Button!' 토스트 출력
```

**1-4.빌드해서 결과물을 확인.**

#### 2. 코드를 통해 추가하는 방법

```js
   // 1. 버튼 컴포넌트 생성 
   const btn001= new AButton(); 

   // 2. 버튼 초기화 
   btn001.init({ id: 'btn001', text: 'button' }); 

   // 3. 버튼 이벤트 설정 
   btn001.addEventListener('click', function(comp, info, e) {
	   AToast.show('Hello Button!'); 
   }); 

   // 4. 버튼 추가 
   this.addComponent(btn001);;
```
