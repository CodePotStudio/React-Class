# 절대 경로와 상대경로 

## 절대경로와 상대경로 

1. 절대주소란?
- 정적인 문자열로 특정 컴퓨터의 파일 위치를 가르키는 경로를 말한다.
- ex ) /home/usr/ubuntu/workspace/mypage/env/templates/mypage.html

2. 상대주소란?
- 현재 디렉토리(비교 대상)를 기준으로 작성된 경로 
- ex ) mypage.html
- /: 루트 디렉토리
- ./: 현재 위지 참조
- ../: 현재 위치의 상위 폴더 참조

- 웹에서 사용할 경우에는 현재 접속중인 URL 뒤에 추가된다.
- ex) http:// myblog.io에서 a src="profile"링크 클릭 시 http://myblog.io/profile로 이동한다.

# 이해
- mypage.html에서 /env 하위 폴더인 /static/background.jpg에 접근하고 싶은 경우 

1. /home/usr/ubuntu/workspace/mypage/env/static/background.jpg(절대경로)
2. ../static/backround.jpg (상대경로)
3. /env/static/background.jpg (웹서버를 통한 접속 시의 절대 경로)

## Flex

- Flex는 Flexible Box,Flexbox라고 불리기도 합니다.
- Flex는 레이아웃 배치 전용 기능으로 고안되었습니다.
- 레이아웃을 만들 떄 딱히 사용할게 없어서 쓰던 float나 inline-block등을 이용한 기존 방식보다 훨씬 강력하고 편리한 기능이 많습니다.
- Grid로도 Flex와 똑같이 구현할 수 있는 경우가 많지만 Grid로는 구현이 어렵거나 Flex를 쓰는게 더 편리한 경우도 있습니다.
- 인터넷 익스플로어 같은 경우에는 Flex 또는 표준 스펙을 지원하지만 Grid는 legacy(고인물) 버전만 지원합니다.
- Flex 레이아웃을 만들기 위한 기본적인 HTML 구조는 다음과 같습니다.

```jsx
<div class="container">
	<div class="item">helloflex</div>
	<div class="item">abc</div>
	<div class="item">helloflex</div>
</div>
```
- 부모 요소인 div.container를 Flex Container(플렉스 컨테이너)라고 부릅니다.
- 자식 요소인 div.item들을 Flex Item(플렉스 아이템)이라고 부릅니다.
- 컨테이너가 Flex의 영향을 받는 전체 공간이며 설정된 속성에 따라 각각의 아이템들이 어떤 형태도 배치되는 것이라 생각하면 됩니다.
- Flex 의 속성은 컨테이너에 적용하는 속성, 아이템에 적용하는 속성으로 나뉩니다.

1. 컨테이너에 적용하는 속성
- display:flex;
```jsx
.container {
	display: flex;
	/* display: inline-flex; */
}
```
- Flex아이템들은 가로 방향으로 배치되고 자신이 가진 내용물의 width만큼만 차지합니다.(inline)
- height는 컨테이너의 높이만큼 늘어납니다.
- height가 알아서 늘어나는 특징은 컬럼 레이아웃을 만들때 편리합니다.
- inline-flex는 block과 inline-block의 관게를 생각하면 됩니다.
- inline-flex는 inline-block처럼 동작합니다.
- 아이템들이 배치된 방향의 축을 메인축(Main Axis)으로 합니다.
- 메인축과 수직인 축을 수직축 또는 교차축(Cross Axis)라고 부릅니다.

## 배치 방향 설정 (flex-direction)

- 아이템들이 배치되는 축의 방향을 결정하는 속성입니다.
```jsx
.container {
	flex-direction: row;
	/* flex-direction: column; */
	/* flex-direction: row-reverse; */
	/* flex-direction: column-reverse; */
}
```
## row (기본값)
- 아이템들이 행(가로) 방향으로 배치됩니다.

