<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GloveLingo - Sign Language Translation</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-pink: #FF6B9D;
            --primary-purple: #9B59B6;
            --secondary-pink: #FFB3D1;
            --secondary-purple: #D2B4DE;
            --light-pink: #FCE4EC;
            --dark-purple: #6A1B9A;
            --gradient-1: linear-gradient(135deg, #FF6B9D 0%, #9B59B6 100%);
            --gradient-2: linear-gradient(45deg, #FFB3D1 0%, #D2B4DE 100%);
            --gradient-3: linear-gradient(180deg, #FCE4EC 0%, #E1BEE7 100%);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Poppins', sans-serif;
            line-height: 1.6;
            color: #333;
            overflow-x: hidden;
        }

        /* Animated background */
        .animated-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            background: var(--gradient-1);
            animation: gradientShift 10s ease infinite;
        }

        @keyframes gradientShift {
            0%, 100% { background: var(--gradient-1); }
            50% { background: var(--gradient-2); }
        }

        .floating-shapes {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: -1;
        }

        .shape {
            position: absolute;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.1);
            animation: float 6s ease-in-out infinite;
        }

        .shape:nth-child(1) { width: 80px; height: 80px; top: 20%; left: 10%; animation-delay: 0s; }
        .shape:nth-child(2) { width: 120px; height: 120px; top: 60%; left: 80%; animation-delay: 2s; }
        .shape:nth-child(3) { width: 60px; height: 60px; top: 80%; left: 20%; animation-delay: 4s; }

        @keyframes float {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-20px) rotate(180deg); }
        }

        /* Navbar */
        .navbar {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
            transition: all 0.3s ease;
        }

        .navbar-brand {
            font-weight: 800;
            font-size: 1.8rem;
            background: var(--gradient-1);
            -webkit-background-clip: text;
            background-clip: text;
            -webkit-text-fill-color: transparent;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        .nav-link {
            font-weight: 500;
            color: var(--dark-purple) !important;
            position: relative;
            transition: all 0.3s ease;
        }

        .nav-link:hover {
            color: var(--primary-pink) !important;
            transform: translateY(-2px);
        }

        .nav-link::after {
            content: '';
            position: absolute;
            width: 0;
            height: 2px;
            bottom: 0;
            left: 50%;
            background: var(--gradient-1);
            transition: all 0.3s ease;
            transform: translateX(-50%);
        }

        .nav-link:hover::after {
            width: 100%;
        }

        /* Hero Section */
        .hero-section {
            height: 100vh;
            display: flex;
            align-items: center;
            position: relative;
            overflow: hidden;
        }

        .hero-content {
            text-align: center;
            color: white;
            z-index: 2;
        }

        .hero-title {
            font-size: 4rem;
            font-weight: 800;
            margin-bottom: 2rem;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
            animation: fadeInUp 1s ease;
        }

        .hero-subtitle {
            font-size: 1.3rem;
            margin-bottom: 3rem;
            opacity: 0.9;
            animation: fadeInUp 1s ease 0.2s both;
        }

        .cta-button {
            background: rgba(255, 255, 255, 0.2);
            border: 2px solid white;
            color: white;
            padding: 15px 40px;
            border-radius: 50px;
            font-weight: 600;
            text-decoration: none;
            display: inline-block;
            transition: all 0.3s ease;
            animation: fadeInUp 1s ease 0.4s both;
        }

        .cta-button:hover {
            background: white;
            color: var(--primary-purple);
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* Section Styles */
        .section {
            padding: 100px 0;
            position: relative;
        }

        .section-title {
            font-size: 3rem;
            font-weight: 700;
            text-align: center;
            margin-bottom: 4rem;
            background: var(--gradient-1);
            -webkit-background-clip: text;
            background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .card-custom {
            background: rgba(255, 255, 255, 0.95);
            border: none;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.1);
            transition: all 0.3s ease;
            backdrop-filter: blur(10px);
            overflow: hidden;
        }

        .card-custom:hover {
            transform: translateY(-10px);
            box-shadow: 0 25px 50px rgba(0, 0, 0, 0.15);
        }

        .card-header-custom {
            background: var(--gradient-1);
            color: white;
            padding: 2rem;
            border: none;
        }

        .timeline-item {
            background: rgba(255, 255, 255, 0.9);
            border-radius: 15px;
            padding: 2rem;
            margin-bottom: 2rem;
            border-left: 5px solid var(--primary-pink);
            transition: all 0.3s ease;
        }

        .timeline-item:hover {
            transform: translateX(10px);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
        }

        .timeline-year {
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--primary-purple);
            margin-bottom: 1rem;
        }

        /* FAQ Section */
        .faq-item {
            background: rgba(255, 255, 255, 0.9);
            border-radius: 15px;
            margin-bottom: 1rem;
            overflow: hidden;
            transition: all 0.3s ease;
        }

        .faq-question {
            background: var(--gradient-2);
            padding: 1.5rem 2rem;
            cursor: pointer;
            font-weight: 600;
            color: var(--dark-purple);
            border: none;
            width: 100%;
            text-align: left;
            transition: all 0.3s ease;
        }

        .faq-question:hover {
            background: var(--gradient-1);
            color: white;
        }

        .faq-answer {
            padding: 2rem;
            background: white;
            color: #666;
            line-height: 1.8;
        }

        /* Footer */
        .footer {
            background: var(--gradient-1);
            color: white;
            padding: 4rem 0 2rem;
            position: relative;
        }

        .footer::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 1px;
            background: linear-gradient(90deg, transparent, white, transparent);
        }

        .footer-title {
            font-size: 1.5rem;
            font-weight: 700;
            margin-bottom: 2rem;
        }

        .footer-link {
            color: rgba(255, 255, 255, 0.8);
            text-decoration: none;
            transition: all 0.3s ease;
            display: block;
            margin-bottom: 0.5rem;
        }

        .footer-link:hover {
            color: white;
            transform: translateX(5px);
        }

        .social-icons a {
            display: inline-block;
            width: 50px;
            height: 50px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 50%;
            text-align: center;
            line-height: 50px;
            margin-right: 1rem;
            color: white;
            font-size: 1.2rem;
            transition: all 0.3s ease;
        }

        .social-icons a:hover {
            background: white;
            color: var(--primary-purple);
            transform: translateY(-3px);
        }

        /* Responsive */
        @media (max-width: 768px) {
            .hero-title {
                font-size: 2.5rem;
            }
            
            .section-title {
                font-size: 2rem;
            }
            
            .hero-section {
                height: 80vh;
            }
        }

        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }

        ::-webkit-scrollbar-track {
            background: var(--light-pink);
        }

        ::-webkit-scrollbar-thumb {
            background: var(--gradient-1);
            border-radius: 4px;
        }

        /* Loading animation */
        .loading-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--gradient-1);
            z-index: 9999;
            display: flex;
            align-items: center;
            justify-content: center;
            opacity: 1;
            transition: opacity 0.5s ease;
        }

        .loading-overlay.hidden {
            opacity: 0;
            pointer-events: none;
        }

        .spinner {
            width: 50px;
            height: 50px;
            border: 3px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            border-top-color: white;
            animation: spin 1s ease-in-out infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <!-- Loading Overlay -->
    <div class="loading-overlay" id="loadingOverlay">
        <div class="spinner"></div>
    </div>

    <!-- Animated Background -->
    <div class="animated-bg"></div>
    <div class="floating-shapes">
        <div class="shape"></div>
        <div class="shape"></div>
        <div class="shape"></div>
    </div>

    <!-- Navbar -->
    <nav class="navbar navbar-expand-lg fixed-top">
        <div class="container">
            <a class="navbar-brand" href="#home">
                <i class="fas fa-hand-paper me-2"></i>GloveLingo
            </a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav ms-auto">
                    <li class="nav-item">
                        <a class="nav-link" href="#home">Home</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#about">About</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#description">Description</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#history">History</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#faq">FAQ</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#contact">Contact</a>
                    </li>
                </ul>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
    <section id="home" class="hero-section">
        <div class="container">
            <div class="row justify-content-center">
                <div class="col-lg-8">
                    <div class="hero-content">
                        <h1 class="hero-title">
                            <i class="fas fa-hand-sparkles mb-3 d-block"></i>
                            GloveLingo
                        </h1>
                        <p class="hero-subtitle">
                            Bridging Communication Through Innovation<br>
                            Translating Sign Language into Speech & Text
                        </p>
                        <a href="#about" class="cta-button">
                            <i class="fas fa-arrow-down me-2"></i>
                            Discover More
                        </a>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- About Section -->
    <section id="about" class="section">
        <div class="container">
            <h2 class="section-title">About GloveLingo</h2>
            <div class="row align-items-center">
                <div class="col-lg-6 mb-4">
                    <div class="card-custom h-100">
                        <div class="card-body p-4">
                            <div class="d-flex align-items-center mb-3">
                                <i class="fas fa-lightbulb fs-2 me-3" style="color: var(--primary-pink);"></i>
                                <h3 style="color: var(--primary-purple);">Innovation</h3>
                            </div>
                            <p class="lead">GloveLingo is an assistive technology project aimed at enabling real-time communication between deaf individuals who use American Sign Language (ASL) and those who do not understand sign language.</p>
                        </div>
                    </div>
                </div>
                <div class="col-lg-6 mb-4">
                    <div class="card-custom h-100">
                        <div class="card-body p-4">
                            <div class="d-flex align-items-center mb-3">
                                <i class="fas fa-cogs fs-2 me-3" style="color: var(--primary-pink);"></i>
                                <h3 style="color: var(--primary-purple);">Technology</h3>
                            </div>
                            <p class="lead">The system is built around a smart glove that detects hand gestures and translates them into text or speech using simple, efficient logic without machine learning or internet connectivity.</p>
                        </div>
                    </div>
                </div>
                <div class="col-12">
                    <div class="card-custom">
                        <div class="card-body p-4">
                            <div class="row">
                                <div class="col-md-4 text-center mb-3">
                                    <i class="fas fa-bluetooth fs-1 mb-3" style="color: var(--primary-pink);"></i>
                                    <h5 style="color: var(--primary-purple);">Bluetooth Connectivity</h5>
                                    <p>Wireless connection via HC-05 module</p>
                                </div>
                                <div class="col-md-4 text-center mb-3">
                                    <i class="fas fa-dollar-sign fs-1 mb-3" style="color: var(--primary-pink);"></i>
                                    <h5 style="color: var(--primary-purple);">Affordable</h5>
                                    <p>Cost-effective solution for daily use</p>
                                </div>
                                <div class="col-md-4 text-center mb-3">
                                    <i class="fas fa-mobile-alt fs-1 mb-3" style="color: var(--primary-pink);"></i>
                                    <h5 style="color: var(--primary-purple);">Portable</h5>
                                    <p>Easy to use mobile integration</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Description Section -->
    <section id="description" class="section" style="background: var(--gradient-3);">
        <div class="container">
            <h2 class="section-title">System Description</h2>
            <div class="row">
                <div class="col-lg-6 mb-4">
                    <div class="card-custom">
                        <div class="card-header-custom">
                            <h4><i class="fas fa-microchip me-2"></i>System Architecture</h4>
                        </div>
                        <div class="card-body p-4">
                            <div class="mb-4">
                                <h6 class="fw-bold" style="color: var(--primary-purple);">Smart Glove Hardware</h6>
                                <ul class="list-unstyled ms-3">
                                    <li><i class="fas fa-hand-point-right me-2" style="color: var(--primary-pink);"></i>Flex Sensors on each finger</li>
                                    <li><i class="fas fa-hand-point-right me-2" style="color: var(--primary-pink);"></i>Variable resistor technology</li>
                                    <li><i class="fas fa-hand-point-right me-2" style="color: var(--primary-pink);"></i>Real-time gesture detection</li>
                                </ul>
                            </div>
                            <div class="mb-4">
                                <h6 class="fw-bold" style="color: var(--primary-purple);">Microcontroller</h6>
                                <ul class="list-unstyled ms-3">
                                    <li><i class="fas fa-hand-point-right me-2" style="color: var(--primary-pink);"></i>Arduino Uno/Nano</li>
                                    <li><i class="fas fa-hand-point-right me-2" style="color: var(--primary-pink);"></i>C/C++ Programming</li>
                                    <li><i class="fas fa-hand-point-right me-2" style="color: var(--primary-pink);"></i>Threshold-based recognition</li>
                                </ul>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="col-lg-6 mb-4">
                    <div class="card-custom">
                        <div class="card-header-custom">
                            <h4><i class="fas fa-bullseye me-2"></i>Project Objectives</h4>
                        </div>
                        <div class="card-body p-4">
                            <div class="mb-3">
                                <div class="d-flex align-items-center mb-2">
                                    <i class="fas fa-check-circle me-2" style="color: var(--primary-pink);"></i>
                                    <span class="fw-bold">Gesture Recognition</span>
                                </div>
                                <p class="mb-0 ms-4">Convert finger gestures into digital signals using sensors</p>
                            </div>
                            <div class="mb-3">
                                <div class="d-flex align-items-center mb-2">
                                    <i class="fas fa-check-circle me-2" style="color: var(--primary-pink);"></i>
                                    <span class="fw-bold">Logic Processing</span>
                                </div>
                                <p class="mb-0 ms-4">Process signals using pure logic-based programming in C</p>
                            </div>
                            <div class="mb-3">
                                <div class="d-flex align-items-center mb-2">
                                    <i class="fas fa-check-circle me-2" style="color: var(--primary-pink);"></i>
                                    <span class="fw-bold">Wireless Communication</span>
                                </div>
                                <p class="mb-0 ms-4">Transmit recognized gestures via Bluetooth</p>
                            </div>
                            <div class="mb-3">
                                <div class="d-flex align-items-center mb-2">
                                    <i class="fas fa-check-circle me-2" style="color: var(--primary-pink);"></i>
                                    <span class="fw-bold">Output Display</span>
                                </div>
                                <p class="mb-0 ms-4">Display text and convert to speech on mobile devices</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="text-center mt-4">
                <div class="d-inline-flex align-items-center">
                    <i class="fas fa-hand-point-right fs-1 me-4" style="color: var(--primary-pink);"></i>
                    <i class="fas fa-hand-rock fs-1 me-4" style="color: var(--primary-purple);"></i>
                    <i class="fas fa-hand-peace fs-1" style="color: var(--primary-pink);"></i>
                </div>
            </div>
        </div>
    </section>

    <!-- History Section -->
    <section id="history" class="section">
        <div class="container">
            <h2 class="section-title">The History of American Sign Language (ASL)</h2>
            <div class="row">
                <div class="col-lg-4 mb-4">
                    <div class="timeline-item">
                        <div class="timeline-year">Pre-1800s</div>
                        <h5 style="color: var(--primary-purple);">Early Signs and Communication</h5>
                        <p>Before ASL existed as a structured language, various forms of home sign were used by deaf individuals and families in the U.S. In Martha's Vineyard, a large deaf population led to the development of Martha's Vineyard Sign Language (MVSL).</p>
                    </div>
                </div>
                <div class="col-lg-4 mb-4">
                    <div class="timeline-item">
                        <div class="timeline-year">1817</div>
                        <h5 style="color: var(--primary-purple);">The Birth of ASL</h5>
                        <p>Thomas Hopkins Gallaudet co-founded the American School for the Deaf with Laurent Clerc. Students brought their home signs which combined with French Sign Language to form early ASL - a new creation rooted in American experiences.</p>
                    </div>
                </div>
                <div class="col-lg-4 mb-4">
                    <div class="timeline-item">
                        <div class="timeline-year">Mid-Late 1800s</div>
                        <h5 style="color: var(--primary-purple);">Growth of Deaf Education</h5>
                        <p>More schools for the deaf were established across the United States. ASL continued to develop and evolve as a natural language within deaf communities, spreading through educational institutions and social networks.</p>
                    </div>
                </div>
                <div class="col-lg-6 mb-4">
                    <div class="timeline-item">
                        <div class="timeline-year">1880</div>
                        <h5 style="color: var(--primary-purple);">The Milan Conference</h5>
                        <p>The Second International Congress on Education of the Deaf concluded that oral education was superior. Many deaf schools banned ASL, and deaf teachers were replaced by hearing ones. Despite this, ASL survived through the deaf community's efforts.</p>
                    </div>
                </div>
                <div class="col-lg-6 mb-4">
                    <div class="timeline-item">
                        <div class="timeline-year">1960s</div>
                        <h5 style="color: var(--primary-purple);">Linguistic Recognition</h5>
                        <p>Dr. William Stokoe proved ASL was a complete language with its own structure and grammar. His research reversed decades of stigma and sparked academic interest in sign language and deaf culture.</p>
                    </div>
                </div>
                <div class="col-12 mb-4">
                    <div class="timeline-item">
                        <div class="timeline-year">1970s-1990s</div>
                        <h5 style="color: var(--primary-purple);">Rise of Deaf Culture and Advocacy</h5>
                        <p>Deaf pride and culture flourished with Total Communication and Bi-Bi education. The 1988 Deaf President Now protest at Gallaudet University marked a turning point in deaf empowerment and leadership.</p>
                    </div>
                </div>
                <div class="col-lg-6 mb-4">
                    <div class="timeline-item">
                        <div class="timeline-year">2000s-Present</div>
                        <h5 style="color: var(--primary-purple);">Widespread Recognition</h5>
                        <p>ASL became one of the most studied languages in the U.S., with online learning apps, deaf influencers on social media, and ADA requirements for interpreters in many settings.</p>
                    </div>
                </div>
                <div class="col-lg-6 mb-4">
                    <div class="timeline-item">
                        <div class="timeline-year">ASL Today</div>
                        <h5 style="color: var(--primary-purple);">Thriving Language</h5>
                        <p>Today, ASL is a thriving, evolving language used by hundreds of thousands of people. It remains distinct from English - a language in its own right with unique syntax, idioms, history, and beauty.</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- FAQ Section -->
    <section id="faq" class="section" style="background: var(--gradient-3);">
        <div class="container">
            <h2 class="section-title">Frequently Asked Questions</h2>
            <p class="text-center mb-5 fs-5" style="color: var(--dark-purple);">If you have any questions, check our FAQs or contact us</p>
            
            <div class="row justify-content-center">
                <div class="col-lg-8">
                    <div class="faq-item">
                        <button class="faq-question" onclick="toggleFAQ(1)">
                            1. What is GloveLingo? <i class="fas fa-chevron-down float-end"></i>
                        </button>
                        <div class="faq-answer" id="faq1" style="display: none;">
                            GloveLingo is a smart glove system that translates American Sign Language (ASL) hand gestures into text and speech in real time using sensors, a microcontroller, and Bluetooth.
                        </div>
                    </div>
                    
                    <div class="faq-item">
                        <button class="faq-question" onclick="toggleFAQ(2)">
                            2. Who created GloveLingo? <i class="fas fa-chevron-down float-end"></i>
                        </button>
                        <div class="faq-answer" id="faq2" style="display: none;">
                            GloveLingo was developed by two senior computer engineering students at the Lebanese International University (LIU), as part of their graduation project.
                        </div>
                    </div>
                    
                    <div class="faq-item">
                        <button class="faq-question" onclick="toggleFAQ(3)">
                            3. Why was this project created? <i class="fas fa-chevron-down float-end"></i>
                        </button>
                        <div class="faq-answer" id="faq3" style="display: none;">
                            We wanted to support the deaf and hard-of-hearing community by building a practical, low-cost communication tool that works without internet or advanced technologies.
                        </div>
                    </div>
                    
                    <div class="faq-item">
                        <button class="faq-question" onclick="toggleFAQ(4)">
                            4. How does GloveLingo work? <i class="fas fa-chevron-down float-end"></i>
                        </button>
                        <div class="faq-answer" id="faq4" style="display: none;">
                            The glove uses flex sensors on each finger to detect gestures. A microcontroller processes the data using logic written in C, and the result is sent via Bluetooth to a smartphone for display or speech output.
                        </div>
                    </div>
                    
                    <div class="faq-item">
                        <button class="faq-question" onclick="toggleFAQ(5)">
                            5. Does GloveLingo use Wi-Fi or the Internet? <i class="fas fa-chevron-down float-end"></i>
                        </button>
                        <div class="faq-answer" id="faq5" style="display: none;">
                            No. GloveLingo works offline. It uses Bluetooth only to connect the glove to a smartphone.
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="footer">
        <div class="container">
            <div class="text-center mb-5">
                <div style="height: 2px; background: linear-gradient(90deg, transparent, white, transparent); margin: 0 auto 3rem;"></div>
            </div>
            
            <div class="row">
                <div class="col-lg-4 mb-4">
                    <h3 class="footer-title">
                        <i class="fas fa-hand-sparkles me-2"></i>
                        GloveLingo
                    </h3>
                    <p class="mb-4">Bridging communication barriers through innovative technology and empowering the deaf community with accessible solutions.</p>
                    <div class="social-icons">
                        <a href="#"><i class="fab fa-facebook-f"></i></a>
                        <a href="#"><i class="fab fa-instagram"></i></a>
                        <a href="#"><i class="fab fa-tiktok"></i></a>
                        <a href="#"><i class="fab fa-pinterest"></i></a>
                        <a href="#"><i class="fab fa-youtube"></i></a>
                    </div>
                </div>
                
                <div class="col-lg-4 mb-4">
                    <h4 class="footer-title">Get In Touch</h4>
                    <div class="mb-3">
                        <i class="fas fa-phone me-3"></i>
                        <span class="fs-5">81924161</span>
                    </div>
                    <div class="mb-3">
                        <i class="fas fa-envelope me-3"></i>
                        <span>info@glovelingo.com</span>
                    </div>
                    <div class="mb-3">
                        <i class="fas fa-map-marker-alt me-3"></i>
                        <span>Lebanese International University, Lebanon</span>
                    </div>
                </div>
                
                <div class="col-lg-4 mb-4">
                    <h4 class="footer-title">Quick Links</h4>
                    <a href="#about" class="footer-link">
                        <i class="fas fa-chevron-right me-2"></i>About Sign Language
                    </a>
                    <a href="#description" class="footer-link">
                        <i class="fas fa-chevron-right me-2"></i>System Description
                    </a>
                    <a href="#history" class="footer-link">
                        <i class="fas fa-chevron-right me-2"></i>ASL History
                    </a>
                    <a href="#faq" class="footer-link">
                        <i class="fas fa-chevron-right me-2"></i>FAQ
                    </a>
                    <a href="#" class="footer-link">
                        <i class="fas fa-chevron-right me-2"></i>Privacy Policy
                    </a>
                    <a href="#" class="footer-link">
                        <i class="fas fa-chevron-right me-2"></i>Terms of Service
                    </a>
                </div>
            </div>
            
            <div class="text-center mt-5">
                <div style="height: 2px; background: linear-gradient(90deg, transparent, white, transparent); margin: 2rem auto;"></div>
                <div class="row">
                    <div class="col-md-6 mb-2">
                        <span>&copy; 2025 GloveLingo. All rights reserved.</span>
                    </div>
                    <div class="col-md-6 mb-2">
                        <span>Developed with <i class="fas fa-heart" style="color: #ff6b9d;"></i> for the deaf community</span>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Scripts -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        // Loading animation
        window.addEventListener('load', function() {
            setTimeout(() => {
                document.getElementById('loadingOverlay').classList.add('hidden');
            }, 1000);
        });

        // Smooth scrolling for navigation links
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    target.scrollIntoView({
                        behavior: 'smooth',
                        block: 'start'
                    });
                }
            });
        });

        // Navbar background change on scroll
        window.addEventListener('scroll', function() {
            const navbar = document.querySelector('.navbar');
            if (window.scrollY > 50) {
                navbar.style.background = 'rgba(255, 255, 255, 0.98)';
                navbar.style.boxShadow = '0 4px 30px rgba(0, 0, 0, 0.15)';
            } else {
                navbar.style.background = 'rgba(255, 255, 255, 0.95)';
                navbar.style.boxShadow = '0 4px 30px rgba(0, 0, 0, 0.1)';
            }
        });

        // FAQ toggle function
        function toggleFAQ(num) {
            const faqAnswer = document.getElementById('faq' + num);
            const button = faqAnswer.previousElementSibling;
            const icon = button.querySelector('i');
            
            if (faqAnswer.style.display === 'none' || faqAnswer.style.display === '') {
                faqAnswer.style.display = 'block';
                icon.classList.remove('fa-chevron-down');
                icon.classList.add('fa-chevron-up');
                button.style.background = 'var(--gradient-1)';
                button.style.color = 'white';
            } else {
                faqAnswer.style.display = 'none';
                icon.classList.remove('fa-chevron-up');
                icon.classList.add('fa-chevron-down');
                button.style.background = 'var(--gradient-2)';
                button.style.color = 'var(--dark-purple)';
            }
        }

        // Intersection Observer for animations
        const observerOptions = {
            threshold: 0.1,
            rootMargin: '0px 0px -50px 0px'
        };

        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.style.animation = 'fadeInUp 0.6s ease forwards';
                }
            });
        }, observerOptions);

        // Observe all cards and timeline items
        document.querySelectorAll('.card-custom, .timeline-item, .faq-item').forEach(el => {
            observer.observe(el);
        });

        // Add parallax effect to floating shapes
        window.addEventListener('scroll', () => {
            const scrolled = window.pageYOffset;
            const shapes = document.querySelectorAll('.shape');
            shapes.forEach((shape, index) => {
                const speed = 0.5 + (index * 0.1);
                shape.style.transform = `translateY(${scrolled * speed}px) rotate(${scrolled * 0.1}deg)`;
            });
        });

        // Add hover effects to cards
        document.querySelectorAll('.card-custom').forEach(card => {
            card.addEventListener('mouseenter', function() {
                this.style.transform = 'translateY(-10px) scale(1.02)';
            });
            
            card.addEventListener('mouseleave', function() {
                this.style.transform = 'translateY(0) scale(1)';
            });
        });

        // Add typing effect to hero title
        function typeWriter(element, text, speed = 100) {
            let i = 0;
            element.innerHTML = '';
            function type() {
                if (i < text.length) {
                    element.innerHTML += text.charAt(i);
                    i++;
                    setTimeout(type, speed);
                }
            }
            type();
        }

        // Initialize typing effect after loading
        setTimeout(() => {
            const heroTitle = document.querySelector('.hero-title');
            if (heroTitle) {
                const originalText = heroTitle.textContent;
                typeWriter(heroTitle, originalText, 150);
            }
        }, 1500);
    </script>
</body>
</html>
