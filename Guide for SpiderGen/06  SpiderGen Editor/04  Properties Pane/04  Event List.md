# 04. Event List

**스파이더젠에서 제공하는 다양한 이벤트들은 사용자 인터페이스와의 상호작용을 처리하는 데 사용됩니다.**

**각 이벤트는 특정한 사용자 동작에 반응하여 호출되며, 개발자는 이를 통해 원하는 기능을 구현할 수 있습니다.**

![](../../../.gitbook/assets/view_events.png)\
⬅️ **View 컴포넌트의 이벤트**

***

![](../../../.gitbook/assets/btn_events.png)\
⬅️ **Button 컴포넌트의 이벤트**

***

**아래는 스파이더젠에서 사용되는 주요 이벤트들에 대한 설명입니다.**

#### 클릭 및 터치 이벤트

1.  **click(comp, info, e)**

    컴포넌트가 클릭될 때 호출됩니다. 주로 버튼 클릭과 같은 단일 클릭 동작을 처리합니다.

    ![](../../../.gitbook/assets/click2.gif)

    ***
2.  **dblclick(comp, info, e)**

    컴포넌트가 더블 클릭될 때 호출됩니다. 더블 클릭 시 특정 동작을 수행할 때 사용됩니다.

    ![](../../../.gitbook/assets/dbclick.gif)

    ***
3.  **longtab(comp, info, e)**

    컴포넌트가 길게 탭될 때 호출됩니다. 길게 누르는 동작을 인식하여 추가 옵션을 표시하거나 특정 기능을 활성화할 때 사용됩니다.

    ### ![](../../../.gitbook/assets/longtab.gif)
4.  **actiondown(comp, info, e)**

    터치나 마우스 클릭이 시작될 때 호출됩니다. 터치 시작 시의 초기 동작을 처리할 때 사용됩니다.

    ![](../../../.gitbook/assets/actionDown.gif)

    ***
5.  **actionmove(comp, info, e)**

    터치나 마우스가 이동할 때 호출됩니다. 드래그 동작을 처리하거나, 터치 이동에 따른 변화를 감지할 때 사용됩니다.

    ![](../../../.gitbook/assets/actionMove.gif)

    ***
6.  **actionup(comp, info, e)**

    터치나 마우스 클릭이 끝날 때 호출됩니다. 터치 종료 시의 동작을 처리할 때 사용됩니다.

    ### ![](../../../.gitbook/assets/actionUp.gif)
7.  **actioncancel(comp, info, e)**

    터치 동작이 취소될 때 호출됩니다. 터치가 중단되거나 취소될 때의 동작을 처리할 때 사용됩니다.

    ***
8.  **actionleave(comp, info, e)**

    터치나 마우스가 컴포넌트 영역을 벗어날 때 호출됩니다. 영역을 벗어날 때의 동작을 처리할 때 사용됩니다.

    ![](../../../.gitbook/assets/actionLeave.gif)

    ***

#### 스크롤 및 스와이프 이벤트

9.  **scroll(comp, info, e)**

    스크롤이 발생할 때 호출됩니다. 스크롤 위치에 따라 콘텐츠를 동적으로 로드하거나, 스크롤 상태를 업데이트할 때 사용됩니다.

    ![](../../../.gitbook/assets/scroll.gif)

    ***
10. **scrollleft(comp, info, e)**

스크롤이 왼쪽 끝에 도달할 때 호출됩니다. 스크롤이 더 이상 왼쪽으로 이동할 수 없을 때의 동작을 처리할 때 사용됩니다.

![](../../../.gitbook/assets/scrollLeft.gif)



11\. **scrollright(comp, info, e)**

스크롤이 오른쪽 끝에 도달할 때 호출됩니다. 스크롤이 더 이상 오른쪽으로 이동할 수 없을 때의 동작을 처리할 때 사용됩니다.



![](../../../.gitbook/assets/scrollRight.gif)

12\. **scrolltop(comp, info, e)**

스크롤이 상단에 도달할 때 호출됩니다. 스크롤이 더 이상 위로 이동할 수 없을 때의 동작을 처리할 때 사용됩니다.

![](../../../.gitbook/assets/scrollTop.gif)

13\. **scrollbottom(comp, info, e)**

스크롤이 바닥에 도달할 때 호출됩니다. 스크롤이 더 이상 아래로 이동할 수 없을 때의 동작을 처리할 때 사용됩니다.

![](../../../.gitbook/assets/scrollBottom.gif)

14\. **swipe(comp, info, e)**

스와이프 동작이 발생할 때 호출됩니다. 빠른 스와이프 제스처를 인식하여 페이지 전환이나 특정 동작을 수행할 때 사용됩니다.

![](../../../.gitbook/assets/swipe.gif)

***

#### 선택 및 키보드 이벤트

15. **select(comp, info, e)**

    데이터 그리드나 리스트에서 항목이 선택될 때 호출됩니다. 선택된 항목의 세부 정보를 표시하거나, 다른 컴포넌트에 데이터를 바인딩할 때 사용됩니다.

    ![](../../../.gitbook/assets/select.gif)



    ```
        alert('선택한 뷰: '  + info.innerText);
    ```

***

16. **keydown(comp, info, e)**

    키보드 키가 눌릴 때 호출됩니다. 특정 키 입력에 반응하여 동작을 수행할 때 사용됩니다.

    ![](../../../.gitbook/assets/keyDown.gif)



    ```
    	if (e.key == 'Enter') {
    		alert('엔터가 입력되었습니다.');
    	}
    ```

    ***
17. **keyup(comp, info, e)**

    키보드 키가 놓일 때 호출됩니다. 키 입력이 끝났을 때의 동작을 처리할 때 사용됩니다.

***

#### 변경 이벤트

18. **change(comp, info, e)**

    입력 값이 변경되었을 때의 동작을 처리할 때 사용됩니다.

    ![](../../../.gitbook/assets/change.gif)



    ```
        console.log(this.textfield.getText());
    ```

***

#### 포커스 및 블러 이벤트

19. **focus(comp, e)**

    컴포넌트가 포커스를 받을 때 호출됩니다. 포커스가 설정되었을 때의 동작을 처리할 때 사용됩니다.

    ![](../../../.gitbook/assets/focus.gif)

    ***
20. **blur(comp, e)**

    컴포넌트에서 포커스가 사라질 때 호출됩니다. 포커스가 해제되었을 때의 동작을 처리할 때 사용됩니다.

    ![](../../../.gitbook/assets/blur.gif)

***

#### 붙여넣기 이벤트

21. **paste(comp, e)**

    컴포넌트에 붙여넣기 동작이 발생할 때 호출됩니다. 붙여넣기 시의 동작을 처리할 때 사용됩니다.

    ![](../../../.gitbook/assets/paste.gif)

***
