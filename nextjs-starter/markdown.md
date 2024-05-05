---
marp: true
theme: black-white
footer: NextJS 시작하기
paginate: true
emoji: twemoji
auto-scaling: true
_paginate: false
transition: fade
---

<!--
_class: lead
_footer: 2024-05-09 @ 튜링의 사과
-->

# NextJS 시작하기

### 누구나 손쉽게 따라할 수 있어요 ^\_^v

---

<!-- footer: 자기소개 -->

# 안녕하세요? 만나서 반갑습니다 ^\_^v

![right](./nabi-chan.jpeg)

> From Imagination Into Reality

안녕하세요? 저는 상상을 현실로 만드는 개발자 **나비**라고 합니다.

고객과 회사를 이어주는 <u>**채널코퍼레이션**</u>에서 프론트엔드 개발자로 근무하고 있어요.

NextJS를 사용하여 여러가지 재미있는 것들을 만들어 나가고 있습니다.

### Contact

- Mail : [hello@nabi.kim](mailto:hello@nabi.kim)
- Github : [@nabi-chan](https://github.com/nabi-chan)
- Blog : https://nabi-blog.vercel.app
- Discord : @nabi-chan

---

<!-- footer: 목차 -->

# 목차

### ~ 발표 후 얻을 수 있는 내용 미리 보기 ~

## 0. `CSR` / `SSR` 이해하기

## 1. NextJS에 대해서 알아보기

- NextJS 설치해보기
- 페이지 만들어보기

## 2. NextJS 더 잘 활용해보기

- `getStaticProps` / `getStaticPath` 로 정적인 페이지 만들어보기
- `getServerSideProps` 로 동적인 페이지 만들어보기
- API Route를 사용하여 API 만들어보기
- 트러블슈팅 가이드

### ~ 10분 휴식 ~

## 3. Vercel로 NextJS 앱 배포해보기

- 서비스 배포해보기
- vercel.json로 할 수 있는 기능들 알아보기
- Vercel을 사용해서 협업해보기

### ~ 질의응답 ~

</div>

---

<!-- footer: 목표 -->

# 목표

(여기에 깔쌈한 비디오 미리보기)

---

<!--
_class: lead
footer: CSR / SSR 에 대해서 알아보기
-->

# CSR/ SSR에 대해서 알아보기

---

# CSR (Client Side Rendering)

<div data-marpit-fragment="1">

**`app.js`**

```tsx
import { render } from "react-dom";

render(<h1>Hello, World!</h1>, document.getElementById("root"));
```

**`index.html (server)`**

```html
<div id="root"></div>
<script src="app.js"></script>
```

</div>

<div data-marpit-fragment="2">

# ⬇️

</div>
<div data-marpit-fragment="3">

**`index.html (browser)`**

```html
<div id="root">
  <h1>Hello, World!</h1>
</div>
<script src="app.js"></script>
```

</div>

---

# SSR (Server Side Rendering)

<div data-marpit-fragment="1">

**`app.js`**

```tsx
import { render } from "react-dom";

render(<h1>Hello, World!</h1>, document.getElementById("root"));
```

**`index.html (server)`**

```html
<div id="root">
  <h1>Hello, World!</h1>
</div>
<script src="app.js"></script>
```

</div>

<div data-marpit-fragment="2">

# ⬇️

</div>
<div data-marpit-fragment="3">

**`index.html (browser)`**

```html
<div id="root">
  <h1>Hello, World!</h1>
</div>
<script src="app.js"></script>
```

</div>

---

<!--
_class: lead
footer: NextJS에 대해서 알아보기
-->

# NextJS에 대해서 알아보기

---

<!-- _class: big-text -->

![right](https://velog.velcdn.com/images/hyumapr/post/87929c44-066f-4893-9f94-e85c0e59e3e0/image.png)

# NextJS, 넌 누구냐

NextJS는 Vercel에서 제작한 풀 스택 어플리케이션을 만들기에 특화된 오픈소스 웹 프레임워크입니다.

Server Side Rendering과 Static Site Generation을 지원하며,
API 엔드포인트를 만들어 풀 스택 어플리케이션을 쉽게 만들 수 있도록 도와줍니다.

주로 지원하는 기능은 다음과 같습니다 ^\_^b

- **Server Side Rendering (SSR)**
- Static Site Generation (SSG)
- **파일 기반 라우팅**
- **API Route**
- SCSS 지원 및 styled-components 기본 지원
- 이미지 / 폰트 최적화
- **타입스크립트** 기본 지원

---

<!-- _class: big-text -->

# 설치하기

0. 자주 사용하는 패키지 매니저를 터미널에서 열어줍니다. <small>(여기서는 bun을 사용할거에요!)</small>
1. `bun create next-app` 을 터미널에 입력합니다. <small>(또는 `npx create-next-app`)</small>
2. 터미널의 질문에 맞춰 내용을 작성해줍니다.

   ```bash
   - What is your project named? <프로젝트 이름>
   - Would you like to use TypeScript? > No / Yes # 타입스크립트 사용 유무
   - Would you like to use ESLint? > No / Yes # ESLint 사용 유무
   - Would you like to use Tailwind CSS? > No / Yes # tailwindcss 사용 유무
   - Would you like to use `src/` directory? > No / Yes # src/ 디렉토리 사용 유무
   - Would you like to use App Router? (recommended) > No / Yes # App Router 사용 유무
   - Would you like to customize the default import alias (@/*)? > No / Yes # import alias (relative path) 사용 유무
   - What import alias would you like configured? > ~/* # import alias 경로 (위에서 Yes를 선택한 경우에만 출력)
   - What import alias would you like configured? … ~/*
   - Creating a new Next.js app in /Users/root/Projects/<프로젝트 이름>.
   ```

3. 자주 사용하는 코드 에디터로 프로젝트를 열어보면 이제 모든 준비가 끝났습니다!

---

<!-- _class: big-text -->

![right](./nextjs.png)

# 서버 실행해보기

1. 에디터로 프로젝트를 열어줍니다.
2. 터미널을 열고 `bun dev` 를 입력합니다.
3. `http://localhost:3000` 을 브라우저에 입력하면...
4. 페이지가 표시됩니다! (야호!)

---

# 파일 기반 라우팅 이해하기

<div class="only" data-marpit-fragment="1">

![right](./hello-world.png)

</div>
<div class="only" data-marpit-fragment="2">

![right](./hello-world-result.png)

</div>

NextJS에서는 `/pages` 폴더의 경로를 기반으로 페이지 라우팅을 지원합니다.

예를 들어, `/pages/hello-world.tsx` 라는 페이지가 있다면,
`http://localhost:3000/hello-world` 로 경로가 설정됩니다.

| 파일 경로                     | 페이지 라우팅         |
| ----------------------------- | --------------------- |
| `/pages/hello-world.tsx`      | `/hello-world`        |
| `/pages/dynamic/[id].tsx`     | `/dynamic/1234`       |
| `/pages/multiple/[...id].tsx` | `/multiple/1234/5678` |

---

# 페이지 만들기

<div class="right">

```tsx
export default function Page() {
  return <div>Hello World!</div>;
}
```

</div>

기본적으로, NextJS의 모든 페이지는 default export가 되어있어야 하며,
반드시 함수의 리턴문에 JSX 코드가 작성되어있어야 합니다..

아까 보았던 hello-world.tsx의 코드를 열어보자면... 다음과 같습니다.

---

<!--
_class: lead
footer: NextJS 더 잘 활용해보기
-->

# NextJS 더 잘 활용해보기

---

# `getServerSideProps` 로 동적인 SSR 페이지 만들어보기

<div class="only" data-marpit-fragment="1">

![right](./ssr-draw.png)

동적인 페이지를 만들기 위해 만들어진 함수입니다.

페이지를 불러올 때, 서버에서 getServerSideProps의 함수를 실행하여 prop을 만들고, 이를 페이지에 prop으로 내려 렌더링을 합니다.

</div>

<div class="only" data-marpit-fragment="2">

**`/pages/product-list.tsx`**

```tsx
export default function Page({ products, total }: PageProps) {
  return (
    <>
      <h1>총 {total} 개의 상품</h1>
      <div>
        {products.map((product) => (
          <div key={product.id}>
            <h2>상품 {product.id} 번</h2>
            <pre key={product.id}>{JSON.stringify(product, null, 2)}</pre>
          </div>
        ))}
      </div>
    </>
  );
}

export async function getServerSideProps() {
  const { products, total } = await fetch(
    "https://dummyjson.com/products"
  ).then((res) => res.json());

  return {
    props: {
      products: products,
      total: total,
    },
  };
}
```

</div>
<div class="only" data-marpit-fragment="3">

![center](./product-list-result.png)

</div>

---

# `getStaticProps` 로 정적인 페이지 만들어보기

![right](./ssg-result.png)

정적인 페이지를 만들기 위해 만들어진 API 입니다.
빌드시에 주어진 **prop에 맞춰 정적인 페이지를 반환**합니다.

**`/pages/static-page.tsx`**

```tsx
export default function Page({ result }: PageProps) {
  return (
    <div>
      <h1>1 + 1의 값은 {result} 입니다</h1>
    </div>
  );
}

export function getStaticProps() {
  return {
    props: {
      result: 1 + 1,
    },
  };
}
```

---

# `getStaticPaths` 로 다양한 정적인 페이지 만들기

<div class="only" data-marpit-fragment="1">

만약 페이지가 dynamic route이고, `getStaticProps`을 사용한다면,
2개 이상의 페이지를 만들어야 하는 경우에는 어떻게 코드를 작성해야 할까요?

이럴때 사용할 수 있는 것이 `getStaticPaths` 입니다.

이 함수는 dynamic route에 맞게 정적인 페이지의 경로를 만들어주는 역할을 하는 함수입니다.

예를 들어, getStaticPaths의 return문이 다음과 같으면...

**`/pages/get-static-path-test/[page-id]/tsx`**

```json
{
  "paths": [
    { "params": { "page-id": 1 } },
    { "params": { "page-id": 2 } },
    { "params": { "page-id": 3 } },
    { "params": { "page-id": 4 } }
  ]
}
```

경로는 자연스럽게 `/get-static-path-test/1`, `/get-static-path-test/2`, `/get-static-path-test/3` 과 같이 paths 배열에 있는 요소에 따라 만들어집니다.

</div>

<div class="only" data-marpit-fragment="2">

**`/pages/static-paths/[product-id].tsx`**

```tsx
// TODO: render product detail page...

export async function getStaticProps(context: GetStaticPropsContext) {
  const product = await fetch(
    `https://dummyjson.com/products/${context.params?.["product-id"]}`
  ).then((res) => res.json());

  return {
    props: {
      product: product,
    },
  };
}

