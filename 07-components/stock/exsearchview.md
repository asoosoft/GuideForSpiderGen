---
description: 검색 뷰 컴포넌트
---

# EXSearchView

<figure><img src="../../.gitbook/assets/image (95).png" alt=""><figcaption><p>&#x3C;EXSearchView 컴포넌트></p></figcaption></figure>

이 컴포넌트는 사용자가 입력한 검색어를 기반으로 데이터를 검색하고 결과를 반환하는 기능을 제공



<figure><img src="../../.gitbook/assets/image (96).png" alt=""><figcaption><p>&#x3C;EXSearchView의 기본 트리 구조></p></figcaption></figure>

{% hint style="warning" %}
**EXSearchView의 레이아웃은 사용자들이 많이 사용하는 구성으로 짜여있으며 이는 삭제하고 사용해도 무방**
{% endhint %}

### Appearance

공통 Appearance 는 [**6. Global Properties**](<../../Guide for SpiderGen/06  SpiderGen Editor/04  Properties Pane/02 Appearence.md>) 속성을 참고

### Attribute

EXSearchView 속성

<figure><img src="../../.gitbook/assets/image (97).png" alt=""><figcaption></figcaption></figure>

**Info**

| 이름           | 속성                                                                                                                       |
| ------------ | ------------------------------------------------------------------------------------------------------------------------ |
| `Search Key` | 검색할 키 목록을 저장하는 배열                                                                 ( 아무것도 작성하지 않을 시 **기본 값:** **`name`**) |

### Example

**1. 프로젝트 생성**

* 프로젝트 트리뷰에서 Source > MainView.lay 파일을 클릭
* MainView의 레이아웃 파일이 오픈되면 컴포넌트 리스트에서 EXSearchView 컴포넌트를 선택하고 드래그하여 레이아웃에 배치
* Class 에서 ID를 searchView로 입력
* 배치한 EXSearchView에 속한 컴포넌트를 그대로 사용하는 예제 진행



**2. 데이터 설정**

* 먼저 MainView.js 파일을 오픈
* 상단의 파일탭에서 MainView.lay 탭을 더블 클릭하거나 우측의 프로젝트 트리에서 MainView.js 파일을 더블 클릭
* 예시와 같이 임시 데이터 설정

```javascript

init(context, evtListener)
{
    super.init(context, evtListener)  

    this.dataArr = 
    [
      [ "005930", "삼성전자", "001" ], 
      [ "003550", "LG", "002" ], 
      [ "005380", "현대자동차", "003" ],
    ];
  
    // setData(data) -> EXSearchView에 데이터 설정
    this.searchView.setData(this.dataArr);           
}
```

<div align="center"><figure><img src="../../.gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure></div>

* 배치한 EXSearchView 의 레이아웃을 위 사진과 같이 일부 변형해서 사용
* 검색 버튼인 searchBtn에 클릭 이벤트 설정

<pre class="language-javascript"><code class="lang-javascript">
onSearchBtnClick(comp, info, e)
{
    // 검색 버튼 클릭 할 때 마다 이전 검색 데이터 삭제
    this.grid.removeAll();
    
<strong>    const searchText = this.searchText.getText();
</strong>
    // EXSearchView의 searchData()로 설정한 데이터 내에서 검색
    const result = this.searchView.searchData(searchText);

    // 결과 출력
    this.grid.setData(result)
}
</code></pre>

**3. 프로젝트 실행**

* 텍스트 필드에 검색할 텍스트 입력 후 검색 버튼 클릭

{% hint style="warning" %}
해당 예제에선 EXSearchView의 Attribute 내 Search Key를 지정하지 않았으므로 name의 value값으로만 검색

<mark style="color:red;">**다른 value값으로도 검색을 진행하고 싶다면 해당 value에 맞는 key값을 Search Key에 입력**</mark>
{% endhint %}

<div><figure><img src="../../.gitbook/assets/image (99).png" alt=""><figcaption><p>&#x3C;검색 결과></p></figcaption></figure> <figure><img src="../../.gitbook/assets/image (100).png" alt=""><figcaption><p>&#x3C;초성 검색 결과></p></figcaption></figure></div>

{% hint style="info" %}
AGrid에서 검색 결과를 위 사진과 같이 2개로 표시하고 싶다면?

AGrid 우클릭 -> Data Properties -> Column의 수를 2로 변경
{% endhint %}

{% hint style="danger" %}
Search is not defined 오류 발생 시

&#x20;<img src="../../.gitbook/assets/image (101).png" alt="" data-size="original">  &#x20;



프로젝트의 Framework -> stock 우클릭 -> Default Load Settings... -> library에 있는 Search.js를 로드

<img src="../../.gitbook/assets/image (102).png" alt="" data-size="original">
{% endhint %}



