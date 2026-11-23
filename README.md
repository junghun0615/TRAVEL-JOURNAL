# TRAVEL-JOURNAL
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>여행일지 | 나만의 여행을 기록하다</title>

    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@400;500;600;700;800&display=swap" rel="stylesheet">

    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css">

    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --blue: #3979d9;
            --dark: #1e293b;
            --gray: #64748b;
            --light: #f5f8fc;
            --line: #e5eaf1;
        }

        body {
            font-family: 'Noto Sans KR', sans-serif;
            color: var(--dark);
            background: white;
        }

        a {
            text-decoration: none;
            color: inherit;
        }

        button {
            font-family: inherit;
            cursor: pointer;
        }

        .container {
            width: min(1200px, 92%);
            margin: auto;
        }

        /* HEADER */

        header {
            height: 76px;
            display: flex;
            align-items: center;
            border-bottom: 1px solid var(--line);
            background: white;
            position: sticky;
            top: 0;
            z-index: 1000;
        }

        .header-inner {
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .logo {
            font-size: 25px;
            font-weight: 800;
            color: var(--blue);
        }

        .logo span {
            margin-right: 5px;
        }

        nav {
            display: flex;
            align-items: center;
            gap: 32px;
            font-size: 14px;
            font-weight: 600;
        }

        nav a:hover {
            color: var(--blue);
        }

        .header-buttons {
            display: flex;
            gap: 10px;
        }

        .btn {
            border: none;
            padding: 10px 18px;
            border-radius: 8px;
            font-size: 13px;
            font-weight: 700;
        }

        .btn-outline {
            background: white;
            border: 1px solid var(--line);
        }

        .btn-blue {
            background: var(--blue);
            color: white;
        }

        /* HERO */

        .hero {
            height: 510px;
            background:
                linear-gradient(90deg, rgba(15, 30, 52, .72), rgba(15, 30, 52, .12)),
                url('https://images.unsplash.com/photo-1533105079780-92b9be482077?auto=format&fit=crop&w=2000&q=85')
                center/cover;
            display: flex;
            align-items: center;
            color: white;
        }

        .hero-content {
            max-width: 650px;
        }

        .hero-tag {
            display: inline-block;
            background: rgba(255,255,255,.2);
            padding: 8px 15px;
            border-radius: 30px;
            font-size: 13px;
            margin-bottom: 22px;
        }

        .hero h1 {
            font-size: 48px;
            line-height: 1.4;
            font-weight: 800;
            margin-bottom: 15px;
        }

        .hero p {
            font-size: 16px;
            color: rgba(255,255,255,.9);
            margin-bottom: 30px;
        }

        .search-box {
            display: flex;
            background: white;
            border-radius: 12px;
            padding: 8px;
            max-width: 550px;
        }

        .search-box input {
            flex: 1;
            min-width: 0;
            border: none;
            outline: none;
            padding: 12px;
            font-size: 14px;
        }

        .search-box button {
            background: var(--blue);
            color: white;
            border: none;
            border-radius: 8px;
            padding: 0 25px;
            font-weight: 700;
        }

        /* COMMON SECTION */

        section {
            padding: 85px 0;
        }

        .section-heading {
            display: flex;
            justify-content: space-between;
            align-items: end;
            margin-bottom: 30px;
        }

        .section-heading h2 {
            font-size: 27px;
            font-weight: 800;
            margin-bottom: 8px;
        }

        .section-heading p {
            color: var(--gray);
            font-size: 14px;
        }

        .more {
            color: var(--blue);
            font-size: 13px;
            font-weight: 700;
        }

        /* MAP */

        .map-section {
            background: var(--light);
        }

        .map-layout {
            display: grid;
            grid-template-columns: 1.6fr 1fr;
            gap: 25px;
        }

        #map {
            width: 100%;
            height: 410px;
            border-radius: 15px;
            z-index: 1;
        }

        .map-info {
            background: white;
            padding: 25px;
            border-radius: 15px;
        }

        .map-info h3 {
            font-size: 19px;
            margin-bottom: 20px;
        }

        .popular-list {
            display: flex;
            flex-direction: column;
            gap: 18px;
        }

        .popular-item {
            display: flex;
            align-items: center;
            gap: 15px;
            padding-bottom: 16px;
            border-bottom: 1px solid var(--line);
        }

        .popular-number {
            color: var(--blue);
            font-size: 20px;
            font-weight: 800;
            width: 25px;
        }

        .popular-item div:nth-child(2) {
            flex: 1;
        }

        .popular-item strong {
            font-size: 14px;
        }

        .popular-item p {
            font-size: 12px;
            color: var(--gray);
            margin-top: 4px;
        }

        /* DESTINATIONS */

        .destination-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 20px;
        }

        .destination-card {
            border-radius: 14px;
            overflow: hidden;
            background: white;
            border: 1px solid var(--line);
            transition: .25s;
        }

        .destination-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 25px rgba(0,0,0,.08);
        }

        .destination-card img {
            width: 100%;
            height: 190px;
            object-fit: cover;
            display: block;
        }

        .destination-content {
            padding: 17px;
        }

        .destination-content h3 {
            font-size: 17px;
            margin-bottom: 6px;
        }

        .destination-content p {
            font-size: 12px;
            color: var(--gray);
        }

        .destination-tag {
            display: inline-block;
            color: var(--blue);
            background: #edf4ff;
            padding: 5px 9px;
            border-radius: 5px;
            font-size: 11px;
            margin-top: 13px;
        }

        /* REVIEWS */

        .review-section {
            background: var(--light);
        }

        .review-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 20px;
        }

        .review-card {
            background: white;
            border-radius: 14px;
            overflow: hidden;
        }

        .review-card img {
            width: 100%;
            height: 210px;
            object-fit: cover;
            display: block;
        }

        .review-content {
            padding: 20px;
        }

        .review-content h3 {
            font-size: 16px;
            margin-bottom: 9px;
        }

        .review-content p {
            color: var(--gray);
            font-size: 13px;
            line-height: 1.7;
        }

        .review-user {
            display: flex;
            align-items: center;
            gap: 9px;
            margin-top: 18px;
            font-size: 12px;
            font-weight: 600;
        }

        .user-icon {
            width: 30px;
            height: 30px;
            background: #e7efff;
            color: var(--blue);
            border-radius: 50%;
            display: grid;
            place-items: center;
        }

        /* ITINERARY */

        .course-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 20px;
        }

        .course-card {
            border: 1px solid var(--line);
            border-radius: 14px;
            padding: 22px;
        }

        .course-label {
            color: var(--blue);
            font-size: 12px;
            font-weight: 700;
            margin-bottom: 12px;
        }

        .course-card h3 {
            font-size: 18px;
            margin-bottom: 10px;
        }

        .course-card p {
            color: var(--gray);
            font-size: 13px;
            line-height: 1.7;
        }

        .course-bottom {
            display: flex;
            justify-content: space-between;
            margin-top: 22px;
            padding-top: 15px;
            border-top: 1px solid var(--line);
            font-size: 12px;
            color: var(--gray);
        }

        /* CTA */

        .cta {
            padding: 65px 0;
            background: #3979d9;
            color: white;
            text-align: center;
        }

        .cta h2 {
            font-size: 28px;
            margin-bottom: 12px;
        }

        .cta p {
            font-size: 14px;
            color: rgba(255,255,255,.85);
            margin-bottom: 25px;
        }

        .cta button {
            background: white;
            color: var(--blue);
            border: none;
            padding: 13px 25px;
            border-radius: 8px;
            font-weight: 700;
        }

        /* FOOTER */

        footer {
            background: #182538;
            color: white;
            padding: 45px 0;
        }

        .footer-inner {
            display: flex;
            justify-content: space-between;
            gap: 30px;
        }

        .footer-logo {
            font-size: 22px;
            font-weight: 800;
            margin-bottom: 12px;
        }

        footer p {
            color: #aab6c6;
            font-size: 12px;
            line-height: 1.8;
        }

        .footer-copy {
            margin-top: 30px;
            padding-top: 20px;
            border-top: 1px solid #354357;
            color: #8190a4;
            font-size: 11px;
        }

        /* RESPONSIVE */

        @media (max-width: 900px) {
            nav {
                gap: 15px;
            }

            .destination-grid {
                grid-template-columns: repeat(2, 1fr);
            }

            .map-layout {
                grid-template-columns: 1fr;
            }

            .review-grid,
            .course-grid {
                grid-template-columns: repeat(2, 1fr);
            }
        }

        @media (max-width: 650px) {
            header {
                height: auto;
                padding: 15px 0;
            }

            .header-inner {
                flex-wrap: wrap;
                gap: 15px;
            }

            nav {
                order: 3;
                width: 100%;
                overflow-x: auto;
                padding: 8px 0;
            }

            .header-buttons {
                margin-left: auto;
            }

            .hero {
                height: 440px;
            }

            .hero h1 {
                font-size: 34px;
            }

            section {
                padding: 60px 0;
            }

            .destination-grid,
            .review-grid,
            .course-grid {
                grid-template-columns: 1fr;
            }

            .section-heading {
                align-items: start;
                gap: 15px;
            }

            .footer-inner {
                flex-direction: column;
            }
        }
    </style>
