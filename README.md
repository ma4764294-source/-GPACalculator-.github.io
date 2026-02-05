<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HNU GPA Calculator</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=Cairo:wght@300;400;600;700;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
    <style>
:root{--bg-primary:#0a0e27;--bg-secondary:#151b3d;--bg-card:#1a2142;--accent:#5b8def;--success:#10b981;--danger:#ef4444;--text-primary:#fff;--text-secondary:#94a3b8;--border:#2d3548}
*{margin:0;padding:0;box-sizing:border-box}
body{font-family:'Inter',sans-serif;background:var(--bg-primary);color:var(--text-primary);overflow-x:hidden}
body[dir="rtl"]{font-family:'Cairo',sans-serif}
@keyframes fadeIn{from{opacity:0;transform:translateY(1.25rem)}to{opacity:1;transform:translateY(0)}}
@keyframes glow{0%,100%{box-shadow:0 0 1.25rem rgba(91,141,239,.3)}50%{box-shadow:0 0 1.875rem rgba(91,141,239,.5)}}
@keyframes sparkle{0%,100%{opacity:1;transform:translateY(0)}50%{opacity:.8;transform:translateY(-0.3125rem)}}
.auth-container{min-height:100vh;display:flex;align-items:center;justify-content:center;padding:5%;background:linear-gradient(-45deg,#0a0e27,#151b3d,#1a2142)}
.auth-card{background:rgba(26,33,66,.95);backdrop-filter:blur(1.25rem);border-radius:1.5rem;padding:8%;max-width:26.25rem;width:100%;box-shadow:0 1.25rem 3.75rem rgba(0,0,0,.5);border:0.0625rem solid rgba(91,141,239,.2);animation:fadeIn .6s ease}
.auth-logo{width:5rem;height:5rem;background:linear-gradient(135deg,var(--accent),#7ba3f5);border-radius:1.25rem;display:flex;align-items:center;justify-content:center;margin:0 auto 1.25rem;font-size:2.25rem}
.auth-title{font-size:1.75rem;font-weight:700;margin-bottom:0.5rem;text-align:center}
.auth-subtitle{color:var(--text-secondary);font-size:0.875rem;text-align:center;margin-bottom:2.5rem}
.form-group{margin-bottom:1.25rem}
.form-label{display:block;margin-bottom:0.5rem;font-weight:500;font-size:0.875rem;color:var(--text-secondary)}
.form-input{width:100%;padding:0.875rem;background:var(--bg-secondary);border:0.0625rem solid var(--border);border-radius:0.75rem;color:var(--text-primary);font-size:0.9375rem}
.form-input:focus{outline:0;border-color:var(--accent)}
.btn-primary{width:100%;padding:1rem;background:linear-gradient(135deg,var(--accent),#7ba3f5);border:none;border-radius:0.75rem;color:#fff;font-size:1rem;font-weight:600;cursor:pointer;margin-bottom:1rem}
.btn-primary:hover{transform:translateY(-0.125rem);box-shadow:0 0.5rem 1.5rem rgba(91,141,239,.4)}
.btn-reset{width:100%;padding:1rem;background:linear-gradient(135deg,var(--danger),#f87171);border:none;border-radius:0.75rem;color:#fff;font-size:1rem;font-weight:600;cursor:pointer;margin-top:1rem;transition:all .3s ease}
.btn-reset:hover{transform:translateY(-0.125rem);box-shadow:0 0.5rem 1.5rem rgba(239,68,68,.4)}
.app-container{display:none}
.sidebar{position:fixed;left:0;top:0;height:100vh;width:17.5rem;background:var(--bg-secondary);padding:1.5rem 0;overflow-y:auto;z-index:1000;border-right:0.0625rem solid var(--border);transition:transform .3s ease;display:flex;flex-direction:column}
body[dir="rtl"] .sidebar{left:auto;right:0;border-right:none;border-left:0.0625rem solid var(--border)}
.sidebar.hidden{transform:translateX(-100%)}
body[dir="rtl"] .sidebar.hidden{transform:translateX(100%)}
.sidebar-header{padding:0 1.5rem 1.5rem;border-bottom:0.0625rem solid var(--border);margin-bottom:1.5rem}
.logo-icon{width:2.5rem;height:2.5rem;background:linear-gradient(135deg,var(--accent),#7ba3f5);border-radius:0.625rem;display:flex;align-items:center;justify-content:center;font-size:1.25rem;margin-bottom:0.75rem}
.sidebar-title{font-size:1.25rem;font-weight:700}
.sidebar-subtitle{font-size:0.75rem;color:var(--text-secondary);margin-top:0.25rem}
.menu-item{display:flex;align-items:center;gap:1rem;padding:0.875rem 1.5rem;margin:0 0.75rem 0.5rem;border-radius:0.75rem;cursor:pointer;transition:all .3s ease;color:var(--text-secondary)}
.menu-item:hover{background:var(--bg-card);color:var(--text-primary)}
.menu-item.active{background:linear-gradient(135deg,var(--accent),#7ba3f5);color:#fff}
.menu-icon{font-size:1.25rem;width:1.5rem}
.main-content{margin-left:17.5rem;padding:1.5rem;min-height:100vh}
body[dir="rtl"] .main-content{margin-left:0;margin-right:17.5rem}
.top-bar{display:flex;justify-content:space-between;align-items:center;margin-bottom:2rem;flex-wrap:wrap;gap:1rem;padding:1.5rem;background:var(--bg-card);border-radius:1rem;border:0.0625rem solid var(--border)}
.greeting{display:flex;flex-direction:column;gap:0.5rem}
.greeting-name{font-size:1.75rem;font-weight:700}
.greeting-info{color:var(--text-secondary);font-size:0.875rem}
.action-btns{display:flex;gap:0.75rem;flex-wrap:wrap}
.btn{padding:0.625rem 1.25rem;border-radius:0.625rem;border:none;cursor:pointer;font-weight:500;font-size:0.875rem;transition:all .3s ease}
.btn-outline{background:transparent;border:0.0625rem solid var(--border);color:var(--text-primary)}
.btn-outline:hover{background:var(--bg-secondary)}
.stats-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(15.625rem,1fr));gap:1.5rem;margin-bottom:2rem}
.stat-card{background:var(--bg-card);padding:1.5rem;border-radius:1rem;border:0.0625rem solid var(--border);animation:fadeIn .6s ease}
.stat-label{color:var(--text-secondary);font-size:0.875rem;margin-bottom:0.5rem}
.stat-value{font-size:2rem;font-weight:700;margin-bottom:0.25rem}
.stat-gpa{background:linear-gradient(135deg,#10b981,#34d399);-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;filter:drop-shadow(0 0 0.625rem rgba(16,185,129,0.6)) drop-shadow(0 0 1.25rem rgba(52,211,153,0.4));animation:glowGreen 2s ease-in-out infinite}
.stat-credits{background:linear-gradient(135deg,#f59e0b,#fbbf24);-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;filter:drop-shadow(0 0 0.625rem rgba(245,158,11,0.6)) drop-shadow(0 0 1.25rem rgba(251,191,36,0.4));animation:glowOrange 2s ease-in-out infinite}
.stat-courses{background:linear-gradient(135deg,#ef4444,#f87171);-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;filter:drop-shadow(0 0 0.625rem rgba(239,68,68,0.6)) drop-shadow(0 0 1.25rem rgba(248,113,113,0.4));animation:glowRed 2s ease-in-out infinite}
.stat-status{color:#5b8def !important;font-weight:600;filter:drop-shadow(0 0 0.375rem rgba(91,141,239,0.5))}
@keyframes glowGreen{0%,100%{filter:drop-shadow(0 0 0.625rem rgba(16,185,129,0.6)) drop-shadow(0 0 1.25rem rgba(52,211,153,0.4))}50%{filter:drop-shadow(0 0 1rem rgba(16,185,129,0.8)) drop-shadow(0 0 1.875rem rgba(52,211,153,0.6))}}
@keyframes glowOrange{0%,100%{filter:drop-shadow(0 0 0.625rem rgba(245,158,11,0.6)) drop-shadow(0 0 1.25rem rgba(251,191,36,0.4))}50%{filter:drop-shadow(0 0 1rem rgba(245,158,11,0.8)) drop-shadow(0 0 1.875rem rgba(251,191,36,0.6))}}
@keyframes glowRed{0%,100%{filter:drop-shadow(0 0 0.625rem rgba(239,68,68,0.6)) drop-shadow(0 0 1.25rem rgba(248,113,113,0.4))}50%{filter:drop-shadow(0 0 1rem rgba(239,68,68,0.8)) drop-shadow(0 0 1.875rem rgba(248,113,113,0.6))}}
.page-content{animation:fadeIn .6s ease}
.page-content.hidden{display:none}
.semester-bar{background:var(--bg-card);border-radius:1rem;margin-bottom:1rem;border:0.0625rem solid var(--border);overflow:hidden;animation:fadeIn .6s ease;transition:all .3s ease}
.semester-header{padding:1.25rem 1.5rem;cursor:pointer;display:flex;justify-content:space-between;align-items:center;transition:all .3s ease}
.semester-header:hover{background:rgba(91,141,239,.05)}
.semester-info{display:flex;align-items:center;gap:1rem}
.semester-icon{transition:transform .3s ease;color:var(--accent)}
.semester-bar.expanded .semester-icon{transform:rotate(90deg)}
body[dir="rtl"] .semester-bar.expanded .semester-icon{transform:rotate(-90deg)}
.semester-title{font-size:1.125rem;font-weight:600}
.semester-stats{display:flex;gap:1.5rem;align-items:center}
.semester-gpa{font-size:1.5rem;font-weight:700;background:linear-gradient(135deg,var(--accent),#7ba3f5);-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
.semester-details{max-height:0;overflow:hidden;transition:max-height .4s ease}
.semester-details.expanded{max-height:200rem;padding:0 1.5rem 1.5rem}
.course-item{display:grid;grid-template-columns:2fr 1fr 1fr 1fr;gap:1rem;padding:1rem;background:var(--bg-secondary);border-radius:0.75rem;margin-bottom:0.75rem;align-items:center}
.course-info{display:flex;flex-direction:column;gap:0.25rem}
.course-code{font-weight:600;color:var(--accent);font-size:0.875rem}
.course-name{font-size:0.9375rem;font-weight:500}
.course-input{padding:0.625rem;background:var(--bg-primary);border:0.0625rem solid var(--border);border-radius:0.5rem;color:var(--text-primary);text-align:center;font-size:0.875rem;width:100%}
.course-input:focus{outline:0;border-color:var(--accent)}
.course-input[readonly]{background:var(--bg-card);cursor:default;border-color:transparent}
.grade-badge{padding:0.375rem 0.75rem;border-radius:0.5rem;font-weight:600;text-align:center;font-size:0.875rem}
.grade-A{background:linear-gradient(135deg,#10b981,#34d399);color:#fff}
.grade-B{background:linear-gradient(135deg,#5b8def,#7ba3f5);color:#fff}
.grade-C{background:linear-gradient(135deg,#f59e0b,#fbbf24);color:#fff}
.grade-D{background:linear-gradient(135deg,#ef4444,#f87171);color:#fff}
.chart-container{background:var(--bg-card);padding:1.5rem;border-radius:1rem;border:0.0625rem solid var(--border);margin-bottom:1.5rem}
.chart-title{font-size:1.25rem;font-weight:600;margin-bottom:1.5rem;color:var(--text-primary)}
.chart-wrapper{position:relative;height:18.75rem}
.modal{position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,.7);display:none;align-items:center;justify-content:center;z-index:2000;padding:5%}
.modal.active{display:flex}
.modal-content{background:var(--bg-card);padding:2rem;border-radius:1rem;max-width:37.5rem;width:100%;border:0.0625rem solid var(--border)}
.modal-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:1.5rem}
.modal-title{font-size:1.5rem;font-weight:700}
.close-btn{background:none;border:none;font-size:1.5rem;color:var(--text-secondary);cursor:pointer;padding:0;width:2rem;height:2rem;display:flex;align-items:center;justify-content:center}
.close-btn:hover{color:var(--text-primary)}
textarea{width:100%;min-height:12.5rem;padding:1rem;background:var(--bg-secondary);border:0.0625rem solid var(--border);border-radius:0.75rem;color:var(--text-primary);font-family:'Courier New',monospace;font-size:0.875rem;resize:vertical}
textarea:focus{outline:0;border-color:var(--accent)}
.overlay{position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,.5);display:none;z-index:999}
.overlay.active{display:block}
.analysis-summary{background:var(--bg-card);padding:1.5rem;border-radius:1rem;border:0.0625rem solid var(--border);margin-bottom:1.5rem}
.analysis-row{display:flex;justify-content:space-between;padding:0.75rem 0;border-bottom:0.0625rem solid var(--border)}
.analysis-row:last-child{border-bottom:none}
.analysis-label{color:var(--text-secondary);font-size:0.9375rem}
.analysis-value{font-weight:600;font-size:1rem}
.status-excellent{color:#10b981}
.status-very-good{color:#5b8def}
.status-good{color:#f59e0b}
.status-pass{color:#ef4444}
.status-risk{color:#dc2626}
@media(max-width:48rem){
.sidebar{transform:translateX(-100%)}
body[dir="rtl"] .sidebar{transform:translateX(100%)}
.sidebar.mobile-open{transform:translateX(0)}
.main-content{margin-left:0}
body[dir="rtl"] .main-content{margin-right:0}
.mobile-menu-btn{display:flex}
.course-item{grid-template-columns:1fr;gap:0.75rem}
.stat-value{font-size:1.5rem}
.greeting-name{font-size:1.25rem}
}
.mobile-menu-btn{display:none;position:fixed;bottom:1.5rem;right:1.5rem;width:3.5rem;height:3.5rem;background:linear-gradient(135deg,var(--accent),#7ba3f5);border:none;border-radius:50%;color:#fff;font-size:1.25rem;cursor:pointer;box-shadow:0 0.25rem 1rem rgba(91,141,239,.4);z-index:1001}
body[dir="rtl"] .mobile-menu-btn{right:auto;left:1.5rem}
@media(max-width:48rem){
.mobile-menu-btn{display:flex;align-items:center;justify-content:center}
}
.developer-name{font-size:1.25rem;font-weight:900;background:linear-gradient(90deg,#3b82f6,#60a5fa,#7ba3f5,#5b8def,#3b82f6);background-size:300% 300%;-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;animation:sparkleGradient 4s ease-in-out infinite;filter:drop-shadow(0 0 0.5rem rgba(91,141,239,0.6)) drop-shadow(0 0 1rem rgba(59,130,246,0.4));letter-spacing:0.15em;font-family:'Courier New',monospace;text-transform:uppercase;font-style:italic}
@keyframes sparkleGradient{0%,100%{background-position:0% 50%}25%{background-position:50% 50%}50%{background-position:100% 50%}75%{background-position:50% 50%}}
</style>
</head>
<body dir="ltr">

<!-- Authentication Screen -->
<div id="authScreen" class="auth-container">
    <div class="auth-card">
        <div class="auth-logo">🎓</div>
        <h1 class="auth-title" data-lang="welcome">Welcome</h1>
        <p class="auth-subtitle" data-lang="auth_subtitle">Enter your name to continue</p>
        <form id="authForm" onsubmit="handleAuth(event)">
            <div class="form-group">
                <label class="form-label" data-lang="name">Name</label>
                <input type="text" id="studentName" class="form-input" required data-lang="name_placeholder" placeholder="Enter your full name">
            </div>
            <button type="submit" class="btn-primary" data-lang="continue">Continue</button>
        </form>
    </div>
</div>

<!-- App Container -->
<div id="appContainer" class="app-container">
    <!-- Sidebar -->
    <div id="sidebar" class="sidebar">
        <div class="menu-item active" data-page="dashboard">
            <i class="fas fa-home menu-icon"></i>
            <span data-lang="dashboard">Dashboard</span>
        </div>
        <div class="menu-item" data-page="courses">
            <i class="fas fa-book menu-icon"></i>
            <span data-lang="courses">Courses</span>
        </div>
        <div class="menu-item" data-page="analysis">
            <i class="fas fa-chart-line menu-icon"></i>
            <span data-lang="analysis">Analysis</span>
        </div>
        <div style="flex:1"></div>
        <div class="sidebar-header" style="border-top:0.0625rem solid var(--border);border-bottom:none;margin-top:1.5rem;padding-top:1.5rem">
            <div class="logo-icon">🎓</div>
            <div class="sidebar-title" data-lang="app_title">HNU GPA</div>
            <div class="sidebar-subtitle" id="studentNameDisplay"></div>
        </div>
        <div class="menu-item" onclick="logout()">
            <i class="fas fa-sign-out-alt menu-icon"></i>
            <span data-lang="logout">Logout</span>
        </div>
    </div>

    <!-- Main Content -->
    <div class="main-content">
        <!-- Top Bar -->
        <div class="top-bar">
            <div class="greeting">
                <div class="greeting-name" id="greetingName"></div>
                <div class="greeting-info" id="currentDate"></div>
            </div>
            <div class="action-btns">
                <button class="btn btn-outline" onclick="openImportModal()">
                    <i class="fas fa-file-import"></i> <span data-lang="import">Import Grades</span>
                </button>
                <button class="btn btn-outline" onclick="toggleLanguage()">
                    <span id="currentLang">🇺🇸 EN</span>
                </button>
            </div>
        </div>

        <!-- Dashboard Page -->
        <div id="dashboardPage" class="page-content">
            <div class="stats-grid">
                <div class="stat-card">
                    <div class="stat-label" data-lang="overall_gpa">Overall GPA</div>
                    <div class="stat-value stat-gpa" id="overallGPA">0.00</div>
                    <div class="stat-label stat-status" id="academicStatus">Not Started</div>
                    <div style="margin-top:0.75rem;padding:0.5rem;background:rgba(91,141,239,0.1);border-radius:0.5rem;font-size:0.75rem;color:#7ba3f5;text-align:center">
                        <i class="fas fa-info-circle"></i> <span data-lang="gpa_hint">Go to Courses section for customization</span>
                    </div>
                </div>
                <div class="stat-card">
                    <div class="stat-label" data-lang="total_credits">Total Credits</div>
                    <div class="stat-value stat-credits" id="totalCredits">0</div>
                </div>
                <div class="stat-card">
                    <div class="stat-label" data-lang="completed_courses">Completed Courses</div>
                    <div class="stat-value stat-courses" id="completedCourses">0</div>
                </div>
            </div>
            <button class="btn-reset" onclick="resetAllData()">
                <i class="fas fa-redo"></i> <span data-lang="reset">Reset Everything</span>
            </button>
            <div style="text-align:center;margin-top:2rem;padding:1.5rem;background:var(--bg-card);border-radius:1rem;border:0.0625rem solid var(--border)">
                <div style="color:var(--text-secondary);font-size:0.875rem;margin-bottom:0.5rem;letter-spacing:0.1em">DEVELOPER</div>
                <div class="developer-name">Mohand Ahmed</div>
            </div>
        </div>

        <!-- Courses Page -->
        <div id="coursesPage" class="page-content hidden">
            <div id="semestersContainer"></div>
        </div>

        <!-- Analysis Page -->
        <div id="analysisPage" class="page-content hidden">
            <div class="analysis-summary">
                <h2 class="chart-title" data-lang="performance_summary">Performance Summary</h2>
                <div class="analysis-row">
                    <span class="analysis-label" data-lang="overall_gpa">Overall GPA</span>
                    <span class="analysis-value" id="analysisGPA">0.00</span>
                </div>
                <div class="analysis-row">
                    <span class="analysis-label" data-lang="academic_status">Academic Status</span>
                    <span class="analysis-value" id="analysisStatus">Not Started</span>
                </div>
                <div class="analysis-row">
                    <span class="analysis-label" data-lang="total_credits">Total Credits Earned</span>
                    <span class="analysis-value" id="analysisCredits">0</span>
                </div>
                <div class="analysis-row">
                    <span class="analysis-label" data-lang="completed_courses">Courses Completed</span>
                    <span class="analysis-value" id="analysisCourses">0</span>
                </div>
                <div class="analysis-row">
                    <span class="analysis-label" data-lang="highest_grade">Highest Grade</span>
                    <span class="analysis-value" id="analysisHighest">-</span>
                </div>
                <div class="analysis-row">
                    <span class="analysis-label" data-lang="lowest_grade">Lowest Grade</span>
                    <span class="analysis-value" id="analysisLowest">-</span>
                </div>
                <div class="analysis-row">
                    <span class="analysis-label" data-lang="average_percentage">Average Percentage</span>
                    <span class="analysis-value" id="analysisAvgPercent">0%</span>
                </div>
            </div>

            <div class="chart-container">
                <h3 class="chart-title" data-lang="semester_gpa">Semester-wise GPA Trend</h3>
                <div class="chart-wrapper">
                    <canvas id="gpaChart"></canvas>
                </div>
            </div>

            <div class="chart-container">
                <h3 class="chart-title" data-lang="grade_distribution">Grade Distribution</h3>
                <div class="chart-wrapper">
                    <canvas id="gradeChart"></canvas>
                </div>
            </div>

            <div class="chart-container">
                <h3 class="chart-title" data-lang="credits_semester">Credits per Semester</h3>
                <div class="chart-wrapper">
                    <canvas id="creditChart"></canvas>
                </div>
            </div>
        </div>
    </div>

    <!-- Mobile Menu Button -->
    <button id="mobileMenuBtn" class="mobile-menu-btn">
        <i class="fas fa-bars"></i>
    </button>

    <!-- Overlay -->
    <div id="overlay" class="overlay"></div>
</div>

<!-- Import Modal -->
<div id="importModal" class="modal">
    <div class="modal-content">
        <div class="modal-header">
            <h2 class="modal-title" data-lang="import_grades">Import Grades</h2>
            <button class="close-btn" onclick="closeImportModal()">×</button>
        </div>
        <p style="color:var(--text-secondary);margin-bottom:1rem" data-lang="import_instructions">Paste your grades data below (from HNU website or formatted text)</p>
        <textarea id="importData" placeholder="TL309 — 184 / 200&#10;THS3011 — 97 / 100&#10;TL3010 — 173 / 200"></textarea>
        <button class="btn-primary" style="margin-top:1rem" onclick="processImport()">
            <i class="fas fa-upload"></i> <span data-lang="import">Import</span>
        </button>
    </div>
</div>

<script>
// Grading System
const GRADING = [
    {grade: 'A+', points: 4.0, min: 95, max: 100},
    {grade: 'A', points: 3.8, min: 90, max: 94.99},
    {grade: 'A-', points: 3.6, min: 85, max: 89.99},
    {grade: 'B+', points: 3.4, min: 82.5, max: 84.99},
    {grade: 'B', points: 3.2, min: 77.5, max: 82.49},
    {grade: 'B-', points: 3.0, min: 75, max: 77.49},
    {grade: 'C+', points: 2.8, min: 72.5, max: 74.99},
    {grade: 'C', points: 2.6, min: 67.5, max: 72.49},
    {grade: 'C-', points: 2.4, min: 65, max: 67.49},
    {grade: 'D+', points: 2.2, min: 62.5, max: 64.99},
    {grade: 'D', points: 2.0, min: 60, max: 62.49},
    {grade: 'F', points: 0.0, min: 0, max: 59.99}
];

// Complete Course Data - All 4 Levels
const COURSES = {
    first_1: [
        {code: 'UN101', name: 'Academic Reading and Writing (1)', name_ar: 'القراءة والكتابة الأكاديمية (1)', hours: 2, total: 100},
        {code: 'THS101', name: 'Basic Physics', name_ar: 'الفيزياء الأساسية', hours: 2, total: 100},
        {code: 'THS102', name: 'Mathematics', name_ar: 'الرياضيات', hours: 2, total: 100},
        {code: 'THS103', name: 'Introduction to Electrical Engineering', name_ar: 'مقدمة في الهندسة الكهربائية', hours: 3, total: 150},
        {code: 'UN102', name: 'Computer Skills', name_ar: 'مهارات الحاسوب', hours: 2, total: 100},
        {code: 'THS104', name: 'Mechanics', name_ar: 'الميكانيكا', hours: 2, total: 100},
        {code: 'UN103', name: 'Critical Thinking', name_ar: 'التفكير النقدي', hours: 2, total: 100}
    ],
    first_2: [
        {code: 'THS115', name: 'Electronic Circuits & Devices', name_ar: 'الدوائر والأجهزة الإلكترونية', hours: 3, total: 150},
        {code: 'THS116', name: 'General Anatomy & Histology', name_ar: 'علم التشريح وعلم الأنسجة العام', hours: 3, total: 150},
        {code: 'THS117', name: 'General Physiology', name_ar: 'علم وظائف الأعضاء العام', hours: 2, total: 100},
        {code: 'THS118', name: 'General Microbiology', name_ar: 'علم الأحياء الدقيقة العام', hours: 2, total: 100},
        {code: 'THS119', name: 'General Chemistry', name_ar: 'الكيمياء العامة', hours: 2, total: 100},
        {code: 'UN114', name: 'Academic Reading and Writing (2)', name_ar: 'القراءة والكتابة الأكاديمية (2)', hours: 2, total: 100},
        {code: 'THS1110', name: 'Professional Ethics', name_ar: 'الأخلاقيات المهنية', hours: 1, total: 50}
    ],
    second_1: [
        {code: 'THS2010', name: 'Mechatronics Engineering', name_ar: 'هندسة الميكاترونكس', hours: 2, total: 100},
        {code: 'TL201', name: 'Biochemistry (1)', name_ar: 'الكيمياء الحيوية (1)', hours: 4, total: 200},
        {code: 'TL202', name: 'Parasitology (1)', name_ar: 'علم الطفيليات (1)', hours: 2, total: 100},
        {code: 'TL203', name: 'Bacteriology', name_ar: 'علم البكتيريا', hours: 4, total: 200},
        {code: 'TL204', name: 'Histology for Lab Technologists', name_ar: 'علم الأنسجة لتقنيي المختبرات', hours: 2, total: 100},
        {code: 'UN5', name: 'Foundation of Digital Technology', name_ar: 'أساسيات التكنولوجيا الرقمية', hours: 2, total: 100},
        {code: 'UN6', name: 'English Language', name_ar: 'اللغة الإنجليزية', hours: 2, total: 100}
    ],
    second_2: [
        {code: 'TL215', name: 'Molecular Biology', name_ar: 'علم الأحياء الجزيئي', hours: 4, total: 200},
        {code: 'TL216', name: 'Hematology (1)', name_ar: 'علم أمراض الدم (1)', hours: 4, total: 200},
        {code: 'TL217', name: 'Systematic Physiology', name_ar: 'علم وظائف الأعضاء المنهجي', hours: 4, total: 200},
        {code: 'TL218', name: 'General Biology', name_ar: 'علم الأحياء العام', hours: 3, total: 150},
        {code: 'ETHS1', name: 'Elective (1)', name_ar: 'اختياري (1)', hours: 1, total: 50}
    ],
    third_1: [
        {code: 'TL309', name: 'Lab Instrumentation (1)', name_ar: 'أجهزة المختبرات (1)', hours: 4, total: 200},
        {code: 'TL3010', name: 'Enzymology & Hormones', name_ar: 'علم الإنزيمات والهرمونات', hours: 4, total: 200},
        {code: 'TL3011', name: 'Parasitology (2)', name_ar: 'علم الطفيليات (2)', hours: 3, total: 150},
        {code: 'TL3012', name: 'Systematic Pathology', name_ar: 'علم الأمراض المنهجي', hours: 3, total: 150},
        {code: 'THS3011', name: 'Infection Control', name_ar: 'مكافحة العدوى', hours: 2, total: 100},
        {code: 'UN7', name: 'Innovation & Entrepreneurship', name_ar: 'الابتكار وريادة الأعمال', hours: 2, total: 100}
    ],
    third_2: [
        {code: 'TL3113', name: 'Biochemistry (2)', name_ar: 'الكيمياء الحيوية (2)', hours: 4, total: 200},
        {code: 'TL3114', name: 'Basic Immunology', name_ar: 'علم المناعة الأساسي', hours: 3, total: 150},
        {code: 'TL3115', name: 'Quality Management (1)', name_ar: 'إدارة الجودة (1)', hours: 4, total: 200},
        {code: 'TL3116', name: 'Lab Instrumentation (2)', name_ar: 'أجهزة المختبرات (2)', hours: 4, total: 200},
        {code: 'ETHS2', name: 'Elective (2)', name_ar: 'اختياري (2)', hours: 1, total: 50}
    ],
    fourth_1: [
        {code: 'TL4017', name: 'Biochemistry (3)', name_ar: 'الكيمياء الحيوية (3)', hours: 3, total: 150},
        {code: 'TL4018', name: 'Virology & Mycology', name_ar: 'علم الفيروسات والفطريات', hours: 3, total: 150},
        {code: 'TL4019', name: 'Hematology (2)', name_ar: 'علم أمراض الدم (2)', hours: 4, total: 200},
        {code: 'TL4020', name: 'Blood Banking', name_ar: 'بنوك الدم', hours: 4, total: 200},
        {code: 'ETHS3', name: 'Elective (3)', name_ar: 'اختياري (3)', hours: 1, total: 50}
    ],
    fourth_2: [
        {code: 'TL4121', name: 'Immunology & Serology', name_ar: 'علم المناعة والأمصال', hours: 4, total: 200},
        {code: 'TL4122', name: 'Age & Pregnancy Investigation', name_ar: 'فحوصات العمر والحمل', hours: 4, total: 200},
        {code: 'TL4123', name: 'Quality Management (2)', name_ar: 'إدارة الجودة (2)', hours: 4, total: 150},
        {code: 'TL4124', name: 'Forensic Chemistry & Toxicology', name_ar: 'الكيمياء الشرعية وعلم السموم', hours: 4, total: 200},
        {code: 'ETHS4', name: 'Elective (4)', name_ar: 'اختياري (4)', hours: 1, total: 50}
    ]
};

// Translations
const translations = {
    en: {
        welcome: 'Welcome',
        auth_subtitle: 'Enter your name to continue',
        name: 'Name',
        name_placeholder: 'Enter your full name',
        continue: 'Continue',
        app_title: 'HNU GPA',
        dashboard: 'Dashboard',
        courses: 'Courses',
        analysis: 'Analysis',
        logout: 'Logout',
        import: 'Import Grades',
        overall_gpa: 'Overall GPA',
        total_credits: 'Total Credits',
        completed_courses: 'Completed Courses',
        reset: 'Reset Everything',
        import_grades: 'Import Grades',
        import_instructions: 'Paste your grades data below (from HNU website or formatted text)',
        performance_summary: 'Performance Summary',
        academic_status: 'Academic Status',
        highest_grade: 'Highest Grade',
        lowest_grade: 'Lowest Grade',
        average_percentage: 'Average Percentage',
        semester_gpa: 'Semester-wise GPA Trend',
        grade_distribution: 'Grade Distribution',
        credits_semester: 'Credits per Semester',
        gpa_hint: 'Go to Courses section for customization'
    },
    ar: {
        welcome: 'مرحباً',
        auth_subtitle: 'أدخل اسمك للمتابعة',
        name: 'الاسم',
        name_placeholder: 'أدخل اسمك الكامل',
        continue: 'متابعة',
        app_title: 'حاسبة المعدل التراكمي',
        dashboard: 'لوحة التحكم',
        courses: 'المقررات',
        analysis: 'التحليل',
        logout: 'تسجيل الخروج',
        import: 'استيراد الدرجات',
        overall_gpa: 'المعدل التراكمي',
        total_credits: 'إجمالي الساعات',
        completed_courses: 'المقررات المكتملة',
        reset: 'إعادة تعيين الكل',
        import_grades: 'استيراد الدرجات',
        import_instructions: 'الصق بيانات درجاتك أدناه (من موقع HNU أو نص منسق)',
        performance_summary: 'ملخص الأداء',
        academic_status: 'الحالة الأكاديمية',
        highest_grade: 'أعلى درجة',
        lowest_grade: 'أدنى درجة',
        average_percentage: 'متوسط النسبة المئوية',
        semester_gpa: 'اتجاه المعدل التراكمي الفصلي',
        grade_distribution: 'توزيع الدرجات',
        credits_semester: 'الساعات لكل فصل دراسي',
        gpa_hint: 'انتقل إلى قسم المقررات للتخصيص'
    }
};

// Global Variables
let studentData = {};
let currentLang = 'en';
let charts = {gpaChart: null, gradeChart: null, creditChart: null};

// Load saved data
function loadFromStorage() {
    const saved = localStorage.getItem('hnu_student_data');
    if (saved) {
        studentData = JSON.parse(saved);
        return true;
    }
    return false;
}

// Save data
function saveToStorage() {
    localStorage.setItem('hnu_student_data', JSON.stringify(studentData));
}

// Handle authentication
function handleAuth(event) {
    event.preventDefault();
    const name = document.getElementById('studentName').value.trim();
    if (name) {
        studentData.name = name;
        saveToStorage();
        showApp();
    }
}

// Show app
function showApp() {
    document.getElementById('authScreen').style.display = 'none';
    document.getElementById('appContainer').style.display = 'block';
    document.getElementById('studentNameDisplay').textContent = studentData.name;
    document.getElementById('greetingName').textContent = `Hello, ${studentData.name}! 👋`;
    
    const now = new Date();
    const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
    document.getElementById('currentDate').textContent = now.toLocaleDateString('en-US', options);
    
    renderAllSemesters();
    calculateAllGPAs();
    updateLanguage();
}

// Logout
function logout() {
    if (confirm('Are you sure you want to logout?')) {
        localStorage.removeItem('hnu_student_data');
        location.reload();
    }
}

// Reset all data
function resetAllData() {
    if (confirm('⚠️ This will delete all your grades and cannot be undone. Are you sure?')) {
        const name = studentData.name;
        studentData = {name: name};
        saveToStorage();
        renderAllSemesters();
        calculateAllGPAs();
        alert('✅ All grades have been reset!');
    }
}

// Toggle language
function toggleLanguage() {
    currentLang = currentLang === 'en' ? 'ar' : 'en';
    document.documentElement.lang = currentLang;
    document.documentElement.dir = currentLang === 'ar' ? 'rtl' : 'ltr';
    document.getElementById('currentLang').textContent = currentLang === 'en' ? '🇺🇸 EN' : '🇸🇦 AR';
    updateLanguage();
    renderAllSemesters();
}

// Update language
function updateLanguage() {
    document.querySelectorAll('[data-lang]').forEach(el => {
        const key = el.getAttribute('data-lang');
        if (translations[currentLang][key]) {
            if (el.tagName === 'INPUT' || el.tagName === 'TEXTAREA') {
                el.placeholder = translations[currentLang][key];
            } else {
                el.textContent = translations[currentLang][key];
            }
        }
    });
}

// Convert percentage to grade
function percentageToGrade(percentage) {
    for (const scale of GRADING) {
        if (percentage >= scale.min && percentage <= scale.max) {
            return {grade: scale.grade, points: scale.points};
        }
    }
    return {grade: 'F', points: 0.0};
}

// Calculate course grade
function calculateCourseGrade(obtained, total) {
    const percentage = (obtained / total) * 100;
    const gradeInfo = percentageToGrade(percentage);
    return {
        percentage: percentage.toFixed(2),
        grade: gradeInfo.grade,
        points: gradeInfo.points
    };
}

// Calculate semester GPA
function calculateSemesterGPA(semester) {
    const courses = COURSES[semester];
    if (!courses || !studentData[semester]) return 0;
    
    let totalPoints = 0;
    let totalHours = 0;
    
    courses.forEach(course => {
        if (studentData[semester][course.code]) {
            const marks = studentData[semester][course.code];
            const gradeInfo = calculateCourseGrade(marks.obtained, marks.total);
            totalPoints += gradeInfo.points * course.hours;
            totalHours += course.hours;
        }
    });
    
    return totalHours > 0 ? (totalPoints / totalHours).toFixed(2) : 0;
}

// Calculate overall GPA
function calculateOverallGPA() {
    let totalPoints = 0;
    let totalHours = 0;
    
    Object.keys(COURSES).forEach(semester => {
        const courses = COURSES[semester];
        courses.forEach(course => {
            if (studentData[semester] && studentData[semester][course.code]) {
                const marks = studentData[semester][course.code];
                const gradeInfo = calculateCourseGrade(marks.obtained, marks.total);
                totalPoints += gradeInfo.points * course.hours;
                totalHours += course.hours;
            }
        });
    });
    
    return totalHours > 0 ? (totalPoints / totalHours).toFixed(2) : 0;
}

// Get academic status
function getAcademicStatus(gpa) {
    if (gpa == 0) return currentLang === 'en' ? 'Not Started' : 'لم يبدأ';
    if (gpa >= 3.6) return currentLang === 'en' ? 'Excellent' : 'ممتاز';
    if (gpa >= 3.0) return currentLang === 'en' ? 'Very Good' : 'جيد جداً';
    if (gpa >= 2.4) return currentLang === 'en' ? 'Good' : 'جيد';
    if (gpa >= 2.0) return currentLang === 'en' ? 'Pass' : 'مقبول';
    return currentLang === 'en' ? 'At Risk' : 'في خطر';
}

// Calculate all GPAs and update dashboard
function calculateAllGPAs() {
    const overallGPA = calculateOverallGPA();
    document.getElementById('overallGPA').textContent = overallGPA;
    
    let totalCredits = 0;
    let completedCourses = 0;
    
    Object.keys(COURSES).forEach(semester => {
        COURSES[semester].forEach(course => {
            if (studentData[semester] && studentData[semester][course.code]) {
                totalCredits += course.hours;
                completedCourses++;
            }
        });
    });
    
    document.getElementById('totalCredits').textContent = totalCredits;
    document.getElementById('completedCourses').textContent = completedCourses;
    document.getElementById('academicStatus').textContent = getAcademicStatus(parseFloat(overallGPA));
    
    // Update analysis section
    updateAnalysis();
}

// Update analysis section
function updateAnalysis() {
    const overallGPA = calculateOverallGPA();
    const status = getAcademicStatus(parseFloat(overallGPA));
    
    let totalCredits = 0;
    let completedCourses = 0;
    let allGrades = [];
    let totalPercentage = 0;
    
    Object.keys(COURSES).forEach(semester => {
        COURSES[semester].forEach(course => {
            if (studentData[semester] && studentData[semester][course.code]) {
                const marks = studentData[semester][course.code];
                const gradeInfo = calculateCourseGrade(marks.obtained, marks.total);
                totalCredits += course.hours;
                completedCourses++;
                allGrades.push({
                    grade: gradeInfo.grade,
                    points: gradeInfo.points,
                    percentage: parseFloat(gradeInfo.percentage)
                });
                totalPercentage += parseFloat(gradeInfo.percentage);
            }
        });
    });
    
    document.getElementById('analysisGPA').textContent = overallGPA;
    document.getElementById('analysisStatus').textContent = status;
    document.getElementById('analysisCredits').textContent = totalCredits;
    document.getElementById('analysisCourses').textContent = completedCourses;
    
    if (allGrades.length > 0) {
        const highest = allGrades.reduce((max, g) => g.points > max.points ? g : max);
        const lowest = allGrades.reduce((min, g) => g.points < min.points ? g : min);
        const avgPercent = (totalPercentage / allGrades.length).toFixed(2);
        
        document.getElementById('analysisHighest').textContent = `${highest.grade} (${highest.percentage}%)`;
        document.getElementById('analysisLowest').textContent = `${lowest.grade} (${lowest.percentage}%)`;
        document.getElementById('analysisAvgPercent').textContent = `${avgPercent}%`;
    } else {
        document.getElementById('analysisHighest').textContent = '-';
        document.getElementById('analysisLowest').textContent = '-';
        document.getElementById('analysisAvgPercent').textContent = '0%';
    }
    
    // Add status color class
    const statusEl = document.getElementById('analysisStatus');
    statusEl.className = 'analysis-value';
    if (parseFloat(overallGPA) >= 3.6) statusEl.classList.add('status-excellent');
    else if (parseFloat(overallGPA) >= 3.0) statusEl.classList.add('status-very-good');
    else if (parseFloat(overallGPA) >= 2.4) statusEl.classList.add('status-good');
    else if (parseFloat(overallGPA) >= 2.0) statusEl.classList.add('status-pass');
    else statusEl.classList.add('status-risk');
}

// Render all semesters
function renderAllSemesters() {
    const container = document.getElementById('semestersContainer');
    container.innerHTML = '';
    
    const semesterNames = {
        first_1: currentLang === 'en' ? 'First Level – 1st Semester' : 'المستوى الأول – الفصل الأول',
        first_2: currentLang === 'en' ? 'First Level – 2nd Semester' : 'المستوى الأول – الفصل الثاني',
        second_1: currentLang === 'en' ? 'Second Level – 1st Semester' : 'المستوى الثاني – الفصل الأول',
        second_2: currentLang === 'en' ? 'Second Level – 2nd Semester' : 'المستوى الثاني – الفصل الثاني',
        third_1: currentLang === 'en' ? 'Third Level – 1st Semester' : 'المستوى الثالث – الفصل الأول',
        third_2: currentLang === 'en' ? 'Third Level – 2nd Semester' : 'المستوى الثالث – الفصل الثاني',
        fourth_1: currentLang === 'en' ? 'Fourth Level – 1st Semester' : 'المستوى الرابع – الفصل الأول',
        fourth_2: currentLang === 'en' ? 'Fourth Level – 2nd Semester' : 'المستوى الرابع – الفصل الثاني'
    };
    
    Object.keys(COURSES).forEach(semesterKey => {
        const courses = COURSES[semesterKey];
        const gpa = calculateSemesterGPA(semesterKey);
        const totalHours = courses.reduce((sum, c) => sum + c.hours, 0);
        
        const semesterDiv = document.createElement('div');
        semesterDiv.className = 'semester-bar';
        
        const coursesHTML = courses.map(course => {
            const marks = studentData[semesterKey] ? studentData[semesterKey][course.code] : null;
            const courseName = currentLang === 'ar' ? course.name_ar : course.name;
            
            let gradeHTML = '';
            if (marks) {
                const gradeInfo = calculateCourseGrade(marks.obtained, marks.total);
                const gradeClass = gradeInfo.grade.includes('A') ? 'grade-A' : 
                                 gradeInfo.grade.includes('B') ? 'grade-B' : 
                                 gradeInfo.grade.includes('C') ? 'grade-C' : 'grade-D';
                
                gradeHTML = `
                    <input type="number" class="course-input" value="${marks.obtained}" 
                           onchange="saveMarks('${semesterKey}','${course.code}',this.value,${course.total})" 
                           max="${course.total}" step="0.01">
                    <div class="grade-badge ${gradeClass}">${gradeInfo.grade}</div>
                    <div style="text-align:center;color:var(--text-secondary)">${gradeInfo.percentage}%</div>
                `;
            } else {
                gradeHTML = `
                    <input type="number" class="course-input" placeholder="0" 
                           onchange="saveMarks('${semesterKey}','${course.code}',this.value,${course.total})" 
                           max="${course.total}" step="0.01">
                    <div style="text-align:center;color:var(--text-secondary)">-</div>
                    <div style="text-align:center;color:var(--text-secondary)">-</div>
                `;
            }
            
            return `
                <div class="course-item">
                    <div class="course-info">
                        <div class="course-code">${course.code}</div>
                        <div class="course-name">${courseName}</div>
                        <div style="font-size:0.75rem;color:var(--text-secondary)">${course.hours}h • ${course.total} pts</div>
                    </div>
                    ${gradeHTML}
                </div>
            `;
        }).join('');
        
        semesterDiv.innerHTML = `
            <div class="semester-header" onclick="toggleSemester('${semesterKey}')">
                <div class="semester-info">
                    <i class="fas fa-chevron-right semester-icon" id="icon-${semesterKey}"></i>
                    <span class="semester-title">${semesterNames[semesterKey]}</span>
                </div>
                <div class="semester-stats">
                    <span style="color:var(--text-secondary);font-size:0.875rem">${totalHours}h</span>
                    <span class="semester-gpa">${gpa}</span>
                </div>
            </div>
            <div class="semester-details" id="details-${semesterKey}">
                ${coursesHTML}
            </div>
        `;
        
        container.appendChild(semesterDiv);
    });
}

// Toggle semester
function toggleSemester(semesterKey) {
    const details = document.getElementById(`details-${semesterKey}`);
    const bar = details.parentElement;
    
    if (details.classList.contains('expanded')) {
        details.classList.remove('expanded');
        bar.classList.remove('expanded');
    } else {
        details.classList.add('expanded');
        bar.classList.add('expanded');
    }
}

// Save marks
function saveMarks(semester, courseCode, obtained, total) {
    if (!obtained || obtained === '') return;
    
    obtained = parseFloat(obtained);
    if (obtained > total) {
        alert(`Grade cannot exceed ${total}`);
        renderAllSemesters();
        return;
    }
    
    if (!studentData[semester]) {
        studentData[semester] = {};
    }
    
    studentData[semester][courseCode] = {
        obtained: obtained,
        total: total
    };
    
    saveToStorage();
    renderAllSemesters();
    calculateAllGPAs();
}

// Import modal functions
function openImportModal() {
    document.getElementById('importModal').classList.add('active');
}

function closeImportModal() {
    document.getElementById('importModal').classList.remove('active');
}

// Process import
function processImport() {
    const data = document.getElementById('importData').value.trim();
    
    if (!data) {
        alert('⚠️ Please paste your grades data first!');
        return;
    }
    
    const lines = data.split('\n');
    let importCount = 0;
    
    for (const line of lines) {
        if (!line.trim()) continue;
        
        // Multiple patterns to catch different formats
        const patterns = [
            // Format: TL3012-Systematic pathology for technologists	3	129 / 150
            /([A-Z]+\d+[A-Z]*)\s*[-–—]\s*.+?\s+\d+\s+(\d+(?:\.\d+)?)\s*[\/\\]\s*(\d+)/i,
            // Format: TL309 — 184 / 200
            /([A-Z]+\d+[A-Z]*)\s*[—\-–:]\s*(\d+(?:\.\d+)?)\s*[\/\\]\s*(\d+)/i,
            // Format: TL309: 184 / 200
            /([A-Z]+\d+[A-Z]*)\s*:\s*(\d+(?:\.\d+)?)\s*[\/\\]\s*(\d+)/i,
            // Format with tabs: TL309	184 / 200
            /([A-Z]+\d+[A-Z]*)\s+(\d+(?:\.\d+)?)\s*[\/\\]\s*(\d+)/i,
            // Format: TL309 184/200
            /([A-Z]+\d+[A-Z]*)\s+(\d+(?:\.\d+)?)[\/\\](\d+)/i
        ];
        
        let match = null;
        for (const pattern of patterns) {
            match = line.match(pattern);
            if (match) break;
        }
        
        if (match) {
            const courseCode = match[1].toUpperCase().replace(/\s+/g, '');
            let obtained, total;
            
            // Find course in all semesters
            let foundSemester = null;
            let foundCourse = null;
            
            for (const [semester, courses] of Object.entries(COURSES)) {
                const course = courses.find(c => c.code === courseCode);
                if (course) {
                    foundSemester = semester;
                    foundCourse = course;
                    break;
                }
            }
            
            if (foundCourse) {
                obtained = parseFloat(match[2]);
                total = parseFloat(match[3]);
                
                if (obtained <= total && !isNaN(obtained) && !isNaN(total)) {
                    saveMarks(foundSemester, courseCode, obtained, total);
                    importCount++;
                }
            }
        }
    }
    
    closeImportModal();
    
    if (importCount > 0) {
        alert(`✅ Successfully imported ${importCount} grade${importCount > 1 ? 's' : ''}!`);
        document.getElementById('importData').value = '';
    } else {
        alert('❌ No valid grades found. Please check the format and try again.\n\nExample formats:\nTL309-Lab instrumentation\t4\t184 / 200\nTL309 — 184 / 200\nTHS101: 76 / 100');
    }
}

// Render charts
function renderCharts() {
    const semesterLabels = ['S1', 'S2', 'S3', 'S4', 'S5', 'S6', 'S7', 'S8'];
    const semesterKeys = Object.keys(COURSES);
    const gpaData = semesterKeys.map(key => calculateSemesterGPA(key));
    
    // GPA Trend Chart
    const gpaCtx = document.getElementById('gpaChart').getContext('2d');
    if (charts.gpaChart) charts.gpaChart.destroy();
    charts.gpaChart = new Chart(gpaCtx, {
        type: 'line',
        data: {
            labels: semesterLabels,
            datasets: [{
                label: 'GPA',
                data: gpaData,
                borderColor: '#5b8def',
                backgroundColor: 'rgba(91, 141, 239, 0.1)',
                tension: 0.4,
                fill: true,
                pointRadius: 5
            }]
        },
        options: {
            responsive: true,
            maintainAspectRatio: true,
            scales: {
                y: {
                    beginAtZero: true,
                    max: 4.0,
                    grid: {color: 'rgba(255, 255, 255, 0.05)'},
                    ticks: {color: '#94a3b8'}
                },
                x: {
                    grid: {color: 'rgba(255, 255, 255, 0.05)'},
                    ticks: {color: '#94a3b8'}
                }
            },
            plugins: {
                legend: {display: false}
            }
        }
    });
    
    // Grade Distribution Chart
    const gradeCtx = document.getElementById('gradeChart').getContext('2d');
    const gradeCount = {'A': 0, 'B': 0, 'C': 0, 'D': 0, 'F': 0};
    
    Object.keys(COURSES).forEach(semester => {
        COURSES[semester].forEach(course => {
            if (studentData[semester] && studentData[semester][course.code]) {
                const marks = studentData[semester][course.code];
                const gradeInfo = calculateCourseGrade(marks.obtained, marks.total);
                const gradeCategory = gradeInfo.grade.charAt(0);
                gradeCount[gradeCategory]++;
            }
        });
    });
    
    if (charts.gradeChart) charts.gradeChart.destroy();
    charts.gradeChart = new Chart(gradeCtx, {
        type: 'doughnut',
        data: {
            labels: Object.keys(gradeCount),
            datasets: [{
                data: Object.values(gradeCount),
                backgroundColor: ['#10b981', '#5b8def', '#f59e0b', '#ef4444', '#6b7280']
            }]
        },
        options: {
            responsive: true,
            plugins: {
                legend: {
                    position: 'bottom',
                    labels: {color: '#94a3b8'}
                }
            }
        }
    });
    
    // Credits per Semester Chart
    const creditCtx = document.getElementById('creditChart').getContext('2d');
    const creditData = semesterKeys.map(key => {
        const courses = COURSES[key];
        return courses.reduce((sum, c) => {
            if (studentData[key] && studentData[key][c.code]) {
                return sum + c.hours;
            }
            return sum;
        }, 0);
    });
    
    if (charts.creditChart) charts.creditChart.destroy();
    charts.creditChart = new Chart(creditCtx, {
        type: 'bar',
        data: {
            labels: semesterLabels,
            datasets: [{
                label: 'Credits',
                data: creditData,
                backgroundColor: '#5b8def',
                borderRadius: 5
            }]
        },
        options: {
            responsive: true,
            scales: {
                y: {
                    beginAtZero: true,
                    grid: {color: 'rgba(255, 255, 255, 0.05)'},
                    ticks: {color: '#94a3b8'}
                },
                x: {
                    grid: {color: 'rgba(255, 255, 255, 0.05)'},
                    ticks: {color: '#94a3b8'}
                }
            },
            plugins: {
                legend: {display: false}
            }
        }
    });
}

// Navigation
document.querySelectorAll('.menu-item[data-page]').forEach(item => {
    item.addEventListener('click', function() {
        const page = this.dataset.page;
        navigateToPage(page);
        document.getElementById('sidebar').classList.remove('mobile-open');
        document.getElementById('overlay').classList.remove('active');
    });
});

function navigateToPage(page) {
    document.querySelectorAll('.menu-item').forEach(item => {
        item.classList.remove('active');
    });
    document.querySelector(`.menu-item[data-page="${page}"]`).classList.add('active');
    
    document.querySelectorAll('.page-content').forEach(p => {
        p.classList.add('hidden');
    });
    document.getElementById(`${page}Page`).classList.remove('hidden');
    
    if (page === 'analysis') {
        setTimeout(() => renderCharts(), 100);
    }
}

// Mobile menu
document.getElementById('mobileMenuBtn').addEventListener('click', function() {
    document.getElementById('sidebar').classList.toggle('mobile-open');
    document.getElementById('overlay').classList.toggle('active');
});

document.getElementById('overlay').addEventListener('click', function() {
    document.getElementById('sidebar').classList.remove('mobile-open');
    this.classList.remove('active');
});

// Initialize
if (loadFromStorage() && studentData.name) {
    showApp();
}
</script>
</body>
</html>
