---
layout: post
title: 'Next.js Data Fetching'
categories: [javascript, nextjs]
image: assets/images/banner/nextjs.jpeg
author: yeon
---

# Next.js Data Fetching

> Data Fetching에 대한 내용은 version 9.3 이상용으로 작성합니다.

<br>

`Next.js`에서 사전랜더링을 위해 데이터를 가져올 수 있는 세가지 함수가 있다. <br>

- getStaticProps (Static Generation) : 빌드시 데이터를 가져온다.
- getStaticPaths (Static Generation) : 데이터를 기반으로 사전 랜더링할 동적 경로를 지정한다.
- getServerSideProps (Server Side Rendering) : 각 요청에서 데이터를 가져온다.

<br><br>

## getStaticProps (Static Generation)

`Next`는 빌드시 getStaticProps라는 비동기 함수를 통해 페이지에 사용할 데이터를 가져옵니다. <br>

```jsx
export async function getStaticProps(context) {
  return {
    props: {}, // will be passed to the page component as props
  };
}
```

getStaticProps에서 사용하는 `context`는 동적 라우팅을 위한 params, 미리보기 정보 그리고 locale 정보를 가진다. <br>

<br><br>

### parameter

- params : 동적 경로를 사용하는 페이지에 대한 매개변수를 포함한다. 만약 페이지가 **[id].js** 형태라면 {id: ...} 다음과 같은 값을 가진다.
- preview : 페이지 미리보기 모드가 있다면 true
- previewData : setPreviewData에 의해 설정된 미리보기 데이터
- locale : 활성화된 locale 정보
- locales : 모든 locale 정보
- defaultLocale : 기본 locale 정보

<br>

### return

- props : 페이지에서 받을 props 정보. (직렬화된 객체)
- revelidate : 페이지 재생성이 발생할 수 있는 시간.
- notFound : 404 상태 반환여부 (fallback false인 경우에는 불필요)
- redirect : 내부 및 외부 리소스로 리다이렉션 할 수 있는지 여부

<br>

#### notFound

```jsx
export async function getStaticProps(context) {
  const res = await fetch(`https://.../data`);
  const data = await res.json();

  if (!data) {
    return {
      notFound: true,
    };
  }

  return {
    props: { data }, // will be passed to the page component as props
  };
}
```

<br><br>

#### redirect

```jsx
export async function getStaticProps(context) {
  const res = await fetch(`https://...`);
  const data = await res.json();

  if (!data) {
    return {
      redirect: {
        destination: '/',
        permanent: false,
      },
    };
  }

  return {
    props: { data }, // will be passed to the page component as props
  };
}
```

<br><br>

### Simple Example

`getStaticProps`를 사용하여 블로그 게시물 목록을 가져와보자.

```jsx
// posts will be populated at build time by getStaticProps()
function Blog({ posts }) {
  return (
    <ul>
      {posts.map((post) => (
        <li>{post.title}</li>
      ))}
    </ul>
  );
}

// This function gets called at build time on server-side.
// It won't be called on client-side, so you can even do
// direct database queries. See the "Technical details" section.
export async function getStaticProps() {
  // Call an external API endpoint to get posts.
  // You can use any data fetching library
  const res = await fetch('https://.../posts');
  const posts = await res.json();

  // By returning { props: { posts } }, the Blog component
  // will receive `posts` as a prop at build time
  return {
    props: {
      posts,
    },
  };
}

export default Blog;
```

<br><br>

### When should I use getStaticProps?

- 사전랜더링으로 `SEO`에 최적화 되어야하고 CDN에 의해 캐시 될 수 있는 HTML 및 JSON 파일을 생성한다.

<br><br>

### Typescript: Use GetStaticProps

타입스크립트 사용시 `GetStaticProps`를 사용하여 타입 지정이 가능하다.

```jsx
import { GetStaticProps } from 'next';

