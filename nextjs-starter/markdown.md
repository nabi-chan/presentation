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

<div data-marpit-fragment="1">

### ~ 발표 후 얻을 수 있는 내용 미리 보기 ~

</div>
<div data-marpit-fragment="2">

## 0. `CSR` / `SSR` 이해하기

## 1. NextJS에 대해서 알아보기

- `getStaticProps` / `getStaticPath` 로 정적인 페이지 만들어보기
- `getServerSideProps` 로 동적인 페이지 만들어보기
- API Route를 사용하여 API 만들어보기
- 트러블슈팅 가이드

</div>
<div data-marpit-fragment="3">

### ~ 10분 휴식 ~

</div>
<div data-marpit-fragment="4">

## 2. Vercel로 NextJS 앱 배포해보기

- 서비스 배포해보기
- vercel.json로 할 수 있는 기능들 알아보기
- Vercel을 사용해서 협업해보기

</div>
<div data-marpit-fragment="5">

### ~ 질의응답 ~

</div>

---

<!-- footer: 발표 후 얻을 수 있는 내용 -->

# 내용물 미리보기

(여기에 깔쌈한 비디오 미리보기)

---

<!--
_class: lead
footer: CSR / SSR 에 대해서 알아보기
-->

# CSR/ SSR에 대해서 알아보기

---

# CSR (Client Side Rendering)

**브라우저(클라이언트)에서 JS를 사용하여 렌더링 하는 방식**

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

**서버에서 리액트를 미리 렌더링 하여 내려주는 방식**

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

# CSR / SSR의 차이점 알아보기

| 분류                    | Client Side Rendering        | Server Side Rendering       |
| ----------------------- | ---------------------------- | --------------------------- |
| 어디에서 렌더링 되는가? | 브라우저                     | 서버                        |
| 사용하는 API            | Browser API (`localStorage`) | NodeJS API (`fs.writeSync`) |

---

<!--
_class: lead
footer: NextJS에 대해서 알아보기
-->

# NextJS에 대해서 알아보기

---

# NextJS, 넌 누구냐

---

# `getStaticProps` / `getStaticPath` 로 정적인 페이지 만들어보기

정적인 페이지 만드는 예시 (fs로 마크다운 파일 가져와서 렌더링 하기)

---

# `getServerSideProps` 로 동적인 페이지 만들어보기

동적인 페이지 만드는 예시 (더미 API 사용해서 랜덤한 유저 정보 뱉어내게 하기)

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
