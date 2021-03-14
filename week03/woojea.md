# 3주차 Review

## import와 export
> ```import``` 가져오기, ```export``` 내보내기
- export 방법들
    - ```export const sayHi = () => console.log("hi");```
    - ```export { fruits, sayHello, sayHi };``` 

### import 시 함수나 변수의 이름 바꾸기
- ```import { fruits as fruitsName, sayHello, sayHi } from "sample1";``` **as라는 예약어 사용**
- export에도 ```as```를 사용할 수 있다.

### import 시 중괄호 유무차이 
> ```export default``` 로 내보내기를 하게 되면 import할 때 {} 없이 import가 가능하다. 여러 변수/함수들을 내보낼 때는 ```export```로 해준다.
- ```import {Table}``` Table이라는 변수/함수 가져오기
- ```import Table``` export default된 것 가져오기

<hr>

## Button 컴포넌트 분리하기
- Component 밑에 Button 폴더를 만들 때 **React가 대문자만 JSX로 인식**하기 때문에 반드시 대문자로 만들어주기 !

- ```Button```폴더에서 Button파일을 따로 만들지 않고 ```index.js``` 파일에서 ```export default Button```을 해주면 ```import Button```을 해올 수 있다.
-  **ES6에서는 폴더에 index.js 파일이 있으면 import문에 index.js를 지정하지 않고 폴더에서 암묵적으로 가져오기를 수행할 수 있다.**

### props
> ```props```는 property의 줄임말로 컴포넌트에 넘겨줄 속성을 의미한다.


<hr>

## 컴포넌트에 스타일 입히기

- 컴포넌트 별로 클래스 이름이 고유하지 않기 때문에 문제가 발생할 수 있다. 코드가 많아지고, 협업 하는 사람이 많으면 많을수록 문제가 가능성이 더 높아진다.
- 해결방법: ```BEM Convention```, ```CSS Module```, ```CSS in Javascript```, ```CSS in CSS```

### BEM Convention
> CSS 클래스네임을 어떻게 지으면 좋은지에 대한 CSS방법론 중 하나.

- 개발, 디버깅, 유지보수를 위하여 CSS 선택자의 이름을 가능한 한 명확하게 만드는 것이 목표.
- **소문자, 숫자 만을 이용해서 작명**

```jsx
.header__navigation--navi-text {
  color: red;
}
```
- 위 코드에서 ```header```는 **Block**, ```naviagtion```은 **Element**, ```navi-text```는 **Modifier**
- BEM은 Block, Element, Modifier를 뜻한다.
- BEM은 기본적으로 **ID를 사용하지 않으며, class만을 사용**한다.
- '어떻게 보이는가'가 아니라 **'어떤 목적인가'**에 따라 이름을 짓는다.
- 이름을 연결할 때는 ```block-name```과 같이 하이픈 하나만 써서 연결한다.

#### Block 
> 재사용 가능한 기능적으로 독립적인 페이지 컴포넌트
- **블록은 환경에 영향을 받지 않아야 한다. 즉, 여백이나 위치를 설정하면 안된다.**
- 블록은 서로 중첩해서 작성 할 수 있다.
    - ```.header>.logo```는 header 블럭 안에 logo 블럭이 들어간 형태

#### Element
> 블록안에서 특정 기능을 담당하는 부분. 블럭은 독립적인 형태인 반면, 엘리먼트는 **의존적인** 형태이다.
- 자신이 속한 블럭 내에서만 의미를 가지기 때문에 블럭 안에서 떼어다 다른 데 쓸 수 없습니다.

```jsx
<form class="search-form">
    <input class="search-form__input"/>
    <button class="search-form__button">Search</button>
</form>
```
- 위 예시에서 ```.search-form```은 블럭이고, ```.search-form__input```과 ```.search-form__button```은 엘리먼트. search-form이란 블럭은 떼어내서 요기조기 마음껏 붙여도 됩니다. 하지만 내부의 input과 button은 검색을 위한 인풋창이자 버튼이기 때문에, search-form 안에서만 존재 의미가 있는 엘리먼트입니다.

