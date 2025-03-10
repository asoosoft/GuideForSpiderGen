![](https://wikidocs.net/images/page/274099/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_144506.png)

두 번 꺾인 선을 그리는 컴포넌트이며 다양한 선의 속성을 설정할 수 있는 기능을 제공.

## Attribute
### Type
| 기능 | 설명 |
|--|--|
| Angle | 선이 꺾이는 지점의 각도. |
| Arrow | 선의 화살표 사용 여부를 설정. |
| Line Color | 선의 색상을 설정할 수 있음. |
| Stroke Width | 선의 두께를 설정할 수 있음. |
| Leaning | 선의 비대칭을 설정할 수 있음. |
| head/tail | 선의 시작점과 끝점을 의미. |

### 1. Angle
#### 0° 예시화면
![](https://wikidocs.net/images/page/274099/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_144722.png)

#### 90° 예시화면
![](https://wikidocs.net/images/page/274099/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_144735.png)

#### 180° 예시화면
![](https://wikidocs.net/images/page/274099/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_144744.png)

#### 270° 예시화면
![](https://wikidocs.net/images/page/274099/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_144755.png)

### 2. Arrow
#### start 예시화면
![](https://wikidocs.net/images/page/274099/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_144808.png)

#### both 예시화면
![](https://wikidocs.net/images/page/274099/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_144826.png)

#### end 예시화면
![](https://wikidocs.net/images/page/274099/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_144817.png)

### 3. Stroke Width
![](https://wikidocs.net/images/page/274099/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_144930.png)

### 4. Leaning
#### 10% 예시화면
![](https://wikidocs.net/images/page/274099/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_144955.png)

#### 50% 예시화면
![](https://wikidocs.net/images/page/274099/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_144940.png)

### head / tail
* 반대 방향으로 전환

![](https://wikidocs.net/images/page/274099/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_145006.png)

## Example
### 화면에 컴포넌트 생성.
![](https://wikidocs.net/images/page/274099/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_171458.png)

### 코드로 컴포넌트 생성.
* Project > Framework > afc  > Default Load Settings  

![](https://wikidocs.net/images/page/274099/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-18_160427.png)

* AFlowThreeLine.js + compEx.css 선택

![](https://wikidocs.net/images/page/274099/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-03_132805.png)


* 생성 코드

```
    onInitDone() {

		super.onInitDone();

		// AFlowThreeLine 인스턴스 생성
		const flowThreeLine = new  AFlowThreeLine();

		flowThreeLine.init(); // 초기화

		// AFlowThreeLine 설정
		flowThreeLine.setLineColor('green'); // 선 색상 설정
		flowThreeLine.setStrokeWidth(3); // 선 두께 설정
		flowThreeLine.setArrow(true); // 화살표 사용 여부 설정
		flowThreeLine.setArrowPosition('end'); // 화살표 위치 설정 (끝점)

		// AFlowThreeLine을 부모 레이아웃에 추가
		this.addComponent(flowThreeLine);

		// 화면 가운데 배치
		flowThreeLine.centerX();
		flowThreeLine.centerY();
	}
```

* 실행 결과

![](https://wikidocs.net/images/page/274099/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-18_160516.png)