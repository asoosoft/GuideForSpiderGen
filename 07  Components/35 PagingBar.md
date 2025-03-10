![](https://wikidocs.net/images/page/274096/pagingbar.png) 

**페이징 바(APagingBar)** 는 데이터를 페이지 단위로 나누어 표시할 때 사용되는 컴포넌트입니다. <br />

페이징 바 컴포넌트를 통해 사용자는 여러 페이지에 걸쳐 있는 데이터를 쉽게 탐색할 수 있습니다. <br />

페이징바 컴포넌트는 다양한 메서드를 제공하여 페이지 설정 및 탐색 기능을 지원합니다.

   
## Event

- **pagingBindData(comp, info)**<br />
	페이지 버튼을 클릭할 때 호출되는 함수입니다.<br />
	이 함수는 **setDelegator**를 통해 위임된 객체에서 정의되어야 합니다. <br />
	페이지 변경 시 필요한 추가 작업을 이 함수에서 처리할 수 있습니다.


## Example

페이징바 컴포넌트를 사용하면 대량의 데이터를 효율적으로 관리하고 사용자에게 직관적인 탐색 경험을 제공할 수 있습니다.

 PagingBar 컴포넌트와 ListView 컴포넌트를 활용한 예제입니다.<br>
> ListView 컴포넌트 설명을 보고오시면 이해가 빠릅니다.<br>
> [ListView 컴포넌트 설명 링크](https://wikidocs.net/24833)<br>

#### 1️⃣ 컴포넌트 배치

**MainView에 PagingBar와 ListView를 배치합니다.**
![](https://wikidocs.net/images/page/274096/pagingbar_ex.png)

> ⚠️ 빌드 시 PagingBar 컴포넌트가 깨져보인다면
> 
> ![](https://wikidocs.net/images/page/274096/afc.png)
> <br>
> 
> Framework 폴더 내 afc에서 우클릭 후 사진과 같은 항목을 클릭
> 
> ![](https://wikidocs.net/images/page/274096/compex.png)
> <br>
> compEx.css 항목을 클릭해서 로딩설정을 저장합니다.

#### 2️⃣ 코드 작성

**아래와 같은 코드를 작성합니다.**

```javascript

init(context, evtListener) 
{
	 super.init(context, evtListener); 

	 // 페이징 바의 delegator를 설정합니다. 
	 this.pagingbar.setDelegator(this);
	 
	 // 페이징 바를 중앙에 배치
	 this.pagingbar.setIsCenter(true);
	 this.page =  1;  //현재 페이지번호.
	 
	 this.send_pageList();
 } 

send_pageList() 
{ 
	// 전체 레코드 수, 현재 페이지 번호, 페이지당 레코드 수, 블럭당 페이지 수 설정 
	this.pagingbar.setPage(250, this.page, 10, 10); 
	
	// 현재 페이지에 맞는 데이터를 가져오는 코드
	// 예: 서버에 요청하여 데이터를 가져오는 로직을 추가
	this.listdata = [] ;
	for(let i=1; i <= per; i++)
	{
	 	let j = ((this.page - 1) * 10 )+ i;
	 	let temp = null;
	 	temp = {
			'number' : j ,
			'title' :j + "번 글 제목입니다."
		}
		this.listdata.push(temp);
	}
	this.pagingbar.addParam(this.listdata);
	
    this.listView.addItem('Source/subview1.lay',this.listdata);
	
	// 페이징 컴포넌트를 렌더링
	this.pagingbar.setPageView();  
} 

// 페이지 버튼을 클릭할 때마다 호출되는 이벤트 함수 
pagingBindData(comp, info) 
{ 

	// 클릭된 페이지가 현재 페이지와 같으면 리턴 
	const page = info.pageIdx; 
	if (page == this.page) return; 
	
	// 페이지 번호 업데이트 
	this.page = page; 
	
	// 새로운 페이지에 맞는 데이터를 가져오는 함수 호출 
	this.send_pageList(); 
}

```

#### 3️⃣ subview1.lay 생성

**ListView 에 추가할 아이템 (레이아웃) 인 subview1.lay를 생성**

#### 4️⃣ 컴포넌트 배치

**subview1에 아래와 같이 label (id: number), label (id: title)을 배치합니다.**

![](https://wikidocs.net/images/page/274096/pagingbar_sublay.png)

#### 5️⃣ 데이터 받기

**MainView에서 subview를 추가할 때 넘겨준 데이터를 받아와 각 label에 넣어줍니다.**
```javascript

setData(data)
{
	this.data = data;
	this.number.setText(data.number);
	this.title.setText(data.title);
}

```

#### 6️⃣ 결과확인

![](https://wikidocs.net/images/page/274096/pagingbar_res.png)
<br>
 페이징 바를 클릭해 결과를 확인해봅니다.