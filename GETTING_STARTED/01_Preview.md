# 01. Preview

## 📌 1.1 개요

TanStack Query(FKA React Query)는 웹 애플리케이션에서 **Server State**의 `fetching`, `caching`, `synchronizing`, `updating`를 쉽게 해줍니다.

### Motivation

대부분의 핵심 웹 프레임워크는 데이터를 통합적으로 fetching/updating하는 것에 취약(?)해, 개발자들은 data-fecthing을 위해 meta-frameworks를 구축하거나, 자신만의 방법을 발명해야 했습니다. 이는 주로 컴포넌트 기반의 상태와 부작용을 대충 맞추거나, 일반적인 용도의 상태 관리 라이브러리를 사용해 애플리케이션 전체에 비동기 데이터를 저장하고 제공하는 형태입니다.

대부분의 전통적인 상태 관리 라이브러리들은 client state를 다루는 데에 좋지만, async나 server state를 다루는 데에는 그닥 좋지 않습니다다. server state가 갖는 아래와 같은 특징 때문입이다.

**서버 상태(Server State)의 특징**

- 사용자가 제어하지 않거나, 소유하지 않은 위치에서 원격으로 유지됨
- fetch/update를 위해 비동기 API를 필요로 함
- 사용자가 모르는 사이에 다른 사용자가 변경할 수 있음
- 주의하지 않는 경우, 애플리케이션 내에서 "오래된" 상태가 될 수 있음

<br/>

애플리케이션의 서버 상태 특성을 파악했다면, 다음과 같은 과제가 있습니다.

**서버 상태(Server State)와 관련한 과제**

- 캐싱(프로그래밍에서 가장 어려울 수 있는...)
- 동일한 데이터에 대한 여러 요청을 단일 요청으로 중복 제거
- 백그라운드에서 "오래된" 데이터 업데이트
- 데이터가 "오래된" 시점 파악
- 데이터의 업데이트를 최대한 신속하게 반영
- pagintaion이나 lazy loading data 같은 성능 최적화
- 서버 상태의 메모리 및 가비지 컬렉션 관리
- 구조적 공유(Structural Sharing)로 쿼리 결과 메모이징(Memoizing)

<br/>

React Query는 서버 상태를 관리하기 위한 최고의 라이브러리 중 하나인데, 초기 설정 없이도 잘 동작하고 애플리케이션에 맞춰 커스터마이징이 가능합니다.

**React Query의 Technical 노트**

- 복잡하고 오해하기 쉬운 코드를 간단한 React Query 로직으로 대체
- 서버 상태를 활용한 새로운 기능 개발 및 유지보수에 용이
- 애플리케이션 응답성 개선에 따라 최종 사용자에게 영향
- 대역폭 절약 및 메모리 성능 향상에 도움

<br/>

## 📌 1.2 예제 코드

아래 예제를 통해 React Query GitHub 프로젝트 자체에 대한 GitHub stats를 가져오는 데 사용되는 가장 기본적이고 간단한 형태의 React Query입니다

```tsx
// react-query 임포트
import {
  QueryClient,
  QueryClientProvider,
  useQuery,
} from "@tanstack/react-query";

// QueryClient 선언
const queryClient = new QueryClient();

export default function App() {
  return (
    // App 전체에서 QueryClient에 접근할 수 있도록 Provider로 감싸기
    <QueryClientProvider client={queryClient}>
      <Example />
    </QueryClientProvider>
  );
}

// 예제 애플리케이션
function Example() {
  // useQuery를 이용한 데이터 fetch
  const { isPending, error, data } = useQuery({
    queryKey: ["repoData"],
    queryFn: () =>
      fetch("https://api.github.com/repos/TanStack/query").then((res) =>
        res.json()
      ),
  });
  // 데이터가 로딩중일때
  if (isPending) return "Loading...";

  // 에러가 발생했을때
  if (error) return "An error has occurred: " + error.message;

  return (
    <div>
      <h1>{data.name}</h1>
      <p>{data.description}</p>
      <strong>👀 {data.subscribers_count}</strong>{" "}
      <strong>✨ {data.stargazers_count}</strong>{" "}
      <strong>🍴 {data.forks_count}</strong>
    </div>
  );
}
```

### [공식문서 보러가기](https://tanstack.com/query/latest/docs/react/overview)
