# React2 202130124 3학년 1반 이지훈
 
## 1주차 8월27일


## 2주차 9월3일
### Install
1. Node.js & npm 설치

리액트 프로젝트를 시작하기 위해서는 Node.js와 npm(Node Package Manager)이 필요하다.

Node.js: 자바스크립트를 브라우저 밖 환경에서 실행할 수 있게 해주는 런타임
npm: 필요한 라이브러리와 패키지를 관리하는 도구.

요즘은 Vite도 많이 사용 하는 거 같다

    node -v   # Node.js 버전 확인
    npm -v    # npm 버전 확인

    npx create-react-app my-app
    cd my-app
    npm start

설치를 마치고 npm run dev를 실행하면 기본 React 화면이 나타난다.
브라우저에서 http://localhost:3000 으로 접속 가능하다.

Node.js와 npm은 React 개발의 필수 기반
최신 React 프로젝트는 Vite를 통해 만드는 것이 빠르고 효율적
설치 후 구조를 이해하면 이후 컴포넌트 작성, 상태 관리, 라우팅 등을 배우기 수월해진다

## 3주차 9월10일
### Router

리액트는 SPA(Single Page Application) 구조를 기반으로 한다.
즉, 한 개의 HTML(index.html)에서 여러 화면을 바꿔 보여주는 방식이다.
이때 화면 간 전환을 담당하는 것이 라우팅(Routing)이며, 이를 쉽게 도와주는 라이브러리가 React Router이다.

1. React Router 설치

프로젝트에서 React Router를 사용하려면 패키지를 설치해야 한다.

    npm install react-router-dom
설치 후 package.json의 dependencies에 react-router-dom이 추가된다.

2. 라우터 기본 설정

    라우터를 사용하려면 최상위 컴포넌트를 BrowserRouter로 감싸야 한다.
// main.jsx
import React from "react";
import ReactDOM from "react-dom/client";
import { BrowserRouter } from "react-router-dom";
import App from "./App";

    ReactDOM.createRoot(document.getElementById("root")).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);

3. 라우팅 구현하기

페이지 이동을 위해 Routes와 Route 컴포넌트를 사용한다.
    App.jsx
    import { Routes, Route, Link } from "react-router-dom";
    import Home from "./pages/Home";
    import About from "./pages/About";

4. 주요 기능
	•	<Link>
a 태그와 비슷하지만, 새로고침 없이 컴포넌트만 전환된다.
	•	중첩 라우트 (Nested Routes)
하나의 페이지 안에서 하위 라우트를 구성할 수 있다.
	•	useParams()
URL 파라미터를 가져올 수 있다. (예: /user/:id)
	•	useNavigate()
코드로 페이지 이동을 제어할 수 있다.


	•	React Router는 SPA 환경에서 화면 전환을 담당한다

	•	BrowserRouter → 프로젝트에 라우팅 기능 부여

	•	Routes & Route → 경로에 따른 컴포넌트 매핑

	•	Link, useNavigate, useParams 등 다양한 기능 제공

## 4주자 9월17일

1. git checkout

과거에는 checkout 하나로 브랜치 이동, 브랜치 생성, 커밋 이동까지 모두 처리했다.
하지만 기능이 많다 보니 초보자에게 혼란을 주었다.

    브랜치 이동
    git checkout feature/login

    브랜치 생성 + 이동
    git checkout -b feature/signup

    특정 커밋으로 이동
    git checkout <commit-id>

 2. git switch

    브랜치 이동
    git switch feature/login

    브랜치 생성 + 이동
    git switch -c feature/signup

        •	checkout은 다기능이지만 복잡하고 실수 위험이 있음
	    •	switch는 브랜치 전용 명령어라서 더 직관적이고 안전함
	    •	최신 Git 환경에서는 switch 사용을 권장


3. layout
웹사이트는 보통 공통적으로 반복되는 영역이 있다.
예를 들어, 헤더(Header), 사이드바(Sidebar), 푸터(Footer) 같은 것들이다.
React에서는 이 공통 구조를 “레이아웃 컴포넌트”로 만들고, 각 페이지를 그 안에 넣어서 재사용할 수 있다.

        Header
        └─ Main Content (변경되는 부분)
        Footer

        import Header from "./Header";
        import Footer from "./Footer";

        function Layout({ children }) {
           return (
              <div>
                <Header />
                <main style={{ minHeight: "80vh" }}>
                {children} {/* 페이지별 내용이 들어가는 자리 */}
            </main>
            <Footer />
            </div>
          );
        }

children을 사용해서 각 페이지 내용을 끼워 넣는다.

4. 라우터와 함께 사용하기

    <!-- // App.jsx
    import { Routes, Route } from "react-router-dom";
    import Layout from "./components/Layout";
    import Home from "./pages/Home";
    import About from "./pages/About";

    function App() {
        return (
            <Routes>
                {/* Layout을 공통으로 적용 */}
                <Route path="/" element={<Layout />}>
                    <Route index element={<Home />} />
                    <Route path="about" element={<About />} />
            </Route>
        </Routes>
    );
    } -->

    export default App;

5. Outlet 사용 예시
<!-- 
    // Layout.jsx
    import { Outlet } from "react-router-dom";
    import Header from "./Header";
    import Footer from "./Footer";

    function Layout() {
        return (
            <div>
                <Header />
                <main>
                    <Outlet /> {/* 라우터에서 지정된 페이지가 들어옴 */}
                </main>
            <Footer />
        </div>
        );
    }

    export default Layout; -->

6. 스타일링 방법
	•	CSS 모듈: Layout.module.css 파일로 분리
	•	Styled-components: JS 안에서 스타일 정의
	•	Tailwind CSS: 클래스명으로 빠르게 레이아웃 잡기

    •	레이아웃은 공통 구조(헤더, 푸터, 사이드바)를 관리하는 컴포넌트
	•	children 또는 Outlet을 활용해서 페이지를 끼워 넣는다
	•	반복되는 코드를 줄이고, 유지보수를 쉽게 만든다
