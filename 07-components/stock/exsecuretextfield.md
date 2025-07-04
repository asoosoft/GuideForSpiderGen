# EXSecureTextField

<figure><img src="../../.gitbook/assets/스크린샷 2025-07-01 101344.png" alt=""><figcaption></figcaption></figure>

민감한 정보(비밀번호 등)를 SecurePadManager 클래스 또는 객체를 이용하여 외부 라이브러리와 손쉽게 연동하여 안전하게 입력받을 수 있는 입력 컴포넌트.



### Appearance

공통 Appearance 는 [**6. Global Properties**](<../../Guide for SpiderGen/06  SpiderGen Editor/04  Properties Pane/02 Appearence.md>) 속성을 참고

### Attribute

EXSecureTextField 속성

<figure><img src="../../.gitbook/assets/스크린샷 2025-06-30 093412.png" alt=""><figcaption></figcaption></figure>

**Data**

<table data-header-hidden><thead><tr><th width="361"></th><th></th></tr></thead><tbody><tr><td><strong>이름</strong></td><td><strong>설명</strong></td></tr><tr><td><strong>속성</strong></td><td></td></tr><tr><td><code>Text</code></td><td>입력값</td></tr><tr><td><code>Placeholder</code></td><td>입력 전 양식</td></tr><tr><td><code>Align</code></td><td>텍스트 정렬(left, center, right)</td></tr><tr><td><code>Pad Title</code></td><td>키패드가 열릴 때 상단 제목</td></tr><tr><td><code>Data Type</code></td><td>키패드 입력 방식</td></tr><tr><td><code>Return Type</code></td><td>결과 반환 방식</td></tr><tr><td><code>MinLength</code></td><td>최소 입력 길이</td></tr><tr><td><code>MaxLength</code></td><td>최대 입력 길이</td></tr></tbody></table>

### Example

**1. 프로젝트 생성**

* 프로젝트 트리뷰에서 Source > MainView.lay 파일을 클릭
* MainView의 레이아웃 파일이 오픈되면 컴포넌트 리스트에서 EXSecureTextField 컴포넌트를 선택하고 드래그하여 레이아웃에 배치
* Class 에서 EXSecureTextField ID를 secureBox, AButton ID를 btn으로 지정



**2. 데이터 설정**

<figure><img src="../../.gitbook/assets/화면 녹화 중 2025-07-04 140530.gif" alt=""><figcaption></figcaption></figure>

* 먼저 MainView.js 파일을 오픈
* 상단의 파일탭에서 MainView.lay 탭을 더블 클릭하거나 우측의 프로젝트 트리에서 MainView.js 파일을 더블 클릭
* 모든 화면뷰는 onInitDone() 함수가 존재하며 이 함수는 화면이 생성될 때 딱 한번 실행
* onInitDone() 함수에서 레이블의 텍스트 내용을 아래와 같이 코드를 입력



**2-1) OpenPad 사용 예제**

```javascript
onInitDone() {
    super.onInitDone();

    // 키패드 열림/닫힘 알림 콜백
    this.onSecurePadChange = function (isOpen) {
        AToast.show('SecurePad 상태: ' + (isOpen ? '열림' : '닫힘'));
    };

    // SecureTextField 설정
    const secureTxf = this.secureBox;
    secureTxf.setAttr('readonly', true);
    secureTxf.setPlaceholder('비밀번호 입력');
    secureTxf.setText('');

    const padOption = {
        title: '비밀번호 입력',
        padType: 'char',
        returnType: '1',
        minLength: 4,
        maxLength: 20
    };

    secureTxf.padOption = padOption;

    // 버튼 클릭 시 보안 키패드 오픈
    this.btn.bindEvent('click', () => {
        const el = document.getElementById(secureTxf.element.id);

        console.log('[ID 추적]', secureTxf.element.id);
        console.log('[DOM 있음?]', el);
        console.log('[acomp 연결됨?]', el?.acomp);

        if (!el || !el.acomp) {
            AToast.show('입력 필드가 아직 렌더링되지 않았습니다.');
            return;
        }

        SecurePadManager.openPad(padOption, (isSuccess, result, length) => {
            if (isSuccess && result) {
                secureTxf.setCipherData(result.val);
                secureTxf.setPwLength(result.len);
                secureTxf.setText(afc.makeDummyString(result.len)); // 마스킹 처리
                secureTxf.reportEvent('change');
            } else {
                AToast.show('입력 취소 또는 실패');
            }
        }, secureTxf);
    });

    // change 이벤트 핸들링
    secureTxf.bindEvent('change', () => {
        AToast.show(
            '입력값: ' + secureTxf.getText() +
            '\n암호화 데이터: ' + secureTxf.getCipherData() +
            '\n입력 길이: ' + secureTxf.getPwLength()
        );
    });
}
```

