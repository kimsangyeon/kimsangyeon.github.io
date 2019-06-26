---
layout: post
title: "Javascript Event Bubbling Capturing"
categories: [ javascript, event ]
image: assets/images/banner/javascript.png
author: yeon
---

## Javascript Event Bubbling Capturing

Javascript에서 전파되는 이벤트를 간단히 정리해 볼까한다. 웹오피스 에디터 개발을 하며, 이벤트 후킹처리로 이벤트를 제품의 입맛에 맞게 동작하게 하는 일들을 많이 하였는데 알고있었던, 그리고 몰랐던 내용을 추가해보며 정리해본다. <br>

<br>

### On Event
일단 이벤트처리를 위해 이벤트 등록이 필요하다. keydown, keypress, keyup, input, click 등 .. <br>

이벤트 등록은 <br>

```javascript
const onClick = (e) => {
    console.log(e);
};
const elBtn = document.getElementById("btn");
elBtn.addEventListener("click", onClick);
``` 

간단하게 addEventListener를 통해 click Event를 등록하였다. Jquery를 사용한다면 on 메소드를 사용하여 손쉽게 등록 가능하다. <br>

<br><br>

### Event Bubbling
이벤트 버블링은 이벤트가 발생한 currentTarget에서 부모로 이벤트가 전달된다. <br>

```html
<html>
    <body>
        <div id="A">
            <div id="B">
                <div id="C"></div>
            </div>
        </div>
        <script type="text/javascript">
            const onClick = (e) => {
                console.log(e.currentTarget);
            };
            const elDivs = document.querySelectorAll('div');
            elDivs.forEach(elDiv => elDiv.addEventListener("click", onClick));

        </script>
    </body>
</html>
```

여기서 third Div를 클릭시 C -> B -> A 순으로 이벤트가 전달된다. <br>
B 클릭시 B -> A로 이벤트가 전파 <br>

<br><br>

### Event Capturing
이벤트 캡쳐링은 버블링과 반대로 부모에서 자식에게로 이벤트가 전달된다. <br>

```html
<html>
    <body>
        <div id="A">
            <div id="B">
                <div id="C"></div>
            </div>
        </div>
        <script type="text/javascript">
            const onClick = (e) => {
                console.log(e.currentTarget);
            };
            const elDivs = document.querySelectorAll('div');
            elDivs.forEach(elDiv => elDiv.addEventListener("click", onClick , {capture: true}));

        </script>
    </body>
</html>
```

캡쳐링 옵션은 addEventListener 세번째 인자로 설정 가능하며, 기본값은 false이다. <br>

<br><br>

### Event Block
이제 이벤트를 막는 방법에 대하 정리해본다. <br>
이벤트를 막는 방법은 여러개가 있지만 일단 기본 이벤트 동작을 막는 **preventDefault**가 있다. <br>

<br>

#### preventDefault
preventDefault는 현재 이벤트의 기본 동작을 막는다. 예로 <br>

```html
<html>
    <body>
        <input id="input" />
        <script type="text/javascript">
            const onKeydown = (e) => {
                e.preventDefault();
            };
            document.getElementById("input").addEventListener("keydown", onKeydown);
        </script>
    </body>
</html>
```

다음과 같이 input keydown 이벤트에 e.preventDefault()를 넣는다면 input에 입력을 할 수 없을 것이다. <br>

<br>

#### stopPropagation
stopPropagation은 이벤트가 부모로 전달 되는 것을 막아준다. 위에서 C -> B -> A 형태로 전파되던 bubbling 이벤트 전달을 막을 수 있다.<br>

<br>

#### stopImmediatePropagation
stopImmediatePropagation는 이벤트가 여러개 걸려있는 경우, 다른 이벤트는 호출되지 않게 막아준다. <br>

```html
<html>
    <body>
        <div id="A"></div>
        <script type="text/javascript">
            const onClickA = (e) => {
                e.stopImmediatePropagation();
                console.log("onClickA");
            };
            const onClickAA = (e) => {
                console.log("onClickAA");
            };
            const elDiv = document.getElementById('A');
            elDiv.addEventListener("click", onClickA);
            elDiv.addEventListener("click", onClickAA);
        </script>
    </body>
</html>
```

다음과 같이 elDiv에 click 이벤트에 onClickA와 onClickAA 등록되어 있는 경우, onClickA에서 stopImmediatePropagation가 호출된다면 onClickAA는 호출되지 않는다. <br>

<br><br><br>