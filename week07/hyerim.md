1-7번까지의 과정을 그대로 따라해보고, 그 것에 대한 생각을 정리하여 code-pot github에 PR을 보내 주세요. 
=> 요약대신 어려웠던거 작성하기

 * 헬멧으로 타이틀을 변경해주고 파비콘을 사용하여 기존에 리액트의 대표이미지를 현재 퀴즈의 일론머스크관련된 이미지 삽입
 => 제일 흥미로웠다.

 * Open Graph 데이터 추가하기
 currentUrl에 현재 url을 알고싶으면 -> 현재도메인 확인 document.location.href
 이미지경로는 <meta property="og:image" content={elon} />로 작성되어있는데
 assets -> images 의 elon.jpg로 경로가 지정??
 => Elements에 들어가서 보면 content="/static/media/elon.04c18389.jpg로 경로가 지정되어있음.

나만의 퀴즈 MBTI로 수정
아직 4주차 진행중인데 css 수정 못했고, E/I // S/N // T/F // J/P를 지정못해줬습니다.
= https://github.com/hyerim9507/MBTItest
