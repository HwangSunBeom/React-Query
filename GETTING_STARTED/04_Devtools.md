# 04. Devtools
리액트 쿼리는 전용 개발자 도구를 제공합니다. 이 도구는 내부 동작을 시각화하는 데 도움이 되고, 비거깅 시간을 절약할 수 있습니다. 단, 현재 리액트 네이티브 환경에서는 지원하지 않습니다.

## 📌 4.1 Import the Devtools
추가 설치는 필요하지 않으며, `react-query/devtools` 패키지에 포함되어 있습니다.

```js
import { ReactQueryDevtools } from 'react-query/devtools'
```

기본적으로 React Query Devtools는 `process.env.NODE_ENV === 'development'`에서만 적용되므로, 프로덕션 빌드 시 제외할 필요가 없습니다.

## 📌 4.2 Floating Mode
플로팅 모드는 Devtools를 고정해 제공하고, 이는 화면 구석에 토글을 통해 표시하거나 숨길 수 있습니다. 토글 상태는 localStorage에서 관리됩니다.

다음 코드를 앱의 상위(root)에 가깝게 작성할수록 좋습니다.

```js
import { ReactQueryDevtools } from 'react-query/devtools'

function App() {
  return (
    <QueryClientProvider client={queryClient}>
      {/* The rest of your application */}
      <ReactQueryDevtools initialIsOpen={false} />
    </QueryClientProvider>
  )
}
```

### [공식문서 보러가기](https://tanstack.com/query/latest/docs/react/overview)