export const getStaticProps: GetStaticProps = async (context) => {
  // ...
}
```

<br>

리액트 컴포넌트에서 추론된 타입을 얻을려면 `inferGetStaticPropsType <typeof getStaticProps>`를 사용할 수 있다.

```jsx
import { InferGetStaticPropsType } from 'next';

function Blog({ posts }: InferGetStaticPropsType<typeof getStaticProps>) {
  // will resolve posts to type Post[]
}

export default Blog;
```

<br>

getStaticProps를 사용하면 정적 컨텐츠도 동적일 수 있다. `Incremental Static Regeneration`을 사용하면 트래픽이 들어올때 백그라운드에서 다시 랜더링을 수행하여 페이지를 업데이트 할 수 있다. <br>

```jsx
function Blog({ posts }) {
  return (
    <ul>
      {posts.map((post) => (
        <li>{post.title}</li>
      ))}
    </ul>
  )
}

// This function gets called at build time on server-side.
// It may be called again, on a serverless function, if
// revalidation is enabled and a new request comes in
export async function getStaticProps() {
  const res = await fetch('https://.../posts')
  const posts = await res.json()

  return {
    props: {
      posts,
    },
    // Next.js will attempt to re-generate the page:
    // - When a request comes in
    // - At most once every second
    revalidate: 1, // In seconds
  }
}

