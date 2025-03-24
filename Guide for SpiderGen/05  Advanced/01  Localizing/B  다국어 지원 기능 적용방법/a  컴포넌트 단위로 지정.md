### 1. 언어별 컨텍스트 메뉴 중 Open As Text 를 눌러 소스코드를 오픈합니다.
   
![](https://wikidocs.net/images/page/42753/local_create.png)

### 2. 리소스 파일에 key : value 형식으로 json파일을 작성합니다. 

- 언어 별로 작성해야합니다.

![](https://wikidocs.net/images/page/42753/local_setting.png)


### 2. Label 컴포넌트를 추가합니다.

* ALabel 의 ID 값은 label 로 설정합니다.
  
![](https://wikidocs.net/images/page/42753/local_label.png)

### 3. 프로젝트명.js 수정

※ 현재 다국어 지원기능은 프로그램이 실행될 때 자동으로 현재 브라우저의 언어를 감지해서 설정하고 있습니다. 수동으로 언어를 변경하려면 다음과 같은 소스코딩을 입력하시면 됩니다. App파일에서 onReady가 된 이후에 LocalizeManager.LANGUAGE 에 언어를 지정해주면 됩니다. (en, ko, zh 등등)

```js
onReady()
{
	super.onReady();
	LocalizeManager.LANGUAGE  =  'zh';
	this.setMainContainer(new  APage('main'))
	this.mainContainer.open('Source/MainView.lay')
}
```

### 4. MainView.js 수정

```js
onInitDone()
{
	super.onInitDone()
	let value =  LocalizeManager.getLocalizedStr('sun');
	this.label.setText(value);
}
```