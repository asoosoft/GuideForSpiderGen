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

1. **라이브러리**

<figure><img src="../../.gitbook/assets/image (109).png" alt=""><figcaption></figcaption></figure>

* _**프로젝트 트리뷰에서 Framework > Library 우클릭 > Add new > Javascript**_&#x20;

| 파일명                     | 설명                                  |
| ----------------------- | ----------------------------------- |
| **SpiderGenKeyPad.js**  | 웹 가상 키보드를 제어하고 표시하기 위한 핵심 라이브러리     |
| **SecurePadManager.js** | 네이티브/웹 보안 키패드의 열기/닫기 및 입력 처리 전반을 관리 |



* **SpiderGenKeyPad.js**

<figure><img src="../../.gitbook/assets/스크린샷 2025-07-04 141758.png" alt=""><figcaption></figcaption></figure>

```javascript
window.SpiderGenKeyPad = {
    showKeyboard: function(id) {
        const input = document.getElementById(id);
        if (!input) {
            console.warn('[SpiderGenKeyPad] 입력 필드 없음:', id);
            return;
        }
        input.focus();
    },

    _onKeyClick: function(key, input) {
        const acomp = input.acomp;
        if (!acomp) {
            console.warn('[SpiderGenKeyPad] acomp 연결 안됨:', input);
            return;
        }

        let val = input.value || '';

        if (key === '←') {
            val = val.slice(0, -1);
        } else if (key === '확인') {
            SpiderGenKeyPad.onWebKeypadClose(input.id);
            document.getElementById('vkey-container')?.remove();
            return;
        } else if (key === 'reset') {
            input.value = '';
            input.dispatchEvent(new Event('input'));
            return;
        } else if (key === '취소') {
            document.getElementById('vkey-container')?.remove();
            if (typeof SecurePadManager?.callback === 'function') {
                SecurePadManager.callback(true, null, 0);
            }
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
        console.log('[SpiderGenKeyPad] Enter 키 눌림');
    },

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

        const infoText = document.createElement('div');
        infoText.innerText = '59초 후에 보안세션이 만료됩니다.';
        infoText.style.color = '#555';
        infoText.style.fontSize = '14px';
        infoText.style.marginBottom = '8px';
        container.appendChild(infoText);

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
                    SpiderGenKeyPad._onKeyClick(key, element);
                };

                row.appendChild(btn);
            });

            container.appendChild(row);
        });

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
                SpiderGenKeyPad._onKeyClick(action, element);
            };

            bottomRow.appendChild(btn);
        });

        container.appendChild(bottomRow);
        document.body.appendChild(container);
    },

    // SecurePadManager에서 참조 시 필요
    onWebKeypadClose: function(id) {
        if (SecurePadManager && typeof SecurePadManager.onWebKeypadClose === 'function') {
            SecurePadManager.onWebKeypadClose(id);
        }
    }
};
```



* **SecurePadManager.js**

```javascript
var SecurePadManager = {
	isEnable: true,//afc.isNative,
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
				SpiderGenKeyPad.setVirtualKeyboard(secureTxf.element);
				secureTxf.setAttr('ds-kb-callback', 'SecurePadManager.onWebKeypadClose()');
			}
			secureTxf.isSetVirtualKeyboard = true;
			SpiderGenKeyPad.showKeyboard(secureTxf.element.id);
			if (rootView && rootView.onSecurePadChange) rootView.onSecurePadChange(true);

			
			if(!secureTxf.isInputEvent) {
				secureTxf.bindEvent('input', function() {
                    const inputVal = this.value;
                    const len = inputVal.length;

                    // 값 저장 (this.acomp는 EXSecureTextField 인스턴스)
                    this.acomp.setCipherData(inputVal);
                    this.acomp.setPwLength(len);

                    if (thisObj.padOption.maxLength == len) {
                        SpiderGenKeyPad[secureTxf.element.id].enterKey();
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
        
        var plainText = SpiderGenKeyPad.getDecryptedPassword(id);
        var len = plainText.length;

        // 여기에서 직접 값 설정
        sxf.setCipherData(plainText);
        sxf.setPwLength(len);

        sxf.element.dispatchEvent(new Event('change', { bubbles: true }));

        SecurePadManager.callback(true, {
            val: plainText,
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
};
```

**2. 프로젝트 생성**

* 프로젝트 트리뷰에서 Source > MainView.lay 파일을 클릭
* MainView의 레이아웃 파일이 오픈되면 컴포넌트 리스트에서 EXSecureTextField 컴포넌트를 선택하고 드래그하여 레이아웃에 배치

**3. 데이터 설정**

* 먼저 MainView.js 파일을 오픈
* 상단의 파일탭에서 MainView.lay 탭을 더블 클릭
* Component 목록 > stock > EXSecureTextField 생성
* Attribute > Data > Text > 'Text' 문자열 제거하고 빈 열로 실행



4. **Default Load Settings 설정**

* _**프로젝트 트리뷰에서 Framework > stock 우클릭 > Default Load Settings.. > Component > EXSecureTextField.js 체크 > 우측 상단  X(창닫기) 클릭 > 변경된 정보를 저장하시겠습니까> > Yes**_

![](../../.gitbook/assets/image.png)



**5. 프로젝트 실행**

<figure><img src="../../.gitbook/assets/화면 녹화 중 2025-07-07 114627.gif" alt=""><figcaption></figcaption></figure>

* 설정한 데이터에 맞춰 보안 키 패드 생성

**6. 코드로&#x20;**_**EXSecureTextField**_**&#x20;생성**

* 먼저 MainView.js 파일을 오픈
* onInitDone() 함수에서 아래와 같이 코드를 입력

```javascript
onInitDone() {

    super.onInitDone();

    // SecureTextField 생성 및 설정
    let secureTxf = new EXSecureTextField();
    secureTxf.init();

    secureTxf.element.acomp = secureTxf;
    this.addComponent(secureTxf);
    secureTxf.setText('');

    secureTxf.setPos(100, 100);
    secureTxf.setAttr('readonly', true);
    
}
```

**7. 프로젝트 실행**

<figure><img src="../../.gitbook/assets/화면 녹화 중 2025-07-07 131231.gif" alt=""><figcaption></figcaption></figure>