export default Blog
```

<br>

`revalidate` 설정으로 1초마다 재검증이 이루어져 새로운 게시물이 추가되더라도 다시 빌드하거나 배포할 필요없이 즉시 사용할 수 있다. 이 동작은 fallback: true 설정과 완벽하게 상호작용하며 항상 최신 게시물로 업데이트되는 게시물 목록을 가질 수 있다. <br>

<br><br>

### Static content at scale

`Incremental Static Regeneration` 증분 정적 재생의 이점

- 페이지가 지속적으로 빠르게 제공되며 지연 시간이 급증하지 않는다.
- 데이터베이스와 백엔드 동작 수행이 빈번하지 않다.

<br><br>

### Reading files: Use process.cwd()

getStaticProps에서 파일시스템 파일을 직접 읽을 수 있다. `__dirname`를 사용할 수 없지만 `process.cwd()`를 사용할 수 있다. <br>

```jsx
// This function gets called at build time on server-side.
// It won't be called on client-side, so you can even do
// direct database queries. See the "Technical details" section.
export async function getStaticProps() {
  const postsDirectory = path.join(process.cwd(), 'posts')
  const filenames = await fs.readdir(postsDirectory)

  const posts = filenames.map(async (filename) => {
    const filePath = path.join(postsDirectory, filename)
    const fileContents = await fs.readFile(filePath, 'utf8')

    // Generally you would parse/transform the contents
    // For example you can transform markdown to HTML here

    return {
      filename,
      content: fileContents,
    }
  })
  // By returning { props: { posts } }, the Blog component
  // will receive `posts` as a prop at build time
  return {
    props: {
      posts: await Promise.all(posts),
    },
  }
}
```

<br><br>

### Technical details

#### only runs at build time

`getStaticProps`는 빌드시 실행되기 때문에 HTML을 생성할때 HTTP헤더와 같이 요청시에만 사용할 수 있는 데이터를 수신하지 않는다. <br>

<br><br>

#### Write server-side code directly

`getStaticProps`는 서버에서만 실행되고 클라이언트에서는 실행되지 않는다. 해당 코드는 브라우저용 JS 번들에도 포함되지 않기 때문에 직접 데이터베이스 쿼리와 같은 코드를 작성 할 수 있다. 서버측 코드를 직접 작성 할 수 있지만 브라우저용 document 등의 DOM API는 사용 할 수 없다. <br>

- 해당 [tool](https://next-code-elimination.vercel.app/)을 사용하여 클라이언트 번들에서 코드를 제거한다

<br><br>

#### Statically Generates both HTML and JSON

`getStaticProps`가 포함된 페이지가 빌드시 미리 렌더링되면 HTML 파일 외에 `Next.js`는 getStaticProps 실행 결과를 보관하는 JSON 파일을 생성한다. <br>

<br>

생성된  JSON 파일은 `next/js`와 `next/router`에 사용된다.  `Next.js`는 빌드시 생성된 JSON 파일을 컴포넌트의 props로 사용하게 된다. <br>

<br><br>

#### Only allowed in a page

`getStaticProps`는 페이지에서만 export로 사용이 가능하다. 페이지가 랜더링되기 전에 페이지 랜더링에 필요한 데이터가 이미 완료되어야 하기 때문이다. <br>

<br>

또한 `export async function getStaticProps() {}` 해당 형태로만 사용이 가능하며 페이지 컴포넌트의 property로써는 동작하지 않는다. <br>

<br>

#### Runs on every request in development

개발 모드인 경우에는 모든 요청에 대해서 `geStaticProps`가 호출된다. <br>

<br><br>

#### Preview Mode

`getStaticProps`는 일반적으로 빌드 시간에 정적 생성되지만 이를 무시하고 요청시간에 페이지를 랜더링 할 수도 있다. 이러한 케이스를 [Preview Mode](https://nextjs.org/docs/advanced-features/preview-mode) 미리보기 모드라고한다. <br>

<br><br>

## getStaticPaths (Static Generation)

동적 경로를 사용하는 페이지에서 `getStaticPaths` 비동기 함수를 내 보내면 `Next.js`는 `getStaticPaths`에서 지정한 모든 경로를 정적으로 사전 랜더링한다. <br>

```jsx
export async function getStaticPaths() {
  return {
    paths: [
      { params: { ... } } // See the "paths" section below
    ],
    fallback: true or false // See the "fallback" section below
  };
}
```

<br><br>

### The paths key (required)

paths키는 미리 랜더링할 경로를 결정한다. 만약 `pages/posts/[id].js`라는 동적 경로를 사용하는 페이지가 있는 경우 getStaticPaths를 export한 경로에 대해 아래 처럼 반환 할 경우 `posts/1` 과 `posts/2` 페이지를 정적으로 생성한다. <br>

```jsx
return {
  paths: [
    { params: { id: '1' } },
    { params: { id: '2' } }
  ],
  fallback: ...
}
```

<br>

각 `params`값은 페이지 이름에 사용된 매개 변수와 일치해야한다. <br>

<br><br>

### The fallback key (required)

- fallback (false) : 인 경우 `getStaticPaths`가 반환하지 않는 모든 경로는 404페이지이다. 사전 랜더링할 경로가 적은 경우와 새 페이지가 자주 추가 되지 않는 경우 유용합니다. 데이터 항목이 추가되고 새 페이지를 랜더링 해야하는 경우 빌드를 다시 해야한다.

- fallback (true) : 인 경우 `getStaticProps`의 동작이 변경된다. 일단 `getStaticPaths`에서 반환된 paths 경로는 모두 빌드시 `getStaticProps`를 거쳐 사전 랜더링된다. 빌드시 생성되지 않는 경로에서는 404페이지로 연결되지 않는다. 백그라운드에서 `Next.js`는 요청된 경로 HTML과 JSON을 정적으로 생성하고 여기에 `getStaticProps` 실행이 포함된다. 해당 생성이 완성되면 브라우저는 생성된 경로에 대한 JSON을 수신하고 페이지를 자동으로 랜더링하는데 사용한다. 동시에 `Next.js`는 경로를 사전 랜더링 페이지 목록에 추가한다. 후에 이루어지는 요청에서는 빌드시 사전랜더링된 페이지와 마찬가지로 동일하게 페이지를 제공한다.

<br><br>

### Fallback pages

라우터를 사용하면 fallback 랜더링 여부를 감지 할수 있으며 router.isFallback으로 확인 가능하다.

```jsx
// pages/posts/[id].js
import { useRouter } from 'next/router'

