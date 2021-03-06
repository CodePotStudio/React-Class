## week 2️⃣: 저번주 복습내용

## 📍 문법복습

### ⚡️ Scope Function(화살표 함수)
>1. 화살표 함수 표현은 `function` 표현에 비해 구문이 짧고 자신의 this, arguments, super, new.target을 바인딩하지 않는다.
>2. 화살표 함수는 항상 익명이다.
>3. 함수 표현은 메소드 함수가 아닌 곳에 가장 적합하다.
>4. 생성자로서 사용할 수 없다.
>5. 화살표 함수는 매개변수가 1개 일 때, 소괄호는 생략가능하다.
>6. 화살표 함수 내부에서 바로 `return`하는 경우, 대괄호는 생략가능하다.

```javascript
// 인자가 1개 일 때

function square(n){
    return n*n
}

function square(n){
    n*n
}

const square = n => {
    return n*n
}

const square = n => n*n
square(10)

// 인자가 2개 일 때
function sum(a, b){
    return a+b
}

function sum(a, b){
    a+b
}

const sum = (a, b) => {
    return a+b
}

const sum = (a, b) => a+b
```

> reference
> 1. <a href='https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/Arrow_functions'>MDN_Arrow_functions</a>
> 2. <a href='https://react.codepot.kr/docs/week02/doc1'>code_pot</a>

---
### ⚡️ Map
> 1. `map()` 메소드는 배열 내의 모든 요소 각각에 대하여 주어진 함수를 호출한 결과를 모아 새로운 배열(list)을 반환한다.
> 2. `callback` 함수는 호출될 때 대상 요소의 값, 그 요소의 인덱스, 그리고 `map`을 호출한 원본 배열 3개의 인수를 전달받는다.
> 3. `map`은 호출한 배열의 값을 변형하지 않는다. `callback`에 의해 변형될 수는 있다.

```javascript
// 배열
const fruits = ['apple', 'banana', 'kiwi', 'orange']

console.log(fruits.map(fruit => fruit))
👉🏽 ["apple", "banana", "kiwi", "orange"]0: "apple"1: "banana"2: "kiwi"3: "orange"

// 배열에 들어있는 숫자들을 제곱해서 새로운 배열을 만들기
const numbers = [1, 2, 3, 4, 5]

console.log(numbers.map(number => number * number))
👉🏽 (5) [1, 4, 9, 16, 25]
```

map 함수의 단순화과정

```javascript
// 선언
const fruits = ['사과', '배', '키위'];

function sayFruit(element){
    console.log(element)
}

// 2번
fruits.map(function sayFruit(element) {
    console.log(element)
})

// 3번
fruits.map((element) => {
    return console.log(element)
})

// 4번
fruits.map(element => console.log(element))

```
> reference
> 1. <a href='https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map'>MDN_array_map</a>
> 2. <a href='https://react.codepot.kr/docs/week02/doc2'>code_pot</a>

---
### ⚡️ Destructuring assignment
> 배열이나 객체의 속성을 해체하여 그 값을 개별 변수에 담을 수 있게 하는 JS표현식

객체 내에 있는 변수값들을 외부로 꺼내려고 할때, `.`, `[]`로 객체의 이름으로 접근하여 값을 가져올 수 있다.
하지만, 이 과정에서 변수를 중복하여 사용하고, 가져와야하는 속성이 많아 질수록 코드의 중복이 많아진다.
이때 주의해야 할 점은 <span style='color:blue'>중괄호 안에 추가된 속성명을 사용해야한다.</span>

객체에서 정의된 변수명을 변경하고 싶을때는 `{속성명: 새로운 변수명}`을 입력하여 변경 할 수 있다.
이때는 `객체`처럼 `key값`이 없기때문에 순서에 맞춰 선언하면된다.

비구조할당은 배열에서 `[]`를, 객체에서는 `{}`를 사용하는 점을 잊지말자.

