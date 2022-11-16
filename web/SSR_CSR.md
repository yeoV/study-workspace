
## MPA vs SPA
- **MPA (Mulit page application)**
	- 여러 페이지로 구성된 웹 어플리케이션
	- 기존 HTML, CSS, JS, PHP, JSP 등 전통적인 방식
	- 탭을 이동할 때 마다 서버로부터 새로운 **html을 받아 렌더링 해야 하는 단점**
	- 정적 리소스를 가져오기에 SSR과 적합

- **SPA (Single Page Application)**
	- 하나의 페이지로 구성된 웹 어플리케이션
	- 데이터가 필요한 부분을 동적으로 구성
	- CSR 렌더링 방식으로 구현
	- 리액트, 뷰, 앵귤러 사용


## SSR vs CSR
### SSR (ServerSideRendering)
- Server 에서 rendering
	- User가 웹사이트 방문 시, 브라우저에서 서버로 콘텐츠 요청.
	- 서버에서 즉시 페이지에 필요한 데이터를 얻어와 CSS 까지 적용하여 **렌더링 준비를 마친 HTML** 과 JS 코드를 브라우저 응답으로 전달
	- 이후 브라우저가 전달 받은 페이지를 띄우고  JS 로직 연결
- 서버에서 HTML 파일을 다운 (웹이 요청받은 파일이 viewable)
- 이미 서버가 제공하는 HTML 파일에 tag가 다 존재함
- Spring, JSP 등을 이용하여 구현
- 웹에서 렌더링되기 이전, 모든 OS를 위한 

**장점**
1. 검색엔진 최적화에 유리
2. 초기 구동 속도가 빠름

**단점**
1. 페이지가 구동되어 보여져도, interactive 하지 않을 수 있음
	- TTV(time to view) 와 TTI(time to interact) 의 차이가 존재
2.  화면 깜빡임 있음
3. 서버 부하가 있음



### SSG (Static Site Generation)
- 바뀔 일이 거의 없는 페이지에 적합
- 페이지들을 서버에서 모두 만들어둔 뒤에 요청시 해당 페이지를 응답하는 방식
- **캐싱 해두면 좋은 페이지에 사용하면 적합**


### CSR (ClientSideRendering)
- Client 에서 rendering 
	- User가 웹사이트를 방문 시, 컨텐츠를 
- browser에게 보내는 Response 파일안에 아무 내용도 없음 **(빈 뼈대 HTML 연결된 JS 링크)**
- Browser가 추가로 **JS 파일을 다운로드** 받음

**장점**
1. 서버의 부하가 적음
	- 클라이언트 측에서 연산, 라우팅 처리. 반응 속도 빠름 
2. TTV(time to view) 와 TTI(time to interact) 의 차이가 없음
3. 화면 깜빡임이 없다
4. 서버 부하 분산
5. 초기 로딩 이후 구동 속도가 빠름


**단점**
1. 초기 로딩속도가 느림
	- 브라우저가 JS를 다운받고 동적으로 DOM 을 구성해야 함
	- 이후 페이지 일부 변경 시, 서버에 해당 데이터만 요청하면 되기에 이후 구동 속도는 빠름
2. 검색엔진 최적화에 불리 (SEO 에 불리)
	- 웹 크롤러가 본 HTML은 비어있기에 검색엔진이 색인할 데이터가 없음 

**단점 극복안**
- code splitting / tree-shaking - chunk 분리 -> 초기 로딩 속도 보완
- pre-rendering -> seo 개선


### CSR + SSR / SSG
1안. express.js 로 별도 서버 구축 (프레임워크 x)
2안. Next.js -> SSR, SSG 선택할 수 있음 


	- 예) react의 App.js 파일을 index.html 에서 import 하여 render 하면, client가 다운받아서 수행
```js
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import "./index.css";

// App 컴포넌트를 호출하여 render 하는 과정이 client side에서 발생
ReactDOM.createRoot(document.getElementById("root")).render(
	<React.StrictMode>
	<App />
	</React.StrictMode>
);
```

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<link rel="icon" type="image/svg+xml" href="/vite.svg" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Vite + React</title>
	</head>
	<body>
		<div id="root"></div>
		<script type="module" src="/src/main.jsx">
		</script>
	</body>
</html>
```
- script 부분에서 jsx 를 호출하면서 client side에서 다운로드




### 무엇을 써야할까?
- User와 상호작용이 많고 대부분 고객 개인 정보로 이루어져 검색엔진 노출될 필요 없을 경우-> CSR
- 회사 홈페이지, 누구에게나 같은 내용, 매주 업데이트 -> SSR
- 사용자에 따라 페이지 내용 달라짐, 빠른 인터렉션 중요, 상위 노출 -> SSR + SSR

### 참고 링크
- 유투브 설명 
- https://www.youtube.com/watch?v=YuqB8D6eCKE&t=301s