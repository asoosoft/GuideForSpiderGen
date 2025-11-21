# File Uploader

![](../../.gitbook/assets/fu.png)

**파일 업로더(AFileUploader)** 는 사용자가 파일을 업로드할 수 있도록 지원하는 컴포넌트입니다.<br>

> 파일업로더는 파일 선택, 업로드, 다중 파일 첨부 등의 기능을 제공하여 사용자로부터 파일을 수집하고 서버로 전송하는 작업을 쉽게 처리할 수 있도록 도와줍니다.

### Attribute

![](../../.gitbook/assets/fu_Attribute_re.png)

**1️⃣ Info**

* **Load Url**\
  파일 업로드 요청을 처리할 서버의 URL을 설정합니다.\
  이 URL은 사용자가 파일을 업로드할 때 요청이 전송되는 서버의 주소를 나타냅니다.

***

**2️⃣ Option**

* **Accept Type**\
  사용자가 선택할 수 있는 파일의 유형을 지정합니다.\
  이 속성을 설정하면 파일 선택 대화상자에서 지정된 유형의 파일만 표시됩니다.
  * **`All Files`**: 모든 파일을 허용합니다.
  *   **`Image Files`**: 모든 이미지 파일을 허용합니다.

      > Accept Type 선택박스 밑에 따로 허용하는 이미지 파일 형식을 적어 파일 형식 별로 허용할 수 있습니다.
  * **`Text Files`**: 텍스트 파일만 허용합니다.
  * **`HTML Files`**: HTML 파일만 허용합니다.
  * **`Video Files`**: 모든 비디오 파일을 허용합니다.
  * **`Audio Files`**: 모든 오디오 파일을 허용합니다.

### Example

FileUploader 컴포넌트는 사용자로부터 파일을 수집하고 서버로 전송하는 작업을 간편하게 처리할 수 있도록 설계되었습니다.<br>

사용자는 파일을 선택하거나 드래그 앤 드롭으로 파일을 추가할 수 있으며, 설정에 따라 다중 파일 첨부도 가능합니다.

> 예를 들어, 이미지 업로드, 문서 제출, 파일 첨부 기능 등 다양한 상황에서 활용될 수 있습니다.

```javascript

// Attribute의 Load Url과 같은 동작
this.fileUploader.setUrl('http://example.com/upload');

// Attribute의 Accept Type과 같은 동작
this.fileUploader.setUrl('image/*');

// drag & drop 기능 추가
this.fileUploader.setDragdrop(true)

// 다중 첨부 가능
this.fileUploader.setMultiple(true)

```

***

**1️⃣ 컴포넌트 생성**<br>

**FileUploader 컴포넌트 생성 및 Button 컴포넌트를 생성합니다.**

![](../../.gitbook/assets/fu_ex.png)

**2️⃣ ID 지정 및 이벤트**<br>

**FileUploader 컴포넌트에 ID 지정 및 Button 컴포넌트에 클릭이벤트를 생성합니다.**

**3️⃣ 함수 작성**<br>

**클릭이벤트 함수에 다음과 같이 작성합니다.**

```javascript

onFileReadClick(comp, info, e)
{
	// 파일정보 가져오기
	const fileInfo = this.fileUploaderID.getFilesInfo();
	
	if (fileInfo && fileInfo.length > 0) {
		let file = fileInfo[0];
	
		// 파일 읽기
		const reader = new FileReader();
		reader.onload = function(event) {
			let fileContent = event.target.result;

			// 콘솔창으로 파일 내용 확인
			console.log(fileContent);
		}
		reader.readAsText(file);
	}
}

```

**4️⃣ 결과**

**FileUploader 컴포넌트를 통해 파일을 올린 후 결과를 확인합니다.**

![](../../.gitbook/assets/fu_ex_result.png)