export async function getStaticPaths() {
  const { products } = await fetch("https://dummyjson.com/products").then(
    (res) => res.json()
  );

  return {
    paths: products.map((product: Product) => ({
      params: {
        "product-id": product.id.toString(),
      },
    })),
    fallback: false,
  };
}
```

</div>
<div class="only" data-marpit-fragment="3">

![center](./static-paths-result.png)

</div>

---

# API Route를 사용하여 API 만들어보기

API 만드는 예시 (fs를 사용한 데이터 CRUD)

---

# 트러블슈팅 가이드

오류 디버깅은 어떻게 하는지 등등...

---

# `@vercel/og` 를 사용하여 오픈그래프 이미지 만들어보기

오픈그래프 만들기

---

<!--
_class: lead
_footer: 휴식 시간
-->

# ~ 10분 휴식 시간 ~

질문이 있다면 편하게 질문해주세요!

---

<!--
_class: lead
footer: Vercel로 NextJS 앱 배포해보기
-->

# Vercel로 NextJS 앱 배포해보기

---

# Vercel은 또 뭔데?

Vercel에 대한 간단한 설명

---

# Vercel로 서비스 배포해보기

- cli를 사용한 배포
- github 레포 연결해서 자동으로 배포하기

---

# vercel의 여러 기능들 알아보기

- 로그 보기
- 인스턴트 롤백
- PR 프리뷰 코멘트
- 특정 브랜치에서만 빌드 되게 하기

---

# vercel.json으로 배포 커스터마이징 하기

- rewrite
- redirect
- headers 추가하기

---

# vercel에서 주기적으로 Node 프로그램 돌리기

- vercel.json cron 돌리기

---

<!--
_class: lead
_footer: 질의응답
-->

# 질의응답 🙋‍♀️

질문이 있다면 편하게 질문해주세요!

---

<!--
_class: lead
_footer: ""
-->

# 감사합니다 🙇‍♀️

- 이메일 : [hello@nabi.kim](mailto:hello@nabi.kim)
- 발표 자료 : https://nabi-blog.vercel.app/s/2024-nextjs-starter
- 소스 코드 : https://nabi-blog.vercel.app/s/2024-nextjs-starter-code
