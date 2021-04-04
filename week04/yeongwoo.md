## 📍 3주차 복습

스터디를 한 주 쉬니까 수업시간에 했던 내용들이 잘 기억이 나지 않아 3주차 영상을 보고 2번정도 혼자서 코드를 작성하면서 복습했다. 
처음에 할 때는 이해가 잘 안갔는데 두번째 복습하니까 이해가 잘 됐다.

3주차의 주된 내용은 다음과 같았다.
`App.css`에 있는 CSS들을 필요한 각각의 `component` 목적에 맞게끔 적용하는것. 그래서 `App.css`파일이 없더라도 CSS가 적용되게끔 하는것이 목적이었다.

하지만, 이러한 리팩토링(refactoring) 작업을 거칠때는 왜?(why?) 그것을 하는지 알아야한다고 생각한다.
그래서 정리해봤다. CSS in CSS와 CSS in JS 차이점.
다음 마크다운에도 적혀져있지만 내용을 계속해서 작성하기 위해 결론부터 설명하자면 각각의 js파일에서 편하게 CSS로 속성을 넘겨주기 위해서 사용한다.

리팩토링의 큰 틀은 다음과 같다.
>1. Constant(QUIZZES) 선언
>2. Button Component refactoring, Theming
>3. 겹치는 CSS들 분리
>4. Global CSS 선언

---
### ❏ CSS in CSS와 CSS in JS 비교하기
> 성능 초점: CSS in CSS(CSS module)
> 개발 생산성: CSS in JS(SASS, styled-components, emotion)

성능구현에 초점을 맞출 때 사용하는 CSS in CSS 중 `CSS module`을 살펴보자.
`CSS module`은 CSS를 특정 `component`에서만 적용하고 싶을 때 주로 사용한다. 이런 경우 외부 CSS에서 내부 CSS의 변수네임과 동일할 때 값이 내부 CSS까지 변경되는데 `CSS module`은 이를 `hash`값으로 변경해주어 CSS의 `unique`함을 보장해준다.

그러나 모든 `component`에 CSS를 적용하고 싶거나 CSS로 원하는 속성을 넘겨주기 번거로울 때(`background-color`의 경우) 그럴때는 `CSS module` 대신 `styled-components`, `emotion`과 같은 CSS in JS를 사용하면 된다. 

`CSS in JS`방법으로 CSS를 작성하면 `Global Namespace, Dependencies, Dead Code Elimination, Minification, Sharing Constants, Non-deterministic Resolution, Isolation` 등등 `Pure CSS`로 작성했을 때의 문제점들을 보완하는 기능들을 가지고 있다.

이쯤되면, 무조건 `CSS in JS`를 써야겠네?!라고 생각할 수 있는데, 무비판적인 수용은 웹사이트의 크기가 커질 때 잠재적인 버그를 일으킬 수 있다. 몇 가지의 단점들 중 가장 치명적인 단점은 `번들 size`가 커진다. 

빠르게 보여줘야하는 웹사이트일수록 사이트의 전체 사이즈가 작아져야하는것은 모두 알고있을 것이다. 만약, `CSS in JS` 중 별도의 라이브러리인 `styled-components`를 추가로 설치한다고 가정했을때 이는 번들 사이즈의 크기가 커진다는 말과 도잉ㄹ하다. 번들사이즈의 크기가 커지면 다운로드 시간이 길어지므로 초기 진입이 느려진다. `CSS in JS`의 경우 `JS`가 모두 로딩된 후에 `CSS`코드가 생성되기 때문에 더욱 느려질 수 있다. 이럴때 SSR(Server Side Rendering)으로 해결 할 수 있다고 생각하지만, 동적 인터렉션이 필요한 웹사이트라면 번들 파일을 내려받기 전에 CSS기능이 제대로 구현되지 않을 수 있다.

