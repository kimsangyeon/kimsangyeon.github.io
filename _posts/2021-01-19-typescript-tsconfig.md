---
layout: post
title: 'Redux Thunk'
categories: [javascript, redux]
image: assets/images/banner/redux.png
author: yeon
---
# tsconfig

`tsconfig.json` 파일을 기점으로 Typescript 프로젝트가 설정된 옵션들로 컴파일된다. **tsc** 커멘드 입력시 상위 디렉토리 체인으로 `tsconfig.json` 파일을 탐색해 나간다. <br>

<br>

커맨드 옵션 -p 혹은 —project를 넣어 직접 `tsconfig.json`  설정도 가능하다. <br>

<br>

- tsconfig.json을 fs 역방향으로 탐색하여 컴파일 실행

> tsc

<br>

- 컴파일할 ts 파일 지정

> tsc index.ts

<br>

- 디렉토리 하위의 ts 파일을 컴파일

> tsc src/*.ts

<br>

- tsconfig.json 컴파일 설정으로 ts 파일을 컴파일

> tsc —project tsconfig.json src/*.ts

<br><br>

## compilerOptions

컴파일에 사용될 속성으로 생략시 컴파일 기본 값이 사용된다.

- [컴파일러 옵션](https://typescript-kr.github.io/pages/compiler-options.html)

<br>

| Key | Description | Ex |
|:---:|:---:|:---:|
| 기본 옵션 | |  | |  |
| target | ECMAScript 대상 버전 설정 | es6 |
| module | 빌드 결과의 모듈 방식 | commonjs |
| lib | 컴파일에 포함될 라이브러리 지정 | ["es6", "dom"] |
| allowJs | .js 파일도 컴파일 대상에 포함 | true |
| checkJs | .js 파일의 오류 보고 | true |
| jsx | .tsx 파일에서 JSX 코드를 지원 | 'preserve' 'react' 'react-native' |
| outDir | 빌드 결과물이 위치할 폴더 | build/dist |
| sourceMap |  bundle 결과물의 .map.js 함께 생성 | true |
| ... |  |  |
| 엄격한 유형 검사 옵션 |  |  |
| strict | 엄격한 유형 검사 옵션 활성화 | true |
| strictNullChecks | 엄격한 null 검사를 활성화 | true |
| noImplictAny | any 표현식 선언에서 오류 발생 | true |
| ... |  |  |
| 모듈 확인 옵션 |  |  |
| typeRoots | 유형 정의를 포함 할 폴더 목록 | ["./typings"] |
| types | 컴파일에 포함될 유형 선언 파일 | ["node", "lodash", "express"] |

<br><br>

### typesRoots & types

기본적으로 유형 정의에 대한 `@types` 패키지는 컴파일에 모두 포함된다. `typeRoots`를 지정할 경우 지정된 타입 정의만이 포함된다. <br>

아래의 경우 `typings`  아래의 패키지만 포함된다. (`./node_modules/@types`)가 포함되지 않음 <br>

```json
{
   "compilerOptions": {
       "typeRoots" : ["./typings"]
   }
}
```

<br><br>

`types`를 지정하면 해당 패키지만 컴파일 목록에 포함된다. <br>

아래와 같이 지정할 경우 . `./node_modules/@types/node`, `./node_modules/@types/lodash` , `./node_modules/@types/express` 가 포함된다. <br>

```json
{
   "compilerOptions": {
       "types" : ["node", "lodash", "express"]
   }
}
```

<br>

`types` 패키지는 `index.d.ts` 파일이 있는 폴더 또는 폴더에 `types` 필드를 가진 `package.json` 이 있는 폴더이다. <br>

<br><br>

## files

컴파일할 파일의 상태 또는 절대 파일 경로 목록을 가진다.

<br>

## include

컴파일에 포함되는 파일 경로 목록을 가진다.

<br>

## exclude

컴파일에서 제외할 파일 경로 목록을 가진다.

<br>

`files`, `include`, `exclude` 는 서로 상관관계를 가지며, `include` 는 `exclude` 에 포함되지 않는 파일만을 포함한다. (`exclude` 로 `include` 목록에 포함된 파일을 필터)

명시적으로 파일을 지정하는 `files` 에 지정된 파일들은 `exclude` 로 제외되지 않는다. <br>

`exclude` 를 지정하지 않는다면 기본적으로 `node_module`, `bower_components`,   `jspm_packages` 와 `<outDir>` 을 제외한다. <br>

<br><br>

## extends

`tsconfig.json` 에서 `extends` 는 다른 파일의 설정을 상속 받을 수 있도록 해준다. 기존 파일의 설정이 먼저 로드된 이후에 상속되는 설정 파일을 가져와 재정의 한다. <br>

<br>

상속파일의 `files` , `include` , `exclude` 는 기본 설정을 덮어쓴다. 설정파일의 모든 상대적 경로는 경로가 원래 있던 설정 파일 기준으로 해석된다. <br>

<br>

- **configs/base.json**

```json
{
  "compilerOptions": {
    "noImplicitAny": true,
    "strictNullChecks": true
  }
}
```

<br>

- **tsconfig.json**

```json
{
  "extends": "./configs/base",
  "files": [
    "main.ts",
    "supplemental.ts"
  ]
}
```

<br><br>

## complieOnSave

해당 속성은 `IDE` 에서 소스 저장 시 컴파일 해야하는 경우 지정된 `tsconfig.json` 에 대한 컴파일을 컴파일러에게 알려준다.

<br><br>

[Ref] :

- [tsconfig.json](https://typescript-kr.github.io/pages/tsconfig.json.html)


<br><br><br>