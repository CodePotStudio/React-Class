## week 3️⃣: 저번주 복습내용

### 드릴말씀 
> 이번주까지는 배웠던 내용을 토대로 복습하고 다음주부터는 프로젝트위주로 복습하겠습니다!! 
> 항상 스터디원들을 위해 노력해주셔서 감사드립니다. 👍🏽 👍🏽

## ✏️ 서론
`Quiz_app` 프로젝트의 전체적인 윤곽은 만든것 같고 이번주부터는 `Code Refactoring`위주로 복습을 했다.
수업을 들으면서 `Code Refactoring`을 잘 하는 개발자가 되고 싶다는 생각을 했다. 
왜냐하면, `Code Refactoring`을 할 때 내가 알고있는 개발의 모든것을 압축(?) 담는 기분이 든다.
또, 같은 동작을 하는 코드지만 짧고 간결하고 가독성있는 코드를 볼 때 희열(?)감을 느낀다.~~(변태는 아니다.)~~
알고리즘을 풀면서 `pythonic`한 코드를 짜는것과 비슷한것 같다.

---
## ✏️ 본론

### 📍 모듈
프로그래밍관점에서의 ` 모듈 `은 본체에 독립된 하위 단위이다. 
즉, 자주 사용되는 코드를 별도의 파일로 만들어서 필요할 때마다 재활용하는것이 모듈화의 목적이다.

초기 스크립트는 크기도 작고 기능도 단순했기 때문에 한 파일에 모든 코드를 작성했지만, 스크립트의 크기가 커지고 기능도 복잡해지면서 스크립트를 모듈화(기능별로 코드를 나눔)해서 필요할 때마다 불러올 수 있게 하는 과정을 겪었다.

이는 `react`에서도 마찬가지인데 코드가 길어질때 같은 코드를 다른파일에 옮겨두고 컴포넌트로 선언하게 되면 코드가 짧아지고 가독성이 좋아지는 장점이 있다.

분리된 파일의 이름을 `모듈(module)`이라고 하는데, 이때 모듈 내에서 함수나 변수 등등 코드에서 사용하는 모든것을 나눌 수 있다.
모듈을 통해 코드를 외부에서 참조할 수도있고, 반대로 다른 모듈에서 해당 모듈의 값을 불러올 수도 있다.

예를들어 `title.js`의 모듈을 부르고 싶을땐 다음과 같이 사용 할 수 있다. 

`title.js`에서는 `export default title`로 내보낼 수 있고 불러올때는 불러오고싶은 모듈에서 `import { title } from 'title.js'`처럼 원하는 모듈을 불러올 수 있다.

보통 모듈을 선언할때는 한번 선언해놓으면 값이 자주 변하지 않는 상수값(constant)들을 모듈로 만든다. 
이때, 첫글자를 대문자로 선언하도록 하는 센스는 잊지말자.

모듈을 만들다보면 `import` 경로를 설정할때 에러가 종종 발생하는데 경로설정은 다음과 같이 설정할 수 있다.
>1. `/`: 현재 드라이브의 루트(root)
>2. `./`: 현재 디렉토리
>3. `../`: 현재 디렉토리의 부모

또, 내가 불러오고 싶은 변수를 사용할 때 `as(alias)`문법을 사용할 수 있는데 파이썬에서 모듈을 호출할때 `as`를 사용하는것과 비슷하다.
```
# javascript
import * as say from './say.js';

# python
import pandas as pd
```

---
### 📍 컴포넌트의 분리
컴포넌트를 분리할때 알아두면 좋은 점이 있는데, ES6에서는 폴더 안에 `index.js`파일이 있으면 `import`코드에 `index.js`를 작성하지 않고도 폴더 내에서 암묵적으로 호출 할 수있다.

예를 들면 다음과 같이 설정 할 수 있다.
`import Button from './Button';`

### 📍 props
props는 `property`의 줄임말로 컴포넌트끼리 넘겨주는 속성을 의미한다. 

만약, 다른 경로에 선언했던 컴포넌트 속 변수를 현재 컴포넌트에서 사용하고 싶다면, `props`라는 문법을 사용해 `Button`컴포넌트에 속성으로 넘겨주면 `props`라는 변수 안에 보관된다. 

하나 주의 할 점은 현재 컴포넌트에서 다음과 같이 `props`를 붙여줘야 한다.

