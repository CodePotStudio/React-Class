1-7번까지의 과정을 그대로 따라해보고, 그 것에 대한 생각을 정리하여 code-pot github에 PR을 보내 주세요
 * import 와 export
    * 모듈
        - 분리된 파일의 이름 ( 함수, 변수 등 사용하는 코드)
        - 모듈 내의 값들을 외부로 내보내기 (export), 다른 모듈에서 값을 불러오기 (import)도 가능.
        - 반드시 export가 되어야 import가 가능.
        - ex) App.js
            import { useState } from "react";
            => react라는 모듈에서 useState라는 함수를 가져오겠다는 의미
        - 위와 같은 코드가 있다면 react.js에서는
            export function useState( ... ){
                ...
            } => react에서 useState 함수를 내보낸다는 의미
    * sample1.js 를 만들어서 export const fruits = ["사과","감","배"]; fruits상수 외부로 내보내기를 하고
        기존 App.js에 vs에서는 일일이 작성하지않고 fruits 작성하고 추천을 해주는걸 엔터치면 import { fruits } from "./sample1";이 자동으로 작성된다. 여기서 ./은 같은 폴더위치에서 파일을 찾는다는 의미.
        ** { } 중괄호 중요!!
        만약에 상수이름을 변경하고 싶다면, import { fruits as fruitsName } from "./sample1"; 과 같이
        변경을 원하는 이름 뒤에 as라는 예약어를 사용하고 변경하고 싶은 이름을 작성해서 console.log로 확인해보면 값이 확인이 되어진다.
 * 퀴즈 데이터 분리하기
    App.js 에있는 const quizzes 를 constants.js 새로운 파일을 만들어서 const QUIZZES로 외부 모듈에 분리.
    여러가지 상수들을 넣기위해 디폴트값으로 export설정하지않고 { }로 설정해준다.
    App.js에서는 import { QUIZZES } from "./constants"; 설정하고 이름이 변경되어 App.js안에 quizzes를 전부 QUIZZES로 변경해준다.
 * 버튼 컴포넌트 분리하기
    App.js를 components안으로 옮겼기때문에 index.js에서 App위치 "./components/App"로 수정해준다.
    이와같이 import "./App.css";를 import "../App.css";로 변경해주고 App.css에서도 App위치를 수정해주는 것처럼 호출하는 모듈의 경로를 바꿔 준다.
    css는 한번만 사용하기때문에 import만 입력해서 설정한다.
    내용안에서의 button태그를 Button으로 변경해주고, Button 컴포넌트를 App.js에 import해준다.
    tip // ES6에서는 폴더에 index.js 파일이 있으면 import문에 index.js를 지정하지 않고 폴더에서 암묵적으로 가져오기를 수행할 수 있다.
 * props: property의 줄임말로 컴포넌트에 넘겨줄 속성을 의미
 * Button컴포넌트에 text 속성을 적용하려면 const Button = (props) => { return <button>{props.text}</button>;} 로 설정해준다. 여기서 실행을 해보면 버튼이 이름이 알맞게 나오지만 다음페이지로 안넘어가므로 onClick props로 {props.onClick} 설정해준다.
 * 모든 button의 css로 설정하기에는 범용적이라서 button의 class를 적용해서 해당class에서만 이용될 수 있도록 설정 해준다.
    해당 className을 answer로 설정하여 css를 .answer로 변경해준다.
    .answer 설정한 css를 Button.css로 옮겨주고 거기에 import "./Button.css"; 설정하면 적용이되어 css분리 완료.
    만약에 중복으로 .answer로 설정을 할 수 있기에 개발자들끼리 BEM Convention을 지키려 하지만 모든 완벽하게 막기는 어렵다.
    * BEM Convention
        - 작명규칙(Naming Convention) : 소문자, 숫자 만 이용해서 작명 & 여러단어 조합은 -으로 연결
        - 블록(Block) : 형태(red, big)가 아닌 목적(menu, button)에 맞게 결정
        - 요소(Element) : block__element 형태로 사용 (더블 언더바)
        - 수식어(Modifier) : 블록이나 요소의 모양(color, size..), 상태(disabled, checked..)를 정의 &  block — modifier 형태로 사용(더블 하이픈)
            블리언 타입 : 수식어가 있으면 값이 true로 가정. (form__button — disabled)
            키-벨류 타입 : 키, 벨류를 하이픈으로 연결하여 표시. (color-red, theme-ocean)
            * 수식어는 단독으로 사용할 수 없고, 기본 블록과 요소에 추가하여 사용해야함.
        - 혼합사용 (Mix) : block1, block2__element 형태로 사용할 수 있다.
        BEM방법이 편할수도 있지만 프로젝트의 규모나 성격에 따라 팀원과 규칙을 정의해서 입맛에 맞게 변형해서 사용하는 것이 효율적일 수 있다.
 * class이름을 중복해서 사용할 수 있어서 고유하게 만드는 컨셉이 CSS Module이다.
    다만 단점은 모든 컴포넌트에 변수를 공유하기가 어렵고 css로 원하는 속성를 넘겨주기가 번거롭다.
    해결위해 나온 것이 CSS in Javascript이고 styled-component, emotion이 있다.
    - styled-component는 터미널에 패키지를 설치해서 styled를 import한다.
    각각 컴포넌트를 분리해서 설정하여 적용을 해주고 각 해당되는 모듈의 import와 export를 설정해준다.
    모든 컴포넌트를 다분리하면 App.css의 스타일이 필요없으나 body 태그의 폰트가 남아 styled component의 globalStyle을 활용해서 globalStyle 파일을 생성해서 외부로 내보내줘서 설정해준다.
    아직 결과 값까지는 페이지가 한페이지만 나와 완벽하게 나오지는 않지만 거의 완성된 기분이라 뿌듯하다.

    [간단한 퀴즈 앱 만들기 과제] 추후에 추가적으로 올리겠습니다!<br>