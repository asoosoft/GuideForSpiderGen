# ExSecureTextField

`ExSecureTextField`는 비밀번호, API 키, 시크릿 키 등 민감한 정보를 안전하게 입력받을 수 있도록 설계된 보안 입력 컴포넌트입니다.

일반 `TextField`와 동일한 입력 기능을 가지면서도 다음과 같은 보안 기능을 제공합니다.

* 입력값 마스킹 (••••• 형태)
* 클립보드 복사 차단
* 자동 완성 차단
* 입력 값 암호화 지원 (옵션)
* 표시/숨김 토글 기능

***

## 주요 기능

* 입력 텍스트 마스킹
* 표시/숨김 토글 버튼 제공
* 클립보드 복사 방지 기능
* 자동 완성/자동 저장 차단
* 입력 값 암호화 및 복호화 지원 (옵션)

***

## UI 구성 요소

| 요소     | 설명                    |
| ------ | --------------------- |
| 입력 필드  | 텍스트 입력 영역 (기본 마스킹 처리) |
| 토글 버튼  | 입력값 표시/숨김 토글          |
| 플레이스홀더 | 입력 안내 텍스트             |
| 오류 표시  | 유효성 검사 실패 시 오류 메시지    |

***

## 메서드

### 입력 및 동작 관련

#### setValue(value)

* 입력값 설정
* 마스킹 상태와 상관없이 내부 값 저장

#### getValue()

* 현재 입력된 실제 값 반환 (마스킹 해제 상태와 무관)

#### clear()

* 입력값 초기화

#### setPlaceholder(text)

* 플레이스홀더 텍스트 설정

#### setReadonly(isReadonly)

* 읽기 전용 상태 설정

### 표시 및 스타일 관련

#### showPassword(isShow)

* true → 텍스트 표시
* false → 마스킹 처리

#### togglePassword()

* 표시/숨김 상태 전환

#### setError(message)

* 오류 메시지 표시

#### clearError()

* 오류 메시지 삭제

### 보안 기능

#### enableClipboardBlock(enable)

* 클립보드 복사/붙여넣기 차단 여부 설정

#### enableAutoCompleteBlock(enable)

* 자동 완성 및 브라우저 저장 차단 여부 설정

#### enableEncryption(secretKey)

* 내부적으로 입력값을 암호화하여 저장
* 반환 시 복호화된 값을 제공

***

## 이벤트

| 이벤트 이름                      | 설명            |
| --------------------------- | ------------- |
| onTextChanged(value)        | 입력 값 변경 시 호출  |
| onEnterPressed()            | 엔터 키 입력 시 호출  |
| onVisibilityToggled(isShow) | 표시/숨김 버튼 클릭 시 |

***

## 속성 및 설정

| 속성                      | 설명                       | 기본값  |
| ----------------------- | ------------------------ | ---- |
| maskCharacter           | 마스킹 문자 (예: '•')          | •    |
| enableClipboardBlock    | 클립보드 복사 차단 여부            | true |
| enableAutoCompleteBlock | 자동 완성 차단 여부              | true |
| showToggleButton        | 표시/숨김 버튼 사용 여부           | true |
| encryptionKey           | 내부 데이터 암호화 키 (설정 시 암호화됨) | 없음   |

***

## UI 예시

```
┌───────────────────────────────┐
│ [•••••••••••••••] [👁️]         │
│  비밀번호를 입력하세요          │
└───────────────────────────────┘

- 👁️ 아이콘 클릭 → 마스킹 해제/적용
```

***

## 사용 예제

```javascript
const secureField = new ExSecureTextField();

// 플레이스홀더 설정
secureField.setPlaceholder('API Secret Key');

// 값 설정
secureField.setValue('mysecret123');

// 값 가져오기
const val = secureField.getValue();
console.log('입력값:', val);

// 표시 토글
secureField.togglePassword();

// 오류 메시지
secureField.setError('입력값이 올바르지 않습니다.');

// 클립보드 차단 설정
secureField.enableClipboardBlock(true);
```

***

## 오류 처리

* 입력값이 비어있거나 유효하지 않은 경우 `setError()`로 오류 메시지 표시
* 암호화 설정 후 키가 불일치하면 복호화 실패
* 클립보드 차단 기능 미지원 브라우저는 내부 경고 로그 출력

***

## 초기화 및 종료 순서

1. 컴포넌트 인스턴스 생성
2. `setPlaceholder()` 및 필요한 설정 적용
3. 입력값 처리
4. 필요 시 `clear()`로 값 초기화
5. 종료 시 별도 정리 불필요