```javascript
import React from 'react';

const Button = (props) => {
return <Button>{props.text}</button>
}

export default Button;
```

`javascript` 코드 뿐만아니라 `CSS`파일도 같이 넘겨 줄 수 있는데 마찬가지로 상단에 `import './Button.css;'`를 사용하면 된다.

하지만 이런 `CSS module`의 경우에는 단점이 몇 가지 존재하는데,

>1. 모든 컴포넌트에 변수를 공유하기 어렵다
`background`속성은 한 컴포넌트가 아닌 모든 컴포넌트에 선언되어야할 기능이다. 
이러한 단점을 극복하기위해 `SASS`, `SCSS` 같은 CSS 전처리 언어(Pre - Processor)를 사용한다.
(전처리 언어를 통해 변수, 함수, 상속 등 일반적인 프로그래밍 개념을 사용하여 해결 할 수 있다.)

>2. css로 원하는 속성을 넘겨주기 번거롭다.
컴포넌트의 속성에 따라 동적으로 `style`을 변경시키기 어렵다.

이러한 단점들을 극복하기위해 `CSS in Javascript`가 나왔는데, 대표적으로 `styled-component`, `emotion`등이 있다. 우리는 `styled-component`를 사용해 리팩토링을 해보자.

`패키지 설치(yarn add styled-components)`하고 나서 `styled`를 `import`해주자. 

사용법은 다음과 같다. `CSS`를 적용할 컴포넌트 마지막에 `=styled.component`를 선언한다.

```javascript
const Button = styled.button`
font-size: 16px;
color: #ffffff;
background-color: #7362ff;
border-radius: 5px;
border: 0px;
height: 56px;
padding: 4px;
margin: 4px;
cursor: pointer;
width: 100%;
outline: none;
font-weight: 700;
&:hover {
background-color: #a99fee;
}
`
```

`styled` 내부에는 `HTML` 태그들이 포함되어있다.

다음과 같이 `style`을 적용시킨 `styledButton` 컴포넌트를 기존 컴포넌트에 넣어주면 리팩토링이 끝난다.

```javascript
const StyledButton = styled.button`
font-size: 16px;
color: #ffffff;
background-color: #7362ff;
border-radius: 5px;
border: 0px;
height: 56px;
padding: 4px;
margin: 4px;
cursor: pointer;
width: 100%;
outline: none;
font-weight: 700;
&:hover {
background-color: #a99fee;
}
}`;

const Button = (props) => (
<StyledButton onClick={props.onClick}>{props.text}</StyledButton>
);

export default Button;
```

또, CSS에서 JSX문법인 삼항연산자를 통해 `font-size`별로 폰트크기를 조정할 수 있다.
예를들어 `fontSize`가 `big`은 32px, `default`는 16px로 설정 할 수 있다.

```javascript
// components/Button/index.js
const StyledButton = styled.button`
font-size: ${(props) => (props.fonSize === "big" ? "32px" : "16px")};
}
`;
```

위 `style component`에서 사용한 템플릿 리터럴 ` ``(backtick)`은 내장된 표현식을 허용하는 문자열 리터럴이다. 여러 줄로 이루어진 문자열과 문자 보간기능을 사용 할 수 있고 변수를 취급할 때는 변수 앞에 ${}를 붙여주면 된다.

```javascript
let a = 5
let b = 10
console.log(`a + b = ${a + b}`)
```

### 📍 Container 컴포넌트 만들기
`App.js`를 보면 `container` 컴포넌트 안에 `{props.children}` 코드를 볼 수 있다. 이는, 내부에 있는 컴포넌트까지 렌더링 할때 사용하는 문법이다. 컴포넌트 안에 컴포넌트의 내용들도 같이 넘겨주고 싶을 때는 `{props.children}`를 사용하도록 하자.

---
## ✏️ 결론

지금까지 컴포넌트 리팩토링을 진행하면서 같은 성능을 내는 코드지만 더욱 코드를 간결하게 만들고 가독성을 높였다. 
하지만 이것중에도 부족한 점이 있는데

1. 페이지가 하나뿐이다.
2. props로 데이터를 공유한다.
다음시간에는 랜딩페이지와 `useContext`를 활용하여 전체 컴포넌트간에 데이터를 공유하는법에 대해 배워보자.






