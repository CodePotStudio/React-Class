1-7번까지의 과정을 그대로 따라해보고, 그 것에 대한 생각을 정리하여 code-pot github에 PR을 보내 주세요

 * React에서 URL 다루기
    * React Router 설치하기
        - npm install react-router-dom
            VS 터미널에 위의 코드를 입력해주면 react router가 설치가 되면서 Link Router컴포넌트를 동작할 수 있도록 도와준다.
    * Route 컴포넌트
     - <Route path="url 경로" component={렌더링할 컴포넌트} />
        path = "url경로" 로 들어오면 component=(렌더링할 컴포넌트) 렌더링해라.
        <Route path="url 경로">
            <렌더링할 컴포넌트 />
        </Route> 로도 가능하다.
        첫번째 방식으로는 여러가지 path를 실행하기 어려워서 두번째방식으로는 여러가지 path를 실행할 수 있다.
        ex) <Router>
                <Route path="/mypage" component={MyPage} />
                <Route path="/about" component={About} />
                <Route path="/" exact component={Home} />
            </Router>
            => 마지막 Route에 exact를 작성하는 이유는 /가 mypage에도 about에도 있는데 Home의 path는 /이기때문에 중복적용이 될 수있기에 정확하게 /만있을경우 Home을 렌더링 위해 props 해주었다.
    * Link 컴포넌트
     - Link태그와 a태그는 기능이 비슷하지만 다른점은 a태그는 페이지를 이동하면 html을 새로 받아와서 실헹되고 초기화되었지만 Link태그는 url만 변경되고, 필요한 부분만 업데이트 되서 초기화 되는 상태는 발생하지 않음.
     <Link to="이동할 URL">링크 이름</Link>
      - a태그는 href로 이동하는데 Link는 to를 이용해서 url을 이동시킴.
 * React 이미지 태그 다루기
    react는 이미지 태그를 사용할때 html에서 사용하듯이 경로를 넣어주면 작동이 되는것이 아니라 파일을 만들어서 이미지를 넣어놓고 import해줘서 연결을 해줘야 한다.
    - import cover from "이미지 경로/cover.jpg";
      <img src={cover} />;
 * 현재 컴포넌트 구조는 App 밑에 Landing / Quiz / Result가 있고 
   유일하게 Quiz만 state가 있는데 Result에 score state가 필요하기에 score state를 설정해준다.
 * React Router 의 useHistory hooks
   이전까지 퀴즈에서 문제만 풀어지고 점수페이지가 안나왔는데 점수페이지가 나오려면 
   const Quiz = ({ setScore }) => {
    const [currentNo, setCurrentNo] = useState(0);
    let history = useHistory();

    const handleClick = (isCorrect) => {
        if (isCorrect) {
            setScore((score) => score + 1);
        }
        if (currentNo === QUIZZES.length - 1) {
            history.push("/result");
        } else {
            setCurrentNo((currentNo) => currentNo + 1);
        }
    };
    특정페이지 이동시키는 history.push("/result");를 작성해준다.
    그러면 점수페이지가 나오고 테스트다시하기 누르고 다시 퀴즈를 풀면 점수가 누적이 되어져 점수를 초기화 시키는 setScore을 실행해준다.
    
[간단한 퀴즈 앱 만들기 과제]....