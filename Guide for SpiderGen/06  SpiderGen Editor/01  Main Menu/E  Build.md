현재 프로젝트를 전체 또는 화면 단위별로 빌드하거나 동시에 실행 할 수 있는 메뉴 입니다.

## Run Project  

현재 프로젝트를 빌드 후 실행하는 메뉴 입니다.


![](https://wikidocs.net/images/page/22816/build01.png)
  
  
## Run Unit  

현재 활성화된 화면을 실행하는 메뉴 입니다. (해당 메뉴를 실행하기전 프로젝트가 빌드되어 있어야 함)
  
  
## Build Project  

현재 프로젝트를 빌드하는 메뉴 입니다. 빌드된 파일은 현재프로젝트/bin 폴더에 저장됩니다.  


## Build Unit  

현재 활성화된 화면을 빌드 합니다.  


## Current Build  

현재 활성화된 파일을 빌드합니다.  


## Current Build & Run  

현재 활성화된 파일을 빌드후 실행합니다.  

## Run As Browser

프로젝트를 웹 브라우저에서 실행하여 테스트할 수 있는 기능입니다.


## Open Build Folder

프로젝트의 빌드 결과물이 저장된 폴더를 쉽게 열 수 있도록 도와주는 기능입니다.

## Copy Build File

빌드된 프로젝트 파일을 다른 위치로 복사할 수 있도록 도와주는 기능입니다.

## Clean Project  

현재 프로젝트 빌드 파일을 삭제합니다.  

 
### Compress Project  

현재 빌드된 프로젝트 파일을 압축합니다. (해당 메뉴는 프로젝트 빌드후 사용합니다.)  


## Make Version Js

JavaScript 파일을 특정 버전으로 관리하기 위해 사용됩니다.

![](https://wikidocs.net/images/page/22816/build02.png)

### Update Index Version  

현재 프로젝트를 빌드후 생성되는 Index.html 버전을 관리하는 기능입니다.

![](https://wikidocs.net/images/page/22816/build03.png)


Index.html에는 프레임워크 관련 파일들(**.js**, **.html**, **.css**)이 링크됩니다.  
따라서 수정 사항이 발생한 프레임워크 파일들 버전관리가 필요 할 경우 해당 파일을 
우측 목록으로 이동시켜 빌드합니다. 

해당 기능은 웹앱의 경우 브라우저가 캐시를 사용하게 될 경우 수정된 프레임워크 파일을 새로이 
적용하기 위해 적합 합니다.