- 엘리먼트 또한 중첩이 가능. 특징으로는 예를들어 ```.block > .block__element1 > .block__element2``` 구조에서 ```.block_element2```를 ```.block_element1```의 하위 엘리먼트로 보지 않고 둘 다 똑같이 ```.block```의 엘리먼트로 취급한다.
- 따라서 **클래스네임에 캐스케이딩을 여러번 표시할 필요가 없다.**
- 
```jsx
// BEM에서는 이렇게 사용하지 않는다
<form class="search-form">
  <div class="search-form__content">
      <input class="search-form__content__input"/>
      <button class="search-form__content__button">Search</button>
  </div>
</form>
```
```jsx
// 올바른 예
<form class="search-form">
  <div class="search-form__content">
      <input class="search-form__input"/>
      <button class="search-form__button">Search</button>
  </div>
</form>
```

#### Modifier
> 블럭이나 엘리먼트의 속성을 정의. 불리언(boolean) 타입과 키-밸류(key-value) 타입이 있다.

```jsx
<ul class="tab">
  <li class="tab__item tab__item--focused">탭 01</li>
  <li class="tab__item">탭 02</li>
  <li class="tab__item">탭 03</li>
</ul>
```
- 위 예제는 boolean타입으로 수식어가 있으면 값이 true 라고 가정한다. (```--focused```가 수식어)

```jsx
<div class="column">
  <strong class="title">일반 로그인</strong>
  <form class="form-login form-login--theme-normal">
    <input type="text" class="form-login__id"/>
    <input type="password" class="form-login__password"/>
  </form>
</div>
 
<div class="column">
  <strong class="title title--color-gray">VIP 로그인 (준비중)</strong>
  <form class="form-login form-login--theme-special form-login--disabled">
      <input type="text" class="form-login__id"/>
      <input type="password" class="form-login__password"/>
  </form>
</div>
```
- key-value 타입은 ```-```로 연결해 표시한다. 여기서는 ```color-gray```과 ```theme-normal```
       
<hr>

## 컴포넌트에 스타일 입히기 (고급)

### CSS Module
> Class 이름을 고유하게 만들기 위해 나온 것
- CSS 파일 이름 앞에 module을 붙여 사용.
    - 예를들어 ```Button.css``` 파일을 ```Button.module.css```로 이름을 바꿔준다.
-  ```css.module```을 사용할 때는 CSS를 import하여 그곳에 있는 class를 직접 입력해 주어야 한다.
    - ```import styles from "./Button.module.css";``` 로 css를 import 해온 뒤, ```className={styles.answer}```로 클래스에 적용

- 하지만 ```CSS Module```방식은 모든 컴포넌트에 변수를 공유하기가 어렵다.

### CSS in Javascript 中 styled-components

- ```npm install styled-components```로 패키지를 설치해준 뒤 ```import styled from "styled-components";```해서 사용
- CSS에서 변수를 사용해 ```props```와 ```styled-component```를 조합해 더 다양하게 사용가능하다.

<hr>

### Theming (컴포넌트들 간에 값 공유하기)
> 다양한 컴포넌트에서 ```style``` 관련된 값들을 공유할 수 있도록 만든 기능

<hr>

## 컴포넌트 더!더!더! 분리하기

### props.children
> 내부에 있는 컴포넌트까지 렌더링할 때 사용하는 것

- ex)
```const Box = () => <div>Hello!</div>;```
```jsx
const App = () => {
    return (
                <Box>
                    <button>버튼</button>
                </Box>
    }
}
```
- 이 경우 ```Hello```만 나타나고 ```button```은 나타나지 않는다.
  
```jsx
const Box = (props) => <div>Hello {props.children}</div>;
```

위와 같이 ```props.children```을 활용하면, ```Hello```와 ```button``` 모두 렌더링된다.

<hr>

- 후기 : themeing, CSS Moudle 등 새로운 것도 배우고 CSS에 대해 부가적인 것도 더 찾아보면서 좀 더 성장하고 이해할 수 있었던 것 같다 :)