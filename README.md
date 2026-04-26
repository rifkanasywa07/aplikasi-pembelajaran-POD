<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MasterLife - Belajar Jadi Dewasa Lebih Seru</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap');
        
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: #f8fafc;
        }

        .glass-card {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(226, 232, 240, 0.8);
        }

        .gradient-text {
            background: linear-gradient(135deg, #6366f1 0%, #a855f7 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .nav-btn.active {
            color: #6366f1;
            border-bottom: 2px solid #6366f1;
        }

        .progress-bar {
            transition: width 0.5s ease-in-out;
        }

        .confetti {
            position: absolute;
            width: 10px;
            height: 10px;
            background-color: #fce38a;
            animation: fall 3s linear forwards;
        }

        @keyframes fall {
            to { transform: translateY(100vh) rotate(360deg); opacity: 0; }
        }
    </style>
</head>
<body class="text-slate-800">

    <!-- Navigation -->
    <nav class="sticky top-0 z-50 glass-card px-4 py-3 shadow-sm">
        <div class="max-w-4xl mx-auto flex justify-between items-center">
            <h1 class="text-xl font-800 gradient-text">MASTERLIFE</h1>
            <div class="flex gap-4 items-center">
                <span class="bg-indigo-100 text-indigo-700 px-3 py-1 rounded-full text-xs font-bold">
                    <i class="fas fa-fire mr-1"></i> XP: <span id="xp-count">0</span>
                </span>
            </div>
        </div>
    </nav>

    <main class="max-w-4xl mx-auto p-4 pb-24">
        
        <!-- Header Section -->
        <header class="mt-4 mb-8">
            <h2 class="text-2xl font-bold mb-2">Halo, Pembelajar! 👋</h2>
            <p class="text-slate-500">Pilih topik yang ingin kamu kuasai hari ini.</p>
        </header>

        <!-- Dynamic Content Area -->
        <div id="content-area">
            <!-- Home View -->
            <div id="home-view" class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <div onclick="showModule('finance')" class="glass-card p-6 rounded-2xl shadow-sm hover:shadow-md cursor-pointer transition-all border-l-4 border-emerald-500">
                    <div class="bg-emerald-100 w-12 h-12 rounded-xl flex items-center justify-center mb-4 text-emerald-600 text-xl">
                        <i class="fas fa-wallet"></i>
                    </div>
                    <h3 class="font-bold text-lg mb-1">Manajemen Keuangan</h3>
                    <p class="text-sm text-slate-500">Atur gaji, investasi, dan bebas hutang.</p>
                </div>

                <div onclick="showModule('comm')" class="glass-card p-6 rounded-2xl shadow-sm hover:shadow-md cursor-pointer transition-all border-l-4 border-blue-500">
                    <div class="bg-blue-100 w-12 h-12 rounded-xl flex items-center justify-center mb-4 text-blue-600 text-xl">
                        <i class="fas fa-comments"></i>
                    </div>
                    <h3 class="font-bold text-lg mb-1">Komunikasi Profesional</h3>
                    <p class="text-sm text-slate-500">Negosiasi gaji dan public speaking.</p>
                </div>

                <div onclick="showModule('mental')" class="glass-card p-6 rounded-2xl shadow-sm hover:shadow-md cursor-pointer transition-all border-l-4 border-purple-500">
                    <div class="bg-purple-100 w-12 h-12 rounded-xl flex items-center justify-center mb-4 text-purple-600 text-xl">
                        <i class="fas fa-brain"></i>
                    </div>
                    <h3 class="font-bold text-lg mb-1">Kesehatan Mental</h3>
                    <p class="text-sm text-slate-500">Manajemen stres dan work-life balance.</p>
                </div>

                <div onclick="showTool('calc')" class="glass-card p-6 rounded-2xl shadow-sm hover:shadow-md cursor-pointer transition-all border-l-4 border-orange-500">
                    <div class="bg-orange-100 w-12 h-12 rounded-xl flex items-center justify-center mb-4 text-orange-600 text-xl">
                        <i class="fas fa-calculator"></i>
                    </div>
                    <h3 class="font-bold text-lg mb-1">Kalkulator Dana Darurat</h3>
                    <p class="text-sm text-slate-500">Alat bantu hitung kesiapan finansialmu.</p>
                </div>
            </div>

            <!-- Module Detail View (Hidden by default) -->
            <div id="module-view" class="hidden">
                <button onclick="showHome()" class="mb-4 text-indigo-600 font-semibold flex items-center">
                    <i class="fas fa-arrow-left mr-2"></i> Kembali
                </button>
                <div id="module-content" class="glass-card p-8 rounded-3xl">
                    <!-- Content injected by JS -->
                </div>
            </div>

            <!-- Quiz View (Hidden by default) -->
            <div id="quiz-view" class="hidden">
                <div class="glass-card p-8 rounded-3xl text-center">
                    <div class="w-full bg-slate-100 h-2 rounded-full mb-6">
                        <div id="quiz-progress" class="progress-bar h-full bg-indigo-600 rounded-full" style="width: 0%"></div>
                    </div>
                    <h2 id="quiz-question" class="text-xl font-bold mb-6">Pertanyaan akan muncul di sini</h2>
                    <div id="quiz-options" class="grid grid-cols-1 gap-3">
                        <!-- Options injected by JS -->
                    </div>
                </div>
            </div>
        </div>

        <!-- Daily Challenge Card -->
        <div id="daily-task" class="mt-8 glass-card bg-indigo-900 p-6 rounded-3xl text-white">
            <h3 class="font-bold text-lg mb-2 flex items-center">
                <i class="fas fa-star text-yellow-400 mr-2"></i> Tantangan Hari Ini
            </h3>
            <p id="task-text" class="text-indigo-100 mb-4 text-sm">Catat setiap pengeluaranmu hari ini, sekecil apapun itu.</p>
            <button onclick="completeTask()" id="task-btn" class="bg-white text-indigo-900 px-4 py-2 rounded-full text-xs font-bold hover:bg-indigo-50 transition-colors">
                Selesaikan (+20 XP)
            </button>
        </div>

    </main>

    <!-- Bottom Navigation -->
    <div class="fixed bottom-0 left-0 right-0 glass-card border-t border-slate-200 px-8 py-4 flex justify-around">
        <button onclick="showHome()" class="flex flex-col items-center gap-1 text-indigo-600">
            <i class="fas fa-home"></i>
            <span class="text-[10px] font-bold">HOME</span>
        </button>
        <button onclick="showNotifications()" class="flex flex-col items-center gap-1 text-slate-400">
            <i class="fas fa-trophy"></i>
            <span class="text-[10px] font-bold">PRESTASI</span>
        </button>
        <button onclick="showProfile()" class="flex flex-col items-center gap-1 text-slate-400">
            <i class="fas fa-user"></i>
            <span class="text-[10px] font-bold">PROFIL</span>
        </button>
    </div>

    <!-- Feedback Message -->
    <div id="toast" class="fixed bottom-24 left-1/2 -translate-x-1/2 bg-slate-800 text-white px-6 py-3 rounded-full text-sm font-bold opacity-0 transition-opacity pointer-events-none">
        Pesan berhasil muncul!
    </div>

    <script>
        // State Management
        let xp = 0;
        let currentModule = '';
        let quizIndex = 0;
        const modules = {
            finance: {
                title: 'Aturan 50/30/20',
                body: `
                    <p class='mb-4'>Cara termudah mengatur keuangan adalah dengan membagi pendapatanmu menjadi tiga bagian utama:</p>
                    <ul class='space-y-3 mb-6'>
                        <li class='flex items-start'><i class='fas fa-check-circle text-emerald-500 mt-1 mr-2'></i> <span><b>50% Kebutuhan:</b> Sewa, makan, tagihan listrik.</span></li>
                        <li class='flex items-start'><i class='fas fa-check-circle text-emerald-500 mt-1 mr-2'></i> <span><b>30% Keinginan:</b> Hiburan, belanja hobi, makan di luar.</span></li>
                        <li class='flex items-start'><i class='fas fa-check-circle text-emerald-500 mt-1 mr-2'></i> <span><b>20% Tabungan/Hutang:</b> Dana darurat atau cicilan.</span></li>
                    </ul>
                    <button onclick="startQuiz('finance')" class="w-full bg-indigo-600 text-white py-4 rounded-2xl font-bold shadow-lg shadow-indigo-200">Mulai Kuis (+50 XP)</button>
                `
            },
            comm: {
                title: 'Teknik Komunikasi Assertive',
                body: `
                    <p class='mb-4'>Berkomunikasi secara asertif berarti menyampaikan keinginanmu tanpa menyakiti orang lain.</p>
                    <div class='bg-blue-50 p-4 rounded-xl mb-6'>
                        <p class='italic text-blue-700 text-sm'>"Saya merasa (perasaan) ketika (situasi), karena saya butuh (kebutuhan)."</p>
                    </div>
                    <button onclick="startQuiz('comm')" class="w-full bg-indigo-600 text-white py-4 rounded-2xl font-bold shadow-lg shadow-indigo-200">Uji Kemampuan (+50 XP)</button>
                `
            },
            mental: {
                title: 'The 4-7-8 Breathing',
                body: `
                    <p class='mb-4'>Gunakan teknik ini saat merasa stres di tempat kerja:</p>
                    <ol class='list-decimal list-inside space-y-2 mb-6 text-slate-600'>
                        <li>Tarik napas (hidung) selama <b>4 detik</b>.</li>
                        <li>Tahan napas selama <b>7 detik</b>.</li>
                        <li>Buang napas (mulut) selama <b>8 detik</b>.</li>
                    </ol>
                    <button onclick="showToast('Mari kita coba tarik napas sekarang...')" class="w-full border-2 border-indigo-600 text-indigo-600 py-4 rounded-2xl font-bold mb-3">Mulai Timer Latihan</button>
                    <button onclick="startQuiz('mental')" class="w-full bg-indigo-600 text-white py-4 rounded-2xl font-bold shadow-lg shadow-indigo-200">Mulai Kuis (+50 XP)</button>
                `
            }
        };

        const quizzes = {
            finance: [
                { q: "Berapa persentase ideal untuk dana darurat/tabungan?", a: ["10%", "20%", "50%"], correct: 1 },
                { q: "Membayar langganan Netflix masuk kategori?", a: ["Kebutuhan", "Keinginan", "Investasi"], correct: 1 }
            ],
            comm: [
                { q: "Apa ciri komunikasi asertif?", a: ["Menyerang orang lain", "Diam saja", "Jujur tapi sopan"], correct: 2 }
            ],
            mental: [
                { q: "Berapa lama membuang napas pada teknik 4-7-8?", a: ["4 detik", "7 detik", "8 detik"], correct: 2 }
            ]
        };

        // Navigation Functions
        function showHome() {
            document.getElementById('home-view').classList.remove('hidden');
            document.getElementById('module-view').classList.add('hidden');
            document.getElementById('quiz-view').classList.add('hidden');
            document.getElementById('daily-task').classList.remove('hidden');
        }

        function showModule(key) {
            currentModule = key;
            const content = modules[key];
            document.getElementById('module-content').innerHTML = `<h2 class="text-3xl font-800 mb-4">${content.title}</h2>` + content.body;
            document.getElementById('home-view').classList.add('hidden');
            document.getElementById('module-view').classList.remove('hidden');
            document.getElementById('daily-task').classList.add('hidden');
        }

        function showTool(type) {
            if(type === 'calc') {
                document.getElementById('module-content').innerHTML = `
                    <h2 class="text-2xl font-bold mb-4">Kalkulator Dana Darurat</h2>
                    <p class="mb-4 text-sm text-slate-500">Minimal dana darurat adalah 6x pengeluaran bulanan.</p>
                    <input type="number" id="monthly-exp" placeholder="Pengeluaran per bulan (Rp)" class="w-full p-4 border rounded-xl mb-4">
                    <button onclick="calcEmergency()" class="w-full bg-orange-500 text-white py-4 rounded-xl font-bold">Hitung Sekarang</button>
                    <div id="calc-result" class="mt-4 p-4 bg-orange-50-hidden"></div>
                `;
                document.getElementById('home-view').classList.add('hidden');
                document.getElementById('module-view').classList.remove('hidden');
            }
        }

        // Quiz Logic
        function startQuiz(key) {
            currentModule = key;
            quizIndex = 0;
            document.getElementById('module-view').classList.add('hidden');
            document.getElementById('quiz-view').classList.remove('hidden');
            loadQuestion();
        }

        function loadQuestion() {
            const data = quizzes[currentModule][quizIndex];
            document.getElementById('quiz-question').innerText = data.q;
            const optionsDiv = document.getElementById('quiz-options');
            optionsDiv.innerHTML = '';
            
            data.a.forEach((opt, idx) => {
                const btn = document.createElement('button');
                btn.className = "p-4 border-2 border-slate-100 rounded-2xl hover:border-indigo-600 hover:bg-indigo-50 transition-all font-semibold text-left";
                btn.innerText = opt;
                btn.onclick = () => checkAnswer(idx);
                optionsDiv.appendChild(btn);
            });

            const progress = ((quizIndex) / quizzes[currentModule].length) * 100;
            document.getElementById('quiz-progress').style.width = progress + '%';
        }

        function checkAnswer(idx) {
            const data = quizzes[currentModule][quizIndex];
            if(idx === data.correct) {
                showToast("Benar! 🎉");
                updateXP(25);
            } else {
                showToast("Oops, coba lagi! 💡");
            }

            quizIndex++;
            if(quizIndex < quizzes[currentModule].length) {
                setTimeout(loadQuestion, 1000);
            } else {
                setTimeout(finishQuiz, 1000);
            }
        }

        function finishQuiz() {
            createConfetti();
            document.getElementById('quiz-view').classList.add('hidden');
            document.getElementById('module-view').classList.remove('hidden');
            document.getElementById('module-content').innerHTML = `
                <div class="text-center">
                    <div class="text-6xl mb-4">🏆</div>
                    <h2 class="text-2xl font-bold mb-2">Modul Selesai!</h2>
                    <p class="text-slate-500 mb-6">Kamu telah mempelajari dasar-dasar topik ini.</p>
                    <button onclick="showHome()" class="bg-indigo-600 text-white px-8 py-3 rounded-full font-bold">Cari Topik Lain</button>
                </div>
            `;
        }

        // Utility Functions
        function updateXP(amount) {
            xp += amount;
            document.getElementById('xp-count').innerText = xp;
        }

        function showToast(msg) {
            const toast = document.getElementById('toast');
            toast.innerText = msg;
            toast.style.opacity = '1';
            setTimeout(() => { toast.style.opacity = '0'; }, 2000);
        }

        function completeTask() {
            updateXP(20);
            showToast("Tantangan selesai! Hebat! +20 XP");
            document.getElementById('task-btn').disabled = true;
            document.getElementById('task-btn').innerText = "Selesai ✅";
            document.getElementById('task-btn').className = "bg-emerald-500 text-white px-4 py-2 rounded-full text-xs font-bold";
        }

        function calcEmergency() {
            const val = document.getElementById('monthly-exp').value;
            if(!val) return;
            const result = val * 6;
            const resDiv = document.getElementById('calc-result');
            resDiv.className = "mt-4 p-4 bg-orange-50 rounded-xl text-orange-800 border border-orange-200 block";
            resDiv.innerHTML = `Target Dana Darurat kamu: <br><b class="text-xl">Rp ${result.toLocaleString('id-ID')}</b><br><small>*Minimal simpanan untuk 6 bulan ke depan.</small>`;
        }

        function createConfetti() {
            for(let i=0; i<30; i++) {
                const c = document.createElement('div');
                c.className = 'confetti';
                c.style.left = Math.random() * 100 + 'vw';
                c.style.backgroundColor = ['#fce38a', '#95e1d3', '#eaffd0', '#ff8b94'][Math.floor(Math.random()*4)];
                document.body.appendChild(c);
                setTimeout(() => c.remove(), 3000);
            }
        }

        // Initial Notification
        window.onload = () => {
            setTimeout(() => showToast("Selamat datang di MasterLife! 🚀"), 1000);
        };
    </script>
</body>
</html>
