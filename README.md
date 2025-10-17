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

### git checkout

과거에는 checkout 하나로 브랜치 이동, 브랜치 생성, 커밋 이동까지 모두 처리했다.
하지만 기능이 많다 보니 초보자에게 혼란을 주었다.

    브랜치 이동
    git checkout feature/login

    브랜치 생성 + 이동
    git checkout -b feature/signup

    특정 커밋으로 이동
    git checkout <commit-id>

 ### git switch

    브랜치 이동
    git switch feature/login

    브랜치 생성 + 이동
    git switch -c feature/signup

        •	checkout은 다기능이지만 복잡하고 실수 위험이 있음
	    •	switch는 브랜치 전용 명령어라서 더 직관적이고 안전함
	    •	최신 Git 환경에서는 switch 사용을 권장


### layout
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

        // App.jsx
        import { Routes, Route } from "react-router-dom";
        import Layout from "./components/Layout";
        import Home from "./pages/Home";
        import About from "./pages/About";

        function App() {
            return (
                <Routes>
                    { Layout을 공통으로 적용 }
                    <Route path="/" element={<Layout />}>
                        <Route index element={<Home />} />
                        <Route path="about" element={<About />} 
                        />
                    </Route>
                </Routes>
            );
        }

        export default App;

### Outlet 사용 예시

        // Layout.jsx
        import { Outlet } from "react-router-dom";
        import Header from "./Header";
        import Footer from "./Footer";

        function Layout() {
            return (
                <div>
                    <Header />
                    <main>
                        <Outlet /> { 라우터에서 지정된 페이지가 들어옴 }
                    </main>
                <Footer />
            </div>
            );
        }

        export default Layout;

###. 스타일링 방법
	•	CSS 모듈: Layout.module.css 파일로 분리
	•	Styled-components: JS 안에서 스타일 정의
	•	Tailwind CSS: 클래스명으로 빠르게 레이아웃 잡기

    •	레이아웃은 공통 구조(헤더, 푸터, 사이드바)를 관리하는 컴포넌트
	•	children 또는 Outlet을 활용해서 페이지를 끼워 넣는다
	•	반복되는 코드를 줄이고, 유지보수를 쉽게 만든다

## 5주자 9월24일

### Next.js searchParams 이해하기 및 동적 렌더링

### searchParams란 무엇인가?
searchParams는 Next.js App Router에서 URL의 쿼리 문자열(Query String)을 컴포넌트 내에서 접근하고 읽을 수 있도록 제공되는 객체입니다.
역할: 클라이언트가 요청한 URL에서 특정 데이터(검색 조건, 페이지 번호 등)를 추출하는 데 사용됩니다.

구조: 페이지 컴포넌트의 props로 전달되며, 내부적으로는 브라우저의 네이티브 Web API인 URLSearchParams와 동일하게 작동합니다.
예시: https://example.com/products? category=shoes&page=2
여기서 category=shoes와 page=2가 searchParams를 통해 접근할 수 있는 검색 파라미터(Search Parameters)입니다.

### searchParams가 동적 렌더링(Dynamic Rendering)을 유발하는 이유
Next.js는 페이지를 크게 정적(Static) 또는 동적(Dynamic)으로 렌더링합니다. searchParams를 사용하면 해당 페이지는 자동으로 동적 렌더링 모드로 전환됩니다.

### 렌더링 방식의 구분
방식,정적 렌더링 (Static Rendering),동적 렌더링 (Dynamic Rendering)
생성 시점,빌드(Build) 시점에 미리 HTML 생성,사용자의 요청(Request) 시점에 HTML 생성
조건,페이지 내용이 빌드 시점에 확정 가능해야 함,페이지 내용이 요청 시점의 데이터에 의존해야 함

### 동적 렌더링으로 전환되는 원리
빌드 시점의 불확실성: searchParams에 담기는 쿼리 문자열(?keyword=nextjs 또는 ?keyword=react 등)의 값은 개발자가 빌드를 수행하는 시점에는 알 수 없습니다. 이 값은 오로지 사용자가 어떤 URL로 접속했는지에 따라 결정됩니다.
요청 시점 데이터 의존: searchParams는 오직 요청이 서버에 도달했을 때만 값을 확정할 수 있는 요청 시점(Request-time) 데이터입니다.
자동 동적 처리: Next.js는 페이지의 렌더링 결과가 요청 시점의 데이터(searchParams, headers, cookies 등)에 따라 달라져야 할 경우, 안정적인 데이터 반영을 위해 해당 페이지를 정적으로 미리 생성할 수 없다고 판단합니다.

결과: 해당 페이지는 매 요청마다 서버에서 새로 렌더링되는 동적 렌더링으로 처리됩니다.
요약: searchParams의 값은 요청이 들어와야만 알 수 있으므로, Next.js는 페이지를 요청이 올 때마다 새로 만들어야 하며, 이것이 동적 렌더링으로 처리되는 이유입니다.

## 6주자 10월1일

### Client-side Transitions (클라이언트 측 전환)
클라이언트 측 전환은 Next.js가 제공하는 핵심 기능 중 하나로, <Link> 컴포넌트를 사용하여 구현됩니다. 이는 서버 렌더링된 애플리케이션의 장점을 유지하면서도, 클라이언트 렌더링(SPA, Single Page Application) 방식의 부드러운 페이지 이동 경험을 제공합니다.

### 일반적인 서버 렌더링 페이지 이동의 문제점
일반적인 웹 애플리케이션에서 서버 렌더링된 페이지로 이동할 때 발생하는 문제는 다음과 같습니다:
전체 페이지 로드: 새로운 페이지로 이동 시 브라우저가 전체 페이지를 새로고침(Full Page Load)합니다.
State 초기화: 이전 페이지의 **클라이언트 측 state (상태)**가 모두 삭제됩니다.
스크롤 재설정: 스크롤 위치가 항상 페이지 상단으로 재설정됩니다.
상호작용 차단: 페이지를 로드하는 동안 사용자의 다른 상호작용이 잠시 차단됩니다.

### Next.js의 클라이언트 측 전환이 해결하는 것
Next.js는 <Link> 컴포넌트를 사용한 클라이언트 측 전환을 통해 위의 문제들을 방지하고, 다음과 같은 이점을 제공합니다:
공유 UI 및 레이아웃 유지:
페이지 이동 시, 공유되는 레이아웃이나 지속적인 UI 요소 (예: 내비게이션 바, 푸터)는 파괴되지 않고 그대로 유지됩니다.
새로 변경되는 페이지 콘텐츠만 효율적으로 가져와 교체합니다.

부드러운 페이지 교체:
Next.js는 <Link>가 가리키는 페이지를 미리 가져와(prefetching) 로딩 상태에 대비하거나, 이미 로드가 완료된 경우 즉시 새로운 페이지로 현재 페이지를 대체합니다.

SPA와 같은 경험:
클라이언트 측 전환은 서버에서 렌더링된 앱을 마치 클라이언트에서 렌더링된 싱글 페이지 앱(SPA)처럼 끊김 없이 부드럽게 느끼게 하는 핵심 요소입니다.

성능 향상:
프리페칭(Prefetching) 및 스트리밍(Streaming) 기능과 함께 사용되면, 동적 경로를 포함한 복잡한 경로에서도 매우 빠르고 효율적인 페이지 전환이 가능해집니다.
페이지 이동에 필요한 최소한의 데이터만 가져오고, 불필요한 리로드를 방지하여 사용자 경험(UX)과 성능을 크게 개선합니다.