</head>

<body>

    <!-- HEADER -->

    <header>
        <div class="container header-inner">

            <a href="#" class="logo">
                <span>📍</span> 여행일지
            </a>

            <nav>
                <a href="#map-section">여행지 찾기</a>
                <a href="#destinations">추천 여행지</a>
                <a href="#reviews">여행 후기</a>
                <a href="#courses">여행 코스</a>
            </nav>

            <div class="header-buttons">
                <button class="btn btn-outline" onclick="alert('로그인 기능은 준비 중입니다.')">로그인</button>
                <button class="btn btn-blue" onclick="alert('회원가입 기능은 준비 중입니다.')">회원가입</button>
            </div>

        </div>
    </header>


    <!-- HERO -->

    <div class="hero">
        <div class="container hero-content">

            <span class="hero-tag">YOUR TRAVEL JOURNAL</span>

            <h1>
                당신의 다음 여행을<br>
                발견해 보세요.
            </h1>

            <p>
                새로운 여행지를 찾고, 소중한 경험을 기록하고,<br>
                다른 여행자들과 이야기를 나눠보세요.
            </p>

            <form class="search-box" id="searchForm">
                <input
                    type="text"
                    id="searchInput"
                    placeholder="어디로 여행을 떠나고 싶으신가요?"
                >
                <button type="submit">여행지 검색</button>
            </form>

        </div>
    </div>


    <!-- MAP SECTION -->

    <section class="map-section" id="map-section">
        <div class="container">

            <div class="section-heading">
                <div>
                    <h2>지도로 떠나는 여행</h2>
                    <p>지도에서 다양한 여행지를 발견해 보세요.</p>
                </div>
                <a href="#destinations" class="more">여행지 둘러보기 →</a>
            </div>

            <div class="map-layout">

                <div id="map"></div>

                <div class="map-info">
                    <h3>인기 여행지 TOP 5</h3>

                    <div class="popular-list">

                        <div class="popular-item">
                            <div class="popular-number">01</div>
                            <div>
                                <strong>일본 도쿄</strong>
                                <p>도시와 문화가 공존하는 여행</p>
                            </div>
                        </div>

                        <div class="popular-item">
                            <div class="popular-number">02</div>
                            <div>
                                <strong>프랑스 파리</strong>
                                <p>낭만적인 분위기의 유럽 여행</p>
                            </div>
                        </div>

                        <div class="popular-item">
                            <div class="popular-number">03</div>
                            <div>
                                <strong>대한민국 제주도</strong>
                                <p>아름다운 자연과 휴식</p>
                            </div>
                        </div>

                        <div class="popular-item">
                            <div class="popular-number">04</div>
                            <div>
                                <strong>그리스 산토리니</strong>
                                <p>푸른 바다와 하얀 건물</p>
                            </div>
                        </div>

                        <div class="popular-item">
                            <div class="popular-number">05</div>
                            <div>
                                <strong>이탈리아 로마</strong>
                                <p>역사와 예술이 살아 있는 도시</p>
                            </div>
                        </div>

                    </div>
                </div>

            </div>
        </div>
    </section>


    <!-- DESTINATIONS -->

    <section id="destinations">
        <div class="container">

            <div class="section-heading">
                <div>
                    <h2>추천 여행지</h2>
                    <p>여행자들이 사랑하는 인기 여행지를 만나보세요.</p>
                </div>
                <a href="#map-section" class="more">전체 보기 →</a>
            </div>

            <div class="destination-grid">

                <article class="destination-card">
                    <img src="https://images.unsplash.com/photo-1540959733332-eab4deabeeaf?auto=format&fit=crop&w=700&q=85" alt="도쿄">
                    <div class="destination-content">
                        <h3>일본 도쿄</h3>
                        <p>전통과 현대가 어우러진 도시</p>
                        <span class="destination-tag">도시 여행</span>
                    </div>
                </article>

                <article class="destination-card">
                    <img src="https://images.unsplash.com/photo-1502602898657-3e91760cbb34?auto=format&fit=crop&w=700&q=85" alt="파리">
                    <div class="destination-content">
                        <h3>프랑스 파리</h3>
                        <p>예술과 낭만이 가득한 도시</p>
                        <span class="destination-tag">감성 여행</span>
                    </div>
                </article>

                <article class="destination-card">
                    <img src="https://images.unsplash.com/photo-1473116763249-2faaef81ccda?auto=format&fit=crop&w=700&q=85" alt="제주도">
                    <div class="destination-content">
                        <h3>대한민국 제주도</h3>
                        <p>자연 속에서 즐기는 여유로운 시간</p>
                        <span class="destination-tag">자연 여행</span>
                    </div>
                </article>

                <article class="destination-card">
                    <img src="https://images.unsplash.com/photo-1533105079780-92b9be482077?auto=format&fit=crop&w=700&q=85" alt="산토리니">
                    <div class="destination-content">
                        <h3>그리스 산토리니</h3>
                        <p>아름다운 바다와 이국적인 풍경</p>
                        <span class="destination-tag">휴양 여행</span>
                    </div>
                </article>

            </div>
        </div>
    </section>


    <!-- REVIEWS -->

    <section class="review-section" id="reviews">
        <div class="container">

            <div class="section-heading">
                <div>
                    <h2>여행자들의 이야기</h2>
                    <p>다른 사람들의 여행 경험을 함께 나눠보세요.</p>
                </div>
                <a href="#" class="more" onclick="alert('여행 후기 게시판은 준비 중입니다.'); return false;">후기 더 보기 →</a>
            </div>

            <div class="review-grid">

                <article class="review-card">
                    <img src="https://images.unsplash.com/photo-1516483638261-f4dbaf036963?auto=format&fit=crop&w=700&q=85" alt="이탈리아 여행">
                    <div class="review-content">
                        <h3>잊지 못할 이탈리아 여행</h3>
                        <p>골목마다 새로운 풍경이 펼쳐졌던 여행. 맛있는 음식과 아름다운 건물들이 정말 인상적이었어요.</p>
                        <div class="review-user">
                            <div class="user-icon">J</div>
                            <span>여행자 J · 이탈리아</span>
                        </div>
                    </div>
                </article>

                <article class="review-card">
                    <img src="https://images.unsplash.com/photo-1500530855697-b586d89ba3ee?auto=format&fit=crop&w=700&q=85" alt="자연 여행">
                    <div class="review-content">
                        <h3>자연 속에서 보낸 하루</h3>
                        <p>복잡한 일상에서 벗어나 자연을 바라보며 여유를 즐겼어요. 다음에도 꼭 다시 방문하고 싶어요.</p>
                        <div class="review-user">
                            <div class="user-icon">M</div>
                            <span>여행자 M · 스위스</span>
                        </div>
                    </div>
                </article>

                <article class="review-card">
                    <img src="https://images.unsplash.com/photo-1519501025264-65ba15a82390?auto=format&fit=crop&w=700&q=85" alt="도시 야경">
                    <div class="review-content">
                        <h3>밤에도 아름다운 도시</h3>
                        <p>낮과는 전혀 다른 분위기의 야경이 기억에 남아요. 사진으로 다 담을 수 없을 만큼 멋졌습니다.</p>
                        <div class="review-user">
                            <div class="user-icon">S</div>
                            <span>여행자 S · 일본</span>
                        </div>
                    </div>
                </article>

            </div>
        </div>
    </section>


    <!-- COURSES -->

    <section id="courses">
        <div class="container">

            <div class="section-heading">
                <div>
                    <h2>추천 여행 코스</h2>
                    <p>다른 여행자들이 공유한 특별한 여행 경로입니다.</p>
                </div>
                <a href="#" class="more" onclick="alert('여행 코스 게시판은 준비 중입니다.'); return false;">코스 더 보기 →</a>
            </div>

            <div class="course-grid">

                <article class="course-card">
                    <div class="course-label">DOMESTIC · 2박 3일</div>
                    <h3>제주도 감성 여행</h3>
                    <p>
                        제주공항 → 애월 카페거리 → 협재해수욕장
                        → 성산일출봉 → 섭지코지
                    </p>
                    <div class="course-bottom">
                        <span>📍 제주도</span>
                        <span>여유로운 자연 여행</span>
                    </div>
                </article>

                <article class="course-card">
                    <div class="course-label">OVERSEAS · 3박 4일</div>
                    <h3>도쿄 도심 여행</h3>
                    <p>
                        시부야 → 하라주쿠 → 신주쿠
                        → 아사쿠사 → 도쿄 스카이트리
                    </p>
                    <div class="course-bottom">
                        <span>📍 일본 도쿄</span>
                        <span>도시 탐방 여행</span>
                    </div>
                </article>

                <article class="course-card">
                    <div class="course-label">OVERSEAS · 4박 5일</div>
                    <h3>파리 낭만 여행</h3>
                    <p>
                        에펠탑 → 루브르 박물관 → 개선문
                        → 몽마르트르 → 센강
                    </p>
                    <div class="course-bottom">
                        <span>📍 프랑스 파리</span>
                        <span>문화와 예술 여행</span>
                    </div>
                </article>

            </div>
        </div>
    </section>


    <!-- CTA -->

    <section class="cta">
        <div class="container">
            <h2>당신만의 여행일지를 시작해 보세요.</h2>
            <p>새로운 장소를 발견하고, 특별한 순간을 기록하고, 여행의 즐거움을 나눠보세요.</p>
            <button onclick="alert('여행 코스 작성 기능은 준비 중입니다.')">
                나만의 여행 기록하기 →
            </button>
        </div>
    </section>


    <!-- FOOTER -->

    <footer>
        <div class="container">

            <div class="footer-inner">

                <div>
                    <div class="footer-logo">📍 여행일지</div>
                    <p>
                        나만의 여행을 발견하고,<br>
                        모두의 경험을 나누다.
                    </p>
                </div>

                <div>
                    <p>여행지 찾기　 |　 추천 여행지　 |　 여행 후기　 |　 여행 코스</p>
                    <p>서비스 소개　 |　 이용약관　 |　 개인정보처리방침</p>
                </div>

            </div>

            <div class="footer-copy">
                © 2026 여행일지. All rights reserved.
            </div>

        </div>
    </footer>


    <!-- JAVASCRIPT -->

    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

    <script>
        // 지도 생성

        const map = L.map('map').setView([25, 10], 2);

        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            attribution: '&copy; OpenStreetMap contributors'
        }).addTo(map);


        // 여행지 데이터

        const destinations = [
            {
                name: '도쿄',
                country: '일본',
                lat: 35.6762,
                lng: 139.6503
            },
            {
                name: '파리',
                country: '프랑스',
                lat: 48.8566,
                lng: 2.3522
            },
            {
                name: '제주도',
                country: '대한민국',
                lat: 33.4996,
                lng: 126.5312
            },
            {
                name: '산토리니',
                country: '그리스',
                lat: 36.3932,
                lng: 25.4615
            },
            {
                name: '로마',
                country: '이탈리아',
                lat: 41.9028,
                lng: 12.4964
            },
            {
                name: '뉴욕',
                country: '미국',
                lat: 40.7128,
                lng: -74.0060
            },
            {
                name: '방콕',
                country: '태국',
                lat: 13.7563,
                lng: 100.5018
            }
        ];


        // 지도 마커 표시

        destinations.forEach(place => {

            const marker = L.marker([place.lat, place.lng]).addTo(map);

            marker.bindPopup(`
                <strong>${place.name}</strong><br>
                ${place.country}
            `);

        });


        // 여행지 검색

        document.getElementById('searchForm').addEventListener('submit', function(event) {

            event.preventDefault();

            const keyword = document.getElementById('searchInput')
                .value.trim()
                .toLowerCase();

            if (!keyword) {
                alert('검색할 여행지를 입력해 주세요.');
                return;
            }

            const result = destinations.find(place =>
                place.name.toLowerCase().includes(keyword) ||
                place.country.toLowerCase().includes(keyword)
            );

            if (result) {

                map.setView([result.lat, result.lng], 7);

                L.popup()
                    .setLatLng([result.lat, result.lng])
                    .setContent(`<strong>${result.name}</strong><br>${result.country}`)
                    .openOn(map);

                document.getElementById('map-section').scrollIntoView({
                    behavior: 'smooth'
                });

            } else {
                alert('검색 결과가 없습니다. 다른 여행지를 검색해 주세요.');
            }

        });

    </script>

</body>
</html>
