# open graph 태그

- 우리가 보고 있는 웹사이트는 기본적으로 HTML 문서이다.
- 가장 중요하게는 오늘 다룰 메타 데이터들이 HTML 태그를 통해 담겨있습니다.
- HTML 문서를 보면 자동으로 무엇이 제목인지, 무엇이 내용에 대한 3줄 요약인지, 무엇이 대표 이미지인지 100% 자동으로 판별하기 아주 어렵습니다.

프로토콜의 작동 원리는 다음과 같습니다.

1. 사용자가 링크를 입력창에 입력합니다.
2. 페이스북, 네이버 블로그, 카카오톡은 입력창의 문자열이 "링크"라는 것을 파악합니다. (흔히 말하는 정규표현식으로 해당 문자열이 링크라는 것을 알아냅니다.)
3. 링크라는 것이 파악되면 페이스북, 네이버 블로그, 카카오톡의 크롤러는 미리 그 웹사이트를 방문해서 HTML head의 오픈그래프(Open Graph) 메타 데이터를 긁어옵니다.
4. 이중에서도 og:title, og:description, og:image가 각각 제목, 설명, 이미지의 정보를 나타냅니다.
5. 그리고 그 정보를 바탕으로 미리보기 화면을 생성해주게 됩니다.

- HTML 문서의 메타정보를 쉽게 표시하기 위해서 메타정보에 해당하는 제목, 설명, 문서의 타입, 대표 URL 등 다양한 요소들에 대해서 사람들이 통일해서 쓸 수 있도록 정의해놓은 프로토콜이며 페이스북에 의하여 기존의 다양한 메타 데이터 표기 방법을 참조하여 만들어졌습니다.

# 오픈그래프가 가지는 위상

- 오픈그래프는 웹문서를 이루고 있는 여러 기술들 중에서 상당히 상위권에 포진하고 있습니다.
- 온갖 다양한 웹사이트 만드는 기술이 포진하고 있는 웹의 생태계에서 이 정도라면 아주 대단한 유행으로 볼 수 있을 것입니다.

# 메타데이터를 지원하는 트위터

- 트위터의 메타 데이터 표기법도 결국에 오픈그래프를 참조한 것입니다.

# 오픈그래프 적용 여부

-  [Sharing Debugger](https://developers.facebook.com/tools/debug/)를 지원하고 있는데 사이트에 들어가서 검사하고 싶은 링크를 입력하면 됩니다. 

# 미리보기가 바뀌지 않는 이유?

- 데이터베이스에 저장된 어떤 정보를 한 번 불러온 후 캐시 메모리에 저장해놓거나, 어떤 HTML, CSS, JavaScript로 이뤄진 웹문서 전체 혹은 이미지 전체를 캐싱하기도 합니다.
- 캐싱에는 TTL(Time-to-Live)라는 소멸시효가 걸려있는데, 이 소멸시효가 지나지 않은 경우 계속적으로 이미 캐싱된 데이터를 참조해서 불러올 수 있습니다.

# 클릭 2의 미스터리

- 바로 쓴 글을 페이스북이 올리면 조회수가 2가 되는 것을 확인할 수 있다.
- 크롤러가 우리 사이트를 한 번 "미리" 방문하는 현상 때문에 조회수가 1 올라갑니다.
- 특히 설치링크라면 더더욱 사소한 문구 하나의 차이가 큰 설치율의 증감을 초래할 수도 있습니다.

# 오픈그래프 사용방법

1. og:title, og:description, og:image를 HTML의 head에 반드시 넣고, 제대로 반영되었는지를 "Sharing Debugger"를 통해서 확인한다.
2. 실제로 카카오톡, 페이스북, 네이버 블로그 등 사용하고자 하는 마케팅 채널에 링크를 넣고 미리보기 화면을 확인한다. (실제 보여지는 이미지가 사이즈가 각 서비스마다 다르기 때문에 반드시 주의할 것)
3. 가능하다면 A/B 테스팅을 통해서 어떤 문구나 이미지가 가장 좋은 효과를 보이는지 확인한다.

# CNAME

- CNAME = Canonical Name의 줄임말로 하나의 도메인에 다른 이름을 부여하는 방식을 의미합니다. 

# A record

- domain name에 하나의 IP Address가 있음을 의미합니다. 하나의 도메인(서브나 루트 포함)에 해당하는 IP 주소의 값을 가지고 있습니다.