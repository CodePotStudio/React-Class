1-7번까지의 과정을 그대로 따라해보고, 그 것에 대한 생각을 정리하여 code-pot github에 PR을 보내 주세요

 * 화살표함수는 일반함수와 기능은 같지만 코드를 간결하게 사용하도록 도와준다.
    ex) function sum(a,b) {
        return a + b ;
    }
    ==> const sum = (a,b) => {
        return a + b ;
    };
    ** const 변수명으로 설정하고 => 이 function의 역활을 한다.
    *** 만약 함수내에서 바로 return할경우에만 더축약이 가능하다.
    ==> const sum = (a,b) => a + b;
    * const square = (n) => n x n;
        매개변수인 n이 하나일 경우에는 소괄호도 축약이 가능하다.
        ==> const sum = n => n x n;
 * 객체 구조분해 할당
    { }로 감싸져있는것을 딕셔너리 X => 파이썬 // 객체 O => 자바스크립트 라고 부른다.
    ex) const people = {
        name: "code pot",
        address: "seoul",
        };
    만약 위의 함수에서 name을 알고싶으면 people.name // people["name"]으로 하고, 만약에 people의 객체에서 name , address를 꺼내서 변수에 저장하고 싶으면
    const name = people.name;
    const address = people.address 저장하고
    console.log(name, address);를 하면
    code pot seoul이 확인되는데 이과정을 할때 중복돠는 과정이있어서 아래와 같이 축약을 시킬 수가 있다.
    const {name, address} = people;
    console.log(name,address); 만 해도 결과값은 동일하게 나온다.
    여기에서 변수명 이름을 변경하고 싶으면, 기존에는 const fullName =  people.name; 으로 선언을 하고 fullName을 하면 codepot로 나온다.
    하지만 구조분해할당에서는 const {name: fullName} = people; 로 선언해줘야한다.
 * 배열 비구조 할당
    const fruits = ["사과","감"];
    const [hello, world]; = fruits; 로 선언하면 
    hello => "사과"
    world => "감" 으로 결과값이 나온다.
 * 중복되는 코드 단순화하기
    ** 베열 내장함수 map : 배열을 순회하면서 인자로 넣어준 함수를 실행
        const fruits = ["사과", "감", "배", "딸기"];
        function sayHello() {
            console.log("hello");
        }
        fruits.map(sayHello); 를 실행해보면
        hello가 4번 실행되었다고 나온다. 그이유는 fruits 안에있는 과일 수대로 배열을 순회하면서 sayHello함수를 실행하기 때문이다.
        만약에 fruits안에있는 과일을 보고싶다면 element 인자에 값이 들어와서 실행을 시켜준다.
        => const fruits = ["사과", "감", "배", "딸기"];
            function sayFruit(element) {
                console.log(element);
            }
            fruits.map(sayFruit); 를 선언하면 결과값은
            사과 / 감 / 배 / 딸기 가나온다.
        축약을 하면 
        => const fruits = ["사과", "감", "배", "딸기"];
            fruits.map(function sayFruits2(elenemt)
            {console.log(element)})로 작성을해도 결과값은 동일하게 
            사과 / 감 / 배 / 딸기 가나온다.
            여기서 화살표 함수로 간결하게 표현하자면
            fruits.map((element) => {console.log(element)})
            ( )안에 이름이 없는 함수인데 fruits.map가 실행이되면서 동일한 결과값을 나타낸다. => 사과 / 감 / 배 / 딸기
            여기서도 리턴을 바로하면 { } 생략이가능해서 fruits.map((element) => console.log(element)) 로 해도되고 element위치에 값이 하나면 앞 element의 ( )로 생각이 가능하여
            fruits.map(element => console.log(element))도 사용가능하다.
 * DRY 원칙의 의미 Don't Repeat Yourself
    프로그래밍에서는 코드중복 무분별한낭비, 반복은 무의미하다. 
    그렇기에 객체지향의 장점은 반복을 최소화하도록 설계되었다는것이다.
 * 배열 내장함수
    * forEach : 가장 쉬운 배열 내장함수, 기존 for 문을 대체할 수 있음.
    * map : 배열 안의 각 원소를 변환 할 때 사용, 이를통해 새로운 배열이
            만들어짐
    * indexOf : 원하는 항목이 몇번째 원소인지 찾아주는 함수
    * findIndex : 배열 안에 있는 값이 숫자, 문자열, 또는 불리언이라면   
                  찾고자하는 항목이 몇번째 원소인지 알수 있으나 배열안에 있는 객체, 배열은 찾을 수 없다.
    * find : findIndex 랑 비슷하나, 찾아낸 값이 몇번째인지 알아내는 것이
             아니라, 찾아낸 값 자체를 반환해준다.
    * filter : 배열에서 특정 조건을 만족하는 값들만 따로 추출하여 새로운 
               배열을 만든다.
    * splice : 배열에서 특정 항목을 제거할 때 사용
    * slice : splice와 비슷한데, slice는 배열을 잘라낼 때 사용하지만, 
              기존의 배열은 건들이지 않는다.
    * shift 와 pop : 비슷하지만 다르다. shift는 첫번째 원소를 배열에서 
                     추출해주는데 추출하는 과정에서 배열에서 해당 원소는 사라진다.
                     pop는 배열의 맨 마지막 항목을 추출한다.
    * unshift : shift의 반대로 배열의 맨 앞에 새 원소를 추가한다.
    * concat : 여러개의 배열을 하나의 배열로 합쳐준다.
    * join : 배열 안의 값들을 문자열 형태로 합쳐준다.
    * reduce : 잘 사용한다면 유용한 함수로 주어진 배열에 대하여 총합을 
               구해야 하는 상황일때 선언이 단축되어 결과값이 나타난다.
