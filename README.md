<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HNU GPA - VIP Dashboard</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700;800;900&family=Cairo:wght@400;600;700;800&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
    <style>
:root{
--bg-primary:#1a1a1a;
--bg-secondary:#2d2d2d;
--bg-card:#242424;
--gold:#d4af37;
--gold-light:#e6c76f;
--gold-dark:#b8941f;
--text-primary:#fff;
--text-secondary:#999;
--border:#3a3a3a;
--shadow:rgba(212,175,55,0.3);
}
*{margin:0;padding:0;box-sizing:border-box;font-family:'Poppins',sans-serif !important}
body{background:#1a1a1a;color:#fff;overflow-x:hidden;font-weight:500}
body[dir="rtl"]{font-family:'Cairo',sans-serif !important}
body[dir="rtl"] *{font-family:'Cairo',sans-serif !important}
@keyframes fadeIn{from{opacity:0;transform:translateY(1.25rem)}to{opacity:1;transform:translateY(0)}}
@keyframes glow{0%,100%{box-shadow:0 0 1.25rem var(--shadow)}50%{box-shadow:0 0 2rem var(--shadow)}}
.auth-container{min-height:100vh;display:flex;align-items:center;justify-content:center;padding:5%;background:linear-gradient(180deg,#1a1a1a 0%,#2d2d2d 100%)}
.auth-card{background:#242424;border-radius:1.5rem;padding:3rem;max-width:26.25rem;width:100%;box-shadow:0 1.25rem 3.75rem rgba(0,0,0,.7);border:0.125rem solid var(--gold);animation:fadeIn .6s ease}
.auth-logo{width:5rem;height:5rem;background:linear-gradient(135deg,var(--gold),var(--gold-light));border-radius:50%;display:flex;align-items:center;justify-content:center;margin:0 auto 1.5rem;font-size:2.5rem;box-shadow:0 0.5rem 2rem var(--shadow)}
.auth-title{font-size:2rem;font-weight:800;margin-bottom:0.5rem;text-align:center;background:linear-gradient(135deg,var(--gold-light),var(--gold));-webkit-background-clip:text;-webkit-text-fill-color:transparent}
.auth-subtitle{color:var(--text-secondary);font-size:0.875rem;text-align:center;margin-bottom:2.5rem}
.form-group{margin-bottom:1.5rem}
.form-label{display:block;margin-bottom:0.75rem;font-weight:600;font-size:0.875rem;color:var(--gold);text-transform:uppercase;letter-spacing:0.05em}
.form-input{width:100%;padding:1rem;background:#2d2d2d;border:0.125rem solid var(--border);border-radius:0.75rem;color:#fff;font-size:0.9375rem;transition:all .3s ease}
.form-input:focus{outline:0;border-color:var(--gold);box-shadow:0 0 0 0.25rem var(--shadow)}
.btn-primary{width:100%;padding:1.125rem;background:linear-gradient(135deg,var(--gold),var(--gold-light));border:none;border-radius:0.75rem;color:#1a1a1a;font-size:1rem;font-weight:700;cursor:pointer;transition:all .3s ease;text-transform:uppercase;letter-spacing:0.05em}
.btn-primary:hover{transform:translateY(-0.125rem);box-shadow:0 0.75rem 2rem var(--shadow)}
.btn-reset{width:100%;padding:1rem;background:linear-gradient(135deg,#dc2626,#ef4444);border:none;border-radius:0.75rem;color:#fff;font-size:1rem;font-weight:700;cursor:pointer;margin-top:1.5rem;transition:all .3s ease;text-transform:uppercase;letter-spacing:0.05em}
.btn-reset:hover{transform:translateY(-0.125rem);box-shadow:0 0.75rem 2rem rgba(220,38,38,.4)}
.app-container{display:none}
.sidebar{position:fixed;left:0;top:0;height:100vh;width:17.5rem;background:linear-gradient(180deg,#1a1a1a 0%,#242424 100%);padding:1.5rem 0;overflow-y:auto;z-index:1000;border-right:0.125rem solid var(--gold);display:flex;flex-direction:column;box-shadow:0.25rem 0 2rem rgba(0,0,0,.5);transition:transform 0.3s ease}
body[dir="rtl"] .sidebar{left:auto;right:0;border-right:none;border-left:0.125rem solid var(--gold)}
.sidebar.mobile-open{transform:translateX(0) !important}
.sidebar-header{padding:1.5rem;border-top:0.125rem solid var(--gold);border-bottom:none;margin-bottom:0.5rem}
.logo-icon{width:3rem;height:3rem;background:linear-gradient(135deg,var(--gold),var(--gold-light));border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:1.5rem;margin-bottom:0.75rem;box-shadow:0 0.25rem 1rem var(--shadow)}
.sidebar-title{font-size:1.125rem;font-weight:700;background:linear-gradient(135deg,var(--gold-light),var(--gold));-webkit-background-clip:text;-webkit-text-fill-color:transparent}
.sidebar-subtitle{font-size:0.75rem;color:var(--text-secondary);margin-top:0.25rem}
.menu-item{display:flex;align-items:center;gap:1rem;padding:0.875rem 1.5rem;margin:0 0.75rem 0.5rem;border-radius:0.75rem;cursor:pointer;transition:all .3s ease;color:var(--text-secondary);position:relative}
.menu-item:hover{background:rgba(212,175,55,0.1);color:var(--gold-light)}
.menu-item.active{background:linear-gradient(135deg,var(--gold),var(--gold-light));color:#1a1a1a;box-shadow:0 0.25rem 1rem var(--shadow)}
.menu-icon{font-size:1.25rem;width:1.5rem}
.main-content{margin-left:17.5rem;padding:2rem;min-height:100vh}
body[dir="rtl"] .main-content{margin-left:0;margin-right:17.5rem}
.top-bar{display:flex;justify-content:space-between;align-items:center;margin-bottom:2.5rem;flex-wrap:wrap;gap:1.5rem;padding:2rem;background:linear-gradient(135deg,var(--gold),var(--gold-light));border-radius:1.25rem;box-shadow:0 0.5rem 2rem var(--shadow)}
.greeting{display:flex;flex-direction:column;gap:0.5rem}
.greeting-name{font-size:2rem;font-weight:800;color:#1a1a1a}
.greeting-info{color:#2d2d2d;font-size:0.875rem;font-weight:600}
.action-btns{display:flex;gap:0.75rem;flex-wrap:wrap}
.btn{padding:0.75rem 1.5rem;border-radius:0.625rem;border:none;cursor:pointer;font-weight:600;font-size:0.875rem;transition:all .3s ease;text-transform:uppercase;letter-spacing:0.05em}
.btn-outline{background:#1a1a1a;border:0.125rem solid var(--gold-dark);color:var(--gold)}
.btn-outline:hover{background:var(--gold-dark);color:#1a1a1a;box-shadow:0 0.25rem 1rem var(--shadow)}
.stats-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(15.625rem,1fr));gap:1.5rem;margin-bottom:2.5rem}
.stat-card{background:linear-gradient(135deg,var(--gold),var(--gold-light));padding:2rem;border-radius:1.25rem;animation:fadeIn .6s ease;position:relative;overflow:hidden;box-shadow:0 0.5rem 2rem var(--shadow)}
.stat-label{color:#2d2d2d;font-size:0.75rem;margin-bottom:0.75rem;text-transform:uppercase;letter-spacing:0.1em;font-weight:700}
.stat-value{font-size:2.5rem;font-weight:800;margin-bottom:0.5rem;color:#1a1a1a}
.stat-status{color:#2d2d2d !important;font-weight:700;font-size:0.875rem}
.page-content{animation:fadeIn .6s ease}
.page-content.hidden{display:none}
.semester-bar{background:var(--bg-card);border-radius:1.25rem;margin-bottom:1.25rem;border:0.125rem solid var(--gold);overflow:hidden;animation:fadeIn .6s ease;transition:all .3s ease;box-shadow:0 0.25rem 1.5rem rgba(0,0,0,.3)}
.semester-bar:hover{box-shadow:0 0.5rem 2rem var(--shadow)}
.semester-header{padding:1.5rem 2rem;cursor:pointer;display:flex;justify-content:space-between;align-items:center;transition:all .3s ease;background:linear-gradient(90deg,transparent,rgba(212,175,55,0.05),transparent)}
.semester-header:hover{background:rgba(212,175,55,0.1)}
.semester-info{display:flex;align-items:center;gap:1rem}
.semester-icon{transition:transform .3s ease;color:var(--gold);font-size:1.125rem}
.semester-bar.expanded .semester-icon{transform:rotate(90deg)}
body[dir="rtl"] .semester-bar.expanded .semester-icon{transform:rotate(-90deg)}
.semester-title{font-size:1.25rem;font-weight:700;color:var(--gold-light)}
.semester-stats{display:flex;gap:2rem;align-items:center}
.semester-gpa{font-size:1.75rem;font-weight:800;background:linear-gradient(135deg,var(--gold),var(--gold-light));-webkit-background-clip:text;-webkit-text-fill-color:transparent}
.semester-details{max-height:0;overflow:hidden;transition:max-height .4s ease}
.semester-details.expanded{max-height:200rem;padding:0 2rem 2rem}
.course-item{display:grid;grid-template-columns:2fr 1fr 1fr 1fr;gap:1.5rem;padding:1.25rem;background:#2d2d2d;border-radius:0.875rem;margin-bottom:1rem;align-items:center;border:0.125rem solid var(--border);transition:all .3s ease}
.course-item:hover{border-color:var(--gold);background:rgba(212,175,55,0.05)}
.course-info{display:flex;flex-direction:column;gap:0.375rem}
.course-code{font-weight:700;color:var(--gold);font-size:0.875rem;text-transform:uppercase;letter-spacing:0.05em}
.course-name{font-size:1rem;font-weight:600;color:#fff}
.course-input{padding:0.75rem;background:#1a1a1a;border:0.125rem solid var(--border);border-radius:0.625rem;color:#fff;text-align:center;font-size:0.9375rem;width:100%;font-weight:600;transition:all .3s ease}
.course-input:focus{outline:0;border-color:var(--gold);box-shadow:0 0 0 0.25rem var(--shadow)}
.course-input[readonly]{background:var(--bg-card);cursor:default;border-color:transparent}
.grade-badge{padding:0.5rem 1rem;border-radius:0.625rem;font-weight:700;text-align:center;font-size:0.9375rem;text-transform:uppercase;letter-spacing:0.05em}
.grade-A{background:linear-gradient(135deg,var(--gold),var(--gold-light));color:#1a1a1a;box-shadow:0 0.25rem 1rem var(--shadow)}
.grade-B{background:linear-gradient(135deg,#c0c0c0,#e8e8e8);color:#1a1a1a;box-shadow:0 0.25rem 1rem rgba(192,192,192,0.3)}
.grade-C{background:linear-gradient(135deg,#cd7f32,#e6a85c);color:#1a1a1a;box-shadow:0 0.25rem 1rem rgba(205,127,50,0.3)}
.grade-D{background:linear-gradient(135deg,#ef4444,#f87171);color:#fff;box-shadow:0 0.25rem 1rem rgba(239,68,68,0.3)}
.charts-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(25rem,1fr));gap:2rem;margin-bottom:2rem}
.chart-card{background:var(--bg-card);padding:2rem;border-radius:1.25rem;border:0.125rem solid var(--gold);box-shadow:0 0.25rem 1.5rem rgba(0,0,0,.3);position:relative;overflow:hidden}
.chart-title{font-size:0.875rem;font-weight:700;margin-bottom:1.5rem;color:var(--gold);text-transform:uppercase;letter-spacing:0.1em;display:flex;align-items:center;gap:0.5rem}
.chart-wrapper{position:relative;height:20rem}
.modal{position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,.8);display:none;align-items:center;justify-content:center;z-index:2000;padding:5%;backdrop-filter:blur(0.625rem)}
.modal.active{display:flex}
.modal-content{background:var(--bg-card);padding:2.5rem;border-radius:1.5rem;max-width:40rem;width:100%;border:0.125rem solid var(--gold);box-shadow:0 2rem 4rem rgba(0,0,0,.7),0 0 2rem var(--shadow)}
.modal-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:2rem;padding-bottom:1rem;border-bottom:0.125rem solid var(--gold)}
.modal-title{font-size:1.75rem;font-weight:800;background:linear-gradient(135deg,var(--gold-light),var(--gold));-webkit-background-clip:text;-webkit-text-fill-color:transparent}
.close-btn{background:none;border:none;font-size:1.75rem;color:var(--text-secondary);cursor:pointer;padding:0;width:2.5rem;height:2.5rem;display:flex;align-items:center;justify-content:center;transition:all .3s ease;border-radius:0.5rem}
.close-btn:hover{color:var(--gold-light);background:rgba(212,175,55,0.1)}
textarea{width:100%;min-height:15rem;padding:1.25rem;background:#2d2d2d;border:0.125rem solid var(--border);border-radius:0.875rem;color:#fff;font-family:'Courier New',monospace !important;font-size:0.875rem;resize:vertical;transition:all .3s ease}
textarea:focus{outline:0;border-color:var(--gold);box-shadow:0 0 0 0.25rem var(--shadow)}
.overlay{position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,.7);display:none;z-index:999;backdrop-filter:blur(0.3125rem)}
.overlay.active{display:block}
.analysis-summary{background:var(--bg-card);padding:2rem;border-radius:1.25rem;border:0.125rem solid var(--gold);margin-bottom:2rem;box-shadow:0 0.25rem 1.5rem rgba(0,0,0,.3)}
.analysis-row{display:flex;justify-content:space-between;padding:1rem 0;border-bottom:0.125rem solid var(--border)}
.analysis-row:last-child{border-bottom:none}
.analysis-label{color:var(--text-secondary);font-size:0.9375rem;font-weight:600;text-transform:uppercase;letter-spacing:0.05em}
.analysis-value{font-weight:700;font-size:1.125rem;color:var(--gold-light)}
.developer-credit{text-align:center;margin-top:2rem;padding:1.5rem;background:var(--bg-card);border-radius:1rem;border:0.125rem solid var(--gold);box-shadow:0 0.25rem 1.5rem rgba(0,0,0,.3)}
.developer-label{color:var(--text-secondary);font-size:0.75rem;margin-bottom:0.5rem;letter-spacing:0.15em;font-weight:600}
.developer-name{font-size:0.95rem;font-weight:900;background:linear-gradient(90deg,var(--gold),var(--gold-light),var(--gold-dark),var(--gold));background-size:300% 300%;-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;animation:sparkleGradient 4s ease-in-out infinite;filter:drop-shadow(0 0 0.5rem var(--shadow));letter-spacing:0.2em;font-family:'Impact','Western',serif !important;text-transform:uppercase}
@keyframes sparkleGradient{0%,100%{background-position:0% 50%}25%{background-position:50% 50%}50%{background-position:100% 50%}75%{background-position:50% 50%}}
.info-hint{margin-top:1rem;padding:0.75rem;background:rgba(212,175,55,0.1);border-left:0.25rem solid var(--gold);border-radius:0.5rem;font-size:0.75rem;color:var(--gold-light);display:flex;align-items:center;gap:0.5rem}
@media(max-width:64rem){
.charts-grid{grid-template-columns:1fr}
}
@media(max-width:48rem){
.sidebar{transform:translateX(-100%)}
body[dir="rtl"] .sidebar{transform:translateX(100%)}
.sidebar.mobile-open{transform:translateX(0)}
.main-content{margin-left:0;padding:1rem}
body[dir="rtl"] .main-content{margin-right:0}
.mobile-menu-btn{display:flex}
.course-item{grid-template-columns:1fr;gap:1rem}
.stat-value{font-size:2rem}
.greeting-name{font-size:1.5rem}
.charts-grid{grid-template-columns:1fr}
.chart-wrapper{height:15rem}
}
.mobile-menu-btn{display:none;position:fixed;bottom:1.5rem;right:1.5rem;width:3.75rem;height:3.75rem;background:linear-gradient(135deg,var(--gold),var(--gold-light));border:none;border-radius:50%;color:#1a1a1a;font-size:1.5rem;cursor:pointer;box-shadow:0 0.5rem 1.5rem var(--shadow);z-index:1001;animation:glow 2s ease-in-out infinite;display:flex;align-items:center;justify-content:center}
body[dir="rtl"] .mobile-menu-btn{right:auto;left:1.5rem}
@media(max-width:48rem){
.mobile-menu-btn{display:flex}
}
</style>
</head>
<body dir="ltr">

<!-- Authentication Screen -->
<div id="authScreen" class="auth-container">
    <div class="auth-card">
        <div class="auth-logo">🎓</div>
        <h1 class="auth-title" data-lang="welcome">Welcome</h1>
        <p class="auth-subtitle" data-lang="auth_subtitle">Enter your name to access VIP dashboard</p>
        <form id="authForm" onsubmit="handleAuth(event)">
            <div class="form-group">
                <label class="form-label" data-lang="name">Student Name</label>
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
            <span class="menu-icon">🏠</span>
            <span data-lang="dashboard">Dashboard</span>
        </div>
        <div class="menu-item" data-page="courses">
            <span class="menu-icon">📚</span>
            <span data-lang="courses">Courses</span>
        </div>
        <div class="menu-item" data-page="analytics">
            <span class="menu-icon">📊</span>
            <span data-lang="analytics">Analytics</span>
        </div>
        
        <div style="flex:1;min-height:2rem"></div>
        
        <div class="sidebar-header">
            <div class="logo-icon">🎓</div>
            <div class="sidebar-title" data-lang="app_title">HNU GPA</div>
            <div class="sidebar-subtitle" id="studentNameDisplay"></div>
        </div>
        <div class="menu-item" onclick="logout()">
            <span class="menu-icon">🚪</span>
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
                    <span>📥 </span><span data-lang="import">Import Grades</span>
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
                    <div class="stat-value" id="overallGPA">0.00</div>
                    <div class="stat-status" id="academicStatus">Not Started</div>
                    <div class="info-hint" style="background:#1a1a1a;border-color:#1a1a1a;color:#2d2d2d">
                        <span>ℹ️ </span><span data-lang="gpa_hint">Go to Courses section for customization</span>
                    </div>
                </div>
                <div class="stat-card">
                    <div class="stat-label" data-lang="total_credits">Total Credits</div>
                    <div class="stat-value" id="totalCredits">0</div>
                </div>
                <div class="stat-card">
                    <div class="stat-label" data-lang="completed_courses">Completed Courses</div>
                    <div class="stat-value" id="completedCourses">0</div>
                </div>
            </div>
            <button class="btn-reset" onclick="resetAllData()">
                <span>🔄 </span><span data-lang="reset">Reset Everything</span>
            </button>
            <div class="developer-credit">
                <div class="developer-label">DEVELOPER</div>
                <div class="developer-name">Mohand Ahmed</div>
            </div>
        </div>

        <!-- Courses Page -->
        <div id="coursesPage" class="page-content hidden">
            <div id="semestersContainer"></div>
        </div>

        <!-- Analytics Page -->
        <div id="analyticsPage" class="page-content hidden">
            <!-- Charts Grid -->
            <div class="charts-grid">
                <div class="chart-card">
                    <h3 class="chart-title" data-lang="semester_performance">📊 Semester Performance</h3>
                    <div class="chart-wrapper">
                        <canvas id="semesterBarChart"></canvas>
                    </div>
                </div>

                <div class="chart-card">
                    <h3 class="chart-title" data-lang="gpa_trend">📈 GPA Trend Analysis</h3>
                    <div class="chart-wrapper">
                        <canvas id="gpaTrendChart"></canvas>
                    </div>
                </div>

                <div class="chart-card">
                    <h3 class="chart-title" data-lang="credits_dist">💳 Credits Distribution</h3>
                    <div class="chart-wrapper">
                        <canvas id="creditsChart"></canvas>
                    </div>
                </div>

                <div class="chart-card">
                    <h3 class="chart-title" data-lang="grade_comparison">🏆 Grade Level Comparison</h3>
                    <div class="chart-wrapper">
                        <canvas id="gradeComparisonChart"></canvas>
                    </div>
                </div>

                <div class="chart-card">
                    <h3 class="chart-title" data-lang="cumulative_progress">📉 Cumulative Progress</h3>
                    <div class="chart-wrapper">
                        <canvas id="areaChart"></canvas>
                    </div>
                </div>

                <div class="chart-card">
                    <h3 class="chart-title" data-lang="course_scatter">🎯 Course Performance Matrix</h3>
                    <div class="chart-wrapper">
                        <canvas id="scatterChart"></canvas>
                    </div>
                </div>

                <div class="chart-card">
                    <h3 class="chart-title" data-lang="grade_distribution">🍩 Grade Distribution</h3>
                    <div class="chart-wrapper">
                        <canvas id="doughnutChart"></canvas>
                    </div>
                </div>

                <div class="chart-card">
                    <h3 class="chart-title" data-lang="semester_radar">📡 Semester Radar Analysis</h3>
                    <div class="chart-wrapper">
                        <canvas id="radarChart"></canvas>
                    </div>
                </div>

                <div class="chart-card">
                    <h3 class="chart-title" data-lang="overall_progress">⚡ Overall Performance Score</h3>
                    <div class="chart-wrapper">
                        <canvas id="gaugeChart"></canvas>
                    </div>
                </div>
            </div>

            <!-- Performance Summary -->
            <div class="analysis-summary">
                <h2 class="chart-title" data-lang="performance_summary">📋 Performance Summary</h2>
                <div class="analysis-row">
                    <span class="analysis-label" data-lang="overall_gpa">Overall GPA</span>
                    <span class="analysis-value" style="background:linear-gradient(135deg,var(--gold),var(--gold-light));-webkit-background-clip:text;-webkit-text-fill-color:transparent;font-size:1.5rem" id="analysisGPA">0.00</span>
                </div>
                <div class="analysis-row">
                    <span class="analysis-label" data-lang="academic_grade">Academic Grade</span>
                    <span class="analysis-value" style="background:linear-gradient(135deg,var(--gold),var(--gold-light));-webkit-background-clip:text;-webkit-text-fill-color:transparent;font-size:1.5rem" id="analysisGrade">-</span>
                </div>
                <div class="analysis-row">
                    <span class="analysis-label" data-lang="academic_status">Academic Status</span>
                    <span class="analysis-value" id="analysisStatus">Not Started</span>
                </div>
                <div class="analysis-row">
                    <span class="analysis-label" data-lang="overall_percentage">Overall Percentage</span>
                    <span class="analysis-value" style="background:linear-gradient(135deg,var(--gold),var(--gold-light));-webkit-background-clip:text;-webkit-text-fill-color:transparent;font-size:1.5rem" id="analysisOverallPercent">0%</span>
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
        </div>
    </div>

    <!-- Mobile Menu Button -->
    <button id="mobileMenuBtn" class="mobile-menu-btn">☰</button>

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
        <p style="color:var(--text-secondary);margin-bottom:1.5rem;font-size:0.875rem" data-lang="import_instructions">Paste your grades data below (from HNU website or formatted text)</p>
        <textarea id="importData" placeholder="TL309-Laboratories instrumentation&#10;4&#10;184 / 200"></textarea>
        <button class="btn-primary" style="margin-top:1.5rem" onclick="processImport()">
            <span>📤 </span><span data-lang="import">Import</span>
        </button>
    </div>
</div>

<script>
// [CONTINUING WITH FULL JAVASCRIPT CODE - SAME AS BEFORE BUT WITH GOLD THEME FOR CHARTS]

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

// Complete Course Data
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
        auth_subtitle: 'Enter your name to access VIP dashboard',
        name: 'Student Name',
        name_placeholder: 'Enter your full name',
        continue: 'Continue',
        app_title: 'HNU GPA',
        dashboard: 'Dashboard',
        courses: 'Courses',
        analytics: 'Analytics',
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
        gpa_hint: 'Go to Courses section for customization',
        semester_performance: 'Semester Performance',
        gpa_trend: 'GPA Trend Analysis',
        credits_dist: 'Credits Distribution',
        grade_comparison: 'Grade Level Comparison',
        cumulative_progress: 'Cumulative Progress',
        course_scatter: 'Course Performance Matrix',
        grade_distribution: 'Grade Distribution',
        semester_radar: 'Semester Radar Analysis',
        overall_progress: 'Overall Performance Score',
        academic_grade: 'Academic Grade',
        overall_percentage: 'Overall Percentage'
    },
    ar: {
        welcome: 'مرحباً',
        auth_subtitle: 'أدخل اسمك للوصول إلى لوحة VIP',
        name: 'اسم الطالب',
        name_placeholder: 'أدخل اسمك الكامل',
        continue: 'متابعة',
        app_title: 'حاسبة المعدل التراكمي',
        dashboard: 'لوحة التحكم',
        courses: 'المقررات',
        analytics: 'التحليلات',
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
        gpa_hint: 'انتقل إلى قسم المقررات للتخصيص',
        semester_performance: 'أداء الفصول الدراسية',
        gpa_trend: 'تحليل اتجاه المعدل',
        credits_dist: 'توزيع الساعات',
        grade_comparison: 'مقارنة مستويات الدرجات',
        cumulative_progress: 'التقدم التراكمي',
        course_scatter: 'مصفوفة أداء المقررات',
        grade_distribution: 'توزيع الدرجات',
        semester_radar: 'تحليل رادار الفصول',
        overall_progress: 'درجة الأداء الإجمالي',
        academic_grade: 'الدرجة الأكاديمية',
        overall_percentage: 'النسبة الإجمالية'
    }
};

// Global Variables
let studentData = {};
let currentLang = 'en';
let charts = {};

// Chart.js default config with gold theme
Chart.defaults.color = '#999';
Chart.defaults.borderColor = '#3a3a3a';

// Load/Save/Auth functions
function loadFromStorage() {
    const saved = localStorage.getItem('hnu_student_data');
    if (saved) {
        studentData = JSON.parse(saved);
        return true;
    }
    return false;
}

function saveToStorage() {
    localStorage.setItem('hnu_student_data', JSON.stringify(studentData));
}

function handleAuth(event) {
    event.preventDefault();
    const name = document.getElementById('studentName').value.trim();
    if (name) {
        studentData.name = name;
        saveToStorage();
        showApp();
    }
}

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

function logout() {
    if (confirm('Are you sure you want to logout?')) {
        localStorage.removeItem('hnu_student_data');
        location.reload();
    }
}

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

function toggleLanguage() {
    currentLang = currentLang === 'en' ? 'ar' : 'en';
    document.documentElement.lang = currentLang;
    document.documentElement.dir = currentLang === 'ar' ? 'rtl' : 'ltr';
    document.getElementById('currentLang').textContent = currentLang === 'en' ? '🇺🇸 EN' : '🇸🇦 AR';
    updateLanguage();
    renderAllSemesters();
}

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

function percentageToGrade(percentage) {
    for (const scale of GRADING) {
        if (percentage >= scale.min && percentage <= scale.max) {
            return {grade: scale.grade, points: scale.points};
        }
    }
    return {grade: 'F', points: 0.0};
}

function calculateCourseGrade(obtained, total) {
    const percentage = (obtained / total) * 100;
    const gradeInfo = percentageToGrade(percentage);
    return {
        percentage: percentage.toFixed(2),
        grade: gradeInfo.grade,
        points: gradeInfo.points
    };
}

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

function getAcademicStatus(gpa) {
    if (gpa == 0) return currentLang === 'en' ? 'Not Started' : 'لم يبدأ';
    if (gpa >= 3.6) return currentLang === 'en' ? 'Excellent' : 'ممتاز';
    if (gpa >= 3.0) return currentLang === 'en' ? 'Very Good' : 'جيد جداً';
    if (gpa >= 2.4) return currentLang === 'en' ? 'Good' : 'جيد';
    if (gpa >= 2.0) return currentLang === 'en' ? 'Pass' : 'مقبول';
    return currentLang === 'en' ? 'At Risk' : 'في خطر';
}

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
    
    updateAnalysis();
}

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
    
    const gpaNum = parseFloat(overallGPA);
    let academicGrade = '-';
    if (gpaNum >= 3.85) academicGrade = 'A+';
    else if (gpaNum >= 3.7) academicGrade = 'A';
    else if (gpaNum >= 3.5) academicGrade = 'A-';
    else if (gpaNum >= 3.3) academicGrade = 'B+';
    else if (gpaNum >= 3.1) academicGrade = 'B';
    else if (gpaNum >= 2.9) academicGrade = 'B-';
    else if (gpaNum >= 2.7) academicGrade = 'C+';
    else if (gpaNum >= 2.5) academicGrade = 'C';
    else if (gpaNum >= 2.3) academicGrade = 'C-';
    else if (gpaNum >= 2.1) academicGrade = 'D+';
    else if (gpaNum >= 2.0) academicGrade = 'D';
    else if (gpaNum > 0) academicGrade = 'F';
    
    const overallPercent = allGrades.length > 0 ? (totalPercentage / allGrades.length).toFixed(2) : 0;
    
    document.getElementById('analysisGPA').textContent = overallGPA;
    document.getElementById('analysisGrade').textContent = academicGrade;
    document.getElementById('analysisStatus').textContent = status;
    document.getElementById('analysisOverallPercent').textContent = `${overallPercent}%`;
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
}

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
                    <div style="text-align:center;color:var(--text-secondary);font-weight:600">${gradeInfo.percentage}%</div>
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
                        <div style="font-size:0.75rem;color:var(--text-secondary);margin-top:0.25rem">${course.hours}h • ${course.total} pts</div>
                    </div>
                    ${gradeHTML}
                </div>
            `;
        }).join('');
        
        semesterDiv.innerHTML = `
            <div class="semester-header" onclick="toggleSemester('${semesterKey}')">
                <div class="semester-info">
                    <span class="semester-icon">▶</span>
                    <span class="semester-title">${semesterNames[semesterKey]}</span>
                </div>
                <div class="semester-stats">
                    <span style="color:var(--text-secondary);font-size:0.875rem;font-weight:600">${totalHours}h</span>
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

function openImportModal() {
    document.getElementById('importModal').classList.add('active');
}

function closeImportModal() {
    document.getElementById('importModal').classList.remove('active');
}

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
        
        const patterns = [
            /([A-Z]+\d+[A-Z]*)\s*[-–—]\s*.+?\s+\d+\s+(\d+(?:\.\d+)?)\s*[\/\\]\s*(\d+)/i,
            /([A-Z]+\d+[A-Z]*)\s*[—\-–:]\s*(\d+(?:\.\d+)?)\s*[\/\\]\s*(\d+)/i,
            /([A-Z]+\d+[A-Z]*)\s*:\s*(\d+(?:\.\d+)?)\s*[\/\\]\s*(\d+)/i,
            /([A-Z]+\d+[A-Z]*)\s+(\d+(?:\.\d+)?)\s*[\/\\]\s*(\d+)/i,
            /([A-Z]+\d+[A-Z]*)\s+(\d+(?:\.\d+)?)[\/\\](\d+)/i
        ];
        
        let match = null;
        for (const pattern of patterns) {
            match = line.match(pattern);
            if (match) break;
        }
        
        if (match) {
            const courseCode = match[1].toUpperCase().replace(/\s+/g, '');
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
                const obtained = parseFloat(match[2]);
                const total = parseFloat(match[3]);
                
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
        alert('❌ No valid grades found.');
    }
}

// Render charts with gold theme
function renderCharts() {
    const semesterLabels = ['S1', 'S2', 'S3', 'S4', 'S5', 'S6', 'S7', 'S8'];
    const semesterKeys = Object.keys(COURSES);
    const gpaData = semesterKeys.map(key => parseFloat(calculateSemesterGPA(key)));
    
    // All charts use gold color scheme
    const goldColor = '#d4af37';
    const goldLight = '#e6c76f';
    
    // 1. Semester Bar Chart
    const semesterBarCtx = document.getElementById('semesterBarChart').getContext('2d');
    if (charts.semesterBar) charts.semesterBar.destroy();
    charts.semesterBar = new Chart(semesterBarCtx, {
        type: 'bar',
        data: {
            labels: semesterLabels,
            datasets: [{
                label: 'GPA',
                data: gpaData,
                backgroundColor: goldColor,
                borderColor: goldLight,
                borderWidth: 2,
                borderRadius: 8
            }]
        },
        options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {legend: {display: false}},
            scales: {
                y: {beginAtZero: true, max: 4.0, grid: {color: '#3a3a3a'}},
                x: {grid: {display: false}}
            }
        }
    });
    
    // 2. GPA Trend Line
    const gpaTrendCtx = document.getElementById('gpaTrendChart').getContext('2d');
    if (charts.gpaTrend) charts.gpaTrend.destroy();
    charts.gpaTrend = new Chart(gpaTrendCtx, {
        type: 'line',
        data: {
            labels: semesterLabels,
            datasets: [{
                data: gpaData,
                borderColor: goldColor,
                backgroundColor: 'transparent',
                tension: 0.4,
                borderWidth: 3,
                pointBackgroundColor: goldColor
            }]
        },
        options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {legend: {display: false}},
            scales: {
                y: {beginAtZero: true, max: 4.0, grid: {color: '#3a3a3a'}},
                x: {grid: {color: '#3a3a3a'}}
            }
        }
    });
    
    // 3. Credits Distribution
    const creditsData = semesterKeys.map(key => {
        return COURSES[key].reduce((sum, c) => {
            if (studentData[key] && studentData[key][c.code]) return sum + c.hours;
            return sum;
        }, 0);
    });
    
    const creditsCtx = document.getElementById('creditsChart').getContext('2d');
    if (charts.credits) charts.credits.destroy();
    charts.credits = new Chart(creditsCtx, {
        type: 'bar',
        data: {
            labels: semesterLabels,
            datasets: [{data: creditsData, backgroundColor: goldLight, borderRadius: 8}]
        },
        options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {legend: {display: false}},
            scales: {y: {beginAtZero: true, grid: {color: '#3a3a3a'}}, x: {grid: {display: false}}}
        }
    });
    
    // 4. Grade Comparison
    const gradeComparisonCtx = document.getElementById('gradeComparisonChart').getContext('2d');
    if (charts.gradeComparison) charts.gradeComparison.destroy();
    charts.gradeComparison = new Chart(gradeComparisonCtx, {
        type: 'bar',
        data: {
            labels: semesterLabels,
            datasets: [{
                data: gpaData,
                backgroundColor: gpaData.map(gpa => gpa >= 3.6 ? goldColor : gpa >= 3.0 ? goldLight : gpa >= 2.4 ? '#c0c0c0' : '#cd7f32'),
                borderRadius: 8
            }]
        },
        options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {legend: {display: false}},
            scales: {y: {beginAtZero: true, max: 4.0, grid: {color: '#3a3a3a'}}, x: {grid: {display: false}}}
        }
    });
    
    // 5. Area Chart
    const cumulativeGPA = gpaData.map((_, index) => {
        const slice = gpaData.slice(0, index + 1).filter(v => v > 0);
        return slice.length > 0 ? (slice.reduce((a, b) => a + b, 0) / slice.length).toFixed(2) : 0;
    });
    
    const areaCtx = document.getElementById('areaChart').getContext('2d');
    if (charts.area) charts.area.destroy();
    charts.area = new Chart(areaCtx, {
        type: 'line',
        data: {
            labels: semesterLabels,
            datasets: [{
                data: cumulativeGPA,
                borderColor: goldColor,
                backgroundColor: (context) => {
                    const ctx = context.chart.ctx;
                    const gradient = ctx.createLinearGradient(0, 0, 0, 300);
                    gradient.addColorStop(0, 'rgba(212, 175, 55, 0.5)');
                    gradient.addColorStop(1, 'rgba(212, 175, 55, 0.0)');
                    return gradient;
                },
                fill: true,
                tension: 0.4,
                borderWidth: 3
            }]
        },
        options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {legend: {display: false}},
            scales: {y: {beginAtZero: true, max: 4.0, grid: {color: '#3a3a3a'}}, x: {grid: {color: '#3a3a3a'}}}
        }
    });
    
    // 6. Scatter Plot
    const scatterData = [];
    Object.keys(COURSES).forEach((semester, sIndex) => {
        COURSES[semester].forEach(course => {
            if (studentData[semester] && studentData[semester][course.code]) {
                const marks = studentData[semester][course.code];
                const gradeInfo = calculateCourseGrade(marks.obtained, marks.total);
                scatterData.push({x: sIndex + 1, y: gradeInfo.points, r: course.hours * 3});
            }
        });
    });
    
    const scatterCtx = document.getElementById('scatterChart').getContext('2d');
    if (charts.scatter) charts.scatter.destroy();
    charts.scatter = new Chart(scatterCtx, {
        type: 'bubble',
        data: {datasets: [{data: scatterData, backgroundColor: 'rgba(212, 175, 55, 0.6)', borderColor: goldLight, borderWidth: 2}]},
        options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {legend: {display: false}},
            scales: {y: {beginAtZero: true, max: 4.0, grid: {color: '#3a3a3a'}}, x: {grid: {color: '#3a3a3a'}}}
        }
    });
    
    // 7. Doughnut Chart
    const gradeCount = {'A': 0, 'B': 0, 'C': 0, 'D': 0, 'F': 0};
    Object.keys(COURSES).forEach(semester => {
        COURSES[semester].forEach(course => {
            if (studentData[semester] && studentData[semester][course.code]) {
                const marks = studentData[semester][course.code];
                const gradeInfo = calculateCourseGrade(marks.obtained, marks.total);
                gradeCount[gradeInfo.grade.charAt(0)]++;
            }
        });
    });
    
    const doughnutCtx = document.getElementById('doughnutChart').getContext('2d');
    if (charts.doughnut) charts.doughnut.destroy();
    charts.doughnut = new Chart(doughnutCtx, {
        type: 'doughnut',
        data: {
            labels: Object.keys(gradeCount),
            datasets: [{
                data: Object.values(gradeCount),
                backgroundColor: [goldColor, goldLight, '#c0c0c0', '#cd7f32', '#6b7280'],
                borderColor: '#242424',
                borderWidth: 3
            }]
        },
        options: {responsive: true, maintainAspectRatio: false, plugins: {legend: {position: 'bottom'}}}
    });
    
    // 8. Radar Chart
    const radarCtx = document.getElementById('radarChart').getContext('2d');
    if (charts.radar) charts.radar.destroy();
    charts.radar = new Chart(radarCtx, {
        type: 'radar',
        data: {
            labels: semesterLabels,
            datasets: [{
                data: gpaData,
                borderColor: goldColor,
                backgroundColor: 'rgba(212, 175, 55, 0.2)',
                pointBackgroundColor: goldColor,
                borderWidth: 2
            }]
        },
        options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {legend: {display: false}},
            scales: {r: {beginAtZero: true, max: 4.0, grid: {color: '#3a3a3a'}, angleLines: {color: '#3a3a3a'}}}
        }
    });
    
    // 9. Gauge Chart
    const overallGPA = parseFloat(calculateOverallGPA());
    const percentage = (overallGPA / 4.0) * 100;
    
    const gaugeCtx = document.getElementById('gaugeChart').getContext('2d');
    if (charts.gauge) charts.gauge.destroy();
    charts.gauge = new Chart(gaugeCtx, {
        type: 'doughnut',
        data: {
            datasets: [{
                data: [percentage, 100 - percentage],
                backgroundColor: [goldColor, '#3a3a3a'],
                borderWidth: 0,
                circumference: 180,
                rotation: 270
            }]
        },
        options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {legend: {display: false}, tooltip: {enabled: false}},
            cutout: '75%'
        },
        plugins: [{
            afterDraw: (chart) => {
                const ctx = chart.ctx;
                const width = chart.width;
                const height = chart.height;
                ctx.restore();
                const fontSize = (height / 114).toFixed(2);
                ctx.font = `bold ${fontSize}em Poppins`;
                ctx.fillStyle = goldColor;
                ctx.textBaseline = 'middle';
                const text = `${overallGPA}`;
                const textX = Math.round((width - ctx.measureText(text).width) / 2);
                const textY = height / 1.6;
                ctx.fillText(text, textX, textY);
                ctx.save();
            }
        }]
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
    document.querySelectorAll('.menu-item').forEach(item => item.classList.remove('active'));
    document.querySelector(`.menu-item[data-page="${page}"]`).classList.add('active');
    document.querySelectorAll('.page-content').forEach(p => p.classList.add('hidden'));
    document.getElementById(`${page}Page`).classList.remove('hidden');
    if (page === 'analytics') setTimeout(() => renderCharts(), 100);
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
if (loadFromStorage() && studentData.name) showApp();
</script>
</body>
</html>
