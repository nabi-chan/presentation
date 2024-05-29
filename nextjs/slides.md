---
theme: apple-basic
title: 코드와 함께하는 NextJS 알아보기
info: |
  ## NextJS를 Vercel과 함께 사용해보세요!

  NextJS는 이제 웹 생태계에서 빠질수 없는 프레임워크가 되었습니다.
  이번 발표에서는, NextJS를 더 잘 사용하는 방법을 알아보도록 하겠습니다.
highlighter: shiki
transition: slide-left
mdc: true
fonts:
  sans: Pretendard
layout: intro
---

# 코드와 함께하는 NextJS 알아보기

NextJS를 알아보고, 더욱 잘 사용하는 방법을 배워봅시다.

<div class="absolute bottom-10">
  <span class="font-700">
    나비
  </span>
</div>

---

# 이 발표에서 다룹니다

- **NextJS의 내장 기능들 알아보기**
  - 파일 기반 라우팅 이해하기
  - Server Side Rendering (SSR)
  - Static Site Generation (SSG)
  - API 엔드포인트 만들기
  - SEO 최적화
  - NextJS 라이브러리 내장 기능들을 활용한 사이트 최적화
- **NextJS 외적인 기능들 알아보기**
  - `next-sitemap` 을 활용한 사이트맵 자동생성
  - `next-translate` 를 활용한 다국어화 처리
  - `@vercel/og` 를 사용한 이미지 생성

---

# 이 발표에서는 이것을 전제합니다.

- NextJS 14.2.3 버전을 기준으로 합니다.
- ES6 이상의 JavaScript 문법을 사용할 수 있음을 전제합니다.
- TypeScript에 대해 기초적인 지식이 있음을 전제합니다. (예제만)
- React의 문법을 이해하고, 이를 원활하게 사용할 수 있음을 전제합니다.

---
layout: statement
---

# 내장 기능들 알아보기

<Toc class="mt-8" mode="onlySiblings" minDepth="2" maxDepth="2" columns="2" />

---

## 파일 기반 라우팅 이해하기

파일 기반 라우팅은 `pages` 폴더 내에 있는 파일 및 폴더의 구조에 따라 자동으로 URL 라우트를 생성하는 방식입니다.

<v-click>

### 기본적인 사용 구조

- `pages/index.tsx` -> `/`
- `pages/about.tsx` -> `/about`
- `pages/blog/test.tsx` -> `/blog/test`

</v-click>
<v-click>

### 동적 라우팅 (`/:id` 와 같습니다)

- `pages/posts/[post-id]` -> `/posts/1234`, `/posts/nextjs`

</v-click>
<v-click>

### catch-all 라우팅 (`/*` 와 같습니다)

- `pages/categories/[...category]` -> `/categories/1depth/2depth/...`

</v-click>
<v-click>

### 전체 catch-all (`*` 와 같습니다.)

- `pages/custom-pages/[[...slug]]` -> `/custom-pages`, `/custom-pages/1234`

</v-click>
---

<h2>파일 기반 라우팅 이해하기</h2>

### 예약된 파일명 살펴보기

<v-click>

### `index.tsx`

- 각 폴더에서의 root route (`/`) 를 담당합니다.

</v-click>
<div v-click class="-mt-4">

### `_app.tsx`

- 리액트에서 Provider / Layout과 같이 페이지 간 공통적으로 사용되는 로직을 추가할 수 있습니다.
- 이곳에서 전역 css를 import 할 수 있습니다.

</div>
<div v-click class="-mt-4">

### `_document.tsx`

- NextJS에서 설정해주는 HTML의 위치등을 변경할 수 있습니다.
- Document class 를 extend하여 styled-components와 같은 css-in-js 라이브러리의 설정을 할 수 있습니다.

</div>
<div v-click class="-mt-4">

### `_error.tsx`

- NextJS에서의 서버사이드 에러 처리를 담당합니다.
- 클라이언트 에러 처리의 경우, ErrorBoundary를 추가해야 합니다.

</div>

---

<h2>파일 기반 라우팅 이해하기</h2>

### 페이지 만들어보기

<section class="flex gap-8 mt-4">
<div v-click class="flex-1">

```tsx
// pages/index.tsx

export default function Page() {
  return <div>Hello, World!</div>
}
```

</div>
<div v-click class="flex items-center">
➡️
</div>
<div v-click class="flex-1">

![NextJS Page Preview](/assets/hello-world.png)

</div>
</section>

---

## `getServerSideProps` 를 사용한 SSR 페이지 만들기

### `GetServerSideProps`란?

