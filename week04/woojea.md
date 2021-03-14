# 4주차 Review

## React에서 URL 다루기

- 전통적인 웹페이지의 경우, 각 URL로 HTML을 요청하면 각 URL에 맞추어 새로운 HTML을 내려주고, 브라우저가 렌더링해준다.
- SPA의 경우, 최초 페이지로 접근할 때 모든 HTML, CSS, Javascript를 받아오고, SPA 프레임워크가 각 URL에 따라 필요한 부분만 업데이트 하는 구조
- Routing : 정해진 url에 접근하면 url에 맞는 컴포넌트로 갈아 끼워 웹페이지를 재구성하는 것, 하지만 React에서는 기능을 따로 제공하지 않으므로 React Router 라이브러리를 사용한다.

- ```Router``` 컴포넌트는 ```Link```, ```Route``` 컴포넌트를 동작하기 위해 반드시 필요한 컴포넌트이다. Link, Route 컴포넌트는 반드시 Router를 상위 컴포넌트로 갖고 있어야 정상적으로 동작한다.

- 여러 ```Router```컴포넌트 중에서는 ```BrowserRouter```가 가장 많이 사용된다. 


### Route 컴포넌트 
- ```Route``` 컴포넌트는 정해진 URL로 고객이 접근하였을 때, 약속된 컴포넌트를 렌더링하는 기능을 제공

- 사용법
```jsx
// Route 컴포넌트 예시
<Route path="url 경로" component={렌더링할 컴포넌트} />

// 이렇게도 사용할 수 있습니다.
<Route path="url 경로">
    <렌더링할 컴포넌트 />
</Route>
```

- 예시
```jsx
import React from "react";
import { BrowserRouter as Router, Route } from "react-router-dom";

// Home, MyPage, About 컴포넌트 생성
const Home = () => <div>Home</div>;
const MyPage = () => <div>MyPage</div>;
const About = () => <div>About</div>;

// 각 URL로 보여줄 컴포넌트 매칭
const App = () => {
    return (
        <Router>
            <Route path="/mypage" component={MyPage} />
            <Route path="/about" component={About} />
            <Route path="/" exact component={Home} />
        </Router>
    );
};
```

### Link Component
- ```a```태그의 기본적인 속성은 페이지를 이동시키면서 페이지 전부를 새로 불러온다. 이로 인해 컴포넌트가 가지고 있는 모든 상태가 **초기화**됩니다. 이에 반해 ```Link``` 태그는 **브라우저의 URL만 바꾸고, 필요한 컴포넌트만 업데이트** 하기 때문에 ```a```태그와 같은 문제가 발생하지 않는다.

- 사용법
```jsx
<Link to="이동할 URL">링크 이름</Link>
```

- 예시
```jsx
import React from "react";
import { BrowserRouter as Router, Route, Link } from "react-router-dom";

// Home, MyPage, About 컴포넌트 생성
const Home = () => <div>Home</div>;
const MyPage = () => <div>MyPage</div>;
const About = () => <div>About</div>;

// 각 URL로 보여줄 컴포넌트 매칭
const App = () => {
    return (
        <Router>
            <ul>
                <li>
                    <Link to="/">Home</Link>
                </li>
            </ul>
            <Route path="/mypage" component={MyPage} />
            <Route path="/about" component={About} />
            <Route path="/" exact component={Home} />
        </Router>
    );
};

export default App;
```

### Switch 
- ```Switch```가 ```exact path``` 와 다른 점은 첫번째 매칭만 본다는 것

<hr>

## 결과 페이지로 이동시키기

### window.history & useHistory
- ```HTML``` ```window```객체에는 ```history```객체가 있다.
- ```React```에서는 ```history```객체를 사용할 때, ```React-Router```가 제공하는 ```useHistory``` hook을 사용한다.