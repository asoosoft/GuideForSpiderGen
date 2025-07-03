# EXSecureTextField

<figure><img src="../../.gitbook/assets/스크린샷 2025-07-01 101344.png" alt=""><figcaption></figcaption></figure>

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
    this.secureField.setPlaceholder('비밀번호 입력');

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

<figure><img src="../../.gitbook/assets/image (103).png" alt=""><figcaption></figcaption></figure>

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

5. **SecurePadManager 예제 코드**

```javascript
onInitDone() {
    super.onInitDone();

    this.onSecurePadChange = function (isOpen) {
        AToast.show(`SecurePad 상태: ${isOpen ? '열림' : '닫힘'}`, 2000);
    };

    const container = new AView();
    container.createElement();
    this.addComponent(container);
    container.init();

    const secureField = new EXSecureTextField();
    secureField.createElement();
    container.addComponent(secureField);
    secureField.init();

    if (afc.isIos) {
        secureField.setDataType('text');
    }
    secureField.setText('');
    secureField.setCipherData('');
    secureField.setPwLength(0);

    secureField.$ele.attr('placeholder', '비밀번호 입력');
    secureField.setPos(100, 100);

    const padOption = {
        title: '비밀번호 입력',
        padType: 'char',
        returnType: '1',
        minLength: 4,
        maxLength: 20
    };

    secureField.padOption = padOption;

    const btn = new AButton();
    btn.createElement();
    container.addComponent(btn);
    btn.init();
    btn.setText('보안 키패드');
    btn.setPos(100, 180);

    btn.bindEvent('click', () => {
        SecurePadManager.openPad(padOption, (isSuccess, result, length) => {
            if (isSuccess && result) {
                secureField.setCipherData(result.val);
                secureField.setPwLength(result.len);

                AToast.show(`암호화된 입력값: ${result.val}\n 입력 길이: ${result.len}`, 3000);
            } else {
                AToast.show('입력 취소 또는 실패', 2000);
            }
        }, secureField);
    });

    secureField.$ele.on('change', () => {
        AToast.show(
            `입력값: ${secureField.getText()}\n 암호화 데이터: ${secureField.getCipherData()}\n 입력 길이: ${secureField.getPwLength()}`,
            3000
        );
    });

    this.secureField = secureField;
}
```

5-1. **라이브러리**

* _**프로젝트 트리뷰에서 Framework > Library 우클릭 > Add new > Javascript >**_**&#x20;ML4WebVKeyPad.js + SecurePadManager.js 생성**

<figure><img src="../../.gitbook/assets/image (104).png" alt=""><figcaption></figcaption></figure>



* **ML4WebVKeyPad.js**

```javascript
// ML4WebVKeyPad (가상 키보드 설정용 Mock)
window.ML4WebVKeyPad = {
    setVirtualKeyboard: function(element) {
        console.log('[Mock] ML4WebVKeyPad.setVirtualKeyboard 호출됨:', element);
    }
};

// ML4WebVKey (키보드 동작 관련 Mock)
window.ML4WebVKey = {
    showKeyboard: function(id) {
        console.log('[Mock] 가상 키보드 표시:', id);

        // 실제 입력 시뮬레이션 (3초 뒤에 입력 완료 이벤트 강제 호출)
        setTimeout(() => {
            const input = document.getElementById(id);
            if (input) {
                input.value = 'mock1234'; // 실제 사용자가 입력한 것처럼 처리
                input.dispatchEvent(new Event('input'));  // input 이벤트 발생
                SecurePadManager.onWebKeypadClose(id);   // 강제 close
            }
        }, 3000); // 3초 뒤 입력 완료 시뮬레이션
    },

    getDecryptedPassword: function(id) {
        const input = document.getElementById(id);
        return input ? input.value : '';
    },

    enterKey: function() {
        console.log('[Mock] Enter 키 눌림');
    }
};

```



* **SecurePadManager.js**

