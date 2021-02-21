1-7번까지의 과정을 그대로 따라해보고, 그 것에 대한 생각을 정리하여 code-pot github에 PR을 보내 주세요.
  * React를 사용하면 필요한부분만 업데이트되어 새로운 html업데이트로인한 지연을 늦출수 있다.
  * 내가 필요한 페이지만 로딩이 되는것이 SPA : Single Page Application라고 하고 속도가빠르다.
  * 서버 사이드 렌더링 과 클라이언트 사이드 렌더링 차이점
    - SSR은 중복된 html 계속생성하고 CSR은 새로운화면만 생성한다.
    - 다만 CSR의 단점은 첫로딩이 약간느리고 SEO 검색엔진 최적화가 잘안된다.
  * npm: node package manager 자바스크립의 노드의 약자다.
  * Yarn: npm의 단점을 보완하기위해서 만든 자바스크립트 패키지 매니저다.
  * 컴포넌트는 독립적이고 재사용 가능하도록 나눈 조각과 비슷함.
  * JSX는 React에서 HTML을 쉽게 사용할 수 있는 문법
    - function App() {
        return <div>Hello React!</div>;
      } 에서 App는 html을 그려주는 컴포넌트
    - babel은 JSX코드를 브라우저가 javascript로 이해할수있게 변환해준다.
    - ReactDOM.render(<App />, document.getElementById("root"));은
        App을 html에서 id가 root인곳에 적용해준다.
  * JSX에서 표현식은 사용가능하나 문장에서는 let, const외에는   
    사용불가능하다. 대체하기위해서는 map으로 사용해야한다.
    - JSX에서 변수를 넣으려면 선언한 변수를 { }로 감싸서 사용가능하다.
    - JSX를 babel을 이용하여 Javascript로 변환하기 위해서는 import React 
        from "react"를 꼭 적어야한다.
    - 태그열면 태그는 꼭 닫아야하고, 부모태그로 꼭 감싸서 사용해야하지만 
        넣기 싫으면 <></>로라도 감싸줘야한다.
    - const는 변수 재선언, 재할당이 불가능한 상수, let은 변수에 재할당이 
        가능한 상수.
  * React에서는 이벤트명에 camelCase를 사용해야한다.  * React에서는 이벤트명에 camelCase를 사용해야한다.
 
  // App.js

  import React from "react";
import "./App.css";

function App() {
  function handleClick(event){
    //alert('버튼 클릭')
    //console.log(event.target.value);
    const answer = event.target.value;
    if (answer === "디자인") {
      alert("당신은 LG그램을 구매하세요!!");
      }else if (answer === "가격") {
        alert("당신은 한성컴퓨터를 구매하세요!!")
      } else if (answer === "사양") {
        alert("당신은 맥북을 구매하세요!!");
    } else {
      alert("당신은 레노버노트북을 구매하세요!!");
      } 
  }
    return (
        <div className="container">
            <div className="app">
                <div className="question-section">
                    <h1 className="question-header">
                        <div className="question-headA">당신에게 알맞은 노트북은?</div>
                        <span>1</span>/5
                    </h1>
                    <div className="question-text">
                        Q1) 당신은 가전제품을 고를때 무엇을 먼저보나요?
                    </div>
                </div>
                <div className="answer-section">
                    <tr>
                      <td className="a"><button onClick={handleClick} value="디자인">디자인</button></td>
                      <td className="b"><button onClick={handleClick} value="가격">가격</button></td>
                      <td className="c"><button onClick={handleClick} value="사양">사양</button></td>
                      <td className="d"><button onClick={handleClick} value="무게">무게</button></td>
                    </tr>
                </div>
            </div>
        </div>
    );
}

export default App;