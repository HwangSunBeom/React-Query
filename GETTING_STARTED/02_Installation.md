# 02. Installation

## 📌 1.1 NPM

```bash
$ npm i @tanstack/react-query
# or
$ pnpm add @tanstack/react-query
# or
$ yarn add @tanstack/react-query
```

## 📌 1.2 CDN
HTML 파일에 아래의 태그를 추가하기만 하면 됩니다.
```html
<script type="module">
  import React from 'https://esm.sh/react@18.2.0'
  import ReactDOM from 'https://esm.sh/react-dom@18.2.0'
  import { QueryClient } from 'https://esm.sh/@tanstack/react-query'
</script>
```

## 📌 1.3 Requirements
React Query는 아래 브라우저와 호환됩니다.
```bash
Chrome >= 91
Firefox >= 90
Edge >= 91
Safari >= 15
iOS >= 15
opera >= 77
```

## 📌 1.4 Recommendations
버그 예방 등을 목적으로 **ESLint Plugin Query** 사용을 추천합니다. 설치는 아래와 같이 할 수 있습니다.
```bash
$ npm i -D @tanstack/eslint-plugin-query
# or
$ pnpm add -D @tanstack/eslint-plugin-query
# or
$ yarn add -D @tanstack/eslint-plugin-query
```

### [공식문서 보러가기](https://tanstack.com/query/latest/docs/react/overview)
