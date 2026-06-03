<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>She Can Foundation - Empowering Women, Transforming Communities</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        /* ==========================================================================
           1. CSS VARIABLES & THEMES
           ========================================================================== */
        :root {
            /* Light Theme Palette */
            --primary: #6C63FF;
            --secondary: #A78BFA;
            --background: #F8FAFC;
            --surface: #FFFFFF;
            --text-main: #0F172A;
            --text-muted: #475569;
            --glass-bg: rgba(255, 255, 255, 0.7);
            --glass-border: rgba(255, 255, 255, 0.4);
            --shadow: 0 10px 30px -10px rgba(108, 99, 255, 0.15);
            --gradient: linear-gradient(135deg, #6C63FF 0%, #A78BFA 100%);
            
            /* Core Transitions & Radius */
            --transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            --radius: 16px;
            --max-width: 1200px;
        }

        [data-theme="dark"] {
            /* Dark Theme Palette */
            --background: #0F172A;
            --surface: #1E293B;
            --text-main: #F8FAFC;
            --text-muted: #94A3B8;
            --glass-bg: rgba(30, 41, 59, 0.7);
            --glass-border: rgba(255, 255, 255, 0.05);
            --shadow: 0 10px 30px -10px rgba(0, 0, 0, 0.5);
        }

        /* ==========================================================================
           2. BASE STYLES & RESET
           ========================================================================== */
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        html {
            scroll-behavior: smooth;
            font-family: 'Plus Jakarta Sans', sans-serif;
            font-size: 16px;
        }

        body {
            background-color: var(--background);
            color: var(--text-main);
            transition: var(--transition);
            overflow-x: hidden;
            line-height: 1.6;
        }

        a {
            text-decoration: none;
            color: inherit;
        }

        ul {
            list-style: none;
        }

        img {
            max-width: 100%;
            height: auto;
            display: block;
        }

        .container {
            width: 100%;
            max-width: var(--max-width);
            margin: 0 auto;
            padding: 0 24px;
        }

        section {
            padding: 100px 0;
        }

        /* ==========================================================================
           3. REUSABLE COMPONENTS & UTILITIES
           ========================================================================== */
        .btn {
            display: inline-flex;
            align-items: center;
            gap: 10px;
            padding: 14px 32px;
            border-radius: 50px;
            font-weight: 600;
            font-size: 1rem;
            cursor: pointer;
            transition: var(--transition);
            border: none;
        }

        .btn-primary {
            background: var(--gradient);
            color: #FFFFFF;
            box-shadow: 0 4px 15px rgba(108, 99, 255, 0.4);
        }

        .btn-primary:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(108, 99, 255, 0.6);
        }

        .glass-card {
            background: var(--glass-bg);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid var(--glass-border);
            border-radius: var(--radius);
            box-shadow: var(--shadow);
            padding: 40px;
            transition: var(--transition);
        }

        .glass-card:hover {
            transform: translateY(-5px);
        }

        /* Intersection Observer Reveal Animation Base */
        .reveal {
            opacity: 0;
            transform: translateY(40px);
            transition: opacity 0.8s ease, transform 0.8s ease;
        }

        .reveal.active {
            opacity: 1;
            transform: translateY(0);
        }

        /* ==========================================================================
           4. PRELOADER
           ========================================================================== */
        #loader {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--background);
            z-index: 9999;
            display: flex;
            justify-content: center;
            align-items: center;
            transition: opacity 0.5s ease, visibility 0.5s ease;
        }

        .spinner {
            width: 50px;
            height: 50px;
            border: 5px solid var(--secondary);
            border-top: 5px solid var(--primary);
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        /* ==========================================================================
           5. NAVIGATION BAR
           ========================================================================== */
        .navbar {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            z-index: 1000;
            background: var(--glass-bg);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border-bottom: 1px solid var(--glass-border);
            transition: var(--transition);
        }

        .nav-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
            height: 80px;
        }

        .logo {
            font-size: 1.5rem;
            font-weight: 800;
            background: var(--gradient);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .nav-menu {
            display: flex;
            align-items: center;
            gap: 32px;
        }

        .nav-link {
            font-weight: 500;
            color: var(--text-main);
            position: relative;
            padding: 8px 0;
            transition: var(--transition);
        }

        .nav-link::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--gradient);
            transition: var(--transition);
        }

        .nav-link:hover::after,
        .nav-link.active::after {
            width: 100%;
        }

        /* Dark Mode Switch Trigger */
        .theme-toggle {
            background: none;
            border: none;
            color: var(--text-main);
            font-size: 1.2rem;
            cursor: pointer;
            padding: 8px;
            border-radius: 50%;
            transition: var(--transition);
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .theme-toggle:hover {
            background: rgba(108, 99, 255, 0.1);
        }

        .nav-toggle {
            display: none;
            font-size: 1.5rem;
            background: none;
            border: none;
            color: var(--text-main);
            cursor: pointer;
        }

        /* ==========================================================================
           6. HERO SECTION
           ========================================================================== */
        .hero {
            min-height: 100vh;
            display: flex;
            align-items: center;
            position: relative;
            padding-top: 120px;
            background: radial-gradient(circle at 90% 10%, rgba(167, 139, 250, 0.1) 0%, transparent 40%),
                        radial-gradient(circle at 10% 90%, rgba(108, 99, 255, 0.1) 0%, transparent 40%);
        }

        .hero-content {
            max-width: 800px;
            margin: 0 auto;
            text-align: center;
        }

        .hero h1 {
            font-size: 3.5rem;
            font-weight: 800;
            line-height: 1.2;
            margin-bottom: 24px;
            background: linear-gradient(135deg, var(--text-main) 30%, var(--primary) 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            animation: fadeInUp 1s ease forwards;
        }

        .hero p {
            font-size: 1.25rem;
            color: var(--text-muted);
            margin-bottom: 40px;
            animation: fadeInUp 1s ease 0.2s forwards;
            opacity: 0;
        }

        .hero .btn {
            animation: fadeInUp 1s ease 0.4s forwards;
            opacity: 0;
        }

        @keyframes fadeInUp {
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* ==========================================================================
           7. ABOUT SECTION
           ========================================================================== */
        .about-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 100%));
            gap: 30px;
            margin-top: 40px;
        }

        .section-title {
            font-size: 2.5rem;
            font-weight: 700;
            text-align: center;
            margin-bottom: 50px;
            position: relative;
        }

        .section-title::after {
            content: '';
            display: block;
            width: 60px;
            height: 4px;
            background: var(--gradient);
            margin: 12px auto 0;
            border-radius: 2px;
        }

        .about-card h3 {
            font-size: 1.5rem;
            margin-bottom: 16px;
            color: var(--primary);
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .about-card p {
            color: var(--text-muted);
        }

        /* ==========================================================================
           8. IMPACT STATISTICS SECTION
           ========================================================================== */
        .stats {
            background: var(--gradient);
            color: #FFFFFF;
            position: relative;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 100%));
            gap: 40px;
            text-align: center;
        }

        .stat-item h2 {
            font-size: 3.5rem;
            font-weight: 800;
            margin-bottom: 8px;
        }

        .stat-item p {
            font-size: 1.1rem;
            opacity: 0.9;
            font-weight: 500;
        }

        /* ==========================================================================
           9. IMAGE SECTION & CTA
           ========================================================================== */
        .image-showcase {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 100%));
            gap: 50px;
            align-items: center;
        }

        .img-container {
            position: relative;
            border-radius: var(--radius);
            overflow: hidden;
            box-shadow: var(--shadow);
        }

        .img-container img {
            width: 100%;
            object-fit: cover;
            height: 450px;
            transition: transform 0.5s ease;
        }

        .img-container:hover img {
            transform: scale(1.05);
        }

        .cta-box {
            text-align: center;
            max-width: 700px;
            margin: 0 auto;
        }

        .cta-box h2 {
            font-size: 2.5rem;
            margin-bottom: 20px;
        }

        .cta-box p {
            color: var(--text-muted);
            margin-bottom: 32px;
            font-size: 1.1rem;
        }

        /* ==========================================================================
           10. FOOTER
           ========================================================================== */
        .footer {
            background: var(--surface);
            padding: 40px 0;
            border-top: 1px solid var(--glass-border);
            transition: var(--transition);
        }

        .footer-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 24px;
            text-align: center;
        }

        .social-links {
            display: flex;
            gap: 20px;
        }

        .social-icon {
            width: 45px;
            height: 45px;
            border-radius: 50%;
            background: var(--background);
            color: var(--text-main);
            display: flex;
            align-items: center;
            justify-content: center;
            transition: var(--transition);
            border: 1px solid var(--glass-border);
        }

        .social-icon:hover {
            background: var(--gradient);
            color: #FFFFFF;
            transform: translateY(-3px);
        }

        .copyright {
            color: var(--text-muted);
            font-size: 0.9rem;
        }

        /* ==========================================================================
           11. BACK TO TOP BUTTON
           ========================================================================== */
        .back-to-top {
            position: fixed;
            bottom: 30px;
            right: 30px;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: var(--gradient);
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            border: none;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(108, 99, 255, 0.3);
            opacity: 0;
            visibility: hidden;
            transition: var(--transition);
            z-index: 999;
        }

        .back-to-top.visible {
            opacity: 1;
            visibility: visible;
        }

        .back-to-top:hover {
            transform: translateY(-5px);
        }

        /* ==========================================================================
           12. RESPONSIVE MEDIA QUERIES (Mobile First)
           ========================================================================== */
        @media (min-width: 768px) {
            .about-grid {
                grid-template-columns: repeat(2, 100%);
            }
            .stats-grid {
                grid-template-columns: repeat(3, 100%);
            }
            .image-showcase {
                grid-template-columns: 1fr 1fr;
            }
        }

        @media (min-width: 1024px) {
            .hero h1 { font-size: 4.5rem; }
            .about-grid { grid-template-columns: repeat(2, 1fr); }
            .stats-grid { grid-template-columns: repeat(3, 1fr); }
        }

        @media (max-width: 767px) {
            .nav-menu {
                position: fixed;
                top: 80px;
                left: -100%;
                width: 100%;
                height: calc(100vh - 80px);
                background: var(--surface);
                flex-direction: column;
                padding: 40px 24px;
                gap: 24px;
                transition: var(--transition);
                align-items: flex-start;
                box-shadow: var(--shadow);
            }

            .nav-menu.active {
                left: 0;
            }

            .nav-toggle {
                display: block;
                order: 3;
            }

            .theme-toggle {
                margin-left: auto;
                margin-right: 16px;
                order: 2;
            }
            
            .hero h1 { font-size: 2.5rem; }
            section { padding: 60px 0; }
        }
    </style>