**2-2) OpenWebPad 사용 예제**

```javascript
onInitDone() {
    super.onInitDone();

    // 키패드 열림/닫힘 알림 콜백
    this.onSecurePadChange = function (isOpen) {
        AToast.show('SecurePad 상태: ' + (isOpen ? '열림' : '닫힘'));
    };

    const secureTxf = this.secureBox;
    secureTxf.setAttr('readonly', true);
    secureTxf.setPlaceholder('비밀번호 입력');
    secureTxf.setText('');

    const padOption = {
        title: '비밀번호 입력',
        padType: 'char',
        returnType: '1',
        minLength: 4,
        maxLength: 20
    };

    secureTxf.padOption = padOption;

    // 버튼 클릭 시 보안 키패드 오픈 (웹 전용 호출로 수정)
    this.btn.bindEvent('click', () => {
        SecureWebPadManager.openWebPad(padOption, (isSuccess, result, length) => {
            if (isSuccess && result) {
                secureTxf.setCipherData(result.val);
                secureTxf.setPwLength(result.len);
                secureTxf.setText(afc.makeDummyString(result.len));
                secureTxf.reportEvent('change');
            } else {
                AToast.show('입력 취소 또는 실패');
            }
        }, secureTxf, this); // ← rootView (this) 추가 전달
    });


    // change 이벤트 핸들링
    secureTxf.bindEvent('change', () => {
        AToast.show(
            '입력값: ' + secureTxf.getText() +
            '\n암호화 데이터: ' + secureTxf.getCipherData() +
            '\n입력 길이: ' + secureTxf.getPwLength()
        );
    });
}
```

**3. 프로젝트 실행**

<figure><img src="../../.gitbook/assets/화면 녹화 중 2025-07-04 135750.gif" alt=""><figcaption></figcaption></figure>

* 설정한 데이터에 맞춰서 컴포넌트와 입력 텍스트가 표시



**4. 코드로&#x20;**_**EXSecureTextField**_**&#x20;생성**

* 먼저 MainView.js 파일을 오픈
* onInitDone() 함수에서 아래와 같이 코드를 입력



**4-1) OpenPad 사용 예제**

