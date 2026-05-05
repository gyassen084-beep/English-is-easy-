# English-is-easy-
A website to save time in learning English 

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>English Is Easy | Visionary Edition</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap" rel="stylesheet">
    <style>
        :root { --j-blue: #004AAD; --j-teal: #00B4D8; }
        
        body { 
            font-family: 'Plus Jakarta Sans', sans-serif; 
            margin: 0; min-height: 100vh;
            background: linear-gradient(135deg, #f8fafc, #e0f2fe, #f1f5f9, #dcfce7, #f8fafc);
            background-size: 400% 400%;
            animation: flow 20s ease-in-out infinite;
        }

        @keyframes flow { 0% { background-position: 0% 50%; } 50% { background-position: 100% 50%; } 100% { background-position: 0% 50%; } }

        .glass-panel { 
            background: rgba(255, 255, 255, 0.85); 
            backdrop-filter: blur(40px); 
            border: 1px solid rgba(255, 255, 255, 0.6);
            box-shadow: 0 30px 60px rgba(0, 74, 173, 0.05);
        }

        .clickable-word {
            cursor: pointer; transition: all 0.2s;
            border-bottom: 2px solid transparent;
        }
        .clickable-word:hover {
            color: #004AAD; background: rgba(0, 180, 216, 0.1);
            border-bottom-color: #00B4D8; border-radius: 4px;
        }

        /* STAR STYLING */
        .sentence-star {
            transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            cursor: pointer;
            filter: drop-shadow(0 0 0px transparent);
        }
        .sentence-star.active {
            fill: #FFD700 !important;
            stroke: #FFD700 !important;
            filter: drop-shadow(0 0 8px rgba(255, 215, 0, 0.6));
            transform: scale(1.2);
        }

        .image-shimmer {
            background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
            background-size: 200% 100%;
            animation: shimmer 1.5s infinite;
        }
        @keyframes shimmer { 0% { background-position: 200% 0; } 100% { background-position: -200% 0; } }
    </style>
</head>
<body class="pb-40">

    <header class="p-10 max-w-6xl mx-auto w-full flex justify-between items-center">
        <div>
            <h1 class="text-4xl font-black tracking-tighter text-slate-900">ENGLISH IS EASY</h1>
            <p class="text-[12px] font-bold text-blue-500 tracking-[0.4em] uppercase opacity-80">If it suits you</p>
        </div>
    </header>

    <main class="max-w-5xl mx-auto px-6 w-full">
        
        <div id="searchView" class="mb-12">
            <div class="relative z-50">
                <input type="text" id="wordInput" autocomplete="off" placeholder="Search and visualize..." 
                    class="w-full h-24 pl-20 pr-6 bg-white/95 rounded-[45px] shadow-2xl border-none outline-none text-3xl font-bold text-slate-800">
                <div id="predictionTray" class="glass-panel overflow-hidden transition-all duration-300 opacity-0 rounded-[35px] mt-4 max-h-0"></div>
            </div>

            <div id="resultBox" class="hidden mt-12 space-y-10 animate-in slide-in-from-bottom-10 duration-700">
                
                <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
                    <div class="lg:col-span-2 glass-panel p-12 rounded-[50px] relative">
                        <div class="flex justify-between items-start mb-8">
                            <h1 id="resWord" class="text-8xl font-black tracking-tighter text-slate-900 capitalize leading-none">...</h1>
                            <button onclick="toggleWordFav()" class="w-16 h-16 bg-white rounded-3xl shadow-md border flex items-center justify-center hover:scale-110 transition-all">
                                <svg id="mainStar" width="30" height="30" viewBox="0 0 24 24" fill="none" stroke="#CBD5E1" stroke-width="2.5"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"></polygon></svg>
                            </button>
                        </div>
                        <div class="flex items-center gap-4 mb-6">
                            <span id="resPos" class="px-5 py-2 bg-slate-900 text-white rounded-full text-xs font-black uppercase">Type</span>
                            <span id="resIpa" class="text-2xl text-slate-300 font-medium tracking-widest">/ipa/</span>
                            <button onclick="playAudio()" class="p-3 bg-blue-500 text-white rounded-2xl hover:scale-110 transition-all">
                                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3"><polygon points="11 5 6 9 2 9 2 15 6 15 11 19 11 5"></polygon></svg>
                            </button>
                        </div>
                        <p id="resDef" class="text-3xl text-slate-700 leading-snug font-bold border-l-8 border-blue-500 pl-8"></p>
                    </div>

                    <div class="glass-panel p-4 rounded-[50px] overflow-hidden min-h-[300px]">
                        <img id="wordImage" class="w-full h-full object-cover rounded-[40px] hidden" alt="visual aid">
                        <div id="imageLoader" class="w-full h-full rounded-[40px] image-shimmer"></div>
                    </div>
                </div>

                <div id="sentenceGrid" class="grid grid-cols-1 gap-6"></div>
            </div>
        </div>

        <div id="vaultView" class="hidden animate-in fade-in">
            <h2 class="text-6xl font-black tracking-tighter mb-10">The Library</h2>
            <div id="vaultContainer" class="grid grid-cols-1 md:grid-cols-2 gap-6"></div>
        </div>
    </main>

    <nav class="fixed bottom-10 left-1/2 -translate-x-1/2 w-[92%] max-w-lg bg-slate-900/95 backdrop-blur-xl h-24 rounded-[50px] flex items-center justify-around px-4 shadow-2xl z-50 border border-white/10">
        <button onclick="navTo('vault')" class="flex flex-col items-center gap-1 text-slate-400">
            <svg width="26" height="26" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M12 21V9M18 21V5M6 21v-7"/></svg>
            <span class="text-[9px] font-black uppercase">Vault</span>
        </button>

        <button onclick="navTo('search')" class="p-7 bg-blue-500 text-white rounded-full -translate-y-12 shadow-2xl shadow-blue-500/40">
            <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="4"><circle cx="11" cy="11" r="8"/><line x1="21" y1="21" x2="16.65" y2="16.65"/></svg>
        </button>

        <button onclick="window.open('https://translate.google.com')" class="flex flex-col items-center gap-1 text-slate-400">
            <svg width="26" height="26" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><circle cx="12" cy="12" r="10"/><path d="M2 12h20M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"/></svg>
            <span class="text-[9px] font-black uppercase">Translate</span>
        </button>
    </nav>

    <script>
        let currentWord = null;
        let savedWords = JSON.parse(localStorage.getItem('vision_words')) || [];
        let savedPhrases = JSON.parse(localStorage.getItem('vision_phrases')) || [];

        const input = document.getElementById('wordInput');
        const tray = document.getElementById('predictionTray');

        function navTo(page) {
            document.getElementById('searchView').classList.toggle('hidden', page === 'vault');
            document.getElementById('vaultView').classList.toggle('hidden', page === 'search');
            if(page === 'vault') renderVault();
        }

        input.addEventListener('input', async (e) => {
            const q = e.target.value.trim();
            if (q.length < 2) { tray.classList.remove('opacity-100'); tray.style.maxHeight = '0px'; return; }
            const res = await fetch(`https://api.datamuse.com/sug?s=${q}&max=5`);
            const data = await res.json();
            tray.innerHTML = data.map(s => `<div onclick="doSearch('${s.word}')" class="p-5 hover:bg-blue-600 hover:text-white cursor-pointer font-bold text-xl">${s.word}</div>`).join('');
            tray.classList.add('opacity-100'); tray.style.maxHeight = '300px';
        });

        async function doSearch(word) {
            const query = word || input.value.trim();
            if(!query) return;
            input.value = query;
            tray.classList.remove('opacity-100'); tray.style.maxHeight = '0px';
            navTo('search');

            // Image Fetch
            const imgRes = await fetch(`https://source.unsplash.com/800x800/?${query}`);
            const img = document.getElementById('wordImage');
            const loader = document.getElementById('imageLoader');
            img.src = imgRes.url;
            img.onload = () => { img.classList.remove('hidden'); loader.classList.add('hidden'); };

            // Data Fetch
            try {
                const res = await fetch(`https://api.dictionaryapi.dev/api/v2/entries/en/${query}`);
                const data = await res.json();
                currentWord = data[0];
                renderUI(currentWord);
            } catch(e) { alert("Not found."); }
        }

        function renderUI(data) {
            document.getElementById('resultBox').classList.remove('hidden');
            document.getElementById('resWord').innerText = data.word;
            document.getElementById('resPos').innerText = data.meanings[0].partOfSpeech;
            document.getElementById('resIpa').innerText = data.phonetic || "";
            document.getElementById('resDef').innerText = data.meanings[0].definitions[0].definition;

            const grid = document.getElementById('sentenceGrid');
            grid.innerHTML = '';
            data.meanings.forEach(m => {
                m.definitions.forEach(d => {
                    if(d.example) {
                        const isSaved = savedPhrases.includes(d.example);
                        grid.innerHTML += `
                            <div class="glass-panel p-10 rounded-[45px] border-l-8 border-blue-400 relative group">
                                <div class="flex justify-between items-start gap-6">
                                    <p class="text-2xl font-bold text-slate-700 italic leading-relaxed">"${recursive(d.example)}"</p>
                                    <div class="flex flex-col gap-4">
                                        <svg onclick="togglePhrase(this, '${d.example.replace(/'/g,"")}')" class="sentence-star ${isSaved ? 'active' : ''}" width="36" height="36" viewBox="0 0 24 24" fill="none" stroke="#CBD5E1" stroke-width="2.5"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"></polygon></svg>
                                        <button onclick="speak('${d.example.replace(/'/g,"")}')" class="p-3 bg-slate-100 rounded-2xl hover:bg-blue-500 hover:text-white transition-all"><svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3"><polygon points="11 5 6 9 2 9 2 15 6 15 11 19 11 5"></polygon></svg></button>
                                    </div>
                                </div>
                            </div>`;
                    }
                });
            });
            updateWordStar();
        }

        function recursive(text) {
            return text.split(' ').map(w => `<span class="clickable-word" onclick="doSearch('${w.replace(/[.,!]/g,'')}')">${w}</span>`).join(' ');
        }

        function speak(text) {
            const synth = window.speechSynthesis;
            const utter = new SpeechSynthesisUtterance(text);
            utter.lang = 'en-US';
            utter.rate = 0.9;
            synth.speak(utter);
        }

        function togglePhrase(svg, p) {
            const idx = savedPhrases.indexOf(p);
            if(idx > -1) { savedPhrases.splice(idx, 1); svg.classList.remove('active'); }
            else { savedPhrases.push(p); svg.classList.add('active'); }
            localStorage.setItem('vision_phrases', JSON.stringify(savedPhrases));
        }

        function toggleWordFav() {
            const w = currentWord.word;
            const idx = savedWords.findIndex(f => f.word === w);
            if(idx > -1) savedWords.splice(idx, 1);
            else savedWords.push({word: w, def: currentWord.meanings[0].definitions[0].definition});
            localStorage.setItem('vision_words', JSON.stringify(savedWords));
            updateWordStar();
        }

        function updateWordStar() {
            document.getElementById('mainStar').classList.toggle('active', savedWords.some(f => f.word === currentWord.word));
        }

        function renderVault() {
            const container = document.getElementById('vaultContainer');
            container.innerHTML = savedWords.map(w => `<div class="glass-panel p-8 rounded-[40px] border-b-4 border-blue-500 cursor-pointer" onclick="doSearch('${w.word}')"><h3 class="text-3xl font-black mb-2">${w.word}</h3><p class="text-sm text-slate-500 line-clamp-2">${w.def}</p></div>`).join('');
        }

        input.addEventListener('keypress', (e) => { if(e.key === 'Enter') doSearch(); });
    </script>
</body>
</html>
