# 03. Quick Start

아래 예제 코드는 React Query와 관련된 3가지 핵심 컨셉을 간략히 보여줍니다.

- [Queries](https://tanstack.com/query/latest/docs/react/guides/queries)
- [Mutations](https://tanstack.com/query/latest/docs/react/guides/mutations)
- [Query Invalidation](https://tanstack.com/query/latest/docs/react/guides/query-invalidation)

## 📌 3.1 Example Code

```tsx
import {
  useQuery,
  useMutation,
  useQueryClient,
  QueryClient,
  QueryClientProvider,
} from '@tanstack/react-query'
import { getTodos, postTodo } from '../my-api'

// 쿼리 클라이언트 생성
const queryClient = new QueryClient()

function App() {
  return (
    // 앱에 쿼리 클라이언트 제공
    <QueryClientProvider client={queryClient}>
      <Todos />
    </QueryClientProvider>
  )
}

function Todos() {
  // 쿼리 클라이언트 접근
  const queryClient = useQueryClient()

  // Queries
  const query = useQuery({ queryKey: ['todos'], queryFn: getTodos })

  // Mutations
  const mutation = useMutation({
    mutationFn: postTodo,
    onSuccess: () => {
      // 쿼리키로 클라이언트에 접근해 쿼리를 만료시키고 갱신함
      queryClient.invalidateQueries({ queryKey: ['todos'] })
    },
  })

  return (
    <div>
      <ul>
        {query.data?.map((todo) => (
          <li key={todo.id}>{todo.title}</li>
        ))}
      </ul>

      <button
        onClick={() => {
          mutation.mutate({
            id: Date.now(),
            title: 'Do Laundry',
          })
        }}
      >
        Add Todo
      </button>
    </div>
  )
}

render(<App />, document.getElementById('root'))
```

### [공식문서 보러가기](https://tanstack.com/query/latest/docs/react/overview)