```javascript
// 배열: 비구조 할당
const foo = ['one', 'two', 'three'];
const [one, two] = foo;

console.log(one)
console.log(two)

// 객체: 비구조 할당
const info = {
    name: 'AYW',
    age: 27,
    address: 'Hwaseong',
    phone: '010-1234-1234'
}

console.log(info.name)
console.log(info.age)
console.log(info.address)
console.log(info.phone)

const {name, age, address, phone} = info;
console.log(name)
console.log(age)
console.log(address)
console.log(phone)
```

이외에도 `map` 함수를 대체할 수 있는 배열 내장함수는 다음과 같다.
1. forEach
2. indexOf
3. findIndex
4. find
등등...

> reference
> 1. <a href='https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment'>Map MDN</a>
> 2. <a href='https://learnjs.vlpt.us/basics/09-array-functions.html'>GitBook_ 배열 내장함수</a>

---
## 💡 추가 문법복습

### ⚡️ 객체(object)의 기본
객체는 관련된 데이터와 함수(일반적으로 여러 데이터와 함수)로 이루어지는데, 객체 안에 있을 때는 보통 프로퍼티(property)와 메소드(method)의 집합이다. 

객체의 기본적인 패턴은 다음과 같다.
```javascript
const objectName = {
    member1Name: member1Value,
    member2Name: member2Value,
    member3Name: member3Value,
}
```
객체(object)에서 한 쌍의 구분은 `,`으로, `key, value`값의 구분은 `:`으로 분리된다. 

객체를 구성하는 멤버의 값은 어떤 것이라도 될 수 있는데, 다음의 예제를 살펴보자.

```javascript
const person = {
  name: ['Bob', 'Smith'],
  age: 32,
  gender: 'male',
  interests: ['music', 'skiing'],
  bio: function() {
    alert(this.name[0] + ' ' + this.name[1] + ' is ' + this.age + ' years old. He likes ' + this.interests[0] + ' and ' + this.interests[1] + '.');
  },
  greeting: function() {
    alert('Hi! I\'m ' + this.name[0] + '.');
  }
};

```

우리가 생성한 `person` 객체는 문자열, 숫자, 2개의 배열과 2개의 함수로 구성되어있다. 

여기서 `문자열(string), 숫자(number), 2개의 배열`은 객체의 프로퍼티(property, 속성)이라고 부르고, 끝에 2개의 함수는 객체의 메소드(method)라고 부른다.

### ⚡️ 객체(object)의 접근
객체내에 값에 접근하려면 `.`을 사용해 접근하고자 하는 항목을 적으면 된다. 간단한 프로퍼티의 이름이 될 수 있고, 배열의 일부 또는 객체의 메소드를 호출 할 수 있다.

위의 예제를 통해 값을 호출해보자.
```javascript
person.name
👉🏽 (2) ["Bob", "Smith"]
person.interests[0]
👉🏽 "music"
person.bio()
```

또, 객체 내부의 객체로 설정 할 수 있는데 
`.` 표기법과 `[]`표기법으로도 접근이 가능하다.

```javascript
const person = {
    name:{
        first: 'bob',
        second: 'kim'
    }
}

person.name.first
person['name']['first']
👉🏽 bob

person.name.second
person['name']['second']
👉🏽 kim
```

### ⚡️ 객체(object)멤버 설정
설정할 멤버를 간단히 명시하여 갱신하는것도 가능하다.
```javascript
person.age = 45;
person['name']['third'] = 'AYW';
```

> reference
> 1. <a href='https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects/Basics'>MDN_Objects</a>
> 2. <a href='https://react.codepot.kr/docs/week02/doc1'>code_pot</a>
---

### ⚡️ DRY원칙
> Don't Repeat Yourself

프로그래밍에 있어 무의미한 반복은 금기시된다.
소스 코드 중복, 무분별한 낭비, 반복은 누군가의 시간, 노력, 효율을 다방면에 걸쳐 큰 손실을 준다.

