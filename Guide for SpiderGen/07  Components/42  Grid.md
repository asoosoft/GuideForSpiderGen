# 42  Grid

![](https://wikidocs.net/images/page/274109/Grid-01.png)

**그리드(Grid)** 는 컴포넌트는 데이터를 테이블 형식으로 표시하고 관리할 수 있는 도구입니다.

> 그리드(Grid)는 다양한 속성과 메서드를 제공하여 데이터를 효율적으로 표시하고 조작할 수 있습니다.

### Attributes

![](https://wikidocs.net/images/page/274109/Grid-02.png)

* **Hide Heade** 헤더 숨김 여부를 설정합니다.
* **Hide Footer** 푸터 숨김 여부를 설정합니다.
* **Fullrow Select** 특정 셀을 클릭해도 그 로우 전체가 선택되도록 설정합니다.
* **Single Select** Ctrl 키를 누르고 선택해도 하나만 선택되도록 설정합니다.
* **Flexible Row** TR의 높이를 TABLE 높이에 맞추는 옵션입니다.
* **Selectable** 선택 가능 여부를 설정합니다.
* **Clear Row Template** 그리드 초기화 후 템플릿 로우를 보존할지 여부를 설정합니다.
* **Sortable** 헤더 선택 시 정렬 처리 여부를 설정합니다.
* **Column Resize** 컬럼 리사이즈 여부를 설정합니다.
* **Width Changable** 컬럼 리사이즈 시 그리드 넓이 변경 여부를 설정합니다.

### Methods

* **setCellData(rowInx, colInx, cellData, noUpdate)** 특정 셀의 데이터를 설정합니다.
* **setData(dataArr)** 그리드에 데이터를 설정합니다.
* **setGridData(dataArr, noUpdate)** 데이터 배열을 설정하고 렌더링 여부를 결정합니다.
* **setRowData(rowInx, rowData, metaData, noUpdate)** 특정 로우에 데이터를 설정합니다.
* **sortColumn(colInx)** 특정 컬럼을 정렬합니다.
* **updateDataGrid()** 데이터 배열의 변화값을 스크롤바에 반영하고 그리드의 각 값을 갱신합니다.

### Example

**1. id를 설정합니다.**

* 그리드(Grid)의 id를 simpleGrid로 설정합니다.

![](https://wikidocs.net/images/page/274109/Grid-06.png)

**2.코드를 추가합니다.**

* 아래 코드를 추가합니다.

```
    onInitDone() {
        super.onInitDone()

        this.simpleGrid.setData([
            ['Item 1', 'Description 1', 'Price 1'],
            ['Item 2', 'Description 2', 'Price 2'],
            ['Item 3', 'Description 3', 'Price 3']
        ]);

    }
    
    onSimpleGridSelect(comp, info, e)
	{
       let cell = info[0];
       let pos = comp.indexOfCell(cell);
       alert("Selected cell at row: " + pos[0] + ", column: " + pos[1]);
	}

```

**3.이벤트(Event)를 설정합니다.**

* select를 눌러 Function Namefme 를 onSimpleGridSelect로 설정 합니다.

![](https://wikidocs.net/images/page/274109/Grid-07.png)

**4.빌드를 실행 합니다.**

> 셀을 선택하면 이벤트가 발생합니다.

![](https://wikidocs.net/images/page/274109/Grid-03.png) ![](https://wikidocs.net/images/page/274109/Grid-05.png)

### 다음 예제는 JavaScript를 사용하여 그리드(Grid)를 추가합니다.

**1. Framework를 추가합니다.**

* Framework의 afc에서 AGrid/AGeidEvent를 추가합니다.

![](https://wikidocs.net/images/page/274109/Grid-04.png)

**2. 코드를 추가합니다.**

* 아래의 코드를 추가합니다.

```
    onInitDone() {
        super.onInitDone()

        // 그리드 생성
        const grid = new AGrid();
        grid.init();

        // 그리드 속성 설정
        grid.setSize('100%', '100%');
        grid.setPos(0, 0);

        // 그리드 옵션 설정
        grid.setOption({
            hideHeader: false,
            hideFooter: false,
            fullrowSelect: true,
            singleSelect: false,
            sortable: true
        });

        // 그리드를 MainView에 추가
        this.getContainer().addComponent(grid);

        // 그리드 데이터 설정
        let data = [
            ['Item 1', 'Description 1', 'Price 1'],
            ['Item 2', 'Description 2', 'Price 2'],
            ['Item 3', 'Description 3', 'Price 3']
        ];
        grid.setData(data);

        // 그리드 이벤트 설정
        grid.addEventListener('select', this, 'onGridSelect');

    }

  //선택 이벤트
    onGridSelect(comp, info, e) {
       let cell = info[0];
       let pos = comp.indexOfCell(cell);
       alert("Selected cell at row: " + pos[0] + ", column: " + pos[1]);
   }
```

**3. 빌드를 실행 합니다.**

* 셀을 선택하면 이벤트가 발생합니다.

![](https://wikidocs.net/images/page/274109/Grid-03.png) ![](https://wikidocs.net/images/page/274109/Grid-05.png)
