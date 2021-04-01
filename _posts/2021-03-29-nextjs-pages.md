---
layout: post
title: 'Next.js Pages'
categories: [javascript, nextjs]
image: assets/images/banner/nextjs.jpeg
author: yeon
---

# Next.js Pages

**Next.js**에서 페이지는 **pages** 디렉터리 하위의 `.js .jsx .ts .tsx` 파일에서 내보낸 React 컴포넌트이다. 각 페이지는 파일이름에 따라 경로로 구성된다. <br>

<br>

예로 아래와 같이 React 컴포넌트를 내보내는 `pages/about.jsx`를 생성하면 `/about` 경로로 해당 페이지를 접근 할 수 있다. <br>

<br><br>

## Pages with Dynamic Routes

```jsx
// pages/about.jsx

const About = () => {
  return <div>Aboout</div>;
};

export default About;
```

**Next.js**는 동적 경로가 있는 페이지를 지원한다. 만약 `pages/posts/[id].jsx` 형태로 파일을 만든다면 posts / 1, posts/ 2 와 같은 형태로 페이지 접근이 가능하다. <br>

<br>

> [Dynamic Routes](https://nextjs.org/docs/routing/dynamic-routes)

<br><br>

## Pre-rendering

기본적으로 **Next.js**는 모든 페이지를 사전 랜더링한다. 즉 **Next.js**는 클라이언트 측 Javascript에서 모든 작업을 수행하는 대신 각 페이지에 대해 미리 HTML을 생성한다. 사전 랜더링은 초기 페이지를 빠르게 제공하는 등의 더 나은 성능과 `SEO` 검색 엔진 최적화의 장점이 있다. <br>

<br>

### Hydration

사전 생성 된 각 HTML은 해당 페이지에 필요한 최소한의 Javascript 코드와 연결된다. 페이지를 로드하면 해당 Javascript 코드가 실행되고 페이지가 동작하게 된다. <br>

<br><br>

## Tow forms of Pre-rendering

**Next.js**에는 정적 생성(SSG: Static Generation)과 서버 사이드 렌더링(SSR: Server Side Rendering) 두가지 형태의 사전 랜더링이 있다. 차이점은 페이지의 HTML을 생성하는 시점이다. <br>

<br>

- **SSG (Static Site Generation)** : HTML은 빌드시 생성되며 각 요청에서 재사용된다.
- **SSR(Server Side Rendering)** :  HTML은 각 요청에 대해 생성된다.

<br><br>

## [Static Site Generation (Recommended)](https://nextjs.org/docs/basic-features/pages#static-generation-recommended)

페이지 정적 생성을 사용하는 경우 HTML은 빌드시 생성된다. 즉, 프로덕션에서 다음 빌드를 실행할 때 페이지 HTML이 생성된다. 이 HTML은 각 요청에서 재사용된다. CDN에 의해 캐시 될 수 있다. <br>

<br>

> 개발 모드 (npm run dev 또는 yarn dev를 실행하는 경우)에서는 정적 생성을 사용하는 페이지의 경우에도 모든 페이지가 각 요청에 대해 사전 렌더링된다.

<br>

외부에서 데이터를 가져올 필요가 없는 경우 사전랜더링하여 빌드 시간동안 HTML을 미리 생성해 두는 것이 좋다. <br>

<br><br>

### Static Site Generation with data

일부 페이지는 사전 렌더링을 위해 외부 데이터를 가져와야한다. 두 가지 시나리오가 있으며 하나 또는 둘 모두가 적용될 수 있다. 각각의 경우 Next.js가 제공하는 특수 기능을 사용할 수 있다. <br>

<br>

- **getStaticProps**
- **getStaticPaths**

<br>

#### Scenario 1 : Your page content depends on external data

```jsx
function Blog({ posts }) {
  // Render posts...
}

// This function gets called at build time
export async function getStaticProps() {
  // Call an external API endpoint to get posts
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

`getStaticProps` : 빌드 타임 때 실행되며 pre rendering시 데이터를 가져와 데이터를 설정 할 수 있다. <br>
사전 랜더링에 데이터를 가져오므로 실시간으로 데이터가 자주 바뀌는 곳에서는 사용을 피하는 것이 좋다. <br>

<br>

#### Scenario 2 : Your page paths depend on external data

<br>

**Next.js**를 사용하면 동적 경로가있는 페이지를 만들 수 있다. 예를 들어 `pages/posts/[id].js`라는 파일을 만들어 Id를 기반으로한 단일 블로그 게시물을 표시 할 수 있다. 이렇게하면 `posts/1`에 액세스 할 때 id : 1 인 블로그 게시물을 표시 할 수 있다. <br>

그러나 빌드시 사전 렌더링하려는 Id는 외부 데이터에 따라 달라질 수 있다. <br>

<br>

```jsx
// This function gets called at build time
export async function getStaticPaths() {
  // Call an external API endpoint to get posts
  const res = await fetch('https://.../posts');
  const posts = await res.json();

  // Get the paths we want to pre-render based on posts
  const paths = posts.map((post) => ({
    params: { id: post.id },
  }));

  // We'll pre-render only these paths at build time.
  // { fallback: false } means other routes should 404.
  return { paths, fallback: false };
}
```

`getStaticPaths` : 사전에 랜더링하려는 페이지 경로를 설정하여 페이지를 미리 사전 랜더링한다. <br>

사전 랜더링 하려는 Id를 기반으로 paths를 설정하여 해당 경로에 맞는 페이지를 사전랜더링한다. <br>

fallback의 경우 해당 경로를 제외한 경로는 404로 인지한다. fallback true로 설정할 경우 nextjs Link 등의 경로를 만날시 경로 진입 전 빌드하여 HTML 페이지를 사전생성한다. <br>

<br>

```jsx
export async function getStaticPaths() {
  // ...
}

// This also gets called at build time
export async function getStaticProps({ params }) {
  // params contains the post `id`.
  // If the route is like /posts/1, then params.id is 1
  const res = await fetch(`https://.../posts/${params.id}`);
  const post = await res.json();

  // Pass post data to the page via props
  return { props: { post } };
}
```

**getStaticProps**를 함께 사용하여 랜더링에 사용할 데이터를 사전랜더링에 설정한다. **getStaticProps**의 params에는 paths 경로에 맞는 params 정보를 가져와 페이지에 맞는 데이터를 api 등을 호출하여 가져올 수 있다. <br>

<br>

가능한 한 정적 생성 (데이터 포함 및 제외)을 사용하는 것이 좋다. 페이지를 한 번 빌드하고 CDN에서 제공 할 수 있으므로 서버가 모든 요청에 대해 페이지를 렌더링하는 것보다 훨씬 빠르다. <br>

<br><br>

## [Server-side Rendering](https://nextjs.org/docs/basic-features/pages#server-side-rendering)

페이지가 서버 측 렌더링을 사용하는 경우 페이지 HTML은 각 요청에서 생성된다. <br>

<br>

> "서버 사이드 랜더링" 또는 "동적 렌더링"이라고도한다.

<br>

페이지에 서버 측 렌더링을 사용하려면 getServerSideProps라는 비동기 함수를 내 보내야한다. 이 함수는 모든 요청에서 서버에 의해 호출된다. <br>

<br>

```jsx
function Page({ data }) {
  // Render data...
}

// This gets called on every request
export async function getServerSideProps() {
  // Fetch data from external API
  const res = await fetch(`https://.../data`);
  const data = await res.json();

  // Pass data to the page via props
  return { props: { data } };
}

export default Page;

```

**getServerSideProps** : **getStaticProps**와 유사하지만 차이점은 **getServerSideProps**가 빌드 시간이 아닌 모든 요청에서 실행된다. <br>

<br>

모든 요청에 실행된다는 점에서 불필요하게 리소스를 사용할 수 있지만 실시간으로 변경되는 데이터를 가져와야 할 경우에 **getServerSideProps** 사용하여 정확한 데이터를 가져와 랜더링 할 수 있다. <br>

<br><br>

## Summary

- **Static Generation (Recommended)** : HTML은 빌드시 생성되며 **getStaticProps**, **getStaticPaths**를 사용하여 경로 및 데이터를 구성할 수 있다. 사용자의 요청전에 미리 랜더링 할 수있는 페이지에 적합하다.
- **Server-Side Rendering** : HTML은 각 요청에 의해 생성된다. 서버 사이드 랜더링을 사용하기 위해선 getServerSideProps를 사용한다. 정적 생성보다는 성능이 느리기 때문에 사용시 고려하여 사용하여야 한다.

<br><br>

[Ref]:

- [Next.js Docs Basic Features Pages](https://nextjs.org/docs/basic-features/pages)


<br><br><br>