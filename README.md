<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=5.0, user-scalable=yes">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="mobile-web-app-capable" content="yes">
    <title>HNU Medical Analysis</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&family=Orbitron:wght@400;700;900&family=Cairo:wght@400;600;700;900&family=Poppins:wght@700;800;900&family=Rajdhani:wght@600;700&display=swap" rel="stylesheet">
    
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
    
    <style>
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
            --glow-blue: #60a5fa;
            --gold: #fbbf24;
            --red-sparkle: #ff1744;
            --cyan: #06b6d4;
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
            --glow-blue: #3b82f6;
            --red-sparkle: #ff1744;
            --cyan: #0891b2;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        html {
            -webkit-text-size-adjust: 100%;
            text-size-adjust: 100%;
            width: 100%;
            overflow-x: hidden;
            scroll-behavior: smooth;
            font-size: 16px;
        }

        @media (max-width: 768px) {
            html {
                font-size: 14px;
            }
        }

        @media (max-width: 480px) {
            html {
                font-size: 13px;
            }
        }

        body {
            font-family: 'Rajdhani', 'Inter', sans-serif;
            background: var(--bg-primary);
            color: var(--text-primary);
            min-height: 100vh;
            transition: background 0.3s, color 0.3s;
            width: 100%;
            overflow-x: hidden;
            font-weight: 700;
        }

        body[dir="rtl"] {
            font-family: 'Cairo', sans-serif;
        }

        /* ========== TOP NAVIGATION BAR ========== */
        .top-nav {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            height: 60px;
            background: var(--bg-card);
            border-bottom: 2px solid var(--border);
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 0 0.75rem;
            z-index: 1000;
            box-shadow: 0 4px 12px var(--shadow);
        }

        @media (min-width: 768px) {
            .top-nav {
                height: 70px;
                padding: 0 1.5rem;
            }
        }

        .greeting {
            font-size: 0.75rem;
            font-weight: 600;
            color: var(--text-secondary);
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
            max-width: 120px;
        }

        @media (min-width: 480px) {
            .greeting {
                font-size: 0.85rem;
                max-width: 200px;
            }
        }

        @media (min-width: 768px) {
            .greeting {
                font-size: 0.9rem;
            }
        }

        .language-switcher {
            display: flex;
            gap: 0.25rem;
            background: var(--bg-secondary);
            border: 2px solid var(--border);
            border-radius: 10px;
            padding: 0.25rem;
        }

        @media (min-width: 480px) {
            .language-switcher {
                gap: 0.5rem;
                padding: 0.4rem;
                border-radius: 12px;
            }
        }

        .lang-btn {
            background: transparent;
            border: 2px solid transparent;
            border-radius: 6px;
            padding: 0.3rem 0.5rem;
            cursor: pointer;
            font-size: 0.7rem;
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 0.25rem;
            color: var(--text-secondary);
            transition: all 0.3s;
            min-width: 44px;
            min-height: 36px;
            justify-content: center;
        }

        @media (min-width: 480px) {
            .lang-btn {
                font-size: 0.8rem;
                padding: 0.4rem 0.7rem;
                border-radius: 8px;
                gap: 0.3rem;
                min-height: 40px;
            }
        }

        @media (min-width: 768px) {
            .lang-btn {
                font-size: 0.85rem;
            }
        }

        .lang-btn:hover {
            background: var(--bg-card);
            color: var(--text-primary);
        }

        .lang-btn.active {
            background: var(--accent);
            color: white;
            border-color: var(--accent);
        }

        .flag {
            width: 16px;
            height: 12px;
        }

        @media (min-width: 480px) {
            .flag {
                width: 18px;
                height: 13px;
            }
        }

        .right-controls {
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        @media (min-width: 480px) {
            .right-controls {
                gap: 1rem;
            }
        }

        .theme-toggle {
            background: var(--accent);
            border: none;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            cursor: pointer;
            font-size: 1.1rem;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 4px 12px var(--shadow);
            transition: transform 0.2s;
            flex-shrink: 0;
        }

        @media (min-width: 480px) {
            .theme-toggle {
                width: 45px;
                height: 45px;
                font-size: 1.3rem;
            }
        }

        .theme-toggle:active {
            transform: scale(0.95);
        }

        @media (hover: hover) {
            .theme-toggle:hover {
                transform: scale(1.1) rotate(20deg);
            }
        }

        .menu-toggle {
            background: var(--accent);
            border: none;
            border-radius: 10px;
            width: 40px;
            height: 40px;
            cursor: pointer;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: 4px;
            box-shadow: 0 4px 12px var(--shadow);
            transition: all 0.3s;
            flex-shrink: 0;
        }

        @media (min-width: 480px) {
            .menu-toggle {
                width: 45px;
                height: 45px;
                border-radius: 12px;
                gap: 5px;
            }
        }

        .menu-toggle:active {
            transform: scale(0.95);
        }

        @media (hover: hover) {
            .menu-toggle:hover {
                transform: scale(1.05);
                background: var(--accent-hover);
            }
        }

        .menu-toggle span {
            width: 20px;
            height: 2.5px;
            background: white;
            border-radius: 2px;
            transition: all 0.3s;
        }

        @media (min-width: 480px) {
            .menu-toggle span {
                width: 24px;
                height: 3px;
            }
        }

        .menu-toggle.active span:nth-child(1) {
            transform: rotate(45deg) translate(6px, 6px);
        }

        .menu-toggle.active span:nth-child(2) {
            opacity: 0;
        }

        .menu-toggle.active span:nth-child(3) {
            transform: rotate(-45deg) translate(6px, -6px);
        }

        @media (min-width: 480px) {
            .menu-toggle.active span:nth-child(1) {
                transform: rotate(45deg) translate(7px, 7px);
            }

            .menu-toggle.active span:nth-child(3) {
                transform: rotate(-45deg) translate(7px, -7px);
            }
        }

        /* ========== SIDE MENU ========== */
        .side-menu {
            position: fixed;
            top: 60px;
            right: -100%;
            width: 85%;
            max-width: 320px;
            height: calc(100vh - 60px);
            background: var(--bg-card);
            border-left: 2px solid var(--border);
            box-shadow: -4px 0 20px var(--shadow);
            transition: right 0.4s cubic-bezier(0.68, -0.55, 0.265, 1.55);
            z-index: 999;
            overflow-y: auto;
            -webkit-overflow-scrolling: touch;
        }

        @media (min-width: 768px) {
            .side-menu {
                top: 70px;
                height: calc(100vh - 70px);
                width: 300px;
                max-width: 300px;
            }
        }

        .side-menu.open {
            right: 0;
        }

        body[dir="rtl"] .side-menu {
            left: -100%;
            right: auto;
            border-left: none;
            border-right: 2px solid var(--border);
        }

        body[dir="rtl"] .side-menu.open {
            left: 0;
        }

        .menu-section {
            padding: 1rem;
            border-bottom: 1px solid var(--border);
        }

        @media (min-width: 480px) {
            .menu-section {
                padding: 1.5rem;
            }
        }

        .menu-section h3 {
            font-size: 1rem;
            margin-bottom: 1rem;
            color: var(--accent);
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        @media (min-width: 480px) {
            .menu-section h3 {
                font-size: 1.1rem;
            }
        }

        @media (min-width: 768px) {
            .menu-section h3 {
                font-size: 1.2rem;
            }
        }

        .menu-item {
            background: var(--bg-secondary);
            border: 2px solid var(--border);
            border-radius: 10px;
            padding: 0.8rem;
            margin-bottom: 0.7rem;
            cursor: pointer;
            font-weight: 700;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: space-between;
            min-height: 48px;
        }

        @media (min-width: 480px) {
            .menu-item {
                border-radius: 12px;
                padding: 0.9rem;
            }
        }

        .menu-item:active {
            transform: scale(0.98);
        }

        @media (hover: hover) {
            .menu-item:hover {
                background: var(--accent);
                color: white;
                transform: translateX(-5px);
                box-shadow: 0 4px 12px var(--glow-blue);
            }

            body[dir="rtl"] .menu-item:hover {
                transform: translateX(5px);
            }
        }

        /* ========== CONTAINER ========== */
        .container {
            max-width: 1400px;
            margin: 70px auto 20px;
            padding: 0 0.75rem;
        }

        @media (min-width: 480px) {
            .container {
                margin: 75px auto 20px;
                padding: 0 1rem;
            }
        }

        @media (min-width: 768px) {
            .container {
                margin: 90px auto 20px;
            }
        }

        /* ========== HERO SECTION ========== */
        .hero-section {
            background: linear-gradient(135deg, var(--accent) 0%, var(--accent-hover) 100%);
            border-radius: 16px;
            padding: 1.5rem 1rem;
            margin-bottom: 1.5rem;
            text-align: center;
            box-shadow: 0 10px 40px var(--shadow);
            position: relative;
            overflow: hidden;
        }

        @media (min-width: 480px) {
            .hero-section {
                border-radius: 18px;
                padding: 2rem 1.5rem;
            }
        }

        @media (min-width: 768px) {
            .hero-section {
                border-radius: 20px;
                padding: 2.5rem 2rem;
                margin-bottom: 2rem;
            }
        }

        .hero-section::before {
            content: '';
            position: absolute;
            top: -50%;
            right: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.1) 0%, transparent 70%);
            animation: rotate 20s linear infinite;
        }

        @keyframes rotate {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }

        .hero-section h1 {
            font-family: 'Orbitron', sans-serif;
            font-size: 1.75rem;
            color: white;
            margin-bottom: 0.6rem;
            text-shadow: 0 4px 20px rgba(0,0,0,0.3);
            position: relative;
            z-index: 1;
            line-height: 1.2;
        }

        @media (min-width: 480px) {
            .hero-section h1 {
                font-size: 2rem;
                margin-bottom: 0.7rem;
            }
        }

        @media (min-width: 768px) {
            .hero-section h1 {
                font-size: 2.5rem;
                margin-bottom: 0.8rem;
            }
        }

        .developer-credit {
            font-size: 0.95rem;
            color: #ff1744;
            font-weight: 900;
            text-shadow: 0 0 10px #ff1744, 0 0 20px #ff1744, 0 0 30px #ff1744;
            animation: sparkle 2s ease-in-out infinite;
            position: relative;
            z-index: 1;
            letter-spacing: 0.5px;
        }

        @media (min-width: 480px) {
            .developer-credit {
                font-size: 1.1rem;
                letter-spacing: 0.75px;
            }
        }

        @media (min-width: 768px) {
            .developer-credit {
                font-size: 1.2rem;
                letter-spacing: 1px;
            }
        }

        @keyframes sparkle {
            0%, 100% {
                transform: translateY(0px);
                text-shadow: 0 0 10px #ff1744, 0 0 20px #ff1744, 0 0 30px #ff1744;
            }
            50% {
                transform: translateY(-3px);
                text-shadow: 0 0 15px #ff1744, 0 0 30px #ff1744, 0 0 45px #ff1744, 0 0 60px #ff1744;
            }
        }

        /* ========== STATS GRID ========== */
        .stats-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 1rem;
            margin-bottom: 1.5rem;
        }

        @media (min-width: 480px) {
            .stats-grid {
                grid-template-columns: repeat(2, 1fr);
            }
        }

        @media (min-width: 768px) {
            .stats-grid {
                grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
                gap: 1.5rem;
                margin-bottom: 2rem;
            }
        }

        .stat-card {
            background: var(--bg-card);
            border: 2px solid var(--border);
            border-radius: 12px;
            padding: 1.25rem;
            text-align: center;
            transition: all 0.3s;
            box-shadow: 0 4px 12px var(--shadow);
        }

        @media (min-width: 480px) {
            .stat-card {
                border-radius: 14px;
                padding: 1.5rem;
            }
        }

        @media (min-width: 768px) {
            .stat-card {
                border-radius: 16px;
                padding: 1.8rem;
            }
        }

        .stat-card:active {
            transform: scale(0.98);
        }

        @media (hover: hover) {
            .stat-card:hover {
                transform: translateY(-5px);
                border-color: var(--accent);
                box-shadow: 0 8px 24px var(--glow-blue);
            }
        }

        .stat-label {
            font-size: 0.75rem;
            color: var(--text-secondary);
            margin-bottom: 0.5rem;
            text-transform: uppercase;
            letter-spacing: 0.75px;
        }

        @media (min-width: 480px) {
            .stat-label {
                font-size: 0.85rem;
                letter-spacing: 0.85px;
            }
        }

        @media (min-width: 768px) {
            .stat-label {
                font-size: 0.9rem;
                letter-spacing: 1px;
            }
        }

        .stat-value {
            font-size: 2rem;
            font-weight: 900;
            color: var(--accent);
            text-shadow: 0 2px 10px var(--glow-blue);
            line-height: 1;
        }

        @media (min-width: 480px) {
            .stat-value {
                font-size: 2.25rem;
            }
        }

        @media (min-width: 768px) {
            .stat-value {
                font-size: 2.5rem;
            }
        }

        .stat-subtext {
            font-size: 0.85rem;
            color: var(--text-secondary);
            margin-top: 0.3rem;
        }

        /* ========== QUICK ACTIONS ========== */
        .quick-actions {
            display: grid;
            grid-template-columns: 1fr;
            gap: 0.75rem;
            margin-bottom: 1.5rem;
        }

        @media (min-width: 480px) {
            .quick-actions {
                grid-template-columns: repeat(2, 1fr);
                gap: 1rem;
            }
        }

        @media (min-width: 768px) {
            .quick-actions {
                grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
                margin-bottom: 2rem;
            }
        }

        .action-btn {
            background: var(--bg-card);
            border: 2px solid var(--border);
            border-radius: 12px;
            padding: 1rem;
            cursor: pointer;
            font-weight: 700;
            font-size: 0.9rem;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
            color: var(--text-primary);
            text-align: center;
            min-height: 56px;
        }

        @media (min-width: 480px) {
            .action-btn {
                font-size: 0.95rem;
                border-radius: 14px;
                padding: 1.2rem;
            }
        }

        .action-btn:active {
            transform: scale(0.97);
        }

        @media (hover: hover) {
            .action-btn:hover {
                background: var(--accent);
                color: white;
                transform: translateY(-3px);
                box-shadow: 0 8px 20px var(--glow-blue);
            }
        }
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.6rem;
            box-shadow: 0 4px 12px var(--shadow);
        }

        .action-btn:hover {
            background: var(--accent);
            color: white;
            transform: scale(1.05);
            box-shadow: 0 6px 20px var(--glow-blue);
        }

        .action-btn.import-special {
            background: linear-gradient(135deg, #ff4757 0%, #ff6348 100%);
            color: white;
            border: 2px solid #ff4757;
            font-size: 1rem;
            font-weight: 800;
            box-shadow: 0 4px 15px rgba(255, 71, 87, 0.4);
        }

        .action-btn.import-special:hover {
            background: linear-gradient(135deg, #ff6348 0%, #ff4757 100%);
            transform: scale(1.03);
            box-shadow: 0 6px 20px rgba(255, 71, 87, 0.5);
        }

        .action-btn.download {
            background: linear-gradient(135deg, var(--accent) 0%, var(--accent-hover) 100%);
            color: white;
            border-color: var(--accent);
        }

        .action-btn.download:hover {
            transform: scale(1.08);
            box-shadow: 0 8px 30px var(--glow-blue);
        }

        /* ========== SEMESTER CARDS ========== */
        .semester-section {
            margin-bottom: 2rem;
        }

        .semester-header {
            background: linear-gradient(135deg, var(--accent) 0%, var(--accent-hover) 100%);
            color: white;
            padding: 1.5rem;
            border-radius: 16px;
            font-size: 1.4rem;
            font-weight: 900;
            display: flex;
            align-items: center;
            justify-content: space-between;
            box-shadow: 0 4px 12px var(--shadow);
            cursor: pointer;
            transition: all 0.3s;
            margin-bottom: 0.5rem;
        }

        .semester-header:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 16px var(--shadow);
        }

        .semester-stats {
            display: flex;
            gap: 2rem;
            font-size: 0.9rem;
            align-items: center;
        }

        .semester-stat-item {
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .semester-stat-label {
            font-size: 0.7rem;
            opacity: 0.9;
            margin-bottom: 0.2rem;
        }

        .semester-stat-value {
            font-size: 1.1rem;
            font-weight: 900;
        }

        .toggle-icon {
            font-size: 1.5rem;
            transition: transform 0.3s;
        }

        .toggle-icon.collapsed {
            transform: rotate(-90deg);
        }

        .semester-body {
            background: var(--bg-card);
            border: 2px solid var(--border);
            border-radius: 16px;
            padding: 1.5rem;
            max-height: 5000px;
            overflow: hidden;
            transition: max-height 0.4s ease-out, opacity 0.3s, padding 0.3s;
            opacity: 1;
        }

        .semester-body.collapsed {
            max-height: 0;
            padding: 0 1.5rem;
            opacity: 0;
            border: none;
        }

        .course-row {
            background: var(--bg-secondary);
            border: 2px solid var(--border);
            border-radius: 12px;
            padding: 1.2rem;
            margin-bottom: 1rem;
            transition: all 0.3s;
        }

        .course-row:hover {
            border-color: var(--accent);
            transform: translateX(5px);
            box-shadow: 0 4px 16px var(--glow-blue);
        }

        .course-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1rem;
            flex-wrap: wrap;
            gap: 0.5rem;
        }

        .course-info {
            flex: 1;
        }

        .course-code {
            font-size: 1.1rem;
            font-weight: 900;
            color: var(--accent);
            margin-bottom: 0.2rem;
        }

        .course-name {
            font-size: 0.9rem;
            color: var(--text-secondary);
        }

        .course-meta {
            display: flex;
            gap: 1rem;
            font-size: 0.85rem;
            color: var(--text-secondary);
        }

        .marks-input-group {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 1rem;
            margin-bottom: 1rem;
        }

        .input-wrapper {
            position: relative;
        }

        .input-wrapper label {
            display: block;
            font-size: 0.8rem;
            color: var(--text-secondary);
            margin-bottom: 0.3rem;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .input-wrapper input {
            width: 100%;
            background: var(--bg-primary);
            border: 2px solid var(--border);
            border-radius: 10px;
            padding: 0.8rem;
            color: var(--text-primary);
            font-size: 1rem;
            font-weight: 700;
            transition: all 0.3s;
        }

        .input-wrapper input:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
        }

        .grade-display {
            background: var(--bg-primary);
            border: 2px solid var(--border);
            border-radius: 12px;
            padding: 1rem;
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 1rem;
            text-align: center;
        }

        .grade-item {
            padding: 0.5rem;
        }

        .grade-item label {
            display: block;
            font-size: 0.75rem;
            color: var(--text-secondary);
            margin-bottom: 0.2rem;
        }

        .grade-item strong {
            font-size: 1.2rem;
            color: var(--accent);
        }

        /* ========== CHARTS ========== */
        .chart-container {
            background: var(--bg-card);
            border: 2px solid var(--border);
            border-radius: 16px;
            padding: 2rem;
            margin-bottom: 2rem;
            box-shadow: 0 4px 12px var(--shadow);
        }

        .chart-container h3 {
            font-size: 1.3rem;
            color: var(--accent);
            margin-bottom: 1.5rem;
            text-align: center;
        }

        .chart-wrapper {
            position: relative;
            height: 300px;
        }

        /* ========== IMPORT MODAL ========== */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.8);
            z-index: 2000;
            align-items: center;
            justify-content: center;
            padding: 1rem;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: var(--bg-card);
            border: 2px solid var(--accent);
            border-radius: 20px;
            padding: 2rem;
            max-width: 600px;
            width: 100%;
            max-height: 90vh;
            overflow-y: auto;
            box-shadow: 0 20px 60px rgba(59, 130, 246, 0.3);
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
        }

        .modal-header h2 {
            font-size: 1.5rem;
            color: var(--accent);
        }

        .close-modal {
            background: var(--danger);
            border: none;
            border-radius: 50%;
            width: 35px;
            height: 35px;
            cursor: pointer;
            font-size: 1.2rem;
            color: white;
            transition: all 0.3s;
        }

        .close-modal:hover {
            transform: rotate(90deg) scale(1.1);
        }

        .import-textarea {
            width: 100%;
            min-height: 200px;
            background: var(--bg-primary);
            border: 2px solid var(--border);
            border-radius: 12px;
            padding: 1rem;
            color: var(--text-primary);
            font-family: monospace;
            font-size: 0.9rem;
            margin-bottom: 1rem;
            resize: vertical;
        }

        .import-textarea:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
        }

        .import-info {
            background: var(--bg-secondary);
            border: 2px solid var(--border);
            border-radius: 12px;
            padding: 1rem;
            margin-bottom: 1rem;
            font-size: 0.85rem;
            color: var(--text-secondary);
        }

        .import-btn {
            width: 100%;
            background: var(--accent);
            border: none;
            border-radius: 12px;
            padding: 1rem;
            color: white;
            font-size: 1rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s;
        }

        .import-btn:hover {
            background: var(--accent-hover);
            transform: scale(1.02);
            box-shadow: 0 6px 20px var(--glow-blue);
        }

        /* ========== PROFILE & SETTINGS FORMS ========== */
        .form-group {
            margin-bottom: 1.5rem;
        }

        .form-group label {
            display: block;
            font-size: 0.9rem;
            color: var(--text-secondary);
            margin-bottom: 0.5rem;
            font-weight: 600;
        }

        .form-group input,
        .form-group select {
            width: 100%;
            background: var(--bg-secondary);
            border: 2px solid var(--border);
            border-radius: 10px;
            padding: 0.9rem;
            color: var(--text-primary);
            font-size: 1rem;
            transition: all 0.3s;
        }

        .form-group input:focus,
        .form-group select:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
        }

        .save-btn {
            width: 100%;
            background: var(--accent);
            border: none;
            border-radius: 12px;
            padding: 1rem;
            color: white;
            font-size: 1.1rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s;
        }

        .save-btn:hover {
            background: var(--accent-hover);
            transform: scale(1.02);
            box-shadow: 0 6px 20px var(--glow-blue);
        }

        /* ========== NOTIFICATION ========== */
        .notification {
            position: fixed;
            top: 90px;
            right: 20px;
            background: var(--accent);
            color: white;
            padding: 1rem 1.5rem;
            border-radius: 12px;
            box-shadow: 0 8px 24px var(--shadow);
            font-weight: 700;
            transform: translateX(400px);
            transition: transform 0.4s;
            z-index: 3000;
        }

        .notification.show {
            transform: translateX(0);
        }

        /* ========== RESPONSIVE ========== */
        @media (max-width: 768px) {
            .container {
                padding: 0 0.5rem;
            }

            .hero-section h1 {
                font-size: 1.8rem;
            }

            .developer-credit {
                font-size: 1rem;
            }

            .stats-grid {
                grid-template-columns: 1fr;
            }

            .quick-actions {
                grid-template-columns: 1fr;
            }

            .marks-input-group {
                grid-template-columns: 1fr;
            }

            .grade-display {
                grid-template-columns: 1fr;
            }

            .chart-wrapper {
                height: 250px;
            }

            .semester-header {
                flex-direction: column;
                gap: 1rem;
                text-align: center;
            }

            .semester-stats {
                width: 100%;
                justify-content: space-around;
                gap: 1rem;
            }

            .semester-stat-item {
                font-size: 0.85rem;
            }
        }

        /* ========== UTILITY CLASSES ========== */
        .hidden {
            display: none !important;
        }

        .text-center {
            text-align: center;
        }

        .mb-1 { margin-bottom: 1rem; }
        .mb-2 { margin-bottom: 2rem; }
        .mt-1 { margin-top: 1rem; }
        .mt-2 { margin-top: 2rem; }
        
        
        /* ========== ADDITIONAL MOBILE RESPONSIVE STYLES ========== */
        
        /* Input fields - touch-friendly */
        input[type="number"],
        input[type="text"],
        input[type="email"],
        select {
            min-height: 48px !important;
            font-size: 16px !important;
        }

        /* Course cards responsive */
        .course-card {
            padding: 0.875rem !important;
        }

        @media (min-width: 480px) {
            .course-card {
                padding: 1rem !important;
            }
        }

        @media (min-width: 768px) {
            .course-card {
                padding: 1.2rem !important;
            }
        }

        /* Semester sections responsive */
        .semester-section {
            padding: 1rem !important;
            margin-bottom: 1.25rem !important;
            border-radius: 12px !important;
        }

        @media (min-width: 480px) {
            .semester-section {
                padding: 1.25rem !important;
                border-radius: 14px !important;
            }
        }

        @media (min-width: 768px) {
            .semester-section {
                padding: 1.5rem !important;
                border-radius: 16px !important;
                margin-bottom: 1.5rem !important;
            }
        }

        /* Semester headers responsive */
        .semester-header h2 {
            font-size: 1.25rem !important;
        }

        @media (min-width: 480px) {
            .semester-header h2 {
                font-size: 1.35rem !important;
            }
        }

        @media (min-width: 768px) {
            .semester-header h2 {
                font-size: 1.4rem !important;
            }
        }

        /* Semester GPA badge */
        .semester-gpa {
            font-size: 0.85rem !important;
            padding: 0.4rem 0.75rem !important;
        }

        @media (min-width: 480px) {
            .semester-gpa {
                font-size: 0.9rem !important;
                padding: 0.5rem 1rem !important;
            }
        }

        /* Charts responsive sizing */
        .chart-container {
            height: 250px !important;
        }

        @media (min-width: 480px) {
            .chart-container {
                height: 280px !important;
            }
        }

        @media (min-width: 768px) {
            .chart-container {
                height: 300px !important;
            }
        }

        /* Buttons responsive */
        button, .btn {
            min-height: 44px !important;
            font-size: 0.9rem !important;
            padding: 0.75rem 1rem !important;
        }

        @media (min-width: 480px) {
            button, .btn {
                min-height: 48px !important;
                font-size: 0.95rem !important;
                padding: 0.85rem 1.25rem !important;
            }
        }

        /* Form groups responsive */
        .form-group {
            margin-bottom: 0.875rem !important;
        }

        @media (min-width: 480px) {
            .form-group {
                margin-bottom: 1rem !important;
            }
        }

        .form-group label {
            font-size: 0.85rem !important;
            margin-bottom: 0.4rem !important;
        }

        @media (min-width: 480px) {
            .form-group label {
                font-size: 0.9rem !important;
                margin-bottom: 0.5rem !important;
            }
        }

        @media (min-width: 768px) {
            .form-group label {
                font-size: 0.95rem !important;
            }
        }

        /* Notification responsive */
        .notification {
            max-width: 90% !important;
            font-size: 0.85rem !important;
            padding: 0.875rem 1.25rem !important;
        }

        @media (min-width: 480px) {
            .notification {
                max-width: 400px !important;
                font-size: 0.9rem !important;
                padding: 1rem 1.5rem !important;
            }
        }

        @media (min-width: 768px) {
            .notification {
                font-size: 0.95rem !important;
                padding: 1rem 2rem !important;
            }
        }

        /* Menu overlay */
        .menu-overlay {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.5);
            z-index: 998;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.3s;
        }

        .menu-overlay.active {
            opacity: 1;
            pointer-events: all;
        }

        /* Prevent double-tap zoom on iOS */
        * {
            touch-action: manipulation;
        }

        /* Better scrolling on mobile */
        .side-menu {
            -webkit-overflow-scrolling: touch;
        }

        /* Course name truncation on very small screens */
        @media (max-width: 360px) {
            .course-name {
                font-size: 0.8rem !important;
                line-height: 1.3;
            }
            
            .course-code {
                font-size: 0.85rem !important;
            }
        }

        /* Improve touch targets */
        input, button, select, textarea {
            -webkit-appearance: none;
            appearance: none;
        }

        /* Fix iOS input zoom */
        @media screen and (max-width: 767px) {
            input[type="number"]:focus,
            input[type="text"]:focus,
            input[type="email"]:focus,
            select:focus,
            textarea:focus {
                font-size: 16px !important;
            }
        }
    </style>
