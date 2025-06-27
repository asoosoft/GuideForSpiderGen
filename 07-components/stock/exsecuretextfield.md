# ExSecureTextField

**ExSecureTextField**는 비밀번호, API 키, 시크릿 키 등 민감한 정보를 안전하게 입력받을 수 있도록 설계된 보안 입력 컴포넌트입니다.

일반 텍스트 필드와 동일한 입력 기능을 가지면서도 다음과 같은 보안 기능을 제공합니다.

* 입력값 마스킹 (••••• 형태)
* 표시/숨김 토글 버튼 제공
* 클립보드 복사 차단
* 자동 완성 및 자동 저장 차단
* 입력 값 암호화 및 복호화 지원 (옵션)

***

### Key Features

* 입력 텍스트 마스킹
* 입력값 표시/숨김 토글 버튼 제공
* 클립보드 복사/붙여넣기 차단
* 브라우저 자동 완성 및 저장 차단
* 선택적으로 입력 값 암호화 지원

***

### UI Components

| Component        | Description                |
| ---------------- | -------------------------- |
| Input Field      | 텍스트 입력 영역 (마스킹 상태로 표시)     |
| Toggle Button    | 👁️ 아이콘. 클릭 시 입력값 표시/숨김 전환 |
| Placeholder Text | 입력 안내 문구                   |
| Error Message    | 유효성 검사 실패 시 오류 표시          |

***

### Events

| Event Name                  | Description         |
| --------------------------- | ------------------- |
| onTextChanged(value)        | 입력값 변경 시 호출         |
| onEnterPressed()            | 엔터 키 입력 시 호출        |
| onVisibilityToggled(isShow) | 표시/숨김 토글 버튼 클릭 시 호출 |

***

### Properties & Settings

| Property                | Description                   | Default |
| ----------------------- | ----------------------------- | ------- |
| maskCharacter           | 마스킹 문자                        | •       |
| enableClipboardBlock    | 클립보드 복사 및 붙여넣기 차단 여부          | true    |
| enableAutoCompleteBlock | 자동 완성 및 브라우저 저장 차단 여부         | true    |
| showToggleButton        | 표시/숨김 토글 버튼 사용 여부             | true    |
| encryptionKey           | 입력 데이터 암호화 키 (설정 시 내부적으로 암호화) | 없음      |

***

### UI Example

```
┌───────────────────────────────┐
│ [•••••••••••••••] [👁️]         │
│  비밀번호를 입력하세요          │
└───────────────────────────────┘

- 👁️ 아이콘 클릭 → 마스킹 해제/적용
```

***

### Example Usage

```javascript
const secureField = new ExSecureTextField();

// 플레이스홀더 설정
secureField.setPlaceholder('API Secret Key');

// 값 설정
secureField.setValue('mysecret123');

// 값 가져오기
const val = secureField.getValue();
console.log('입력값:', val);

// 표시 상태 토글
secureField.togglePassword();

// 오류 메시지 표시
secureField.setError('입력값이 올바르지 않습니다.');

// 클립보드 차단 활성화
secureField.enableClipboardBlock(true);
```

***

### Error Handling

* 입력값이 비어있거나 유효하지 않은 경우 오류 메시지 표시
* 암호화 키가 불일치하는 경우 복호화 실패
* 클립보드 차단 기능이 지원되지 않는 브라우저는 내부 경고 출력

***

### Initialization & Lifecycle

1. 컴포넌트 인스턴스 생성
2. 플레이스홀더 및 필요한 속성 설정
3. 입력값 처리
4. 필요 시 값 초기화
5. 종료 시 별도 정리 불필요

