# 1주차 Review

### React ?
> Javascript 라이브러리
1. SPA(Single Page Application) - 단 하나의 HTML 파일을 기반으로 javascript 를 이용해 동적으로 화면을 이리저리 컨텐츠를 바꾸는 방식의 웹 어플리케이션
2. Component 기반의 UI로 쉽게 재사용 가능
3. 여러 플랫폼에서 사용 가능



### npm vs yarn 
- npm은 자바스크립트 노드에서 node package manager의 약자로 런타임 동안 Node.js 환경에서 서로 다른 종류의 패키지를 관리하는 데 사용되는 기본 절차

- yarn은 페이스북에서 개발한 새로운 자바스크립트 패키지 매니저로 더욱 빠르고 안정적이며 보안성이 뛰어나다고 주장하며 등장했지만 최근들어 성능은 비슷

### create-react-app의 방법
- 익히 알고 있는 ```npx create-react-app```뿐 아니라 ```npm init react-app my-app```, ```yarn create react-app my-app```도 가능

### React에서 HTML을 다루는 방법
- JSX -> React에서 HTML을 쉽게 사용할 수 있는 문법
- React App을 최초 생성할 때, 설치되는 라이브러리 Babel이 JSX를 이해하게 해준다

### 표현식(expressions) vs 문장(statements)
#### 표현식
> 값을 산출해내는 코드의 조각
-  **JSX 내 에서는 표현식만 사용가능** 
-  따라서 **if문은 삼항연산자를 통해, for문은 map을 통해 사용**
```jsx
// 숫자 표현식
10;
10 + 20;

// 문자 표현식
("hello");
"hello" + "world";

// 논리 표현식
30 > 20;
10 < 20;

// 할당 연산자를 통한 표현식
i = 10;
total = 0;
fruits[1] = "avocado";

// 함수 호출 표현식
sayHello();
```

#### 문장
> 특정한 행동을 하겠다는 설명
```jsx
// 변수 선언
var sum;
var average;

// if, else 문
if (expression)
    statement 1
else
    statement 2

// for 문
for(let i = 0; i < 10; i++){
    console.log(i)
}
```

#### JSX사용시 주의사항
1. HTML처럼 반드시 태그 닫기
2. HTML과 달리 반드시 최상위 태그(부모 태그) 필요 -> ```<div>```,```<>```등으로 전체 HTML감싸기

<hr>

- 이번엔 첫주차로 기본기부터 다시 다진 느낌이었다 