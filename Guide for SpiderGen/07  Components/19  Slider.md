
![](https://wikidocs.net/images/page/24861/slider.png) 

**슬라이더(ASlider)** 는 사용자가 값을 조정할 수 있는 슬라이더를 제공하는 컴포넌트입니다. <br />
>슬라이더는 주로 범위 내에서 값을 선택하거나 조정할 때 사용됩니다.<br />
> ASlider는 다양한 속성과 메서드를 통해 슬라이더의 동작과 외형을 제어할 수 있습니다.

## Attribute

![](https://wikidocs.net/images/page/24861/slider_Attribute.png)
#### **Data**

-   **Value**   
    슬라이더의 초기 값을 설정하는 속성입니다.<br />
    사용자가 슬라이더를 움직일 때 이 값이 변경됩니다.
    
-   **Min**   
    슬라이더의 최소값을 설정하는 속성입니다. <br />
    슬라이더가 가질 수 있는 가장 작은 값입니다.
	
  - **Max**<br />
      슬라이더의 최대값을 설정하는 속성입니다. <br />
      슬라이더가 가질 수 있는 가장 큰 값입니다.

  - **Step**<br />
      슬라이더의 이동 단위를 설정하는 속성입니다. <br />
      슬라이더를 움직일 때 이 단위로 값이 변경됩니다.


  
## Example
 
#### 1️⃣ 컴포넌트 배치

**layout 에 다음 내용을 참고해서 컴포넌트를 배치합니다.** 

| component	| id	|   text   	|  value |
| -------- | -------- | -------- | -------- |
| AProgress	| progress	|   |   |
| ASlider	| slider	| 	| value:25, min:0, max:100, step:5 |
| ALabel	| label|  현재값	| 	|   
 
 
![](https://wikidocs.net/images/page/24861/slider_ex.png) 
 
 
#### 2️⃣ 함수 추가

**슬라이더의 값을 표현하기 위해 사용자 함수를 추가합니다.** 
  
```javascript

setValue(val) 
{          
    this.label.setText(val); 
    this.progress.setValue(val); 
};  
 
```
 
 
#### 3️⃣ 이벤트 설정

**슬라이더에 Change 이벤트를 설정합니다.** 
 
```javascript
 
onSliderChange(comp, info, e) 
{ 
    // 위에서 만든 사용자 함수 호출 
    this.setValue(comp.getValue());     
 
}; 
 
``` 
 
 
#### 4️⃣ 실행

**F5 키로 프로젝트를 빌드하고 실행합니다.** 
* 슬라이더에 바를 움직여 값을 조정해 봅니다. 
* 조정된 값에 따라 프로그래스 바가 변경되는걸 확인합니다.    

![](https://wikidocs.net/images/page/24861/slider_ex_result.png) 
 
  
 