function Post({ post }) {
  const router = useRouter()

  // If the page is not yet generated, this will be displayed
  // initially until getStaticProps() finishes running
  if (router.isFallback) {
    return <div>Loading...</div>
  }

  // Render post...
}

// This function gets called at build time
export async function getStaticPaths() {
  return {
    // Only `/posts/1` and `/posts/2` are generated at build time
    paths: [{ params: { id: '1' } }, { params: { id: '2' } }],
    // Enable statically generating additional pages
    // For example: `/posts/3`
    fallback: true,
  }
}

// This also gets called at build time
export async function getStaticProps({ params }) {
  // params contains the post `id`.
  // If the route is like /posts/1, then params.id is 1
  const res = await fetch(`https://.../posts/${params.id}`)
  const post = await res.json()

  // Pass post data to the page via props
  return {
    props: { post },
    // Re-generate the post at most once per second
    // if a request comes in
    revalidate: 1,
  }
}

export default Post
```

<br><br>

### when is fallback: true useful?

빌드시 생성해야하는 정적 페이지가 많은 경우 빌드하는데 시간이 오래 걸리게 된다. 이때 작은단위로 일부 페이지만 정적으로 생성하고 나머지는 fallback: true를 사용하여 생성한다. 누군가 아직 생성되지 않은 페이지를 요청하게되면 `getStaticProps`가 완료되고 요청된 페이지가 랜더링된다. 이후 동일한 페이지를 요청한 사람은 정적으로 생성된 사전 랜더링된 페이지를 받게된다. <br>

<br>

fallback: true로 생성된 페이지는 업데이트 되지 않는다. <br>

<br><br>

#### fallback: blocking

fallback: blocking인 경우 `getStaticPaths`에서 반환하지 않은 경로는 SSR과 동일한 HTML이 생성되기를 기다린다. 요청에 대해서는 캐시되므로 경로당 한번만 발생한다. <br>

<br>

paths에 설덩된 경로의 페이지는 빌드시 생성된다. <br>

<br>

빌드시 생성되지 않은 경로는 404페이지가 되지 않는다. `Next.js`에서 첫번째 요청에서 SSR을 수앻아고 생성된 HTML을 반환한다. <br>

<br>

브라우저는 생성된 경로에 대한 HTML을 수신한다. 동시에 Next.js는 경로를 사전랜더링 페이지 목록에 추가하고 동일한 경로의 요청은 빌드시 사전랜더링된 페이지와 동일하게 페이지를 제공한다. <br>

<br><br>

### when should I use getStaticPaths?

동적 경로를 사용하는 페이지를 정적으로 사전랜더링 해야하는 경우 `getStaticPaths`를 사용해야한다. <br>

<br><br>

### TypeScript: Use GetStaticPaths

```jsx
import { GetStaticPaths } from 'next'

