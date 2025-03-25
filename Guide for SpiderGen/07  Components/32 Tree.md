# 32 Tree

![](https://wikidocs.net/images/page/274094/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_104143.png)\
계층 구조를 시각적으로 표현하는 데 사용되는 **트리 컴포넌트**

> 아이템을 추가하거나 삭제할 수 있으며, 특정 아이템을 선택하거나 선택 해제 가능.

> 드래그 앤 드롭 기능을 통해 아이템을 이동할 수 있으며, 아이템의 선택 스타일, 드래그 오버 스타일 등을 설정 가능.

### Example

**1. Component에서 `Tree` 를 추가하여 배치하거나, 직접 코드로 추가**

#### 컴포넌트에서 추가하여 배치하는 경우

![](https://wikidocs.net/images/page/274094/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_105432.png)

> Tree ID = `myTreeId`

#### 직접 코드로 추가하는 경우

**1. 생성 및 초기화**

```js
// 트리 컴포넌트 생성 
const myTree = new ATree(); 

// 2. 트리 컴포넌트 초기화 
myTree.init({ 
	id: 'myTreeId', 
	position: 'left:10px, top:10px', 
	size: 'width:300px, height:400px' 
});
```

**2. 데이터를 설정**

```js
const treeData = { 
	name: '메뉴', 
	sub: [ 
		{ name: '홈' }, 
		{ name: '나의정보', 
		  sub: [
			  { name: '회원수정' }, 
			  { name: '회원탈퇴' }
			  ] 
		} 
	] 
};
```

**3. 함수를 작성하고 호출**

```js
insertTreeData(tree, data) { 
	const item = tree.insertItemObj(data, true); 
	if (data.sub) { 
		data.sub.forEach(subData => { 
			subData.pItem = item; 
			this.insertTreeData(tree, subData); 
		}); 
	} 
	return item; 
} 

this.insertTreeData(this.myTreeId, treeData);

// 상황에 맞게 this. 를 삭제하거나 추가.
```

`Tree 옵션을 지정 (선택)`

```js
this.myTreeId.setOption({ 
	// ctrl 키를 누르고 선택해도 하나만 선택됩니다.
	isSingleSelect: true,  
	
	// 아이템 선택 시 선택 표시가 라인 전체로 표시되지 않습니다.
	isFullSelect: false,  
	
	// 트리 드래그 여부
	isDraggable: true,
	  
	// 드래그 아이콘
	dragIcon: './Source/img/drag.png' });
```

**4. 결과 확인**

![](https://wikidocs.net/images/page/274094/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_104143.png)
