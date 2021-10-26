## 📍 엘리스 SW 엔지니어 트랙 

## 📍 O.T
1. 주 5일, 총 560시간 동안 온/오프라인 병행하여 진행
- Part 1: JS 기초(1~4주차)
- Part 2: `Typescript`, `Node.js`, `SQL(5~9주차)` + 웹 서비스 프로젝트1
- Part 3: `React` + 웹 서비스 프로젝트2

2. 열심히 했는지 안 했는지 플랫폼에서 추천 할 수 있는 기능이 있음. 열심히 한 만큼 회사에 추천 가능성 증가
3. 팀 프로젝트(GitLab): 기여도 확인, 커스터마이징 가능, 답을 밖에 공개하기 보다는 `GitLab`의 `private` 사용 
4. 수료는 전체 교육의 80% 이상 출석해야 수료
5. 온라인 학습일 (수, 금): 로그인 / 로그아웃 시간 데이터 확인(학습시간이 7시간이 넘어야 출석으로 인정된다. 일정 시간 이상 활동하지 않으면 학습시간 기록 종료)
6. 오프라인 교육시 선릉역, 삼성역 인근의 교육장을 이용
   
## 📍 10.26.화. 1일차
수업은 <a href='https://www.youtube.com/c/%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A91'>이고잉</a>튜터님께서 가르쳐주셨다. 내가 맨 처음 프론트엔드를 하겠다는 마음을 먹고 유튜브에서 찾아봤던 영상이 이고잉님 강의였는데, 다른 레이서들과 함께 온라인 수업을 실시간으로 가르쳐주시니까 놀라웠다.

### ❏ CSS 우선순위
1. `!important` 태그
2. `HTML` 태그 안에 직접 `style`을 지정한 태그( `inline style`은 별로 추천하지 않는다.) 
3. `#id` 
4. `.class`, `추상class`, `수도클래스(:first-child)`
5. `HTML` 태그 
6. 상위 객체에 상속된 속성

### ❏ 수업 내용
1. `CSS`는 `HTML` 이 등장한지 4년 이후에 나왔다.
2. `DOM`: `JS`를 이용하여 웹 브라우저를 제어하는 방법
3. 수업내용 이전에 배운 내용이 잇다면 처음부터 전체적인 구조를 생각하며 배운다. (제일 중요한 것은 `HTML`)
4. 지식인이 되기 보다는 실천적인 사람이 되자.
5. 중급자로 올라 갈 수록 해당 개념에 대한 세부적인 강의도 없어진다. 따라서 어떤 개념이 베이스가 되는지 알고 추론을 잘해야한다.
6. `tag`: 옷에 달려있는 태그가 옷을 설명하듯이 코드를 감싸는 태그는 코드를 설명하는 기능을 한다.
7. `git`: 내가 작성한 코드를 안전하게 마치 `dropbox` 같은 곳에 저장하는 저장소
8. `img`는 `width`만 사용하고, `height`만 사용하는 것을 권장한다. (`width`만 사용하면 `height`는 컴퓨터가 알맞은 높이를 자동으로 계산하여 나타내고, 반대로 `height`만 사용하면 `width`는 컴퓨터가 알맞은 너비를 자동으로 계산하여 나타낸다.)
9. 태그에 붙어있는 `src`, `alt`, `width`, `height` 등은 속성(attribute)를 나타낸다.
10. `hyper link`: 모든 형식의 자료를 클릭 한번으로 연결하고 가리킬 수 있는 참조 고리이다.
11. `server - client`: `client`에서 주소표시창에 `Domain name`을 입력하고 `Enter`를 누르면 `Domain name`과 연결되어있는 `IP address`를 찾고 해당 주소를 통해 `server`에 접근한다. 이때, `server`는 `client`에게 `HTML`파일을 보여주는데 기본적으로 `index.html`로 설정되어있다.
12. `CSS selector`: CSS 규칙을 적용할 요소를 정의한다.
13. 하단과 같이 시각적인 도움만 주는 `CSS`코드는 권장되지 않는다. `HTML2`부터는 `HTML`태그로 문서의 구조와 의미를 표현하고, `CSS`태그로 문서의 스타일만 표현하면서 문서의 구조와 스타일을 분리하는 쪽으로 발전되었다. 즉, 시각적인 정보만 주는 태그는 사용하지 않는다. (`HTML5`부터 더 이상 지원하지 않는다.)

```css
<font color="red">
    <h1>html</h1>
</font>
<font color="orange">
    <h1>css</h1>
</font>
<font color="blue">
    <h1>js</h1>
</font>
```

1.  `HTML tag`는 각자 자기만의 `style`이 존재한다. (예 `h1`: `display:block`, `font-size:2em`, `font-weight:bold` 등)
2.  `padding`: `content`와 `테두리(border)` 사이의 간격
3.  `margin`: `테두리(border)`와 `테두리(border)` 사이의 간격 (상하 관계의 `margin`은 <a href='https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing'>margin-collapsing</a>으로 인해 제일 큰 여백의 크기를 가진 단일 여백으로 상쇄된다.)
4.  `block`: 화면 전체를 사용한다. 가로 길이를 조정하고 싶으면 `width`를 사용하기
5.  `inline`: 자기 `content` 만큼의 크기만을 갖는다.