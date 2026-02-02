  <html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Applied Health Sciences Technology - GPA Calculator</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&family=Orbitron:wght@400;700;900&family=Cairo:wght@400;600;700;900&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-primary: #0a0e27;
            --bg-secondary: #151b3d;
            --bg-card: #1a2142;
            --accent: #3b82f6;
            --accent-hover: #2563eb;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #ef4444;
            --text-primary: #e2e8f0;
            --text-secondary: #94a3b8;
            --border: #1e293b;
            --shadow: rgba(0, 0, 0, 0.3);
        }

        [data-theme="light"] {
            --bg-primary: #ffffff;
            --bg-secondary: #f8fafc;
            --bg-card: #f1f5f9;
            --accent: #2563eb;
            --accent-hover: #1d4ed8;
            --success: #059669;
            --warning: #d97706;
            --danger: #dc2626;
            --text-primary: #0f172a;
            --text-secondary: #64748b;
            --border: #e2e8f0;
            --shadow: rgba(0, 0, 0, 0.05);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent; /* Remove tap highlight on mobile */
        }

        /* Prevent text size adjustment on orientation change */
        html {
            -webkit-text-size-adjust: 100%;
            -moz-text-size-adjust: 100%;
            -ms-text-size-adjust: 100%;
            text-size-adjust: 100%;
        }

        body {
            font-family: 'Inter', sans-serif;
            background: var(--bg-primary);
            color: var(--text-primary);
            min-height: 100vh;
            transition: background 0.3s, color 0.3s;
            padding-bottom: 3rem;
        }

        body[dir="rtl"] {
            font-family: 'Cairo', sans-serif;
        }

        .theme-toggle {
            position: fixed;
            top: 1.5rem;
            right: 1.5rem;
            z-index: 1000;
            background: var(--accent);
            border: none;
            border-radius: 50%;
            width: 50px;
            height: 50px;
            cursor: pointer;
            font-size: 1.5rem;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 4px 12px var(--shadow);
            transition: transform 0.2s;
        }

        body[dir="rtl"] .theme-toggle {
            right: auto;
            left: 1.5rem;
        }

        .theme-toggle:hover {
            transform: scale(1.1);
        }

        /* Language Switcher */
        .language-switcher {
            position: fixed;
            top: 1.5rem;
            left: 1.5rem;
            z-index: 1000;
            display: flex;
            gap: 0.5rem;
            background: var(--bg-card);
            border: 2px solid var(--border);
            border-radius: 12px;
            padding: 0.5rem;
            box-shadow: 0 4px 12px var(--shadow);
        }

        body[dir="rtl"] .language-switcher {
            left: auto;
            right: 1.5rem;
        }

        .lang-btn {
            background: transparent;
            border: 2px solid transparent;
            border-radius: 8px;
            padding: 0.5rem 1rem;
            cursor: pointer;
            font-size: 0.9rem;
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            color: var(--text-secondary);
            transition: all 0.3s;
        }

        .lang-btn:hover {
            background: var(--bg-secondary);
            color: var(--text-primary);
        }

        .lang-btn.active {
            background: var(--accent);
            color: white;
            border-color: var(--accent);
        }

        .flag {
            width: 20px;
            height: 15px;
            display: inline-block;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 2rem;
        }

        header {
            text-align: center;
            padding: 2rem 1rem;
            margin-bottom: 2rem;
        }

        h1 {
            font-size: 2.5rem;
            font-weight: 900;
            font-family: 'Orbitron', sans-serif;
            background: linear-gradient(135deg, var(--accent), #60a5fa);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 0.5rem;
            letter-spacing: 2px;
            text-transform: uppercase;
        }

        body[dir="rtl"] h1 {
            font-family: 'Cairo', sans-serif;
            letter-spacing: 0;
        }

        .subtitle {
            color: var(--text-secondary);
            font-size: 1.1rem;
            margin-bottom: 0.5rem;
        }

        .credits {
            color: #ff0000;
            font-size: 1.15rem;
            margin-top: 0.5rem;
            font-weight: 700;
            font-family: 'Orbitron', sans-serif;
            position: relative;
            display: inline-block;
            animation: sparkle 2s ease-in-out infinite;
            text-shadow: 
                0 0 10px #ff0000,
                0 0 20px #ff0000,
                0 0 30px #ff0000,
                0 0 40px #ff3333;
        }

        body[dir="rtl"] .credits {
            font-family: 'Cairo', sans-serif;
        }

        @keyframes sparkle {
            0%, 100% {
                filter: brightness(1);
                transform: translateY(0px);
            }
            50% {
                filter: brightness(1.5);
                transform: translateY(-3px);
            }
        }

        .credits::before {
            content: '✨';
            position: absolute;
            left: -30px;
            animation: sparkleMove 2s ease-in-out infinite;
        }

        body[dir="rtl"] .credits::before {
            left: auto;
            right: -30px;
        }

        .credits::after {
            content: '✨';
            position: absolute;
            right: -30px;
            animation: sparkleMove 2s ease-in-out infinite 1s;
        }

        body[dir="rtl"] .credits::after {
            right: auto;
            left: -30px;
        }

        @keyframes sparkleMove {
            0%, 100% {
                opacity: 0.5;
                transform: scale(0.8);
            }
            50% {
                opacity: 1;
                transform: scale(1.2);
            }
        }

        .button-group {
            display: flex;
            gap: 1rem;
            justify-content: center;
            margin-top: 1rem;
            flex-wrap: wrap;
        }

        .smart-import-btn {
            background: linear-gradient(135deg, #8b5cf6, #6366f1);
            color: white;
            border: none;
            padding: 1.2rem 2.5rem;
            border-radius: 12px;
            font-size: 1.2rem;
            font-weight: 900;
            font-family: 'Orbitron', sans-serif;
            cursor: pointer;
            box-shadow: 0 4px 16px rgba(139, 92, 246, 0.4);
            transition: all 0.3s;
            letter-spacing: 1.5px;
            text-transform: uppercase;
        }

        body[dir="rtl"] .smart-import-btn {
            font-family: 'Cairo', sans-serif;
            letter-spacing: 0;
        }

        .smart-import-btn:hover {
            transform: translateY(-3px) scale(1.05);
            box-shadow: 0 8px 24px rgba(139, 92, 246, 0.5);
        }

        .reset-btn {
            background: linear-gradient(135deg, #ef4444, #dc2626);
            color: white;
            border: none;
            padding: 1.2rem 2.5rem;
            border-radius: 12px;
            font-size: 1.2rem;
            font-weight: 900;
            font-family: 'Orbitron', sans-serif;
            cursor: pointer;
            box-shadow: 0 4px 16px rgba(239, 68, 68, 0.4);
            transition: all 0.3s;
            letter-spacing: 1.5px;
            text-transform: uppercase;
        }

        body[dir="rtl"] .reset-btn {
            font-family: 'Cairo', sans-serif;
            letter-spacing: 0;
        }

        .reset-btn:hover {
            transform: translateY(-3px) scale(1.05);
            box-shadow: 0 8px 24px rgba(239, 68, 68, 0.5);
        }

        .stats-panel {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1.5rem;
            margin-bottom: 2rem;
        }

        .stat-card {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 12px;
            padding: 1.5rem;
            text-align: center;
            box-shadow: 0 2px 8px var(--shadow);
            position: relative;
            overflow: hidden;
            transition: transform 0.3s, box-shadow 0.3s;
        }

        .stat-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 6px 20px var(--shadow);
        }

        .stat-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 4px;
            height: 100%;
            background: var(--accent);
        }

        body[dir="rtl"] .stat-card::before {
            left: auto;
            right: 0;
        }

        .stat-label {
            font-size: 0.8rem;
            color: var(--text-secondary);
            text-transform: uppercase;
            letter-spacing: 0.5px;
            margin-bottom: 0.5rem;
            font-weight: 600;
        }

        .stat-value {
            font-size: 2rem;
            font-weight: 800;
            color: var(--accent);
        }

        /* Accordion Semester Sections */
        .semester-accordion {
            margin-bottom: 1rem;
            animation: fadeInUp 0.5s ease-out;
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .semester-header {
            background: var(--bg-card);
            border: 2px solid var(--border);
            border-radius: 12px;
            padding: 1.5rem;
            cursor: pointer;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            margin-bottom: 0.5rem;
            position: relative;
            overflow: hidden;
        }

        /* Animated gradient bar on semester headers */
        .semester-header::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, 
                transparent, 
                rgba(59, 130, 246, 0.3), 
                transparent);
            animation: slideBar 3s ease-in-out infinite;
        }

        @keyframes slideBar {
            0% {
                left: -100%;
            }
            50% {
                left: 100%;
            }
            100% {
                left: 100%;
            }
        }

        .semester-header:hover {
            border-color: var(--accent);
            background: var(--bg-secondary);
            transform: translateX(5px) scale(1.02);
            box-shadow: 0 5px 15px var(--shadow);
        }

        body[dir="rtl"] .semester-header:hover {
            transform: translateX(-5px) scale(1.02);
        }

        .semester-header:hover::before {
            animation: slideBar 1.5s ease-in-out infinite;
        }

        .semester-header.active {
            background: linear-gradient(135deg, var(--accent), #2563eb);
            color: white;
            border-color: var(--accent);
            box-shadow: 0 4px 16px rgba(59, 130, 246, 0.4);
        }

        .semester-header.active::before {
            background: linear-gradient(90deg, 
                transparent, 
                rgba(255, 255, 255, 0.2), 
                transparent);
        }

        .semester-title {
            font-size: 1.3rem;
            font-weight: 700;
            font-family: 'Orbitron', sans-serif;
            display: flex;
            align-items: center;
            gap: 1rem;
            position: relative;
            z-index: 1;
        }

        body[dir="rtl"] .semester-title {
            font-family: 'Cairo', sans-serif;
        }

        .semester-icon {
            transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            font-size: 1.2rem;
        }

        .semester-header.active .semester-icon {
            transform: rotate(180deg);
        }

        .semester-gpa {
            font-size: 1.1rem;
            font-weight: 800;
            padding: 0.5rem 1rem;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 8px;
            position: relative;
            z-index: 1;
        }

        .semester-content {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .semester-content.active {
            max-height: 5000px;
        }

        .courses-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 1rem;
            padding: 1rem;
        }

        .course-card {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 10px;
            padding: 1.25rem;
            transition: all 0.3s;
            box-shadow: 0 2px 6px var(--shadow);
        }

        .course-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 16px var(--shadow);
            border-color: var(--accent);
        }

        .course-name {
            font-weight: 700;
            font-size: 1rem;
            margin-bottom: 0.5rem;
            color: var(--text-primary);
        }

        .course-code {
            font-size: 0.85rem;
            color: var(--text-secondary);
            margin-bottom: 1rem;
            font-family: 'Courier New', monospace;
        }

        .input-group {
            display: flex;
            gap: 0.75rem;
            margin-bottom: 1rem;
        }

        .input-wrapper {
            flex: 1;
            display: flex;
            flex-direction: column;
        }

        .input-label {
            font-size: 0.75rem;
            color: var(--text-secondary);
            margin-bottom: 0.25rem;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .marks-input {
            background: var(--bg-secondary);
            border: 2px solid var(--border);
            border-radius: 8px;
            padding: 0.75rem;
            color: var(--text-primary);
            font-size: 1rem;
            font-weight: 600;
            transition: all 0.3s;
            width: 100%;
        }

        .marks-input:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
        }

        .results-row {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 0.5rem;
            margin-top: 0.75rem;
        }

        .result-item {
            text-align: center;
            padding: 0.5rem;
            background: var(--bg-secondary);
            border-radius: 6px;
        }

        .result-label {
            font-size: 0.7rem;
            color: var(--text-secondary);
            text-transform: uppercase;
            letter-spacing: 0.5px;
            margin-bottom: 0.25rem;
        }

        .result-value {
            font-size: 0.95rem;
            font-weight: 700;
            color: var(--text-primary);
        }

        .grade-badge {
            padding: 0.5rem 1rem;
            border-radius: 6px;
            font-weight: 700;
            font-size: 1.1rem;
            display: inline-block;
        }

        .grade-A {
            background: linear-gradient(135deg, #10b981, #059669);
            color: white;
        }

        .grade-B {
            background: linear-gradient(135deg, #3b82f6, #2563eb);
            color: white;
        }

        .grade-C {
            background: linear-gradient(135deg, #f59e0b, #d97706);
            color: white;
        }

        .grade-D {
            background: linear-gradient(135deg, #ef4444, #dc2626);
            color: white;
        }

        .grade-F {
            background: linear-gradient(135deg, #64748b, #475569);
            color: white;
        }

        /* Smart Import Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.7);
            z-index: 2000;
            align-items: center;
            justify-content: center;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: var(--bg-card);
            border-radius: 16px;
            padding: 2rem;
            max-width: 600px;
            width: 90%;
            max-height: 80vh;
            overflow-y: auto;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.4);
            text-align: center;
        }

        body[dir="rtl"] .modal-content {
            text-align: center;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
        }

        body[dir="rtl"] .modal-header {
            flex-direction: row-reverse;
        }

        .modal-title {
            font-size: 1.5rem;
            font-weight: 700;
        }

        .close-btn {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: var(--text-secondary);
            transition: color 0.2s;
        }

        .close-btn:hover {
            color: var(--text-primary);
        }

        .import-textarea {
            width: 100%;
            min-height: 300px;
            background: var(--bg-secondary);
            border: 2px solid var(--border);
            border-radius: 8px;
            padding: 1rem;
            color: var(--text-primary);
            font-family: 'Courier New', monospace;
            font-size: 0.9rem;
            resize: vertical;
        }

        .import-textarea:focus {
            outline: none;
            border-color: var(--accent);
        }

        .modal-actions {
            display: flex;
            gap: 1rem;
            margin-top: 1.5rem;
        }

        .btn {
            flex: 1;
            padding: 1rem;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
        }

        .btn-primary {
            background: var(--accent);
            color: white;
        }

        .btn-primary:hover {
            background: var(--accent-hover);
            transform: translateY(-2px);
        }

        .btn-secondary {
            background: var(--bg-secondary);
            color: var(--text-primary);
            border: 1px solid var(--border);
        }

        .btn-secondary:hover {
            background: var(--border);
        }

        .notification {
            position: fixed;
            bottom: 2rem;
            right: 2rem;
            background: var(--success);
            color: white;
            padding: 1rem 1.5rem;
            border-radius: 8px;
            font-weight: 600;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
            animation: slideIn 0.3s ease-out;
            z-index: 3000;
            max-width: 400px;
            white-space: pre-line;
        }

        body[dir="rtl"] .notification {
            right: auto;
            left: 2rem;
        }

        @media (max-width: 768px) {
            .notification {
                bottom: 1rem;
                right: 1rem;
                left: 1rem;
                max-width: calc(100% - 2rem);
            }

            body[dir="rtl"] .notification {
                left: 1rem;
                right: 1rem;
            }
        }

        @keyframes slideIn {
            from {
                transform: translateX(400px);
                opacity: 0;
            }
            to {
                transform: translateX(0);
                opacity: 1;
            }
        }

        @media (max-width: 768px) {
            /* Prevent auto-zoom on input focus */
            body {
                font-size: 16px;
                -webkit-text-size-adjust: 100%;
                -moz-text-size-adjust: 100%;
                -ms-text-size-adjust: 100%;
                text-size-adjust: 100%;
            }

            .container {
                padding: 1rem;
            }

            h1 {
                font-size: 1.8rem;
                margin-top: 3.5rem; /* Space for fixed buttons */
            }

            .subtitle {
                font-size: 1rem;
            }

            .credits {
                font-size: 1.05rem;
            }

            .courses-grid {
                grid-template-columns: 1fr;
            }

            .stats-panel {
                grid-template-columns: 1fr 1fr;
                gap: 1rem;
            }

            .language-switcher {
                top: 1rem;
                left: 1rem;
                padding: 0.4rem;
                gap: 0.3rem;
            }

            body[dir="rtl"] .language-switcher {
                left: auto;
                right: 1rem;
            }
            
            .lang-btn {
                padding: 0.4rem 0.7rem;
                font-size: 0.85rem;
                gap: 0.3rem;
            }
            
            .flag {
                width: 18px;
                height: 13px;
            }

            .theme-toggle {
                top: 1rem;
                right: 1rem;
                width: 45px;
                height: 45px;
                font-size: 1.3rem;
            }

            body[dir="rtl"] .theme-toggle {
                left: 1rem;
                right: auto;
            }

            .smart-import-btn, .reset-btn {
                width: 100%;
                padding: 1rem 1.5rem;
                font-size: 1rem;
                min-height: 48px; /* Touch-friendly minimum */
            }

            .button-group {
                flex-direction: column;
                width: 100%;
                gap: 0.75rem;
            }

            .semester-header {
                padding: 1rem;
                flex-direction: column;
                gap: 0.5rem;
                align-items: flex-start;
            }

            body[dir="rtl"] .semester-header {
                align-items: flex-start;
            }

            .semester-title {
                font-size: 1.1rem;
            }

            .input-group {
                flex-direction: column;
            }

            .marks-input {
                font-size: 16px; /* Prevent zoom on iOS */
                padding: 0.9rem;
            }

            .modal-content {
                width: 95%;
                padding: 1.5rem;
            }

            .import-textarea {
                font-size: 16px; /* Prevent zoom on iOS */
                min-height: 250px;
            }

            .results-row {
                grid-template-columns: 1fr;
                gap: 0.75rem;
            }

            .stat-card {
                padding: 1rem;
            }

            .stat-value {
                font-size: 1.8rem;
            }

            .course-card {
                padding: 1.25rem;
            }
            
            .course-name {
                font-size: 1rem;
            }
            
            .course-code {
                font-size: 0.85rem;
            }
            
            .course-credits {
                font-size: 0.9rem;
            }
        }
    </style>
</head>
<body>
    <button class="theme-toggle" onclick="toggleTheme()">🌙</button>

    <!-- Language Switcher -->
    <div class="language-switcher">
        <button class="lang-btn active" onclick="switchLanguage('en')" id="lang-en">
            <span class="flag">🇺🇸</span>
            <span>EN</span>
        </button>
        <button class="lang-btn" onclick="switchLanguage('ar')" id="lang-ar">
            <span class="flag">🇸🇦</span>
            <span>AR</span>
        </button>
    </div>

    <div class="container">
        <header>
            <h1 data-en="🧬 Applied Health Sciences Technology" data-ar="🧬 تكنولوجيا العلوم الصحية التطبيقية">🧬 Applied Health Sciences Technology</h1>
            <div class="subtitle" data-en="GPA Calculator" data-ar="حاسبة المعدل التراكمي">GPA Calculator</div>
            <div class="credits" data-en="Made by Mohand" data-ar="صنع بواسطة مهند">Made by Mohand</div>
            <div class="button-group">
                <button class="smart-import-btn" onclick="openSmartImport()" data-en="⚡ Calculate Your GPA with 1 Click" data-ar="⚡ احسب معدلك بضغطة واحدة">⚡ Calculate Your GPA with 1 Click</button>
                <button class="reset-btn" onclick="resetAll()" data-en="🔄 Reset All" data-ar="🔄 إعادة تعيين الكل">🔄 Reset All</button>
            </div>
        </header>

        <!-- Stats Panel -->
        <div class="stats-panel">
            <div class="stat-card">
                <div class="stat-label" data-en="Cumulative GPA" data-ar="المعدل التراكمي">Cumulative GPA</div>
                <div class="stat-value" id="cumulativeGPA">0.00</div>
            </div>
            <div class="stat-card">
                <div class="stat-label" data-en="Total Hours" data-ar="مجموع الساعات">Total Hours</div>
                <div class="stat-value" id="totalCredits">0</div>
            </div>
            <div class="stat-card">
                <div class="stat-label" data-en="Overall Grade" data-ar="التقدير العام">Overall Grade</div>
                <div class="stat-value" id="overallGrade">-</div>
            </div>
            <div class="stat-card">
                <div class="stat-label" data-en="Percentage" data-ar="النسبة المئوية">Percentage</div>
                <div class="stat-value" id="overallPercentage">0.0%</div>
            </div>
        </div>

        <!-- Semesters Container -->
        <div id="semestersContainer"></div>
    </div>

    <!-- Smart Import Modal -->
    <div id="smartImportModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title" data-en="📋 Smart Import" data-ar="📋 استيراد ذكي">📋 Smart Import</h2>
                <button class="close-btn" onclick="closeModal()">×</button>
            </div>
            <p style="color: var(--text-secondary); margin-bottom: 1rem;" data-en="Paste your transcript text below. The system will automatically extract course codes and grades!" data-ar="الصق نص كشف الدرجات أدناه. سيقوم النظام تلقائياً باستخراج رموز المقررات والدرجات!">
                Paste your transcript text below. The system will automatically extract course codes and grades!
            </p>
            <textarea 
                id="importText" 
                class="import-textarea" 
                data-placeholder-en="Paste your transcript here...

Example formats:
UN101: Written: 75
THS101 Total: 85
TL201 - 90"
                data-placeholder-ar="الصق كشف الدرجات هنا...

أمثلة على التنسيقات:
UN101: Written: 75
THS101 Total: 85
TL201 - 90"
                placeholder="Paste your transcript here...

Example formats:
UN101: Written: 75
THS101 Total: 85
TL201 - 90"></textarea>
            <div class="modal-actions">
                <button class="btn btn-secondary" onclick="closeModal()" data-en="Cancel" data-ar="إلغاء">Cancel</button>
                <button class="btn btn-primary" onclick="processSmartImport()" data-en="Import Grades" data-ar="استيراد الدرجات">Import Grades</button>
            </div>
        </div>
    </div>

    <script>
        let grades = {};
        let currentTheme = 'dark';
        let currentLang = 'en';
        
        const translations = {
            en: {
                'Your Marks': 'Your Marks',
                'Total Marks': 'Total Marks',
                'Grade': 'Grade',
                'Percentage': 'Percentage',
                'Points': 'Points',
                'GPA': 'GPA'
            },
            ar: {
                'Your Marks': 'درجاتك',
                'Total Marks': 'مجموع الدرجات',
                'Grade': 'التقدير',
                'Percentage': 'النسبة',
                'Points': 'النقاط',
                'GPA': 'المعدل'
            }
        };

        const courseDatabase = {
            // First Level - 1st Semester
            'UN101': { name: { en: 'Academic Reading and Writing (1)', ar: 'القراءة والكتابة الأكاديمية (1)' }, credits: 2, maxMarks: 100, semester: { en: 'First Level – 1st Semester', ar: 'المستوى الأول - الفصل الأول' } },
            'THS101': { name: { en: 'Basic Physics', ar: 'الفيزياء الأساسية' }, credits: 2, maxMarks: 100, semester: { en: 'First Level – 1st Semester', ar: 'المستوى الأول - الفصل الأول' } },
            'THS102': { name: { en: 'Mathematics', ar: 'الرياضيات' }, credits: 2, maxMarks: 100, semester: { en: 'First Level – 1st Semester', ar: 'المستوى الأول - الفصل الأول' } },
            'THS103': { name: { en: 'Introduction to Electrical Engineering', ar: 'مقدمة في الهندسة الكهربائية' }, credits: 3, maxMarks: 150, semester: { en: 'First Level – 1st Semester', ar: 'المستوى الأول - الفصل الأول' } },
            'UN102': { name: { en: 'Computer Skills', ar: 'مهارات الحاسوب' }, credits: 2, maxMarks: 100, semester: { en: 'First Level – 1st Semester', ar: 'المستوى الأول - الفصل الأول' } },
            'THS104': { name: { en: 'Mechanics', ar: 'الميكانيكا' }, credits: 2, maxMarks: 100, semester: { en: 'First Level – 1st Semester', ar: 'المستوى الأول - الفصل الأول' } },
            'UN103': { name: { en: 'Critical Thinking', ar: 'التفكير النقدي' }, credits: 2, maxMarks: 100, semester: { en: 'First Level – 1st Semester', ar: 'المستوى الأول - الفصل الأول' } },

            // First Level - 2nd Semester
            'THS115': { name: { en: 'Electronic Circuits & Devices', ar: 'الدوائر والأجهزة الإلكترونية' }, credits: 3, maxMarks: 150, semester: { en: 'First Level – 2nd Semester', ar: 'المستوى الأول - الفصل الثاني' } },
            'THS116': { name: { en: 'General Anatomy & Histology', ar: 'التشريح العام والأنسجة' }, credits: 3, maxMarks: 150, semester: { en: 'First Level – 2nd Semester', ar: 'المستوى الأول - الفصل الثاني' } },
            'THS117': { name: { en: 'General Physiology', ar: 'علم وظائف الأعضاء العام' }, credits: 2, maxMarks: 100, semester: { en: 'First Level – 2nd Semester', ar: 'المستوى الأول - الفصل الثاني' } },
            'THS118': { name: { en: 'General Microbiology', ar: 'علم الأحياء الدقيقة العام' }, credits: 2, maxMarks: 100, semester: { en: 'First Level – 2nd Semester', ar: 'المستوى الأول - الفصل الثاني' } },
            'THS119': { name: { en: 'General Chemistry', ar: 'الكيمياء العامة' }, credits: 2, maxMarks: 100, semester: { en: 'First Level – 2nd Semester', ar: 'المستوى الأول - الفصل الثاني' } },
            'UN114': { name: { en: 'Academic Reading and Writing (2)', ar: 'القراءة والكتابة الأكاديمية (2)' }, credits: 2, maxMarks: 100, semester: { en: 'First Level – 2nd Semester', ar: 'المستوى الأول - الفصل الثاني' } },
            'THS1110': { name: { en: 'Professional Ethics', ar: 'الأخلاقيات المهنية' }, credits: 1, maxMarks: 50, semester: { en: 'First Level – 2nd Semester', ar: 'المستوى الأول - الفصل الثاني' } },

            // Second Level - 1st Semester
            'THS2010': { name: { en: 'Mechatronics Engineering', ar: 'هندسة الميكاترونيكس' }, credits: 2, maxMarks: 100, semester: { en: 'Second Level – 1st Semester', ar: 'المستوى الثاني - الفصل الأول' } },
            'TL201': { name: { en: 'Biochemistry (1)', ar: 'الكيمياء الحيوية (1)' }, credits: 4, maxMarks: 200, semester: { en: 'Second Level – 1st Semester', ar: 'المستوى الثاني - الفصل الأول' } },
            'TL202': { name: { en: 'Parasitology (1)', ar: 'علم الطفيليات (1)' }, credits: 2, maxMarks: 100, semester: { en: 'Second Level – 1st Semester', ar: 'المستوى الثاني - الفصل الأول' } },
            'TL203': { name: { en: 'Bacteriology', ar: 'علم البكتيريا' }, credits: 4, maxMarks: 200, semester: { en: 'Second Level – 1st Semester', ar: 'المستوى الثاني - الفصل الأول' } },
            'TL204': { name: { en: 'Histology for Lab Technologists', ar: 'علم الأنسجة لفنيي المختبرات' }, credits: 2, maxMarks: 100, semester: { en: 'Second Level – 1st Semester', ar: 'المستوى الثاني - الفصل الأول' } },
            'UN5': { name: { en: 'Foundation of Digital Technology', ar: 'أساسيات التقنية الرقمية' }, credits: 2, maxMarks: 100, semester: { en: 'Second Level – 1st Semester', ar: 'المستوى الثاني - الفصل الأول' } },
            'UN6': { name: { en: 'English Language', ar: 'اللغة الإنجليزية' }, credits: 2, maxMarks: 100, semester: { en: 'Second Level – 1st Semester', ar: 'المستوى الثاني - الفصل الأول' } },

            // Second Level - 2nd Semester
            'TL215': { name: { en: 'Molecular Biology', ar: 'البيولوجيا الجزيئية' }, credits: 4, maxMarks: 200, semester: { en: 'Second Level – 2nd Semester', ar: 'المستوى الثاني - الفصل الثاني' } },
            'TL216': { name: { en: 'Hematology (1)', ar: 'علم الدم (1)' }, credits: 4, maxMarks: 200, semester: { en: 'Second Level – 2nd Semester', ar: 'المستوى الثاني - الفصل الثاني' } },
            'TL217': { name: { en: 'Systematic Physiology', ar: 'علم وظائف الأعضاء المنهجي' }, credits: 4, maxMarks: 200, semester: { en: 'Second Level – 2nd Semester', ar: 'المستوى الثاني - الفصل الثاني' } },
            'TL218': { name: { en: 'General Biology', ar: 'الأحياء العامة' }, credits: 3, maxMarks: 150, semester: { en: 'Second Level – 2nd Semester', ar: 'المستوى الثاني - الفصل الثاني' } },
            'ETHS1': { name: { en: 'Elective (1)', ar: 'اختياري (1)' }, credits: 1, maxMarks: 50, semester: { en: 'Second Level – 2nd Semester', ar: 'المستوى الثاني - الفصل الثاني' } },

            // Third Level - 1st Semester
            'TL309': { name: { en: 'Lab Instrumentation (1)', ar: 'أجهزة المختبرات (1)' }, credits: 4, maxMarks: 200, semester: { en: 'Third Level – 1st Semester', ar: 'المستوى الثالث - الفصل الأول' } },
            'TL3010': { name: { en: 'Enzymology & Hormones', ar: 'علم الإنزيمات والهرمونات' }, credits: 4, maxMarks: 200, semester: { en: 'Third Level – 1st Semester', ar: 'المستوى الثالث - الفصل الأول' } },
            'TL3011': { name: { en: 'Parasitology (2)', ar: 'علم الطفيليات (2)' }, credits: 3, maxMarks: 150, semester: { en: 'Third Level – 1st Semester', ar: 'المستوى الثالث - الفصل الأول' } },
            'TL3012': { name: { en: 'Systematic Pathology', ar: 'علم الأمراض المنهجي' }, credits: 3, maxMarks: 150, semester: { en: 'Third Level – 1st Semester', ar: 'المستوى الثالث - الفصل الأول' } },
            'THS3011': { name: { en: 'Infection Control', ar: 'مكافحة العدوى' }, credits: 2, maxMarks: 100, semester: { en: 'Third Level – 1st Semester', ar: 'المستوى الثالث - الفصل الأول' } },
            'UN7': { name: { en: 'Innovation & Entrepreneurship', ar: 'الابتكار وريادة الأعمال' }, credits: 2, maxMarks: 100, semester: { en: 'Third Level – 1st Semester', ar: 'المستوى الثالث - الفصل الأول' } },

            // Third Level - 2nd Semester
            'TL3113': { name: { en: 'Biochemistry (2)', ar: 'الكيمياء الحيوية (2)' }, credits: 4, maxMarks: 200, semester: { en: 'Third Level – 2nd Semester', ar: 'المستوى الثالث - الفصل الثاني' } },
            'TL3114': { name: { en: 'Basic Immunology', ar: 'علم المناعة الأساسي' }, credits: 3, maxMarks: 150, semester: { en: 'Third Level – 2nd Semester', ar: 'المستوى الثالث - الفصل الثاني' } },
            'TL3115': { name: { en: 'Quality Management (1)', ar: 'إدارة الجودة (1)' }, credits: 4, maxMarks: 200, semester: { en: 'Third Level – 2nd Semester', ar: 'المستوى الثالث - الفصل الثاني' } },
            'TL3116': { name: { en: 'Lab Instrumentation (2)', ar: 'أجهزة المختبرات (2)' }, credits: 4, maxMarks: 200, semester: { en: 'Third Level – 2nd Semester', ar: 'المستوى الثالث - الفصل الثاني' } },
            'ETHS2': { name: { en: 'Elective (2)', ar: 'اختياري (2)' }, credits: 1, maxMarks: 50, semester: { en: 'Third Level – 2nd Semester', ar: 'المستوى الثالث - الفصل الثاني' } },

            // Fourth Level - 1st Semester
            'TL4017': { name: { en: 'Biochemistry (3)', ar: 'الكيمياء الحيوية (3)' }, credits: 3, maxMarks: 150, semester: { en: 'Fourth Level – 1st Semester', ar: 'المستوى الرابع - الفصل الأول' } },
            'TL4018': { name: { en: 'Virology & Mycology', ar: 'علم الفيروسات والفطريات' }, credits: 3, maxMarks: 150, semester: { en: 'Fourth Level – 1st Semester', ar: 'المستوى الرابع - الفصل الأول' } },
            'TL4019': { name: { en: 'Hematology (2)', ar: 'علم الدم (2)' }, credits: 4, maxMarks: 200, semester: { en: 'Fourth Level – 1st Semester', ar: 'المستوى الرابع - الفصل الأول' } },
            'TL4020': { name: { en: 'Blood Banking', ar: 'بنك الدم' }, credits: 4, maxMarks: 200, semester: { en: 'Fourth Level – 1st Semester', ar: 'المستوى الرابع - الفصل الأول' } },
            'ETHS3': { name: { en: 'Elective (3)', ar: 'اختياري (3)' }, credits: 1, maxMarks: 50, semester: { en: 'Fourth Level – 1st Semester', ar: 'المستوى الرابع - الفصل الأول' } },

            // Fourth Level - 2nd Semester
            'TL4121': { name: { en: 'Immunology & Serology', ar: 'علم المناعة والمصول' }, credits: 4, maxMarks: 200, semester: { en: 'Fourth Level – 2nd Semester', ar: 'المستوى الرابع - الفصل الثاني' } },
            'TL4122': { name: { en: 'Age & Pregnancy Investigation', ar: 'فحوصات العمر والحمل' }, credits: 4, maxMarks: 200, semester: { en: 'Fourth Level – 2nd Semester', ar: 'المستوى الرابع - الفصل الثاني' } },
            'TL4123': { name: { en: 'Quality Management (2)', ar: 'إدارة الجودة (2)' }, credits: 4, maxMarks: 150, semester: { en: 'Fourth Level – 2nd Semester', ar: 'المستوى الرابع - الفصل الثاني' } },
            'TL4124': { name: { en: 'Forensic Chemistry & Toxicology', ar: 'الكيمياء الجنائية والسموم' }, credits: 4, maxMarks: 200, semester: { en: 'Fourth Level – 2nd Semester', ar: 'المستوى الرابع - الفصل الثاني' } },
            'ETHS4': { name: { en: 'Elective (4)', ar: 'اختياري (4)' }, credits: 1, maxMarks: 50, semester: { en: 'Fourth Level – 2nd Semester', ar: 'المستوى الرابع - الفصل الثاني' } }
        };

        // Initialize
        loadGrades();
        loadLanguage();
        renderSemesters();
        calculateCumulativeGPA();

        function switchLanguage(lang) {
            currentLang = lang;
            document.body.setAttribute('dir', lang === 'ar' ? 'rtl' : 'ltr');
            
            // Update button states
            document.getElementById('lang-en').classList.toggle('active', lang === 'en');
            document.getElementById('lang-ar').classList.toggle('active', lang === 'ar');
            
            // Update all text elements with data-en and data-ar attributes
            document.querySelectorAll('[data-en]').forEach(el => {
                const text = el.getAttribute('data-' + lang);
                if (text) {
                    if (el.tagName === 'TEXTAREA') {
                        el.placeholder = text;
                    } else {
                        el.textContent = text;
                    }
                }
            });
            
            // Save preference
            localStorage.setItem('medLabLang', lang);
            
            // Re-render semesters with new language
            renderSemesters();
            calculateCumulativeGPA();
        }

        function loadLanguage() {
            const saved = localStorage.getItem('medLabLang');
            if (saved && (saved === 'en' || saved === 'ar')) {
                switchLanguage(saved);
            }
        }

        function renderSemesters() {
            const semesters = {};
            
            Object.entries(courseDatabase).forEach(([code, course]) => {
                const semesterName = course.semester[currentLang];
                if (!semesters[semesterName]) {
                    semesters[semesterName] = [];
                }
                semesters[semesterName].push({ code, ...course });
            });

            const container = document.getElementById('semestersContainer');
            container.innerHTML = Object.entries(semesters).map(([semester, courses]) => `
                <div class="semester-accordion">
                    <div class="semester-header" onclick="toggleSemester('${semester}')">
                        <div class="semester-title">
                            <span class="semester-icon">📚</span>
                            ${semester}
                        </div>
                        <div class="semester-gpa" id="gpa-${semester.replace(/\s+/g, '-').replace(/–/g, '-')}">
                            ${translations[currentLang]['GPA']}: 0.00
                        </div>
                    </div>
                    <div class="semester-content" id="semester-${semester.replace(/\s+/g, '-').replace(/–/g, '-')}">
                        <div class="courses-grid">
                            ${courses.map(course => `
                                <div class="course-card">
                                    <div class="course-name">${course.name[currentLang]}</div>
                                    <div class="course-code">${course.code} • ${course.credits} ${currentLang === 'en' ? 'Hours' : 'ساعة'}</div>
                                    <div class="input-group">
                                        <div class="input-wrapper">
                                            <label class="input-label">${translations[currentLang]['Your Marks']}</label>
                                            <input 
                                                type="number" 
                                                class="marks-input" 
                                                placeholder="0"
                                                min="0"
                                                max="${course.maxMarks}"
                                                value="${grades[course.code] || ''}"
                                                oninput="updateGrade('${course.code}', this.value, ${course.maxMarks}, ${course.credits})"
                                            >
                                        </div>
                                        <div class="input-wrapper">
                                            <label class="input-label">${translations[currentLang]['Total Marks']}</label>
                                            <input 
                                                type="number" 
                                                class="marks-input" 
                                                value="${course.maxMarks}"
                                                disabled
                                                style="opacity: 0.6;"
                                            >
                                        </div>
                                    </div>
                                    <div class="results-row">
                                        <div class="result-item">
                                            <div class="result-label">${translations[currentLang]['Grade']}</div>
                                            <div class="result-value">
                                                <span id="grade-${course.code}" class="grade-badge grade-F">-</span>
                                            </div>
                                        </div>
                                        <div class="result-item">
                                            <div class="result-label">${translations[currentLang]['Percentage']}</div>
                                            <div class="result-value" id="percentage-${course.code}">-</div>
                                        </div>
                                        <div class="result-item">
                                            <div class="result-label">${translations[currentLang]['Points']}</div>
                                            <div class="result-value" id="points-${course.code}">-</div>
                                        </div>
                                    </div>
                                </div>
                            `).join('')}
                        </div>
                    </div>
                </div>
            `).join('');
            
            // Update existing grades display
            Object.keys(grades).forEach(code => {
                if (grades[code] && courseDatabase[code]) {
                    updateGradeDisplay(code, grades[code], courseDatabase[code].maxMarks, courseDatabase[code].credits);
                }
            });
        }

        function toggleSemester(semester) {
            const header = event.currentTarget;
            const content = document.getElementById(`semester-${semester.replace(/\s+/g, '-').replace(/–/g, '-')}`);
            
            header.classList.toggle('active');
            content.classList.toggle('active');
        }

        function updateGrade(code, marks, maxMarks, credits) {
            marks = parseFloat(marks) || 0;
            if (marks === 0) {
                delete grades[code];
            } else {
                grades[code] = marks;
            }
            
            updateGradeDisplay(code, marks, maxMarks, credits);
            saveGrades();
            calculateCumulativeGPA();
            calculateSemesterGPAs();
        }

        function updateGradeDisplay(code, marks, maxMarks, credits) {
            const grade = getGrade(marks, maxMarks);
            const points = calculatePoints(marks, maxMarks, credits);
            const percentage = marks > 0 ? ((marks / maxMarks) * 100).toFixed(1) : 0;
            
            const gradeEl = document.getElementById('grade-' + code);
            const percentageEl = document.getElementById('percentage-' + code);
            const pointsEl = document.getElementById('points-' + code);
            
            if (gradeEl) {
                gradeEl.textContent = marks > 0 ? grade : '-';
                gradeEl.className = 'grade-badge grade-' + (marks > 0 ? getGradeClass(marks, maxMarks) : 'F');
            }
            if (percentageEl) {
                percentageEl.textContent = marks > 0 ? percentage + '%' : '-';
            }
            if (pointsEl) {
                pointsEl.textContent = marks > 0 ? points.toFixed(2) : '-';
            }
        }

        function getGrade(marks, maxMarks) {
            if (marks === 0) return 'F';
            const percentage = (marks / maxMarks) * 100;
            
            if (percentage >= 95) return 'A+';
            if (percentage >= 90) return 'A';
            if (percentage >= 85) return 'A-';
            if (percentage >= 80) return 'B+';
            if (percentage >= 75) return 'B';
            if (percentage >= 70) return 'B-';
            if (percentage >= 65) return 'C+';
            if (percentage >= 60) return 'C';
            if (percentage >= 55) return 'C-';
            if (percentage >= 53) return 'D+';
            if (percentage >= 52) return 'D';
            if (percentage >= 50) return 'D-';
            return 'F';
        }

        function getGradeClass(marks, maxMarks) {
            if (!marks) return 'F';
            const grade = getGrade(marks, maxMarks);
            if (grade.startsWith('A')) return 'A';
            if (grade.startsWith('B')) return 'B';
            if (grade.startsWith('C')) return 'C';
            if (grade.startsWith('D')) return 'D';
            return 'F';
        }

        function calculatePoints(marks, maxMarks, credits) {
            if (marks === 0) return 0;
            const percentage = (marks / maxMarks) * 100;
            let gradePoint = 0;
            
            if (percentage >= 95) gradePoint = 4.0;
            else if (percentage >= 90) gradePoint = 3.7;
            else if (percentage >= 85) gradePoint = 3.5;
            else if (percentage >= 80) gradePoint = 3.3;
            else if (percentage >= 75) gradePoint = 3.1;
            else if (percentage >= 70) gradePoint = 2.85;
            else if (percentage >= 65) gradePoint = 2.65;
            else if (percentage >= 60) gradePoint = 2.45;
            else if (percentage >= 55) gradePoint = 2.25;
            else if (percentage >= 53) gradePoint = 2.25;
            else if (percentage >= 52) gradePoint = 2.15;
            else if (percentage >= 50) gradePoint = 2.0;
            else gradePoint = 0;
            
            return gradePoint * credits;
        }

        function calculateSemesterGPAs() {
            // Group courses by semester
            const semesterGroups = {};
            Object.entries(courseDatabase).forEach(([code, course]) => {
                const semesterName = course.semester[currentLang];
                if (!semesterGroups[semesterName]) {
                    semesterGroups[semesterName] = [];
                }
                semesterGroups[semesterName].push({ code, ...course });
            });

            // Calculate GPA for each semester
            Object.entries(semesterGroups).forEach(([semesterName, courses]) => {
                let semesterPoints = 0;
                let semesterCredits = 0;
                
                courses.forEach(course => {
                    if (grades[course.code] && grades[course.code] > 0) {
                        const points = calculatePoints(grades[course.code], course.maxMarks, course.credits);
                        semesterPoints += points;
                        semesterCredits += course.credits;
                    }
                });
                
                const gpaElement = document.getElementById(`gpa-${semesterName.replace(/\s+/g, '-').replace(/–/g, '-')}`);
                if (gpaElement) {
                    if (semesterCredits > 0) {
                        const semesterGPA = semesterPoints / semesterCredits;
                        gpaElement.textContent = `${translations[currentLang]['GPA']}: ${semesterGPA.toFixed(2)}`;
                    } else {
                        gpaElement.textContent = `${translations[currentLang]['GPA']}: 0.00`;
                    }
                }
            });
        }

        function calculateCumulativeGPA() {
            let totalPoints = 0;
            let totalCredits = 0;
            
            // Only count courses that have actual grades entered (ignore empty ones)
            Object.entries(courseDatabase).forEach(([code, course]) => {
                if (grades[code] && grades[code] > 0) {
                    const points = calculatePoints(grades[code], course.maxMarks, course.credits);
                    totalPoints += points;
                    totalCredits += course.credits;
                }
            });
            
            if (totalCredits > 0) {
                const cgpa = totalPoints / totalCredits;
                const percentage = (cgpa / 4.0) * 100;
                const grade = getGradeFromGPA(cgpa);
                
                document.getElementById('cumulativeGPA').textContent = cgpa.toFixed(2);
                document.getElementById('totalCredits').textContent = totalCredits;
                document.getElementById('overallGrade').textContent = grade;
                document.getElementById('overallPercentage').textContent = percentage.toFixed(1) + '%';
            } else {
                // Reset to defaults when no grades are entered
                document.getElementById('cumulativeGPA').textContent = '0.00';
                document.getElementById('totalCredits').textContent = '0';
                document.getElementById('overallGrade').textContent = '-';
                document.getElementById('overallPercentage').textContent = '0.0%';
            }
        }

        function getGradeFromGPA(gpa) {
            if (gpa >= 3.8) return 'A+';
            if (gpa >= 3.6) return 'A';
            if (gpa >= 3.4) return 'A-';
            if (gpa >= 3.2) return 'B+';
            if (gpa >= 3.0) return 'B';
            if (gpa >= 2.8) return 'B-';
            if (gpa >= 2.6) return 'C+';
            if (gpa >= 2.4) return 'C';
            if (gpa >= 2.2) return 'C-';
            if (gpa >= 2.21) return 'D+';
            if (gpa >= 2.1) return 'D';
            if (gpa >= 2.0) return 'D-';
            return 'F';
        }

        function openSmartImport() {
            document.getElementById('smartImportModal').classList.add('active');
        }

        function closeModal() {
            document.getElementById('smartImportModal').classList.remove('active');
        }

        function processSmartImport() {
            const text = document.getElementById('importText').value;
            const lines = text.split('\n');
            let importedCount = 0;
            let notFoundCodes = [];
            
            lines.forEach(line => {
                if (!line.trim()) return; // Skip empty lines
                
                // First try to find a course code (case insensitive)
                const codeMatch = line.match(/\b([A-Z]{2,4}\d{1,4})\b/i);
                if (!codeMatch) return;
                
                const code = codeMatch[1].toUpperCase();
                if (!courseDatabase[code]) {
                    if (!notFoundCodes.includes(code)) {
                        notFoundCodes.push(code);
                    }
                    return;
                }
                
                let score = null;
                
                // Priority 1: Look for "Total: XX" format (most reliable for final marks)
                const totalMatch = line.match(/Total:\s*(\d+(?:\.\d+)?)/i);
                if (totalMatch) {
                    score = parseFloat(totalMatch[1]);
                }
                
                // Priority 2: Look for "Written: XX" format
                if (score === null) {
                    const writtenMatch = line.match(/Written:\s*(\d+(?:\.\d+)?)/i);
                    if (writtenMatch) {
                        score = parseFloat(writtenMatch[1]);
                    }
                }
                
                // Priority 3: Look for "Practical: XX" format
                if (score === null) {
                    const practicalMatch = line.match(/Practical:\s*(\d+(?:\.\d+)?)/i);
                    if (practicalMatch) {
                        score = parseFloat(practicalMatch[1]);
                    }
                }
                
                // Priority 4: Look for "XX/YYY" or "XX / YYY" format (score/total)
                if (score === null) {
                    const slashMatch = line.match(/(\d+(?:\.\d+)?)\s*\/\s*(\d+(?:\.\d+)?)/);
                    if (slashMatch) {
                        const num1 = parseFloat(slashMatch[1]);
                        const num2 = parseFloat(slashMatch[2]);
                        // Use the first number (the score)
                        score = num1;
                        // Validate that it's not bigger than the total
                        if (num2 > 0 && num1 > num2) {
                            score = Math.min(num1, num2);
                        }
                    }
                }
                
                // Priority 5: Look for standalone number after course code
                if (score === null) {
                    // Remove common non-score patterns first
                    let cleanLine = line.replace(/Hours?:\s*\d+/gi, '')
                                         .replace(/Credits?:\s*\d+/gi, '')
                                         .replace(/Term Work:\s*\d+/gi, '');
                    
                    // Find the course code position
                    const codeIndex = cleanLine.toUpperCase().indexOf(code);
                    if (codeIndex >= 0) {
                        // Get text after the course code
                        const afterCode = cleanLine.substring(codeIndex + code.length);
                        // Look for first number that could be a score
                        const numberMatch = afterCode.match(/[:\-–—\s]+(\d+(?:\.\d+)?)/);
                        if (numberMatch) {
                            const potentialScore = parseFloat(numberMatch[1]);
                            // Only accept if it's reasonable (not hours, not too high)
                            if (potentialScore <= courseDatabase[code].maxMarks) {
                                score = potentialScore;
                            }
                        }
                    }
                }
                
                // Save the grade if we found a valid score
                if (score !== null && score >= 0 && score <= courseDatabase[code].maxMarks) {
                    grades[code] = score;
                    importedCount++;
                }
            });
            
            if (importedCount > 0) {
                saveGrades();
                renderSemesters();
                calculateCumulativeGPA();
                calculateSemesterGPAs();
                
                let successMsg = currentLang === 'en' 
                    ? `✅ Successfully imported ${importedCount} grade${importedCount > 1 ? 's' : ''}!`
                    : `✅ تم استيراد ${importedCount} درجة بنجاح!`;
                
                if (notFoundCodes.length > 0) {
                    successMsg += currentLang === 'en'
                        ? `\n⚠️ Warning: Could not find courses: ${notFoundCodes.join(', ')}`
                        : `\n⚠️ تحذير: لم يتم العثور على المقررات: ${notFoundCodes.join(', ')}`;
                }
                
                showNotification(successMsg);
                closeModal();
                document.getElementById('importText').value = '';
            } else {
                let errorMsg = currentLang === 'en'
                    ? '⚠️ No valid grades found. Please check the format:\n'
                    : '⚠️ لم يتم العثور على درجات صالحة. يرجى التحقق من التنسيق:\n';
                
                errorMsg += currentLang === 'en'
                    ? 'Example: UN101 Total: 85 or TL201: 90'
                    : 'مثال: UN101 Total: 85 أو TL201: 90';
                
                if (notFoundCodes.length > 0) {
                    errorMsg += currentLang === 'en'
                        ? `\n\n⚠️ Course codes not in database: ${notFoundCodes.join(', ')}`
                        : `\n\n⚠️ رموز المقررات غير موجودة: ${notFoundCodes.join(', ')}`;
                }
                
                showNotification(errorMsg);
            }
        }

        function resetAll() {
            if (confirm(currentLang === 'en' ? 'Are you sure you want to reset all grades?' : 'هل أنت متأكد من إعادة تعيين جميع الدرجات؟')) {
                grades = {};
                saveGrades();
                renderSemesters();
                calculateCumulativeGPA();
                calculateSemesterGPAs();
                const resetMsg = currentLang === 'en' 
                    ? '✅ All grades have been reset!'
                    : '✅ تم إعادة تعيين جميع الدرجات!';
                showNotification(resetMsg);
            }
        }

        function saveGrades() {
            localStorage.setItem('medLabGrades', JSON.stringify(grades));
        }

        function loadGrades() {
            const saved = localStorage.getItem('medLabGrades');
            if (saved) {
                try {
                    grades = JSON.parse(saved);
                } catch (e) {
                    grades = {};
                }
            }
        }

        function toggleTheme() {
            const body = document.body;
            const btn = document.querySelector('.theme-toggle');
            
            if (currentTheme === 'dark') {
                body.setAttribute('data-theme', 'light');
                btn.textContent = '☀️';
                currentTheme = 'light';
            } else {
                body.setAttribute('data-theme', 'dark');
                btn.textContent = '🌙';
                currentTheme = 'dark';
            }
        }

        function showNotification(message) {
            const notification = document.createElement('div');
            notification.className = 'notification';
            notification.textContent = message;
            document.body.appendChild(notification);
            
            // Longer display time for multi-line messages
            const displayTime = message.includes('\n') ? 5000 : 3000;
            
            setTimeout(() => {
                notification.remove();
            }, displayTime);
        }
    </script>
</body>
</html>