앞서 살펴본 내용을 토대로 간략하게 정리를 하자면, 인터렉션이나 속도가 중요한 웹사이트라면 `CSS-in-CSS`를, 반대로 관리자 페이지나 위키같이 정적인 웹사이트라면 `CSS-in-JS`를 사용하는것이 더 낫다.

하지만 둘 중 어떤 방식이 더 낫다고 단정 할 수 없으며, 서비스의 용도와 목적에 따라 적절한 선택이 필요하다. 단지, CSS-in-JS가 유행이라고해서 맹목적으로 사용한다면 결국, 서비스의 품질을 떨어뜨리는 결과를 만들 수 있다.

>reference: 
1. <a href='https://blueshw.github.io/2020/09/14/why-css-in-css/#sassscss%EC%99%80-css-modules%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EC%9E%90'>CSS-in-JS에서 CSS-in-CSS로 바꿔야 하는 이유</a>
2. <a href='https://blueshw.github.io/2020/09/14/why-css-in-css/#sassscss%EC%99%80-css-modules%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EC%9E%90'>CSS-in-JS(Styled Components) vs CSS-inCSS(CSS Modules) 성능 비교</a>

---
### ⚡️ 순서별 적용 방법

---
#### 1️⃣ Constant(QUIZZES) 선언
지금까지 우리는 `App.js`에 `QUIZZES`를 선언했다. 그런데, `QUIZZES`는 잘 변하지 않는 값이기 때문에 상수(Constant)로 취급하여 다른 파일에 보관하면 `App.js` 코드의 가독성이 좋아질 것이다. 방법은 단순하다. 새로운 파일에 `QUIZZES`값을 넣고 `export, import`를 적용하자.

---
#### 2️⃣ Button Refactoring
다음은 버튼 리팩토링인데, 우리는 `Button`이란 폴더를 만들고 그 안에 `index.js` 이름의 파일을 만들것이다. 이유는 ES6에서 `index.js` 파일이 있으면 이름을 지정하지 않고도 폴더에서 암묵적으로 가져오기 때문이다.

다음 버튼 리팩토링의 세부적인 순서는 다음과 같다.

>1. HTML코드 작성
`Button` 컴포넌트를 만들고 `HTML`코드를 넣어주자

>2. `styled-component`라이브러리를 이용해 `CSS`를 작성한다.
이후 `ButtonWrapper` 컴포넌트를 만들고 그 안에 `button CSS`를 넣어준다.
전체적인 틀은 다음과 같다.

```javascript
const ButtonWrapper = styled.div`
// ... Button CSS ...
`
const Button = ({text, handleClick, fontSize}) => {
  return <ButtonWrapper onClick={handleClick} fontSize={fontSize}>{text}</ButtonWrapper>;
};
```

>3. 삼항연산자를 이용해 `styled-component` 변수를 설정 할 수 있다.
대표적으로 다크모드 기능을 구현할 때 사용되는 기능이다. 정해진 변수를 넣으면 그에 맞게 변환하는 기능이다. `styled-component`안에 적용가능하다.
```javascript
const ButtonWrapper = styled.div`
font-size: ${(props) => (props.fontSize === 'Big' ? '32px' : '16px')};
`
```

>4. `theme`을 사용해 전체 `App.js` 코드에 원하는 색상을 부여할수있다.
`theme`은 다양한 컴포넌트에서 `style` 관련한 값들을 공유할 수 있는 기능인데, 전역변수로 설정할때 사용하면 편한 기능이다.
`theme`파일을 하나 만들고 `props`로 값을 넘길 수 있다.

주의 할 점은 `App.js` HTML 전체 코드에 `<ThemeProvider theme={theme}></ThemeProvider>`를 선언해줘야 모든 컴포넌트에 넘겨줄 수 있다. 

```javascript
// theme.js
const theme = {
    primaryColor100: "#7362ff",
    primaryColor80: "#a99fee",
};

export default theme;

// button.js
const ButtonWrapper = styled.div`
background-color: ${(props) => (props.theme.primaryBackGroundColor100)};
`
```