</head>
<body>
    <!-- Menu Overlay -->
    <div class="menu-overlay" id="menuOverlay" onclick="toggleMenu()"></div>
    
    <!-- TOP NAVIGATION -->
    <div class="top-nav">
        <div class="greeting">
            <span id="greetingText">🧬 Medical Analysis</span>
        </div>
        
        <div class="language-switcher">
            <button class="lang-btn active" onclick="switchLang('en')" data-lang="en">
                <span class="flag">🇺🇸</span> EN
            </button>
            <button class="lang-btn" onclick="switchLang('ar')" data-lang="ar">
                <span class="flag">🇪🇬</span> AR
            </button>
        </div>
        
        <div class="right-controls">
            <button class="theme-toggle" onclick="toggleTheme()">🌙</button>
            <button class="menu-toggle" onclick="toggleMenu()">
                <span></span>
                <span></span>
                <span></span>
            </button>
        </div>
    </div>

    <!-- SIDE MENU -->
    <div class="side-menu" id="sideMenu">
        <div class="menu-section">
            <h3>📊 QUICK ACTIONS</h3>
            <div class="menu-item" onclick="openImportModal()">
                📥 Paste Result Page
            </div>
            <div class="menu-item" onclick="clearAllData()">
                🗑️ Clear All Data
            </div>
            <div class="menu-item" onclick="downloadTranscript()">
                📥 Download Transcript
            </div>
        </div>

        <div class="menu-section" id="profileSection">
            <h3>👤 PROFILE</h3>
            <div class="form-group">
                <label>Full Name</label>
                <input type="text" id="userName" placeholder="Enter your name">
            </div>
            <div class="form-group">
                <label>Student ID</label>
                <input type="text" id="studentID" placeholder="Enter your ID">
            </div>
            <div class="form-group">
                <label>Email</label>
                <input type="email" id="userEmail" placeholder="Enter your email">
            </div>
            <button class="save-btn" onclick="saveProfile()">💾 SAVE PROFILE</button>
        </div>

        <div class="menu-section hidden" id="settingsSection">
            <h3>⚙️ SETTINGS</h3>
            <div class="form-group">
                <label>Theme</label>
                <select id="themeSelect">
                    <option value="dark">Dark Mode</option>
                    <option value="light">Light Mode</option>
                </select>
            </div>
            <div class="form-group">
                <label>Decimal Precision</label>
                <select id="decimalPrecision">
                    <option value="2">2 Decimals</option>
                    <option value="3">3 Decimals</option>
                    <option value="4">4 Decimals</option>
                </select>
            </div>
            <button class="save-btn" onclick="saveSettings()">💾 SAVE SETTINGS</button>
        </div>
    </div>

    <!-- IMPORT MODAL -->
    <div class="modal" id="importModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>📋 COPY HERE YOUR RESULT PAGE</h2>
                <button class="close-modal" onclick="closeImportModal()">×</button>
            </div>
            
            <div class="import-info">
                <strong>📋 Instructions:</strong><br>
                Paste your complete result page text here. The system will automatically detect all course codes and grades.<br><br>
                <strong>Supported Codes:</strong><br>
                UN101, THS101, THS102, TL201, and all Medical Analysis courses
            </div>
            
            <textarea class="import-textarea" id="importTextarea" placeholder="Paste your complete result page here..."></textarea>
            
            <button class="import-btn" onclick="processImport()">🚀 AUTO-DETECT & IMPORT</button>
        </div>
    </div>

    <!-- MAIN CONTAINER -->
    <div class="container">
        <!-- HERO SECTION -->
        <div class="hero-section">
            <h1>HNU GPA CALCULATOR</h1>
            <div class="developer-credit">Made by Mohand</div>
        </div>

        <!-- STATS GRID -->
        <div class="stats-grid">
            <div class="stat-card">
                <div class="stat-label">CUMULATIVE GPA</div>
                <div class="stat-value" id="cumulativeGPA">0.00</div>
                <div class="stat-subtext">Overall Performance</div>
            </div>
            <div class="stat-card">
                <div class="stat-label">OVERALL GRADE</div>
                <div class="stat-value" id="overallGrade">-</div>
                <div class="stat-subtext">Letter Grade</div>
            </div>
            <div class="stat-card">
                <div class="stat-label">TOTAL HOURS</div>
                <div class="stat-value" id="totalHours">0</div>
                <div class="stat-subtext">Credit Hours</div>
            </div>
            <div class="stat-card">
                <div class="stat-label">COURSES COMPLETED</div>
                <div class="stat-value" id="completedCourses">0</div>
                <div class="stat-subtext">Out of 41</div>
            </div>
        </div>

        <!-- QUICK ACTIONS -->
        <div class="quick-actions">
            <button class="action-btn import-special" onclick="openImportModal()">
                📋 COPY HERE YOUR RESULT PAGE
            </button>
            <button class="action-btn print" onclick="printTranscript()">
                🖨️ Print Transcript
            </button>
            <button class="action-btn" onclick="shareGPA()">
                📤 Share Results
            </button>
            <button class="action-btn" onclick="clearAllData()">
                🗑️ Clear All
            </button>
        </div>

        <!-- CHARTS -->
        <div class="chart-container">
            <h3>📊 GPA PROGRESSION BY SEMESTER</h3>
            <div class="chart-wrapper">
                <canvas id="gpaChart"></canvas>
            </div>
        </div>

        <div class="chart-container">
            <h3>📈 GRADE DISTRIBUTION</h3>
            <div class="chart-wrapper">
                <canvas id="gradeChart"></canvas>
            </div>
        </div>

        <!-- SEMESTERS CONTAINER -->
        <div id="semestersContainer"></div>
    </div>

    <!-- NOTIFICATION -->
    <div class="notification" id="notification"></div>

    <script>
        // ========== GLOBAL VARIABLES ==========
        let currentTheme = 'dark';
        let currentLang = 'en';
        let decimalPrecision = 2;
        let userGrades = {};
        let gpaChart = null;
        let gradeChart = null;

        // ========== MEDICAL LABORATORY PROGRAM DATABASE (41 Courses) ==========
        const courseDatabase = {
            // First Level - 1st Semester
            'UN101': { name: 'Academic Reading and Writing (1)', nameAr: 'القراءة والكتابة الأكاديمية (1)', hours: 2, total: 100, semester: 1 },
            'THS101': { name: 'Basic Physics', nameAr: 'الفيزياء الأساسية', hours: 2, total: 100, semester: 1 },
            'THS102': { name: 'Mathematics', nameAr: 'الرياضيات', hours: 2, total: 100, semester: 1 },
            'THS103': { name: 'Introduction to Electrical Engineering', nameAr: 'مقدمة في الهندسة الكهربائية', hours: 3, total: 150, semester: 1 },
            'UN102': { name: 'Computer Skills', nameAr: 'مهارات الحاسوب', hours: 2, total: 100, semester: 1 },
            'THS104': { name: 'Mechanics', nameAr: 'الميكانيكا', hours: 2, total: 100, semester: 1 },
            'UN103': { name: 'Critical Thinking', nameAr: 'التفكير النقدي', hours: 2, total: 100, semester: 1 },
            
            // First Level - 2nd Semester
            'THS115': { name: 'Electronic Circuits & Devices', nameAr: 'الدوائر والأجهزة الإلكترونية', hours: 3, total: 150, semester: 2 },
            'THS116': { name: 'General Anatomy & Histology', nameAr: 'التشريح وعلم الأنسجة العام', hours: 3, total: 150, semester: 2 },
            'THS117': { name: 'General Physiology', nameAr: 'علم وظائف الأعضاء العام', hours: 2, total: 100, semester: 2 },
            'THS118': { name: 'General Microbiology', nameAr: 'علم الأحياء الدقيقة العام', hours: 2, total: 100, semester: 2 },
            'THS119': { name: 'General Chemistry', nameAr: 'الكيمياء العامة', hours: 2, total: 100, semester: 2 },
            'UN114': { name: 'Academic Reading and Writing (2)', nameAr: 'القراءة والكتابة الأكاديمية (2)', hours: 2, total: 100, semester: 2 },
            'THS1110': { name: 'Professional Ethics', nameAr: 'أخلاقيات المهنة', hours: 1, total: 50, semester: 2 },
            
            // Second Level - 1st Semester
            'THS2010': { name: 'Mechatronics Engineering', nameAr: 'هندسة الميكاترونكس', hours: 2, total: 100, semester: 3 },
            'TL201': { name: 'Biochemistry (1)', nameAr: 'الكيمياء الحيوية (1)', hours: 4, total: 200, semester: 3 },
            'TL202': { name: 'Parasitology (1)', nameAr: 'علم الطفيليات (1)', hours: 2, total: 100, semester: 3 },
            'TL203': { name: 'Bacteriology', nameAr: 'علم البكتيريا', hours: 4, total: 200, semester: 3 },
            'TL204': { name: 'Histology for Lab Technologists', nameAr: 'علم الأنسجة لفنيي المختبرات', hours: 2, total: 100, semester: 3 },
            'UN5': { name: 'Foundation of Digital Technology', nameAr: 'أساسيات التكنولوجيا الرقمية', hours: 2, total: 100, semester: 3 },
            'UN6': { name: 'English Language', nameAr: 'اللغة الإنجليزية', hours: 2, total: 100, semester: 3 },
            
            // Second Level - 2nd Semester
            'TL215': { name: 'Molecular Biology', nameAr: 'البيولوجيا الجزيئية', hours: 4, total: 200, semester: 4 },
            'TL216': { name: 'Hematology (1)', nameAr: 'أمراض الدم (1)', hours: 4, total: 200, semester: 4 },
            'TL217': { name: 'Systematic Physiology', nameAr: 'علم وظائف الأعضاء المنهجي', hours: 4, total: 200, semester: 4 },
            'TL218': { name: 'General Biology', nameAr: 'علم الأحياء العام', hours: 3, total: 150, semester: 4 },
            'ETHS1': { name: 'Elective (1)', nameAr: 'اختياري (1)', hours: 1, total: 50, semester: 4 },
            
            // Third Level - 1st Semester
            'TL309': { name: 'Lab Instrumentation (1)', nameAr: 'أجهزة المختبر (1)', hours: 4, total: 200, semester: 5 },
            'TL3010': { name: 'Enzymology & Hormones', nameAr: 'علم الإنزيمات والهرمونات', hours: 4, total: 200, semester: 5 },
            'TL3011': { name: 'Parasitology (2)', nameAr: 'علم الطفيليات (2)', hours: 3, total: 150, semester: 5 },
            'TL3012': { name: 'Systematic Pathology', nameAr: 'علم الأمراض المنهجي', hours: 3, total: 150, semester: 5 },
            'THS3011': { name: 'Infection Control', nameAr: 'مكافحة العدوى', hours: 2, total: 100, semester: 5 },
            'UN7': { name: 'Innovation & Entrepreneurship', nameAr: 'الابتكار وريادة الأعمال', hours: 2, total: 100, semester: 5 },
            
            // Third Level - 2nd Semester
            'TL3113': { name: 'Biochemistry (2)', nameAr: 'الكيمياء الحيوية (2)', hours: 4, total: 200, semester: 6 },
            'TL3114': { name: 'Basic Immunology', nameAr: 'علم المناعة الأساسي', hours: 3, total: 150, semester: 6 },
            'TL3115': { name: 'Quality Management (1)', nameAr: 'إدارة الجودة (1)', hours: 4, total: 200, semester: 6 },
            'TL3116': { name: 'Lab Instrumentation (2)', nameAr: 'أجهزة المختبر (2)', hours: 4, total: 200, semester: 6 },
            'ETHS2': { name: 'Elective (2)', nameAr: 'اختياري (2)', hours: 1, total: 50, semester: 6 },
            
            // Fourth Level - 1st Semester
            'TL4017': { name: 'Biochemistry (3)', nameAr: 'الكيمياء الحيوية (3)', hours: 3, total: 150, semester: 7 },
            'TL4018': { name: 'Virology & Mycology', nameAr: 'علم الفيروسات والفطريات', hours: 3, total: 150, semester: 7 },
            'TL4019': { name: 'Hematology (2)', nameAr: 'أمراض الدم (2)', hours: 4, total: 200, semester: 7 },
            'TL4020': { name: 'Blood Banking', nameAr: 'بنك الدم', hours: 4, total: 200, semester: 7 },
            'ETHS3': { name: 'Elective (3)', nameAr: 'اختياري (3)', hours: 1, total: 50, semester: 7 }
        };

        const semesterLabels = {
            1: 'First Level - 1st Semester',
            2: 'First Level - 2nd Semester',
            3: 'Second Level - 1st Semester',
            4: 'Second Level - 2nd Semester',
            5: 'Third Level - 1st Semester',
            6: 'Third Level - 2nd Semester',
            7: 'Fourth Level - 1st Semester'
        };

        const semesterLabelsAr = {
            1: 'المستوى الأول - الفصل الأول',
            2: 'المستوى الأول - الفصل الثاني',
            3: 'المستوى الثاني - الفصل الأول',
            4: 'المستوى الثاني - الفصل الثاني',
            5: 'المستوى الثالث - الفصل الأول',
            6: 'المستوى الثالث - الفصل الثاني',
            7: 'المستوى الرابع - الفصل الأول'
        };

        // ========== HNU GRADING SYSTEM ==========
        function getGradeFromPercentage(percentage) {
            if (percentage >= 95) return { grade: 'A+', points: 4.0 };
            if (percentage >= 90) return { grade: 'A', points: 3.8 };
            if (percentage >= 85) return { grade: 'A-', points: 3.6 };
            if (percentage >= 82.5) return { grade: 'B+', points: 3.4 };
            if (percentage >= 77.5) return { grade: 'B', points: 3.2 };
            if (percentage >= 75) return { grade: 'B-', points: 3.0 };
            if (percentage >= 72.5) return { grade: 'C+', points: 2.8 };
            if (percentage >= 67.5) return { grade: 'C', points: 2.6 };
            if (percentage >= 65) return { grade: 'C-', points: 2.4 };
            if (percentage >= 62.5) return { grade: 'D+', points: 2.2 };
            if (percentage >= 60) return { grade: 'D', points: 2.0 };
            return { grade: 'F', points: 0.0 };
        }

        // ========== THEME TOGGLE ==========
        function toggleTheme() {
            if (currentTheme === 'dark') {
                document.body.setAttribute('data-theme', 'light');
                document.querySelector('.theme-toggle').textContent = '☀️';
                currentTheme = 'light';
            } else {
                document.body.removeAttribute('data-theme');
                document.querySelector('.theme-toggle').textContent = '🌙';
                currentTheme = 'dark';
            }
            localStorage.setItem('theme', currentTheme);
            updateCharts();
        }

        // ========== MENU TOGGLE ==========
        function toggleMenu() {
            const menu = document.getElementById('sideMenu');
            const toggle = document.querySelector('.menu-toggle');
            const overlay = document.getElementById('menuOverlay');
            menu.classList.toggle('open');
            toggle.classList.toggle('active');
            if (overlay) overlay.classList.toggle('active');
        }

        // ========== TRANSLATIONS ==========
        const translations = {
            en: {
                greeting: '🧬 Medical Analysis',
                heroTitle: 'HNU GPA CALCULATOR',
                madeBy: 'Made by Mohand',
                cumulativeGPA: 'CUMULATIVE GPA',
                overallGrade: 'OVERALL GRADE',
                totalHours: 'TOTAL HOURS',
                coursesCompleted: 'COURSES COMPLETED',
                overallPerformance: 'Overall Performance',
                letterGrade: 'Letter Grade',
                creditHours: 'Credit Hours',
                outOf: 'Out of 41',
                copyResultPage: '📋 COPY HERE YOUR RESULT PAGE',
                printTranscript: '🖨️ Print Transcript',
                shareResults: '📤 Share Results',
                clearAll: '🗑️ Clear All',
                gpaProgression: '📊 GPA PROGRESSION BY SEMESTER',
                gradeDistribution: '📈 GRADE DISTRIBUTION',
                quickActions: '📊 QUICK ACTIONS',
                pasteResult: '📥 Paste Result Page',
                clearData: '🗑️ Clear All Data',
                downloadTranscript: '📥 Download Transcript',
                profile: '👤 PROFILE',
                fullName: 'Full Name',
                studentID: 'Student ID',
                email: 'Email',
                saveProfile: '💾 SAVE PROFILE',
                settings: '⚙️ SETTINGS',
                theme: 'Theme',
                darkMode: 'Dark Mode',
                lightMode: 'Light Mode',
                decimalPrecision: 'Decimal Precision',
                saveSettings: '💾 SAVE SETTINGS',
                instructions: '📋 Instructions:',
                instructionsText: 'Paste your complete result page text here. The system will automatically detect all course codes and grades.',
                supportedCodes: '📋 Supported Codes:',
                codesText: 'UN101, THS101, THS102, TL201, and all Medical Analysis courses',
                autoDetect: '🚀 AUTO-DETECT & IMPORT',
                yourMarks: 'Your Marks',
                percentage: 'Percentage',
                grade: 'GRADE',
                gpaPoints: 'GPA POINTS',
                status: 'STATUS',
                graded: '✅ Graded',
                pending: '⏳ Pending',
                enterMarks: 'Enter marks',
                enterName: 'Enter your name',
                enterID: 'Enter your ID',
                enterEmail: 'Enter your email',
                hours: 'Hours',
                total: 'Total'
            },
            ar: {
                greeting: '🧬 التحليلات الطبية',
                heroTitle: 'حاسبة المعدل التراكمي',
                madeBy: 'صنع بواسطة مهند',
                cumulativeGPA: 'المعدل التراكمي',
                overallGrade: 'التقدير العام',
                totalHours: 'إجمالي الساعات',
                coursesCompleted: 'المقررات المكتملة',
                overallPerformance: 'الأداء العام',
                letterGrade: 'التقدير بالحروف',
                creditHours: 'الساعات المعتمدة',
                outOf: 'من أصل 41',
                copyResultPage: '📋 الصق هنا صفحة النتيجة',
                printTranscript: '🖨️ طباعة كشف الدرجات',
                shareResults: '📤 مشاركة النتائج',
                clearAll: '🗑️ مسح الكل',
                gpaProgression: '📊 تطور المعدل التراكمي حسب الفصول',
                gradeDistribution: '📈 توزيع الدرجات',
                quickActions: '📊 إجراءات سريعة',
                pasteResult: '📥 لصق صفحة النتيجة',
                clearData: '🗑️ مسح جميع البيانات',
                downloadTranscript: '📥 تحميل كشف الدرجات',
                profile: '👤 الملف الشخصي',
                fullName: 'الاسم الكامل',
                studentID: 'رقم الطالب',
                email: 'البريد الإلكتروني',
                saveProfile: '💾 حفظ الملف الشخصي',
                settings: '⚙️ الإعدادات',
                theme: 'المظهر',
                darkMode: 'الوضع الداكن',
                lightMode: 'الوضع الفاتح',
                decimalPrecision: 'دقة الأرقام العشرية',
                saveSettings: '💾 حفظ الإعدادات',
                instructions: '📋 التعليمات:',
                instructionsText: 'الصق نص صفحة النتيجة الكاملة هنا. سيقوم النظام تلقائيًا باكتشاف جميع رموز المقررات والدرجات.',
                supportedCodes: '📋 الرموز المدعومة:',
                codesText: 'UN101، THS101، THS102، TL201، وجميع مقررات برنامج المختبرات الطبية',
                autoDetect: '🚀 اكتشاف تلقائي واستيراد',
                yourMarks: 'درجتك',
                percentage: 'النسبة المئوية',
                grade: 'التقدير',
                gpaPoints: 'نقاط المعدل',
                status: 'الحالة',
                graded: '✅ مُقيّم',
                pending: '⏳ قيد الانتظار',
                enterMarks: 'أدخل الدرجات',
                enterName: 'أدخل اسمك',
                enterID: 'أدخل رقمك',
                enterEmail: 'أدخل بريدك الإلكتروني',
                hours: 'ساعات',
                total: 'المجموع'
            }
        };

        // ========== LANGUAGE SWITCH ==========
        function switchLang(lang) {
            currentLang = lang;
            document.querySelectorAll('.lang-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            document.querySelector(`[data-lang="${lang}"]`).classList.add('active');
            
            if (lang === 'ar') {
                document.body.setAttribute('dir', 'rtl');
            } else {
                document.body.removeAttribute('dir');
            }
            
            updateLanguage();
            localStorage.setItem('language', lang);
        }

        function updateLanguage() {
            const t = translations[currentLang];
            
            // Update all text elements
            document.getElementById('greetingText').textContent = t.greeting;
            document.querySelector('.hero-section h1').textContent = t.heroTitle;
            document.querySelector('.developer-credit').textContent = t.madeBy;
            
            // Stats
            document.querySelectorAll('.stat-label')[0].textContent = t.cumulativeGPA;
            document.querySelectorAll('.stat-label')[1].textContent = t.overallGrade;
            document.querySelectorAll('.stat-label')[2].textContent = t.totalHours;
            document.querySelectorAll('.stat-label')[3].textContent = t.coursesCompleted;
            
            document.querySelectorAll('.stat-subtext')[0].textContent = t.overallPerformance;
            document.querySelectorAll('.stat-subtext')[1].textContent = t.letterGrade;
            document.querySelectorAll('.stat-subtext')[2].textContent = t.creditHours;
            document.querySelectorAll('.stat-subtext')[3].textContent = t.outOf;
            
            // Buttons
            const actionBtns = document.querySelectorAll('.action-btn');
            actionBtns[0].innerHTML = t.copyResultPage;
            actionBtns[1].innerHTML = t.printTranscript;
            actionBtns[2].innerHTML = t.shareResults;
            actionBtns[3].innerHTML = t.clearAll;
            
            // Charts
            document.querySelectorAll('.chart-container h3')[0].textContent = t.gpaProgression;
            document.querySelectorAll('.chart-container h3')[1].textContent = t.gradeDistribution;
            
            // Menu
            document.querySelectorAll('.menu-section h3')[0].textContent = t.quickActions;
            const menuItems = document.querySelectorAll('.menu-item');
            menuItems[0].textContent = t.pasteResult;
            menuItems[1].textContent = t.clearData;
            menuItems[2].textContent = t.downloadTranscript;
            
            // Profile section
            document.querySelector('#profileSection h3').textContent = t.profile;
            const profileLabels = document.querySelectorAll('#profileSection label');
            profileLabels[0].textContent = t.fullName;
            profileLabels[1].textContent = t.studentID;
            profileLabels[2].textContent = t.email;
            
            const profileInputs = document.querySelectorAll('#profileSection input');
            profileInputs[0].placeholder = t.enterName;
            profileInputs[1].placeholder = t.enterID;
            profileInputs[2].placeholder = t.enterEmail;
            
            document.querySelector('#profileSection .save-btn').textContent = t.saveProfile;
            
            // Settings section
            document.querySelector('#settingsSection h3').textContent = t.settings;
            const settingsLabels = document.querySelectorAll('#settingsSection label');
            settingsLabels[0].textContent = t.theme;
            settingsLabels[1].textContent = t.decimalPrecision;
            
            document.querySelector('#settingsSection .save-btn').textContent = t.saveSettings;
            
            // Modal
            document.querySelector('.modal-header h2').textContent = t.copyResultPage;
            
            // Re-render semesters with new language
            renderSemesters();
        }

        // ========== IMPORT MODAL ==========
        function openImportModal() {
            document.getElementById('importModal').classList.add('active');
        }

        function closeImportModal() {
            document.getElementById('importModal').classList.remove('active');
        }

        function processImport() {
            const textarea = document.getElementById('importTextarea');
            const input = textarea.value.trim().toUpperCase();
            
            if (!input) {
                showNotification('❌ Please paste your result page!');
                return;
            }

            const lines = input.split('\n');
            let importedCount = 0;
            let updatedCount = 0;
            
            // Extract all course codes and their marks from the input
            Object.keys(courseDatabase).forEach(code => {
                // Look for the course code in the text
                for (let i = 0; i < lines.length; i++) {
                    const line = lines[i].toUpperCase();
                    if (line.includes(code)) {
                        // Check if this is a new course or update
                        if (userGrades[code] === undefined) {
                            userGrades[code] = null; // Initialize as null (course added but not graded)
                            importedCount++;
                        }
                        
                        // Try to extract marks - look for patterns like "85/100" or just numbers
                        // Match patterns like: "85/100", "85 /100", "85", etc.
                        const maxMarks = courseDatabase[code].total;
                        
                        // Try to find "number/total" pattern first
                        const fractionMatch = line.match(new RegExp(`(\\d+)\\s*\\/\\s*${maxMarks}`));
                        if (fractionMatch) {
                            const mark = parseInt(fractionMatch[1]);
                            if (mark <= maxMarks && mark >= 0) {
                                if (userGrades[code] !== mark) {
                                    userGrades[code] = mark;
                                    updatedCount++;
                                }
                                break;
                            }
                        }
                        
                        // If no fraction found, look for standalone numbers that make sense as marks
                        const numbers = line.match(/\d+/g);
                        if (numbers) {
                            for (let num of numbers) {
                                const mark = parseInt(num);
                                // Only accept marks that are reasonable (between 0 and maxMarks)
                                // Skip hours (typically 1-4) and the total itself
                                if (mark > 10 && mark <= maxMarks && mark !== maxMarks) {
                                    if (userGrades[code] !== mark) {
                                        userGrades[code] = mark;
                                        updatedCount++;
                                    }
                                    break;
                                }
                            }
                        }
                        break;
                    }
                }
            });

            if (importedCount > 0 || updatedCount > 0) {
                saveGrades();
                renderSemesters();
                calculateOverallGPA();
                updateCharts();
                
                let message = '';
                if (importedCount > 0 && updatedCount > 0) {
                    message = `✅ Imported ${importedCount} courses and updated ${updatedCount} grades!`;
                } else if (importedCount > 0) {
                    message = `✅ Successfully imported ${importedCount} courses!`;
                } else if (updatedCount > 0) {
                    message = `✅ Updated ${updatedCount} grades!`;
                }
                
                showNotification(message);
                triggerConfetti();
            } else {
                showNotification('⚠️ No valid course codes found in the text!');
            }

            closeImportModal();
            textarea.value = '';
        }

        // ========== RENDER SEMESTERS ==========
        function renderSemesters() {
            const container = document.getElementById('semestersContainer');
            container.innerHTML = '';

            const semesters = {};
            Object.entries(courseDatabase).forEach(([code, course]) => {
                if (!semesters[course.semester]) {
                    semesters[course.semester] = [];
                }
                semesters[course.semester].push({ code, ...course });
            });

            const labels = currentLang === 'ar' ? semesterLabelsAr : semesterLabels;
            const t = translations[currentLang];

            Object.keys(semesters).sort((a, b) => a - b).forEach(semNum => {
                const semesterDiv = document.createElement('div');
                semesterDiv.className = 'semester-section';
                
                const semesterGPA = calculateSemesterGPA(semesters[semNum]);
                
                // Calculate semester stats
                let totalHours = 0;
                let completedCourses = 0;
                let totalPercentage = 0;
                let coursesWithGrades = 0;
                
                semesters[semNum].forEach(course => {
                    const marks = userGrades[course.code];
                    if (marks != null && marks !== '') {
                        totalHours += course.hours;
                        completedCourses++;
                        const percentage = (marks / course.total) * 100;
                        totalPercentage += percentage;
                        coursesWithGrades++;
                    }
                });
                
                const avgPercentage = coursesWithGrades > 0 ? (totalPercentage / coursesWithGrades).toFixed(1) : '0.0';
                
                semesterDiv.innerHTML = `
                    <div class="semester-header" onclick="toggleSemester(${semNum})">
                        <span>${labels[semNum]}</span>
                        <div class="semester-stats">
                            <div class="semester-stat-item">
                                <div class="semester-stat-label">${currentLang === 'ar' ? 'المعدل' : 'GPA'}</div>
                                <div class="semester-stat-value">${semesterGPA.toFixed(decimalPrecision)}</div>
                            </div>
                            <div class="semester-stat-item">
                                <div class="semester-stat-label">${currentLang === 'ar' ? 'النسبة' : 'Avg %'}</div>
                                <div class="semester-stat-value">${avgPercentage}%</div>
                            </div>
                            <div class="semester-stat-item">
                                <div class="semester-stat-label">${currentLang === 'ar' ? 'الساعات' : 'Hours'}</div>
                                <div class="semester-stat-value">${totalHours}</div>
                            </div>
                            <span class="toggle-icon" id="toggle-${semNum}">▼</span>
                        </div>
                    </div>
                    <div class="semester-body" id="semester${semNum}">
                    </div>
                `;
                
                container.appendChild(semesterDiv);
                
                const semesterBody = document.getElementById(`semester${semNum}`);
                semesters[semNum].forEach(course => {
                    const courseRow = createCourseRow(course);
                    semesterBody.appendChild(courseRow);
                });
            });
        }

        function toggleSemester(semNum) {
            const body = document.getElementById(`semester${semNum}`);
            const icon = document.getElementById(`toggle-${semNum}`);
            
            body.classList.toggle('collapsed');
            icon.classList.toggle('collapsed');
        }

        function createCourseRow(course) {
            const div = document.createElement('div');
            div.className = 'course-row';
            
            const t = translations[currentLang];
            const courseName = currentLang === 'ar' ? course.nameAr : course.name;
            
            const marks = userGrades[course.code] || '';
            const percentage = marks ? (marks / course.total) * 100 : 0;
            const gradeInfo = marks ? getGradeFromPercentage(percentage) : { grade: '-', points: 0 };
            
            div.innerHTML = `
                <div class="course-header">
                    <div class="course-info">
                        <div class="course-code">${course.code}</div>
                        <div class="course-name">${courseName}</div>
                    </div>
                    <div class="course-meta">
                        <span>📚 ${course.hours} ${t.hours}</span>
                        <span>📊 ${t.total}: ${course.total}</span>
                    </div>
                </div>
                
                <div class="marks-input-group">
                    <div class="input-wrapper">
                        <label>${t.yourMarks}</label>
                        <input type="number" 
                               min="0" 
                               max="${course.total}" 
                               value="${marks}" 
                               placeholder="${t.enterMarks}"
                               onchange="updateGrade('${course.code}', this.value, ${course.total}, ${course.hours})">
                    </div>
                    <div class="input-wrapper">
                        <label>${t.percentage}</label>
                        <input type="text" 
                               value="${marks ? percentage.toFixed(2) + '%' : ''}" 
                               readonly 
                               style="background: var(--bg-card); cursor: not-allowed;">
                    </div>
                </div>
                
                <div class="grade-display">
                    <div class="grade-item">
                        <label>${t.grade}</label>
                        <strong id="grade-${course.code}">${gradeInfo.grade}</strong>
                    </div>
                    <div class="grade-item">
                        <label>${t.gpaPoints}</label>
                        <strong id="points-${course.code}">${gradeInfo.points.toFixed(1)}</strong>
                    </div>
                    <div class="grade-item">
                        <label>${t.status}</label>
                        <strong style="color: ${marks ? 'var(--success)' : 'var(--warning)'}">
                            ${marks ? t.graded : t.pending}
                        </strong>
                    </div>
                </div>
            `;
            
            return div;
        }

        function calculateSemesterGPA(courses) {
            let totalPoints = 0;
            let totalHours = 0;
            
            courses.forEach(course => {
                const marks = userGrades[course.code];
                if (marks != null && marks !== '') {
                    const percentage = (marks / course.total) * 100;
                    const gradeInfo = getGradeFromPercentage(percentage);
                    totalPoints += gradeInfo.points * course.hours;
                    totalHours += course.hours;
                }
            });
            
            return totalHours > 0 ? totalPoints / totalHours : 0;
        }

        // ========== GRADE CALCULATION ==========
        function updateGrade(code, marks, total, hours) {
            marks = parseFloat(marks);
            
            if (isNaN(marks) || marks < 0 || marks > total) {
                showNotification('❌ Invalid marks entered!');
                return;
            }
            
            userGrades[code] = marks;
            saveGrades();
            
            const percentage = (marks / total) * 100;
            const gradeInfo = getGradeFromPercentage(percentage);
            
            document.getElementById(`grade-${code}`).textContent = gradeInfo.grade;
            document.getElementById(`points-${code}`).textContent = gradeInfo.points.toFixed(1);
            
            calculateOverallGPA();
            updateCharts();
        }

        function calculateOverallGPA() {
            let totalPoints = 0;
            let totalHours = 0;
            let completedCount = 0;
            
            Object.entries(courseDatabase).forEach(([code, course]) => {
                const marks = userGrades[code];
                if (marks != null && marks !== '') {
                    const percentage = (marks / course.total) * 100;
                    const gradeInfo = getGradeFromPercentage(percentage);
                    totalPoints += gradeInfo.points * course.hours;
                    totalHours += course.hours;
                    completedCount++;
                }
            });
            
            const cgpa = totalHours > 0 ? totalPoints / totalHours : 0;
            const overallGradeInfo = getGradeFromPercentage((cgpa / 4.0) * 100);
            
            document.getElementById('cumulativeGPA').textContent = cgpa.toFixed(decimalPrecision);
            document.getElementById('overallGrade').textContent = overallGradeInfo.grade;
            document.getElementById('totalHours').textContent = totalHours;
            document.getElementById('completedCourses').textContent = completedCount;
            
            renderSemesters();
        }

        // ========== CHARTS ==========
        function updateCharts() {
            updateGPAChart();
            updateGradeChart();
        }

        function updateGPAChart() {
            const ctx = document.getElementById('gpaChart');
            
            const semesterGPAs = [];
            const labels = [];
            
            for (let i = 1; i <= 7; i++) {
                const courses = Object.entries(courseDatabase)
                    .filter(([code, course]) => course.semester === i)
                    .map(([code, course]) => ({ code, ...course }));
                
                const gpa = calculateSemesterGPA(courses);
                if (gpa > 0 || Object.keys(userGrades).length > 0) {
                    semesterGPAs.push(gpa);
                    
                    // Create simple labels like "Semester 1", "Semester 2"
                    if (currentLang === 'ar') {
                        labels.push(`الفصل ${i}`);
                    } else {
                        labels.push(`Semester ${i}`);
                    }
                }
            }
            
            if (gpaChart) {
                gpaChart.destroy();
            }
            
            const isDark = currentTheme === 'dark';
            const textColor = isDark ? '#94a3b8' : '#64748b';
            const gridColor = isDark ? '#1e293b' : '#e2e8f0';
            
            gpaChart = new Chart(ctx, {
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
                        pointRadius: 6,
                        pointBackgroundColor: '#3b82f6',
                        pointBorderColor: '#fff',
                        pointBorderWidth: 2
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: false
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            max: 4.0,
                            ticks: {
                                color: textColor,
                                stepSize: 0.5
                            },
                            grid: {
                                color: gridColor
                            }
                        },
                        x: {
                            ticks: {
                                color: textColor,
                                font: {
                                    size: 11
                                }
                            },
                            grid: {
                                color: gridColor
                            }
                        }
                    }
                }
            });
        }

        function updateGradeChart() {
            const ctx = document.getElementById('gradeChart');
            
            const gradeCounts = {
                'A+': 0, 'A': 0, 'A-': 0,
                'B+': 0, 'B': 0, 'B-': 0,
                'C+': 0, 'C': 0, 'C-': 0,
                'D+': 0, 'D': 0, 'F': 0
            };
            
            Object.entries(courseDatabase).forEach(([code, course]) => {
                const marks = userGrades[code];
                if (marks != null && marks !== '') {
                    const percentage = (marks / course.total) * 100;
                    const gradeInfo = getGradeFromPercentage(percentage);
                    gradeCounts[gradeInfo.grade]++;
                }
            });
            
            if (gradeChart) {
                gradeChart.destroy();
            }
            
            const isDark = currentTheme === 'dark';
            const textColor = isDark ? '#94a3b8' : '#64748b';
            const gridColor = isDark ? '#1e293b' : '#e2e8f0';
            
            gradeChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: Object.keys(gradeCounts),
                    datasets: [{
                        label: currentLang === 'ar' ? 'عدد المقررات' : 'Number of Courses',
                        data: Object.values(gradeCounts),
                        backgroundColor: '#3b82f6',
                        borderColor: '#2563eb',
                        borderWidth: 2,
                        borderRadius: 8
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: false
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            ticks: {
                                stepSize: 1,
                                color: textColor
                            },
                            grid: {
                                color: gridColor
                            }
                        },
                        x: {
                            ticks: {
                                color: textColor
                            },
                            grid: {
                                color: gridColor
                            }
                        }
                    }
                }
            });
        }

        // ========== DATA MANAGEMENT ==========
        function clearAllData() {
            if (confirm('⚠️ Are you sure you want to clear all data? This cannot be undone!')) {
                userGrades = {};
                saveGrades();
                renderSemesters();
                calculateOverallGPA();
                updateCharts();
                showNotification('🗑️ All data cleared!');
            }
        }

        function saveGrades() {
            localStorage.setItem('userGrades', JSON.stringify(userGrades));
        }

        function loadGrades() {
            const saved = localStorage.getItem('userGrades');
            if (saved) {
                userGrades = JSON.parse(saved);
            }
        }

        // ========== PROFILE ==========
        function saveProfile() {
            const userName = document.getElementById('userName').value;
            const studentID = document.getElementById('studentID').value;
            const userEmail = document.getElementById('userEmail').value;
            
            localStorage.setItem('userName', userName);
            localStorage.setItem('studentID', studentID);
            localStorage.setItem('userEmail', userEmail);
            
            showNotification('✅ Profile saved successfully!');
            triggerConfetti();
        }

        function loadProfile() {
            document.getElementById('userName').value = localStorage.getItem('userName') || '';
            document.getElementById('studentID').value = localStorage.getItem('studentID') || '';
            document.getElementById('userEmail').value = localStorage.getItem('userEmail') || '';
        }

        // ========== SETTINGS ==========
        function saveSettings() {
            const theme = document.getElementById('themeSelect').value;
            const precision = document.getElementById('decimalPrecision').value;
            
            decimalPrecision = parseInt(precision);
            
            if (theme !== currentTheme) {
                toggleTheme();
            }
            
            localStorage.setItem('decimalPrecision', precision);
            showNotification('✅ Settings saved!');
            calculateOverallGPA();
        }

        function loadSettings() {
            const savedTheme = localStorage.getItem('theme');
            const savedPrecision = localStorage.getItem('decimalPrecision');
            
            if (savedTheme) {
                currentTheme = savedTheme;
                document.getElementById('themeSelect').value = savedTheme;
                if (savedTheme === 'light') {
                    document.body.setAttribute('data-theme', 'light');
                    document.querySelector('.theme-toggle').textContent = '☀️';
                }
            }
            
            if (savedPrecision) {
                decimalPrecision = parseInt(savedPrecision);
                document.getElementById('decimalPrecision').value = savedPrecision;
            }
        }

        // ========== PRINT & DOWNLOAD ==========
        function printTranscript() {
            window.print();
        }

        function downloadTranscript() {
            const userName = localStorage.getItem('userName') || 'Student';
            const studentID = localStorage.getItem('studentID') || 'N/A';
            const cgpa = document.getElementById('cumulativeGPA').textContent;
            const grade = document.getElementById('overallGrade').textContent;
            const totalCredits = document.getElementById('totalCredits').textContent;
            const completedCourses = document.getElementById('completedCourses').textContent;
            const overallPercentage = document.getElementById('overallPercentage').textContent;
            
            const currentDate = new Date().toLocaleDateString('en-US', { 
                year: 'numeric', 
                month: 'long', 
                day: 'numeric' 
            });
            
            let htmlContent = `<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Academic Transcript - ${userName}</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { 
            font-family: 'Arial', sans-serif; 
            padding: 40px; 
            background: #f5f5f5;
        }
        .transcript { 
            max-width: 900px; 
            margin: 0 auto; 
            background: white; 
            padding: 40px; 
            box-shadow: 0 4px 20px rgba(0,0,0,0.1);
        }
        .header { 
            text-align: center; 
            border-bottom: 3px solid #3b82f6; 
            padding-bottom: 20px; 
            margin-bottom: 30px;
        }
        .header h1 { 
            color: #1a2142; 
            font-size: 32px; 
            margin-bottom: 10px;
        }
        .header h2 { 
            color: #3b82f6; 
            font-size: 24px; 
            margin-bottom: 5px;
        }
        .info-grid { 
            display: grid; 
            grid-template-columns: repeat(2, 1fr); 
            gap: 15px; 
            margin-bottom: 30px;
            background: #f8fafc;
            padding: 20px;
            border-radius: 8px;
        }
        .info-item { 
            display: flex; 
            gap: 10px;
        }
        .info-item strong { 
            color: #1a2142; 
            min-width: 140px;
        }
        .stats { 
            display: grid; 
            grid-template-columns: repeat(4, 1fr); 
            gap: 15px; 
            margin-bottom: 30px;
        }
        .stat-box { 
            background: #3b82f6; 
            color: white; 
            padding: 20px; 
            border-radius: 8px; 
            text-align: center;
        }
        .stat-box .label { 
            font-size: 12px; 
            opacity: 0.9; 
            margin-bottom: 8px;
        }
        .stat-box .value { 
            font-size: 24px; 
            font-weight: bold;
        }
        table { 
            width: 100%; 
            border-collapse: collapse; 
            margin-bottom: 20px;
        }
        th { 
            background: #1a2142; 
            color: white; 
            padding: 12px; 
            text-align: left; 
            font-size: 14px;
        }
        td { 
            padding: 10px 12px; 
            border-bottom: 1px solid #e2e8f0;
        }
        tr:nth-child(even) { 
            background: #f8fafc;
        }
        .semester-title { 
            background: #3b82f6; 
            color: white; 
            padding: 10px 15px; 
            margin-top: 30px; 
            margin-bottom: 15px; 
            border-radius: 5px;
            font-size: 18px;
            font-weight: bold;
        }
        .footer { 
            text-align: center; 
            margin-top: 40px; 
            padding-top: 20px; 
            border-top: 2px solid #e2e8f0; 
            color: #64748b;
        }
        @media print {
            body { padding: 0; background: white; }
            .transcript { box-shadow: none; }
        }
        @media (max-width: 768px) {
            body { padding: 20px; }
            .transcript { padding: 20px; }
            .stats { grid-template-columns: repeat(2, 1fr); }
            .info-grid { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>
    <div class="transcript">
        <div class="header">
            <h1>🧬 HNU Medical Analysis</h1>
            <h2>Academic Transcript</h2>
            <p style="color: #64748b; margin-top: 10px;">Generated on ${currentDate}</p>
        </div>
        
        <div class="info-grid">
            <div class="info-item">
                <strong>Student Name:</strong>
                <span>${userName}</span>
            </div>
            <div class="info-item">
                <strong>Student ID:</strong>
                <span>${studentID}</span>
            </div>
            <div class="info-item">
                <strong>Program:</strong>
                <span>Medical Analysis</span>
            </div>
            <div class="info-item">
                <strong>Date:</strong>
                <span>${currentDate}</span>
            </div>
        </div>
        
        <div class="stats">
            <div class="stat-box">
                <div class="label">CUMULATIVE GPA</div>
                <div class="value">${cgpa}</div>
            </div>
            <div class="stat-box">
                <div class="label">LETTER GRADE</div>
                <div class="value">${grade}</div>
            </div>
            <div class="stat-box">
                <div class="label">TOTAL CREDITS</div>
                <div class="value">${totalCredits}</div>
            </div>
            <div class="stat-box">
                <div class="label">PERCENTAGE</div>
                <div class="value">${overallPercentage}</div>
            </div>
        </div>
`;

            // Add courses by semester
            const semesters = ['1-1', '1-2', '2-1', '2-2', '3-1', '3-2', '4-1'];
            const semesterNames = {
                '1-1': 'Level 1 - Semester 1',
                '1-2': 'Level 1 - Semester 2',
                '2-1': 'Level 2 - Semester 1',
                '2-2': 'Level 2 - Semester 2',
                '3-1': 'Level 3 - Semester 1',
                '3-2': 'Level 3 - Semester 2',
                '4-1': 'Level 4 - Semester 1'
            };

            semesters.forEach(sem => {
                const courses = Object.entries(courseDatabase).filter(([_, course]) => course.semester === sem);
                if (courses.length === 0) return;
                
                const semesterGPA = calculateSemesterGPA(sem);
                const hasCourses = courses.some(([code]) => userGrades[code] != null && userGrades[code] !== '');
                
                if (!hasCourses) return;

                htmlContent += `
        <div class="semester-title">${semesterNames[sem]} - GPA: ${semesterGPA}</div>
        <table>
            <thead>
                <tr>
                    <th>Course Code</th>
                    <th>Course Name</th>
                    <th>Credits</th>
                    <th>Marks</th>
                    <th>Grade</th>
                    <th>Points</th>
                </tr>
            </thead>
            <tbody>`;

                courses.forEach(([code, course]) => {
                    const marks = userGrades[code];
                    if (marks != null && marks !== '') {
                        const percentage = (marks / course.total) * 100;
                        const gradeInfo = getGradeFromPercentage(percentage);
                        htmlContent += `
                <tr>
                    <td>${code}</td>
                    <td>${course.name}</td>
                    <td>${course.hours}</td>
                    <td>${marks}/${course.total}</td>
                    <td>${gradeInfo.grade}</td>
                    <td>${gradeInfo.gpa.toFixed(2)}</td>
                </tr>`;
                    }
                });

                htmlContent += `
            </tbody>
        </table>`;
            });

            htmlContent += `
        <div class="footer">
            <p><strong>HNU Medical Analysis Program</strong></p>
            <p>This is an unofficial transcript generated by the GPA Calculator</p>
            <p style="margin-top: 10px; font-size: 12px;">© ${new Date().getFullYear()} - Generated automatically</p>
        </div>
    </div>
</body>
</html>`;

            // Create and download the file
            const blob = new Blob([htmlContent], { type: 'text/html' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `Transcript_${userName.replace(/\s+/g, '_')}_${Date.now()}.html`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
            
            showNotification('✅ Transcript downloaded!');
        }

        function shareGPA() {
            const cgpa = document.getElementById('cumulativeGPA').textContent;
            const grade = document.getElementById('overallGrade').textContent;
            const shareText = `🎓 My CGPA: ${cgpa} (${grade})\n🧬 HNU Medical Analysis`;
            
            if (navigator.share) {
                navigator.share({ title: 'My GPA', text: shareText }).catch(() => {
                    copyToClipboard(shareText);
                });
            } else {
                copyToClipboard(shareText);
            }
        }

        function copyToClipboard(text) {
            navigator.clipboard.writeText(text).then(() => {
                showNotification('✅ Copied to clipboard!');
            }).catch(() => {
                showNotification('❌ Could not copy');
            });
        }

        // ========== NOTIFICATIONS ==========
        function showNotification(message) {
            const notification = document.getElementById('notification');
            notification.textContent = message;
            notification.classList.add('show');
            
            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }

        // ========== CONFETTI ==========
        function triggerConfetti() {
            if (typeof confetti !== 'undefined') {
                confetti({
                    particleCount: 100,
                    spread: 70,
                    origin: { y: 0.6 }
                });
            }
        }

        // ========== INITIALIZATION ==========
        document.addEventListener('DOMContentLoaded', function() {
            loadProfile();
            loadSettings();
            loadGrades();
            
            const savedLang = localStorage.getItem('language') || 'en';
            currentLang = savedLang;
            if (savedLang === 'ar') {
                document.body.setAttribute('dir', 'rtl');
                document.querySelector('[data-lang="ar"]').classList.add('active');
                document.querySelector('[data-lang="en"]').classList.remove('active');
            }
            
            updateLanguage();
            renderSemesters();
            calculateOverallGPA();
            updateCharts();
        });
    </script>
</body>
</html>
