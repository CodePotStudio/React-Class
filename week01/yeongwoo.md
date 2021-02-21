## 저번 주 복습내용!
저번주에 배웠던 내용들 중에서 내가 잘 모르는 내용들만 가져와서 정리해봤다.

### 📍 JSX
`JSX`는 `React`에서 `HTML`을 쉽게 사용할 수 있게하는 문법이다.
브라우저는 `HTML`, `CSS`, `JavaScript`만 인식할 수 있는데, `JSX`는 `babel`이라는 라이브러리를 통해 브라우저가 문법을 이해할 수 있도록 도와준다.

우리가 편하게 사용 하는 문장을 예로 들자
```javascript
function App(){
    return(
        <div>Hello</div>
    )
}
```
이대로 browser에게 보여주면 에러를 뿜을 것이다. 
`babel`은 해당코드를 다음과 같이 바꿔준다.
```javascript
function App() {
    return React.createElement('div', null, 'Hello');
}

```

그렇다면, 우리가 작성한 코드를 어디에 그려주는지 살펴보자.
`index.js`파일에 들어가면 다음과 같은 코드가 있다.
```javascript
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```
여기서 `ReactDOM.render` 함수의 역할은 정해진 위치에 원하는 컴포넌트를 렌더링하는 것이다.
`document.getElementById('root')` 코드를 해석하면

>1. `html`에서 `id`가 `root`인 엘리먼트를 찾는다
>2. 찾은 엘리먼트에 `App` 컴포넌트를 렌더링한다.

또, `public - index.html`에서 `<div id="root"></div>` id=root를 다른 이름으로 변경한다면 에러를 뿜는다.

---

### 📍 event
event는 어떤 사건을 의미한다. 브라우저에서의 사건이란 사용자가 클릭했을 때, 스르롤 할 때, 필드의 내용을 바꿀 때와 같은 것을 의미한다. 

>1. event target: `target`은 이벤트가 일어날 객체를 의미한다. 예를 들어 버튼을 누르면 새로운 창이 열리는 객체가 있다고 하자. 그러면 여기서 버튼은 `event target`이 된다.
>2. event type: 이벤트의 종류를 의미한다. 스크롤이나, 마우스가 움직였을 때 발생하는 것들도 모두 이벤트 타입이다.
>3. event handler: 이벤트가 발생했을 때 동작하는 코드를 의미한다.

react에서 event를 처리하는 방식은 DOM 엘리먼트에서 이벤트를 처리하는 방식과 매우 유사한데, 몇 가지 문법차이는 다음과 같다.
>1. React의 이벤트는 소문자 대신 캐멀 케이스를 사용한다.
>2. JSX를 사용하여 문자열이 아닌 함수로 이벤트 핸들러를 전달한다.

또, React에서는 `false`를 반환해도 기본동작을 방지 할 수 없다. 
따라서, `preventDefault`를 명시적으로 호출해야하는데, 
예를 들어 일반 `HTML`에서 새 페이지를 여는 링크의 기본 동작을 방지하기 위해 다음과 같은 코드를 작성할 수 있다.
```javascript
function handleClick(e) {
    e.preventDefault();
    console.log('The link was clicked.');
  }
```

만약 다음과 같은 함수를 사용하면 `event`를 반환할 수 있다.(자주 사용하는 함수만 가져옴)
>1. 마우스 이벤트: onClick, onDrop ...
>2. 키보드 이벤트: onKeyDown, onKeyUp, onKeyPress
>3. 폼 이벤트: onChange, onSubmit, onInput...

그렇다면, 이벤트가 발생했을 때 해당 엘리먼드의 값을 가져오려면 어떻게 할까? 
>1. button에 value값을 넣어주고 value값을 가져온다.
>2. 이벤트 핸들링 함수에서 event를 받는다.

다음과 같이 작성 할 수 있다.
```javascript
const eventHandle = (e) => {
  console.log(e.target.value)
}

return(
<>
  <button onClick = {eventHandle} value='1'></button>
  <button onClick = {eventHandle} value='2'></button>
  <button onClick = {eventHandle} value='3'></button>
</>  
)
```

---

### 📍 '==' vs '==='
python에서 코딩테스트를 풀다보면 `i=0`, `i==0`인 코드가 자주 나온다.
여기서의 `=`은 할당 연산자로, 우항에 있는 변수를 좌항에 있는 변수로 선언할때 사용한다. 즉, 변수를 선언할때 주로 사용한다.
`==`는 비교 연산자로, 두 객체(object: 숫자, 문자열, 리스트, 튜플 ...)의 값이 같은지 비교하고 같으면 True, 다르면 False를 출력한다.

그럼 javaScript에서 '=='와 '==='의 차이는 뭘까?
`==`는 동등 연산자로 피연산자가 서로 다른 타입이면 타입을 강제로 변환하여 비교한다. (추상적 비교)
`===`은 일치연산자로 두 피연산자를 정확하게 비교한다. (엄격한 비교)
따라서, 특별한 경우가 아니라면 ==보다는 ===을 쓰도록 하자.

---

### 📍 튜터에게 드릴 말씀
>1. 복습한 내용 중 코드의 반복이 많았던 `button` 컴포넌트에 `map`함수를 사용하여 코드를 간결하게 구현했습니다.
  * <a href ='https://github.com/YWTechIT/quiz_project/pull/1/files'>YW_techIT Github</a>
>2. 이번 프로젝트의 주제는 `병과(군사특기) 성향 테스트`를 해보고 싶습니다. 다른 성향테스트를 많이 찾아봤지만 비슷비슷한것들이 많았는데 유독 군대 관련한 테스트는 없었습니다. 남자들이라면 한번씩 재미삼아 테스트하지 않을까 싶은 목적으로 만들고싶네요!
>3. typescript로 코드를 작성하려고 참고자료의 `velopert`님을 따라하는데 조금 어렵네요 혹시 타입스크립트 관련해서 추천해주실만한 강의나 서적이 있을까요?!