- 서버에서 '페이지를 요청하는 시점의 데이터' 를 가져와 페이지에 전달하는 함수입니다.
- 데이터베이스로 관리되는 게시글과 같이 동적인 사이트를 만드는데 사용됩니다.

### pages/getServerSideProps.tsx

````md magic-move
```tsx
import type { GetServerSideProps } from "next"

export const getServerSideProps = (async (ctx) => {
  return {
    props: {
      foo: "bar"
    }
  }
}) satisfies GetServerSideProps

export default function Page({ foo }: InferGetServerSideProps<typeof getServerSideProps>) {
  return (
    <div>what is foo? : {foo}</div>
  )
}
```
```tsx
import type { GetServerSideProps } from "next"

export const getServerSideProps = (async (ctx) => {
  const article = fetch("https://api.example.com/article")

  return {
    props: {
      article: await article.json()
    }
  }
}) satisfies GetServerSideProps

export default function Page({ article }: InferGetServerSideProps<typeof getServerSideProps>) {
  // ...
}
```
```tsx
import type { GetServerSideProps } from "next"

export const getServerSideProps = (async (ctx) => {
  if (IF_INVALID_ACCESS) {
    return {
      // / 페이지로 리다이렉트
      redirect: {
        destination: "/",
        permanent: false
      }
    }
  }
}) satisfies GetServerSideProps

```
```tsx
import type { GetServerSideProps } from "next"

export const getServerSideProps = (async (ctx) => {
  if (!ctx.params.id) {
    return {
      // 404 페이지 반환
      notFound: true
    }
  }
}) satisfies GetServerSideProps
```
````

---

## `getStaticProps` 를 사용한 정적 페이지 만들기

### `GetStaticProps` 란?

- 서버에서 '프로젝트를 빌드하는 시점의 데이터'를 가져와 페이지에 전달하는 함수입니다.
- 개인정보 약관과 같이 자주 변경되지 않는 정적인 파일 등에 주로 사용됩니다.

### pages/getStaticProps.tsx


````md magic-move
```tsx
import type { GetStaticProps, InferGetStaticProps } from "next"

export const getStaticProps = (async (ctx) => {
  return {
    // 기본적인 문법은 GetServerSideProps와 동일합니다.
    props: {
      foo: "bar"
    }
  }
}) satisfies GetStaticProps


export default function Page({ foo }: InferGetStaticProps<typeof getStaticProps>) {
  return (
    <div>what is foo? : {foo}</div>
  )
}
```
```tsx
import type { GetStaticProps, InferGetStaticProps } from "next"

export const getStaticProps = (async (ctx) => {
  return {
    // 10초 뒤에 새로운 요청이 들어오는 경우 다시 페이지 생성
    revalidate: 10,
    props: {
      foo: "bar"
    }
  }
}) satisfies GetStaticProps

export default function Page({ foo }: InferGetStaticProps<typeof getStaticProps>) {
  return (
    <div>This page will be re-generated after 10 seconds.</div>
  )
}
```
````

---

## `getStaticPath` 를 사용한 많은 정적 페이지 만들기

### `GetStaticPath` 란?

- `GetStaticProps` 와 함께 사용하며, 다양한 정적인 페이지들을 만들어야 할 때 주로 사용됩니다.
- 마크다운으로 만들어진 글들이나, 크롤링된 페이지들을 표시할 수 있습니다.

### `pages/getStaticPaths/[id].tsx`


<div class="max-h-[300px]">

