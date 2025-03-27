# Listview

![](../../.gitbook/assets/listView.png)



여러 개의 아이템을 리스트 형태로 표시하고 관리할 수 있는 컴포넌트

### Apperance

**Style**

* **`select item`**
  * ListView 에서 기본적으로 선택될 아이템을 설정하는 기능
  * 이 옵션을 사용하면 리스트뷰가 초기화 될 때 특정 아이템이 선택된 상태로 사용 가능

### Attribute

![](../../.gitbook/assets/listview_attribute.png)

**Item**

| 이름           | 내용                      |
| ------------ | ----------------------- |
| **`Height`** | 리스트뷰의 각 아이템 높이를 지정하는 속성 |
| **`Gap`**    | 리스트뷰의 각 아이템 사이의 간격을 설정  |

**Contents**

| 이름                | 내용                                         |
| ----------------- | ------------------------------------------ |
| **`Default Url`** | 리스트뷰에 아이템을 추가할 때 기본적으로 사용할 레이아웃 파일의 경로를 설정 |
| **`add`**         | 새로운 아이템을 리스트뷰에 추가                          |
| **`edit`**        | 기존에 추가된 아이템의 경로를 수정                        |
| **`del`**         | 리스트뷰에서 특정 아이템을 삭제                          |
| **`up`**          | 선택한 아이템을 한 단계 위로 이동                        |
| **`down`**        | 선택한 아이템을 한 단계 아래로 이동                       |

**Option**

* **`Direction`**
  * **`vertical`** : 리스트뷰가 상하 방향으로 스크롤
  * **`horizontal`** : 리스트뷰가 좌우 방향으로 스크롤
* **`Selectable`**
  * 리스트뷰의 아이템이 선택 가능한지 여부 확인
  * 활성화 시 리스트뷰의 아이템을 선택 가능
* **`Wrap`**
  * 리스트뷰의 아이템이 가로로 배치될 때, 공간이 부족하면 개행하여 다시 추가할지 여부를 설정
  * 활성화 시 아이템이 화면에 맞게 자동으로 줄바꿈되어 표시

### Example

**1. lay 파일 오픈 및 컴포넌트 배치**

| component | id       | text   |
| --------- | -------- | ------ |
| ALabel    | lbl001   | 선택내용   |
| AListView | listView |        |
| AButton   | btnAdd   | Add    |
| AButton   | btnDel   | Delete |

![](../../.gitbook/assets/listview_view.png)

**2. 리스트뷰에 추가할 데이터 작성**

* MainView.js 파일을 오픈 후 다음과 같이 데이터를 설정

```javascript
...

init(context, evtListener)
{
	super.init(context, evtListener)

	this.listData =  [
		{
			title :  'List Content Title 1'
		},
		{
			title :  'List Content Title 2'
		},
		{
			title :  'List Content Title 3'
		},
		{
			title :  'List Content Title 4'
		},
		{
			title :  'List Content Title 5'
		}
	]
}

...
 
```

**3. 리스트뷰에 데이터를 바인딩**

* MainView.js 파일 오픈 후 다음과 같이 설정

```javascript
...

onInitDone()
{
	this.listView.addItem('Source/Items/ItemView.lay',  this.listData);
}

...
```

**4. Source 폴더 안에 Items 폴더를 생성**

생성한 Items 폴더 내에 ItemView 이름의 뷰를 추가하고 아래 내용을 참고해서 컴포넌트를 배치

| component | id     | text | etc                     |
| --------- | ------ | ---- | ----------------------- |
| ItemView  |        |      | background: transparent |
| ALabel    | lbl001 |      | background: transparent |
| AButton   | btn001 |      | Delete                  |

![](../../.gitbook/assets/listview_ItemView.png)

**5. setData 메소드를 추가**

* 데이터가 바인딩 될 때 호출됩니다.
* ItmeView.js 파일 오픈 후 다음과 같이 설정

```javascript
...

// ItemView의 setData 메소드 호출은 MainView.js에 오버라이드된 bindData 메소드 내에서 호출
setData(data) 
{     
    this.data = data; 
 
    this.lbl001.setText(this.data.title); 
};  

... 
```

**6. 프로젝트 실행**

![](../../.gitbook/assets/listview_exam.png)

**7. Add 버튼 Click 이벤트를 추가**

```javascript
...

onBtnAddClick(comp, info, e) 
{ 
 
    //리스트 데이터는 배열로 들어가야 함. 
    //데이터의 첫번째 데이터를 배열에 넣어서 추가함. 
    this.listView.addItem('Source/Items/ItemView.lay', [this.listData[0]]); 
 
    //리스트뷰 스크롤을 맨 아래로 이동 
    this.listView.scrollToBottom(); 
 
}; 

... 
```

**8. 프로젝트 실행**

![](../../.gitbook/assets/listView_add.png)

**9. 아이템 선택 시 스타일 적용**

* 프로젝트 트리 Template 폴더에서 오른쪽 클릭 > 메뉴에서 Add new 클릭
* Style 파일을 생성 > Name 은 listView 로 설정 >listView.stl 오른쪽 클릭 후 오픈
* 오픈 된 Styler 메뉴 중에 상단 오른쪽 끝 + 버튼을 클릭\
  ![](../../.gitbook/assets/listview_tpl.png)

![](../../.gitbook/assets/listView_style.png)

* 추가된 스타일 이름을 selected\_item 이라 설정
* 스타일 css 를 아래처럼 설정

```css
.selected_item
{
	background:  linear-gradient(rgb(239,239,239),  rgb(128,128,128));

}
```

![](../../.gitbook/assets/listview_style_select.png)

* MainView.lay에 listView 클릭 > Appearance > Style > select item 속성 더블클릭 > show all 버튼 누르고 selected\_item 추가 > 적용

![](../../.gitbook/assets/listVeiw_Appear.png)

* listView > Class > select 더블 클릭 후 생성
* F5 누르고 프로젝트를 빌드하고 실행
* 실행된 화면에서 리스트의 아이템을 선택하고 스타일이 적용되는걸 확인![](../../.gitbook/assets/listView_check.png)

**10. 리스트 아이템 선택 및 삭제**

* ItemView.lay에서 아이템에 있는 Delete 버튼에 Click 이벤트를 설정 후 설정 함수 내용은 다음과 같이 수정

```javascript
...

onBnt001Click(comp, info, e) 
{ 
    //아이템의 상위객체 리스트뷰에 정의 함수 호출 
    this.owner.removeItem(this.getItem()); 
 
};   

...  
```

* 프로젝트를 빌드하고 실행한 후 리스트 아이템에 있는 Delete 버튼을 클릭 후 클릭한 아이템이 삭제 되는 것을 확인

**11. 모든 아이템 삭제 기능 추가**

* Delete 버튼에 Click 이벤트를 설정하고 설정 함수는 다음과 같이 수정

```javascript
...

onBtnDelClick(comp, info, e)  
{
	this.listView.removeAllItems();
}

... 
```
