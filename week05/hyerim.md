1-7번까지의 과정을 그대로 따라해보고, 그 것에 대한 생각을 정리하여 code-pot github에 PR을 보내 주세요. 
=> 요약대신 어려웠던거 작성하기

* Import 경로를 절대 경로로 바꾸기
    처음 작성했을때 안되다가 다시 삭제하고 재작성했더니 오류가 안났다.
    왜 오류가 났는지는 아직도 모르겠다.

*  일반적인 버튼 사용방법
    <Button>Hello</Hello>
    태그안에 싸여있는 "Hello"는 children 이라는 props에 담아서 들어온다.
    - 그래서 index.js에 props에서 children을꺼내서 사용한다.

*  삼항연산자 to props
   const Button = (props) => {
    const { onClick, children, to } = props;
    return<StyledButton onClick={props.onClick}>{props.children}</StyledBytton>};
    }
=> const Button = (onClick, children, to) => {
    if(to) {
        return (
            <StyledLink>
                <StyledButton onClick={onClick}>{children}</StyledButton>
            </StyledLink>
        );
    } else {
        return <StyledButton onClick={onClick}>{children}</StyledButton>;
        }
    }
=> const Button = (onClick, children, to) => {
    return to ? <StyledLink to ={to}>
    <StyledButton onClick={onClick}>{children}</StyledButton>
    </StyledLink>: (
        <StyledButton onClick={onClick}>{children}</StyledButton>
    )
};
    --> Link 태그에 어디로 가야할지 꼭 작성해주어야한다.<StyledLink to ={to}></StyledLink>

**** 반드시 export했으면 import작성하기!!