````md magic-move max-h-[300px] overflow-y-auto
```tsx
import type { GetStaticProps, GetStaticPaths, InferGetStaticProps } from "next"

export const getStaticPaths = (async () => {
  const res = await fetch('https://.../posts')
  const posts = await res.json()

  return {
    // [{ id: 1 }, { id: 2 }] 와 같이 반환됩니다.
    paths: posts.map((post) => ({
      params: { id: post.id },
    }))
  }
}) satisfies GetStaticPaths

export const getStaticProps = (async (ctx) => {
  return {
    props: {
      postId: ctx.params.id
      foo: "bar"
    }
  }
}) satisfies GetStaticProps

export default function Page({ postId, foo }: InferGetServerSideProps<typeof getStaticProps>) {
  return (
    <div>what is postId? : {postId}</div>
  )
}
```
```tsx
import type { GetStaticProps, GetStaticPaths, InferGetStaticProps } from "next"

export const getStaticPaths = (async () => {
  const res = await fetch('https://.../posts')
  const posts = await res.json()

  return {
    // 페이지가 로딩되지 않은 경우, 로딩 페이지를 우선적으로 반환합니다.
    fallback: true,
    paths: posts.map((post) => ({
      params: { id: post.id },
    }))
  }
}) satisfies GetStaticPaths

export const getStaticProps = (async (ctx) => {
  // ...
}) satisfies GetStaticProps
```
```tsx
import type { GetStaticProps, GetStaticPaths, InferGetStaticProps } from "next"

export const getStaticPaths = (async () => {
  const res = await fetch('https://.../posts')
  const posts = await res.json()

  return {
    // 페이지가 없는 경우, 404 페이지를 반환합니다.
    fallback: false,
    paths: posts.map((post) => ({
      params: { id: post.id },
    }))
  }
}) satisfies GetStaticPaths

export const getStaticProps = (async (ctx) => {
  // ...
}) satisfies GetStaticProps
```
```tsx
import type { GetStaticProps, GetStaticPaths, InferGetStaticProps } from "next"
import { useRouter } from "next/router"

export const getStaticPaths = (async () => {
  const res = await fetch('https://.../posts')
  const posts = await res.json()

  return {
    // 페이지가 없는 경우, 페이지가 생성될 때까지 기다립니다.
    fallback: 'blocking',
    paths: posts.map((post) => ({
      params: { id: post.id },
    }))
  }
}) satisfies GetStaticPaths

export default function Page() {
  const { isFallback } = useRouter()

  if (isFallback) {
    return <div>로딩중입니다...</div>
  }

  return <div>로딩 완료!</div>
}

export const getStaticProps = (async (ctx) => {
  // ...
}) satisfies GetStaticProps
```
````

</div>

---

## API Route를 이용한 API 만들기

- `pages/api` 폴더 하위에 페이지를 만듦으로써 API를 만들 수 있습니다.

### `/pages/api/hello-world.ts`

```ts twoslash
import type { NextApiRequest, NextApiResponse } from 'next'
 
type ResponseData = {
  message: string
}
 
export default async function handler(
  req: NextApiRequest,
  res: NextApiResponse<ResponseData>
) {
  res.status(200).json({ message: 'Hello from Next.js!' })
}
```

---

## `next/link` 를 이용한 페이지 이동

- `<Link>` 태그를 사용하여 react-router와 같은 라이브러리 없이도 SPA 라우팅을 사용할 수 있습니다.

### `/pages/link-preview.tsx`
```tsx twoslash
import React from "react"
import Link from "next/link"

export default function Page() {
  return (
    <>
      <Link href="/another-page">Go To Another Page</Link>
      <Link
        href={{
          pathname: '/blog/[slug]',
          query: { slug: 'my-post' },
        }}
      >
        Go To Blog Post
      </Link>
    </>
  )
}
```

---

## `next/head` 를 이용한 SEO 최적화

- `<Head>` 태그를 사용하여 각 페이지에 맞는 메타태그를 넣을 수 있습니다.

### `/pages/head-preview.tsx`
```tsx twoslash
import React from "react"
import Head from "next/Head"

export default function Page() {
  return (
    <Head>
      <title>next/head 시연해보기</title>
      <meta name="description" content="Free Web tutorials" />
      <meta name="keywords" content="HTML, CSS, JavaScript" />
      <meta name="author" content="John Doe" />
    </Head>
  )
}
```

---

## `next/font` 를 이용한 폰트 최적화

- `next/font/google` 을 사용해 구글 폰트를 번들에 포함할 수 있습니다.
- 구글 폰트가 번들에 포함되면 같은 서버에서 파일을 요청하기에 빠른 응답속도를 가질 수 있습니다.

```tsx twoslash
import React from "react"
import { Inter, JetBrains_Mono } from "next/font/google";

const inter = Inter({ subsets: ["latin"] });
const jetBrainsMono = JetBrains_Mono({ subsets: ["latin"] });

export default function Page() {
  return (
    <div>
      <span className={inter.className}>Inter 폰트입니다</span>
      <span className={jetBrainsMono.className}>jetBrains Mono 폰트입니다</span>
    </div>
  )
}
```

---

## `next/image` 를 이용한 이미지 최적화

---
layout: statement
---

# 유용한 외부 기능들 알아보기

<Toc mode="onlyCurrentTree" minDepth="2" maxDepth="2" />

---

## `next-sitemap` 을 이용한 사이트맵 자동 생성

---

## `next-translate` 를 활용한 다국어화 처리

---

## `@vercel/og` 를 사용한 정적 이미지 생성

---
layout: statement
---

# Q&A

---
layout: statement
---

# 감사합니다! 🙇‍♀️