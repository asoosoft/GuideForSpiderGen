# ExSecureTextField

비밀번호, API 키, 시크릿 키 등 민감한 정보를 안전하게 입력받을 수 있도록 설계된 보안 입력 컴포넌트.



### Appearance

공통 Appearance 는 [**6. Global Properties**](<../../Guide for SpiderGen/06  SpiderGen Editor/04  Properties Pane/02 Appearence.md>) 속성을 참고

### Attribute

EXSecureTextField 속성

<figure><img src="../../.gitbook/assets/스크린샷 2025-06-30 093412.png" alt=""><figcaption></figcaption></figure>

**Data**

<table data-header-hidden><thead><tr><th width="361"></th><th></th></tr></thead><tbody><tr><td><strong>이름</strong></td><td><strong>설명</strong></td></tr><tr><td><strong>속성</strong></td><td></td></tr><tr><td><code>Text</code></td><td>초기값</td></tr><tr><td><code>Placeholder</code></td><td>입력 전 양식</td></tr><tr><td><code>Align</code></td><td>텍스트 정렬(left, center, right)</td></tr><tr><td><code>Pad Title</code></td><td>키패드가 열릴 때 상단 제목</td></tr><tr><td><code>Data Type</code></td><td>키패드 입력 방식</td></tr><tr><td><code>Return Type</code></td><td>결과 반환 방식</td></tr><tr><td><code>MinLength</code></td><td>최소 입력 길이</td></tr><tr><td><code>MaxLength</code></td><td>최대 입력 길이</td></tr></tbody></table>

### Example

**1. 프로젝트 생성**

* 프로젝트 트리뷰에서 Source > MainView.lay 파일을 클릭
* MainView의 레이아웃 파일이 오픈되면 컴포넌트 리스트에서 EXSecureTextField 컴포넌트를 선택하고 드래그하여 레이아웃에 배치
* Class 에서 ID를&#x20;
* secureField로 입력



**2. 데이터 설정**

* 먼저 MainView.js 파일을 오픈
* 상단의 파일탭에서 MainView.lay 탭을 더블 클릭하거나 우측의 프로젝트 트리에서 MainView.js 파일을 더블 클릭
* 모든 화면뷰는 onInitDone() 함수가 존재하며 이 함수는 화면이 생성될 때 딱 한번 실행
* onInitDone() 함수에서 레이블의 텍스트 내용을 아래와 같이 코드를 입력

```javascript
onInitDone() {
    super.onInitDone();

    // ✅ Placeholder 설정
    this.secureField.setPlaceholder('비밀번호 입력하세요');

    // ✅ Pad 설정
    this.secureField.padOption = {
        title: '비밀번호 입력',
        padType: 'char',
        returnType: '1',   // Hash 반환
        minLength: 4,
        maxLength: 20
    };

    // ✅ 값 초기화
    this.secureField.setText('');

    // ✅ jQuery 방식으로 이벤트 연결
    this.secureField.$ele.on('change', () => {
        console.log('암호화:', this.secureField.getCipherData());
        console.log('입력된 길이:', this.secureField.getPwLength());
    });

    // ✅ 위치
    this.secureField.setPos(100, 100);
}
```

**3. 프로젝트 실행**

* 설정한 데이터에 맞춰서 컴포넌트와 입력 텍스트가 표시

<figure><img src="../../.gitbook/assets/스크린샷 2025-06-30 111554.png" alt=""><figcaption></figcaption></figure>

**4. 코드로&#x20;**_**EXSecureTextField**_**&#x20;생성**

* 먼저 MainView.js 파일을 오픈
* onInitDone() 함수에서 아래와 같이 코드를 입력
*

    ```javascript
    onInitDone() {
        super.onInitDone();

        const container = new AView();
        container.createElement();
        this.addComponent(container);
        container.init();

        const secureField = new EXSecureTextField();
        secureField.createElement();
        container.addComponent(secureField);
        secureField.init();

        // ✅ placeholder 설정
        secureField.$ele.attr('placeholder', '비밀번호 입력');

        // ✅ pad 옵션 설정
        secureField.padOption = {
            title: '비밀번호 입력',
            padType: 'char',
            returnType: '1',
            minLength: 4,
            maxLength: 20
        };

        // ✅ 텍스트 초기화
        secureField.setText('');

        // ✅ 위치 설정
        secureField.setPos(100, 100);

        // ✅ 입력 이벤트
        secureField.$ele.on('change', () => {
            console.log('입력값:', secureField.getText());
            console.log('암호화 데이터:', secureField.getCipherData());
            console.log('입력 길이:', secureField.getPwLength());
        });

        // ✅ 전역 변수로 저장 (필요 시)
        this.secureField = secureField;
    }

    ```

<figure><img src="../../.gitbook/assets/스크린샷 2025-06-30 134027.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
<mark style="color:red;">**Build 에러 발생 시**</mark>

_**프로젝트 트리뷰에서 Framework > stock 우클릭 > Default Load Settings.. > Component > EXSecureTextField.js 체크**_

<img src="../../.gitbook/assets/스크린샷 2025-06-30 093825.png" alt="" data-size="original">
{% endhint %}



