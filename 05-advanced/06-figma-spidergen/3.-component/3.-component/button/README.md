---
description: 일반적으로 사용하는 버튼 컴포넌트.
---

# Button

## 1. 기본 버튼 생성

* 배경 설정
  * 프레임 선택후 버튼의 기본 영역을 그립니다.
  * 배경 색상을 적당히 설정합니다
    *

        <figure><img src="../../../../../.gitbook/assets/image (200).png" alt=""><figcaption></figcaption></figure>

        &#x20;
* 텍스트 설정 (Optional)
  * TextTool 로 Frame 안에 버튼 텍스트를 추가합니다
  * 이미지만 사용하는 버튼인경우 이 과정을 생략합니다.
    *

        <figure><img src="../../../../../.gitbook/assets/image (201).png" alt=""><figcaption></figcaption></figure>



* 이미지 설정  (Optional)
  * 이미지는 2가지 방식으로 가능합니다.
    * 자식에 Frame 을 추가하세
* 다중 이미지 설정 (Optional)
* 레이어로 이미지 설정(Optional)

## 2. 컴포넌트 크기조절에 따른 처리

* Auto Layout 설정
* Constraint 설정



## 3. 배경 이미지 처리



## 3. 컴포넌트 완성하기

* Component Configuration 설정



* 상태 추가



*



* Variants
  * Normal&#x20;
  * Over
  * Down
  * Disable
* 계층 구조
  * 배경혹은 Icon 을 추가하기 위한 이미지 Node
    * 이미지 Node 는 기본적으로 계층의 틀을 잡기위해 추가되었으나 기본상태는 비활성화.
  * 텍스트 Node&#x20;
  *

      <figure><img src="../../../../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>



## 2. Component Configuration

<figure><img src="../../../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

* 용도
  * Template 컴포넌트를 복사해서 사용하지 않고  직접 처음부터 생성하는경우, 아래 코드를 Component Configuration 에 추가해야 합니다.

Code:

```ini
기본적인 버튼 컴포넌트 입니다.
$${{"acomp":"AButton","class":["","","",""]}}
```



## 3. 활용&#x20;

### 1. 텍스트  버튼

<figure><img src="../../../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

* 텍스트만 표시할때 사용되는 버튼
* 계층 구조
  * 텍스트 Node
    *

        <figure><img src="../../../../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

### 2. 이미지 버튼

<figure><img src="../../../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

* 이미지만 표시할때 사용되는 버튼
* 계층구조
  * 이미지 Node
    *

        <figure><img src="../../../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>


  * 좀더 복잡한 구조의 이미지사용이 필요한 경우,  [image-guide.md](../image-guide.md "mention") 참고 (필독!)

### 3. 복합 버튼

<figure><img src="../../../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

* 이미지, 텍스트 둘다 표시할떄 사용되는 버튼.
* 계층구조
  * 이미지
  * 텍스트
    *

        <figure><img src="../../../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>


  * 백그라운드와 아이콘을 함께 쓰는등의 복잡한 사용이 필요한 경우, [image-guide.md](../image-guide.md "mention") 참고







