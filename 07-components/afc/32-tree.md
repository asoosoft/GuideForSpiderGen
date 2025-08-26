# Tree

![](../../.gitbook/assets/스크린샷_2025-01-24_104143.png)

\
계층 구조를 시각적으로 표현하는 데 사용되는 컴포넌&#xD2B8;**.** 아이템을 추가하거나 삭제할 수 있으며, 특정 아이템을 선택하거나 선택 해제 가능.

### Example

**컴포넌트 생성**

* id값 myTreeId로 지정

<div align="left"><figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div>



* MainView.js 수정

```javascript
onInitDone() {
    super.onInitDone();

    const treeData = { 
        name: '메뉴', 
        sub: [ 
            { name: '홈' }, 
            { name: '나의정보', 
            sub: [
                { name: '회원수정' }, 
                { name: '회원탈퇴' }
                ] 
            } 
        ] 
    };

    this.insertTreeData(this.myTreeId, treeData);

}

insertTreeData(tree, data) { 
    const item = tree.insertItemObj(data, true); 
    if (data.sub) { 
        data.sub.forEach(subData => { 
            subData.pItem = item; 
            this.insertTreeData(tree, subData); 
        }); 
    } 
    return item; 
} 
```



**코드로 생성**

```javascript
onInitDone() {
    super.onInitDone();

    // 트리 컴포넌트 생성
    this.myTreeId = new ATree();
    this.myTreeId.init();
    this.addComponent(this.myTreeId);

    this.myTreeId.setSize("300px", "200px");
    this.myTreeId.setPos(20, 20);

    // 트리 데이터 삽입
    const treeData = {
        name: '메뉴',
        sub: [
            { name: '홈' },
            {
                name: '나의정보',
                sub: [
                    { name: '회원수정' },
                    { name: '회원탈퇴' }
                ]
            }
        ]
    };

    this.insertTreeData(this.myTreeId, treeData);
}

insertTreeData(tree, data) {
    const item = tree.insertItemObj(data, true);
    if (data.sub) {
        data.sub.forEach(subData => {
            subData.pItem = item;
            this.insertTreeData(tree, subData);
        });
    }
    return item;
}
```



* 프로젝트 실행

<div align="left"><figure><img src="../../.gitbook/assets/화면 녹화 중 2025-07-10 163332.gif" alt=""><figcaption></figcaption></figure></div>
