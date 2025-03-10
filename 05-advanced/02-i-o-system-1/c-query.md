## 쿼리파일 추가 방법

프로젝트 뷰의 Query 폴더에 쿼리파일을 추가 합니다. 마우스 우측 버튼을 클릭해서 컨텍스트 메뉴를 오픈 합니다. 

![](https://wikidocs.net/images/page/24912/%EC%BF%BC%EB%A6%AC%ED%8C%8C%EC%9D%BC%EC%B6%94%EA%B0%80.png)

* ( **기존 쿼리파일 추가** ) Add existing files... 를 클릭 한 후 이미 존재하는 쿼리파일을 추가합니다.
* ( **쿼리파일 새로 생성** ) Query Maker 를 클릭하여 아래 단계를 통해 신규 쿼리파일을 생성합니다.

## Query Maker 를 이용하여 신규 쿼리파일생성

![](https://wikidocs.net/images/page/24912/queryMaker%EC%84%A4%EB%AA%85.png)

\+ 버튼을 눌러서 New Query 생성을 시작합니다.

이 때 Name 은 사용할 쿼리파일의 파일명이고 comment 는 SpiderGen Project Menu 에서 보여질 설명 코멘트 입니다. (생략가능)

![](https://wikidocs.net/images/page/24912/%EC%BF%BC%EB%A6%AC%ED%8C%8C%EC%9D%BC%EC%83%9D%EC%84%B1.png)

그 후 생성 되었다면 신규쿼리파일의 설명과 타입, 각 InBlock 과 OutBlock 에 사용할 쿼리 정보를 입력합니다.

* **`desc:`** 생성한 쿼리에 대한 설명
* **`queryType:`** 생성한 쿼리의 타입(ex. json, etc...)
* **`InBlock1:`** 데이터 통신을 할 때 Input 역할을 합니다.
* **`OutBlock1:`** 입력한 Input 에 대한 서버 결과값(Output) 역할을 합니다.

저장하게 된다면 Project Query 폴더에 위에서 만든 쿼리파일이 추가된 것을 확인 할 수 있습니다.

파일을 열면 json 형식의 쿼리정보를 담은 쿼리파일을 확인할 수 있습니다.

<예시>
![](https://wikidocs.net/images/page/24912/%EC%BF%BC%EB%A6%AC%EC%83%9D%EC%84%B1%ED%9B%84%EB%A9%94%EB%89%B4.png)

**이 때 새로운 InBlock 이나 OutBlock 을 추가하기 위해서는 .qry 파일을 열어서 직접 타이핑하여 추가하는 방법과 QueryMaker 에서 키보드 Tab 버튼을 클릭하여 추가하는 방법이 있습니다.**

### 1. .qry 파일 직접 타이핑하여 수정하기

![](https://wikidocs.net/images/page/24912/%EC%BF%BC%EB%A6%AC%EC%BD%94%EB%93%9C%EC%88%98%EC%A0%95.png)

### 2. Query Maker 에서 새로운 InBlock/OutBlock 추가

예시로 InBlock1 아래에 InBlock2 를 생성하려면 오른쪽 버튼을 클릭하여 Add InBlock 을 클릭합니다.

![](https://wikidocs.net/images/page/24912/AddInBlock.png)

그 후 필드값을 추가하기 위해서는 InBlock2 에 마우스 포커싱을 한뒤 키보드 Tab 버튼을 클릭하여 추가합니다.

![](https://wikidocs.net/images/page/24912/%EB%A1%9C%EC%9A%B0%EC%B6%94%EA%B0%80.png)

그 후 위 단계를 따라서 들어갈 내용을 차례대로 입력하면 됩니다.

### 3. 생성한 Query 호출

사용할 화면 .js 에서 아래처럼 함수를 만들면 Query 를 호출하고 데이터를 송신 받을 수 있습니다.

```javascript
sendData() {
	// 첫 번째 파라미터: 호출할 쿼리명
	// 두 번째 파라미터: 데이터를 수신할 화면번호(일반적으로 containerId 로 지정함)
	// 세 번째 파라미터: 그룹명을 지정한 컴포넌트만 데이터를 수신하고 싶은 경우 세팅(null 입력시 모든 컴포넌트 수신)
	// 네 번째 파라미터: InBlock 데이터 요청하는 함수
	// 다섯 번째 파라미터: OutBlock 데이터 송신받는 함수
    theApp.queryManager.sendProcessByName('testQuery01', this.getContainerId(), null,
	    // InBlock 을 전송하는 함수
	    function(queryData) { 
		    // 전송할 queryData 에 InBlock1 데이터
	        let InBlock1 = queryData.getBlockData('InBlock1'); 
			
			// InBlock1 에 맞는 데이터 주입	        
	        InBlock1[0].userId= 'testId';
		    InBlock1[0].userPwd= 'testPwd';
	    },
	    
	    // 서버에서 결과값이 내려오면 OutBlock 을 송신받는 함수(콜백함수개념)
	    function(queryData) { 
		    // queryData 가 없는 경우 예외처리 방어코드
	        if(!queryData) return; 
	        
	        // 결과값으로 내려온 queryData 에 OutBlock1 데이터
	        let OutBlock1 = queryData.getBlockData('OutBlock1');
	    }); 
		
		// 송신 받은 queryData console 에 출력하는 함수
		queryData.printQueryData();
};  
```

## 컴포넌트에 Query 매핑하기

.lay 에서 Query 를 매핑할 컴포넌트를 오른쪽 클릭합니다.

![](https://wikidocs.net/images/page/24912/%EC%BF%BC%EB%A6%AC%EB%A7%A4%ED%95%91.png)
 
 All Query 에서 매핑할 쿼리를 선택하고, 컴포넌트에 매핑할 OutBlock 데이터를 더블클릭하여 등록한 후 적용을 눌러 저장합니다.
 ![](https://wikidocs.net/images/page/24912/%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%A7%A4%ED%95%91.png)

그 후 위에 작성한 함수를 호출한다면 testQuery01 의 result(결과값) 이 ALabel 에 매핑되어 데이터가 출력되는 것을 확인할 수 있습니다.

###  매핑관련 참고사항 
* 각 컴포넌트마다 매핑 가능한 개수는 정해져 있습니다. 
* View, Layout 컴포넌트는 자식 컴포넌트의 개수 만큼 매핑이 가능합니다. 
* 또한, 매핑 할 항목이 연속되어 있는 경우 컴포넌트도 연속되게 생성하고 다중 추가하면 편리합니다.   
 
 
 