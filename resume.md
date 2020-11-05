---
layout: page
title: PORTFOLIO
comments: true
---

<head>
    <title>Photon by HTML5 UP</title>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no" />
    <link rel="stylesheet" href="assets/css/about.css" />
    <noscript><link rel="stylesheet" href="assets/css/noscript.css" /></noscript>
</head>
<div class="is-preload">
    <!-- Header -->
    <section id="header">
        <div class="inner">
            <span class="icon major fa-cloud"></span>
            <h1><strong>Front-End</strong> Developer</h1>
            <p><strong>Javascript</strong> 개발자 김상연입니다.</p>
            <ul class="actions special">
                <li><a href="https://github.com/kimsangyeon" class="button scrolly">GitHub</a></li>
            </ul>
        </div>
    </section>
    <!-- Working -->
    <section id="three" class="main style1 special">
        <div class="container">
            <header class="major">
                <h2>My Working</h2>
            </header>
            <p>Javascript Front-End Web Service.</p>
            <div class="row gtr-150">
                <div class="col-4 col-12-medium">
                    <span class="image tmon"><img src="images/about/tmon.jpg" alt="" /></span>
                    <h3><a href="#resume-tmon">TMON</a></h3>
                    <p>2019.11 ~ ing</p>
                    <ul class="actions special">
                        <li><a href="https://www.tmon.co.kr/" class="button">More</a></li>
                    </ul>
                </div>
                <div class="col-4 col-12-medium">
                    <span class="image editor"><img src="images/about/editor.png" alt="" /></span>
                    <h3><a href="#resume-synapeditor">Synap Editor</a></h3>
                    <p>2018.02 ~ 2019.11</p>
                    <ul class="actions special">
                        <li><a href="http://www.synapsoft.co.kr/editor" class="button">More</a></li>
                    </ul>
                </div>
                <div class="col-4 col-12-medium">
                    <span class="image office"><img src="images/about/office.png" alt="" /></span>
                    <h3><a href="#resume-synapoffice">Synap Office</a></h3>
                    <p>2016.01 ~ 2018.02</p>
                    <ul class="actions special">
                        <li><a href="http://www.synapsoft.co.kr/office" class="button">More</a></li>
                    </ul>
                </div>
            </div>
        </div>
    </section>
    <!-- TMON -->
    <section id="one" class="main style1">
        <div class="container">
            <div class="row gtr-150">
                <div class="col-6 col-12-medium">
                    <header class="major">
                        <h2 id="resume-tmon">TMON</h2><br>
                        <h5>2019.11 ~ ing</h5>
                    </header>
                    <h3>Description</h3>
                    <p>TMON FE 개발</p>
                    <p>TMON 상품 판매 페이지인 딜상세 개발을 담당하며 딜상세 일부 영역 React 부분 개편작업. API 호출 개선 및 랜더링 개선. TMON 홈 메인 페이지 브랜드관 애니메이션 인터렉션 구현. Webpack 버전 마이그레이션(1->4)</p><br>
                    <h3>Tech</h3>
                    <p>Javascript, Jquery가 주로 사용되었으며, ES6 문법으로 작성 webpack, babel을 사용하여 모듈화. React 사용하여 딜상세 페이지 부분 개편.</p><br>
                    <h4>딜상세</h4>
                    <ul>
                        <li>딜상세 페이지 상품정보 영역 React 부분 전환</li>
                        <li>Intersection Observer 활용한 API 호출 개선</li>
                        <li>메인 페이지에 사용자 인터렉션 가능한 브랜드관 애니메이션 구현</li>
                        <li>Webpack v1에서 v4로 마이그레이션</li>
                    </ul>
                    <h4>홈 메인</h4>
                    <ul>
                        <li>브랜드관 애니메이션 인터렉션 구현</li>
                    </ul>
                </div>
                <div class="col-6 col-12-medium imp-medium">
                    <span class="image fit"><img src="images/about/tmon2.jpg" alt="" /></span>
                </div>
            </div>
        </div>
    </section>
    <!-- SynapEditor -->
    <section id="one" class="main style1">
        <div class="container">
            <div class="row gtr-150">
                <div class="col-6 col-12-medium">
                    <header class="major">
                        <h2 id="resume-synapeditor">Synap Editor</h2><br>
                        <h5>2018.02 ~ 2019.11</h5>
                    </header>
                    <h3>Description</h3>
                    <p>ContentEditable을 사용하지 않은 모델 편집중심 웹 에디터 개발 참여.</p>
                    <p>사이냅 에디터 프로젝트 시작부터 제품 출시까지 원활한 입력이 가능한 IME(입력기) 개발, 에디터 편집을 전담하여 개발하였습니다.</p><br>
                    <h3>Tech</h3>
                    <p>Javascript, Jquery가 주로 사용되었으며, MVC Model 편집부터 랜더링 구조로 작업. Mocha, karma를 사용한 브라우저 테스트 환경 구축. ES6 문법으로 작성 webpack, babel을 사용하여 모듈화. cross browsing 지원 작업 (IE10 이상)</p><br>
                    <h4>에디터 편집</h4>
                    <ul>
                        <li>텍스트 입력 및 삭제</li>
                        <li>개체 (이미지) 편집 핸들</li>
                        <li>Undo/Redo</li>
                        <li>레이어 편집</li>
                    </ul>
                    <h4>에디터 도형 표현</h4>
                    <ul>
                        <li>임포트 도형 표현</li>
                    </ul>
                    <h4>API</h4>
                    <ul>
                        <li>DOM API</li>
                    </ul>
                    <h4>Test</h4>
                    <ul>
                        <li>Mocha</li>
                        <li>Karma</li>
                    </ul>
                </div>
                <div class="col-6 col-12-medium imp-medium">
                    <span class="image fit"><img src="images/about/editor2.jpg" alt="" /></span>
                </div>
            </div>
        </div>
    </section>
    <!-- Synap Office -->
    <section id="one" class="main style1">
        <div class="container">
            <div class="row gtr-150">
                <div class="col-6 col-12-medium">
                    <header class="major">
                        <h2 id="resume-synapoffice">Synap Office</h2><br>
                        <h5>2016.01 ~ 2018.02</h5>
                    </header>
                    <h3>Description</h3>
                    <p>MS문서(Word, Cell, Slide) 및 HWP 임포트 편집 가능한 웹오피스입니다.</p>
                    <p>사이냅 오피스 슬라이드 프론트엔드 담당하였으며, 네이버 슬라이드 이슈 대응 및 성능개선 진행하였습니다. 또한 슬라이드 내부 content Editor 작업 진행 및 워드, 셀 도형 랜더링 작업을 하였습니다.</p><br>
                    <h3>Tech</h3>
                    <p>Javascript, Jquery, Jindo js 등이 주로 사용되었으며, cross browsing 지원 작업 (IE9 이상)</p><br>
                    <h4>슬라이드 편집</h4>
                    <ul>
                        <li>네이버 오피스 공동 편집 대응</li>
                        <li>슬라이드 에디터 작업</li>
                        <li>슬라이드 랜더링 성능 개선</li>
                    </ul>
                    <h4>오피스 도형 표현 작업</h4>
                    <ul>
                        <li>오피스 워드 도형 표현</li>
                        <li>오피스 셀 도형 표현</li>
                        <li>슬라이드 랜더링 성능 개선</li>
                    </ul>
                </div>
                <div class="col-6 col-12-medium imp-medium">
                    <span class="image fit"><img src="images/about/office2.jpg" alt="" /></span>
                </div>
            </div>
        </div>
    </section>
    <!-- skills -->
    <section id="two" class="main style2">
        <div class="container">
            <div class="row gtr-150">
                <div class="col-6 col-12-medium">
                    <ul class="major-icons">
                        <li><span class="icon style1 major fa-code"></span></li>
                        <li><span class="icon style2 major fa-bolt"></span></li>
                        <li><span class="icon style3 major fa-camera-retro"></span></li>
                        <li><span class="icon style4 major fa-cog"></span></li>
                        <li><span class="icon style5 major fa-desktop"></span></li>
                        <li><span class="icon style6 major fa-calendar"></span></li>
                    </ul>
                </div>
                <div class="col-6 col-12-medium">
                    <header class="major">
                        <h2>Skills</h2>
                    </header>
                    <h3>Javascript</h3>
                    <ul>
                        <li>ES6</li>
                        <li>webpack</li>
                        <li>babel</li>
                        <li>react</li>
                        <li>mocha + karma</li>
                    </ul>
                    <h3>etc</h3>
                    <ul>
                        <li>HTML5</li>
                        <li>css3</li>
                    </ul>
                    <h3>tools</h3>
                    <ul>
                        <li>git</li>
                        <li>slack</li>
                        <li>issue tracking system (jira)</li>
                    </ul>
                </div>
            </div>
        </div>
    </section>
    <!-- contact -->
    <section id="one" class="main style1">
        <div class="container">
            <div class="row gtr-150">
                <div class="col-6 col-12-medium">
                    <header class="major">
                        <h3>Contact</h3>
                    </header>
                    <ul>
                        <li>tel: 010-5105-7419</li>
                        <li>email: overflowscript@gmail.com</li>
                        <li>blog: <a href="https://kimsangyeon.github.io/">yeon blog</a></li>
                        <li>github: <a href="https://kimsangyeon.github.io/">yeon github</a></li>
                    </ul>
                </div>
                <div class="col-6 col-12-medium imp-medium">
                    <span class="image fit"><img src="images/about/contact.jpg" alt="" /></span>
                </div>
            </div>
        </div>
    </section>
    <!-- Footer -->
    <section id="footer">
        <ul class="icons">
            <li><a href="https://www.instagram.com/overflow_script/" class="icon alt fa-instagram"><span class="label">Instagram</span></a></li>
            <li><a href="https://github.com/kimsangyeon" class="icon alt fa-github"><span class="label">GitHub</span></a></li>
            <li><a href="mailto:overflowscript@gmail.com" class="icon alt fa-envelope"><span class="label">Email</span></a></li>
        </ul>
        <ul class="copyright">
            <li>&copy; Untitled</li><li>Design: <a href="http://html5up.net">HTML5 UP</a></li>
        </ul>
    </section>
    <!-- Scripts -->
    <script src="assets/js/jquery.min.js"></script>
    <script src="assets/js/jquery.scrolly.min.js"></script>
    <script src="assets/js/browser.min.js"></script>
    <script src="assets/js/breakpoints.min.js"></script>
    <script src="assets/js/util.js"></script>
    <script src="assets/js/main.js"></script>
</div>