```javascript
onInitDone() {
    super.onInitDone();

    // SecurePad 열고 닫힐 때 알림
    this.onSecurePadChange = function (isOpen) {
        AToast.show('SecurePad 상태: ' + (isOpen ? '열림' : '닫힘'));
    };

    // SecureTextField 생성 및 설정
    let secureTxf = new EXSecureTextField();

    let id = 'secure-input-' + Date.now();
    secureTxf.createElement();              // DOM 생성
    secureTxf.setComponentId(id);           // 컴포넌트 ID 등록
    secureTxf.init();                       // 초기화

    secureTxf.element.id = id;              // DOM에 직접 ID 지정
    secureTxf.element.acomp = secureTxf;  // acomp 연결
    this.addComponent(secureTxf);           // 실제로 화면에 붙임
    secureTxf.setText('');

    secureTxf.setPlaceholder('비밀번호 입력');
    secureTxf.setPos(100, 100);
    secureTxf.setAttr('readonly', true);

    // 패드 옵션 설정
    let padOption = {
        title: '비밀번호 입력',
        padType: 'char',
        returnType: '1',
        minLength: 4,
        maxLength: 20
    };

    secureTxf.padOption = padOption;

    // 버튼 생성 및 설정
    const btn = new AButton();
    btn.createElement();
    this.addComponent(btn);
    btn.init();
    btn.setText('🔐 보안 키패드');
    btn.setPos(100, 150);
    btn.setSize(200, 40);

    // 버튼 클릭 시 SecurePad 열기
    btn.bindEvent('click', () => {
        requestAnimationFrame(() => {  // DOM이 렌더된 이후 실행
            const el = document.getElementById(secureTxf.element.id);

            if (!el || !el.acomp) {
                AToast.show('입력 필드가 아직 렌더링되지 않았습니다.');
                return;
            }

            SecurePadManager.openPad(padOption, (isSuccess, result, length) => {
                if (isSuccess && result) {
                    secureTxf.setCipherData(result.val);
                    secureTxf.setPwLength(result.len);
                    secureTxf.setText(afc.makeDummyString(result.len)); // 마스킹
                    secureTxf.reportEvent('change');
                } else {
                    AToast.show('입력 취소 또는 실패');
                }
            }, secureTxf);
        });
    });


    // 변경 시 알림
    secureTxf.bindEvent('change', () => {
        AToast.show(
            '입력값: ' + secureTxf.getText() +
            '\n암호화 데이터: ' + secureTxf.getCipherData() +
            '\n입력 길이: ' + secureTxf.getPwLength()
        );
    });

    // this.secureTxf 저장
    this.secureTxf = secureTxf;
}
```



**4-2) OpenWebPad 사용 예제**

```javascript
onInitDone() {
    super.onInitDone();

    // 키패드 열림/닫힘 알림 콜백
    this.onSecurePadChange = function (isOpen) {
        AToast.show('SecurePad 상태: ' + (isOpen ? '열림' : '닫힘'));
    };

    // SecureTextField 생성 및 설정
    const secureTxf = new EXSecureTextField();

    const id = 'secure-input-' + Date.now();
    secureTxf.createElement();              // DOM 생성
    secureTxf.setComponentId(id);           // 컴포넌트 ID 등록
    secureTxf.init();                       // 초기화

    secureTxf.element.id = id;              // DOM에 직접 ID 지정
    secureTxf.element.acomp = secureTxf;    // acomp 연결
    this.addComponent(secureTxf);           // 화면에 붙임
    secureTxf.setText('');

    secureTxf.setPlaceholder('비밀번호 입력');
    secureTxf.setPos(100, 100);
    secureTxf.setAttr('readonly', true);

    // 패드 옵션 설정
    const padOption = {
        title: '비밀번호 입력',
        padType: 'char',
        returnType: '1',
        minLength: 4,
        maxLength: 20
    };

    secureTxf.padOption = padOption;

    // 버튼 생성 및 설정
    const btn = new AButton();
    btn.createElement();
    this.addComponent(btn);
    btn.init();
    btn.setText('🔐 보안 키패드');
    btn.setPos(100, 150);
    btn.setSize(200, 40);

    // 버튼 클릭 시 SecureWebPadManager 사용
    btn.bindEvent('click', () => {
        requestAnimationFrame(() => {
            const el = document.getElementById(secureTxf.element.id);
            console.log('[ID 추적]', secureTxf.element.id);
            console.log('[DOM 있음?]', el);
            console.log('[acomp 연결됨?]', el?.acomp);

            if (!el || !el.acomp) {
                AToast.show('입력 필드가 아직 렌더링되지 않았습니다.');
                return;
            }

            SecureWebPadManager.openWebPad(padOption, (isSuccess, result, length) => {
                if (isSuccess && result) {
                    secureTxf.setCipherData(result.val);
                    secureTxf.setPwLength(result.len);
                    secureTxf.setText(afc.makeDummyString(result.len)); // 마스킹 처리
                    secureTxf.reportEvent('change');
                } else {
                    AToast.show('입력 취소 또는 실패');
                }
            }, secureTxf, this);  // ← rootView로 this 전달
        });
    });

    // 값 변경 시 이벤트
    secureTxf.bindEvent('change', () => {
        AToast.show(
            '입력값: ' + secureTxf.getText() +
            '\n암호화 데이터: ' + secureTxf.getCipherData() +
            '\n입력 길이: ' + secureTxf.getPwLength()
        );
    });

    // 나중에 접근할 수 있도록 저장
    this.secureTxf = secureTxf;
}
```



