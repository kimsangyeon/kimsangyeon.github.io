---
layout: post
title: 'Javascript Drag & Drop Elements'
categories: [javascript]
image: assets/images/banner/javascript.png
author: yeon
---

# Javascript Drag & Drop Elements

Javascript App에서 **Drag and Drop** 기능을 추가하기위한 많은 Library들이 존재합니다. 하지만 HTML에서 DOM 요소를 **Drag and Drop** 할 수 있도록 도와주는 기본 내장 API가 존재합니다. 여기서 **HTML Drag and Drop API**와 **Vanilla Javascript**를 사용하여 간단한 DOM Drag and Drop 기능을 구현해보겠습니다. <br>

<br>

HTML drag and drop API는 DOM의 이벤트 모델을 사용하여 해당 요소를 끌어서 놓기가 가능하도록 도와줍니다. 이는 CSS 스타일을 업데이트 한다던지, 요소를 이동시키는 대신 복사하여 요소를 복제하는 것도 가능하게 합니다. <br>

<br>x

## Making HTML Elements Draggable

먼저 **Drag** 항목부터 정리하겠습니다. 하나의 컨네이너안에 두가지 하위 요소를 만들어 보겠습니다. 끌어놓을 항목을 **draggable**로 만들고 끌어놓았던 항목을 넣을 곳을 **dropzone**이라고 만들겠습니다.

```html
<div class='parent'>
  <span id='draggableSpan'>
    draggable
  </span>
  <span> dropzone </span>
</div>
```

위처럼 HTML DOM만 생성시 span 영역의 draggable은 Drag 하지못합니다. drag가 가능하게 하기위해 `draggable = 'true'`속성을 설정해 주어야합니다. <br>

<br>

```html
<div class='parent'>
  <span id='draggableSpan' draggable='true'>
    draggable
  </span>
  <span> dropzone </span>
</div>
```

`draggable = 'true'` 속성을 설정시 span draggable이 drag가 가능한 것을 체험할 수 있을 것입니다. `draggable attribute` 기본값은 auto이며 브라우저 기본 설정에 따라 결정됩니다. 예를 들어 `( <a> )` 태그는 기본적으로 drag가 가능합니다. <br>

<br><br>

## Creating Drag and Drop Event Handlers

Making HTML Elements Draggable 예제로는 drag는 되지만 이후 동작에 대한 처리가 없어 큰 도움이 되지 않는 drag 동작입니다. **Drag and Drop API**를 사용하여 3가지 이벤트에 대해 처리하여 사용해 봅시다. <br>

<br>

처리할 3가지 이벤트
- ondragstart
- ondragover
- ondrop

<br>

[HTML Drag and Drop Event](https://developer.mozilla.org/ko/docs/Web/API/HTML_%EB%93%9C%EB%9E%98%EA%B7%B8_%EC%95%A4_%EB%93%9C%EB%A1%AD_API)는 8개가 존재하며 [DragEvent](https://developer.mozilla.org/ko/docs/Web/API/DragEvent), [DataTransfer](https://developer.mozilla.org/ko/docs/Web/API/DataTransfer), DataTransferItem, DataTransferItemList 인터페이스를 사용하여 Drag and Drop API를 운용하는데 도움을 줍니다.

~~~
참고: DragEvent and DataTransfer는 여러 데스크탑 브라우저에서 폭넓게 지원하고 있습니다. 하지만 DataTransferItem와 DataTransferItemList는 제한적으로 사용 가능합니다. 드래그 앤 드롭의 상호 운용성에 대한 더 많은 정보를 찾아보기 위해 Interoperability를 보십시오.
~~~

<br>

### Updating Our Element on Drag

처음 시작으로 `ondragstart`를 보겠습니다. 이는 drag 시작시 발생하는 이벤트로 CSS를 갱신하거나 DOM event를 통해 다른 요소에 접근하여 갱신할 수도 있습니다. <br>
`ondragstart`에서  `dataTransfer` 객체의 `setData` 속성을 사용하여 필요한 상태 정보를 설정할 수 있습니다. 두개의 매개변수를 사용하며 전송되는 format과 데이터를 설정합니다.

```javascript
  function onDragStart(event) {
    event.dataTransfer.setData('text/plain', event.target.id);
  }
```

<br>

우리의 목표는 drag 한 요소를 새로운 부모로 옮기는 것으로 event target id로 drag 된 요소를 기억하여 사용할 수 있도록 합니다. 또한 drag 중인 요소의 CSS를 변경하는 것도 가능합니다.

```javascript
  function onDragStart(event) {
    event.dataTransfer.setData('text/plan', event.target.id);
    event.currentTarget.style.backgroundColor = 'yellow';
  }
```

<br>

위 처럼 작성한 함수를 drag 할 DOM Element에 설정합니다.

```html
<div class='parent'>
  <span id='draggableSpan'
    draggable='true'
    ondragstart='onDragStart(event)'>
    draggable
  </span>
  <span> dropzone </span>
</div>
```

해당 영역들을 동작시 draggable 요소를 drag시 background color가 yellow로 변경되어 drag 되는 것을 확인 할 수 있을 것입니다. <br>

<br>

### Allowing Droppable Elements

브라우저에서는 기본적으로 drop 동작에 대해 방지되고 있어 drop 동작을 방지 하지 못하도록 `ondragover`에서 처리가 필요합니다.

```javascript
  function onDragOver(event) {
    event.preventDefault();
  }
```

<br>

`ondragover`는 브라우저가 drop 동작을 방지하는 것을 막아주는 역할만 하며 dropzone 영역에 `ondragover`를 설정합니다.

```html
<div class='parent'>
  <span id='draggableSpan'
    draggable='true'
    ondragstart='onDragStart(event)'>
    draggable
  </span>
  <span ondragover='onDragOver(event)'>
   dropzone 
  </span>
</div>
```

<br<br>

### What To Do On Drop

마지막으로 `ondrop` 설정을 하도록 하겠습니다. `ondrop`에서는 `ondragstart`에서 기억하고 있던 dataTransfer에 저장된 id data를 기반으로 DOM Element를 가져와 컨트롤하는 작업이 필요합니다.

```javascript
  function onDrop(event) {
    const id = event.dataTransfer.getData('text');
    const elDraggable = document.getElementById(id);
    const elDropzone = event.target;

    elDropzone.appendChild(elDraggable);
    
    event.dataTransfer.clearData();
  }
```

`event.dataTransfer.getData`를 사용하여 저장하였던 id 정보를 기반으로 span draggable을 가져와 span dropzone 자식으로 넣는 동작을 추가합니다. <br>

<br>

HTML Element에 `ondrop`을 설정 후 정상적으로 drop 되어 appendChild 되는지 확인해봅니다.

```html
<div class='parent'>
  <span id='draggableSpan'
    draggable='true'
    ondragstart='onDragStart(event)'>
      draggable
  </span>

  <span
    ondragover='onDragOver(event)'
    ondrop='onDrop(event)'>
      dropzone
  </span>
</div>
```

<br><br>

[참고: Drag & Drop Elements with Vanilla JavaScript and HTML](https://alligator.io/js/drag-and-drop-vanilla-js/?fbclid=IwAR1a1dWzwxf_XbcnxSHL5f8eP4xtI-oeLMEZStafKQemgMtmBWocpCHNAQ8)



<br><br><br>