## row-reverse
- 아이템들이 역순으로 가로 배치가 됩니다.

## column
- 아이템들이 열(세로) 방향으로 배치됩니다.
- block요소들을 쌓아놓은것처럼 보입니다.

## column-reverse
- 아이템들이 역순으로 세로 배치가 됩니다.
- column으로 배치하다가 일정한 폭 이상이 되면 row로 바꿔주는 식으로 반응형 레이아웃을 구현할 수 있습니다.

## 줄넘김 처리 설정 flex-wrap

```jsx
.container {
	flex-wrap: nowrap;
	/* flex-wrap: wrap; */
	/* flex-wrap: wrap-reverse; */
}
```

## nowrap (기본값)
- 줄바꿈을 하지 않습니다. 

## row-reverse
- 아이템들이 역순으로 가로 배치됩니다.

## column
- 아이템들이 열(세로) 방향으로 배치됩니다.

## column-reverse
- 아이템들이 역순으로 세로 배치 됩니다.

## 줄넘김 처리 설정 flex-wrap
- 컨테이너가 더 이상 아이템들을 한 줄에 담을 여유 공간이 없을 때 아이템 줄바꿈을 어떻게 할지 결정하는 속성입니다.
```jsx
.container {
	flex-wrap: nowrap;
	/* flex-wrap: wrap; */
	/* flex-wrap: wrap-reverse; */
}
```

## nowrap (기본값)
- 줄바꿈을 하지 않습니다. 넘치면 그냥 삐져 나가요.

## wrap
- 줄바꿈을 합니다. float이나 inline-block으로 배치한 요소들과 비슷하게 동작합니다.

## wrap-reverse
- 줄바꿈을 하는데, 아이템을 역순으로 배치합니다. 

## flex-flow
- flex-direction과 flex-wrap을 한꺼번에 지정할 수 있는 단축 속성입니다.
- flex-direction, flex-wrap의 순으로 한 칸 떼고 써주시면 됩니다.
```jsx
.container {
	flex-flow: row wrap;
	/* 아래의 두 줄을 줄여 쓴 것 */
	/* flex-direction: row; */
	/* flex-wrap: wrap; */
}
```

## 메인축 방향 정렬 justify-content
```jsx
.container {
	justify-content: flex-start;
	/* justify-content: flex-end; */
	/* justify-content: center; */
	/* justify-content: space-between; */
	/* justify-content: space-around; */
	/* justify-content: space-evenly; */
}
```

## flex-start (기본값)
- 아이템들을 시작점으로 정렬합니다.

## flex-end
- 아이템들을 끝점으로 정렬합니다.

## center
- 아이템들을 가운데로 정렬합니다.

## space-between
- 아이템들의 “사이(between)”에 균일한 간격을 만들어 줍니다.

## space-around
- 아이템들의 “둘레(around)”에 균일한 간격을 만들어 줍니다.

## space-evenly
- 아이템들의 사이와 양 끝에 균일한 간격을 만들어 줍니다.
- IE와 엣지(Edge)에서는 지원되지 않습니다👎

## 수직축 방향 정렬 align-items
- 수직축 방향으로 아이템을들 정렬하는 속성입니다.
```jsx
.container {
	align-items: stretch;
	/* align-items: flex-start; */
	/* align-items: flex-end; */
	/* align-items: center; */
	/* align-items: baseline; */
}
```

## stretch (기본값)
- 아이템들이 수직축 방향으로 끝까지 쭈욱 늘어납니다.

## flex-start
- 아이템들을 시작점으로 정렬합니다.

## flex-end
- 아이템들을 끝으로 정렬합니다.

## center
- 아이템들을 가운데로 정렬합니다.

## baseline
- 아이템들을 텍스트 베이스라인 기준으로 정렬합니다.