5. **라이브러리**

<figure><img src="../../.gitbook/assets/스크린샷 2025-07-04 141522.png" alt=""><figcaption></figcaption></figure>

* _**프로젝트 트리뷰에서 Framework > Library 우클릭 > Add new > Javascript**_&#x20;

| 파일명                        | 설명                                    |
| -------------------------- | ------------------------------------- |
| **ML4WebVKeyPad.js**       | 웹 가상 키보드를 제어하고 표시하기 위한 핵심 라이브러리       |
| **CryptoJS.js**            | 입력된 데이터를 간단하게 암호화하거나 복호화하는 유틸리티 함수 모음 |
| **SecurePadManager.js**    | 네이티브/웹 보안 키패드의 열기/닫기 및 입력 처리 전반을 관리   |
| **SecureWebPadManager.js** | 웹에서만 동작하는 보안 키패드의 세부 로직을 별도로 관리       |



* **CryptoJS.js**

```javascript
window.CryptoJS = {};

CryptoJS.AES = {};

CryptoJS.AES.encrypt = function (plainText, key) {
    var result = '';
    for (var i = 0; i < plainText.length; i++) {
        var charCode = plainText.charCodeAt(i) ^ key.charCodeAt(i % key.length);
        result += String.fromCharCode(charCode);
    }

    return {
        toString: function () {
            return btoa(result); // Base64 인코딩
        }
    };
};

CryptoJS.AES.decrypt = function (cipherText, key) {
    var decoded = atob(cipherText); // Base64 디코딩
    var result = '';
    for (var i = 0; i < decoded.length; i++) {
        var charCode = decoded.charCodeAt(i) ^ key.charCodeAt(i % key.length);
        result += String.fromCharCode(charCode);
    }
    return result;
};

```



* **ML4WebVKeyPad.js (PC 버전)**

<figure><img src="../../.gitbook/assets/스크린샷 2025-07-04 141758.png" alt=""><figcaption></figcaption></figure>

