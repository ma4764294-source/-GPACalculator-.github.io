<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=5.0, user-scalable=yes">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="mobile-web-app-capable" content="yes">
    <title>HNU GPA Calculator</title>
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
            --red-sparkle: #ff1744;
            --blue-sparkle: #00d4ff;
            --dark-blue: #0f172a;
            --paste-dark: #1e1b4b;
            
            /* Responsive sizing variables */
            --nav-height: 8rem;
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
            --dark-blue: #1e3a8a;
            --paste-dark: #e0e7ff;
        }

        /* ========== SPARKLE ANIMATIONS ========== */
        @keyframes sparkle-red {
            0%, 100% { text-shadow: 0 0 0.5rem var(--red-sparkle), 0 0 1rem var(--red-sparkle); }
            50% { text-shadow: 0 0 1rem var(--red-sparkle), 0 0 2rem var(--red-sparkle), 0 0 3rem var(--red-sparkle); }
        }

        @keyframes sparkle-blue {
            0%, 100% { text-shadow: 0 0 0.5rem var(--blue-sparkle), 0 0 1rem var(--blue-sparkle); }
            50% { text-shadow: 0 0 1rem var(--blue-sparkle), 0 0 2rem var(--blue-sparkle), 0 0 3rem var(--blue-sparkle); }
        }

        @keyframes slideIn {
            from { transform: translateX(-100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(1rem); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        @keyframes shimmer {
            0% { background-position: -100% 0; }
            100% { background-position: 200% 0; }
        }

        @keyframes gradientShift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        /* ========== RESPONSIVE FONT SIZING ========== */
        @media screen and (max-width: 480px) {
            html { font-size: 14px; }
            :root { 
                --nav-height: 9rem;
                --base-padding: 3%;
                --card-padding: 5%;
            }
        }
        
        @media screen and (min-width: 481px) and (max-width: 768px) {
            html { font-size: 15px; }
            :root { 
                --nav-height: 8.5rem;
                --base-padding: 3%;
            }
        }
        
        @media screen and (min-width: 769px) and (max-width: 1024px) {
            html { font-size: 16px; }
            :root { 
                --nav-height: 5rem;
                --base-padding: 2.5%;
            }
        }
        
        @media screen and (min-width: 1025px) and (max-width: 1440px) {
            html { font-size: 17px; }
            :root { 
                --nav-height: 5.5rem;
                --base-padding: 2%;
            }
        }
        
        @media screen and (min-width: 1441px) {
            html { font-size: 18px; }
            :root { 
                --nav-height: 6rem;
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
            min-height: var(--nav-height);
            background: var(--bg-card);
            border-bottom: 0.125rem solid var(--border);
            display: flex;
            flex-direction: column;
            z-index: 1000;
            box-shadow: 0 0.25rem 1rem var(--shadow);
        }

        .nav-main {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: clamp(0.6rem, 2vw, 1rem) var(--base-padding);
        }

        .app-title {
            font-size: clamp(1.1rem, 3vw, 1.6rem);
            font-weight: 700;
            background: linear-gradient(135deg, var(--accent), var(--accent-light));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            display: flex;
            align-items: center;
            gap: 0.5em;
            flex: 1;
            min-width: 0;
        }

        .nav-controls {
            display: flex;
            align-items: center;
            gap: clamp(0.4rem, 1.5vw, 0.8rem);
            flex-shrink: 0;
        }

        .language-switcher-nav {
            display: flex;
            gap: clamp(0.3rem, 1vw, 0.5rem);
            background: var(--bg-secondary);
            border: 0.0625rem solid var(--border);
            border-radius: 0.75rem;
            padding: 0.3rem;
            box-shadow: 0 0.125rem 0.5rem var(--shadow);
        }

        .lang-btn-nav {
            padding: 0.5em 1em;
            background: transparent;
            color: var(--text-secondary);
            border: none;
            border-radius: 0.5rem;
            cursor: pointer;
            transition: all 0.3s;
            font-size: clamp(0.85rem, 2vw, 1.05rem);
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 0.4em;
            position: relative;
            overflow: hidden;
        }

        .lang-btn-nav::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.1), transparent);
            transition: left 0.5s;
        }

        .lang-btn-nav:hover::before {
            left: 100%;
        }

        .lang-btn-nav.active {
            background: linear-gradient(135deg, var(--accent), var(--accent-hover));
            color: white;
            box-shadow: 0 0.25rem 0.75rem rgba(59, 130, 246, 0.4);
        }

        .theme-toggle, .menu-toggle {
            width: clamp(2.2rem, 6vw, 2.8rem);
            height: clamp(2.2rem, 6vw, 2.8rem);
            background: var(--bg-secondary);
            border: 0.0625rem solid var(--border);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.3s;
            font-size: clamp(1rem, 2.5vw, 1.3rem);
        }

        .theme-toggle:hover, .menu-toggle:hover {
            background: var(--accent);
            transform: scale(1.1);
        }

        /* ========== SEMESTER BAR WITH GPA ========== */
        .semester-bar {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 1rem var(--base-padding);
            background: linear-gradient(135deg, var(--accent), var(--accent-hover));
            border-bottom: 0.125rem solid var(--border);
            flex-wrap: wrap;
            gap: 1rem;
        }

        .semester-info {
            display: flex;
            align-items: center;
            gap: 1.5%;
            flex-wrap: wrap;
        }

        .semester-stat {
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(10px);
            padding: 0.6rem 1.2rem;
            border-radius: 0.5rem;
            border: 1px solid rgba(255, 255, 255, 0.2);
            text-align: center;
            min-width: 8rem;
        }

        .semester-stat-label {
            font-size: 0.75rem;
            color: rgba(255, 255, 255, 0.8);
            font-weight: 500;
            text-transform: uppercase;
            letter-spacing: 0.05em;
            margin-bottom: 0.25rem;
        }

        .semester-stat-value {
            font-size: 1.4rem;
            color: white;
            font-weight: 700;
            text-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
        }

        /* ========== OVERALL STATS ========== */
        .overall-stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(min(100%, 15rem), 1fr));
            gap: var(--gap-medium);
            padding: var(--base-padding);
            max-width: 100%;
        }

        .stat-card {
            background: var(--bg-card);
            border: 0.0625rem solid var(--border);
            border-radius: var(--border-radius);
            padding: var(--card-padding);
            text-align: center;
            transition: all 0.3s;
            animation: fadeIn 0.6s ease-out;
            box-shadow: 0 0.25rem 1rem var(--shadow);
        }

        .stat-card:hover {
            transform: translateY(-0.5rem);
            box-shadow: 0 0.5rem 2rem var(--shadow);
        }

        .stat-label {
            color: var(--text-secondary);
            font-size: clamp(0.75rem, 2vw, 0.875rem);
            font-weight: 600;
            margin-bottom: 0.5rem;
            text-transform: uppercase;
            letter-spacing: 0.05em;
        }

        .stat-value {
            font-size: clamp(2rem, 5vw, 3rem);
            font-weight: 700;
            background: linear-gradient(135deg, var(--accent), var(--accent-light));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 0.5rem;
        }

        .stat-grade {
            font-size: clamp(1rem, 2.5vw, 1.25rem);
            font-weight: 600;
            color: var(--success);
        }

        /* ========== SMART IMPORT SECTION ========== */
        .smart-import-section {
            margin: var(--gap-large) var(--base-padding);
            background: linear-gradient(135deg, #0f172a 0%, #1e1b4b 50%, #0f172a 100%);
            border: 0.125rem solid rgba(59, 130, 246, 0.4);
            border-radius: var(--border-radius);
            padding: var(--card-padding);
            box-shadow: 0 0.5rem 2rem rgba(59, 130, 246, 0.2);
            animation: fadeIn 0.6s ease-out;
            position: relative;
            overflow: hidden;
        }

        .smart-import-section::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 50%;
            height: 100%;
            background: linear-gradient(90deg, 
                transparent 0%, 
                rgba(96, 165, 250, 0.1) 50%,
                transparent 100%
            );
            animation: shineSlide 4s ease-in-out infinite;
            pointer-events: none;
        }

        .smart-import-header {
            text-align: center;
            margin-bottom: 1.5rem;
        }

        .smart-import-title {
            font-size: clamp(1.3rem, 3.5vw, 1.8rem);
            font-weight: 700;
            background: linear-gradient(135deg, #60a5fa, #3b82f6, #2563eb);
            background-size: 200% 200%;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            animation: gradientShift 3s ease infinite;
            margin-bottom: 0.5rem;
        }

        .smart-import-subtitle {
            color: var(--text-secondary);
            font-size: clamp(0.85rem, 2vw, 1rem);
        }

        .paste-area {
            width: 100%;
            min-height: 12rem;
            background: rgba(0, 0, 0, 0.3);
            border: 0.125rem dashed rgba(96, 165, 250, 0.5);
            border-radius: 0.5rem;
            padding: 1.5rem;
            color: var(--text-primary);
            font-size: 0.95rem;
            font-family: 'Inter', monospace;
            resize: vertical;
            transition: all 0.3s;
            margin-bottom: 1.5rem;
        }

        .paste-area:focus {
            outline: none;
            border-color: var(--accent-light);
            background: rgba(0, 0, 0, 0.4);
            box-shadow: 0 0 1rem rgba(59, 130, 246, 0.3);
        }

        .paste-area::placeholder {
            color: var(--text-secondary);
        }

        .import-btn {
            width: 100%;
            padding: 1.2rem 2rem;
            background: linear-gradient(135deg, #1e1b4b, #0f172a);
            color: white;
            border: 0.125rem solid var(--accent);
            border-radius: 0.75rem;
            font-size: clamp(1rem, 2.5vw, 1.2rem);
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s;
            text-transform: uppercase;
            letter-spacing: 0.05em;
            box-shadow: 0 0.25rem 1rem rgba(59, 130, 246, 0.4);
            position: relative;
            overflow: hidden;
        }

        .import-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            transition: left 0.5s;
        }

        .import-btn:hover::before {
            left: 100%;
        }

        .import-btn:hover {
            transform: translateY(-0.25rem);
            box-shadow: 0 0.5rem 1.5rem rgba(59, 130, 246, 0.6);
            background: linear-gradient(135deg, #0f172a, #1e1b4b);
        }

        .import-btn:active {
            transform: translateY(0);
        }

        /* ========== CHARTS SECTION ========== */
        .charts-section {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(min(100%, 25rem), 1fr));
            gap: var(--gap-medium);
            padding: var(--base-padding);
            margin-top: var(--gap-large);
            min-height: 20rem;
        }

        .chart-card {
            background: var(--bg-card);
            border: 0.0625rem solid var(--border);
            border-radius: var(--border-radius);
            padding: var(--card-padding);
            animation: fadeIn 0.6s ease-out;
            box-shadow: 0 0.25rem 1rem var(--shadow);
            transition: all 0.3s;
            min-height: 25rem;
        }

        .chart-card:hover {
            transform: translateY(-0.25rem);
            box-shadow: 0 0.5rem 2rem var(--shadow);
            border-color: rgba(59, 130, 246, 0.5);
        }

        .chart-title {
            font-size: clamp(1.1rem, 2.5vw, 1.3rem);
            font-weight: 700;
            margin-bottom: 1.5rem;
            color: var(--text-primary);
        }

        .chart-container {
            position: relative;
            width: 100%;
            height: 18rem;
            min-height: 15rem;
        }

        .download-chart-btn {
            width: 100%;
            padding: 0.8rem;
            margin-top: 1rem;
            background: var(--accent);
            color: white;
            border: none;
            border-radius: 0.5rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
        }

        .download-chart-btn:hover {
            background: var(--accent-hover);
            transform: translateY(-0.125rem);
        }

        /* ========== SEMESTERS SECTION ========== */
        .semesters-section {
            padding: var(--base-padding);
            margin-top: var(--gap-large);
            min-height: 10rem;
        }

        .semesters-title {
            font-size: clamp(1.5rem, 3.5vw, 2rem);
            font-weight: 700;
            margin-bottom: 1.5rem;
            text-align: center;
            animation: fadeIn 0.6s ease-out;
        }

        .semester-accordion {
            margin-bottom: 1.5rem;
            animation: fadeIn 0.6s ease-out;
            animation-fill-mode: both;
        }

        .semester-header {
            background: linear-gradient(135deg, #1e3a8a 0%, #0f172a 100%);
            padding: 1.2rem var(--card-padding);
            border-radius: var(--border-radius);
            cursor: pointer;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: all 0.3s;
            flex-wrap: wrap;
            gap: 1rem;
            position: relative;
            overflow: hidden;
            border: 0.0625rem solid rgba(59, 130, 246, 0.3);
            box-shadow: 0 0.25rem 1rem rgba(15, 23, 42, 0.5);
        }

        .semester-header::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 50%;
            height: 100%;
            background: linear-gradient(90deg, 
                transparent 0%, 
                rgba(148, 163, 184, 0.15) 25%,
                rgba(148, 163, 184, 0.3) 50%,
                rgba(148, 163, 184, 0.15) 75%,
                transparent 100%
            );
            animation: shineSlide 3s ease-in-out infinite;
            pointer-events: none;
        }

        @keyframes shineSlide {
            0% {
                left: -100%;
            }
            100% {
                left: 200%;
            }
        }

        .semester-header:hover {
            transform: translateY(-0.25rem);
            box-shadow: 0 0.5rem 1.5rem rgba(30, 58, 138, 0.4);
            border-color: rgba(59, 130, 246, 0.5);
        }

        .semester-header:hover::before {
            animation-duration: 1.5s;
        }

        .semester-header-info {
            display: flex;
            align-items: center;
            gap: 2%;
            flex: 1;
            flex-wrap: wrap;
        }

        .semester-name {
            font-size: clamp(1.1rem, 2.5vw, 1.4rem);
            font-weight: 700;
            color: white;
        }

        .semester-stats-inline {
            display: flex;
            gap: 1.5rem;
            align-items: center;
            flex-wrap: wrap;
        }

        .semester-stat-inline {
            display: flex;
            flex-direction: column;
            align-items: center;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            padding: 0.6rem 1.2rem;
            border-radius: 0.5rem;
            border: 0.0625rem solid rgba(255, 255, 255, 0.25);
            min-width: 6rem;
            box-shadow: 0 0.125rem 0.5rem rgba(0, 0, 0, 0.2);
            transition: all 0.3s;
        }

        .semester-stat-inline:hover {
            background: rgba(255, 255, 255, 0.15);
            transform: translateY(-0.125rem);
            box-shadow: 0 0.25rem 0.75rem rgba(0, 0, 0, 0.3);
        }

        .semester-stat-inline-label {
            font-size: 0.7rem;
            color: rgba(255, 255, 255, 0.8);
            font-weight: 500;
            text-transform: uppercase;
            margin-bottom: 0.2rem;
        }

        .semester-stat-inline-value {
            font-size: 1.1rem;
            color: white;
            font-weight: 700;
        }

        .semester-toggle {
            color: white;
            font-size: 1.5rem;
            transition: transform 0.3s;
        }

        .semester-accordion.active .semester-toggle {
            transform: rotate(180deg);
        }

        .semester-content {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s ease-out;
            background: var(--bg-card);
            border: 0.0625rem solid var(--border);
            border-top: none;
            border-radius: 0 0 var(--border-radius) var(--border-radius);
        }

        .semester-accordion.active .semester-content {
            max-height: 200rem;
        }

        .course-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(min(100%, 18rem), 1fr));
            gap: var(--gap-medium);
            padding: var(--card-padding);
        }

        .course-card {
            background: var(--bg-secondary);
            border: 0.0625rem solid var(--border);
            border-radius: 0.5rem;
            padding: 1.2rem;
            transition: all 0.3s;
            box-shadow: 0 0.125rem 0.5rem var(--shadow);
        }

        .course-card:hover {
            transform: translateY(-0.25rem);
            box-shadow: 0 0.5rem 1.5rem var(--shadow);
            border-color: var(--accent);
        }

        .course-name {
            font-size: 0.95rem;
            font-weight: 600;
            color: var(--text-primary);
            margin-bottom: 0.8rem;
        }

        .course-details {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 0.5rem;
            font-size: 0.85rem;
            color: var(--text-secondary);
            margin-bottom: 1rem;
        }

        .grade-input-group {
            display: flex;
            flex-direction: column;
            gap: 0.5rem;
        }

        .grade-input-label {
            font-size: 0.8rem;
            font-weight: 600;
            color: var(--text-secondary);
        }

        .grade-input {
            width: 100%;
            padding: 0.7rem;
            background: var(--bg-primary);
            border: 0.0625rem solid var(--border);
            border-radius: 0.375rem;
            color: var(--text-primary);
            font-size: 0.95rem;
            transition: all 0.3s;
        }

        .grade-input:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 0.5rem rgba(59, 130, 246, 0.3);
        }

        /* ========== SIDE MENU ========== */
        .side-menu {
            position: fixed;
            top: var(--nav-height);
            right: -100%;
            width: min(85%, 25rem);
            height: calc(100vh - var(--nav-height));
            background: var(--bg-card);
            border-left: 0.0625rem solid var(--border);
            box-shadow: -0.5rem 0 2rem var(--shadow);
            transition: right 0.3s ease-out;
            z-index: 999;
            overflow-y: auto;
        }

        body[dir="rtl"] .side-menu {
            right: auto;
            left: -100%;
            border-left: none;
            border-right: 0.0625rem solid var(--border);
        }

        .side-menu.active {
            right: 0;
        }

        body[dir="rtl"] .side-menu.active {
            right: auto;
            left: 0;
        }

        .menu-overlay {
            position: fixed;
            top: var(--nav-height);
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.5);
            backdrop-filter: blur(0.25rem);
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s;
            z-index: 998;
        }

        .menu-overlay.active {
            opacity: 1;
            visibility: visible;
        }

        .menu-header {
            padding: 1.5rem;
            border-bottom: 0.0625rem solid var(--border);
            font-size: 1.3rem;
            font-weight: 700;
        }

        .menu-items {
            padding: 1rem;
        }

        .menu-item {
            width: 100%;
            padding: 1rem 1.5rem;
            background: var(--bg-secondary);
            border: 0.0625rem solid var(--border);
            border-radius: 0.5rem;
            margin-bottom: 0.8rem;
            color: var(--text-primary);
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            gap: 0.8rem;
            text-align: left;
            box-shadow: 0 0.125rem 0.5rem var(--shadow);
            position: relative;
            overflow: hidden;
        }

        .menu-item::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(59, 130, 246, 0.2), transparent);
            transition: left 0.5s;
        }

        .menu-item:hover::before {
            left: 100%;
        }

        body[dir="rtl"] .menu-item {
            text-align: right;
        }

        .menu-item:hover {
            background: linear-gradient(135deg, var(--accent), var(--accent-hover));
            color: white;
            transform: translateX(-0.25rem);
            box-shadow: 0 0.25rem 1rem rgba(59, 130, 246, 0.4);
        }

        body[dir="rtl"] .menu-item:hover {
            transform: translateX(0.25rem);
        }

        /* ========== MODALS ========== */
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.7);
            backdrop-filter: blur(0.5rem);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 2000;
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s;
            padding: 5%;
        }

        .modal.active {
            opacity: 1;
            visibility: visible;
        }

        .modal-content {
            background: var(--bg-card);
            border: 0.0625rem solid var(--border);
            border-radius: var(--border-radius);
            padding: var(--card-padding);
            width: 100%;
            max-width: 35rem;
            max-height: 90vh;
            overflow-y: auto;
            transform: scale(0.9);
            transition: transform 0.3s;
        }

        .modal.active .modal-content {
            transform: scale(1);
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
        }

        .modal-title {
            font-size: 1.5rem;
            font-weight: 700;
        }

        .modal-close {
            width: 2rem;
            height: 2rem;
            background: var(--bg-secondary);
            border: none;
            border-radius: 50%;
            color: var(--text-primary);
            font-size: 1.3rem;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .modal-close:hover {
            background: var(--danger);
            color: white;
            transform: rotate(90deg);
        }

        .form-group {
            margin-bottom: 1.2rem;
        }

        .form-label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 600;
            color: var(--text-secondary);
        }

        .form-input, .form-select {
            width: 100%;
            padding: 0.8rem;
            background: var(--bg-secondary);
            border: 0.0625rem solid var(--border);
            border-radius: 0.5rem;
            color: var(--text-primary);
            font-size: 1rem;
            transition: all 0.3s;
        }

        .form-input:focus, .form-select:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 0.5rem rgba(59, 130, 246, 0.3);
        }

        .btn-primary {
            width: 100%;
            padding: 1rem;
            background: var(--accent);
            color: white;
            border: none;
            border-radius: 0.5rem;
            font-size: 1.1rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s;
            margin-top: 1rem;
        }

        .btn-primary:hover {
            background: var(--accent-hover);
            transform: translateY(-0.125rem);
        }

        /* ========== ABOUT PAGE ========== */
        .about-page {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: var(--bg-primary);
            z-index: 3000;
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s;
            overflow-y: auto;
            padding: 5%;
        }

        .about-page.active {
            opacity: 1;
            visibility: visible;
        }

        .about-container {
            max-width: 50rem;
            margin: 0 auto;
            background: var(--bg-card);
            border: 0.0625rem solid var(--border);
            border-radius: var(--border-radius);
            padding: var(--card-padding);
        }

        .about-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 2rem;
            padding-bottom: 1rem;
            border-bottom: 0.125rem solid var(--border);
        }

        .about-title {
            font-size: 2rem;
            font-weight: 700;
            background: linear-gradient(135deg, var(--accent), var(--accent-light));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .about-close {
            width: 2.5rem;
            height: 2.5rem;
            background: var(--bg-secondary);
            border: none;
            border-radius: 50%;
            color: var(--text-primary);
            font-size: 1.5rem;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .about-close:hover {
            background: var(--danger);
            color: white;
            transform: rotate(90deg);
        }

        .about-content {
            line-height: 1.8;
            color: var(--text-secondary);
            margin-bottom: 2rem;
        }

        .about-content p {
            margin-bottom: 1rem;
        }

        .about-credits {
            background: var(--bg-secondary);
            border: 0.0625rem solid var(--border);
            border-radius: 0.5rem;
            padding: 1.5rem;
        }

        .about-credits h3 {
            font-size: 1.3rem;
            margin-bottom: 1rem;
            color: var(--text-primary);
        }

        .credit-item {
            display: flex;
            justify-content: space-between;
            padding: 0.8rem 0;
            border-bottom: 0.0625rem solid var(--border);
        }

        .credit-item:last-child {
            border-bottom: none;
        }

        .credit-label {
            font-weight: 600;
            color: var(--text-secondary);
        }

        .credit-value {
            color: var(--accent);
            font-weight: 600;
        }

        /* ========== NOTIFICATION ========== */
        .notification {
            position: fixed;
            bottom: 2rem;
            left: 50%;
            transform: translateX(-50%) translateY(10rem);
            background: var(--bg-card);
            border: 0.0625rem solid var(--accent);
            border-radius: 0.75rem;
            padding: 1rem 2rem;
            box-shadow: 0 0.5rem 2rem var(--shadow);
            z-index: 9999;
            opacity: 0;
            transition: all 0.3s;
            font-weight: 600;
            max-width: 90%;
            text-align: center;
        }

        .notification.show {
            transform: translateX(-50%) translateY(0);
            opacity: 1;
        }

        /* ========== FOOTER ========== */
        .footer {
            text-align: center;
            padding: 3% var(--base-padding);
            margin-top: 5%;
            border-top: 0.0625rem solid var(--border);
            color: var(--text-secondary);
            background: var(--bg-secondary);
        }

        .footer-content {
            display: flex;
            flex-direction: row;
            gap: 4%;
            align-items: center;
            justify-content: center;
            flex-wrap: wrap;
        }

        .developer-credit {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 0.5rem;
            transition: all 0.3s;
        }

        .developer-credit:hover {
            transform: scale(1.05);
        }

        .credit-label {
            font-size: 0.75rem;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.1em;
            color: var(--text-secondary);
        }

        .developer-name {
            font-weight: 700;
            text-decoration: none;
            transition: all 0.3s;
            position: relative;
            font-size: 1.2rem;
        }

        .developer-name.red-sparkle {
            color: #ff1744;
            animation: sparkle-red 1.5s infinite;
        }

        .developer-name.blue-sparkle {
            color: #00d4ff;
            animation: sparkle-blue 1.5s infinite;
        }

        .developer-name::after {
            content: '';
            position: absolute;
            bottom: -0.125rem;
            left: 0;
            width: 0;
            height: 0.125rem;
            background: currentColor;
            transition: width 0.3s;
        }

        .developer-name:hover::after {
            width: 100%;
        }

        @media (max-width: 768px) {
            .footer-content {
                flex-direction: column;
                gap: 1.5rem;
            }
        }

        /* ========== RESPONSIVE ADJUSTMENTS ========== */
        @media (max-width: 768px) {
            .semester-stats-inline {
                width: 100%;
                justify-content: center;
            }

            .overall-stats {
                grid-template-columns: 1fr;
            }

            .charts-section {
                grid-template-columns: 1fr;
            }

            .course-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body dir="ltr">
    <!-- Top Navigation -->
    <nav class="top-nav">
        <div class="nav-main">
            <div class="app-title">
                <span>🎓</span>
                <span>HNU GPA Calculator</span>
            </div>
            <div class="nav-controls">
                <div class="language-switcher-nav">
                    <button class="lang-btn-nav active" onclick="switchLanguage('en')">
                        <span>🇺🇸</span>
                        <span>EN</span>
                    </button>
                    <button class="lang-btn-nav" onclick="switchLanguage('ar')">
                        <span>🇸🇦</span>
                        <span>AR</span>
                    </button>
                </div>
                <button class="theme-toggle" onclick="toggleTheme()">🌙</button>
                <button class="menu-toggle" onclick="toggleMenu()">☰</button>
            </div>
        </div>
    </nav>

    <!-- Menu Overlay -->
    <div class="menu-overlay" onclick="toggleMenu()"></div>

    <!-- Side Menu -->
    <div class="side-menu">
        <div class="menu-header" data-translate="menu">Menu</div>
        <div class="menu-items">
            <button class="menu-item" onclick="openModal('profileModal')">
                <span>👤</span>
                <span data-translate="profile">Profile</span>
            </button>
            <button class="menu-item" onclick="openModal('settingsModal')">
                <span>⚙️</span>
                <span data-translate="settings">Settings</span>
            </button>
            <button class="menu-item" onclick="shareGPA()">
                <span>📤</span>
                <span data-translate="shareGPA">Share GPA</span>
            </button>
            <button class="menu-item" onclick="clearAllData()">
                <span>🗑️</span>
                <span data-translate="clearData">Clear All Data</span>
            </button>
            <button class="menu-item" onclick="openAboutPage()">
                <span>ℹ️</span>
                <span data-translate="about">About</span>
            </button>
        </div>
    </div>

    <!-- Main Content -->
    <main>
        <!-- Overall Stats -->
        <div class="overall-stats">
            <div class="stat-card">
                <div class="stat-label" data-translate="cumulativeGPA">CUMULATIVE GPA</div>
                <div class="stat-value" id="cumulativeGPA">0.00</div>
                <div class="stat-grade" id="overallGrade">-</div>
            </div>
            <div class="stat-card">
                <div class="stat-label" data-translate="totalCredits">Total Credits</div>
                <div class="stat-value" id="totalCredits">0</div>
            </div>
            <div class="stat-card">
                <div class="stat-label" data-translate="avgPercentage">Avg %</div>
                <div class="stat-value" id="avgPercentage">0%</div>
            </div>
            <div class="stat-card">
                <div class="stat-label" data-translate="totalCourses">Total Courses</div>
                <div class="stat-value" id="totalCourses">0</div>
            </div>
        </div>

        <!-- Smart Import Section -->
        <div class="smart-import-section">
            <div class="smart-import-header">
                <h2 class="smart-import-title" data-translate="pasteTitle">📋 PASTE YOUR GPA PAGE BY 1 CLICK</h2>
                <p class="smart-import-subtitle" data-translate="pasteSubtitle">Simply paste your GPA page text here and it will auto-fill all your grades!</p>
            </div>
            <textarea 
                class="paste-area" 
                id="pasteArea" 
                placeholder="Paste your GPA page content here..."></textarea>
            <button class="import-btn" onclick="smartImport()">
                <span data-translate="pasteBtn">🚀 Auto-Fill Grades</span>
            </button>
        </div>

        <!-- Charts Section -->
        <div class="charts-section">
            <div class="chart-card">
                <h3 class="chart-title" data-translate="gpaProgress">📈 GPA Progress</h3>
                <div class="chart-container">
                    <canvas id="gpaProgressChart"></canvas>
                </div>
                <button class="download-chart-btn" onclick="downloadChart('gpaProgressChart')" data-translate="downloadGPA">DOWNLOAD GPA PROGRESS</button>
            </div>
            <div class="chart-card">
                <h3 class="chart-title" data-translate="gradeDistribution">📊 Grade Distribution</h3>
                <div class="chart-container">
                    <canvas id="gradeDistributionChart"></canvas>
                </div>
            </div>
        </div>

        <!-- Semesters Section -->
        <div class="semesters-section">
            <h2 class="semesters-title" data-translate="semesters">📚 Semesters</h2>
            <div id="semestersContainer"></div>
        </div>

        <!-- Footer -->
        <footer class="footer">
            <div class="footer-content">
                <div class="developer-credit">
                    <span class="credit-label">MADE BY</span>
                    <a href="#" class="developer-name red-sparkle">Mohand</a>
                </div>
                <div class="developer-credit">
                    <span class="credit-label">DEVELOPER HELPER</span>
                    <a href="#" class="developer-name blue-sparkle">Mahmoud</a>
                </div>
            </div>
        </footer>
    </main>

    <!-- Profile Modal -->
    <div id="profileModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 class="modal-title" data-translate="profile">Profile</h3>
                <button class="modal-close" onclick="closeModal('profileModal')">×</button>
            </div>
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

    <!-- Settings Modal -->
    <div id="settingsModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 class="modal-title" data-translate="settings">Settings</h3>
                <button class="modal-close" onclick="closeModal('settingsModal')">×</button>
            </div>
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
                    <option value="1">1 decimal</option>
                    <option value="2">2 decimals</option>
                    <option value="3">3 decimals</option>
                </select>
            </div>
            <button class="btn-primary" onclick="saveSettings()" data-translate="saveSettings">Save Settings</button>
        </div>
    </div>

    <!-- About Page -->
    <div id="aboutPage" class="about-page">
        <div class="about-container">
            <div class="about-header">
                <h2 class="about-title" data-translate="about">About</h2>
                <button class="about-close" onclick="closeAboutPage()">×</button>
            </div>
            <div class="about-content">
                <p data-translate="aboutText">This is a free GPA calculator website designed to help HNU Medical Laboratory students calculate and track their academic performance. Please note that this calculator provides estimates and is not an official representation of your actual GPA from the university.</p>
            </div>
            <div class="about-credits">
                <h3 data-translate="credits">Credits</h3>
                <div class="credit-item">
                    <span class="credit-label" data-translate="developer">Developer</span>
                    <span class="credit-value">Mohand Ahmed</span>
                </div>
                <div class="credit-item">
                    <span class="credit-label" data-translate="devHelper">Developer Helper</span>
                    <span class="credit-value">Mahmoud Mohamed</span>
                </div>
                <div class="credit-item">
                    <span class="credit-label">Version</span>
                    <span class="credit-value">2.0</span>
                </div>
            </div>
        </div>
    </div>

    <!-- Notification -->
    <div id="notification" class="notification"></div>

    <script>
        // ========== GLOBAL VARIABLES ==========
        let currentLang = 'en';
        let currentTheme = 'dark';
        let decimalPrecision = 2;
        let userGrades = {};
        let gpaProgressChart = null;
        let gradeDistributionChart = null;

        // ========== GPA SCALE ==========
        const gpaScale = {
            'A+': { min: 95, max: 100, points: 4.0 },
            'A': { min: 90, max: 94.99, points: 3.8 },
            'A-': { min: 85, max: 89.99, points: 3.6 },
            'B+': { min: 82.5, max: 84.99, points: 3.4 },
            'B': { min: 77.5, max: 82.49, points: 3.2 },
            'B-': { min: 75, max: 77.49, points: 3.0 },
            'C+': { min: 72.5, max: 74.99, points: 2.8 },
            'C': { min: 67.5, max: 72.49, points: 2.6 },
            'C-': { min: 65, max: 67.49, points: 2.4 },
            'D+': { min: 62.5, max: 64.99, points: 2.2 },
            'D': { min: 60, max: 62.49, points: 2.0 },
            'F': { min: 0, max: 59.99, points: 0 }
        };

        // ========== CURRICULUM DATA ==========
        const curriculum = {
            "First Level - 1st Semester": [
                { code: "UN101", name: "Academic Reading and Writing (1)", credits: 2, total: 100 },
                { code: "THS101", name: "Basic Physics", credits: 2, total: 100 },
                { code: "THS102", name: "Mathematics", credits: 2, total: 100 },
                { code: "THS103", name: "Introduction to Electrical Engineering", credits: 3, total: 150 },
                { code: "UN102", name: "Computer Skills", credits: 2, total: 100 },
                { code: "THS104", name: "Mechanics", credits: 2, total: 100 },
                { code: "UN103", name: "Critical Thinking", credits: 2, total: 100 }
            ],
            "First Level - 2nd Semester": [
                { code: "THS115", name: "Electronic Circuits & Devices", credits: 3, total: 150 },
                { code: "THS116", name: "General Anatomy & Histology", credits: 3, total: 150 },
                { code: "THS117", name: "General Physiology", credits: 2, total: 100 },
                { code: "THS118", name: "General Microbiology", credits: 2, total: 100 },
                { code: "THS119", name: "General Chemistry", credits: 2, total: 100 },
                { code: "UN114", name: "Academic Reading and Writing (2)", credits: 2, total: 100 },
                { code: "THS1110", name: "Professional Ethics", credits: 1, total: 50 }
            ],
            "Second Level - 1st Semester": [
                { code: "THS2010", name: "Mechatronics Engineering", credits: 2, total: 100 },
                { code: "TL201", name: "Biochemistry (1)", credits: 4, total: 200 },
                { code: "TL202", name: "Parasitology (1)", credits: 2, total: 100 },
                { code: "TL203", name: "Bacteriology", credits: 4, total: 200 },
                { code: "TL204", name: "Histology for Lab Technologists", credits: 2, total: 100 },
                { code: "UN5", name: "Foundation of Digital Technology", credits: 2, total: 100 },
                { code: "UN6", name: "English Language", credits: 2, total: 100 }
            ],
            "Second Level - 2nd Semester": [
                { code: "TL215", name: "Molecular Biology", credits: 4, total: 200 },
                { code: "TL216", name: "Hematology (1)", credits: 4, total: 200 },
                { code: "TL217", name: "Systematic Physiology", credits: 4, total: 200 },
                { code: "TL218", name: "General Biology", credits: 3, total: 150 },
                { code: "ETHS1", name: "Elective (1)", credits: 1, total: 50 }
            ],
            "Third Level - 1st Semester": [
                { code: "TL309", name: "Lab Instrumentation (1)", credits: 4, total: 200 },
                { code: "TL3010", name: "Enzymology & Hormones", credits: 4, total: 200 },
                { code: "TL3011", name: "Parasitology (2)", credits: 3, total: 150 },
                { code: "TL3012", name: "Systematic Pathology", credits: 3, total: 150 },
                { code: "THS3011", name: "Infection Control", credits: 2, total: 100 },
                { code: "UN7", name: "Innovation & Entrepreneurship", credits: 2, total: 100 }
            ],
            "Third Level - 2nd Semester": [
                { code: "TL3113", name: "Biochemistry (2)", credits: 4, total: 200 },
                { code: "TL3114", name: "Basic Immunology", credits: 3, total: 150 },
                { code: "TL3115", name: "Quality Management (1)", credits: 4, total: 200 },
                { code: "TL3116", name: "Lab Instrumentation (2)", credits: 4, total: 200 },
                { code: "ETHS2", name: "Elective (2)", credits: 1, total: 50 }
            ],
            "Fourth Level - 1st Semester": [
                { code: "TL4017", name: "Biochemistry (3)", credits: 3, total: 150 },
                { code: "TL4018", name: "Virology & Mycology", credits: 3, total: 150 },
                { code: "TL4019", name: "Hematology (2)", credits: 4, total: 200 },
                { code: "TL4020", name: "Blood Banking", credits: 4, total: 200 },
                { code: "ETHS3", name: "Elective (3)", credits: 1, total: 50 }
            ],
            "Fourth Level - 2nd Semester": [
                { code: "TL4121", name: "Immunology & Serology", credits: 4, total: 200 },
                { code: "TL4122", name: "Age & Pregnancy Investigation", credits: 4, total: 200 },
                { code: "TL4123", name: "Quality Management (2)", credits: 4, total: 150 },
                { code: "TL4124", name: "Forensic Chemistry & Toxicology", credits: 4, total: 200 },
                { code: "ETHS4", name: "Elective (4)", credits: 1, total: 50 }
            ]
        };

        // ========== HELPER FUNCTIONS ==========
        function getLetterGrade(percentage) {
            for (const [grade, range] of Object.entries(gpaScale)) {
                if (percentage >= range.min && percentage <= range.max) {
                    return grade;
                }
            }
            return 'F';
        }

        function getGradePoints(percentage) {
            const grade = getLetterGrade(percentage);
            return gpaScale[grade].points;
        }

        function calculateSemesterGPA(semesterName) {
            const courses = curriculum[semesterName];
            let totalPoints = 0;
            let totalCredits = 0;
            let totalPercentage = 0;
            let courseCount = 0;

            courses.forEach(course => {
                const key = `${semesterName}_${course.code}`;
                const grade = userGrades[key];
                
                if (grade !== undefined && grade !== null && grade !== '') {
                    const percentage = parseFloat(grade);
                    if (!isNaN(percentage) && percentage >= 0 && percentage <= 100) {
                        const points = getGradePoints(percentage);
                        totalPoints += points * course.credits;
                        totalCredits += course.credits;
                        totalPercentage += percentage;
                        courseCount++;
                    }
                }
            });

            if (totalCredits === 0) return { gpa: 0, credits: 0, percentage: 0, courses: 0 };

            return {
                gpa: totalPoints / totalCredits,
                credits: totalCredits,
                percentage: totalPercentage / courseCount,
                courses: courseCount
            };
        }

        function calculateOverallGPA() {
            let totalPoints = 0;
            let totalCredits = 0;
            let totalPercentage = 0;
            let totalCourses = 0;

            Object.keys(curriculum).forEach(semesterName => {
                const semesterData = calculateSemesterGPA(semesterName);
                totalPoints += semesterData.gpa * semesterData.credits;
                totalCredits += semesterData.credits;
                totalPercentage += semesterData.percentage * semesterData.courses;
                totalCourses += semesterData.courses;
            });

            const cgpa = totalCredits > 0 ? totalPoints / totalCredits : 0;
            const avgPercentage = totalCourses > 0 ? totalPercentage / totalCourses : 0;

            document.getElementById('cumulativeGPA').textContent = cgpa.toFixed(decimalPrecision);
            document.getElementById('totalCredits').textContent = totalCredits;
            document.getElementById('avgPercentage').textContent = avgPercentage.toFixed(1) + '%';
            document.getElementById('totalCourses').textContent = totalCourses;
            document.getElementById('overallGrade').textContent = getLetterGrade(avgPercentage);

            // Apply sparkle effect
            const gradeElement = document.getElementById('overallGrade');
            const letterGrade = getLetterGrade(avgPercentage);
            
            gradeElement.style.animation = 'none';
            setTimeout(() => {
                if (letterGrade.startsWith('A')) {
                    gradeElement.style.animation = 'sparkle-blue 1.5s infinite';
                } else if (letterGrade.startsWith('F') || letterGrade.startsWith('D')) {
                    gradeElement.style.animation = 'sparkle-red 1.5s infinite';
                }
            }, 10);
        }

        // ========== SMART IMPORT FUNCTION ==========
        function smartImport() {
            const pasteText = document.getElementById('pasteArea').value;
            
            if (!pasteText.trim()) {
                showNotification(currentLang === 'ar' ? '⚠️ الرجاء لصق النص أولاً' : '⚠️ Please paste text first');
                return;
            }

            let importCount = 0;
            const lines = pasteText.split('\n');
            
            // Extract grades from pasted text
            Object.keys(curriculum).forEach(semesterName => {
                curriculum[semesterName].forEach(course => {
                    // Try to find the course code and extract the grade
                    const codePattern = new RegExp(course.code + '[\\s\\S]*?(\\d+\\.?\\d*)\\s*(?:\\/|من|out of|\\s)\\s*' + course.total, 'i');
                    const match = pasteText.match(codePattern);
                    
                    if (match && match[1]) {
                        const score = parseFloat(match[1]);
                        const percentage = (score / course.total) * 100;
                        
                        if (percentage >= 0 && percentage <= 100) {
                            const key = `${semesterName}_${course.code}`;
                            userGrades[key] = percentage.toFixed(2);
                            importCount++;
                        }
                    }
                });
            });

            if (importCount > 0) {
                saveGrades();
                renderSemesters();
                calculateOverallGPA();
                updateCharts();
                
                if (typeof confetti !== 'undefined') {
                    confetti({
                        particleCount: 200,
                        spread: 100,
                        origin: { y: 0.6 }
                    });
                }
                
                showNotification(
                    currentLang === 'ar' 
                        ? `✅ تم استيراد ${importCount} درجة بنجاح!` 
                        : `✅ Successfully imported ${importCount} grades!`
                );
            } else {
                showNotification(
                    currentLang === 'ar' 
                        ? '❌ لم يتم العثور على أي درجات' 
                        : '❌ No grades found'
                );
            }
        }

        // ========== RENDER FUNCTIONS ==========
        function renderSemesters() {
            const container = document.getElementById('semestersContainer');
            container.innerHTML = '';

            Object.keys(curriculum).forEach((semesterName, index) => {
                const semesterData = calculateSemesterGPA(semesterName);
                
                const accordion = document.createElement('div');
                accordion.className = 'semester-accordion';
                accordion.style.animationDelay = `${index * 0.1}s`;

                const header = document.createElement('div');
                header.className = 'semester-header';
                header.onclick = () => toggleSemester(accordion);

                const headerInfo = document.createElement('div');
                headerInfo.className = 'semester-header-info';
                
                const semesterNameEl = document.createElement('div');
                semesterNameEl.className = 'semester-name';
                semesterNameEl.textContent = semesterName;
                
                const statsInline = document.createElement('div');
                statsInline.className = 'semester-stats-inline';
                
                // GPA stat
                const gpaStat = document.createElement('div');
                gpaStat.className = 'semester-stat-inline';
                gpaStat.innerHTML = `
                    <div class="semester-stat-inline-label">GPA</div>
                    <div class="semester-stat-inline-value">${semesterData.gpa.toFixed(decimalPrecision)}</div>
                `;
                
                // Percentage stat
                const percentStat = document.createElement('div');
                percentStat.className = 'semester-stat-inline';
                percentStat.innerHTML = `
                    <div class="semester-stat-inline-label">%</div>
                    <div class="semester-stat-inline-value">${semesterData.percentage.toFixed(1)}%</div>
                `;
                
                // Credits stat
                const creditsStat = document.createElement('div');
                creditsStat.className = 'semester-stat-inline';
                creditsStat.innerHTML = `
                    <div class="semester-stat-inline-label">${currentLang === 'ar' ? 'ساعات' : 'Hrs'}</div>
                    <div class="semester-stat-inline-value">${semesterData.credits}</div>
                `;
                
                statsInline.appendChild(gpaStat);
                statsInline.appendChild(percentStat);
                statsInline.appendChild(creditsStat);
                
                headerInfo.appendChild(semesterNameEl);
                headerInfo.appendChild(statsInline);
                
                const toggle = document.createElement('div');
                toggle.className = 'semester-toggle';
                toggle.textContent = '▼';

                header.appendChild(headerInfo);
                header.appendChild(toggle);

                const content = document.createElement('div');
                content.className = 'semester-content';

                const courseGrid = document.createElement('div');
                courseGrid.className = 'course-grid';

                curriculum[semesterName].forEach(course => {
                    const card = document.createElement('div');
                    card.className = 'course-card';

                    const key = `${semesterName}_${course.code}`;
                    const currentGrade = userGrades[key] || '';

                    card.innerHTML = `
                        <div class="course-name">${course.code} - ${course.name}</div>
                        <div class="course-details">
                            <div>${currentLang === 'ar' ? 'ساعات' : 'Credits'}: ${course.credits}</div>
                            <div>${currentLang === 'ar' ? 'إجمالي' : 'Total'}: ${course.total}</div>
                        </div>
                        <div class="grade-input-group">
                            <label class="grade-input-label">${currentLang === 'ar' ? 'النسبة المئوية (%)' : 'Percentage (%)'}</label>
                            <input 
                                type="number" 
                                class="grade-input" 
                                min="0" 
                                max="100" 
                                step="0.01"
                                value="${currentGrade}"
                                placeholder="0-100"
                                onchange="updateGrade('${key}', this.value)"
                            >
                        </div>
                    `;

                    courseGrid.appendChild(card);
                });

                content.appendChild(courseGrid);
                accordion.appendChild(header);
                accordion.appendChild(content);
                container.appendChild(accordion);
            });
        }

        function toggleSemester(accordion) {
            accordion.classList.toggle('active');
        }

        function updateGrade(key, value) {
            const percentage = parseFloat(value);
            
            if (value === '' || value === null) {
                delete userGrades[key];
            } else if (!isNaN(percentage) && percentage >= 0 && percentage <= 100) {
                userGrades[key] = percentage;
            } else {
                showNotification(currentLang === 'ar' ? '⚠️ قيمة غير صالحة' : '⚠️ Invalid value');
                return;
            }

            saveGrades();
            calculateOverallGPA();
            renderSemesters();
            updateCharts();
        }

        // ========== CHARTS ==========
        function updateCharts() {
            updateGPAProgressChart();
            updateGradeDistributionChart();
        }

        function updateGPAProgressChart() {
            const ctx = document.getElementById('gpaProgressChart');
            
            const labels = [];
            const data = [];
            
            Object.keys(curriculum).forEach(semesterName => {
                const semesterData = calculateSemesterGPA(semesterName);
                if (semesterData.courses > 0) {
                    labels.push(semesterName.replace(' - ', '\n'));
                    data.push(semesterData.gpa.toFixed(decimalPrecision));
                }
            });

            if (gpaProgressChart) {
                gpaProgressChart.destroy();
            }

            gpaProgressChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: labels,
                    datasets: [{
                        label: 'Semester GPA',
                        data: data,
                        borderColor: '#3b82f6',
                        backgroundColor: 'rgba(59, 130, 246, 0.1)',
                        borderWidth: 3,
                        fill: true,
                        tension: 0.4,
                        pointRadius: 5,
                        pointHoverRadius: 8
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: true,
                            labels: { color: getComputedStyle(document.body).getPropertyValue('--text-primary') }
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            max: 4.0,
                            ticks: { color: getComputedStyle(document.body).getPropertyValue('--text-secondary') },
                            grid: { color: getComputedStyle(document.body).getPropertyValue('--border') }
                        },
                        x: {
                            ticks: { color: getComputedStyle(document.body).getPropertyValue('--text-secondary') },
                            grid: { color: getComputedStyle(document.body).getPropertyValue('--border') }
                        }
                    }
                }
            });
        }

        function updateGradeDistributionChart() {
            const ctx = document.getElementById('gradeDistributionChart');
            
            const distribution = {};
            Object.keys(gpaScale).forEach(grade => distribution[grade] = 0);

            Object.keys(curriculum).forEach(semesterName => {
                curriculum[semesterName].forEach(course => {
                    const key = `${semesterName}_${course.code}`;
                    const grade = userGrades[key];
                    
                    if (grade !== undefined && grade !== null && grade !== '') {
                        const percentage = parseFloat(grade);
                        if (!isNaN(percentage)) {
                            const letterGrade = getLetterGrade(percentage);
                            distribution[letterGrade]++;
                        }
                    }
                });
            });

            if (gradeDistributionChart) {
                gradeDistributionChart.destroy();
            }

            gradeDistributionChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: Object.keys(distribution),
                    datasets: [{
                        label: 'Number of Courses',
                        data: Object.values(distribution),
                        backgroundColor: [
                            '#10b981', '#10b981', '#10b981',
                            '#3b82f6', '#3b82f6', '#3b82f6',
                            '#f59e0b', '#f59e0b', '#f59e0b',
                            '#ef4444', '#ef4444', '#ef4444'
                        ],
                        borderWidth: 0
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: true,
                            labels: { color: getComputedStyle(document.body).getPropertyValue('--text-primary') }
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            ticks: { 
                                color: getComputedStyle(document.body).getPropertyValue('--text-secondary'),
                                stepSize: 1
                            },
                            grid: { color: getComputedStyle(document.body).getPropertyValue('--border') }
                        },
                        x: {
                            ticks: { color: getComputedStyle(document.body).getPropertyValue('--text-secondary') },
                            grid: { color: getComputedStyle(document.body).getPropertyValue('--border') }
                        }
                    }
                }
            });
        }

        function downloadChart(chartId) {
            const canvas = document.getElementById(chartId);
            const url = canvas.toDataURL('image/png');
            const link = document.createElement('a');
            link.download = `${chartId}_${new Date().toISOString().split('T')[0]}.png`;
            link.href = url;
            link.click();
            showNotification('✅ Chart downloaded!');
        }

        // ========== UI FUNCTIONS ==========
        function toggleMenu() {
            document.querySelector('.side-menu').classList.toggle('active');
            document.querySelector('.menu-overlay').classList.toggle('active');
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
            
            document.querySelectorAll('.lang-btn-nav').forEach(btn => {
                btn.classList.remove('active');
            });
            event.target.classList.add('active');
            
            updateLanguage();
            renderSemesters();
            updateCharts();
        }

        function updateLanguage() {
            const translations = {
                en: {
                    madeBy: 'Made by',
                    devHelper: 'Developer Helper',
                    cumulativeGPA: 'CUMULATIVE GPA',
                    totalCredits: 'Total Credits',
                    grade: 'Grade',
                    avgPercentage: 'Avg %',
                    totalCourses: 'Total Courses',
                    pasteTitle: '📋 PASTE YOUR GPA PAGE BY 1 CLICK',
                    pasteSubtitle: 'Simply paste your GPA page text here and it will auto-fill all your grades!',
                    pasteBtn: '🚀 Auto-Fill Grades',
                    gpaProgress: '📈 GPA Progress',
                    gradeDistribution: '📊 Grade Distribution',
                    downloadGPA: 'DOWNLOAD GPA PROGRESS',
                    semesters: '📚 Semesters',
                    menu: 'Menu',
                    profile: 'Profile',
                    settings: 'Settings',
                    shareGPA: 'Share GPA',
                    clearData: 'Clear All Data',
                    about: 'About',
                    aboutText: 'This is a free GPA calculator website designed to help HNU Medical Laboratory students calculate and track their academic performance. Please note that this calculator provides estimates and is not an official representation of your actual GPA from the university.',
                    credits: 'Credits',
                    developer: 'Developer',
                    name: 'Name',
                    studentID: 'Student ID',
                    email: 'Email',
                    saveProfile: 'Save Profile',
                    theme: 'Theme',
                    decimalPrecision: 'Decimal Precision',
                    saveSettings: 'Save Settings'
                },
                ar: {
                    madeBy: 'صُنع بواسطة',
                    devHelper: 'مساعد المطور',
                    cumulativeGPA: 'المعدل التراكمي',
                    totalCredits: 'إجمالي الساعات',
                    grade: 'التقدير',
                    avgPercentage: 'متوسط %',
                    totalCourses: 'إجمالي المقررات',
                    pasteTitle: '📋 الصق صفحة المعدل بنقرة واحدة',
                    pasteSubtitle: 'ما عليك سوى لصق نص صفحة المعدل هنا وسيتم ملء جميع الدرجات تلقائيًا!',
                    pasteBtn: '🚀 تعبئة تلقائية',
                    gpaProgress: '📈 تقدم المعدل',
                    gradeDistribution: '📊 توزيع الدرجات',
                    downloadGPA: 'تحميل تقرير المعدل',
                    semesters: '📚 الفصول الدراسية',
                    menu: 'القائمة',
                    profile: 'الملف الشخصي',
                    settings: 'الإعدادات',
                    shareGPA: 'مشاركة المعدل',
                    clearData: 'مسح جميع البيانات',
                    about: 'حول',
                    aboutText: 'هذا موقع مجاني لحساب المعدل التراكمي مصمم لمساعدة طلاب المختبرات الطبية بجامعة حائل في حساب وتتبع أدائهم الأكاديمي. يرجى ملاحظة أن هذه الآلة الحاسبة توفر تقديرات وليست تمثيلاً رسميًا لمعدلك الفعلي من الجامعة.',
                    credits: 'الفضل',
                    developer: 'المطور',
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
                    if (elem.tagName === 'INPUT' || elem.tagName === 'TEXTAREA') {
                        elem.placeholder = translations[currentLang][key];
                    } else {
                        elem.textContent = translations[currentLang][key];
                    }
                }
            });
        }

        function openModal(id) {
            document.getElementById(id).classList.add('active');
            if (document.querySelector('.side-menu').classList.contains('active')) {
                toggleMenu();
            }
        }

        function closeModal(id) {
            document.getElementById(id).classList.remove('active');
        }

        function openAboutPage() {
            document.getElementById('aboutPage').classList.add('active');
            if (document.querySelector('.side-menu').classList.contains('active')) {
                toggleMenu();
            }
        }

        function closeAboutPage() {
            document.getElementById('aboutPage').classList.remove('active');
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
            renderSemesters();
            updateCharts();
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