</head>
<body>

    <div id="loader" aria-hidden="true">
        <div class="spinner"></div>
    </div>

    <header class="navbar">
        <div class="container nav-container">
            <a href="#hero" class="logo" aria-label="She Can Foundation Home">
                <i class="fa-solid fa-hand-holding-heart"></i> She Can Foundation
            </a>
            
            <button class="nav-toggle" id="navToggle" aria-label="Toggle navigation menu" aria-expanded="false">
                <i class="fa-solid fa-bars"></i>
            </button>

            <button class="theme-toggle" id="themeToggle" aria-label="Toggle dark mode">
                <i class="fa-solid fa-moon"></i>
            </button>

            <nav class="nav-menu" id="navMenu">
                <ul>
                    <li style="display:inline-block; margin: 0 16px;"><a href="#hero" class="nav-link active">Home</a></li>
                    <li style="display:inline-block; margin: 0 16px;"><a href="#about" class="nav-link">About</a></li>
                    <li style="display:inline-block; margin: 0 16px;"><a href="#impact" class="nav-link">Impact</a></li>
                    <li style="display:inline-block; margin: 0 16px;"><a href="#showcase" class="nav-link">Our Work</a></li>
                </ul>
            </nav>
        </div>
    </header>

    <main>
        <section id="hero" class="hero">
            <div class="container hero-content">
                <h1>Empowering Women,<br>Transforming Communities</h1>
                <p>We break barriers by providing structural opportunities, foundational education, and economic independence pipelines to women and girls globally.</p>
                <a href="#cta" class="btn btn-primary">Join Our Mission <i class="fa-solid fa-arrow-right"></i></a>
            </div>
        </section>

        <section id="about" class="reveal">
            <div class="container">
                <h2 class="section-title">Who We Are</h2>
                <div class="about-grid">
                    <div class="glass-card about-card">
                        <h3><i class="fa-solid fa-eye"></i> Our Vision</h3>
                        <p>To cultivate an inclusive world where every woman possesses the agency, education, and systemic support needed to construct her own future and lift her community tier by tier.</p>
                    </div>
                    <div class="glass-card about-card">
                        <h3><i class="fa-solid fa-bullseye"></i> Our Mission</h3>
                        <p>We actively dismantle socio-economic inequalities by implementing scalable vocational training, modern digital literacy labs, legal aid clinics, and dynamic mentorship networks.</p>
                    </div>
                </div>
            </div>
        </section>

        <section id="impact" class="stats">
            <div class="container stats-grid">
                <div class="stat-item">
                    <h2 class="counter" data-target="25000">0</h2>
                    <p>Women Empowered</p>
                </div>
                <div class="stat-item">
                    <h2 class="counter" data-target="120">0</h2>
                    <p>Communities Reached</p>
                </div>
                <div class="stat-item">
                    <h2 class="counter" data-target="1500">0</h2>
                    <p>Volunteers</p>
                </div>
            </div>
        </section>

        <section id="showcase" class="reveal">
            <div class="container image-showcase">
                <div class="img-container">
                    <img src="https://images.unsplash.com/photo-1573496359142-b8d87734a5a2?auto=format&fit=crop&q=80&w=800" alt="Empowered corporate leaders collaborating in an office space">
                </div>
                <div>
                    <h2 style="font-size: 2rem; margin-bottom: 20px;">Driving Sustainable, Generational Change</h2>
                    <p style="color: var(--text-muted); margin-bottom: 20px;">When you structurally support one woman, you reliably impact an entire communityecosystem. Our localized educational initiatives focus on structural autonomy, leadership acceleration, and sustainable community economic frameworks.</p>
                    <p style="color: var(--text-muted);">By creating highly repeatable frameworks for equity, our foundation ensures long-term operational resilience that self-sustains over generations.</p>
                </div>
            </div>
        </section>

        <section id="cta" class="reveal" style="background: radial-gradient(circle at center, rgba(167, 139, 250, 0.05) 0%, transparent 70%);">
            <div class="container cta-box">
                <h2>Ready to Make an Impact?</h2>
                <p>Your advocacy, time, or contributions directly sustain our field training operations. Partner with us today to accelerate global gender equity alongside global communities.</p>
                <button class="btn btn-primary" onclick="alert('Thank you for your willingness to join! A registration portal will go live shortly.')">Join Our Mission <i class="fa-solid fa-heart"></i></button>
            </div>
        </section>
    </main>

    <footer class="footer">
        <div class="container footer-container">
            <div class="logo">
                <i class="fa-solid fa-hand-holding-heart"></i> She Can Foundation
            </div>
            <div class="social-links">
                <a href="#" class="social-icon" aria-label="Facebook"><i class="fa-brands fa-facebook-f"></i></a>
                <a href="#" class="social-icon" aria-label="Twitter"><i class="fa-brands fa-x-twitter"></i></a>
                <a href="#" class="social-icon" aria-label="Instagram"><i class="fa-brands fa-instagram"></i></a>
                <a href="#" class="social-icon" aria-label="LinkedIn"><i class="fa-brands fa-linkedin-in"></i></a>
            </div>
            <p class="copyright">&copy; <span id="year"></span> She Can Foundation. All rights reserved.</p>
        </div>
    </footer>

    <button class="back-to-top" id="backToTop" aria-label="Scroll to top of page">
        <i class="fa-solid fa-arrow-up"></i>
    </button>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            
            // 1. Loading screen termination
            const loader = document.getElementById('loader');
            window.addEventListener('load', () => {
                loader.style.opacity = '0';
                loader.style.visibility = 'hidden';
            });

            // 2. Dynamic Copyright Year Assignment
            document.getElementById('year').textContent = new Date().getFullYear();

            // 3. Dark Mode Core Engine & Syncing Preferences
            const themeToggle = document.getElementById('themeToggle');
            const toggleIcon = themeToggle.querySelector('i');
            
            const setTheme = (theme) => {
                document.documentElement.setAttribute('data-theme', theme);
                localStorage.setItem('theme', theme);
                if (theme === 'dark') {
                    toggleIcon.className = 'fa-solid fa-sun';
                } else {
                    toggleIcon.className = 'fa-solid fa-moon';
                }
            };

            // Detect matching saved storage settings or environment system settings
            const savedTheme = localStorage.getItem('theme');
            const systemPrefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
            
            if (savedTheme) {
                setTheme(savedTheme);
            } else if (systemPrefersDark) {
                setTheme('dark');
            }

            themeToggle.addEventListener('click', () => {
                const currentTheme = document.documentElement.getAttribute('data-theme');
                setTheme(currentTheme === 'dark' ? 'light' : 'dark');
            });

            // 4. Mobile Responsive Dropdown Menu Toggle Handler
            const navToggle = document.getElementById('navToggle');
            const navMenu = document.getElementById('navMenu');
            const menuLinks = document.querySelectorAll('.nav-link');

            const toggleMenu = () => {
                const isExpanded = navToggle.getAttribute('aria-expanded') === 'true';
                navToggle.setAttribute('aria-expanded', !isExpanded);
                navMenu.classList.toggle('active');
                navToggle.querySelector('i').classList.toggle('fa-bars');
                navToggle.querySelector('i').classList.toggle('fa-xmark');
            };

            navToggle.addEventListener('click', toggleMenu);

            menuLinks.forEach(link => {
                link.addEventListener('click', () => {
                    if (navMenu.classList.contains('active')) toggleMenu();
                });
            });

            // 5. Statistics Frame Animated Counters System
            const counters = document.querySelectorAll('.counter');
            const animationSpeed = 200; // Lower numbers equal faster calculation increments

            const startCounter = (counter) => {
                const updateCount = () => {
                    const target = +counter.getAttribute('data-target');
                    const count = +counter.innerText;
                    const increment = Math.ceil(target / animationSpeed);

                    if (count < target) {
                        counter.innerText = count + increment;
                        setTimeout(updateCount, 15);
                    } else {
                        counter.innerText = target.toLocaleString() + "+";
                    }
                };
                updateCount();
            };

            // 6. Navigation Link Highlighting Sync Engine via Scroll Spatial Assessment
            const sections = document.querySelectorAll('section');
            
            const activeNavOnScroll = () => {
                let scrollPosition = window.scrollY + 150;

                sections.forEach(section => {
                    if (scrollPosition >= section.offsetTop && scrollPosition < section.offsetTop + section.offsetHeight) {
                        const currentId = section.getAttribute('id');
                        menuLinks.forEach(link => {
                            link.classList.remove('active');
                            if (link.getAttribute('href') === `#${currentId}`) {
                                link.classList.add('active');
                            }
                        });
                    }
                });
            };

            // 7. Floating Action Interface Controls (Back To Top Utility)
            const backToTopBtn = document.getElementById('backToTop');
            
            const handleScrollUtils = () => {
                // Toggle Button Viewability
                if (window.scrollY > 400) {
                    backToTopBtn.classList.add('visible');
                } else {
                    backToTopBtn.classList.remove('visible');
                }
                activeNavOnScroll();
            };

            window.addEventListener('scroll', handleScrollUtils);
            
            backToTopBtn.addEventListener('click', () => {
                window.scrollTo({ top: 0, behavior: 'smooth' });
            });

            // 8. Intersection Observer Strategy for Global Animations & Component Triggers
            const revealOptions = {
                threshold: 0.15,
                rootMargin: "0px 0px -50px 0px"
            };

            const observer = new IntersectionObserver((entries, observer) => {
                entries.forEach(entry => {
                    if (!entry.isIntersecting) return;
                    
                    // Trigger elements using reveal animations
                    if (entry.target.classList.contains('reveal')) {
                        entry.target.classList.add('active');
                        observer.unobserve(entry.target);
                    }
                    
                    // Trigger numerical animation routines safely inside target container boundaries
                    if (entry.target.id === 'impact') {
                        counters.forEach(counter => startCounter(counter));
                        observer.unobserve(entry.target);
                    }
                });
            }, revealOptions);

            // Subscribing target structural elements into functional observation arrays
            document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
            const impactSection = document.getElementById('impact');
            if (impactSection) observer.observe(impactSection);
        });
    </script>
</body>
</html>
