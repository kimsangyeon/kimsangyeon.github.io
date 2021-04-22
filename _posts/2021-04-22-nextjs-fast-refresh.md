---
layout: post
title: 'Fast Refresh'
categories: [javascript, nextjs]
image: assets/images/banner/nextjs.jpeg
author: yeon
---

# Fast Refresh

Fast Refresh는 React 컴포넌트 편집에 대한 즉각적인 피드백을 제공하는 기능이다. Next.js 9.4 이상에서 기본적으로 활성화된다. 이는 편집 내용이 컴포넌트의 상태를 유지한채로 1초내에 표시된다. <br>

<br><br>

## How It Works

React 컴포넌트만 export 하는 파일을 편집하는 경우 Fast Refresh는 해당 파일에 대한 코드만 업데이트하고 컴포넌트를 랜더링한다. <br>

<br>

React 컴포넌트가 아닌 export 된 파일을 편집하는 경우 Fast Refresh는 해당 파일과 파일을 가져오는 다른 파일을 모두 다시 실행한다. 만약 Button.js와 Modal.js가  theme.js를 import 하고 있다면 두가지 파일 모두 업데이트 된다. <br>

<br>

React 트리 외부의 파일에서 가져온 파일을 편집하는 Fast Refresh는 전체 재로드를 수행한다. <br>

<br><br>

## Error Resilience

<br>

### Syntax Errors

개발중에 Syntax Error가 발생 했을때 이를 수정하고 파일을 저장할 경우 오류는 자동으로 사라지고 앱을 다시 로드할 필요가 없다. 이때 컴포넌트는 상태를 유지한채로 적용된다. <br>

<br>

### Runtime Errors

컴포넌트에서 런타임 오류를 한 경우 오버레이가 표시되고 오류를 수정시에 앱을 다시 로드하지않고도 자동으로 오버레이가 해제된다. <br>

랜더중 오류가 발생하지 않은 경우 컴포넌트 상태는 유지된다. <br>

<br><br>

## Limitations

Fast Refresh는 편집중 컴포넌트에서 로컬 React 상태를 유지하려고 하지만 이 경우는 안전한 경우에만 가능하다. <br>

- 클래스 컴포넌트는 로컬 상태가 유지되지 않는다. (함수컴포넌트와 훅인 경우에만 상태를 유지)
- 편집중인 파일에는 React 컴포넌트 외에 다른 export가 있을 수 있다.

<br><br>

## Tip

- Fast Refresh는 기본적으로 함수 컴포넌트 및 훅 사용인 경우에만 React 로컬 상태를 유지한다.
- 경우에 따라서 상태를 강제로 재설정하고 구성요소를 다시 마운트해야 할 수 있다. 마운트시 발생하는 애니메이션을 조정하는 경우 

<br>

편집중인 파일 내에 //@refresh reset 을 추가 할 수 있다. 해당 구문이 있는 파일을 편집 할 경우 다시 마운트하도록 빠른 새로 고침을 지시한다. <br>

<br><br>

## Fast Refresh and Hooks

Fast Refresh는 편집 사이의 컴포넌트의 상태를 유지하려고 한다. useState 및 useRef 인수 또는 Hook 호출 순서를 변경하지 않는 한 이전 상태값을 유지한다. <br>

<br>

useEffect, useMemo 및 useCallback과 값은 dependencies를 가지는 훅은 Fast Refresh 중에 업데이트된다. Fast Refresh 동안에는 dependencies는 무시된다. <br>

예를 들어 useMemo (() => x * 2, [x])를 useMemo (() => x * 10, [x])로 편집하면 x (종속성)가 그렇지 않더라도 다시 실행된다. <br>

<br><br>

[Ref]:

- [Next.js Docs Basic Features Fast Refresh](https://nextjs.org/docs/basic-features/fast-refresh)


<br><br><br>