```javascript
window.ML4WebVKey = {
    showKeyboard: function(id) {
        const input = document.getElementById(id);
        if (!input) {
            console.warn('[ML4WebVKey] 입력 필드 없음:', id);
            return;
        }
        input.focus();
    },

    _onKeyClick: function(key, input) {
        const acomp = input.acomp;
        if (!acomp) {
            console.warn('[ML4WebVKey] acomp 연결 안됨:', input);
            return;
        }

        let val = input.value || '';

        if (key === '←') {
            val = val.slice(0, -1);
        } else if (key === '확인') {
            SecurePadManager.onWebKeypadClose(input.id);
            //SecureWebPadManager.onWebKeypadClose(input.id); 2-2) openWebPad 사용 시 주석 해제
            document.getElementById('vkey-container')?.remove();
            return;
        } else if (key === 'reset') {
            input.value = '';
            input.dispatchEvent(new Event('input'));
            return;
        } else {
            val += key;
        }

        input.value = val;
        input.dispatchEvent(new Event('input'));
    },

    getDecryptedPassword: function(id) {
        const input = document.getElementById(id);
        return input ? input.value : '';
    },

    enterKey: function() {
        console.log('[ML4WebVKey] Enter 키 눌림');
    }
};

window.ML4WebVKeyPad = {
    setVirtualKeyboard: function (element) {
        if (document.getElementById('vkey-container')) return;

        const container = document.createElement('div');
        container.id = 'vkey-container';
        container.style.position = 'fixed';
        container.style.bottom = '0';
        container.style.left = '0';
        container.style.width = '100%';
        container.style.background = '#f2f2f2';
        container.style.padding = '12px';
        container.style.zIndex = '9999';
        container.style.boxShadow = '0 -2px 8px rgba(0,0,0,0.2)';
        container.style.display = 'flex';
        container.style.flexDirection = 'column';
        container.style.alignItems = 'center';
        container.style.gap = '12px';

        // 상단 안내 텍스트
        const infoText = document.createElement('div');
        infoText.innerText = '59초 후에 보안세션이 만료됩니다.';
        infoText.style.color = '#555';
        infoText.style.fontSize = '14px';
        infoText.style.marginBottom = '8px';
        container.appendChild(infoText);

        // 숫자 키 배열
        const rows = [
            ['🔒', '0', '1', '2', '3', '4'],
            ['5', '6', '7', '🔒', '8', '9']
        ];

        rows.forEach(rowKeys => {
            const row = document.createElement('div');
            row.style.display = 'flex';
            row.style.justifyContent = 'center';
            row.style.gap = '10px';

            rowKeys.forEach(key => {
                const btn = document.createElement('button');
                btn.innerText = key;
                btn.style.width = '48px';
                btn.style.height = '48px';
                btn.style.borderRadius = '10px';
                btn.style.border = 'none';
                btn.style.background = '#fff';
                btn.style.color = '#000';
                btn.style.fontSize = '18px';
                btn.style.boxShadow = '0 2px 4px rgba(0,0,0,0.2)';
                btn.style.cursor = 'pointer';

                btn.onclick = () => {
                    ML4WebVKey._onKeyClick(key, element);
                };

                row.appendChild(btn);
            });

            container.appendChild(row);
        });

        // 하단 특수 키 영역
        const bottomRow = document.createElement('div');
        bottomRow.style.display = 'flex';
        bottomRow.style.justifyContent = 'center';
        bottomRow.style.gap = '12px';
        bottomRow.style.marginTop = '8px';

        const specialKeys = [
            { label: '↻', action: 'reset', bg: '#ccc' },
            { label: '⌫', action: '←', bg: '#ccc' },
            { label: '✔', action: '확인', bg: '#2196f3', color: '#fff' },
            { label: '✖', action: '취소', bg: '#ccc' }
        ];

        specialKeys.forEach(({ label, action, bg, color }) => {
            const btn = document.createElement('button');
            btn.innerText = label;
            btn.style.width = '56px';
            btn.style.height = '48px';
            btn.style.borderRadius = '10px';
            btn.style.border = 'none';
            btn.style.background = bg;
            btn.style.color = color || '#000';
            btn.style.fontSize = '18px';
            btn.style.boxShadow = '0 2px 4px rgba(0,0,0,0.2)';
            btn.style.cursor = 'pointer';

            btn.onclick = () => {
                if (action === '취소') {
                    document.getElementById('vkey-container')?.remove();
                } else {
                    ML4WebVKey._onKeyClick(action, element);
                }
            };

            bottomRow.appendChild(btn);
        });

        container.appendChild(bottomRow);
        document.body.appendChild(container);
    }
};

```



* **ML4WebVKeyPad.js (모바일 버전)**

<figure><img src="../../.gitbook/assets/스크린샷 2025-07-04 141206.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/화면 녹화 중 2025-07-04 155629.gif" alt=""><figcaption></figcaption></figure>

