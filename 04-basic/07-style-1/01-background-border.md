<style>
.flex {
  display : flex;
}
.fs20 {
	font-size : 20px;
}
.fs30 {
	font-size : 30px;
}
.wd300 {
  width : 300px;
  margin : auto;
}
.wd400 {
  width : 400px;
  margin : auto;
}
.wd500 {
  width : 500px;
  margin : auto;
}
.gradBtn{
  background-color : rgb(70,70,70);
  color : white;
  border : 1px solid rgba(255,255,255,0.5);
  border-radius : 5px;
}
.mgauto{
   margin : auto;
}
</style>



<img
class="wd300 flex" src="https://wikidocs.net/images/page/276197/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-13_171900.png">
 
<p style="text-align: center"> 
✅ 이 영역에서 디자인을 적용
</p>

<h1 class="fs30"> 1. Background 디자인 </h1>

## 💫 백그라운드 컬러 지정
 <img class="wd300 flex" src="https://wikidocs.net/images/page/276197/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-13_173102.png">
 
 <p style="text-align: center"> 
✅ 백그라운드 컬러를 지정한 모습
</p>

<p style="text-align: center; color:#337AB7;"> 
Background -> Color 에서 지정
</p>

> RGB값 및 16진수값을 직접 입력하거나, 사각형 버튼을 클릭 해 직접 색상을 선택 가능

 <img class="wd300 flex" src="https://wikidocs.net/images/page/276197/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-13_174134.png">
 
  <p style="text-align: center"> 
✅ 그라데이션 컬러를 지정한 모습
</p>

<p style="text-align: center; color:#337AB7;"> 
Background -> Image를 클릭하면  지정 가능
</p>

<div style="display: flex; flex-direction: column; width: 50%; margin: auto;">
<div class="flex">
    <button class="gradBtn">Line</button> - 직선  그라디언트 (Linear Gradient)

</div>
<div class="flex">
    <button class="gradBtn">Circle</button> - 원형 그라디언트 (Radial Gradient)
</div>
<div class="flex">
    <button class="gradBtn">Reverse</button> - 그라디언트 반전
</div>
</div>

## 💫 백그라운드 이미지 지정

 <img class="wd400 flex" src="https://wikidocs.net/images/page/276197/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-14_095325.png">
 
 <p style="text-align: center"> 
✅ 백그라운드 이미지를 지정한 모습
</p>

<p style="text-align: center; color:#337AB7;"> 
Background -> Image -> ... 버튼을 클릭해 지정 
 
</p>

> 1. 'show all' 을 클릭해 현재 프로젝트의 파일을 로드
> 
> 2. 파일을 선택 후 'OK' 버튼 클릭하여 적용

| Option 값 | 설명 | 유사한 CSS  |
|--|--|--|
| `original` | 이미지를 원래 크기 그대로 표시 | **background-size: auto;**|
|`fit` |이미지를 컴포넌트의 크기에 맞게 조정 (비율 유지됨) | **background-size: contain;**|
|`stretch` | 이미지를 컴포넌트의 크기에 맞게 조정 (비율 변경됨) |**background-size: 100% 100%;** |
|`custom` |사용자가 직접 이미지의 크기와 위치를 설정 |**background-size,** **background-position** 값  |


<h1 class="fs30"> 2. Border 디자인 </h1>

## 💫 테두리(Border) 지정

 <img class="wd400 flex" src="https://wikidocs.net/images/page/276197/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-14_104705.png">
 
 <p style="text-align: center"> 
✅ 테두리(Border)를 지정한 모습
</p>

<p style="text-align: center; color:#337AB7;"> 
'Border' 에서 지정
</p>

> 컴포넌트를 선택한 후 Appearance 속성 패널에서 'Border' 옵션을 설정. 여기서 테두리의 두께, 색상, 스타일, 모서리 반경을 지정하여 원하는 테두리 스타일을 적용

![](https://wikidocs.net/images/page/276197/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2025-02-14_104810.png)

 
| 값 | 예시 | 설명 | 
|--|--| --|
| `테두리 굵기` | 1px | 테두리의 두께를 설정 |
|`테두리 스타일` | solid | 테두리의 스타일을 설정 |
|`테두리 색` | black |테두리의 색상을 설정 |
|`테두리 둥글기(Round)` |5px|테두리의 둥길기 (border-radius) |
|`모든 테두리 적용(shorthand)` | | 체크 시 모든 테두리를 한번에 지정 가능.<br>체크 해제 시 각 테두리 별 지정 가능.|


<p style="text-align: center"> 
⬇️ 각 테두리 스타일 (border-style) 미리보기
</p>
<img class="mgauto flex" src="https://wikidocs.net/images/page/276197/html-and-css-border.png">
