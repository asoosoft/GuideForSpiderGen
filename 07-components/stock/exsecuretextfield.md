# ExSecureTextField

<figure><img src="../../.gitbook/assets/스크린샷 2025-06-27 164147.png" alt=""><figcaption></figcaption></figure>

비밀번호, API 키, 시크릿 키 등 민감한 정보를 안전하게 입력받을 수 있도록 설계된 보안 입력 컴포넌트.



### Appearance

공통 Appearance 는 [**6. Global Properties**](<../../Guide for SpiderGen/06  SpiderGen Editor/04  Properties Pane/02 Appearence.md>) 속성을 참고

### Attribute

EXSecureTextField 속성

<figure><img src="../../.gitbook/assets/스크린샷 2025-06-30 093412.png" alt=""><figcaption></figcaption></figure>

**Data**

<table data-header-hidden><thead><tr><th width="361"></th><th></th></tr></thead><tbody><tr><td><strong>이름</strong></td><td><strong>설명</strong></td></tr><tr><td><strong>속성</strong></td><td></td></tr><tr><td><code>Text</code></td><td>매핑된 쿼리파일의 현재값의 필드명을 입력</td></tr><tr><td><code>Placeholder</code></td><td>매핑된 쿼리파일의 기본값의 필드명을 입력</td></tr><tr><td><code>Align</code></td><td>호가를 하단에 표현될 로우의 개수를 지정</td></tr><tr><td><code>Pad Title</code></td><td>호가의 단계 설정</td></tr><tr><td><code>Data Type</code></td><td>호가 상승색 설정</td></tr><tr><td><code>Return Type</code></td><td>호가 하락색 설정</td></tr><tr><td><code>MinLength</code></td><td>호가 보합색 설정</td></tr><tr><td><code>MaxLength</code></td><td>호가 잔량을 표현하는 바의 높이를 지정</td></tr></tbody></table>

### Example

**1. 프로젝트 생성**

* 프로젝트 트리뷰에서 Source > MainView.lay 파일을 클릭
* MainView의 레이아웃 파일이 오픈되면 컴포넌트 리스트에서 EXSecureTextField 컴포넌트를 선택하고 드래그하여 레이아웃에 배치
* Class 에서 ID를securetextfield 로 입력



**2. 데이터 설정**

* 먼저 MainView.js 파일을 오픈
* 상단의 파일탭에서 MainView.lay 탭을 더블 클릭하거나 우측의 프로젝트 트리에서 MainView.js 파일을 더블 클릭
* 모든 화면뷰는 onInitDone() 함수가 존재하며 이 함수는 화면이 생성될 때 딱 한번 실행
* onInitDone() 함수에서 레이블의 텍스트 내용을 아래와 같이 코드를 입력

```javascript
onInitDone()
{
	super.onInitDone()

}
```

**3. 프로젝트 실행**

* 설정한 데이터에 맞춰서 각 가격과 거래량, 평균가, 현재가가 표시

**5. 코드로&#x20;**_**EXSecureTextField**_**&#x20;생성**

* 먼저 MainView.js 파일을 오픈
* onInitDone() 함수에서 아래와 같이 코드를 입력

```javascript
onInitDone()
{
	super.onInitDone()
	

}
```

{% hint style="info" %}
<mark style="color:red;">**Build 에러 발생 시**</mark>

_**프로젝트 트리뷰에서 Framework > stock 우클릭 > Default Load Settings.. > Component > EXSecureTextField.js 체크**_

<img src="../../.gitbook/assets/스크린샷 2025-06-30 093825.png" alt="" data-size="original">
{% endhint %}



