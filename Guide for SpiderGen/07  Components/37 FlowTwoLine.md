# 37 FlowTwoLine

![](https://wikidocs.net/images/page/274098/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_135229.png)

꺾인 선을 그리는 컴포넌트. 다양한 속성과 메서드를 통해 선의 스타일과 방향을 설정.

기본적으로 한번 꺾인 선을 그리며, 컴포넌트의 사이즈 정보가 변경될 때 자동으로 선을 다시 그리는 역할.

선의 양 끝에 화살표를 추가할 수 있으며 선의 색상과 두께를 설정 가능.

### Attribute

| 기능           | 설명                                             |
| ------------ | ---------------------------------------------- |
| Angle        | 선의 방향을 결정하는 데 사용되며, 꺾이는 지점에서의 방향 전환을 설정할 수 있음. |
| Arrow        | 선의 양 끝에 화살표를 추가할 수 있음.                         |
| Line Color   | 선의 색상을 지정할 수 있음.                               |
| Stroke Width | 선의 두께를 설정할 수 있음.                               |
| Extra Line   | 추가적인 선을 의미할 수 있으며, 주로 시각적 강조나 보조선을 그릴 때 사용.    |

#### 1. Angle

| Angle | 설명                 |
| ----- | ------------------ |
| 0°    | 선이 수평으로 오른쪽으로 그려짐. |
| 90°   | 선이 수직으로 아래쪽으로 꺾임.  |
| 180°  | 선이 수평으로 왼쪽으로 그려짐.  |
| 270°  | 선이 수직으로 위쪽으로 꺾임.   |

**0° 예시화면**

![](https://wikidocs.net/images/page/274098/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_142028.png)

**90° 예시화면**

![](https://wikidocs.net/images/page/274098/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_142048.png)

**180° 예시화면**

![](https://wikidocs.net/images/page/274098/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_142101.png)

**270° 예시화면**

![](https://wikidocs.net/images/page/274098/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_142109.png)

#### 2. Arrow

| Arrow | 설명                   |
| ----- | -------------------- |
| start | 화살표가 직선의 시작점에 위치.    |
| end   | 화살표가 직선의 끝점에 위치.     |
| both  | 화살표가 직선의 양 끝에 모두 위치. |

* start 예시화면

![](https://wikidocs.net/images/page/274098/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_142541.png)

* end 예시화면

![](https://wikidocs.net/images/page/274098/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_142552.png)

* both 예시화면

![](https://wikidocs.net/images/page/274098/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_142600.png)

#### 3. Stroke Width

![](https://wikidocs.net/images/page/274098/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_142641.png)

#### 4. Extra Line

* 30% 적용 예시

![](https://wikidocs.net/images/page/274098/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_142650.png)

* 50% 적용 예시

![](https://wikidocs.net/images/page/274098/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_142701.png)

* 70% 적용 예시

![](https://wikidocs.net/images/page/274098/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_142712.png)

### Example

#### 화면에 컴포넌트 생성

![](https://wikidocs.net/images/page/274098/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-01-24_171001.png)

#### 코드로 컴포넌트 생성

* Practice > Framework > afc > Default Load Settings

![](https://wikidocs.net/images/page/274098/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-18_154447.png)

* AFlowTwoLine.js + compEx.css 선택

![](https://wikidocs.net/images/page/274098/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-03_132418.png)

* 생성 코드

```
    onInitDone() {

		super.onInitDone();

		// AFlowTwoLine 인스턴스 생성
		const flowTwoLine = new  AFlowTwoLine();
		flowTwoLine.init(); // 초기화

		// AFlowTwoLine 설정
		flowTwoLine.setLineColor('green'); // 선 색상 설정
		flowTwoLine.setStrokeWidth(3); // 선 두께 설정
		flowTwoLine.setArrow(true); // 화살표 사용 여부 설정
		flowTwoLine.setArrowPosition('end'); // 화살표 위치 설정 (끝점)

		// AFlowTwoLine을 부모 레이아웃에 추가
		this.addComponent(flowTwoLine);

		// 화면 가운데 배치
		flowTwoLine.centerX();
		flowTwoLine.centerY();
	}
```

* 실행 화면

![](https://wikidocs.net/images/page/274098/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-18_155121.png)