## 여러 행 정렬 align-content
- flex-wrap: wrap;이 설정된 상태에서, 아이템들의 행이 2줄 이상 되었을 때의 수직축 방향 정렬을 결정하는 속성입니다.
```jsx
.container {
	flex-wrap: wrap;
	align-content: stretch;
	/* align-content: flex-start; */
	/* align-content: flex-end; */
	/* align-content: center; */
	/* align-content: space-between; */
	/* align-content: space-around; */
	/* align-content: space-evenly; */
}
```
-  space-evenly는 MS 계열 브라우저(IE, 엣지)에서는 지원되지 않습니다

2. 아이템에 적용하는 속성들

 ## 유연한 박스의 기본 영역 flex-basis
 -  Flex 아이템의 기본 크기를 설정합니다(flex-direction이 row일 때는 너비, column일 때는 높이).
 ```jsx
 .item {
	flex-basis: auto; /* 기본값 */
	/* flex-basis: 0; */
	/* flex-basis: 50%; */
	/* flex-basis: 300px; */
	/* flex-basis: 10rem; */
	/* flex-basis: content; */
}
 ```

- flex-basis의 값으로는 우리가 width, height 등에 사용하는 각종 단위의 수가 들어갈 수 있습니다.
- 기본값 auto는 해당 아이템의 width값을 사용합니다.

## 유연하게 늘리기 flex-grow
- flex-grow는 아이템이 flex-basis의 값보다 커질 수 있는지를 결정하는 속성입니다.
```jsx
.item {
	flex-grow: 1;
	/* flex-grow: 0; */ /* 기본값 */
}
```
- flex-grow에 들어가는 숫자의 의미는, 아이템들의 flex-basis를 제외한 여백 부분을 flex-grow에 지정된 숫자의 비율로 나누어 가진다고 생각하시면 됩니다.
```jsx
/* 1:2:1의 비율로 세팅할 경우 */
.item:nth-child(1) { flex-grow: 1; }
.item:nth-child(2) { flex-grow: 2; }
.item:nth-child(3) { flex-grow: 1; }
```

## 유연하게 줄이기 flex-shrink

- flex-shrink는 flex-grow와 쌍을 이루는 속성으로, 아이템이 flex-basis의 값보다 작아질 수 있는지를 결정합니다.
- 몇이든 일단 0보다 큰 값이 세팅되면 해당 아이템이 유연한 (Flexible)박스로 변하고  flex-basis보다 작아집니다.

```jsx
.item {
	flex-basis: 150px;
	flex-shrink: 1; /* 기본값 */
}
```
```jsx
.container {
	display: flex;
}
.item:nth-child(1) {
	flex-shrink: 0;
	width: 100px;
}
.item:nth-child(2) {
	flex-grow: 1;
}
```

## flex
- flex-grow, flex-shrink, flex-basis를 한 번에 쓸 수 있는 축약형 속성입니다.

```jsx
.item {
	flex: 1;
	/* flex-grow: 1; flex-shrink: 1; flex-basis: 0%; */
	flex: 1 1 auto;
	/* flex-grow: 1; flex-shrink: 1; flex-basis: auto; */
	flex: 1 500px;
	/* flex-grow: 1; flex-shrink: 1; flex-basis: 500px; */
}
```
- flex: 1; 이런 식으로 flex-basis를 생략해서 쓰면 flex-basis의 값은 0이 됩니다.
```jsx
.item {
	flex: 1 1 0;
}
.item:nth-child(2) {
	flex: 2 1 0;
}
```
- 2단 컬럼의 사각형 목록을 만들면 다음과 같습니다.
```jsx
.container {
	display: flex;
	flex-wrap: wrap;
}
.item {
	flex: 1 1 40%;
}
```
## 수직축으로 아이템 정렬 align-self

- align이니 수직축 정렬입니다.
```jsx
.item {
	align-self: auto;
	/* align-self: stretch; */
	/* align-self: flex-start; */
	/* align-self: flex-end; */
	/* align-self: center; */
	/* align-self: baseline; */
}
```

