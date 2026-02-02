<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=5.0, user-scalable=yes">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="mobile-web-app-capable" content="yes">
    <title>HNU - GPA Calculator Pro</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Cairo:wght@400;600;700&display=swap" rel="stylesheet">
    
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
    
    <style>
        /* ========== CSS VARIABLES ========== */
        :root {
            --bg-primary: #0a0e27;
            --bg-secondary: #151b3d;
            --bg-card: #1a2142;
            --accent: #3b82f6;
            --accent-hover: #2563eb;
            --accent-light: #60a5fa;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #ef4444;
            --text-primary: #e2e8f0;
            --text-secondary: #94a3b8;
            --border: #1e293b;
            --shadow: rgba(0, 0, 0, 0.3);
            
            /* Responsive sizing variables */
            --nav-height: 4rem;
            --base-padding: 2.5%;
            --card-padding: 4%;
            --border-radius: 0.75rem;
            --gap-small: 1%;
            --gap-medium: 2.5%;
            --gap-large: 4%;
        }

        [data-theme="light"] {
            --bg-primary: #ffffff;
            --bg-secondary: #f8fafc;
            --bg-card: #f1f5f9;
            --accent: #2563eb;
            --accent-hover: #1d4ed8;
            --accent-light: #3b82f6;
            --success: #059669;
            --warning: #d97706;
            --danger: #dc2626;
            --text-primary: #0f172a;
            --text-secondary: #64748b;
            --border: #e2e8f0;
            --shadow: rgba(0, 0, 0, 0.05);
        }

        /* ========== RESPONSIVE FONT SIZING ========== */
        @media screen and (max-width: 480px) {
            html { font-size: 14px; }
            :root { 
                --nav-height: 3.5rem;
                --base-padding: 3%;
                --card-padding: 5%;
            }
        }
        
        @media screen and (min-width: 481px) and (max-width: 768px) {
            html { font-size: 15px; }
            :root { 
                --nav-height: 4rem;
                --base-padding: 3%;
            }
        }
        
        @media screen and (min-width: 769px) and (max-width: 1024px) {
            html { font-size: 16px; }
            :root { 
                --nav-height: 4.5rem;
                --base-padding: 2.5%;
            }
        }
        
        @media screen and (min-width: 1025px) and (max-width: 1440px) {
            html { font-size: 17px; }
            :root { 
                --nav-height: 5rem;
                --base-padding: 2%;
            }
        }
        
        @media screen and (min-width: 1441px) {
            html { font-size: 18px; }
            :root { 
                --nav-height: 5.5rem;
                --base-padding: 1.5%;
            }
        }

        /* ========== RESET & BASE ========== */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        html {
            width: 100%;
            overflow-x: hidden;
            scroll-behavior: smooth;
        }

        body {
            font-family: 'Inter', sans-serif;
            background: var(--bg-primary);
            color: var(--text-primary);
            min-height: 100vh;
            transition: background 0.3s, color 0.3s;
            width: 100%;
            overflow-x: hidden;
            padding-top: var(--nav-height);
        }

        body[dir="rtl"] {
            font-family: 'Cairo', sans-serif;
        }

        /* ========== TOP NAVIGATION ========== */
        .top-nav {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            height: var(--nav-height);
            background: var(--bg-card);
            border-bottom: 0.125rem solid var(--border);
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 0 var(--base-padding);
            z-index: 1000;
            box-shadow: 0 0.25rem 1rem var(--shadow);
        }

        .app-title {
            font-size: clamp(0.9rem, 2.5vw, 1.3rem);
            font-weight: 700;
            color: var(--accent);
            display: flex;
            align-items: center;
            gap: 0.5em;
            flex: 1;
            min-width: 0;
        }

        .app-title-text {
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .nav-controls {
            display: flex;
            align-items: center;
            gap: clamp(0.4rem, 1.5vw, 0.8rem);
            flex-shrink: 0;
        }

        .icon-btn {
            background: var(--bg-secondary);
            border: 0.0625rem solid var(--border);
            border-radius: 0.5rem;
            width: clamp(2.2rem, 6vw, 3rem);
            height: clamp(2.2rem, 6vw, 3rem);
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: clamp(1rem, 2.5vw, 1.4rem);
            transition: all 0.2s;
            color: var(--text-primary);
            flex-shrink: 0;
        }

        .icon-btn:active {
            transform: scale(0.95);
            background: var(--accent);
            color: white;
        }

        .menu-toggle {
            background: var(--accent);
            color: white;
        }

        /* ========== CONTAINER ========== */
        .container {
            max-width: 90rem;
            width: 100%;
            margin: 0 auto;
            padding: var(--base-padding);
            padding-bottom: 5%;
        }

        /* ========== CARDS ========== */
        .card {
            background: var(--bg-card);
            border: 0.0625rem solid var(--border);
            border-radius: var(--border-radius);
            padding: var(--card-padding);
            margin-bottom: var(--gap-medium);
            box-shadow: 0 0.25rem 1rem var(--shadow);
        }

        .card-header {
            font-size: clamp(1rem, 2.5vw, 1.5rem);
            font-weight: 700;
            margin-bottom: clamp(0.8rem, 2vw, 1.2rem);
            color: var(--accent);
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        /* ========== GPA DISPLAY ========== */
        .gpa-display {
            text-align: center;
            padding: clamp(1.2rem, 4vw, 2.5rem);
            background: linear-gradient(135deg, var(--accent), var(--accent-light));
            border-radius: var(--border-radius);
            margin-bottom: var(--gap-medium);
        }

        .gpa-value {
            font-size: clamp(2.5rem, 8vw, 5rem);
            font-weight: 800;
            color: white;
            margin: 0.2em 0;
            line-height: 1;
        }

        .gpa-label {
            font-size: clamp(0.75rem, 2vw, 1.1rem);
            color: rgba(255, 255, 255, 0.95);
            text-transform: uppercase;
            letter-spacing: 0.1em;
            font-weight: 600;
        }

        .gpa-grade {
            font-size: clamp(1.2rem, 3.5vw, 2rem);
            font-weight: 700;
            color: white;
            margin-top: 0.3em;
        }

        /* ========== STATS GRID ========== */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(clamp(8rem, 22vw, 12rem), 1fr));
            gap: var(--gap-medium);
            margin-bottom: var(--gap-medium);
        }

        .stat-card {
            background: var(--bg-secondary);
            border: 0.0625rem solid var(--border);
            border-radius: calc(var(--border-radius) * 0.8);
            padding: clamp(0.8rem, 3vw, 1.5rem);
            text-align: center;
        }

        .stat-value {
            font-size: clamp(1.3rem, 3.5vw, 2.2rem);
            font-weight: 700;
            color: var(--accent);
            margin: 0.2em 0;
            line-height: 1.2;
        }

        .stat-label {
            font-size: clamp(0.7rem, 1.8vw, 1rem);
            color: var(--text-secondary);
            line-height: 1.3;
        }

        /* ========== SEMESTER SECTION ========== */
        .semester {
            margin-bottom: clamp(0.8rem, 2vw, 1.2rem);
        }

        .semester-header {
            background: var(--bg-secondary);
            padding: clamp(0.8rem, 2.5vw, 1.2rem);
            border-radius: calc(var(--border-radius) * 0.8);
            cursor: pointer;
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 0.5em;
            border: 0.0625rem solid var(--border);
            transition: all 0.2s;
        }

        .semester-header:hover {
            background: var(--bg-card);
            transform: translateY(-0.125rem);
        }

        .semester-header:active {
            transform: translateY(0);
        }

        .semester-title {
            font-size: clamp(0.9rem, 2.2vw, 1.3rem);
            font-weight: 600;
        }

        .semester-gpa {
            font-size: clamp(1rem, 2.5vw, 1.5rem);
            font-weight: 700;
            color: var(--accent);
        }

        .semester-content {
            display: none;
            padding: clamp(0.5rem, 1.5vw, 1rem) 0;
        }

        .semester-content.active {
            display: block;
        }

        /* ========== COURSE ROW ========== */
        .course-row {
            background: var(--bg-secondary);
            border: 0.0625rem solid var(--border);
            border-radius: calc(var(--border-radius) * 0.7);
            padding: clamp(0.8rem, 2.5vw, 1.2rem);
            margin-bottom: clamp(0.5rem, 1.5vw, 0.8rem);
        }

        .course-info {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: clamp(0.5rem, 1.5vw, 0.8rem);
            gap: 0.5rem;
        }

        .course-name {
            font-size: clamp(0.8rem, 2vw, 1.1rem);
            font-weight: 600;
            color: var(--text-primary);
            flex: 1;
            line-height: 1.3;
        }

        .course-credits {
            font-size: clamp(0.7rem, 1.8vw, 0.95rem);
            color: var(--text-secondary);
            white-space: nowrap;
            flex-shrink: 0;
        }

        .marks-input-group {
            display: flex;
            align-items: center;
            gap: clamp(0.5rem, 1.5vw, 0.8rem);
        }

        .marks-input {
            flex: 1;
            background: var(--bg-primary);
            border: 0.0625rem solid var(--border);
            border-radius: calc(var(--border-radius) * 0.6);
            padding: clamp(0.6rem, 2vw, 0.9rem) clamp(0.8rem, 2.5vw, 1.2rem);
            color: var(--text-primary);
            font-size: clamp(0.9rem, 2.2vw, 1.2rem);
            text-align: center;
            font-weight: 600;
        }

        .marks-input:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 0 0.125rem rgba(59, 130, 246, 0.2);
        }

        .grade-badge {
            background: var(--accent);
            color: white;
            padding: clamp(0.4rem, 1.5vw, 0.6rem) clamp(0.8rem, 2.5vw, 1.2rem);
            border-radius: calc(var(--border-radius) * 0.5);
            font-size: clamp(0.8rem, 2vw, 1.1rem);
            font-weight: 700;
            min-width: clamp(3rem, 8vw, 4rem);
            text-align: center;
            flex-shrink: 0;
        }

        .grade-badge.success {
            background: var(--success);
        }

        .grade-badge.warning {
            background: var(--warning);
        }

        .grade-badge.danger {
            background: var(--danger);
        }

        /* ========== CHARTS ========== */
        .chart-container {
            position: relative;
            height: clamp(15rem, 40vw, 25rem);
            margin: clamp(1rem, 2.5vw, 1.5rem) 0;
        }

        /* ========== MENU OVERLAY ========== */
        .menu-overlay {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.7);
            z-index: 998;
            display: none;
        }

        .menu-overlay.active {
            display: block;
        }

        .side-menu {
            position: fixed;
            top: 0;
            right: -100%;
            width: clamp(18rem, 80vw, 25rem);
            height: 100%;
            background: var(--bg-card);
            z-index: 999;
            transition: right 0.3s;
            overflow-y: auto;
            box-shadow: -0.25rem 0 1rem var(--shadow);
        }

        body[dir="rtl"] .side-menu {
            right: auto;
            left: -100%;
        }

        .side-menu.active {
            right: 0;
        }

        body[dir="rtl"] .side-menu.active {
            left: 0;
            right: auto;
        }

        .menu-header {
            background: var(--accent);
            color: white;
            padding: clamp(1.2rem, 3.5vw, 2rem);
            font-size: clamp(1.2rem, 3vw, 1.8rem);
            font-weight: 700;
        }

        .menu-item {
            padding: clamp(1rem, 3vw, 1.5rem) clamp(1.2rem, 3.5vw, 2rem);
            border-bottom: 0.0625rem solid var(--border);
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: clamp(0.8rem, 2.5vw, 1.2rem);
            transition: background 0.2s;
        }

        .menu-item:hover {
            background: var(--bg-secondary);
        }

        .menu-item:active {
            background: var(--accent);
            color: white;
        }

        .menu-icon {
            font-size: clamp(1.2rem, 3vw, 1.8rem);
            flex-shrink: 0;
        }

        .menu-text {
            font-size: clamp(0.9rem, 2.2vw, 1.2rem);
            font-weight: 500;
        }

        /* ========== MODAL ========== */
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.8);
            z-index: 1001;
            display: none;
            align-items: center;
            justify-content: center;
            padding: var(--base-padding);
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: var(--bg-card);
            border-radius: var(--border-radius);
            width: 100%;
            max-width: clamp(20rem, 90vw, 35rem);
            max-height: 90vh;
            overflow-y: auto;
        }

        .modal-header {
            background: var(--accent);
            color: white;
            padding: clamp(1rem, 3vw, 1.5rem) clamp(1.2rem, 3.5vw, 2rem);
            border-radius: var(--border-radius) var(--border-radius) 0 0;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .modal-title {
            font-size: clamp(1.1rem, 2.8vw, 1.6rem);
            font-weight: 700;
        }

        .close-modal {
            background: transparent;
            border: none;
            color: white;
            font-size: clamp(1.5rem, 4vw, 2.2rem);
            cursor: pointer;
            width: clamp(2rem, 5vw, 2.5rem);
            height: clamp(2rem, 5vw, 2.5rem);
            display: flex;
            align-items: center;
            justify-content: center;
            flex-shrink: 0;
        }

        .modal-body {
            padding: clamp(1.2rem, 3.5vw, 2rem);
        }

        .form-group {
            margin-bottom: clamp(1rem, 2.5vw, 1.5rem);
        }

        .form-label {
            display: block;
            font-size: clamp(0.85rem, 2vw, 1.1rem);
            font-weight: 600;
            color: var(--text-secondary);
            margin-bottom: 0.5em;
        }

        .form-input, .form-select {
            width: 100%;
            background: var(--bg-primary);
            border: 0.0625rem solid var(--border);
            border-radius: calc(var(--border-radius) * 0.7);
            padding: clamp(0.8rem, 2.5vw, 1.2rem);
            color: var(--text-primary);
            font-size: clamp(0.9rem, 2.2vw, 1.1rem);
        }

        .form-input:focus, .form-select:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 0 0.125rem rgba(59, 130, 246, 0.2);
        }

        .btn-primary {
            width: 100%;
            background: var(--accent);
            color: white;
            border: none;
            border-radius: calc(var(--border-radius) * 0.7);
            padding: clamp(0.9rem, 2.8vw, 1.4rem);
            font-size: clamp(0.95rem, 2.3vw, 1.2rem);
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
        }

        .btn-primary:hover {
            background: var(--accent-hover);
            transform: translateY(-0.125rem);
            box-shadow: 0 0.5rem 1rem var(--shadow);
        }

        .btn-primary:active {
            background: var(--accent-hover);
            transform: translateY(0);
        }

        /* ========== LANGUAGE SWITCHER ========== */
        .language-switcher {
            display: flex;
            gap: clamp(0.5rem, 1.5vw, 0.8rem);
            padding: clamp(0.8rem, 2.5vw, 1.2rem) clamp(1.2rem, 3.5vw, 2rem);
            border-bottom: 0.0625rem solid var(--border);
        }

        .lang-btn {
            flex: 1;
            background: var(--bg-secondary);
            border: 0.0625rem solid var(--border);
            border-radius: calc(var(--border-radius) * 0.6);
            padding: clamp(0.6rem, 2vw, 0.9rem);
            cursor: pointer;
            font-size: clamp(0.8rem, 2vw, 1.1rem);
            font-weight: 600;
            color: var(--text-secondary);
            transition: all 0.2s;
        }

        .lang-btn.active {
            background: var(--accent);
            color: white;
            border-color: var(--accent);
        }

        /* ========== NOTIFICATION ========== */
        .notification {
            position: fixed;
            top: calc(var(--nav-height) + 1rem);
            left: 50%;
            transform: translateX(-50%) translateY(-6rem);
            background: var(--bg-card);
            color: var(--text-primary);
            padding: clamp(0.8rem, 2.5vw, 1.2rem) clamp(1.2rem, 3.5vw, 2rem);
            border-radius: calc(var(--border-radius) * 0.7);
            box-shadow: 0 0.5rem 1.5rem var(--shadow);
            z-index: 1002;
            opacity: 0;
            transition: all 0.3s;
            border: 0.0625rem solid var(--border);
            max-width: 90%;
            font-size: clamp(0.85rem, 2vw, 1.1rem);
            text-align: center;
        }

        .notification.show {
            transform: translateX(-50%) translateY(0);
            opacity: 1;
        }

        /* ========== PRINT STYLES ========== */
        @media print {
            .top-nav,
            .menu-toggle,
            .theme-toggle,
            .menu-overlay,
            .side-menu,
            .notification {
                display: none !important;
            }
            
            body {
                padding-top: 0;
            }
            
            .container {
                max-width: 100%;
            }
        }
    </style>
