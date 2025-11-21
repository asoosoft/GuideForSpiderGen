# PivotGrid

![](../../../.gitbook/assets/pg.png)

**피벗 그리드(APivotGrid)** 는 데이터를 피벗 테이블 형식으로 시각화하는 데 사용되는 컴포넌트<br>

> 데이터를 다양한 방식으로 요약하고 분석할 수 있도록 도와줍니다.

Grid 와 동일하나, 대량의 컬럼으로 구성할경우 좌우 스크롤시 첫 열을 고정시킬수 있는 컴포넌트

### Attribute

![](../../../.gitbook/assets/pg_Attribute.png)

**1️⃣ Option**

* **Hide Header**\
  헤더를 숨길지 여부를 설정합니다.
* **Hide Footer**\
  푸터를 숨길지 여부를 설정합니다.
* **Fullrow Select**\
  특정 셀을 클릭해도 해당 행 전체가 선택되도록 설정합니다.
* **Single Select**\
  Ctrl 키를 누르고 선택해도 하나만 선택되도록 설정합니다.
* **Clear Row Template**\
  그리드 초기화 후 템플릿 행을 보존할지 여부를 설정합니다.
* **Selectable**\
  선택 가능 여부를 설정합니다.
* **Column Resize**\
  컬럼 리사이즈 가능 여부를 설정합니다.
* **Width Changable**\
  컬럼 리사이즈 시 그리드 넓이 변경 여부를 설정합니다.

**2️⃣ Data**

* **Pivot Grid Width**\
  피벗 그리드의 가로 길이를 설정합니다.
* **Main Grid Width**\
  메인 그리드의 가로 길이를 설정합니다.

### Example

PivotGrid는 데이터를 다양한 방식으로 요약하고 분석할 수 있는 강력한 도구로, 대량의 데이터를 효율적으로 시각화하고자 할 때 유용하게 사용됩니다.\
이를 통해 사용자는 데이터를 쉽게 탐색하고 인사이트를 얻을 수 있습니다.

1️⃣ 레이아웃에서 PivotGrid 컴포넌트를 생성한 경우<br>

```javascript

onInitDone()
{
	// Pivot Grid 에 데이터 넣기

	// 데이터 배열을 설정 
	const dataArr = [ 
		{ category: 'A', value: 10 }, 
		{ category: 'B', value: 20 }, 
		{ category: 'C', value: 30 } 
	];

	// PivotGrid에 데이터 설정 
	this.pivotGrid.setData(dataArr);
}

```

\
<br>

2️⃣ 코드에서 PivotGrid 컴포넌트를 생성한 경우<br>

```javascript

onInitDone()
{
	// 사용자 함수 불러오기
	this.createPivotGrid()
}

createPivotGrid()
{
	// PivotGrid 생성
	const pivotGrid = new APivotGrid();

	// 피벗그리드 속성 설정
	pivotGrid.setOption({ 
		hideHeader: false, 
		hideFooter: false, 
		fullrowSelect: true, 
		singleSelect: false, 
		selectable: true, 
		columnResize: true, 
		widthChangable: true 
	}); 
	
	// 피벗 그리드의 크기 설정 
	pivotGrid.setSize('100%', '400px');

	// 데이터 설정 
	const dataArr = [ 
		{ category: 'A', value: 10 }, 
		{ category: 'B', value: 20 }, 
		{ category: 'C', value: 30 } 
	]; 
	
	// PivotGrid에 데이터 설정 
	pivotGrid.setData(dataArr);

	// 피벗그리드를 특정 컨테이너에 추가
	// jQuery 객체를 사용하여 추가 
	this.view.$ele.append(pivotGrid.$ele); 
}

```

### Event Example

피벗그리드의 이벤트들 중 몇가지를 예시로 안내해드리겠습니다.<br>

이벤트는 피벗그리드를 선택한 후 Class Pane > Event에서 확인할 수 있습니다.

1️⃣ **click 이벤트**

> 그리드에서 아이템을 선택할 때 호출됩니다.

```javascript

onPivotGridSelect(comp, info, e)
{
	alert('Selected Item: ' + info.selectedItem);
}

```

2️⃣ **scrollTop 이벤트**

> 그리드의 스크롤이 가장 위에 도달하면 호출됩니다.

```javascript

onPivotGridScrollTop(comp, info, e)
{
	console.log('Scrolled to top');
}

```

3️⃣ **scrollBottom 이벤트**

> 그리드의 스크롤이 가장 아래에 도달하면 호출됩니다.

```javascript

onPivotGridScrollBottom(comp, info, e)
{
	console.log('Scrolled to bottom');
}

```

4️⃣ **longTab이벤트**

> 그리드의 셀을 길게 탭할 때 호출됩니다.

```javascript

onPivotGridScrollTop(comp, info, e)
{
	alert('Long tab on cell');
}

```
