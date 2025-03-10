![](https://wikidocs.net/images/page/24712/dropBox.png)
####
클릭하여 선택할 수 있는 아이템들을 띄우거나 검색하여 선택할 수 있는 컴포넌트
 
## Attribute
![](https://wikidocs.net/images/page/24712/db_Attribute.png) 
 
#### Data
| 이름 | 내용 |
|--|--|
| **`Placeholder`** | 플레이스홀더 텍스트를 설정하는 속성 |
| **`Align`** | 텍스트의 정렬을 설정하는 속성 |
| **`Align-left`** | 텍스트를 좌측 정렬 |
| **`Align-center`** | 텍스트를 중앙 정렬 |
| **`Align-right`** | 텍스트를 우측 정렬 |

## Example

#### 1. 컴포넌트 배치
 
| component |id |text |	placeholder |
| -------- | -------- | -------- | --------
| ATextField|txtText |	| text |
| ATextField |txtValue|	  |	value |
| AButton |	Button |등록|  |
| ADropBox |drop  |	|  | 
 
![](https://wikidocs.net/images/page/24712/dp_screen2.png) 
 
#### 2.  click 이벤트를 등록
![](https://wikidocs.net/images/page/24712/db_regi.png)

```javascript
 onButtonClick(comp, info, e)
{
	// 입력 텍스트와 데이터 값을 저장
	let iTxt =  this.txtText.getText()
	let	iData =  this.txtValue.getText();
		
	if(iTxt.trim()  ===  ''  || iData.trim()  ===  '')
	{
		alert('텍스트와 데이터 내용을 입력하세요.');
	}
	else
	{
		this.drop.addItem(iTxt, iData);  // DropBox 에 데이터 추가
		// 입력 초기화
		this.txtText.setText('');
		this.txtValue.setText('');
		alert(iTxt +  ','  + iData +  ' 데이터를 추가');
	}
};  
```
![](https://wikidocs.net/images/page/24712/dp_test3.png)
   
   ![](https://wikidocs.net/images/page/24712/db_test2.png)
   
#### 3.  select 이벤트 등록 

이벤트명은 onDropSelect라고 사용

처리 내용은 드롭박스의 아이템이 선택되면 선택된 내용을 확인하는 토스트 메시지를 출력  
![](https://wikidocs.net/images/page/24712/db_select.png)
 
```javascript
...

onDropSelect(comp, info, e) 
{ 
    AToast.show(comp.getSelectedItemText() + ':' + comp.getSelectedItemData());    
};
 
...
```
***AToast Component 추가***

**_프로젝트 트리뷰에서 Framework > afc 우클릭 > Default Load Settings... > Component > AToast.js 체크_**
![](https://wikidocs.net/images/page/24712/dp_test_suc.png)
 

## 검색기능

**`DropBox`** DropBox에 특정 키워드 입력 시, 그에 맞는 항목만 목록에서 필터링해서 긴 목록에서 원하는 항목 빠르게 찾기 가능

**검색 기능을 쓰기 위한 코드 추가**
```javascript

init(context, evtListener)
{
	super.init(context, evtListener)
	//TODO:edit here
	this.drop.setReadOnly(false);
}
 
```
 
**프로젝트 실행 후 데이터 입력 및 등록.**

| text | value |
|--|--|
| 우리나라 | 1 |
| 대한민국 | 2 |
| 만세!! | 3 |
| 독도는 | 4 |
| 우리땅 | 5 |




 * 검색전
 
![](https://wikidocs.net/images/page/24712/db_search_before.png)

 * 검색후

![](https://wikidocs.net/images/page/24712/db_search_after.png)


## 코드로 DropBox 생성하는 법

**_ADropBox Component 추가_**

**_프로젝트 트리뷰에서 Framework > afc 우클릭 > Default Load Settings... > Component > ADropBox.js 체크_**

**MainView.js 를 열어서 수정**

```javascript
...

onInitDone()
{
	super.onInitDone()

	this.drop2 =  new ADropBox();
	this.drop2.init();
	this.addComponent(this.drop2);
	this.drop2.setPos(100,100);
	this.drop2.setReadOnly(false);
}

...
```
![](https://wikidocs.net/images/page/24712/dp_new.png)