export const getStaticPaths: GetStaticPaths = async () => {
  // ...
}
```

<br><br>

### Technical details

동적 경로 매개 변수가 있는 페이지에서 `getStaticProps`를 사용하는 경우 `getStaticPaths`를 사용해야한다. <br>

<br><br>

#### Only runs at build time on server-side

서버측에서 빌드시에만 실행된다. <br>

<br><br>

#### Only allowed in a page

`getStaticPaths`는 페이지에서만 export 할 수 있다. 페이지가 아닌 파일에서는 내보낼 수 없다. <br>

<br><br>

#### Runs on every request in development

개발 모드인 경우에는 모든 요청에 대해서 `geStaticPaths`가 호출된다. <br>

<br><br>

## getServerSideProps (Server-Side-Rendering)

페이지에서 `getServerSideProps` 비동기 함수를 export 하면 `Next.js`는 `getServerSideProps`에서 반환된 데이터를 사용하여 각 요청에 대하여 페이지를 미리 랜더링한다. <br>

```jsx
export async function getServerSideProps(context) {
  return {
    props: {}, // will be passed to the page component as props
  }
}
```

<br><br>

### parameter

- params : 페이지가 동적 경로를 사용하는 경우, 경로 매개 변수가 포함된다.
- req : HTTP request object
- res : HTTP response object
- query : query string
- preview : 미리보기 모드라면 true / false
- previewData
- resolvedUrl : query 값을 포함하는 요청 URL의 정규화된 버
- locale : 활성화된 locale 정보
- locales : 모든 locale 정보
- defaultLocale : 기본 locale 정보

<br><br>

### return

- props : 페이지 컴포넌트에서 받을 props, 직렬화 가능한 객체
- notFound : 페이지가 404 페이지를 허용하는 값 true / false
- redirect : 내부 및 외부 리소스로 리다이렉션 할 수 있는 옵션

```jsx
export async function getServerSideProps(context) {
  const res = await fetch(`https://...`)
  const data = await res.json()

  if (!data) {
    return {
      notFound: true,
    }
  }

  return {
    props: {}, // will be passed to the page component as props
  }
}
```

<br><br>

### Simple example

```jsx
function Page({ data }) {
  // Render data...
}

// This gets called on every request
export async function getServerSideProps() {
  // Fetch data from external API
  const res = await fetch(`https://.../data`)
  const data = await res.json()

  // Pass data to the page via props
  return { props: { data } }
}

export default Page
```

<br><br>

### When should I use getServerSideProps?

요청하여 데이터를 가져와 페이지를 사전 랜더링해야하는 경우에 `getServerSideProps`를 사용한다. <br>

<br>

서버가 모든 요청에 대해 결과를 계산하고 CDN에 의해 캐시 할 수 없기 때문에 `getStaticProps`보다는 느리다. <br>

<br><br>

### TypeScript: Use GetServerSideProps

```jsx
import { GetServerSideProps } from 'next'

export const getServerSideProps: GetServerSideProps = async (context) => {
  // ...
}
```

<br><br>

### Technical details

<br>

#### Only runs on server-side

`getServerSideProps`는 서버 측에서만 실행되며 브라우저에서는 실행되지 않는다. <br>

<br>

페이지를 요청하게 되는 경우 `getServerSideProps`가 실행되고 반횐된 props로 페이지가 사전 랜더링된다. <br>

<br><br>

#### Only allowed in a page

`getServerSideProps`는 페이지에서만 export 가능하다. <br>

<br><br>

## Fetching data on the client side

페이지에 자주 업데이트되는 데이터가 포함되어있고 데이터를 사전에 랜더링 할 필요가 없는 경우 클라이언트 측에서 데이터를 가져올 수 있다. <br>

<br>

- 먼저 데이터가 없는 형태의 페이지를 랜더링한다. 페이지 일부는 정적 생성하여 미리 랜더링하고 데이터가 필요한 상태를 표시한다.
- 그리고 클라이언트에서 데이터를 가져와 준비가되면 랜더링한다.

<b>

사용자 정보를 표시하는 페이지의 경우 SEO 최적화를 위한 처리와 사전 랜더링을 할 필요가 없다. 그리고 데이터가 자주 업데이트 될 수 있기 때문에 요청시간에 데이터를 가져오는 것이 좋다. <br>

<br><br>

### SWR

`Next.js`에서는 `SWR`이라는 데이터를 가져오기위한 React Hook을 만들었다. 이는 클라이언트에서 데이터 가져오기위한 Hook으로 캐싱, 재검증 등 처리를 한다. <br>

```jsx
import useSWR from 'swr'

function Profile() {
  const { data, error } = useSWR('/api/user', fetch)

  if (error) return <div>failed to load</div>
  if (!data) return <div>loading...</div>
  return <div>hello {data.name}!</div>
}
```

<br><br>

[Ref]:

- [Next.js Docs Basic Features Data Fetching](https://nextjs.org/docs/basic-features/data-fetching)


<br><br><br>