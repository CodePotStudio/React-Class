# 자바스크립트 웹 스토리지(localStorage, sessionStorage) 사용법

- 자바스크립트로 웹 개발을 하게 된다고 한다면 간단한 애플리케이션이라도 데이터를 저장해야 할 일이 생긴다.
- 이때 DB나 서버나 클라우드 플랫폼에 데이터를 저장하는 경우가 생깁니다.
- 데이터가 중요하지 않거나 유실되도 무방한 데이터라고 한다면 데이터를 저장하는 것이 낭비일 수 있습니다.

## 로컬 스토리지 vs 세션 스토리지

- 웹 스토리지(web storage)에는 로컬 스토리지 (localStorage)와 세션 스토리지 (session Storage)가 있습니다.
- 이 두 개의 매커니즘의 차이점은 데이터가 어떤 범위 내에서 얼마나 오래 보존되느냐에 있습니다.
- 세션 스토리지는 웹페이지의 세션이 끝날때 저장된 데이터가 지워집니다.
- 로컬 스토리지는 웹 페이지의 세션이 끝나더라도 데이터가 지워지지 않습니다.
- 브라우저에서 같은 웹사이트를 여러 탭이나 창에 띄우게 되면 세션 스토리지에 데이터가 서로 격리되어 저장됩니다.
- 이렇게 되면 각 탭이나 창이 닫힐 때 저장해둔 데이터도 함께 소멸됩니다.
- 로컬 스토리지의 경우 여러 탭이나 창 간에 데이터가 서로 공유되며 탭이나 창을 닫아도 데이터는 브라우저에 그대로 남아있습니다.
- `로컬 스토리지`의 데이터 영속성(persistence) 어디까지나 계속해서 동일한 컴퓨터에서 동일한 브라우저를 사용할 때만 해당합니다.
- 같은 컴퓨터에서 다른 브라우저를 사용하거나 (e.g. 크롬을 쓰다가 사파리를 쓰면) 다른 컴퓨터에서 같은 브라우저를 사용하는 경우  (e.g. 집에서 크롬을 쓰다가 회사에서 크롬을 쓰면)
- 다른 브라우저이므로 다른 두개의 로컬 스토리지에 데이터가 저장이 될 것입니다.
- 다른 기기나 브라우저 간에 데이터가 공유되고 영속되어야 한다면 클라우드 (Cloud) 플랫폼이나 데이터베이스 (DB) 서버를 사용해야 합니다.

- `로컬 스토리지와 세션 스토리지의 공통점은` 데이터를 브라우저 상에 저장한다는 것입니다.
- 자바스크립트 API가 완전히 동일한 형태입니다.

## 기본 API

- 웹 스토리지는 기본적으로 키(key)와 값(value)으로 이루어진 데이터를 저장할 수 있습니다.
- 해시 테이블 자료 구조를 생각하시면 이해가 쉬우실 것 같습니다.

```jsx
// 키에 데이터 쓰기
localStorage.setItem("key", value)

// 키로 부터 데이터 읽기
localStorage.getItem("key")

// 키의 데이터 삭제
localStorage.removeItem("key")

// 모든 키의 데이터 삭제
localStorage.clear()

// 저장된 키/값 쌍의 개수
localStorage.length
```

- 엄밀하게는 `window.localStorage`를 사용해야 하지만 `window` 객체의 대부분의 속성이 그러하듯 줄여서 `localStorage`로 로컬 스토리지 객체에 접근할 수 있습니다.

```jsx
> localStorage.getItem('name')
null
> localStorage.getItem('email')
null
> localStorage.setItem('email', 'test@user.com')
undefined
> localStorage.getItem('email')
"test@user.com"
> localStorage.setItem('email', 'test@admin.com')
undefined
> localStorage.getItem('email')
"test@admin.com"
> localStorage.removeItem('email')
undefined
> localStorage.getItem('email')
null
```

## 주의 사항

- 웹 스토리지를 사용할 때 주의해야할 부분은 오직 문자형(String) 데이터 타입만 지원한다는 것입니다.

```jsx
> localStorage.setItem('num', 1)
undefined
> localStorage.getItem('num') === 1
false
> localStorage.getItem('num')
"1"
> typeof localStorage.getItem('num')
"string"
```

- 이러한 웹 스토리지의 성질 때문에 객체형 데이터를 저장할 때 다음과 같이 큰 낭패를 볼 수 있습니다.

```jsx
> localStorage.setItem('obj', {a: 1, b: 2})
undefined
> localStorage.getItem('obj')
"[object Object]"
```

- 이런 문제가 발생하는 이유는 웹 스토리지는 문자열 데이터밖에 저장할 수 없고 또 다른 타입의 데이터를 저장하려고 한다면 문자형으로 변환을 하기 때문입니다.

```jsx
> String(1)
"1"
> String({a: 1, b: 2})
"[object Object]"
```

## 해결 방법

- 웹 스토리지를 사용할 때 많이 사용하는 방법이 JSON형태로 데이터를 읽고 쓰는 것입니다.

```jsx
> localStorage.setItem('json', JSON.stringify({a: 1, b: 2}))
undefined
> JSON.parse(localStorage.getItem('json'))
{a: 1, b: 2}
```

- 로컬 스토리지에 쓸 데이터를 JSON 형태로 직렬화(serialization)하고, 읽은 데이터를 JSON형태로 역직렬화 (deserialization)해주면 원본의 데이터를 그대로 얻을 수 있습니다.
- 배열형 데이터를 로컬 스토리지에 저장할 때도 동일한 방법으로 문제를 예방할 수 있습니다.

```jsx
> localStorage.setItem('nums', JSON.stringify([1, 2, 3]))
undefined
> JSON.parse(localStorage.getItem('nums'))
[1, 2, 3]
```

## 데이터 청소

- 로컬 스토리지에 저장된 데이터는 웹페이지를 닫는다고 해서 사라지지 않습니다.
- 불필요한 데이터가 남지 않도록 직접 청소하는 것이 좋습니다.

```jsx
> localStorage.length
5
> localStorage.key(0)
"email"
> localStorage.removeItem('obj')
undefined
> localStorage.length
4
> localStorage.clear()
undefined
> localStorage.length
0
```

- 브라우저의 개발자 도구를 통해서 웹 스토리지에 어떤 데이터가 저장되어 있는지를 쉽게 확인하고 삭제할 수 있습니다.