```
window.ML4WebVKeyPad = {
    setVirtualKeyboard: function(element) {
        // 이미 열려있으면 스킵
        if (document.getElementById('vkey-container')) return;

        const container = document.createElement('div');
        container.id = 'vkey-container';
        container.style.position = 'fixed';
        container.style.bottom = '0';
        container.style.left = '0';
        container.style.width = '100%';
        container.style.background = '#222'; // 다크 톤
        container.style.padding = '10px';
        container.style.display = 'grid';
        container.style.gridTemplateColumns = 'repeat(10, 1fr)';
        container.style.gap = '8px';
        container.style.zIndex = '9999';
        container.style.boxShadow = '0 -3px 10px rgba(0,0,0,0.5)';

        const keys = [
            '1','2','3','4','5','6','7','8','9','0',
            'Q','W','E','R','T','Y','U','I','O','P',
            'A','S','D','F','G','H','J','K','L',
            'Z','X','C','V','B','N','M',
            '←','확인'
        ];

        keys.forEach(key => {
            const btn = document.createElement('button');
            btn.textContent = key;
            btn.style.fontSize = '18px';
            btn.style.padding = '16px';
            btn.style.borderRadius = '8px';
            btn.style.border = 'none';
            btn.style.background = key === '확인' ? '#1e88e5' : (key === '←' ? '#555' : '#444');
            btn.style.color = '#fff';
            btn.style.boxShadow = '0 2px 5px rgba(0,0,0,0.3)';
            btn.style.cursor = 'pointer';
            btn.style.transition = 'background 0.2s';

            btn.onmouseover = () => { btn.style.background = '#666'; };
            btn.onmouseout = () => {
                btn.style.background = key === '확인' ? '#1e88e5' : (key === '←' ? '#555' : '#444');
            };

            btn.onclick = () => {
                ML4WebVKey._onKeyClick(key, element);
            };

            container.appendChild(btn);
        });

        document.body.appendChild(container);
    }
};

window.ML4WebVKey = {
    showKeyboard: function(id) {
        const input = document.getElementById(id);
        if (!input) {
            console.warn('[ML4WebVKey] 입력 필드 없음:', id);
            return;
        }
        input.focus();
    },

    _onKeyClick: function(key, input) {
        const acomp = input.acomp;
        if (!acomp) {
            console.warn('[ML4WebVKey] acomp 연결 안됨:', input);
            return;
        }

        let val = input.value || '';

        if (key === '←') {
            val = val.slice(0, -1);
        } else if (key === '확인') {
            SecurePadManager.onWebKeypadClose(input.id);
            //SecureWebPadManager.onWebKeypadClose(input.id); 2-2) openWebPad 사용 시 주석 해제
            document.getElementById('vkey-container')?.remove();
            return;
        } else {
            val += key;
        }

        input.value = val;
        input.dispatchEvent(new Event('input'));
    },

    getDecryptedPassword: function(id) {
        const input = document.getElementById(id);
        return input ? input.value : '';
    },

    enterKey: function() {
        console.log('[ML4WebVKey] Enter 키 눌림');
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



{% hint style="info" %}
<mark style="color:red;">**Build 에러 발생 시**</mark>

_**프로젝트 트리뷰에서 Framework > stock 우클릭 > Default Load Settings.. > Component > EXSecureTextField.js 체크**_

_**프로젝트 트리뷰에서 Framework > afc 우클릭 > Default Load Settings.. > Component > AButton.js + AButtonEvent.js + AToast.js 체크(Button 라이브러리는 5번 예제부터 필요)**_

<img src="../../.gitbook/assets/스크린샷 2025-07-04 103126.png" alt="" data-size="original"><img src="../../.gitbook/assets/스크린샷 2025-07-04 103134.png" alt="" data-size="original"><img src="../../.gitbook/assets/스크린샷 2025-07-04 103232.png" alt="" data-size="original">
{% endhint %}