* 정답 체크 함수 최적화 하기
    handleClick 함수에서 answer === "스페이스 엑스" 처럼 정답 값을 일일이 확인하고 있는데, 이렇게 되면 다른 퀴즈 문제가 추가될 수 없다.
    이벤트 핸들러에 매개변수를 넘겨서 event대신 isCorrect값을 기준으로 alet창을 띄우고 handleClick함수에 보내주는데 화살표로 감싸주면 handleClick에 원하는 값을 전달할 수 있다.
* 컴포넌트 내부에서 관리하는 변수
    state 사용하기 useState hooks => state 사용위해서 useState함수를 사용한다.
    ex) const state = useState(0);
        const currentNo = state[0];
        const setCurrentNo = state[1];
    useState는 인자로 state초기값을 받는데 currentNo의 초기값은 0이므로 useState에 0을 넣는데 useState는 결과값으로 state의 변수와 갱신할 수 있는 함수를 리스트에 담아서 반환해준다.
    위의 값을 축약하면 아래와 같이 사용가능하다.
    => const [currentNo, setCurrentNo] = useState(0);
// const [currentNo, setCurrentNo] = useState(0);에서 currentNo & setCurrentNo 는 퀴즈들의 index이다. 그래서 useState가 업데이트가 되면 재렌더링이되서 App이 재실행되면서 currentNo가 1이 더해진 숫자의 퀴즈가 보여진다.
setCurrentNo(currentNo+1)를 여러번 중복해서 작성을해도 함수는 1번만 실행이되는데 setCurrentNo((currentNo)=>currentNo+1)을 6번 작성하면 6번 실행되어 값이 계산된다.
* state간의 관계가 없는 이상 분리를 해서 작성을 해준다.
* JAM stack는 JavaScript와 Markup에 해당하는 HTML, CSS와 API를 활용하여 웹app을 구성하고 CDN에 배포하여 관리하는 스택이다.
  기존 Web와 다른점은 웹서버를 관리할 필요가없고 프론트엔드와 백엔드가 분리된다.


[간단한 퀴즈 앱 만들기 과제] 추후에 다시 추가적으로 올리겠습니다!<br>