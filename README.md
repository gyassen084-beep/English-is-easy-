<!DOCTYPE html>
<html lang="en" dir="ltr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>English Made Easy - Yassin Jamal</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Noto+Naskh+Arabic:wght@400;600;700&family=Playfair+Display:wght@700;800&display=swap" rel="stylesheet">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        :root {
            --primary: #1e3a5f; --primary-light: #2c5282; --primary-dark: #0f172a;
            --accent: #d4a843; --accent-light: #f0d78c;
            --bg: #f0f4f8; --surface: #ffffff; --text: #1e293b; --text-light: #64748b;
            --border: #e2e8f0;
            --shadow: 0 4px 6px -1px rgba(0,0,0,0.1), 0 2px 4px -1px rgba(0,0,0,0.06);
            --shadow-lg: 0 20px 25px -5px rgba(0,0,0,0.1), 0 10px 10px -5px rgba(0,0,0,0.04);
            --radius: 16px; --radius-sm: 8px;
        }
        body { font-family: 'Inter', sans-serif; background: var(--bg); color: var(--text); min-height: 100vh; overflow-x: hidden; }
        .bg-animation { position: fixed; top: 0; left: 0; width: 100%; height: 100%; z-index: -1; background: linear-gradient(135deg, #1e3a5f 0%, #2c5282 25%, #3b82f6 50%, #1e40af 75%, #1e3a5f 100%); background-size: 400% 400%; animation: gradientShift 20s ease infinite; opacity: 0.06; }
        @keyframes gradientShift { 0% { background-position: 0% 50%; } 50% { background-position: 100% 50%; } 100% { background-position: 0% 50%; } }
        .orb { position: fixed; border-radius: 50%; filter: blur(80px); z-index: -1; opacity: 0.25; animation: float 25s infinite ease-in-out; }
        .orb-1 { width: 350px; height: 350px; background: var(--primary); top: 5%; left: -8%; animation-delay: 0s; }
        .orb-2 { width: 300px; height: 300px; background: var(--accent); top: 50%; right: -5%; animation-delay: 8s; }
        .orb-3 { width: 250px; height: 250px; background: var(--primary-light); bottom: 15%; left: 25%; animation-delay: 16s; }
        @keyframes float { 0%,100% { transform: translate(0,0) scale(1); } 33% { transform: translate(30px,-30px) scale(1.1); } 66% { transform: translate(-20px,20px) scale(0.9); } }
        .app-container { max-width: 900px; margin: 0 auto; padding: 20px; padding-bottom: 120px; min-height: 100vh; }
        .header { text-align: center; padding: 40px 20px 30px; position: relative; }
        .logo { font-family: 'Playfair Display', serif; font-size: 2.8rem; font-weight: 800; background: linear-gradient(135deg, var(--primary), var(--accent)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; margin-bottom: 8px; letter-spacing: -1px; }
        .tagline { color: var(--text-light); font-size: 1rem; font-weight: 400; letter-spacing: 0.5px; }
        .nav-container { position: fixed; bottom: 0; left: 0; right: 0; background: rgba(255,255,255,0.9); backdrop-filter: blur(20px); -webkit-backdrop-filter: blur(20px); border-top: 1px solid rgba(255,255,255,0.5); padding: 12px 20px calc(12px + env(safe-area-inset-bottom)); z-index: 1000; box-shadow: 0 -4px 20px rgba(0,0,0,0.05); }
        .nav-items { display: flex; justify-content: space-around; max-width: 600px; margin: 0 auto; }
        .nav-item { display: flex; flex-direction: column; align-items: center; gap: 4px; padding: 8px 16px; border-radius: 12px; cursor: pointer; transition: all 0.3s cubic-bezier(0.4,0,0.2,1); border: none; background: transparent; color: var(--text-light); font-family: inherit; position: relative; }
        .nav-item:hover { color: var(--primary); transform: translateY(-2px); }
        .nav-item.active { color: var(--primary); background: rgba(30,58,95,0.08); }
        .nav-item.active::after { content: ''; position: absolute; top: -12px; left: 50%; transform: translateX(-50%); width: 4px; height: 4px; border-radius: 50%; background: var(--primary); box-shadow: 0 0 8px var(--primary); }
        .nav-icon { width: 24px; height: 24px; stroke-width: 2; stroke-linecap: round; stroke-linejoin: round; fill: none; stroke: currentColor; }
        .nav-label { font-size: 0.75rem; font-weight: 500; }
        .page { display: none; animation: fadeIn 0.4s ease-out; }
        .page.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        .search-container { position: relative; margin-bottom: 30px; }
        .search-box { width: 100%; padding: 16px 24px; padding-left: 52px; border: 2px solid var(--border); border-radius: var(--radius); font-size: 1.1rem; font-family: inherit; background: var(--surface); color: var(--text); transition: all 0.3s ease; box-shadow: var(--shadow); }
        .search-box:focus { outline: none; border-color: var(--primary); box-shadow: 0 0 0 4px rgba(30,58,95,0.1), var(--shadow); }
        .search-icon { position: absolute; left: 18px; top: 50%; transform: translateY(-50%); color: var(--text-light); width: 20px; height: 20px; }
        .search-box:focus + .search-icon { color: var(--primary); }
        .suggestions { position: absolute; top: calc(100% + 8px); left: 0; right: 0; background: var(--surface); border-radius: var(--radius-sm); box-shadow: var(--shadow-lg); border: 1px solid var(--border); max-height: 300px; overflow-y: auto; z-index: 100; display: none; }
        .suggestions.show { display: block; }
        .suggestion-item { padding: 12px 20px; cursor: pointer; display: flex; align-items: center; gap: 12px; transition: background 0.2s; border-bottom: 1px solid var(--border); }
        .suggestion-item:last-child { border-bottom: none; }
        .suggestion-item:hover { background: rgba(30,58,95,0.05); }
        .suggestion-text { font-weight: 500; color: var(--text); }
        .suggestion-type { font-size: 0.75rem; color: var(--text-light); margin-left: auto; background: var(--bg); padding: 2px 8px; border-radius: 20px; }
        .result-card { background: var(--surface); border-radius: var(--radius); padding: 30px; box-shadow: var(--shadow); border: 1px solid var(--border); margin-bottom: 20px; animation: slideUp 0.4s ease-out; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        .word-header { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 20px; flex-wrap: wrap; gap: 15px; }
        .word-title { font-family: 'Playfair Display', serif; font-size: 2.2rem; font-weight: 700; color: var(--primary); letter-spacing: -0.5px; }
        .phonetic { font-family: 'Courier New', monospace; color: var(--text-light); font-size: 1rem; background: var(--bg); padding: 4px 12px; border-radius: 20px; }
        .star-btn { background: none; border: none; cursor: pointer; padding: 8px; border-radius: 50%; transition: all 0.3s; color: var(--text-light); }
        .star-btn:hover { background: rgba(212,168,67,0.1); color: var(--accent); transform: scale(1.1); }
        .star-btn.saved { color: var(--accent); }
        .star-btn.saved svg { fill: currentColor; }
        .audio-section { display: flex; gap: 12px; margin-bottom: 24px; flex-wrap: wrap; }
        .audio-btn { display: inline-flex; align-items: center; gap: 8px; padding: 8px 16px; border-radius: 24px; border: 1px solid var(--border); background: var(--bg); color: var(--text); font-family: inherit; font-size: 0.875rem; cursor: pointer; transition: all 0.3s; }
        .audio-btn:hover { background: var(--primary); color: white; border-color: var(--primary); transform: translateY(-1px); box-shadow: 0 4px 12px rgba(30,58,95,0.3); }
        .meanings-section { margin-top: 24px; }
        .part-of-speech { font-weight: 600; color: var(--primary); margin-bottom: 12px; padding-bottom: 8px; border-bottom: 2px solid var(--accent); display: inline-block; text-transform: uppercase; letter-spacing: 1px; font-size: 0.85rem; }
        .meaning-list { list-style: none; margin-bottom: 24px; }
        .meaning-item { padding: 12px 0; padding-left: 24px; position: relative; border-bottom: 1px solid rgba(226,232,240,0.5); }
        .meaning-item::before { content: ''; position: absolute; left: 0; top: 20px; width: 8px; height: 8px; border-radius: 50%; background: var(--accent); }
        .definition { font-size: 1rem; line-height: 1.6; color: var(--text); margin-bottom: 6px; }
        .example { font-size: 0.9rem; color: var(--text-light); font-style: italic; padding-left: 16px; border-left: 3px solid var(--accent-light); margin-top: 8px; line-height: 1.5; }
        .example-word { color: var(--primary); font-weight: 600; }
        .antonyms-section { margin-top: 20px; padding: 16px; background: rgba(30,58,95,0.03); border-radius: var(--radius-sm); border-left: 4px solid var(--primary); }
        .antonyms-title { font-weight: 600; color: var(--primary); font-size: 0.875rem; margin-bottom: 8px; text-transform: uppercase; letter-spacing: 0.5px; }
        .antonym-tag { display: inline-block; padding: 4px 12px; background: white; border: 1px solid var(--primary-light); color: var(--primary-light); border-radius: 20px; font-size: 0.875rem; margin: 4px; cursor: pointer; transition: all 0.2s; }
        .antonym-tag:hover { background: var(--primary); color: white; transform: translateY(-1px); }
        .arabic-section { margin-top: 24px; padding: 20px; background: linear-gradient(135deg, rgba(30,58,95,0.03), rgba(212,168,67,0.05)); border-radius: var(--radius-sm); border: 1px solid rgba(30,58,95,0.1); }
        .arabic-title { font-size: 0.875rem; font-weight: 600; color: var(--primary); margin-bottom: 12px; display: flex; align-items: center; gap: 8px; }
        .arabic-text { font-family: 'Noto Naskh Arabic', serif; font-size: 1.4rem; line-height: 1.8; color: var(--text); direction: rtl; }
        .translate-link { display: inline-flex; align-items: center; gap: 6px; margin-top: 12px; color: var(--primary); text-decoration: none; font-size: 0.875rem; font-weight: 500; transition: all 0.2s; }
        .translate-link:hover { color: var(--primary-dark); gap: 10px; }
        .library-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 24px; }
        .library-title { font-family: 'Playfair Display', serif; font-size: 1.8rem; font-weight: 700; color: var(--primary); }
        .library-count { background: var(--primary); color: white; padding: 4px 12px; border-radius: 20px; font-size: 0.875rem; font-weight: 600; }
        .saved-list { display: flex; flex-direction: column; gap: 12px; }
        .saved-item { background: var(--surface); border-radius: var(--radius-sm); padding: 20px; box-shadow: var(--shadow); border: 1px solid var(--border); display: flex; justify-content: space-between; align-items: center; transition: all 0.3s; cursor: pointer; }
        .saved-item:hover { transform: translateX(4px); border-color: var(--accent); box-shadow: var(--shadow-lg); }
        .saved-word-info h3 { font-family: 'Playfair Display', serif; font-size: 1.25rem; color: var(--primary); margin-bottom: 4px; }
        .saved-word-info p { font-size: 0.875rem; color: var(--text-light); }
        .saved-star { color: var(--accent); background: none; border: none; cursor: pointer; padding: 8px; transition: transform 0.2s; }
        .saved-star:hover { transform: scale(1.1); }
        .empty-state { text-align: center; padding: 60px 20px; color: var(--text-light); }
        .empty-state svg { width: 64px; height: 64px; margin-bottom: 16px; opacity: 0.3; }
        .tools-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin-top: 20px; }
        .tool-card { background: var(--surface); border-radius: var(--radius); padding: 28px; box-shadow: var(--shadow); border: 1px solid var(--border); transition: all 0.3s; text-decoration: none; color: inherit; display: block; }
        .tool-card:hover { transform: translateY(-4px); box-shadow: var(--shadow-lg); border-color: var(--accent); }
        .tool-icon { width: 48px; height: 48px; border-radius: 12px; display: flex; align-items: center; justify-content: center; margin-bottom: 16px; font-size: 1.5rem; }
        .tool-icon.translate { background: linear-gradient(135deg, var(--primary-light), var(--primary)); }
        .tool-icon.grammar { background: linear-gradient(135deg, var(--accent), #c05621); }
        .tool-icon.thesaurus { background: linear-gradient(135deg, #2c5282, var(--primary)); }
        .tool-title { font-family: 'Playfair Display', serif; font-size: 1.125rem; font-weight: 600; margin-bottom: 8px; color: var(--primary); }
        .tool-desc { font-size: 0.875rem; color: var(--text-light); line-height: 1.5; }
        .tool-arrow { margin-top: 16px; color: var(--primary); font-size: 1.25rem; transition: transform 0.2s; }
        .tool-card:hover .tool-arrow { transform: translateX(4px); }
        .quick-translate { background: var(--surface); border-radius: var(--radius); padding: 24px; box-shadow: var(--shadow); border: 1px solid var(--border); margin-bottom: 24px; }
        .qt-header { font-family: 'Playfair Display', serif; font-size: 1.125rem; font-weight: 600; margin-bottom: 16px; display: flex; align-items: center; gap: 8px; color: var(--primary); }
        .qt-boxes { display: grid; grid-template-columns: 1fr; gap: 12px; }
        @media (min-width: 640px) { .qt-boxes { grid-template-columns: 1fr auto 1fr; } }
        .qt-textarea { width: 100%; min-height: 120px; padding: 16px; border: 2px solid var(--border); border-radius: var(--radius-sm); font-family: inherit; font-size: 1rem; resize: vertical; transition: all 0.3s; }
        .qt-textarea:focus { outline: none; border-color: var(--primary); }
        .qt-textarea[dir="rtl"] { font-family: 'Noto Naskh Arabic', serif; font-size: 1.1rem; }
        .qt-divider { display: flex; align-items: center; justify-content: center; color: var(--text-light); }
        .qt-btn { width: 100%; padding: 14px; background: linear-gradient(135deg, var(--primary), var(--primary-dark)); color: white; border: none; border-radius: var(--radius-sm); font-family: inherit; font-size: 1rem; font-weight: 600; cursor: pointer; transition: all 0.3s; margin-top: 12px; }
        .qt-btn:hover { transform: translateY(-2px); box-shadow: 0 8px 20px rgba(30,58,95,0.3); }
        .loading { text-align: center; padding: 40px; color: var(--text-light); }
        .spinner { width: 40px; height: 40px; border: 3px solid var(--border); border-top-color: var(--primary); border-radius: 50%; animation: spin 0.8s linear infinite; margin: 0 auto 16px; }
        @keyframes spin { to { transform: rotate(360deg); } }
        .presenter-section { margin-top: 60px; margin-bottom: 40px; padding: 40px 30px; background: linear-gradient(135deg, var(--surface), rgba(30,58,95,0.02)); border-radius: var(--radius); box-shadow: var(--shadow); border: 1px solid var(--border); text-align: center; position: relative; overflow: hidden; }
        .presenter-section::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 4px; background: linear-gradient(90deg, var(--primary), var(--accent), var(--primary)); }
        .presenter-image { width: 180px; height: 180px; border-radius: 50%; object-fit: cover; border: 4px solid var(--accent); box-shadow: 0 8px 30px rgba(30,58,95,0.2); margin-bottom: 24px; transition: transform 0.3s ease; }
        .presenter-image:hover { transform: scale(1.05); }
        .presenter-name { font-family: 'Playfair Display', serif; font-size: 1.8rem; font-weight: 700; color: var(--primary); margin-bottom: 12px; }
        .presenter-tagline { font-size: 1.1rem; color: var(--text-light); line-height: 1.7; max-width: 600px; margin: 0 auto 20px; }
        .presenter-cta { display: inline-block; padding: 12px 32px; background: linear-gradient(135deg, var(--primary), var(--primary-light)); color: white; border-radius: 30px; font-weight: 600; font-size: 1rem; text-decoration: none; transition: all 0.3s; box-shadow: 0 4px 15px rgba(30,58,95,0.3); }
        .presenter-cta:hover { transform: translateY(-2px); box-shadow: 0 8px 25px rgba(30,58,95,0.4); }
        .divider-line { width: 60px; height: 3px; background: var(--accent); border-radius: 2px; margin: 20px auto; }
        @media (max-width: 640px) { .logo { font-size: 2.2rem; } .result-card { padding: 20px; } .word-title { font-size: 1.8rem; } .arabic-text { font-size: 1.2rem; } .presenter-image { width: 140px; height: 140px; } .presenter-name { font-size: 1.4rem; } .presenter-tagline { font-size: 1rem; } }
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb { background: var(--border); border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: var(--text-light); }
        .toast { position: fixed; top: 20px; left: 50%; transform: translateX(-50%) translateY(-100px); background: var(--surface); color: var(--text); padding: 12px 24px; border-radius: var(--radius-sm); box-shadow: var(--shadow-lg); border: 1px solid var(--border); z-index: 2000; font-weight: 500; transition: transform 0.3s cubic-bezier(0.4,0,0.2,1); display: flex; align-items: center; gap: 8px; }
        .toast.show { transform: translateX(-50%) translateY(0); }
        .toast svg { width: 20px; height: 20px; color: #10b981; }
    </style>
</head>
<body>
    <div class="bg-animation"></div>
    <div class="orb orb-1"></div>
    <div class="orb orb-2"></div>
    <div class="orb orb-3"></div>
    <div class="app-container">
        <header class="header">
            <h1 class="logo">English Made Easy</h1>
            <p class="tagline">Your Personal English Learning Companion</p>
        </header>
        <div id="page-search" class="page active">
            <div class="search-container">
                <input type="text" id="searchInput" class="search-box" placeholder="Search for a word..." autocomplete="off">
                <svg class="search-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="11" cy="11" r="8"></circle><path d="m21 21-4.35-4.35"></path></svg>
                <div id="suggestions" class="suggestions"></div>
            </div>
            <div id="searchResults"></div>
            <div id="initialState" style="text-align: center; padding: 60px 20px; color: var(--text-light);">
                <svg width="80" height="80" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" style="margin-bottom: 16px; opacity: 0.4;"><circle cx="11" cy="11" r="8"></circle><path d="m21 21-4.35-4.35"></path></svg>
                <p style="font-size: 1.1rem;">Type a word to see definitions, pronunciations, and examples</p>
            </div>
            <div class="presenter-section">
                <img src="/mnt/agents/upload/ChatGPT Image 13 يونيو 2025، 03_05_23 ص.png" alt="Yassin Jamal" class="presenter-image">
                <div class="divider-line"></div>
                <h2 class="presenter-name">Yassin Jamal</h2>
                <p class="presenter-tagline">
                    Presents a website to save you time while learning English.<br>
                    All you have to do is search for the word you want.<br>
                    <strong>What are you waiting for? Go search now!</strong>
                </p>
                <a href="#" class="presenter-cta" onclick="document.getElementById('searchInput').focus(); return false;">Start Searching</a>
            </div>
        </div>
        <div id="page-library" class="page">
            <div class="library-header">
                <h2 class="library-title">My Library</h2>
                <span class="library-count" id="savedCount">0</span>
            </div>
            <div id="savedList" class="saved-list">
                <div class="empty-state">
                    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M11.049 2.927c.3-.921 1.603-.921 1.902 0l1.519 4.674a1 1 0 00.95.69h4.915c.969 0 1.371 1.24.588 1.81l-3.976 2.888a1 1 0 00-.363 1.118l1.518 4.674c.3.922-.755 1.688-1.538 1.118l-3.976-2.888a1 1 0 00-1.176 0l-3.976 2.888c-.783.57-1.838-.197-1.538-1.118l1.518-4.674a1 1 0 00-.363-1.118l-3.976-2.888c-.784-.57-.38-1.81.588-1.81h4.914a1 1 0 00.951-.69l1.519-4.674z"/></svg>
                    <h3>No saved words yet</h3>
                    <p>Search for words and click the star to save them here</p>
                </div>
            </div>
        </div>
        <div id="page-tools" class="page">
            <h2 style="font-family: 'Playfair Display', serif; font-size: 1.8rem; font-weight: 700; color: var(--primary); margin-bottom: 8px;">Tools</h2>
            <p style="color: var(--text-light); margin-bottom: 24px;">Helpful resources for your learning journey</p>
            <div class="quick-translate">
                <div class="qt-header"><span>🌐</span> Quick Translate (English ↔ Arabic)</div>
                <div class="qt-boxes">
                    <textarea id="sourceText" class="qt-textarea" placeholder="Enter English text..."></textarea>
                    <div class="qt-divider"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h14M12 5l7 7-7 7"/></svg></div>
                    <textarea id="targetText" class="qt-textarea" placeholder="الترجمة تظهر هنا..." dir="rtl" readonly></textarea>
                </div>
                <button class="qt-btn" onclick="quickTranslate()">Translate to Arabic</button>
            </div>
            <div class="tools-grid">
                <a href="https://translate.google.com/?sl=en&tl=ar" target="_blank" class="tool-card"><div class="tool-icon translate">🌐</div><div class="tool-title">Google Translate</div><div class="tool-desc">Full Google Translate interface with English to Arabic support, voice input, and camera translation.</div><div class="tool-arrow">→</div></a>
                <a href="https://www.thesaurus.com/" target="_blank" class="tool-card"><div class="tool-icon thesaurus">📚</div><div class="tool-title">Thesaurus.com</div><div class="tool-desc">Find synonyms and antonyms to expand your vocabulary and express yourself better.</div><div class="tool-arrow">→</div></a>
                <a href="https://www.grammarly.com/" target="_blank" class="tool-card"><div class="tool-icon grammar">✍️</div><div class="tool-title">Grammarly</div><div class="tool-desc">Check your English writing for grammar, spelling, and style improvements.</div><div class="tool-arrow">→</div></a>
                <a href="https://youglish.com/" target="_blank" class="tool-card"><div class="tool-icon" style="background: linear-gradient(135deg, #10b981, #059669);">🎥</div><div class="tool-title">YouGlish</div><div class="tool-desc">Search YouTube videos to hear how words are pronounced by native speakers in context.</div><div class="tool-arrow">→</div></a>
                <a href="https://www.oxfordlearnersdictionaries.com/" target="_blank" class="tool-card"><div class="tool-icon" style="background: linear-gradient(135deg, #f97316, #ea580c);">📖</div><div class="tool-title">Oxford Learner's</div><div class="tool-desc">Alternative dictionary with British English focus and detailed learner guides.</div><div class="tool-arrow">→</div></a>
                <a href="https://www.bbc.co.uk/learningenglish/" target="_blank" class="tool-card"><div class="tool-icon" style="background: linear-gradient(135deg, #ef4444, #dc2626);">🇬🇧</div><div class="tool-title">BBC Learning English</div><div class="tool-desc">Free English lessons, videos, and quizzes from the BBC.</div><div class="tool-arrow">→</div></a>
            </div>
        </div>
    </div>
    <div id="toast" class="toast"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 13l4 4L19 7"/></svg><span id="toastMessage">Word saved!</span></div>
    <nav class="nav-container">
        <div class="nav-items">
            <button class="nav-item active" onclick="switchPage('search')">
                <svg class="nav-icon" viewBox="0 0 24 24"><circle cx="11" cy="11" r="8"></circle><path d="m21 21-4.35-4.35"></path></svg>
                <span class="nav-label">Search</span>
            </button>
            <button class="nav-item" onclick="switchPage('library')">
                <svg class="nav-icon" viewBox="0 0 24 24"><path d="M19 21l-7-5-7 5V5a2 2 0 0 1 2-2h10a2 2 0 0 1 2 2z"></path></svg>
                <span class="nav-label">Library</span>
            </button>
            <button class="nav-item" onclick="switchPage('tools')">
                <svg class="nav-icon" viewBox="0 0 24 24"><path d="M14.7 6.3a1 1 0 0 0 0 1.4l1.6 1.6a1 1 0 0 0 1.4 0l3.77-3.77a6 6 0 0 1-7.94 7.94l-6.91 6.91a2.12 2.12 0 0 1-3-3l6.91-6.91a6 6 0 0 1 7.94-7.94l-3.76 3.76z"></path></svg>
                <span class="nav-label">Tools</span>
            </button>
        </div>
    </nav>
    <script>
// State Management
let savedWords = JSON.parse(localStorage.getItem('englishmadeeasy_saved')) || [];
let currentWord = null;
let debounceTimer;

// Common English words for suggestions
const commonWords = [
    "ability","able","about","above","accept","according","account","across","act","action",
    "activity","actually","add","address","administration","admit","adult","affect","after",
    "again","against","age","agency","agent","ago","agree","agreement","ahead","air","all",
    "allow","almost","alone","along","already","also","although","always","American","among",
    "amount","analysis","and","animal","another","answer","any","anyone","anything","appear",
    "apply","approach","area","argue","arm","around","arrive","art","article","artist","as",
    "ask","assume","at","attack","attention","attorney","audience","author","authority","available",
    "avoid","away","baby","back","bad","bag","ball","bank","bar","base","be","beat","beautiful",
    "because","become","bed","before","begin","behavior","behind","believe","benefit","best","better",
    "between","beyond","big","bill","billion","bit","black","blood","blue","board","body","book",
    "born","both","box","boy","break","bring","brother","budget","build","building","business",
    "but","buy","by","call","camera","campaign","can","cancer","candidate","capital","car","card",
    "care","career","carry","case","catch","cause","cell","center","central","century","certain",
    "certainly","chair","challenge","chance","change","character","charge","check","child","choice",
    "choose","church","citizen","city","civil","claim","class","clear","clearly","close","coach",
    "cold","collection","college","color","come","commercial","common","community","company",
    "compare","computer","concern","condition","conference","Congress","consider","consumer",
    "contain","continue","control","cost","could","country","couple","course","court","cover",
    "create","crime","cultural","culture","cup","current","customer","cut","dark","data","daughter",
    "day","dead","deal","death","debate","decade","decide","decision","deep","defense","degree",
    "Democrat","democratic","describe","design","despite","detail","determine","develop","development",
    "die","difference","different","difficult","dinner","direction","director","discover","discuss",
    "discussion","disease","do","doctor","dog","door","down","draw","dream","drive","drop","drug",
    "during","each","early","east","easy","eat","economic","economy","edge","education","effect",
    "effort","eight","either","election","else","employee","end","energy","enjoy","enough","enter",
    "entire","environment","environmental","especially","establish","even","evening","event","ever",
    "every","everybody","everyone","everything","evidence","exactly","example","executive","exist",
    "expect","experience","expert","explain","eye","face","fact","factor","fail","fall","family",
    "far","fast","father","fear","federal","feel","feeling","few","field","fight","figure","fill",
    "film","final","finally","financial","find","fine","finger","finish","fire","firm","first",
    "fish","five","floor","fly","focus","follow","food","foot","for","force","foreign","forget",
    "form","former","forward","four","free","friend","from","front","full","fund","future","game",
    "garden","gas","general","generation","get","girl","give","glass","go","goal","good",
    "government","great","green","ground","group","grow","growth","guess","gun","guy","hair",
    "half","hand","hang","happen","happy","hard","have","he","head","health","hear","heart",
    "heat","heavy","help","her","here","herself","high","him","himself","his","history","hit",
    "hold","home","hope","hospital","hot","hotel","hour","house","how","however","huge","human",
    "hundred","husband","I","idea","identify","if","image","imagine","impact","important","improve",
    "in","include","including","increase","indeed","indicate","individual","industry","information",
    "inside","instead","institution","interest","interesting","international","interview","into",
    "investment","involve","issue","it","item","its","itself","job","join","just","keep","key",
    "kid","kill","kind","kitchen","know","knowledge","land","language","large","last","late",
    "later","laugh","law","lawyer","lay","lead","leader","learn","least","leave","left","leg",
    "legal","less","let","letter","level","lie","life","light","like","likely","line","list",
    "listen","little","live","local","long","look","lose","loss","lot","love","low","machine",
    "magazine","main","maintain","major","majority","make","man","manage","management","manager",
    "many","market","marriage","material","matter","may","maybe","me","mean","measure","media",
    "medical","meet","meeting","member","memory","mention","message","method","middle","might",
    "military","million","mind","minute","miss","mission","model","modern","moment","money",
    "month","more","morning","most","mother","mouth","move","movement","movie","Mr","Mrs","much",
    "music","must","my","myself","name","nation","national","natural","nature","near","nearly",
    "necessary","need","network","never","new","news","newspaper","next","nice","night","no",
    "none","nor","north","not","note","nothing","notice","now","number","occur","of","off",
    "offer","office","officer","official","often","oh","oil","ok","old","on","once","one",
    "only","onto","open","operation","opportunity","option","or","order","organization","other",
    "others","our","out","outside","over","own","owner","page","pain","painting","paper","parent",
    "park","part","participant","particular","particularly","partner","party","pass","past","patient",
    "pattern","pay","peace","people","per","perform","performance","perhaps","period","person",
    "personal","phone","physical","pick","picture","piece","place","plan","plant","play","player",
    "PM","point","police","policy","political","politics","poor","popular","population","position",
    "positive","possible","power","practice","prepare","present","president","pressure","pretty",
    "prevent","price","private","probably","problem","process","produce","product","production",
    "professional","professor","program","project","property","protect","prove","provide","public",
    "pull","purpose","push","put","quality","question","quickly","quite","race","radio","raise",
    "range","rate","rather","reach","read","ready","real","reality","realize","really","reason",
    "receive","recent","recently","recognize","record","red","reduce","reflect","region","relate",
    "relationship","religious","remain","remember","remove","report","represent","Republican",
    "require","research","resource","respond","response","responsibility","rest","result","return",
    "reveal","rich","right","rise","risk","road","rock","role","room","rule","run","safe","same",
    "save","say","scene","school","science","scientist","score","sea","season","seat","second",
    "section","security","see","seek","seem","sell","send","senior","sense","series","serious",
    "serve","service","set","seven","several","sex","sexual","shake","share","she","shoot",
    "short","shot","should","shoulder","show","side","sign","significant","similar","simple",
    "simply","since","sing","single","sister","sit","site","situation","six","size","skill",
    "skin","small","smile","so","social","society","soldier","some","somebody","someone",
    "something","sometimes","son","song","soon","sort","sound","source","south","southern",
    "space","speak","special","specific","speech","spend","sport","spring","staff","stage",
    "stand","standard","star","start","state","statement","station","stay","step","still","stock",
    "stop","store","story","strategy","street","strong","structure","student","studio","study",
    "stuff","style","subject","success","successful","such","suddenly","suffer","suggest","summer",
    "support","sure","surface","system","table","take","talk","task","tax","teach","teacher",
    "team","technology","television","tell","ten","tend","term","test","than","thank","that",
    "the","their","them","themselves","then","theory","there","these","they","thing","think",
    "third","this","those","though","thought","thousand","threat","three","through","throughout",
    "throw","thus","time","to","today","together","tonight","too","top","total","tough","toward",
    "town","trade","traditional","training","travel","treat","treatment","tree","trial","trip",
    "trouble","true","truth","try","turn","TV","two","type","under","understand","unit","until",
    "up","upon","us","use","usually","value","various","very","victim","view","violence","visit",
    "voice","vote","wait","walk","wall","want","war","watch","water","way","we","weapon","wear",
    "week","weight","well","west","western","what","whatever","when","where","whether","which",
    "while","white","who","whole","whom","whose","why","wide","wife","will","win","wind",
    "window","wish","with","within","without","woman","wonder","word","work","worker","world",
    "worry","would","write","writer","wrong","yard","yeah","year","yes","yet","you","young",
    "your","yourself"
];

// Page Switching
function switchPage(pageName) {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
    document.getElementById('page-' + pageName).classList.add('active');
    event.currentTarget.classList.add('active');
    if (pageName === 'library') renderLibrary();
}

// Search Suggestions
const searchInput = document.getElementById('searchInput');
const suggestionsBox = document.getElementById('suggestions');

searchInput.addEventListener('input', (e) => {
    clearTimeout(debounceTimer);
    const query = e.target.value.trim().toLowerCase();
    if (query.length < 1) {
        suggestionsBox.classList.remove('show');
        return;
    }
    debounceTimer = setTimeout(() => {
        const matches = commonWords.filter(w => 
            w.toLowerCase().startsWith(query) || w.toLowerCase().includes(query)
        ).slice(0, 8);
        if (matches.length > 0) {
            let html = '';
            for (let word of matches) {
                html += '<div class="suggestion-item" onclick="selectWord(' + "'" + word + "'" + ')">' +
                    '<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" style="color: var(--text-light);">' +
                    '<circle cx="11" cy="11" r="8"></circle><path d="m21 21-4.35-4.35"></path></svg>' +
                    '<span class="suggestion-text">' + word + '</span>' +
                    '<span class="suggestion-type">word</span></div>';
            }
            suggestionsBox.innerHTML = html;
            suggestionsBox.classList.add('show');
        } else {
            suggestionsBox.classList.remove('show');
        }
    }, 150);
});

searchInput.addEventListener('keypress', (e) => {
    if (e.key === 'Enter') {
        suggestionsBox.classList.remove('show');
        performSearch(searchInput.value.trim());
    }
});

document.addEventListener('click', (e) => {
    if (!e.target.closest('.search-container')) {
        suggestionsBox.classList.remove('show');
    }
});

function selectWord(word) {
    searchInput.value = word;
    suggestionsBox.classList.remove('show');
    performSearch(word);
}

// Dictionary API Integration
async function performSearch(word) {
    if (!word) return;
    const resultsDiv = document.getElementById('searchResults');
    const initialState = document.getElementById('initialState');
    initialState.style.display = 'none';
    resultsDiv.innerHTML = '<div class="loading"><div class="spinner"></div>Searching...</div>';
    try {
        const response = await fetch('https://api.dictionaryapi.dev/api/v2/entries/en/' + encodeURIComponent(word));
        const data = await response.json();
        if (response.ok) {
            currentWord = data[0];
            renderResult(data[0]);
        } else {
            resultsDiv.innerHTML = '<div class="result-card" style="text-align: center; color: var(--text-light);">' +
                '<svg width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" style="margin-bottom: 12px; opacity: 0.5;">' +
                '<circle cx="12" cy="12" r="10"></circle><path d="M12 8v4M12 16h.01"></path></svg>' +
                '<h3>Word not found</h3><p>Try checking the spelling or search for a different word</p></div>';
        }
    } catch (error) {
        resultsDiv.innerHTML = '<div class="result-card" style="text-align: center; color: var(--text-light);">' +
            '<p>Connection error. Please check your internet and try again.</p></div>';
    }
}

function renderResult(data) {
    const isSaved = savedWords.some(w => w.word === data.word);
    const phonetic = data.phonetic || (data.phonetics && data.phonetics.find(p => p.text)?.text) || '';
    const ukAudio = data.phonetics?.find(p => p.audio && (p.audio.includes('uk') || p.audio.includes('gb')))?.audio || '';
    const usAudio = data.phonetics?.find(p => p.audio && (p.audio.includes('us') || p.audio.includes('aa')))?.audio || '';
    const anyAudio = data.phonetics?.find(p => p.audio)?.audio || '';

    let html = '<div class="result-card">' +
        '<div class="word-header"><div>' +
        '<h2 class="word-title">' + data.word + '</h2>' +
        (phonetic ? '<span class="phonetic">' + phonetic + '</span>' : '') +
        '</div>' +
        '<button class="star-btn ' + (isSaved ? 'saved' : '') + '" onclick="toggleSave(' + "'" + data.word + "'" + ')" title="' + (isSaved ? 'Remove from library' : 'Save to library') + '">' +
        '<svg width="28" height="28" viewBox="0 0 24 24" fill="' + (isSaved ? 'currentColor' : 'none') + '" stroke="currentColor" stroke-width="2">' +
        '<path d="M11.049 2.927c.3-.921 1.603-.921 1.902 0l1.519 4.674a1 1 0 00.95.69h4.915c.969 0 1.371 1.24.588 1.81l-3.976 2.888a1 1 0 00-.363 1.118l1.518 4.674c.3.922-.755 1.688-1.538 1.118l-3.976-2.888a1 1 0 00-1.176 0l-3.976 2.888c-.783.57-1.838-.197-1.538-1.118l1.518-4.674a1 1 0 00-.363-1.118l-3.976-2.888c-.784-.57-.38-1.81.588-1.81h4.914a1 1 0 00.951-.69l1.519-4.674z"/></svg></button></div>';

    if (ukAudio || usAudio || anyAudio) {
        html += '<div class="audio-section">';
        if (ukAudio) {
            html += '<button class="audio-btn" onclick="playAudio(' + "'" + ukAudio + "'" + ')">' +
                '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">' +
                '<polygon points="11 5 6 9 2 9 2 15 6 15 11 19 11 5"></polygon>' +
                '<path d="M19.07 4.93a10 10 0 0 1 0 14.14M15.54 8.46a5 5 0 0 1 0 7.07"></path></svg>UK Pronunciation</button>';
        }
        if (usAudio) {
            html += '<button class="audio-btn" onclick="playAudio(' + "'" + usAudio + "'" + ')">' +
                '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">' +
                '<polygon points="11 5 6 9 2 9 2 15 6 15 11 19 11 5"></polygon>' +
                '<path d="M19.07 4.93a10 10 0 0 1 0 14.14M15.54 8.46a5 5 0 0 1 0 7.07"></path></svg>US Pronunciation</button>';
        }
        if (!ukAudio && !usAudio && anyAudio) {
            html += '<button class="audio-btn" onclick="playAudio(' + "'" + anyAudio + "'" + ')">' +
                '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">' +
                '<polygon points="11 5 6 9 2 9 2 15 6 15 11 19 11 5"></polygon>' +
                '<path d="M19.07 4.93a10 10 0 0 1 0 14.14M15.54 8.46a5 5 0 0 1 0 7.07"></path></svg>Listen</button>';
        }
        html += '</div>';
    }

    html += '<div class="meanings-section">';
    for (let meaning of data.meanings) {
        html += '<div style="margin-bottom: 24px;">' +
            '<div class="part-of-speech">' + meaning.partOfSpeech + '</div>' +
            '<ol class="meaning-list" style="list-style: none; padding: 0;">';
        let defs = meaning.definitions.slice(0, 4);
        for (let i = 0; i < defs.length; i++) {
            let def = defs[i];
            let example = '';
            if (def.example) {
                let regex = new RegExp(data.word, 'gi');
                example = def.example.replace(regex, '<span class="example-word">' + data.word + '</span>');
            }
            html += '<li class="meaning-item">' +
                '<div class="definition">' + (i + 1) + '. ' + def.definition + '</div>' +
                (example ? '<div class="example">"' + example + '"</div>' : '') +
                '</li>';
        }
        html += '</ol>';
        let ants = meaning.antonyms || [];
        if (ants.length > 0) {
            html += '<div class="antonyms-section"><div class="antonyms-title">Antonyms</div>';
            for (let ant of ants.slice(0, 6)) {
                html += '<span class="antonym-tag" onclick="performSearch(' + "'" + ant + "'" + ')">' + ant + '</span>';
            }
            html += '</div>';
        }
        html += '</div>';
    }
    html += '</div>';

    html += '<div class="arabic-section">' +
        '<div class="arabic-title"><svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">' +
        '<path d="M5 8l6 6M11 8l-6 6M19 5v14"/></svg>Arabic Translation</div>' +
        '<div class="arabic-text" id="arabicTranslation">Loading...</div>' +
        '<a href="https://translate.google.com/?sl=en&tl=ar&text=' + encodeURIComponent(data.word) + '" target="_blank" class="translate-link">' +
        'Open in Google Translate<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">' +
        '<path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6M15 3h6v6M10 14L21 3"/></svg></a></div>';
    html += '</div>';

    document.getElementById('searchResults').innerHTML = html;
    fetchArabicTranslation(data.word);
}

async function fetchArabicTranslation(word) {
    try {
        const response = await fetch('https://api.mymemory.translated.net/get?q=' + encodeURIComponent(word) + '&langpair=en|ar');
        const data = await response.json();
        const el = document.getElementById('arabicTranslation');
        if (el) {
            if (data.responseData && data.responseData.translatedText) {
                el.textContent = data.responseData.translatedText;
            } else {
                el.textContent = '—';
            }
        }
    } catch (e) {
        const el = document.getElementById('arabicTranslation');
        if (el) el.textContent = '—';
    }
}

function playAudio(url) {
    const audio = new Audio(url);
    audio.play().catch(e => {
        showToast('Audio not available for this word');
    });
}

function toggleSave(word) {
    const index = savedWords.findIndex(w => w.word === word);
    if (index > -1) {
        savedWords.splice(index, 1);
        showToast('Removed from library');
    } else {
        const wordData = {
            word: word,
            savedAt: new Date().toISOString(),
            phonetic: currentWord && currentWord.phonetic ? currentWord.phonetic : ''
        };
        savedWords.push(wordData);
        showToast('Saved to library!');
    }
    localStorage.setItem('englishmadeeasy_saved', JSON.stringify(savedWords));
    const starBtn = document.querySelector('.star-btn');
    if (starBtn) {
        starBtn.classList.toggle('saved');
        const isSaved = index === -1;
        starBtn.title = isSaved ? 'Remove from library' : 'Save to library';
        starBtn.querySelector('svg').setAttribute('fill', isSaved ? 'currentColor' : 'none');
    }
}

function renderLibrary() {
    const list = document.getElementById('savedList');
    const count = document.getElementById('savedCount');
    count.textContent = savedWords.length;
    if (savedWords.length === 0) {
        list.innerHTML = '<div class="empty-state">' +
            '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">' +
            '<path d="M11.049 2.927c.3-.921 1.603-.921 1.902 0l1.519 4.674a1 1 0 00.95.69h4.915c.969 0 1.371 1.24.588 1.81l-3.976 2.888a1 1 0 00-.363 1.118l1.518 4.674c.3.922-.755 1.688-1.538 1.118l-3.976-2.888a1 1 0 00-1.176 0l-3.976 2.888c-.783.57-1.838-.197-1.538-1.118l1.518-4.674a1 1 0 00-.363-1.118l-3.976-2.888c-.784-.57-.38-1.81.588-1.81h4.914a1 1 0 00.951-.69l1.519-4.674z"/></svg>' +
            '<h3>No saved words yet</h3><p>Search for words and click the star to save them here</p></div>';
        return;
    }
    let html = '';
    const reversed = savedWords.slice().reverse();
    for (let item of reversed) {
        html += '<div class="saved-item" onclick="loadSavedWord(' + "'" + item.word + "'" + ')">' +
            '<div class="saved-word-info"><h3>' + item.word + '</h3>' +
            '<p>' + (item.phonetic || '') + ' &bull; Saved ' + new Date(item.savedAt).toLocaleDateString() + '</p></div>' +
            '<button class="saved-star" onclick="event.stopPropagation(); removeWord(' + "'" + item.word + "'" + ')">' +
            '<svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor" stroke="currentColor" stroke-width="2">' +
            '<path d="M11.049 2.927c.3-.921 1.603-.921 1.902 0l1.519 4.674a1 1 0 00.95.69h4.915c.969 0 1.371 1.24.588 1.81l-3.976 2.888a1 1 0 00-.363 1.118l1.518 4.674c.3.922-.755 1.688-1.538 1.118l-3.976-2.888a1 1 0 00-1.176 0l-3.976 2.888c-.783.57-1.838-.197-1.538-1.118l1.518-4.674a1 1 0 00-.363-1.118l-3.976-2.888c-.784-.57-.38-1.81.588-1.81h4.914a1 1 0 00.951-.69l1.519-4.674z"/></svg></button></div>';
    }
    list.innerHTML = html;
}

function removeWord(word) {
    savedWords = savedWords.filter(w => w.word !== word);
    localStorage.setItem('englishmadeeasy_saved', JSON.stringify(savedWords));
    renderLibrary();
    showToast('Removed from library');
}

function loadSavedWord(word) {
    switchPage('search');
    searchInput.value = word;
    performSearch(word);
}

async function quickTranslate() {
    const source = document.getElementById('sourceText').value.trim();
    const target = document.getElementById('targetText');
    if (!source) {
        target.value = '';
        return;
    }
    target.value = '... translating';
    try {
        const response = await fetch('https://api.mymemory.translated.net/get?q=' + encodeURIComponent(source) + '&langpair=en|ar');
        const data = await response.json();
        if (data.responseData && data.responseData.translatedText) {
            target.value = data.responseData.translatedText;
        } else {
            target.value = 'Translation error. Please try again.';
        }
    } catch (e) {
        target.value = 'Connection error. Please check your internet.';
    }
}

function showToast(message) {
    const toast = document.getElementById('toast');
    document.getElementById('toastMessage').textContent = message;
    toast.classList.add('show');
    setTimeout(() => {
        toast.classList.remove('show');
    }, 2500);
}

document.addEventListener('DOMContentLoaded', () => {
    searchInput.focus();
});
    </script>
</body>
</html>