## 배치 순서 order
- 아이템들의 시각적 나열 순서를 결정하는 속성입니다.
```jsx
.item:nth-child(1) { order: 3; } /* A */
.item:nth-child(2) { order: 1; } /* B */
.item:nth-child(3) { order: 2; } /* C */
```

## z-index
- z-index로 Z축 정렬을 할 수 있어요. 숫자가 클 수록 위로 올라옵니다.
```jsx
.item:nth-child(2) {
	z-index: 1;
	transform: scale(2);
}
/* z-index를 설정 안하면 0이므로, 1만 설정해도 나머지 아이템을 보다 위로 올라온다 */

```

## useEffect 

### TLDR (Too Long; Didn’t Read)

1. useEffect 로 componentDidMount 동작을 흉내내려면 어떻게 해야하는가?
- useEffect(fn, []) 으로 가능합니다. 
- 콜백 안에서도 초기 prop과 state를 확인할 수 있습니다. 
- 이펙트를 다루는 멘탈 모델은 componentDidMount 나 다른 라이프사이클 메서드와 다르다는 점을 인지하셔야 합니다.

2. useEffect 안에서 데이터 페칭은 어떻게 해야할까? 두번째 인자로 오는 배열([]) 은 뭐지?
- [] 는 이펙트에 리액트 데이터 흐름에 관여하는 어떠한 값도 사용하지 않겠다는 뜻입니다.
- 한번 적용되어도 안전하다는 뜻이기도 합니다. 
- 잘못된 방식으로 의존성 체크를 생략하는 것 보다 의존성을 필요로 하는 상황을 제거하는 몇 가지 전략을(주로 useReducer, useCallback) 익혀야 할 필요가 있습니다.

3. 이펙트를 일으키는 의존성 배열에 함수를 명시해도 되는걸까?
- prop이나 state를 반드시 요구하지 않는 함수는 컴포넌트 바깥에 선언해서 호이스팅합니다.
- 이펙트 안에서만 사용되는 함수는 이펙트 함수 내부에 선언하는 겁니다. 
- 만약에 랜더 범위 안에 있는 함수를 이펙트가 사용하고 있다면 (prop으로 내려오는 함수 포함해서), 구현부를 useCallback 으로 감싸세요. 
-  함수는 prop과 state로부터 값을 “볼 수” 있습니다. 

4.  왜 가끔씩 데이터 페칭이 무한루프에 빠지는걸까?
- 이펙트 안에서 데이터 페칭을 할 때 두 번째 인자로 의존성 배열을 전달하지 않았을 때 생길 수 있는 문제입니다.
- 이게 없으면 이펙트는 매 랜더마다 실행됩니다. 
-  state를 설정하는 일은 또 다시 이펙트를 실행합니다.
- 사용하고 있는 의존 값을 지우는 일은(아니면 맹목적으로 [] 을 지정하는 것은) 보통 잘못된 해결법입니다. 

5. 이펙트 안에서 이전 state나 prop 값을 참조할까?
- 자신이 정의된 블록 안에서 랜더링이 일어날 때마다 prop과 state를 “지켜봅니다”. 
- 이렇게 하면 버그를 방지할 수 있지만 어떤 경우에는 짜증날 수 있습니다.
- 명시적으로 어떤 값을 가변성 ref에 넣어서 관리할 수 있습니다.
- 랜더링 될때마다 prop이나 stat가 보인다면 아마도 의존성 배열에 값을 지정하는 것을 깜빡했을 것입니다.

### 모든 랜더링은 고유의 Prop과 State가 있다

```jsx
function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```
-  `count` 는 그저 숫자입니다. 마법의 “데이터 바인딩” 이나 “워쳐” 나 “프록시”, 혹은 비슷한 그 어떤 것도 아닙니다. 그냥 아래와 같이 단순한 숫자에 불과합니다.

```jsx
const count = 42;
// ...
<p>You clicked {count} times</p>
// ...
```