</head>
<body>
    <!-- Top Navigation -->
    <div class="top-nav">
        <div class="app-title">
            <span>🎓</span>
            <span class="app-title-text" data-translate="appTitle">GPA Calculator</span>
        </div>
        <div class="nav-controls">
            <button class="icon-btn theme-toggle" onclick="toggleTheme()" title="Toggle Theme">🌙</button>
            <button class="icon-btn menu-toggle" onclick="toggleMenu()" title="Menu">☰</button>
        </div>
    </div>

    <!-- Main Container -->
    <div class="container">
        <!-- GPA Display Card -->
        <div class="gpa-display">
            <div class="gpa-label" data-translate="cumulativeGPA">CUMULATIVE GPA</div>
            <div class="gpa-value" id="cumulativeGPA">0.00</div>
            <div class="gpa-grade" id="overallGrade">-</div>
        </div>

        <!-- Quick Stats -->
        <div class="stats-grid">
            <div class="stat-card">
                <div class="stat-value" id="totalCredits">0</div>
                <div class="stat-label" data-translate="totalCredits">Total Credits</div>
            </div>
            <div class="stat-card">
                <div class="stat-value" id="completedCourses">0</div>
                <div class="stat-label" data-translate="completed">Completed</div>
            </div>
            <div class="stat-card">
                <div class="stat-value" id="averagePercentage">0%</div>
                <div class="stat-label" data-translate="avgPercentage">Avg %</div>
            </div>
            <div class="stat-card">
                <div class="stat-value" id="totalCourses">0</div>
                <div class="stat-label" data-translate="totalCourses">Total Courses</div>
            </div>
        </div>

        <!-- Charts -->
        <div class="card">
            <div class="card-header" data-translate="gpaProgress">GPA Progress</div>
            <div class="chart-container">
                <canvas id="progressChart"></canvas>
            </div>
        </div>

        <div class="card">
            <div class="card-header" data-translate="gradeDistribution">Grade Distribution</div>
            <div class="chart-container">
                <canvas id="gradeChart"></canvas>
            </div>
        </div>

        <!-- Semesters -->
        <div class="card">
            <div class="card-header" data-translate="semesters">Semesters</div>
            <div id="semestersContainer"></div>
        </div>
    </div>

    <!-- Menu Overlay -->
    <div class="menu-overlay" onclick="toggleMenu()"></div>
    
    <!-- Side Menu -->
    <div class="side-menu">
        <div class="menu-header" data-translate="menu">Menu</div>
        
        <div class="language-switcher">
            <button class="lang-btn active" data-lang="en" onclick="switchLanguage('en')">🇬🇧 English</button>
            <button class="lang-btn" data-lang="ar" onclick="switchLanguage('ar')">🇸🇦 العربية</button>
        </div>

        <div class="menu-item" onclick="openModal('profileModal')">
            <span class="menu-icon">👤</span>
            <span class="menu-text" data-translate="profile">Profile</span>
        </div>
        <div class="menu-item" onclick="openModal('settingsModal')">
            <span class="menu-icon">⚙️</span>
            <span class="menu-text" data-translate="settings">Settings</span>
        </div>
        <div class="menu-item" onclick="shareGPA()">
            <span class="menu-icon">📤</span>
            <span class="menu-text" data-translate="shareGPA">Share GPA</span>
        </div>
        <div class="menu-item" onclick="printTranscript()">
            <span class="menu-icon">🖨️</span>
            <span class="menu-text" data-translate="print">Print Transcript</span>
        </div>
        <div class="menu-item" onclick="clearAllData()">
            <span class="menu-icon">🗑️</span>
            <span class="menu-text" data-translate="clearData">Clear All Data</span>
        </div>
    </div>

    <!-- Profile Modal -->
    <div class="modal" id="profileModal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title" data-translate="profile">Profile</div>
                <button class="close-modal" onclick="closeModal('profileModal')">×</button>
            </div>
            <div class="modal-body">
                <div class="form-group">
                    <label class="form-label" data-translate="name">Name</label>
                    <input type="text" class="form-input" id="userName" placeholder="Enter your name">
                </div>
                <div class="form-group">
                    <label class="form-label" data-translate="studentID">Student ID</label>
                    <input type="text" class="form-input" id="studentID" placeholder="Enter your student ID">
                </div>
                <div class="form-group">
                    <label class="form-label" data-translate="email">Email</label>
                    <input type="email" class="form-input" id="userEmail" placeholder="Enter your email">
                </div>
                <button class="btn-primary" onclick="saveProfile()" data-translate="saveProfile">Save Profile</button>
            </div>
        </div>
    </div>

    <!-- Settings Modal -->
    <div class="modal" id="settingsModal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title" data-translate="settings">Settings</div>
                <button class="close-modal" onclick="closeModal('settingsModal')">×</button>
            </div>
            <div class="modal-body">
                <div class="form-group">
                    <label class="form-label" data-translate="theme">Theme</label>
                    <select class="form-select" id="themeSelect">
                        <option value="dark">Dark</option>
                        <option value="light">Light</option>
                    </select>
                </div>
                <div class="form-group">
                    <label class="form-label" data-translate="decimalPrecision">Decimal Precision</label>
                    <select class="form-select" id="decimalPrecision">
                        <option value="2">2 decimals</option>
                        <option value="3">3 decimals</option>
                        <option value="4">4 decimals</option>
                    </select>
                </div>
                <button class="btn-primary" onclick="saveSettings()" data-translate="saveSettings">Save Settings</button>
            </div>
        </div>
    </div>

    <!-- Notification -->
    <div class="notification" id="notification"></div>

    <script>
        // ========== GLOBAL VARIABLES ==========
        let currentTheme = 'dark';
        let currentLang = 'en';
        let decimalPrecision = 2;
        let userGrades = {};
        let progressChart = null;
        let gradeChart = null;

        // ========== COURSE DATABASE ==========
        const courseDatabase = {
            // Level 1 - Semester 1
            '101BIO': { name: { en: 'General Biology 1', ar: 'أحياء عامة 1' }, credits: 3, total: 100, semester: 1 },
            '101CHEM': { name: { en: 'General Chemistry 1', ar: 'كيمياء عامة 1' }, credits: 3, total: 100, semester: 1 },
            '101PHYS': { name: { en: 'General Physics 1', ar: 'فيزياء عامة 1' }, credits: 3, total: 100, semester: 1 },
            '101MATH': { name: { en: 'Calculus 1', ar: 'حساب تفاضل وتكامل 1' }, credits: 3, total: 100, semester: 1 },
            '101ENG': { name: { en: 'English Language 1', ar: 'لغة إنجليزية 1' }, credits: 3, total: 100, semester: 1 },
            '101COMP': { name: { en: 'Computer Skills', ar: 'مهارات الحاسب الآلي' }, credits: 2, total: 100, semester: 1 },
            '101ISL': { name: { en: 'Islamic Culture 1', ar: 'ثقافة إسلامية 1' }, credits: 2, total: 100, semester: 1 },
            
            // Level 1 - Semester 2
            '102BIO': { name: { en: 'General Biology 2', ar: 'أحياء عامة 2' }, credits: 3, total: 100, semester: 2 },
            '102CHEM': { name: { en: 'General Chemistry 2', ar: 'كيمياء عامة 2' }, credits: 3, total: 100, semester: 2 },
            '102PHYS': { name: { en: 'General Physics 2', ar: 'فيزياء عامة 2' }, credits: 3, total: 100, semester: 2 },
            '102STAT': { name: { en: 'Biostatistics', ar: 'إحصاء حيوي' }, credits: 3, total: 100, semester: 2 },
            '102ENG': { name: { en: 'English Language 2', ar: 'لغة إنجليزية 2' }, credits: 3, total: 100, semester: 2 },
            '102ISL': { name: { en: 'Islamic Culture 2', ar: 'ثقافة إسلامية 2' }, credits: 2, total: 100, semester: 2 },
            
            // Level 2 - Semester 3
            '201ANAT': { name: { en: 'Human Anatomy', ar: 'تشريح الإنسان' }, credits: 3, total: 100, semester: 3 },
            '201PHYS': { name: { en: 'Human Physiology', ar: 'فسيولوجيا الإنسان' }, credits: 3, total: 100, semester: 3 },
            '201BIOCHEM': { name: { en: 'Biochemistry', ar: 'كيمياء حيوية' }, credits: 3, total: 100, semester: 3 },
            '201MICRO': { name: { en: 'General Microbiology', ar: 'أحياء دقيقة عامة' }, credits: 3, total: 100, semester: 3 },
            '201HEMA': { name: { en: 'Hematology 1', ar: 'علم الدم 1' }, credits: 3, total: 100, semester: 3 },
            '201MED': { name: { en: 'Medical Terminology', ar: 'مصطلحات طبية' }, credits: 2, total: 100, semester: 3 },
            
            // Level 2 - Semester 4
            '202PATH': { name: { en: 'General Pathology', ar: 'علم الأمراض العام' }, credits: 3, total: 100, semester: 4 },
            '202HEMA': { name: { en: 'Hematology 2', ar: 'علم الدم 2' }, credits: 3, total: 100, semester: 4 },
            '202IMMUN': { name: { en: 'Immunology', ar: 'علم المناعة' }, credits: 3, total: 100, semester: 4 },
            '202PARA': { name: { en: 'Parasitology', ar: 'علم الطفيليات' }, credits: 3, total: 100, semester: 4 },
            '202CHEM': { name: { en: 'Clinical Chemistry 1', ar: 'كيمياء سريرية 1' }, credits: 3, total: 100, semester: 4 },
            '202BAC': { name: { en: 'Bacteriology', ar: 'علم البكتيريا' }, credits: 3, total: 100, semester: 4 },
            
            // Level 3 - Semester 5
            '301HISTO': { name: { en: 'Histology', ar: 'علم الأنسجة' }, credits: 3, total: 100, semester: 5 },
            '301CYTO': { name: { en: 'Cytology', ar: 'علم الخلايا' }, credits: 3, total: 100, semester: 5 },
            '301CHEM': { name: { en: 'Clinical Chemistry 2', ar: 'كيمياء سريرية 2' }, credits: 3, total: 100, semester: 5 },
            '301VIRO': { name: { en: 'Virology', ar: 'علم الفيروسات' }, credits: 3, total: 100, semester: 5 },
            '301MYCO': { name: { en: 'Mycology', ar: 'علم الفطريات' }, credits: 2, total: 100, semester: 5 },
            '301BANK': { name: { en: 'Blood Banking', ar: 'بنوك الدم' }, credits: 3, total: 100, semester: 5 },
            
            // Level 3 - Semester 6
            '302MOL': { name: { en: 'Molecular Biology', ar: 'بيولوجيا جزيئية' }, credits: 3, total: 100, semester: 6 },
            '302CLIN': { name: { en: 'Clinical Biochemistry', ar: 'كيمياء حيوية سريرية' }, credits: 3, total: 100, semester: 6 },
            '302SERO': { name: { en: 'Serology', ar: 'علم الأمصال' }, credits: 3, total: 100, semester: 6 },
            '302QC': { name: { en: 'Quality Control', ar: 'ضبط الجودة' }, credits: 2, total: 100, semester: 6 },
            '302RES': { name: { en: 'Research Methods', ar: 'طرق البحث' }, credits: 2, total: 100, semester: 6 },
            '302TRAIN': { name: { en: 'Clinical Training 1', ar: 'تدريب سريري 1' }, credits: 4, total: 100, semester: 6 },
            
            // Level 4 - Semester 7
            '401ADV': { name: { en: 'Advanced Hematology', ar: 'علم الدم المتقدم' }, credits: 3, total: 100, semester: 7 },
            '401GEN': { name: { en: 'Clinical Genetics', ar: 'علم الوراثة السريري' }, credits: 3, total: 100, semester: 7 },
            '401ENDO': { name: { en: 'Clinical Endocrinology', ar: 'علم الغدد الصماء' }, credits: 3, total: 100, semester: 7 },
            '401MANAGE': { name: { en: 'Lab Management', ar: 'إدارة المختبرات' }, credits: 2, total: 100, semester: 7 },
            '401TRAIN': { name: { en: 'Clinical Training 2', ar: 'تدريب سريري 2' }, credits: 6, total: 100, semester: 7 },
            
            // Level 4 - Semester 8
            '402PROJECT': { name: { en: 'Graduation Project', ar: 'مشروع التخرج' }, credits: 4, total: 100, semester: 8 },
            '402SEMINAR': { name: { en: 'Seminar', ar: 'ندوة' }, credits: 2, total: 100, semester: 8 },
            '402INTERN': { name: { en: 'Internship', ar: 'امتياز' }, credits: 12, total: 100, semester: 8 }
        };

        // ========== GRADING SYSTEM ==========
        function getGradeFromPercentage(percentage) {
            if (percentage >= 95) return { grade: 'A+', gpa: 4.0, class: 'success' };
            if (percentage >= 90) return { grade: 'A', gpa: 4.0, class: 'success' };
            if (percentage >= 85) return { grade: 'A-', gpa: 3.7, class: 'success' };
            if (percentage >= 80) return { grade: 'B+', gpa: 3.3, class: 'success' };
            if (percentage >= 75) return { grade: 'B', gpa: 3.0, class: 'warning' };
            if (percentage >= 70) return { grade: 'B-', gpa: 2.7, class: 'warning' };
            if (percentage >= 65) return { grade: 'C+', gpa: 2.3, class: 'warning' };
            if (percentage >= 60) return { grade: 'C', gpa: 2.0, class: 'danger' };
            if (percentage >= 55) return { grade: 'C-', gpa: 1.7, class: 'danger' };
            if (percentage >= 50) return { grade: 'D+', gpa: 1.3, class: 'danger' };
            if (percentage >= 45) return { grade: 'D', gpa: 1.0, class: 'danger' };
            return { grade: 'F', gpa: 0.0, class: 'danger' };
        }

        // ========== RENDER SEMESTERS ==========
        function renderSemesters() {
            const container = document.getElementById('semestersContainer');
            const semesters = {};
            
            Object.entries(courseDatabase).forEach(([code, course]) => {
                if (!semesters[course.semester]) {
                    semesters[course.semester] = [];
                }
                semesters[course.semester].push({ code, ...course });
            });
            
            container.innerHTML = Object.keys(semesters).sort((a, b) => a - b).map(sem => {
                const courses = semesters[sem];
                const semesterGPA = calculateSemesterGPA(sem);
                
                return `
                    <div class="semester">
                        <div class="semester-header" onclick="toggleSemester(${sem})">
                            <span class="semester-title">
                                ${currentLang === 'ar' ? `المستوى ${Math.ceil(sem / 2)} - الفصل ${sem % 2 === 0 ? 2 : 1}` : `Level ${Math.ceil(sem / 2)} - Semester ${sem % 2 === 0 ? 2 : 1}`}
                            </span>
                            <span class="semester-gpa">${semesterGPA}</span>
                        </div>
                        <div class="semester-content" id="semester-${sem}">
                            ${courses.map(course => `
                                <div class="course-row">
                                    <div class="course-info">
                                        <span class="course-name">${course.name[currentLang]}</span>
                                        <span class="course-credits">${course.credits} ${currentLang === 'ar' ? 'ساعة' : 'cr'}</span>
                                    </div>
                                    <div class="marks-input-group">
                                        <input type="number" 
                                               class="marks-input" 
                                               id="marks-${course.code}"
                                               placeholder="0-${course.total}"
                                               min="0" 
                                               max="${course.total}"
                                               value="${userGrades[course.code] || ''}"
                                               onchange="updateGrade('${course.code}', this.value, ${course.total})">
                                        <span class="grade-badge" id="grade-${course.code}">-</span>
                                    </div>
                                </div>
                            `).join('')}
                        </div>
                    </div>
                `;
            }).join('');
            
            updateAllGrades();
        }

        function toggleSemester(sem) {
            const content = document.getElementById(`semester-${sem}`);
            content.classList.toggle('active');
        }

        function updateGrade(code, marks, total) {
            const marksNum = parseFloat(marks);
            if (isNaN(marksNum) || marksNum < 0 || marksNum > total) {
                delete userGrades[code];
                document.getElementById(`grade-${code}`).textContent = '-';
                document.getElementById(`grade-${code}`).className = 'grade-badge';
            } else {
                userGrades[code] = marksNum;
                const percentage = (marksNum / total) * 100;
                const gradeInfo = getGradeFromPercentage(percentage);
                const badge = document.getElementById(`grade-${code}`);
                badge.textContent = gradeInfo.grade;
                badge.className = `grade-badge ${gradeInfo.class}`;
            }
            
            saveGrades();
            calculateOverallGPA();
            updateCharts();
        }

        function updateAllGrades() {
            Object.entries(courseDatabase).forEach(([code, course]) => {
                const marks = userGrades[code];
                if (marks != null && marks !== '') {
                    const percentage = (marks / course.total) * 100;
                    const gradeInfo = getGradeFromPercentage(percentage);
                    const badge = document.getElementById(`grade-${code}`);
                    if (badge) {
                        badge.textContent = gradeInfo.grade;
                        badge.className = `grade-badge ${gradeInfo.class}`;
                    }
                }
            });
        }

        function calculateSemesterGPA(semester) {
            let totalPoints = 0;
            let totalCredits = 0;
            
            Object.entries(courseDatabase).forEach(([code, course]) => {
                if (course.semester === parseInt(semester)) {
                    const marks = userGrades[code];
                    if (marks != null && marks !== '') {
                        const percentage = (marks / course.total) * 100;
                        const gradeInfo = getGradeFromPercentage(percentage);
                        totalPoints += gradeInfo.gpa * course.credits;
                        totalCredits += course.credits;
                    }
                }
            });
            
            return totalCredits > 0 ? (totalPoints / totalCredits).toFixed(decimalPrecision) : '0.00';
        }

        function calculateOverallGPA() {
            let totalPoints = 0;
            let totalCredits = 0;
            let completedCourses = 0;
            let totalPercentage = 0;
            let coursesWithGrades = 0;
            
            Object.entries(courseDatabase).forEach(([code, course]) => {
                const marks = userGrades[code];
                if (marks != null && marks !== '') {
                    const percentage = (marks / course.total) * 100;
                    const gradeInfo = getGradeFromPercentage(percentage);
                    totalPoints += gradeInfo.gpa * course.credits;
                    totalCredits += course.credits;
                    completedCourses++;
                    totalPercentage += percentage;
                    coursesWithGrades++;
                }
            });
            
            const cgpa = totalCredits > 0 ? (totalPoints / totalCredits).toFixed(decimalPrecision) : '0.00';
            const avgPercentage = coursesWithGrades > 0 ? (totalPercentage / coursesWithGrades).toFixed(1) : '0.0';
            
            document.getElementById('cumulativeGPA').textContent = cgpa;
            document.getElementById('totalCredits').textContent = totalCredits;
            document.getElementById('completedCourses').textContent = completedCourses;
            document.getElementById('totalCourses').textContent = Object.keys(courseDatabase).length;
            document.getElementById('averagePercentage').textContent = avgPercentage + '%';
            
            const overallGradeInfo = getGradeFromPercentage(parseFloat(avgPercentage));
            document.getElementById('overallGrade').textContent = overallGradeInfo.grade;
        }

        // ========== CHARTS ==========
        function updateCharts() {
            updateProgressChart();
            updateGradeChart();
        }

        function updateProgressChart() {
            const ctx = document.getElementById('progressChart');
            const semesterGPAs = [];
            const labels = [];
            
            for (let i = 1; i <= 8; i++) {
                const gpa = calculateSemesterGPA(i);
                if (parseFloat(gpa) > 0) {
                    semesterGPAs.push(parseFloat(gpa));
                    labels.push(currentLang === 'ar' ? `فصل ${i}` : `Sem ${i}`);
                }
            }
            
            if (progressChart) { progressChart.destroy(); }
            
            const isDark = currentTheme === 'dark';
            const textColor = isDark ? '#94a3b8' : '#64748b';
            const gridColor = isDark ? '#1e293b' : '#e2e8f0';
            
            progressChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: labels,
                    datasets: [{
                        label: currentLang === 'ar' ? 'المعدل الفصلي' : 'Semester GPA',
                        data: semesterGPAs,
                        borderColor: '#3b82f6',
                        backgroundColor: 'rgba(59, 130, 246, 0.1)',
                        borderWidth: 3,
                        tension: 0.4,
                        fill: true,
                        pointRadius: 5,
                        pointBackgroundColor: '#3b82f6'
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: { legend: { display: false } },
                    scales: {
                        y: {
                            beginAtZero: true,
                            max: 4.0,
                            ticks: { color: textColor },
                            grid: { color: gridColor }
                        },
                        x: {
                            ticks: { color: textColor },
                            grid: { color: gridColor }
                        }
                    }
                }
            });
        }

        function updateGradeChart() {
            const ctx = document.getElementById('gradeChart');
            const gradeCounts = {
                'A+': 0, 'A': 0, 'A-': 0, 'B+': 0, 'B': 0, 'B-': 0,
                'C+': 0, 'C': 0, 'C-': 0, 'D+': 0, 'D': 0, 'F': 0
            };
            
            Object.entries(courseDatabase).forEach(([code, course]) => {
                const marks = userGrades[code];
                if (marks != null && marks !== '') {
                    const percentage = (marks / course.total) * 100;
                    const gradeInfo = getGradeFromPercentage(percentage);
                    gradeCounts[gradeInfo.grade]++;
                }
            });
            
            if (gradeChart) { gradeChart.destroy(); }
            
            const isDark = currentTheme === 'dark';
            const textColor = isDark ? '#94a3b8' : '#64748b';
            const gridColor = isDark ? '#1e293b' : '#e2e8f0';
            
            gradeChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: Object.keys(gradeCounts),
                    datasets: [{
                        data: Object.values(gradeCounts),
                        backgroundColor: '#3b82f6',
                        borderRadius: 6
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: { legend: { display: false } },
                    scales: {
                        y: {
                            beginAtZero: true,
                            ticks: { stepSize: 1, color: textColor },
                            grid: { color: gridColor }
                        },
                        x: {
                            ticks: { color: textColor },
                            grid: { color: gridColor }
                        }
                    }
                }
            });
        }

        // ========== UI FUNCTIONS ==========
        function toggleMenu() {
            document.querySelector('.menu-overlay').classList.toggle('active');
            document.querySelector('.side-menu').classList.toggle('active');
        }

        function toggleTheme() {
            currentTheme = currentTheme === 'dark' ? 'light' : 'dark';
            document.body.setAttribute('data-theme', currentTheme);
            document.querySelector('.theme-toggle').textContent = currentTheme === 'dark' ? '🌙' : '☀️';
            localStorage.setItem('theme', currentTheme);
            updateCharts();
        }

        function switchLanguage(lang) {
            currentLang = lang;
            document.body.setAttribute('dir', lang === 'ar' ? 'rtl' : 'ltr');
            localStorage.setItem('language', lang);
            
            document.querySelectorAll('.lang-btn').forEach(btn => {
                btn.classList.toggle('active', btn.dataset.lang === lang);
            });
            
            updateLanguage();
            renderSemesters();
            updateCharts();
        }

        function updateLanguage() {
            const translations = {
                en: {
                    appTitle: 'GPA Calculator',
                    cumulativeGPA: 'CUMULATIVE GPA',
                    totalCredits: 'Total Credits',
                    completed: 'Completed',
                    avgPercentage: 'Avg %',
                    totalCourses: 'Total Courses',
                    gpaProgress: 'GPA Progress',
                    gradeDistribution: 'Grade Distribution',
                    semesters: 'Semesters',
                    menu: 'Menu',
                    profile: 'Profile',
                    settings: 'Settings',
                    shareGPA: 'Share GPA',
                    print: 'Print Transcript',
                    clearData: 'Clear All Data',
                    name: 'Name',
                    studentID: 'Student ID',
                    email: 'Email',
                    saveProfile: 'Save Profile',
                    theme: 'Theme',
                    decimalPrecision: 'Decimal Precision',
                    saveSettings: 'Save Settings'
                },
                ar: {
                    appTitle: 'حاسبة المعدل',
                    cumulativeGPA: 'المعدل التراكمي',
                    totalCredits: 'إجمالي الساعات',
                    completed: 'المكتملة',
                    avgPercentage: 'متوسط %',
                    totalCourses: 'إجمالي المقررات',
                    gpaProgress: 'تقدم المعدل',
                    gradeDistribution: 'توزيع الدرجات',
                    semesters: 'الفصول الدراسية',
                    menu: 'القائمة',
                    profile: 'الملف الشخصي',
                    settings: 'الإعدادات',
                    shareGPA: 'مشاركة المعدل',
                    print: 'طباعة الكشف',
                    clearData: 'مسح جميع البيانات',
                    name: 'الاسم',
                    studentID: 'الرقم الجامعي',
                    email: 'البريد الإلكتروني',
                    saveProfile: 'حفظ الملف',
                    theme: 'السمة',
                    decimalPrecision: 'دقة الأرقام',
                    saveSettings: 'حفظ الإعدادات'
                }
            };
            
            document.querySelectorAll('[data-translate]').forEach(elem => {
                const key = elem.dataset.translate;
                if (translations[currentLang][key]) {
                    elem.textContent = translations[currentLang][key];
                }
            });
        }

        function openModal(id) {
            document.getElementById(id).classList.add('active');
            toggleMenu();
        }

        function closeModal(id) {
            document.getElementById(id).classList.remove('active');
        }

        function showNotification(message) {
            const notification = document.getElementById('notification');
            notification.textContent = message;
            notification.classList.add('show');
            setTimeout(() => notification.classList.remove('show'), 3000);
        }

        // ========== PROFILE & SETTINGS ==========
        function saveProfile() {
            localStorage.setItem('userName', document.getElementById('userName').value);
            localStorage.setItem('studentID', document.getElementById('studentID').value);
            localStorage.setItem('userEmail', document.getElementById('userEmail').value);
            showNotification('✅ Profile saved!');
            closeModal('profileModal');
            if (typeof confetti !== 'undefined') {
                confetti({ particleCount: 100, spread: 70, origin: { y: 0.6 } });
            }
        }

        function loadProfile() {
            document.getElementById('userName').value = localStorage.getItem('userName') || '';
            document.getElementById('studentID').value = localStorage.getItem('studentID') || '';
            document.getElementById('userEmail').value = localStorage.getItem('userEmail') || '';
        }

        function saveSettings() {
            const theme = document.getElementById('themeSelect').value;
            const precision = document.getElementById('decimalPrecision').value;
            
            decimalPrecision = parseInt(precision);
            localStorage.setItem('decimalPrecision', precision);
            
            if (theme !== currentTheme) { toggleTheme(); }
            
            showNotification('✅ Settings saved!');
            closeModal('settingsModal');
            calculateOverallGPA();
        }

        function loadSettings() {
            const savedTheme = localStorage.getItem('theme') || 'dark';
            const savedPrecision = localStorage.getItem('decimalPrecision') || '2';
            
            currentTheme = savedTheme;
            decimalPrecision = parseInt(savedPrecision);
            
            document.getElementById('themeSelect').value = savedTheme;
            document.getElementById('decimalPrecision').value = savedPrecision;
            
            if (savedTheme === 'light') {
                document.body.setAttribute('data-theme', 'light');
                document.querySelector('.theme-toggle').textContent = '☀️';
            }
        }

        // ========== DATA MANAGEMENT ==========
        function saveGrades() {
            localStorage.setItem('userGrades', JSON.stringify(userGrades));
        }

        function loadGrades() {
            const saved = localStorage.getItem('userGrades');
            if (saved) { userGrades = JSON.parse(saved); }
        }

        function clearAllData() {
            if (confirm(currentLang === 'ar' ? 
                '⚠️ هل أنت متأكد من حذف جميع البيانات؟' : 
                '⚠️ Are you sure you want to clear all data?')) {
                userGrades = {};
                saveGrades();
                renderSemesters();
                calculateOverallGPA();
                updateCharts();
                showNotification(currentLang === 'ar' ? '🗑️ تم مسح جميع البيانات!' : '🗑️ All data cleared!');
            }
        }

        function shareGPA() {
            const cgpa = document.getElementById('cumulativeGPA').textContent;
            const grade = document.getElementById('overallGrade').textContent;
            const shareText = `🎓 My CGPA: ${cgpa} (${grade})\n📚 HNU Medical Laboratory Program`;
            
            if (navigator.share) {
                navigator.share({ title: 'My GPA', text: shareText })
                    .catch(() => copyToClipboard(shareText));
            } else {
                copyToClipboard(shareText);
            }
        }

        function copyToClipboard(text) {
            navigator.clipboard.writeText(text)
                .then(() => showNotification('✅ Copied to clipboard!'))
                .catch(() => showNotification('❌ Could not copy'));
        }

        function printTranscript() {
            window.print();
        }

        // ========== INITIALIZATION ==========
        document.addEventListener('DOMContentLoaded', function() {
            loadProfile();
            loadSettings();
            loadGrades();
            
            const savedLang = localStorage.getItem('language') || 'en';
            if (savedLang === 'ar') {
                switchLanguage('ar');
            }
            
            updateLanguage();
            renderSemesters();
            calculateOverallGPA();
            updateCharts();
        });
    </script>
</body>
</html>
        
