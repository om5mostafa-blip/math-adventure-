<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>مغامرات الرياضيات - تعلم عبر القصص والألغاز</title>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700;800;900&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #6366f1;
            --primary-dark: #4f46e5;
            --secondary: #f59e0b;
            --accent: #ec4899;
            --success: #22c55e;
            --danger: #ef4444;
            --dark: #1e1b4b;
            --light: #f8fafc;
            --card-bg: rgba(255,255,255,0.95);
            --glass: rgba(255,255,255,0.15);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }

        body {
            font-family: 'Tajawal', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 50%, #f093fb 100%);
            min-height: 100vh;
            overflow-x: hidden;
            color: var(--dark);
        }

        .particles {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            pointer-events: none;
            z-index: 0;
            overflow: hidden;
        }
        .particle {
            position: absolute;
            border-radius: 50%;
            background: rgba(255,255,255,0.3);
            animation: float 15s infinite ease-in-out;
        }
        @keyframes float {
            0%, 100% { transform: translateY(0) rotate(0deg); opacity: 0.3; }
            50% { transform: translateY(-100px) rotate(180deg); opacity: 0.8; }
        }

        .app-container {
            position: relative;
            z-index: 1;
            max-width: 900px;
            margin: 0 auto;
            padding: 20px;
        }

        .app-header {
            text-align: center;
            padding: 30px 20px;
            color: white;
            margin-bottom: 20px;
        }
        .app-header h1 {
            font-size: 2.8rem;
            font-weight: 900;
            text-shadow: 2px 2px 20px rgba(0,0,0,0.3);
            margin-bottom: 10px;
            animation: titlePulse 3s ease-in-out infinite;
        }
        @keyframes titlePulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.02); }
        }
        .app-header p {
            font-size: 1.2rem;
            opacity: 0.9;
        }

        .stats-bar {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-bottom: 30px;
            flex-wrap: wrap;
        }
        .stat-card {
            background: var(--glass);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 15px 25px;
            color: white;
            display: flex;
            align-items: center;
            gap: 12px;
            border: 1px solid rgba(255,255,255,0.2);
            transition: all 0.3s;
            min-width: 160px;
        }
        .stat-card:hover { transform: translateY(-5px); background: rgba(255,255,255,0.25); }
        .stat-card i { font-size: 1.8rem; }
        .stat-info { text-align: right; }
        .stat-value { font-size: 1.5rem; font-weight: 800; }
        .stat-label { font-size: 0.85rem; opacity: 0.8; }

        .level-progress {
            background: var(--card-bg);
            border-radius: 24px;
            padding: 25px;
            margin-bottom: 25px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.1);
        }
        .level-progress h3 {
            margin-bottom: 15px;
            color: var(--dark);
            font-size: 1.3rem;
        }
        .progress-track {
            background: #e2e8f0;
            border-radius: 15px;
            height: 12px;
            overflow: hidden;
        }
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, var(--primary), var(--accent));
            border-radius: 15px;
            transition: width 1s ease;
            width: 0%;
        }
        .xp-text {
            text-align: center;
            margin-top: 8px;
            color: #64748b;
            font-size: 0.9rem;
        }

        .nav-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 25px;
            overflow-x: auto;
            padding-bottom: 5px;
        }
        .nav-tab {
            background: var(--glass);
            backdrop-filter: blur(10px);
            border: 2px solid rgba(255,255,255,0.3);
            border-radius: 16px;
            padding: 12px 24px;
            color: white;
            cursor: pointer;
            font-family: 'Tajawal', sans-serif;
            font-size: 1rem;
            font-weight: 700;
            transition: all 0.3s;
            white-space: nowrap;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .nav-tab:hover, .nav-tab.active {
            background: white;
            color: var(--primary);
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(0,0,0,0.15);
        }
        .nav-tab.active { border-color: white; }

        .content-section { display: none; }
        .content-section.active { display: block; animation: fadeIn 0.5s; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        .stories-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 20px;
        }
        .story-card {
            background: var(--card-bg);
            border-radius: 24px;
            overflow: hidden;
            box-shadow: 0 10px 40px rgba(0,0,0,0.1);
            transition: all 0.4s;
            cursor: pointer;
            position: relative;
        }
        .story-card:hover {
            transform: translateY(-10px) scale(1.02);
            box-shadow: 0 20px 60px rgba(0,0,0,0.2);
        }
        .story-card.locked { opacity: 0.6; filter: grayscale(0.5); cursor: not-allowed; }
        .story-card.locked:hover { transform: none; }
        .story-image {
            height: 160px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 4rem;
            position: relative;
            overflow: hidden;
        }
        .story-image::after {
            content: '';
            position: absolute;
            bottom: 0; left: 0; right: 0;
            height: 50%;
            background: linear-gradient(transparent, rgba(0,0,0,0.3));
        }
        .story-badge {
            position: absolute;
            top: 12px; left: 12px;
            background: rgba(255,255,255,0.9);
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 700;
            z-index: 2;
        }
        .story-content { padding: 20px; }
        .story-content h3 { font-size: 1.2rem; margin-bottom: 8px; color: var(--dark); }
        .story-content p { color: #64748b; font-size: 0.95rem; margin-bottom: 15px; }
        .story-meta {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .difficulty {
            display: flex;
            gap: 3px;
        }
        .difficulty-dot {
            width: 10px; height: 10px;
            border-radius: 50%;
            background: #e2e8f0;
        }
        .difficulty-dot.active { background: var(--secondary); }
        .story-btn {
            background: var(--primary);
            color: white;
            border: none;
            padding: 8px 20px;
            border-radius: 12px;
            font-family: 'Tajawal', sans-serif;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s;
        }
        .story-btn:hover { background: var(--primary-dark); transform: scale(1.05); }

        .puzzle-container {
            background: var(--card-bg);
            border-radius: 24px;
            padding: 30px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.1);
            text-align: center;
        }
        .puzzle-header {
            margin-bottom: 25px;
        }
        .puzzle-header h2 {
            color: var(--dark);
            font-size: 1.5rem;
            margin-bottom: 10px;
        }
        .puzzle-scene {
            background: linear-gradient(135deg, #fef3c7, #fde68a);
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 25px;
            position: relative;
            min-height: 200px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }
        .scene-character {
            font-size: 5rem;
            margin-bottom: 15px;
            animation: bounce 2s infinite;
        }
        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-15px); }
        }
        .scene-text {
            font-size: 1.2rem;
            color: #78350f;
            line-height: 1.8;
            max-width: 600px;
        }
        .math-problem {
            background: white;
            border-radius: 16px;
            padding: 25px;
            margin: 20px 0;
            font-size: 1.8rem;
            font-weight: 800;
            color: var(--dark);
            border: 3px dashed var(--primary);
            display: inline-block;
            min-width: 300px;
        }
        .answer-options {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            max-width: 500px;
            margin: 0 auto;
        }
        .answer-btn {
            background: linear-gradient(135deg, #f1f5f9, #e2e8f0);
            border: 3px solid transparent;
            border-radius: 16px;
            padding: 18px;
            font-size: 1.4rem;
            font-weight: 800;
            font-family: 'Tajawal', sans-serif;
            cursor: pointer;
            transition: all 0.3s;
            color: var(--dark);
        }
        .answer-btn:hover {
            border-color: var(--primary);
            transform: scale(1.05);
            background: white;
        }
        .answer-btn.correct {
            background: linear-gradient(135deg, #dcfce7, #bbf7d0);
            border-color: var(--success);
            color: var(--success);
            animation: correctPulse 0.5s;
        }
        .answer-btn.wrong {
            background: linear-gradient(135deg, #fee2e2, #fecaca);
            border-color: var(--danger);
            color: var(--danger);
            animation: shake 0.5s;
        }
        @keyframes correctPulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }
        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-10px); }
            75% { transform: translateX(10px); }
        }

        .feedback {
            margin-top: 20px;
            padding: 20px;
            border-radius: 16px;
            font-size: 1.1rem;
            font-weight: 700;
            display: none;
        }
        .feedback.show { display: block; animation: fadeIn 0.3s; }
        .feedback.success {
            background: linear-gradient(135deg, #dcfce7, #bbf7d0);
            color: #166534;
        }
        .feedback.error {
            background: linear-gradient(135deg, #fee2e2, #fecaca);
            color: #991b1b;
        }

        .next-btn {
            background: linear-gradient(135deg, var(--primary), var(--accent));
            color: white;
            border: none;
            padding: 15px 40px;
            border-radius: 16px;
            font-size: 1.2rem;
            font-weight: 800;
            font-family: 'Tajawal', sans-serif;
            cursor: pointer;
            margin-top: 20px;
            transition: all 0.3s;
            display: none;
        }
        .next-btn.show { display: inline-block; }
        .next-btn:hover { transform: scale(1.05); box-shadow: 0 10px 30px rgba(99,102,241,0.4); }

        .achievements-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 15px;
        }
        .achievement-card {
            background: var(--card-bg);
            border-radius: 20px;
            padding: 20px;
            text-align: center;
            box-shadow: 0 5px 20px rgba(0,0,0,0.08);
            transition: all 0.3s;
        }
        .achievement-card:hover { transform: translateY(-5px); }
        .achievement-card.locked { opacity: 0.4; filter: grayscale(1); }
        .achievement-icon {
            font-size: 3rem;
            margin-bottom: 10px;
        }
        .achievement-card h4 { font-size: 1rem; color: var(--dark); margin-bottom: 5px; }
        .achievement-card p { font-size: 0.85rem; color: #64748b; }

        .leaderboard {
            background: var(--card-bg);
            border-radius: 24px;
            padding: 25px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.1);
        }
        .leaderboard h3 {
            text-align: center;
            margin-bottom: 20px;
            color: var(--dark);
            font-size: 1.3rem;
        }
        .leader-item {
            display: flex;
            align-items: center;
            padding: 12px 15px;
            border-radius: 12px;
            margin-bottom: 8px;
            transition: all 0.3s;
        }
        .leader-item:hover { background: #f1f5f9; }
        .leader-rank {
            width: 36px; height: 36px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 800;
            margin-left: 12px;
            font-size: 0.9rem;
        }
        .leader-rank.gold { background: linear-gradient(135deg, #fcd34d, #f59e0b); color: white; }
        .leader-rank.silver { background: linear-gradient(135deg, #e5e7eb, #9ca3af); color: white; }
        .leader-rank.bronze { background: linear-gradient(135deg, #fdba74, #f97316); color: white; }
        .leader-rank.normal { background: #f1f5f9; color: #64748b; }
        .leader-name { flex: 1; font-weight: 700; }
        .leader-score { font-weight: 800; color: var(--primary); }

        .modal-overlay {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: rgba(0,0,0,0.6);
            backdrop-filter: blur(5px);
            display: none;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            padding: 20px;
        }
        .modal-overlay.show { display: flex; animation: fadeIn 0.3s; }
        .modal-content {
            background: white;
            border-radius: 30px;
            padding: 40px;
            max-width: 500px;
            width: 100%;
            text-align: center;
            animation: modalPop 0.4s;
            position: relative;
        }
        @keyframes modalPop {
            0% { transform: scale(0.5); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }
        .modal-close {
            position: absolute;
            top: 15px; left: 15px;
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #94a3b8;
        }
        .modal-emoji { font-size: 5rem; margin-bottom: 15px; }
        .modal-content h2 { color: var(--dark); margin-bottom: 10px; }
        .modal-content p { color: #64748b; margin-bottom: 20px; }
        .modal-xp {
            background: linear-gradient(135deg, #fef3c7, #fde68a);
            padding: 15px 30px;
            border-radius: 16px;
            display: inline-block;
            font-weight: 800;
            color: #92400e;
            font-size: 1.2rem;
        }

        #confetti-canvas {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            pointer-events: none;
            z-index: 999;
        }

        @media (max-width: 600px) {
            .app-header h1 { font-size: 2rem; }
            .stories-grid { grid-template-columns: 1fr; }
            .answer-options { grid-template-columns: 1fr; }
            .stat-card { min-width: 140px; padding: 12px 18px; }
        }
    </style>
</head>
<body>
    <div class="particles" id="particles"></div>
    <canvas id="confetti-canvas"></canvas>

    <div class="app-container">
        <header class="app-header">
            <h1>🧮 مغامرات الرياضيات</h1>
            <p>تعلم الرياضيات عبر قصص مشوقة وألغاز ممتعة!</p>
        </header>

        <div class="stats-bar">
            <div class="stat-card">
                <i class="fas fa-star" style="color: #fbbf24;"></i>
                <div class="stat-info">
                    <div class="stat-value" id="total-xp">0</div>
                    <div class="stat-label">نقطة خبرة</div>
                </div>
            </div>
            <div class="stat-card">
                <i class="fas fa-trophy" style="color: #fbbf24;"></i>
                <div class="stat-info">
                    <div class="stat-value" id="current-level">1</div>
                    <div class="stat-label">المستوى</div>
                </div>
            </div>
            <div class="stat-card">
                <i class="fas fa-check-circle" style="color: #4ade80;"></i>
                <div class="stat-info">
                    <div class="stat-value" id="solved-count">0</div>
                    <div class="stat-label">ألغاز محلولة</div>
                </div>
            </div>
            <div class="stat-card">
                <i class="fas fa-fire" style="color: #f97316;"></i>
                <div class="stat-info">
                    <div class="stat-value" id="streak-count">0</div>
                    <div class="stat-label">سلسلة الإجابات</div>
                </div>
            </div>
        </div>

        <div class="level-progress">
            <h3>📊 تقدمك في المستوى <span id="level-num">1</span></h3>
            <div class="progress-track">
                <div class="progress-fill" id="progress-fill"></div>
            </div>
            <div class="xp-text"><span id="current-xp">0</span> / <span id="xp-needed">100</span> نقطة للمستوى التالي</div>
        </div>

        <div class="nav-tabs">
            <button class="nav-tab active" onclick="showSection('stories')">
                <i class="fas fa-book-open"></i> القصص
            </button>
            <button class="nav-tab" onclick="showSection('puzzle')">
                <i class="fas fa-puzzle-piece"></i> الألغاز
            </button>
            <button class="nav-tab" onclick="showSection('achievements')">
                <i class="fas fa-medal"></i> الإنجازات
            </button>
            <button class="nav-tab" onclick="showSection('leaderboard')">
                <i class="fas fa-chart-line"></i> المتصدرون
            </button>
        </div>

        <div class="content-section active" id="stories-section">
            <div class="stories-grid" id="stories-grid"></div>
        </div>

        <div class="content-section" id="puzzle-section">
            <div class="puzzle-container">
                <div class="puzzle-header">
                    <h2 id="puzzle-title">🎯 لغز اليوم</h2>
                    <p id="puzzle-subtitle">حل اللغز لكسب النقاط!</p>
                </div>
                <div class="puzzle-scene">
                    <div class="scene-character" id="scene-character">🧙‍♂️</div>
                    <div class="scene-text" id="scene-text">اختر قصة من الأعلى لبدء المغامرة!</div>
                </div>
                <div class="math-problem" id="math-problem" style="display:none;"></div>
                <div class="answer-options" id="answer-options"></div>
                <div class="feedback" id="feedback"></div>
                <button class="next-btn" id="next-btn" onclick="nextPuzzle()">التالي ⬅️</button>
            </div>
        </div>

        <div class="content-section" id="achievements-section">
            <div class="achievements-grid" id="achievements-grid"></div>
        </div>

        <div class="content-section" id="leaderboard-section">
            <div class="leaderboard">
                <h3>🏆 لوحة المتصدرين</h3>
                <div id="leaderboard-list"></div>
            </div>
        </div>
    </div>

    <div class="modal-overlay" id="modal">
        <div class="modal-content">
            <button class="modal-close" onclick="closeModal()">✕</button>
            <div class="modal-emoji" id="modal-emoji">🎉</div>
            <h2 id="modal-title">تهانينا!</h2>
            <p id="modal-text">لقد أكملت اللغز بنجاح!</p>
            <div class="modal-xp" id="modal-xp">+50 نقطة خبرة</div>
        </div>
    </div>

    <script>
        const stories = [
            {
                id: 1,
                title: "مغامرة الساحر والأرقام المفقودة",
                desc: "ساعد الساحر عمر في استعادة الأرقام السحرية المفقودة من كتابه القديم!",
                emoji: "🧙‍♂️",
                color: "linear-gradient(135deg, #c084fc, #a855f7)",
                difficulty: 1,
                locked: false,
                puzzles: [
                    { text: "في غابة الأرقام، وجد الساحر ٣ كرات سحرية و٥ كرات أخرى. كم كرة سحرية لديه الآن؟", problem: "3 + 5 = ?", answers: [6, 7, 8, 9], correct: 2, xp: 20 },
                    { text: "أعطى الساحر ٢ كرة من مجموعته لصديقه الأرنب. كم كرة تبقت معه؟", problem: "8 - 2 = ?", answers: [4, 5, 6, 7], correct: 2, xp: 25 },
                    { text: "وجد الساحر صندوقاً فيه ٤ صفوف، وكل صف فيه ٣ كرات. كم كرة في الصندوق؟", problem: "4 × 3 = ?", answers: [10, 11, 12, 13], correct: 2, xp: 30 },
                    { text: "قسم الساحر ١٢ كرة بالتساوي على ٣ أصدقاء. كم كرة لكل صديق؟", problem: "12 ÷ 3 = ?", answers: [3, 4, 5, 6], correct: 1, xp: 35 }
                ]
            },
            {
                id: 2,
                title: "رحلة الفضاء والكواكب",
                desc: "انطلق مع رائد الفضاء سالم في رحلة لاكتشاف أسرار الكواكب!",
                emoji: "🚀",
                color: "linear-gradient(135deg, #60a5fa, #3b82f6)",
                difficulty: 2,
                locked: false,
                puzzles: [
                    { text: "سافر رائد الفضاء ٢٤٠ كم في الساعة الأولى و١٨٠ كم في الثانية. ما المسافة الإجمالية؟", problem: "240 + 180 = ?", answers: [400, 410, 420, 430], correct: 2, xp: 30 },
                    { text: "كوكب المريخ أبعد عن الشمس بـ ٢٢٨ مليون كم، والأرض بـ ١٤٩ مليون كم. ما الفرق؟", problem: "228 - 149 = ?", answers: [69, 79, 89, 99], correct: 1, xp: 35 },
                    { text: "كل صاروخ يحمل ٨ رواد. كم رائداً في ٦ صواريخ؟", problem: "8 × 6 = ?", answers: [42, 46, 48, 52], correct: 2, xp: 40 },
                    { text: "قسمت محطة الفضاء ٥٤ لتراً من الماء على ٩ رواد. كم لتراً لكل رائد؟", problem: "54 ÷ 9 = ?", answers: [5, 6, 7, 8], correct: 1, xp: 40 }
                ]
            },
            {
                id: 3,
                title: "كنز القراصنة",
                desc: "ساعد القرصانة ليلى في فك رموز الخريطة للوصول إلى الكنز المفقود!",
                emoji: "🏴‍☠️",
                color: "linear-gradient(135deg, #fbbf24, #f59e0b)",
                difficulty: 2,
                locked: true,
                puzzles: [
                    { text: "وجدت ليلى صندوقاً فيه ١٤٥ قطعة ذهبية وصندوقاً آخر فيه ٢٣٧ قطعة. كم القطع الإجمالية؟", problem: "145 + 237 = ?", answers: [372, 382, 392, 402], correct: 1, xp: 35 },
                    { text: "كان لدى ليلى ٥٠٠ قطعة ذهبية وأنفقت ١٨٧ قطعة. كم تبقى؟", problem: "500 - 187 = ?", answers: [303, 313, 323, 333], correct: 1, xp: 40 },
                    { text: "كل صندوق كنز يحتوي على ١٢ جوهرة. كم جوهرة في ١٥ صندوقاً؟", problem: "12 × 15 = ?", answers: [170, 180, 190, 200], correct: 1, xp: 45 },
                    { text: "قسمت ليلى ٣٦٠ جوهرة بالتساوي على ٨ بحارة. كم جوهرة لكل بحار؟", problem: "360 ÷ 8 = ?", answers: [40, 45, 50, 55], correct: 1, xp: 45 }
                ]
            },
            {
                id: 4,
                title: "مملكة التنانين",
                desc: "ادخل مملكة التنانين وحل الألغاز لإنقاذ الأميرة من البرج العالي!",
                emoji: "🐉",
                color: "linear-gradient(135deg, #f87171, #ef4444)",
                difficulty: 3,
                locked: true,
                puzzles: [
                    { text: "التنين الأول يحرس ٣٤٥ جوهرة والثاني يحرس ٢٨٩ جوهرة. كم الجواهر الإجمالية؟", problem: "345 + 289 = ?", answers: [624, 634, 644, 654], correct: 1, xp: 40 },
                    { text: "كان في البرج ١٠٠٠ جوهرة وسرق التنين ٤٥٦ منها. كم تبقى؟", problem: "1000 - 456 = ?", answers: [534, 544, 554, 564], correct: 1, xp: 45 },
                    { text: "كل تنين يحرس ٢٥ جوهرة في ١٤ غرفة. كم جوهرة في البرج؟", problem: "25 × 14 = ?", answers: [340, 350, 360, 370], correct: 1, xp: 50 },
                    { text: "قسمت الأميرة ٨٤٠ جوهرة على ١٢ فارساً. كم جوهرة لكل فارس؟", problem: "840 ÷ 12 = ?", answers: [65, 70, 75, 80], correct: 1, xp: 50 }
                ]
            },
            {
                id: 5,
                title: "مدينة الروبوتات",
                desc: "ساعد المهندسة نورا في برمجة الروبوتات وحل المعادلات المعقدة!",
                emoji: "🤖",
                color: "linear-gradient(135deg, #34d399, #10b981)",
                difficulty: 3,
                locked: true,
                puzzles: [
                    { text: "صنعت نورا ٤٥٦ روبوتاً في الأسبوع الأول و٣٧٨ في الثاني. كم الروبوتات الإجمالية؟", problem: "456 + 378 = ?", answers: [824, 834, 844, 854], correct: 1, xp: 45 },
                    { text: "كان لدى المصنع ٢٠٠٠ قطعة واستخدمت ١٢٣٤ قطعة. كم تبقى؟", problem: "2000 - 1234 = ?", answers: [756, 766, 776, 786], correct: 1, xp: 50 },
                    { text: "كل خط إنتاج يصنع ٣٦ روبوتاً يومياً. كم روبوتاً في ٢٨ يوماً؟", problem: "36 × 28 = ?", answers: [988, 1008, 1028, 1048], correct: 1, xp: 55 },
                    { text: "قسمت نورا ١٤٤٠ روبوتاً على ١٦ متجراً. كم روبوتاً لكل متجر؟", problem: "1440 ÷ 16 = ?", answers: [85, 90, 95, 100], correct: 1, xp: 55 }
                ]
            },
            {
                id: 6,
                title: "غابة الألغاز",
                desc: "ادخل الغابة السحرية وحل أصعب الألغاز لإيجاد بوابة الخروج!",
                emoji: "🌲",
                color: "linear-gradient(135deg, #a78bfa, #8b5cf6)",
                difficulty: 3,
                locked: true,
                puzzles: [
                    { text: "وجدت في الغابة ٧٨٩ حجراً سحرياً و٦٥٤ زهرة سحرية. كم العدد الإجمالي؟", problem: "789 + 654 = ?", answers: [1433, 1443, 1453, 1463], correct: 1, xp: 50 },
                    { text: "كان في البحيرة ٥٠٠٠ سمكة وخرج ٢٣٤٥ منها. كم تبقى؟", problem: "5000 - 2345 = ?", answers: [2555, 2655, 2755, 2855], correct: 1, xp: 55 },
                    { text: "كل شجرة تنتج ٤٨ تفاحة سحرية. كم تفاحة في ٣٥ شجرة؟", problem: "48 × 35 = ?", answers: [1660, 1680, 1700, 1720], correct: 1, xp: 60 },
                    { text: "قسمت الجنية ٢٤٠٠ تفاحة على ٤٨ حيواناً. كم تفاحة لكل حيوان؟", problem: "2400 ÷ 48 = ?", answers: [48, 50, 52, 54], correct: 1, xp: 60 }
                ]
            }
        ];

        const achievements = [
            { id: 1, icon: "🌟", title: "بداية المغامرة", desc: "أكمل أول لغز", unlocked: false },
            { id: 2, icon: "🔥", title: "سلسلة نارية", desc: "أجب بشكل صحيح ٥ مرات متتالية", unlocked: false },
            { id: 3, icon: "🏆", title: "بطل الرياضيات", desc: "أكمل ١٠ ألغاز", unlocked: false },
            { id: 4, icon: "💎", title: "جامع الكنوز", desc: "اجمع ٥٠٠ نقطة خبرة", unlocked: false },
            { id: 5, icon: "🧠", title: "عبقري الرياضيات", desc: "أكمل قصة كاملة", unlocked: false },
            { id: 6, icon: "👑", title: "ملك الألغاز", desc: "أكمل كل القصص", unlocked: false }
        ];

        const leaderboard = [
            { name: "أحمد", score: 1250 },
            { name: "سارة", score: 1100 },
            { name: "محمد", score: 980 },
            { name: "نور", score: 850 },
            { name: "علي", score: 720 },
            { name: "ليلى", score: 650 },
            { name: "عمر", score: 540 },
            { name: "فاطمة", score: 480 }
        ];

        let state = {
            xp: 0,
            level: 1,
            solved: 0,
            streak: 0,
            currentStory: null,
            currentPuzzleIndex: 0,
            unlockedStories: [1],
            solvedPuzzles: [],
            achievements: []
        };

        function loadState() {
            const saved = localStorage.getItem('mathAdventureState');
            if (saved) {
                state = JSON.parse(saved);
                achievements.forEach(a => { a.unlocked = state.achievements.includes(a.id); });
                stories.forEach(s => { s.locked = !state.unlockedStories.includes(s.id); });
            }
        }

        function saveState() {
            localStorage.setItem('mathAdventureState', JSON.stringify(state));
        }

        function createParticles() {
            const container = document.getElementById('particles');
            for (let i = 0; i < 20; i++) {
                const p = document.createElement('div');
                p.className = 'particle';
                p.style.width = Math.random() * 20 + 5 + 'px';
                p.style.height = p.style.width;
                p.style.left = Math.random() * 100 + '%';
                p.style.top = Math.random() * 100 + '%';
                p.style.animationDelay = Math.random() * 15 + 's';
                p.style.animationDuration = (Math.random() * 10 + 10) + 's';
                container.appendChild(p);
            }
        }

        function renderStories() {
            const grid = document.getElementById('stories-grid');
            grid.innerHTML = stories.map(story => `
                <div class="story-card ${story.locked ? 'locked' : ''}" onclick="${story.locked ? '' : `startStory(${story.id})`}">
                    <div class="story-image" style="background: ${story.color};">
                        <span style="z-index:2;">${story.emoji}</span>
                        <span class="story-badge">${story.locked ? '🔒 مقفل' : '✓ متاح'}</span>
                    </div>
                    <div class="story-content">
                        <h3>${story.title}</h3>
                        <p>${story.desc}</p>
                        <div class="story-meta">
                            <div class="difficulty">
                                ${[1,2,3].map(i => `<div class="difficulty-dot ${i <= story.difficulty ? 'active' : ''}"></div>`).join('')}
                            </div>
                            <button class="story-btn">${story.locked ? '🔒' : 'ابدأ المغامرة'}</button>
                        </div>
                    </div>
                </div>
            `).join('');
        }

        function renderAchievements() {
            const grid = document.getElementById('achievements-grid');
            grid.innerHTML = achievements.map(a => `
                <div class="achievement-card ${a.unlocked ? '' : 'locked'}">
                    <div class="achievement-icon">${a.icon}</div>
                    <h4>${a.title}</h4>
                    <p>${a.desc}</p>
                </div>
            `).join('');
        }

        function renderLeaderboard() {
            const list = document.getElementById('leaderboard-list');
            const allPlayers = [...leaderboard, { name: "أنت", score: state.xp }].sort((a, b) => b.score - a.score);
            list.innerHTML = allPlayers.map((p, i) => `
                <div class="leader-item">
                    <div class="leader-rank ${i === 0 ? 'gold' : i === 1 ? 'silver' : i === 2 ? 'bronze' : 'normal'}">${i + 1}</div>
                    <div class="leader-name">${p.name}</div>
                    <div class="leader-score">${p.score} نقطة</div>
                </div>
            `).join('');
        }

        function updateStats() {
            document.getElementById('total-xp').textContent = state.xp;
            document.getElementById('current-level').textContent = state.level;
            document.getElementById('solved-count').textContent = state.solved;
            document.getElementById('streak-count').textContent = state.streak;
            
            const xpNeeded = state.level * 100;
            const currentLevelXp = state.xp - ((state.level - 1) * 100);
            const progress = Math.min((currentLevelXp / 100) * 100, 100);
            
            document.getElementById('level-num').textContent = state.level;
            document.getElementById('current-xp').textContent = currentLevelXp;
            document.getElementById('xp-needed').textContent = 100;
            document.getElementById('progress-fill').style.width = progress + '%';
        }

        function showSection(section) {
            document.querySelectorAll('.content-section').forEach(s => s.classList.remove('active'));
            document.querySelectorAll('.nav-tab').forEach(t => t.classList.remove('active'));
            
            document.getElementById(section + '-section').classList.add('active');
            event.target.closest('.nav-tab').classList.add('active');
            
            if (section === 'achievements') renderAchievements();
            if (section === 'leaderboard') renderLeaderboard();
        }

        function startStory(storyId) {
            state.currentStory = storyId;
            state.currentPuzzleIndex = 0;
            saveState();
            showSection('puzzle');
            document.querySelectorAll('.nav-tab')[1].classList.add('active');
            document.querySelectorAll('.nav-tab')[0].classList.remove('active');
            loadPuzzle();
        }

        function loadPuzzle() {
            const story = stories.find(s => s.id === state.currentStory);
            if (!story) return;
            
            const puzzle = story.puzzles[state.currentPuzzleIndex];
            
            document.getElementById('puzzle-title').textContent = story.title;
            document.getElementById('scene-character').textContent = story.emoji;
            document.getElementById('scene-text').textContent = puzzle.text;
            document.getElementById('math-problem').textContent = puzzle.problem;
            document.getElementById('math-problem').style.display = 'inline-block';
            
            const optionsDiv = document.getElementById('answer-options');
            optionsDiv.innerHTML = puzzle.answers.map((ans, i) => `
                <button class="answer-btn" onclick="checkAnswer(${i})">${ans}</button>
            `).join('');
            
            document.getElementById('feedback').classList.remove('show');
            document.getElementById('next-btn').classList.remove('show');
        }

        function checkAnswer(index) {
            const story = stories.find(s => s.id === state.currentStory);
            const puzzle = story.puzzles[state.currentPuzzleIndex];
            const buttons = document.querySelectorAll('.answer-btn');
            const feedback = document.getElementById('feedback');
            
            buttons.forEach(b => b.disabled = true);
            
            if (index === puzzle.correct) {
                buttons[index].classList.add('correct');
                feedback.className = 'feedback success show';
                feedback.innerHTML = '🎉 إجابة صحيحة! أحسنت!';
                
                state.xp += puzzle.xp;
                state.solved++;
                state.streak++;
                
                const newLevel = Math.floor(state.xp / 100) + 1;
                if (newLevel > state.level) {
                    state.level = newLevel;
                    showModal('🎊', 'ترقية!', `وصلت إلى المستوى ${state.level}!`, `+${puzzle.xp} نقطة خبرة`);
                } else {
                    showModal('⭐', 'أحسنت!', 'لقد حللت اللغز بنجاح!', `+${puzzle.xp} نقطة خبرة`);
                }
                
                checkAchievements();
                
                if (state.currentPuzzleIndex < story.puzzles.length - 1) {
                    document.getElementById('next-btn').classList.add('show');
                } else {
                    unlockNextStory(story.id);
                    setTimeout(() => {
                        showModal('🏆', 'قصة مكتملة!', `أكملت "${story.title}" بنجاح!`, 'مكافأة خاصة: +50 نقطة');
                        state.xp += 50;
                        updateStats();
                        showSection('stories');
                        document.querySelectorAll('.nav-tab')[0].classList.add('active');
                        document.querySelectorAll('.nav-tab')[1].classList.remove('active');
                    }, 1500);
                }
            } else {
                buttons[index].classList.add('wrong');
                buttons[puzzle.correct].classList.add('correct');
                feedback.className = 'feedback error show';
                feedback.innerHTML = '❌ إجابة خاطئة. حاول مرة أخرى في اللغز التالي!';
                state.streak = 0;
                
                if (state.currentPuzzleIndex < story.puzzles.length - 1) {
                    document.getElementById('next-btn').classList.add('show');
                } else {
                    setTimeout(() => {
                        showSection('stories');
                        document.querySelectorAll('.nav-tab')[0].classList.add('active');
                        document.querySelectorAll('.nav-tab')[1].classList.remove('active');
                    }, 2000);
                }
            }
            
            updateStats();
            saveState();
        }

        function nextPuzzle() {
            state.currentPuzzleIndex++;
            saveState();
            loadPuzzle();
        }

        function unlockNextStory(currentId) {
            const nextStory = stories.find(s => s.id === currentId + 1);
            if (nextStory && !state.unlockedStories.includes(nextStory.id)) {
                state.unlockedStories.push(nextStory.id);
                nextStory.locked = false;
                saveState();
                renderStories();
            }
        }

        function checkAchievements() {
            const newAchievements = [];
            
            if (state.solved >= 1 && !state.achievements.includes(1)) newAchievements.push(1);
            if (state.streak >= 5 && !state.achievements.includes(2)) newAchievements.push(2);
            if (state.solved >= 10 && !state.achievements.includes(3)) newAchievements.push(3);
            if (state.xp >= 500 && !state.achievements.includes(4)) newAchievements.push(4);
            
            const completedStories = stories.filter(s => {
                const storyPuzzles = s.puzzles.map((_, i) => `${s.id}-${i}`);
                return storyPuzzles.every(p => state.solvedPuzzles.includes(p));
            });
            if (completedStories.length >= 1 && !state.achievements.includes(5)) newAchievements.push(5);
            if (completedStories.length === stories.length && !state.achievements.includes(6)) newAchievements.push(6);
            
            newAchievements.forEach(id => {
                state.achievements.push(id);
                const ach = achievements.find(a => a.id === id);
                if (ach) {
                    ach.unlocked = true;
                    setTimeout(() => {
                        showModal(ach.icon, 'إنجاز جديد!', ach.title, ach.desc);
                    }, 2000);
                }
            });
            
            if (newAchievements.length > 0) saveState();
        }

        function showModal(emoji, title, text, xp) {
            document.getElementById('modal-emoji').textContent = emoji;
            document.getElementById('modal-title').textContent = title;
            document.getElementById('modal-text').textContent = text;
            document.getElementById('modal-xp').textContent = xp;
            document.getElementById('modal').classList.add('show');
            
            if (emoji === '🎊' || emoji === '🏆') {
                fireConfetti();
            }
        }

        function closeModal() {
            document.getElementById('modal').classList.remove('show');
        }

        function fireConfetti() {
            const canvas = document.getElementById('confetti-canvas');
            const ctx = canvas.getContext('2d');
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
            
            const colors = ['#6366f1', '#ec4899', '#f59e0b', '#22c55e', '#3b82f6', '#f97316'];
            const particles = [];
            
            for (let i = 0; i < 100; i++) {
                particles.push({
                    x: canvas.width / 2,
                    y: canvas.height / 2,
                    vx: (Math.random() - 0.5) * 15,
                    vy: (Math.random() - 0.5) * 15 - 5,
                    color: colors[Math.floor(Math.random() * colors.length)],
                    size: Math.random() * 8 + 4,
                    rotation: Math.random() * 360,
                    rotationSpeed: (Math.random() - 0.5) * 10
                });
            }
            
            let frame = 0;
            function animate() {
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                
                particles.forEach(p => {
                    p.x += p.vx;
                    p.y += p.vy;
                    p.vy += 0.2;
                    p.rotation += p.rotationSpeed;
                    
                    ctx.save();
                    ctx.translate(p.x, p.y);
                    ctx.rotate(p.rotation * Math.PI / 180);
                    ctx.fillStyle = p.color;
                    ctx.fillRect(-p.size/2, -p.size/2, p.size, p.size);
                    ctx.restore();
                });
                
                frame++;
                if (frame < 120) requestAnimationFrame(animate);
                else ctx.clearRect(0, 0, canvas.width, canvas.height);
            }
            animate();
        }

        function init() {
            createParticles();
            loadState();
            renderStories();
            renderAchievements();
            renderLeaderboard();
            updateStats();
        }

        init();
    </script>
</body>
</html>