```javascript

var SecurePadManager = {
	isEnable: (navigator.userAgent.indexOf('HanwhaODS')>-1),//afc.isNative,
	callback: null,

	//보안키패드 오픈 함수
	openPad: function(padOption, callback, secureTxf)
	{
		var rootView = secureTxf.getRootView();
		var thisObj = this;
        this.padOption = padOption;
		if(afc.isNative) { //App
			padOption.id = secureTxf.element.id;
			if(SecurePadManager.callback) return;
			
			this.coverWin = new BaseWindow();
			this.coverWin.setOption({ isFocusLostClose: true, modalBgOption: 'none' });
			this.coverWin.openAsDialog();
			this.coverWin.setResultCallback(() => {
				if(SecurePadManager.callback) {
					cordova.exec(null, null, 'SecurePadPlugin', 'close', []);
					callback(true, null, 0); //실패
					SecurePadManager.callback = null;
					if(rootView.onSecurePadChange) rootView.onSecurePadChange(false);
				}

				this.coverWin = null;
			});
			
			cordova.exec(function(obj) {
				//확인
				callback(true, obj.encData, obj.plaintxtlength);
				SecurePadManager.callback = null;
				thisObj.coverWin.close();
				if(rootView.onSecurePadChange) rootView.onSecurePadChange(false);
				
			}, function() {
				//취소
				callback(true, null, 0); //실패
				SecurePadManager.callback = null;
				thisObj.coverWin.close();
				if(rootView.onSecurePadChange) rootView.onSecurePadChange(false);
				
			}, 'SecurePadPlugin', 'open', [padOption]);
			
			if (rootView && rootView.onSecurePadChange) rootView.onSecurePadChange(true);

		
		} else { //Web
		
			//IOS 일 때 password 인 경우 이상하게 동작하므로 text로 변경함
			if(afc.isIos) secureTxf.setDataType('text');
		
			if(secureTxf.isSetVirtualKeyboard) return;
			
			//해당 컴포넌트는 뷰에 객체로 저장이 되어있으므로 id를 계속 변경한다.
			//if(!secureTxf.element.id) secureTxf.setComponentId('sxf' + Date.now());
			secureTxf.setComponentId('sxf' + Date.now());
			
			//console.error(padOption);
			secureTxf.setAttr('ds-kb-type', padOption.padType=='char'?'qwerty':'number');
			secureTxf.setAttr('ds-kb-focus', true);
			if(!secureTxf.isSetVirtualKeyboard) {
				ML4WebVKeyPad.setVirtualKeyboard(secureTxf.element);
				secureTxf.setAttr('ds-kb-callback', 'SecurePadManager.onWebKeypadClose()');
			}
			secureTxf.isSetVirtualKeyboard = true;
			ML4WebVKey.showKeyboard(secureTxf.element.id);
			if (rootView && rootView.onSecurePadChange) rootView.onSecurePadChange(true);

			
			if(!secureTxf.isInputEvent) {
				secureTxf.bindEvent('input', function() {
                    const inputVal = this.value;
                    const len = inputVal.length;

                    // 값 저장 (this.acomp는 EXSecureTextField 인스턴스)
                    this.acomp.setCipherData(inputVal);
                    this.acomp.setPwLength(len);

                    if (thisObj.padOption.maxLength == len) {
                        ML4WebVKey[secureTxf.element.id].enterKey();
                    }
                });

				secureTxf.isInputEvent = true;
			}
		}
		
		
		//키패드를 누를 때도 이벤트 받아서 컴포넌트에 세팅해야하므로 콜백을 저장한다.
		this.callback = callback;
	},
	
	closePad: function(sxf)
	{
		if(SecurePadManager.callback) {
			cordova.exec(null, null, 'SecurePadPlugin', 'close', []);
			SecurePadManager.callback(true, null, 0); //실패
			SecurePadManager.callback = null;
			var rootView = sxf.getRootView();
			if(rootView && rootView.onSecurePadChange) rootView.onSecurePadChange(false);
		}
	},
	
	onWebKeypadClose: function(id)
    {
        var sxf = document.getElementById(id).acomp;
        
        var plainText = ML4WebVKey.getDecryptedPassword(id);
        var len = plainText.length;

        // 여기에서 직접 값 설정
        sxf.setCipherData(plainText);
        sxf.setPwLength(len);

        sxf.$ele.trigger('change');

        SecurePadManager.callback(true, {
            val: CryptoJS.AES.encrypt(plainText, id).toString(),
            info: id,
            len: len
        }, len);

        console.error('onKeypadClose');
        var rootView = sxf.getRootView();
        if(rootView && rootView.onSecurePadChange) rootView.onSecurePadChange(false);
    },
	
	//키패드를 누를 때 발생하는 이벤트함수
	onKeyPadClick: function(obj)
	{
		if(SecurePadManager.callback) SecurePadManager.callback(false, null, obj.plaintxtlength);
	},
	
	//키패드를 누를 때 발생하는 이벤트함수
	checkPwd: function(key, callback)
	{
		if(!key) {
			callback(false, false);
			return;
		}
		
		if(afc.isNative) {
			cordova.exec(function(arr) {
				callback(arr[0], arr[1]);

			}, function() {
				callback(false, false);

			}, 'SecurePadPlugin', 'checkPwd', [key]);	
		} else {
			var result1 = !!(key && key[0].match(/[a-zA-z]/)),
				result2 = !!((key.length >= 8) &&
				(key.length < 16) &&
				(key.match(/[a-zA-z]/)) &&
				(key.match(/[0-9]/)) &&
				(key.match(/[\!\?\@\#\$\%\^\&\*\(\)\:\;\+\-\=\~\{\}\<\>\_\[\]\\\"\'\,\.\/\`\|]/)));
			callback(result1, result2);
		}
	}
};
```



* 실행 결과

<figure><img src="../../.gitbook/assets/화면 녹화 중 2025-07-03 162650.gif" alt=""><figcaption></figcaption></figure>



6. **SecureWebPadManager 예제 코드**