---
#### 3️⃣ 겹치는 CSS 분리
겹치는 CSS라는 말은 `App.js`파일안에 `className`을 모두 `component`화 시켜주는 것이다. 이러한 작업을 하게되면 결과적으로 코드의 가독성이 좋아진다.

세부적인 순서는 다음과 같다.
>1. Question Section
>2. Answer Section
>3. Result Section
>4. Container Section

한 컴포넌트를 만들고 props로 값을 전달해준 뒤 그 안에 컴포넌트를 선언하면 하단의 사진처럼 `App.js`가 깔끔하게 보인다.

![](https://images.velog.io/images/abcd8637/post/ef99cc71-a1c5-4ffa-8f5c-c06599603ecb/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-03-17%2021.56.05.png)

---
#### 4️⃣ global style선언
3번까지 진행했으면, `app.css`파일에 남아있는 코드는 `body`코드 일 것이다. 
`body`는 특정 `component`가 아닌 전역변수로 설정해줘야하는 값이기때문에 `theme`처럼 모든 `HTML`을 감싸줘야한다.
새로운 파일을 만들고 해당 파일에 `globalStyle`값을 넣어주자 마찬가지로 `export, import`를 해주면 쉽게 값을 꺼내 올 수 있다.

다음 사진은 `globalStyle` 컴포넌트로 전체 `HTML`를 감싸는 모습을 보여주는 사진이다. 이처럼 하면 쉽게 적용가능하다.

![](https://images.velog.io/images/abcd8637/post/87358884-233b-4707-a140-3afdfda1997b/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-03-17%2021.58.34.png)

---
#### 5️⃣ 결론
지금까지 `refactoring` 작업을 진행했다. 강의로 들을 때는 쉬워보였는데 막상 내 손으로 처음부터 진행하려니까 막히는 부분도 많았고 삽질하는 부분도 많았다. 

하지만, 여전히 부족한 점도 있는데 이는 다음주에 배워보도록 하자.
>1. 페이지가 하나 뿐이다.
>2. props로 데이터를 공유한다.

---
## 📍 4주차 복습
이번주는 각 페이지별로 URL을 만들어서 각각의 기능들을 만들어보자. 만들어야하는 URL은 다음과 같다.
1. 랜딩페이지: `/`
2. 퀴즈페이지: `/quiz`
3. 결과페이지: `/result`

이를 위해 크게 순서를 나눠보면..
> 퀴즈페이지 나누기 -> 랜딩페이지 나누기 -> 결과페이지 만들기 -> Quiz, result페이지 연결하기 -> 결과페이지로 이동시키기 -> 결과 초기화하기 과정을 거쳐야한다.

본론으로 들어가기 전에 전통 웹페이지와 SPA의 차이를 알아보자면, 전통적인 웹페이지는 URL에 맞춰 HTML을 내려주고, 브라우저가 렌더링을 한다. 반면, SPA는 최초 페이지로 접근할 때 모든 HTML, CSS, JavaScript를 받아오고, SPA 프레임워크가 각 URL에 따라 필요한 부분만 업데이트하는 구조를 보인다.

그리고 이번 과정은 `ReactRouter`를 이용하는데, `ReactRouter`에는 `Browser Router`와 `Hash Router`가 존재한다. 

이 둘의 차이점을 간단하게 살펴보면

### HashRouter
1. 주소에 해쉬(#)가 붙는다.
2. 검색 엔진이 읽지 못한다.
3. URL 해쉬를 서버에서 읽을 수 없기 때문에 SSR으로 설정을 백업 할 수 없다.
4. Hash History를 지원하지 않는다.

### BrowserRouter
1. Link 컴포넌트로 to 속성에 이동할 경로를 써준다.
2. Route 컴포넌트 path 속성을 Link의 to 속성을 component mapping 경로를 기술한다.
3. 새로고침을 하면 경로에서 못 찾아 에러가 난다.
4. History API를 사용할 수 있다.

### ⚡️ 순서별 적용 방법
---
#### 1️⃣ 퀴즈 페이지 나누기
URL로 라우팅을 해야하기 때문에 `app.js`에는 라우팅 코드만 남겨두고 다른 코드들은 가독성을 위해 `component`를 만들어 따로 보관해주자.

퀴즈가 보이는 페이지를 `QUIZ` 컴포넌트를 만들어 따로 보관해준다. 이때 모든 `state`와 `event Handler`까지 퀴즈에만 사용하는 기능이기때문에 전부 옮겨주자. 다음으로 Route 컴포넌트를 만들어 링크를 설정해주자.
```javascript
const App = () => {
    return(
        <Router>
            <Route path='/quiz' component={Quiz} /> 
        </Router>
    )
}
```

---
#### 2️⃣ 랜딩 페이지 만들기
랜딩 페이지는 검색 엔진, 광고 등을 경유하여 접속하는 이용자가 최초로 보게되는 웹페이지다. 따라서 랜딩페이지로 처음 웹페이지를 선보이는만큼 깔끔하고 가독성이 좋아야한다. 

깔끔해보이도록 `img`를 넣을려고 하는데 `react`에서는 `img`를 추가하는 방법이 기존 `javascript`와 조금 다르다. img 변수명을 정하고 img가 들어있는 경로를 작성해주자.

```javascript
import cover from '../../img.jpg'>

<img src={cover} />;
```

`img`를 설정할 때 작은 팁이 있는데 `img`보다 `div`설정이 작으면 `img`가 영역밖으로 튀어나올 경우가 있다. 
이를 방지하기 위해 다음 코드를 추가해주자.
```javascript
const Image = styled.img`
max-width: 100%;
display: block;
`
```
3주차에서 공부했던 `theme`을 통해 원하는 색을 입혀줄 수도 있다.

---
#### 3️⃣ 결과 페이지 만들기
결과 페이지는 지금까지 만들었던 방법과는 조금 다른데 사용자가 성향 검사를 종료하고 결과가 나올 때 누군가에게 공유하기 위해서는 결과페이지만의 URL을 따로 생성해야한다. 

기존의 `state`로 결과 페이지를 만들고 새로고침을 하게되면 다시 처음으로 돌아가기 때문이다. 최종 점수를 보여주는 변수인 `convertedScore`는 `result` 컴포넌트에서 새로 만들자.

---
#### 4️⃣ Quiz와 Result 페이지 연결하기
3번의 과정으로 통해 `Result` 컴포넌트를 새로 생성했다. 하지만 여기서 문제가 생겼는데, `Quiz`에 들어있는 state인 `score`는 `Result`에 들어있는 `convertedScore`를 사용하기 위해 필요한 변수이다. 

그러나, 동등한 컴포넌트에서는 `state`를 `props` 해 줄 수 없기 때문에 `redux` 혹은 `상위 component`를 통해 변수를 전달해줘야한다. 

여기서는 `redux`대신 상위 컴포넌트인 `app.js`로 변수를 보내고 `props`의 절차를 밟아주자.

그러면 `props`로 받은 `score`값을 바탕으로 `convertedScore`를 만들 수 있다.

다음과 같이 작성가능하다.
```javascript
const App = () => {
    const [score, setScore] = useState(0)
    return(
        <Router>
            <Route>
                <Quiz setScore={setScore}></Quiz>
            </Route>
            <Route>
                <Result score={score}></Result>
            </Route>
        </Router>
    )
}
```

이렇게 변수를 전달해줘도 결과 page가 제대로 계산되지 않는다. 이는 마지막 퀴즈에서 버튼을 클릭 할 때 `/result` 페이지로 이동하지 않았기 때문이다.
이는 `useHistory Hook`을 이용하여 간단하게 해결 할 수 있다.

---
#### 5️⃣ 결과 페이지로 이동하기
`Quiz` 컴포넌트에서 `history` state를 선언하고 함수에 다음과 같이 작성해주자.

이때 `history` 변수를 `let`으로 정했는데, 객체가 자주 변경되기 때문에 `let`으로 설정했다.

```javascript
import { useHistory } from 'react-router';

const Quiz = () => {
    let history = useHistory();

    const handleClick = (isCorrect) => {
        if (isCorrect) {
            setScore((score) => score + 1)
        }
        if (currentNo === QUIZZES.length -1){
            history.push('/result')
        }else{
            setCurrentNo((currentNo) => currentNo + 1)
        }
    }
}
```
정상적으로 페이지가 이동하는것을 볼 수 있지만, 테스트를 다시하게되면 이전테스트의 점수를 누적하여 결과가 표시된다. 이를 수정해보자.

---
#### 6️⃣ 결과 초기화하기
결과를 초기화 시키려면 점수를 보여주는 `state`의 값을 0으로 초기화 시키는 설정을 해야한다. 언제? `테스트 다시하기`버튼을 누를 때
그러나, 점수를 보여주는 `setScore`는 `QUIZ`컴포넌트에 있다. 

따라서 `Result` 컴포넌트에도 값을 추가하려면 3번 방법과 마찬가지로 상위 컴포넌트 `App.js`에서 설정해줘야한다. 

이후 `result`에서 테스트 다시하기 버튼의 내부 값을 조정해주자.

```javascript
// App.js
const App = () => {
    const [score, setScore] = useState(0)
    return(
        <Router>
            <Route>
                <Quiz setScore={setScore}></Quiz>
            </Route>
            <Route>
                <Result score={score} setScore={setScore}></Result>
            </Route>
        </Router>
    )
}

// Result
const Result = () => {
    <Link to ='/'>
        <Button text = '테스트 다시하기' onClick={() => setScore(0)}>
    </Link>
}
```

이렇게 설정하면 정상적으로 기능이 구현되는것을 알 수 있다.

---
#### 7️⃣ 결론
하지만, 여기서 더 추가하고 싶은 기능이 있는데
1. 점수에 따른 다양한 결과 페이지 노출
2. 결과 로딩페이지 구현
3. 다른사람에게 공유할 때 메타 데이터 표현
이 기능들은 다음시간에 다시 공부하도록 하자.

이렇게 해서 3 ~ 4주차의 공부를 끝냈다.
1주차부터 코드를 작성하며 느낀것은 내가 만들고 싶은 기능은 어떻게든 찾아서 만들 수 있는데 해당 코드를 `refactoring` 할 때 생각보다 쉽지 않다는 점이다.

`refactoring`을 잘하는 개발자는 프론트엔드의 고수가 되기위한 조건이 아닐까 생각한다.

다시 1주차부터 `typeScript`를 이용해 만들어보고 싶지만, 지금 배우는 과정과 복습이 끝나고 해 볼 계획이다.
그 전까지는 배운것을 최대한 머릿속에 집어넣고 싶다.

이번주 복습 끝!

---
## 📍 질문
1. router코드로 컴포넌트를 감싸 줄 때 실행 결과는 같지만, 두 코드의 차이점이 있나요? 있다면 언제 사용하지 알고 싶습니다.
```javascript
// 1번
const App = () => {
    return (
        <Router>
            <Route path="/result" component={Result} />
            <Route path="/quiz" component={Quiz} />
            <Route path="/" exact component={Landing} />
        </Router>
    );
}

// 2번
const App = () => {
    return (
        <Router>
            <Route path="/result" component={Result} />
        </Router>
        <Router>
            <Route path="/quiz" component={Quiz} />
        </Router>
        <Router>
            <Route path="/" exact component={Landing} />
        </Router>
    );
}
```

2. `<Button>` 컴포넌트에 값을 넣을 때 왜 1번과 같이 선언하지 않고 2번과 같이 선언하나요??
```javascript
// 1번
const Result = () => (
    <Link to="/">
        <Button>테스트 다시하기</Button>
    </Link>
);

// 2번
const Result = () => (
    <Link to="/">
        <Button text="테스트 다시하기"></Button>
    </Link>
);
```