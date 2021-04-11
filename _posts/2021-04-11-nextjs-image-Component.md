---
layout: post
title: 'Image Component and Image Optimization'
categories: [javascript, nextjs]
image: assets/images/banner/nextjs.jpeg
author: yeon
---

# Image Component and Image Optimization

Next.js 버전 10.0.0 부터 이미지 컴포넌트 제공되어 이미지 최적화가 가능하다. <br>
Next.js에서 이미지 컴포넌트는 `next/image` 로 HTML img tag의 확장이다. <br>

<br>

자동 이미지 최적화를 사용하면 브라우저가 지원하는 경우 WebP와 같은 최신 형식으로 이미지 크기를 조정하고 최적화된 이미지를 제공 할 수 있다. 이렇게 하면 뷰포트가 더 작은 장치로 큰 이미지가 전송되는 것을 방지 할 수 있다. 자동이미지 최적화는 모든 이미지 소스에서 작동하고 이미지가 CMS와 같은 이부 데이터 소스에서 호스팅 되는 경우에도 여전히 최적화 할 수 있다. <br>

<br>

빌드시 이미지를 최적화 하는 대신 Next.js는 사용자가 요청할 때 이미지를 on-demand로 최적화 한다. 빌드 시간은 이미지 10개를 전송하든 1,000만개를 전송하든 증가하지 않는다. 이미지는 기본적으로 지연로드되고 뷰포트 외부의 이미지에 대해서는 페이지 속도에 불이익이 없다. <br>

<br>

## Image Component

이미지를 추가하고 싶다면 `next/image` 컴포넌트를 import 하자. <br>

```jsx
import Image from 'next/image'

function Home() {
  return (
    <>
      <h1>My Homepage</h1>
      <Image
        src="/me.png"
        alt="Picture of the author"
        width={500}
        height={500}
      />
      <p>Welcome to my homepage!</p>
    </>
  )
}

export default Home
```

<br><br>

## Configuration

`next.config.js`를 통해서 이미지 최적화를 선택적으로 구성할 수도 있다. <br>

<br><br>

### Domains

외부 웹사이트에서 호스팅되는 이미지 최적화를 사용하려면 이미지 src에 절대 URL을 사용하고 최적화 할 수 있는 도메인을 지정해야한다. <br>

```jsx
module.exports = {
  images: {
    domains: ['example.com'],
  },
}
```

<br><br>

## Loader

Next.js의 기본 제공 이미지 최적화를 사용하는 대신 클라우드 공급자를 사용하여 이미지를 최적화 하려는 경우 로더 및 경로 접두사를 구성 할 수 있다. 이를 통해 Image src에 상대 URL을 사용하고 올바른 절대 URL을 자동으로 생성 할 수 있다. <br>

```jsx
module.exports = {
  images: {
    loader: 'imgix',
    path: 'https://example.com/myaccount/',
  },
}
```

<br>

- [Vercel](https://vercel.com/): Works automatically when you deploy on Vercel, no configuration necessary.
- [Imgix](https://www.imgix.com/): `loader: 'imgix'`
- [Cloudinary](https://cloudinary.com/): `loader: 'cloudinary'`
- [Akamai](https://www.akamai.com/): `loader: 'akamai'`
- Default: Works automatically with `next dev`, `next start`, or a custom server

<br><br>

## Caching

이미지는 요청에따라 동적으로 최적화 되고 <distDir> / cache / images 디렉토리에 저장된다. 만료일에 도달 할 때까지 후속 요청에 최적화된 이미지를 제공한다. <br>

<br>

만료시간(Max Age)은 업스트림 서버의 Cache-Control 헤더에 의해 정의된다. Cache-Control에서 s-maxage가 있다면 이를 사용한다. s-maxage가 없다면 max-age가 사용된다. max-age도 없다면 기본값으로 60초가 사용된다. <br>

<br><br>

## Static File Serving

Next.js는 루트 디렉토리의 public 폴더 아래에 이미지와 같은 정적 파일을 제공 할 수 있다. 기본 URL에서 / 경로 기점으로 public 내부의 파일을 참조 할 수 있다. <br>

<br>

예로 public/me.png 이미지를 사용해보자. <br>

```jsx
import Image from 'next/image'

function Avatar() {
  return <Image src="/me.png" alt="me" width="64" height="64" />
}

export default Avatar
```

<br><br>

[Ref]:

- [Next.js Docs Basic Features Image Component and Image Optimization](https://nextjs.org/docs/basic-features/image-optimization)
- [Next.js Docs Basic Features Static File Serving](https://nextjs.org/docs/basic-features/static-file-serving)


<br><br><br>