```javascript
onInitDone() {
    super.onInitDone();

    this.onSecurePadChange = function (isOpen) {
        AToast.show(`SecurePad 상태: ${isOpen ? '열림' : '닫힘'}`, 2000);
    };

    const container = new AView();
    container.createElement();
    this.addComponent(container);
    container.init();

    const secureField = new EXSecureTextField();
    secureField.createElement();
    container.addComponent(secureField);
    secureField.init();

    secureField.$ele.attr('placeholder', '비밀번호 입력');
    secureField.setPos(100, 100);

    const padOption = {
        title: '비밀번호 입력',
        padType: 'char',
        returnType: '1',
        minLength: 4,
        maxLength: 20
    };

    secureField.padOption = padOption;

    const btn = new AButton();
    btn.createElement();
    container.addComponent(btn);
    btn.init();
    btn.setText('보안 키패드');
    btn.setPos(100, 180);

    btn.bindEvent('click', () => {
        SecureWebPadManager.openWebPad(padOption, (isSuccess, result, length) => {
            if (isSuccess && result) {
                secureField.setCipherData(result.val);
                secureField.setPwLength(result.len);

                AToast.show(`암호화된 입력값: ${result.val}\n 입력 길이: ${result.len}`, 3000);
            } else {
                AToast.show('❌ 입력 취소 또는 실패', 2000);
            }
        }, secureField);
    });

    secureField.$ele.on('change', () => {
        AToast.show(
            `입력값: ${secureField.getText()}\n 암호화 데이터: ${secureField.getCipherData()}\n 입력 길이: ${secureField.getPwLength()}`,
            3000
        );
    });

    this.secureField = secureField;
}
```

6-1. **라이브러리**

* _**프로젝트 트리뷰에서 Framework > Library 우클릭 > Add new > Javascript >**_**&#x20;ML4WebVKeyPad.js + SecureWebPadManager.js 생성**

<figure><img src="../../.gitbook/assets/image (105).png" alt=""><figcaption></figcaption></figure>

* **SecureWebPadManager.js**

```javascript
var SecureWebPadManager = {
    callback: null,
    padOption: null,

    // 웹 보안 키패드 열기
    openWebPad: function(padOption, callback, secureTxf) {
        const rootView = secureTxf.getRootView();
        this.padOption = padOption;

        // iOS 대응 (password 이상 동작 시 text로 변경)
        if (afc.isIos) secureTxf.setDataType('text');

        // id 세팅
        const id = 'sxf' + Date.now();
        secureTxf.setComponentId(id);

        // 키패드 속성 부여
        secureTxf.setAttr('ds-kb-type', padOption.padType === 'char' ? 'qwerty' : 'number');
        secureTxf.setAttr('ds-kb-focus', true);
        secureTxf.setAttr('ds-kb-callback', 'SecureWebPadManager.onWebKeypadClose()');

        // 가상 키패드 설정
        if (!secureTxf.isSetVirtualKeyboard) {
            ML4WebVKeyPad.setVirtualKeyboard(secureTxf.element);
            secureTxf.isSetVirtualKeyboard = true;
        }

        // 키보드 표시
        ML4WebVKey.showKeyboard(secureTxf.element.id);

        if (rootView && rootView.onSecurePadChange) rootView.onSecurePadChange(true);

        // input 이벤트 바인딩
        if (!secureTxf.isInputEvent) {
            secureTxf.bindEvent('input', function () {
                const inputVal = this.value;
                const len = inputVal.length;

                // 암호화 전 평문 저장
                this.acomp.setCipherData(inputVal);
                this.acomp.setPwLength(len);

                // 최대 길이 도달 시 enterKey 호출
                if (SecureWebPadManager.padOption.maxLength === len) {
                    ML4WebVKey[secureTxf.element.id].enterKey();
                }
            });

            secureTxf.isInputEvent = true;
        }

        // 콜백 저장
        this.callback = callback;
    },

    // 키패드 닫힘 이벤트
    onWebKeypadClose: function(id) {
        const sxf = document.getElementById(id).acomp;
        const plainText = ML4WebVKey.getDecryptedPassword(id);
        const len = plainText.length;

        // 암호화 후 설정
        sxf.setCipherData(plainText);
        sxf.setPwLength(len);
        sxf.$ele.trigger('change');

        const encrypted = CryptoJS.AES.encrypt(plainText, id).toString();

        if (this.callback) {
            this.callback(true, {
                val: encrypted,
                info: id,
                len: len
            }, len);

            this.callback = null;
        }

        const rootView = sxf.getRootView();
        if (rootView && rootView.onSecurePadChange) rootView.onSecurePadChange(false);
    }
};

```



* 실행 결과

<figure><img src="../../.gitbook/assets/화면 녹화 중 2025-07-03 160639.gif" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
<mark style="color:red;">**Build 에러 발생 시**</mark>

_**프로젝트 트리뷰에서 Framework > stock 우클릭 > Default Load Settings.. > Component > EXSecureTextField.js 체크**_

_**프로젝트 트리뷰에서 Framework > afc 우클릭 > Default Load Settings.. > Component > AButton.js + AButtonEvent.js + AToast.js 체크**_

<img src="../../.gitbook/assets/스크린샷 2025-07-03 154421 (1).png" alt="" data-size="original"><img src="../../.gitbook/assets/스크린샷 2025-07-03 154435 (3).png" alt="" data-size="original">
{% endhint %}



