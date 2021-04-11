---
layout: post
title: 'Environment Variables'
categories: [javascript, nextjs]
image: assets/images/banner/nextjs.jpeg
author: yeon
---

# Environment Variables

> Next.js 9.4버전 이상용 입니다.

Next.js는 환경 변수에 대한 기본 지원을 제공한다. <br>

- `.env.local`을 사용하여 환경변수 로드
- 브라우저에 환경 변수 노출

<br><br>

## Loading Environment Variables

Next.js는 `.env.local`에서 `process.env`로 환경 변수 로드를 제공한다. <br>

- `.env.local`

```tsx
# .env.local
DB_HOST=localhost
DB_USER=myuser
DB_PASS=mypassword
```

<br>

위와 같이 작성된 경우 process.env.DB_HOST, process.env.DB_USER, process.env.DB_PASS가  Node.js 환경에 로드되어 Next.js에서 데이터를 가져와 사용할 수 있다. <br>

```tsx
// pages/index.js
export async function getStaticProps() {
  const db = await myDB.connect({
    host: process.env.DB_HOST,
    username: process.env.DB_USER,
    password: process.env.DB_PASS,
  })
  // ...
}
```

<br>

Next.js는 .env 파일내에서 자동으로 변수를 확장한다. 변수는 $VAR와 같은 형태로 사용이 가능하다. <br>

```tsx
# .env
HOSTNAME=localhost
PORT=8080
HOST=http://$HOSTNAME:$PORT
```

<br>

실제값에 $가 있는 경우 /$ 형태로 처리한다. <br>

```tsx
# .env
A=abc

# becomes "preabc"
WRONG=pre$A

# becomes "pre$A"
CORRECT=pre\$A
```

<br><br>

## Exposing Environment Variables to the Browser

기본적으로 .env.local을 통해 로드된 환경변수는 Node.js 환경에서만 사용할 수 있으므로 브라우저에는 노출되지 않는다. <br>
브라우저에 변수를 노출하려면 변수 앞에 NEXT_PUBLIC_을 붙여야한다. <br>

```tsx
NEXT_PUBLIC_ANALYTICS_ID=abcdefghijk
```

<br>

위와 같이 설정 된 경우 process.env.NEXT_PUBLIC_ANALYTICS_ID는 Node.js 환경에 로드되어 사용가능하고 브라우저로 전송되는 Javascript에 빌드시 인라인되어 브라우저에서도 사용이 가능하게된다. <br>

```tsx
// pages/index.js
import setupAnalyticsService from '../lib/my-analytics-service'

// NEXT_PUBLIC_ANALYTICS_ID can be used here as it's prefixed by NEXT_PUBLIC_
setupAnalyticsService(process.env.NEXT_PUBLIC_ANALYTICS_ID)

function HomePage() {
  return <h1>Hello World</h1>
}

export default HomePage
```

<br><br>

## Default Environment Variables

일반적으로 .env.local 파일은 하나만 필요하다. 그러나 때로는 개발, 프로덕션 환경에 대한 설정별로 나눌 수 있다. <br>
Next.js를 사용하여 .env.development 및 .env.production 환경 형태로 기본값 설정이 가능하다. 여기서 .env.local은 모든 환경의 기본값으로 동작하여 다른 환경에서 선언시 기본값에 대한 재정의로 동작합니다. <br>

<br><br>

## Test Environment Variables

개발 및 프로덕션 환경 이외에도 테스트 환경을 설정하여 사용할 수 있다. 테스트에는 .env.test 형태의 파일을 사용하고 테스트 도구인 jest 또는 cypress 같은 테스트를 실행할 때 유용하다. <br>

<br>

다른 환경과 다른점은 .env.local에 대한 기본값은 로드되지 않습니다. (development, production의 경우 local 기본값 로드 후 재정의) <br>

<br>

단위테스트를 실행하는 동안  @next/env 패키지의 loadEnvConfig 함수를 사용하여  Next.js와 동일한 방식으로 환경변수를 로드할 수 있다. <br>

```tsx
// The below can be used in a Jest global setup file or similar for your testing set-up
import { loadEnvConfig } from '@next/env'

export default async () => {
  const projectDir = process.cwd()
  loadEnvConfig(projectDir)
}
```

<br><br>

[Ref]:

- [Next.js Docs Basic Features Environment Variables](https://nextjs.org/docs/basic-features/environment-variables)


<br><br><br>