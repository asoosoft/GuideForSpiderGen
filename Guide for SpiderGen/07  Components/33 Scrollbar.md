![](https://wikidocs.net/images/page/274095/scrollBar.png)
####

콘텐츠의 스크롤 가능 영역을 제공하여 사용자가 화면 내에서 콘텐츠를 상하 또는 좌우로 이동할 수 있도록 하는 컴포넌트

## Example

**_Framework > afc > AScrollBar.js 추가_**

### 컴포넌트 생성

#### 1. listVIew & ScrollBar 컴포넌트 배치
* listView ID는 listview, ScrollBar ID는 scrollbar 

![](https://wikidocs.net/images/page/274095/scorll_first.png)

#### 2. item.lay 생성
* ALabel 컴포넌트 추가 & ID는 txtLbl로 설정
![](https://wikidocs.net/images/page/274095/scorll_list.png)

#### 3. item.js 아래 코드 입력

```javascript
...

setData(data)
{
	this.txtLbl.setText(data.title)
}

...
```

#### 4. MainView.js 아래 코드 입력

```javascript
...

init(context, evtListener)
{
	super.init(context, evtListener)
	//TODO:edit here
	this.listData =  [];
	for(let i=0; i<50; i++){
		this.listData.push({
		title:  `example${i}`
		})
	}
}

onInitDone()
{
	super.onInitDone()
	//TODO:edit here
	let listViewElement =  this.listview.getElement();
	let listViewHeight =  this.listview.getHeight();
	this.scrollbar.setScrollArea(listViewHeight ,10,100,true);
	this.scrollbar.setWidth(200);
	this.scrollbar.setHeight(400);

	this.scrollbar.setDataCount(this.listData.length);
	this.scrollbar.addWheelArea(listViewElement);
	this.scrollbar.offsetBarPos(0);

	this.listview.addItem('Source/item.lay',  this.listData);
}

...
```

![](https://wikidocs.net/images/page/274095/scroll_result.png)

### 코드로 ScrollBar 생성

#### 1. 프로젝트 생성

#### 2. & MainView.js 파일 수정

```javascript
...

constructor()
{
	super()
	// 스크롤 바 생성 & 리스트뷰 생성
	this.scrollbar =  new  AScrollBar();
	this.listview =  new  AListView();
}

init(context, evtListener)
{
	super.init(context, evtListener)

	this.listData =  [];
		for(let i=0; i<50; i++){
		this.listData.push({
		title:  `example${i}`
		})
	}
}

onInitDone()
{
	super.onInitDone()
	this.listview.init();
	// listview를 컴포넌트에 추가
	this.addComponent(this.listview);
	this.element.appendChild(this.listview.getElement());

	this.scrollbar.init();
	this.listview.getElement().appendChild(this.scrollbar.getElement());
	
	let listViewElement =  this.listview.getElement();
	let listViewHeight =  this.listview.getHeight();
	
	// 스크롤바가 표현해야 할 스크롤 영역 설정. 스크롤 영역 높이, 패딩, 갭 등을 지정
	this.scrollbar.setScrollArea(listViewHeight,10,150,true);

	// 스크롤 영역에 표현되는 데이터의 개수를 설정
	this.scrollbar.setDataCount(this.listData.length);
	
	// 휠 이벤트를 등록할 영역을 설정하여 휠 이벤트 발생 시 스크롤바 이동
	this.scrollbar.addWheelArea(listViewElement)
	
	// 스크롤바의 스크롤 영역을 이동시킨다.
	// Y 좌표 이동
	this.scrollbar.offsetBarPos(0);

	this.listview.addItem('Source/item.lay',  this.listData);
}

...
```

![](https://wikidocs.net/images/page/274095/scroll_view2.png)