> 2. <a href='https://medium.com/@covj12/dry-%ED%8C%A8%ED%84%B4%EC%9D%98-%EC%9D%98%EB%AF%B8-b2332d255610'>medium_DRY원칙의 의미</a>

---
## 📍 프로젝트 복습
>1. `<button>` 코드 단순화시키기

위에서 배웠던 `map`함수를 사용해서 코드를 단순화 시켰다. 
`map`을 사용하기위해서 객체를 생성해 문제를 추가했다.
또, 객체내부의 값에 접근할때는 `.`을 사용해 접근했다. (`Quiz.text`)

>2. `event`값에 매개변수 넘기기

기존에 정답판정은 만약 text값이 ~일때 정답, 오답으로 간주했다.
하지만, 문제가 많아지게되면 하드코딩으로 작성해야하기때문에 코드가 길어지게 되고 이것은 곧 비효율적인 결과를 나타낸다.

이를 개선하기위해서 기존의 함수에 `true`, `false`값을 넘겨 정답판정을 하면 긴 코드를 작성하지 않고도 해결 할 수 있다.

그래서 각 문제마다 `isCorrect`를 변수로 선언하여 `true, false` 값을 넘기게끔 작성했다.

여기서 주의할 점은 화살표 함수를 쓰지않고 `<button onClick={handleClick(answer.isCorrect}>`을 작성하게되면 `<button>` 컴포넌트를 그릴 때 곧바로 함수를 실행하기 때문에 원하는 기능이 나타나지 않는다.

따라서, 버튼을 누를 때만 작동할 수 있게 화살표 함수를 넣어주자.

>3. 여러퀴즈 렌더링하기
코드 중간에 `0번째 중 0번째`코드가 있다.
그런데, 문제가 바뀔 때마다 해당 `index`도 변경되어야한다.
이럴때는 `useState`를 통해 편하게 사용 할 수 있는데, `state`는 컴포넌트 내부에서만 관리되고, 컴포넌트 렌더링에 영향을 미치는 객체이다. 즉, `state`가 변경되면 `state`가 속한 컴포넌트가 다시 랜더링되기때문에 값이 바뀔 수 있다.

여기서 주의 할 점은
<span style='color:blue'>state를 직접 수정하지 말자</span> 

직접 `state`를 수정하게 되면 `react`에서 변경을 인지하지 못하기 때문에 렌더링이 일어나지 않는다.

<span style='color:blue'>독립적인 state는 분리하여 사용하자.</span> 

그래서 `handleClick` 함수에 `setCurrent`라는 `useState`를 추가해서 버튼이 실행될때마다 +1이 되도록 설정했다.
`state`가 변경됐기 때문에 렌더링이 일어나게 되고 현재 id값은 증가했기 때문에 문제가 바뀌어 보이게 된다.

>4. 퀴즈 결과 페이지 보여주기
결과페이지를 보여주는 기능은 조금 생각해보면 쉽게 해결책을 떠올릴 수 있다.
만약, 문제를 다 풀고 결과페이지로 이동한다고 가정하자. 이때, 컴퓨터가 언제 결과페이지를 보여주게 설정할 수 있을까? 

여러가지 방법이 있겠지만, 현재페이지가 `quiz.length-1` 이면 결과페이지를 보여주게 설정하면 간편하다. 저번주에 배웠던 삼항연산자를 이용해 설정하자.

>5. 결과 페이지에 점수 표시하기
점수를 표시할때는 지금까지 맞춘 정답의 점수를 `length`로 나누고 * 100을 해주면 된다.
이때에도, `score`를 보여주는 변수에 `useState`를 사용하면 관리하기 편하다.

---

## 📍 튜터님께 드릴 말씀
>1. 이번주는 없습니다!
>2. quiz 문제만 살짝 변형해서 혼자 복습해봤습니다.
<a href='https://github.com/YWTechIT/quiz_project_practice/pull/1/files'> YWtechIT_git </a>