![](https://wikidocs.net/images/page/24779/selectBox.png)
 
사용자가 미리 정의된 옵션 목록에서 하나의 항목을 선택할 수 있도록 하는 UI 컴포넌트.

드롭다운 메뉴 형태로 제공되며, 사용자가 선택한 항목을 기반으로 다른 동작을 수행.
 
 
## Attribute
### Default Data4
![](https://wikidocs.net/images/page/24779/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-03_093757.png) 

셀렉트박스에 보여질 리스트 데이터를 설정. 

텍스트와 값은 (,) 콤머로 구분하고 아이템들은 개행(엔터)으로 구분. 

SelectBox를 처음 생성할 때, Default Data에 "item1,value1"과 같은 형식으로 생성. 

여기서 콤마(,)는 텍스트와 값을 구분하는 역할.

item1은 셀렉트박스에 표시될 아이템의 텍스트. 사용자가 드롭다운을 열었을 때 보게 되는 이름.

value1은 해당 아이템의 값. 이 값은 주로 프로그램 내에서 선택된 아이템을 식별하거나 처리할 때 사용. 

사용자가 item1을 선택하면, 실제로는 "value1"이라는 값이 선택된 것으로 간주.

## Example
### 1. 화면에 컴포넌트 및 이벤트 생성.
* 컴포넌트 > SelectBox 선택

![](https://wikidocs.net/images/page/24779/makeselectbox.png)

* Attribute > Data에 옵션 추가

![](https://wikidocs.net/images/page/24779/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-23_152739.png)

* SelectBox 선택 > Event > Change 클릭

![](https://wikidocs.net/images/page/24779/selectboxevent.png)

* 코드 생성

```
onSelectBoxChange(comp, info, e){
	// 선택된 아이템의 텍스트와 값을 가져옴
	const selectedText = comp.getSelectedItemText();
	const selectedValue = comp.getSelectedItemValue();
	// 선택된 아이템 정보를 콘솔에 출력
	alert('선택된 아이템:', selectedText, selectedValue);
}
```

### 2. 코드로 컴포넌트 생성. 
* Project > Framework > afc > Default Load Settings 

![](https://wikidocs.net/images/page/24779/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-23_155755.png)


* ASelectBox.js 선택 > 창닫기 > 변경된 정보를 저장하시겠습니까? > Yes

![](https://wikidocs.net/images/page/24779/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-18_162355.png)


* 코드 생성

```
	init(context, evtListener) {

		super.init(context, evtListener);

		// SelectBox 인스턴스 생성
		this.selectBox = new  ASelectBox();

		this.selectBox.init(); // 초기화

		// SelectBox 속성 설정
		this.selectBox.setWidth(200);
		this.selectBox.setHeight(30);

		// 부모 뷰에 SelectBox 추가
		this.addComponent(this.selectBox);

		// SelectBox에 아이템 추가
		this.selectBox.addItem('사과', 'apple');
		this.selectBox.addItem('포도', 'grape');
		this.selectBox.addItem('오렌지', 'orange');

		// SelectBox 가운데 정렬
		this.selectBox.centerX();
		this.selectBox.centerY();
	}
```

* 실행 화면

![](https://wikidocs.net/images/page/24779/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-18_162155.png)