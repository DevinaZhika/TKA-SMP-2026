<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TKA Adventure - CBT System Matematika</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts Nunito, Poppins & Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Nunito:wght@400;600;700;800;900&family=Poppins:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Chart.js CDN -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        heading: ['Poppins', 'sans-serif'],
                        game: ['Nunito', 'sans-serif'],
                    },
                    colors: {
                        brand: {
                            50: '#f0f4ff',
                            100: '#dbeafe',
                            200: '#bfdbfe',
                            300: '#93c5fd',
                            400: '#60a5fa',
                            500: '#3b82f6', 
                            600: '#2563eb', 
                            700: '#1d4ed8', 
                            800: '#1e40af',
                            950: '#172554',
                        },
                        vibrant: {
                            emerald: '#059669', 
                            amber: '#f59e0b',   
                            rose: '#e11d48',
                            cyan: '#06b6d4'
                        }
                    },
                    boxShadow: {
                        'premium': '0 10px 25px -5px rgba(30, 64, 175, 0.08), 0 8px 10px -6px rgba(30, 64, 175, 0.08)',
                        'glow': '0 0 15px rgba(59, 130, 246, 0.35)',
                        'glow-success': '0 0 15px rgba(16, 185, 129, 0.35)'
                    }
                }
            }
        }
    </script>

    <style>
        /* Modern Scrollbar styling */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f5f9;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 99px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #93c5fd;
        }

        /* Pure flat yellow highlighter for blocked text */
        .highlighted-text {
            background-color: #fef08a !important; 
            color: #1e293b !important;
            padding: 2px 4px !important;
            border-radius: 4px !important;
            font-weight: 600;
            box-shadow: 0 1px 3px rgba(234, 179, 8, 0.3) !important;
        }

        /* Allow text selection specifically for reading areas */
        .allow-select {
            user-select: text !important;
            -webkit-user-select: text !important;
        }

        /* Active Option Box Single Choice */
        .option-card input[type="radio"]:checked + label {
            border-color: #10b981 !important; 
            background-color: #ecfdf5 !important; 
            color: #065f46 !important; 
            box-shadow: 0 4px 15px -1px rgba(16, 185, 129, 0.25) !important;
            transform: scale(1.01);
            transition: all 0.2s ease;
        }
        .option-card input[type="radio"]:checked + label span:first-child {
            background-color: #10b981 !important;
            color: #ffffff !important;
            border-color: #10b981 !important;
        }

        /* Active Option Box Multiple Answer Checkbox */
        .option-card input[type="checkbox"]:checked + label {
            border-color: #3b82f6 !important; 
            background-color: #eff6ff !important; 
            color: #1e40af !important; 
            box-shadow: 0 4px 15px -1px rgba(59, 130, 246, 0.25) !important;
            transform: scale(1.01);
            transition: all 0.2s ease;
        }
        .option-card input[type="checkbox"]:checked + label span:first-child {
            background-color: #3b82f6 !important;
            color: #ffffff !important;
            border-color: #3b82f6 !important;
        }

        /* Reading Ruler Focus Overlay */
        .ruler-focus-active .reading-stimulus p:not(.focused-line) {
            opacity: 0.25;
            filter: blur(0.5px);
            transition: all 0.25s ease;
        }
        .reading-stimulus p {
            transition: all 0.2s ease;
            cursor: pointer;
            border-left: 3px solid transparent;
            padding-left: 8px;
        }
        .reading-stimulus p:hover {
            background-color: #f8fafc;
            border-left-color: #bfdbfe;
        }
        .focused-line {
            border-left-color: #3b82f6 !important;
            background-color: #eff6ff !important;
            font-weight: 500;
            color: #1e3a8a !important;
            opacity: 1 !important;
            filter: none !important;
        }

        /* Gamified Layout Animations */
        .game-btn {
            transition: transform 0.15s cubic-bezier(0.175, 0.885, 0.32, 1.275), background-color 0.2s;
        }
        .game-btn:hover {
            transform: scale(1.02);
        }
        .game-btn:active {
            transform: scale(0.98);
        }

        /* Background Animated Clouds */
        @keyframes moveClouds {
            0% { transform: translateX(-10%); }
            50% { transform: translateX(10%); }
            100% { transform: translateX(-10%); }
        }
        .animated-clouds {
            animation: moveClouds 35s ease-in-out infinite;
        }

        /* Slide Transition */
        .slide-fade-in {
            animation: slideFade 0.4s cubic-bezier(0.16, 1, 0.3, 1) forwards;
        }
        @keyframes slideFade {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 font-sans min-h-screen flex flex-col justify-between overflow-x-hidden select-none">

    <div class="fixed inset-0 -z-50 overflow-hidden pointer-events-none">
        <div class="absolute inset-0 bg-gradient-to-b from-sky-300 via-blue-100 to-indigo-50"></div>
        <div class="absolute top-12 right-12 w-48 h-48 rounded-full bg-yellow-200 opacity-20 blur-3xl animate-pulse"></div>
        <div class="absolute inset-0 animated-clouds opacity-40">
            <svg class="absolute top-16 left-[5%] w-32 h-12 fill-white opacity-85" viewBox="0 0 100 40"><path d="M10 30 Q15 15 30 20 Q45 10 60 25 Q75 15 90 30 Z"/></svg>
            <svg class="absolute top-36 left-[55%] w-48 h-16 fill-white opacity-90" viewBox="0 0 100 40"><path d="M10 30 Q15 15 30 20 Q45 10 60 25 Q75 15 90 30 Z"/></svg>
        </div>
        <svg class="absolute bottom-0 left-0 w-full h-[35vh] fill-emerald-100/30 opacity-70" viewBox="0 0 1440 320" preserveAspectRatio="none">
            <path d="M0,224L120,202.7C240,181,480,139,720,144C960,149,1200,203,1320,229.3L1440,256L1440,320L0,320Z"></path>
        </svg>
        <div class="absolute top-1/4 left-10 w-12 h-12 opacity-15 text-brand-800 rotate-12 animate-bounce"><i class="fa-solid fa-square-root-variable text-5xl"></i></div>
        <div class="absolute top-1/3 right-16 w-12 h-12 opacity-15 text-brand-800 -rotate-12 animate-bounce"><i class="fa-solid fa-calculator text-5xl"></i></div>
    </div>

    <header class="bg-gradient-to-r from-brand-950 via-blue-950 to-slate-900 border-b border-brand-800 sticky top-0 z-40 shadow-md">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center gap-3">
                <div class="bg-gradient-to-tr from-brand-500 to-cyan-400 text-white p-2.5 rounded-xl flex items-center justify-center shadow-lg shadow-brand-500/20">
                    <i class="fa-solid fa-calculator text-lg"></i>
                </div>
                <div>
                    <h1 class="font-heading font-extrabold text-sm sm:text-base text-white tracking-wide">TKA ADVENTURE - MATEMATIKA</h1>
                </div>
            </div>
            
            <div class="flex items-center gap-2">
                <button onclick="toggleAudio()" id="btn-sound-toggle" class="px-3 py-1.5 text-xs font-semibold rounded-lg text-brand-200 hover:text-white hover:bg-white/10 flex items-center gap-1.5 transition mr-2">
                    <i id="sound-icon" class="fa-solid fa-volume-high"></i> <span id="sound-text">Sound ON</span>
                </button>

                <button onclick="switchView('student-gate')" id="tab-student" class="px-3 py-1.5 text-xs sm:text-sm font-semibold rounded-lg transition-all duration-200 bg-brand-600 text-white shadow-md flex items-center gap-1.5">
                    <i class="fa-solid fa-user-pen"></i> <span>Siswa</span>
                </button>
                <button onclick="openTeacherLogin()" id="tab-teacher" class="px-3 py-1.5 text-xs sm:text-sm font-semibold rounded-lg transition-all duration-200 text-brand-200 hover:text-white hover:bg-white/10 flex items-center gap-1.5">
                    <i class="fa-solid fa-user-tie"></i> <span>Portal Guru</span>
                </button>
            </div>
        </div>
    </header>

    <main class="flex-grow max-w-7xl w-full mx-auto p-4 sm:p-6 lg:p-8 relative">

        <div id="view-student-gate" class="max-w-md mx-auto my-6 bg-white/80 backdrop-blur-md rounded-3xl border border-blue-100 p-6 sm:p-8 shadow-premium slide-fade-in relative overflow-hidden">
            <div class="text-center mb-6">
                <div class="inline-flex mb-3">
                    <div class="w-20 h-20 bg-gradient-to-tr from-brand-600 to-cyan-500 text-white rounded-3xl flex items-center justify-center shadow-lg shadow-brand-500/30 text-3xl font-black">
                        ∑
                    </div>
                </div>
                <h2 class="font-heading font-extrabold text-2xl text-brand-950 font-game">🏆 TKA Adventure MTK</h2>
                <p class="text-slate-500 text-xs mt-1 leading-relaxed">System Ujian CBT TKA Matematika Interaktif</p>
            </div>

            <!-- HALAMAN KETENTUAN TIMER DENGAN PERSYARATAN KHUSUS -->
            <div class="p-4 bg-blue-50/90 border border-blue-200 rounded-2xl text-xs text-brand-900 mb-5 space-y-2 shadow-sm">
                <div class="font-bold flex items-center gap-2 text-brand-800 text-sm">
                    <i class="fa-solid fa-clock text-brand-600 text-base"></i> KETENTUAN TIMER & FITUR LOCK:
                </div>
                <ul class="list-disc list-inside text-[11px] text-slate-700 space-y-1.5 leading-relaxed font-medium">
                    <li><strong>TOTAL WAKTU UJIAN <span id="gate-total-time-display">75</span> MENIT</strong></li>
                    <li><strong>TIMER PER SOAL BERJALAN MUNDUR. JIKA HABIS, JAWABAN SOAL TERSEBUT TERLOCK</strong></li>
                    <li><strong>SOAL TERDIRI DARI PILIHAN GANDA, PILIHAN GANDA KOMPLEKS, BENAR/SALAH</strong></li>
                </ul>
            </div>

            <form id="form-login-siswa" onsubmit="startExam(event)" class="space-y-4">
                <div>
                    <label class="block text-xs font-bold uppercase text-slate-400 mb-1 tracking-wider" for="input-nama">Nama Lengkap</label>
                    <div class="relative">
                        <span class="absolute inset-y-0 left-0 flex items-center pl-3.5 text-slate-400">
                            <i class="fa-solid fa-user text-sm"></i>
                        </span>
                        <input type="text" id="input-nama" required class="w-full pl-10 pr-4 py-2.5 border border-slate-200 rounded-xl focus:ring-2 focus:ring-brand-500 text-sm font-medium bg-white/90" placeholder="Contoh: Andi Wijaya">
                    </div>
                </div>
                
                <div class="grid grid-cols-2 gap-4">
                    <div>
                        <label class="block text-xs font-bold uppercase text-slate-400 mb-1 tracking-wider" for="input-kelas">Kelas</label>
                        <select id="input-kelas" required class="w-full px-3.5 py-2.5 border border-slate-200 rounded-xl focus:ring-2 focus:ring-brand-500 text-sm font-medium bg-white transition">
                            <option value="">Pilih...</option>
                            <option value="9A">Kelas 9A</option>
                            <option value="9B">Kelas 9B</option>
                            <option value="9C">Kelas 9C</option>
                            <option value="9D">Kelas 9D</option>
                            <option value="9E">Kelas 9E</option>
                            <option value="9F">Kelas 9F</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-xs font-bold uppercase text-slate-400 mb-1 tracking-wider" for="input-absen">Nomor Absen</label>
                        <div class="relative">
                            <span class="absolute inset-y-0 left-0 flex items-center pl-3.5 text-slate-400">
                                <i class="fa-solid fa-hashtag text-sm"></i>
                            </span>
                            <input type="number" id="input-absen" min="1" max="50" required class="w-full pl-10 pr-4 py-2.5 border border-slate-200 rounded-xl focus:ring-2 focus:ring-brand-500 text-sm font-medium bg-white/90" placeholder="1">
                        </div>
                    </div>
                </div>

                <button type="submit" class="game-btn w-full py-3.5 px-4 bg-gradient-to-r from-brand-600 to-indigo-600 hover:from-brand-700 hover:to-indigo-700 text-white font-bold rounded-xl shadow-lg shadow-brand-600/20 flex items-center justify-center gap-2 text-sm mt-2">
                    🚀 Mulai Petualangan Ujian
                </button>
            </form>
        </div>

        <div id="view-student-exam" class="hidden flex flex-col gap-4 slide-fade-in">
            
            <!-- Top Panel: Student Info, Timers & Progress Bar -->
            <div class="bg-white border border-slate-200 rounded-2xl p-4 shadow-sm flex flex-col gap-4">
                
                <div class="flex flex-col md:flex-row gap-4 items-center justify-between">
                    <div class="flex items-center gap-3 w-full md:w-auto">
                        <div class="bg-brand-50 border border-brand-100 px-3.5 py-2 rounded-xl text-xs w-full md:w-auto">
                            <span class="text-brand-400 block font-bold uppercase text-[9px] tracking-wider">Peserta Ujian</span>
                            <strong id="display-student-name" class="text-brand-950 text-sm">Siswa</strong>
                            <span class="text-brand-600 ml-1 font-semibold">(Kelas <span id="display-student-class">9A</span> / Absen <span id="display-student-absen">01</span>)</span>
                        </div>

                        <div class="bg-indigo-950 text-white px-3 py-2 rounded-xl text-xs flex items-center gap-1.5 font-bold shadow-sm">
                            <span id="display-badge-icon">⭐</span> <span id="display-badge-text">Explorer</span>
                        </div>
                    </div>

                    <!-- PROGRESS BAR -->
                    <div class="flex flex-col w-full md:w-64">
                        <div class="flex justify-between items-center text-[10px] font-bold text-slate-400 uppercase mb-1">
                            <span id="label-quest-progress">Progress Misi</span>
                            <span id="percent-quest-progress" class="text-brand-600 font-extrabold">0%</span>
                        </div>
                        <div class="w-full bg-slate-100 rounded-full h-2.5 border overflow-hidden">
                            <div id="quest-progress-bar" class="bg-gradient-to-r from-brand-500 to-emerald-500 h-full w-0 transition-all duration-500"></div>
                        </div>
                    </div>

                    <!-- DUAL TIMERS DISPLAY -->
                    <div class="flex items-center gap-3 w-full md:w-auto justify-end">
                        <!-- Per-Question Timer -->
                        <div id="question-timer-card" class="bg-amber-50 border border-amber-200 px-3 py-1.5 rounded-xl text-right transition-colors">
                            <span class="text-[9px] text-amber-700 block font-bold uppercase tracking-wider" id="question-timer-label"><i class="fa-solid fa-hourglass-half text-amber-500"></i> Timer Soal Ini</span>
                            <div id="question-timer" class="text-sm font-mono font-black text-amber-800">02:00</div>
                        </div>

                        <!-- Total Exam Timer -->
                        <div class="bg-rose-50 border border-rose-200 px-3 py-1.5 rounded-xl text-right">
                            <span class="text-[9px] text-rose-700 block font-bold uppercase tracking-wider"><i class="fa-solid fa-clock text-rose-500"></i> Total Sisa Waktu</span>
                            <div id="exam-timer" class="text-sm font-mono font-black text-vibrant-rose animate-pulse">01:15:00</div>
                        </div>
                    </div>
                </div>

                <!-- ASSISTIVE READ TOOLBAR -->
                <div class="flex flex-wrap items-center gap-2 bg-slate-50 p-2 rounded-xl border border-slate-200 text-xs">
                    <span class="text-[10px] font-bold text-slate-400 px-2 uppercase tracking-wide">Alat Bantu Pengerjaan:</span>
                    <button onclick="toggleHighlighter()" id="btn-highlighter" class="px-3 py-1.5 text-xs font-semibold rounded-lg bg-white border text-slate-700 hover:bg-brand-50 flex items-center gap-1.5 transition">
                        <i class="fa-solid fa-marker text-amber-500"></i> <span id="label-highlighter-status">Stabilo Teks (Off)</span>
                    </button>
                    <button onclick="clearHighlights()" id="btn-clear-highlights" class="px-2.5 py-1.5 text-xs font-semibold rounded-lg bg-white border text-slate-600 hover:bg-slate-100 flex items-center gap-1 transition">
                        <i class="fa-solid fa-eraser text-slate-400"></i> Hapus Stabilo
                    </button>
                    <button onclick="toggleReadingRuler()" id="btn-ruler" class="px-3 py-1.5 text-xs font-semibold rounded-lg bg-white border text-slate-700 hover:bg-brand-50 flex items-center gap-1.5 transition">
                        <i class="fa-solid fa-grip-lines text-brand-500"></i> Mistar Fokus
                    </button>
                    <button onclick="toggleScratchpad()" class="px-3 py-1.5 text-xs font-semibold rounded-lg bg-white border text-slate-700 hover:bg-brand-50 flex items-center gap-1.5 transition">
                        <i class="fa-solid fa-feather-pointed text-brand-500"></i> Papan Coretan Hitungan
                    </button>
                </div>
            </div>

            <!-- Workspace: Split Screen Layout -->
            <div class="grid grid-cols-1 lg:grid-cols-12 gap-4">
                
                <!-- STIMULUS PANEL (Left Side) -->
                <div id="panel-stimulus" class="lg:col-span-6 bg-white border border-slate-200 rounded-2xl p-5 shadow-sm flex flex-col justify-between max-h-[550px] overflow-y-auto">
                    <div>
                        <div class="flex items-center justify-between border-b border-slate-100 pb-3 mb-4">
                            <span class="text-xs font-bold text-brand-600 uppercase tracking-wider"><i class="fa-solid fa-file-invoice"></i> Stimulus / Konteks Soal</span>
                            <span id="display-difficulty-badge" class="text-[10px] bg-brand-50 text-brand-700 px-2.5 py-1 rounded-full font-bold">Sedang</span>
                        </div>
                        <div id="display-stimulus-container" class="reading-stimulus text-slate-700 text-sm sm:text-base space-y-3 leading-relaxed allow-select">
                            <!-- Rendered dynamically -->
                        </div>
                    </div>
                </div>

                <!-- QUESTION & OPTIONS PANEL (Right Side) -->
                <div id="panel-soal" class="lg:col-span-6 bg-white border border-slate-200 rounded-2xl p-5 shadow-sm flex flex-col justify-between min-h-[450px] relative">
                    
                    <!-- Locked Question Overlay Banner -->
                    <div id="locked-question-banner" class="hidden mb-4 p-3 bg-red-100 border border-red-300 rounded-xl flex items-center gap-2.5 text-red-700 text-xs font-bold shadow-sm">
                        <i class="fa-solid fa-lock text-red-600 text-lg animate-bounce"></i>
                        <div>
                            <span>SOAL DILOCK / TERKUNCI!</span>
                            <p class="text-[11px] font-normal text-red-600">Waktu khusus pengerjaan soal ini telah habis. Jawaban tidak dapat diubah lagi.</p>
                        </div>
                    </div>

                    <div>
                        <div class="flex items-center justify-between border-b border-slate-100 pb-3 mb-4">
                            <div class="flex items-center gap-2">
                                <span class="px-3 py-1 bg-brand-50 text-brand-700 text-xs font-bold rounded-lg" id="display-mapel">
                                    TKA Matematika
                                </span>
                                <span id="display-question-type-badge" class="px-2.5 py-1 bg-indigo-50 text-indigo-700 text-[10px] font-extrabold rounded-lg uppercase tracking-wider">
                                    Pilihan Ganda
                                </span>
                            </div>
                            <span class="text-xs font-semibold text-slate-500">
                                Soal No <strong id="current-question-num" class="text-brand-600">1</strong> dari <span id="total-questions-num">25</span>
                            </span>
                        </div>

                        <div class="space-y-4">
                            <h3 class="text-xs uppercase font-extrabold text-slate-400 tracking-wider" id="label-quest-title">Level 1 Challenge</h3>
                            <p id="display-soal-text" class="text-brand-950 font-bold text-sm sm:text-base leading-relaxed allow-select">
                                Memuat butir pertanyaan...
                            </p>

                            <!-- Options Container (Dynamic: Single Choice, Checkbox MCMA, or Benar/Salah Table) -->
                            <div id="display-opsi-container" class="grid grid-cols-1 gap-2.5">
                                <!-- Rendered dynamically -->
                            </div>
                        </div>
                    </div>

                    <!-- Action Buttons -->
                    <div class="mt-6 pt-4 border-t border-slate-100 flex items-center justify-between gap-2">
                        <button id="btn-prev-question" onclick="goToQuestion(currentQuestionIndex - 1)" class="game-btn px-3 sm:px-4 py-2.5 text-xs font-bold text-slate-600 bg-slate-100 hover:bg-slate-200 rounded-xl flex items-center gap-1.5 transition">
                            <i class="fa-solid fa-chevron-left"></i> Sebelumnya
                        </button>
                        
                        <button id="btn-doubtful-toggle" onclick="toggleDoubtful()" class="game-btn px-3.5 py-2.5 text-xs font-bold rounded-xl flex items-center justify-center gap-1.5 transition border border-amber-300 bg-amber-50 text-amber-700 hover:bg-amber-100">
                            <i class="fa-regular fa-square" id="icon-doubtful"></i> Ragu-Ragu
                        </button>

                        <button id="btn-next-question" onclick="goToQuestion(currentQuestionIndex + 1)" class="game-btn px-3 sm:px-4 py-2.5 text-xs font-bold text-white bg-brand-600 hover:bg-brand-700 rounded-xl flex items-center gap-1.5 transition shadow">
                            Selanjutnya <i class="fa-solid fa-chevron-right"></i>
                        </button>

                        <button id="btn-finish-exam" onclick="confirmEndExam()" class="game-btn hidden px-5 sm:px-6 py-2.5 text-xs font-bold text-white bg-vibrant-emerald hover:bg-emerald-600 rounded-xl flex items-center gap-1.5 transition shadow-md">
                            <i class="fa-solid fa-paper-plane"></i> Selesai & Kirim
                        </button>
                    </div>
                </div>

            </div>

            <!-- Question Grid Nav -->
            <div class="bg-white border border-slate-200 rounded-2xl p-4 shadow-sm">
                <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-2 mb-3">
                    <h4 class="font-heading font-bold text-xs text-brand-950 uppercase tracking-widest">Peta Level Soal (25 Soal)</h4>
                    <div class="flex flex-wrap items-center gap-3 text-[10px] font-bold uppercase tracking-wider">
                        <div class="flex items-center gap-1.5"><span class="w-3 h-3 rounded-full bg-slate-200 border border-slate-300 inline-block"></span> Belum Dijawab</div>
                        <div class="flex items-center gap-1.5"><span class="w-3 h-3 rounded-full bg-emerald-600 inline-block"></span> Sudah Dijawab</div>
                        <div class="flex items-center gap-1.5"><span class="w-3 h-3 rounded-full bg-amber-500 inline-block"></span> Ragu-Ragu</div>
                        <div class="flex items-center gap-1.5"><span class="w-3.5 h-3.5 rounded-md bg-red-600 flex items-center justify-center text-white text-[8px] inline-flex"><i class="fa-solid fa-lock"></i></span> Terkunci</div>
                    </div>
                </div>
                <div id="student-grid-indicators" class="flex flex-wrap gap-2.5">
                    <!-- Dynamic generated circles / locked buttons -->
                </div>
            </div>

        </div>

        <!-- SCRATCHPAD DIGITAL PANEL -->
        <div id="scratchpad-panel" class="hidden fixed right-4 bottom-4 z-50 bg-white border border-brand-200 w-80 rounded-2xl shadow-2xl p-4 space-y-3 slide-fade-in">
            <div class="flex items-center justify-between border-b pb-2">
                <span class="text-xs font-bold text-brand-950 uppercase"><i class="fa-solid fa-feather-pointed text-brand-500"></i> Coretan Rumus & Hitungan</span>
                <button onclick="toggleScratchpad()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
            </div>
            <div>
                <textarea id="scratchpad-text" rows="7" class="w-full text-xs p-3 border border-slate-200 rounded-xl focus:ring-2 focus:ring-brand-500 focus:outline-none font-mono" placeholder="Gunakan area ini untuk menghitung cakar-cakar angka..."></textarea>
            </div>
        </div>

        <div id="view-student-results" class="hidden max-w-lg mx-auto bg-white border border-brand-50 rounded-3xl p-6 sm:p-8 shadow-premium slide-fade-in">
            <div class="text-center mb-6">
                <div class="inline-flex p-4 bg-emerald-50 text-vibrant-emerald rounded-full mb-3 shadow-inner">
                    <i class="fa-solid fa-circle-check text-4xl"></i>
                </div>
                <h2 class="font-heading font-extrabold text-2xl text-brand-950">🎉 Ujian TKA Selesai!</h2>
                <p class="text-slate-500 text-xs mt-1">Hasil pengerjaan Anda telah tersimpan secara aman ke database server.</p>
            </div>

            <div class="bg-slate-50 rounded-2xl p-4 border border-slate-100 mb-5 space-y-2 text-xs">
                <div class="flex justify-between">
                    <span class="text-slate-500">Nama Peserta</span>
                    <strong id="res-student-name" class="text-brand-950">Andi</strong>
                </div>
                <div class="flex justify-between">
                    <span class="text-slate-500">Kelas / Absen</span>
                    <strong id="res-student-class" class="text-brand-950">9A / 12</strong>
                </div>
            </div>

            <div class="bg-brand-50 border border-brand-100 rounded-2xl p-5 text-center space-y-4 shadow-inner mb-6">
                <p class="text-brand-800 text-xs uppercase tracking-widest font-extrabold">Hasil Akhir Nilai Ujian</p>
                <div class="grid grid-cols-2 gap-4 border-b border-brand-100 pb-4">
                    <div>
                        <span class="text-[11px] text-brand-500 font-semibold uppercase">Benar</span>
                        <div id="res-total-correct" class="text-2xl font-black text-emerald-600">0</div>
                    </div>
                    <div>
                        <span class="text-[11px] text-brand-500 font-semibold uppercase">Salah</span>
                        <div id="res-total-incorrect" class="text-2xl font-black text-vibrant-rose">0</div>
                    </div>
                </div>

                <div>
                    <span class="text-[11px] text-brand-500 font-semibold uppercase block mb-1">Skor Akhir (Skala 100)</span>
                    <div id="res-final-score" class="text-6xl font-black text-brand-600 tracking-tight">00.00</div>
                </div>
            </div>

            <div class="p-3 bg-slate-50 border border-slate-200 rounded-xl text-xs text-slate-500 text-center flex items-center justify-center gap-1.5">
                <i class="fa-solid fa-lock text-slate-400"></i> Kunci jawaban dan pembahasan dikunci oleh sistem.
            </div>
        </div>

        <div id="view-teacher-login" class="hidden max-w-sm mx-auto my-12 bg-white border border-slate-200 rounded-3xl p-6 shadow-premium slide-fade-in">
            <div class="text-center mb-6">
                <div class="inline-flex p-3 bg-brand-50 text-brand-600 rounded-2xl mb-2">
                    <i class="fa-solid fa-user-shield text-2xl"></i>
                </div>
                <h3 class="font-heading font-bold text-lg text-brand-950">Portal Keamanan Guru</h3>
                <p class="text-slate-500 text-xs">Masukkan kata sandi guru untuk mengakses dashboard.</p>
            </div>
            
            <form onsubmit="verifyTeacherLogin(event)" class="space-y-4">
                <div>
                    <input type="password" id="input-teacher-pwd" class="w-full px-4 py-2.5 border border-slate-200 rounded-xl focus:ring-2 focus:ring-brand-500 text-sm text-center font-mono" placeholder="Password Guru" required>
                </div>
                <p id="error-pwd-msg" class="text-vibrant-rose text-xs text-center font-semibold hidden"><i class="fa-solid fa-circle-exclamation"></i> Password salah! (Default: adminTKA2026)</p>
                <button type="submit" class="game-btn w-full py-2.5 bg-brand-950 hover:bg-slate-900 text-white font-semibold rounded-xl text-sm transition-all">
                    Masuk ke Dashboard
                </button>
            </form>
        </div>

        <div id="view-teacher-dashboard" class="hidden space-y-6 slide-fade-in">
            
            <!-- Dashboard Menu Header -->
            <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between border-b border-slate-200 pb-4 gap-4">
                <div>
                    <h2 class="font-heading font-extrabold text-xl text-brand-950">Dashboard Analisis & Portal Guru</h2>
                    <p class="text-slate-500 text-xs">Kelola soal, pengatur waktu keseluruhan & per-soal, serta rekap hasil analisis peserta.</p>
                </div>
                <div class="flex flex-wrap items-center gap-2">
                    <button onclick="switchTeacherTab('tab-peserta')" id="btn-tab-peserta" class="px-3 py-1.5 text-xs font-semibold rounded-lg bg-brand-600 text-white shadow-sm">Daftar Peserta</button>
                    <button onclick="switchTeacherTab('tab-butir')" id="btn-tab-butir" class="px-3 py-1.5 text-xs font-semibold rounded-lg text-slate-600 hover:bg-slate-100 transition">Rekap Soal</button>
                    <button onclick="switchTeacherTab('tab-analisis')" id="btn-tab-analisis" class="px-3 py-1.5 text-xs font-semibold rounded-lg text-slate-600 hover:bg-slate-100 transition">Analisis Soal</button>
                    <button onclick="switchTeacherTab('tab-matriks')" id="btn-tab-matriks" class="px-3 py-1.5 text-xs font-semibold rounded-lg text-slate-600 hover:bg-slate-100 transition">Matriks Jawaban</button>
                    <button onclick="switchTeacherTab('tab-soal-editor')" id="btn-tab-soal" class="px-3 py-1.5 text-xs font-semibold rounded-lg text-brand-600 hover:bg-brand-50 transition"><i class="fa-solid fa-clock-rotate-left mr-1"></i> Atur Soal & Waktu</button>
                    <button onclick="clearAllData()" class="px-2.5 py-1.5 text-xs font-bold text-vibrant-rose hover:bg-rose-50 rounded-lg ml-auto sm:ml-0 transition"><i class="fa-solid fa-trash-can"></i> Reset Data</button>
                </div>
            </div>

            <!-- TEACHER TAB: DAFTAR PESERTA -->
            <div id="subview-tab-peserta" class="space-y-4">
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                    <div class="bg-white border border-slate-200 p-4 rounded-2xl shadow-sm flex items-center justify-between">
                        <div>
                            <span class="text-[10px] text-slate-400 font-bold uppercase tracking-wider">Total Peserta</span>
                            <div id="dash-stat-total" class="text-2xl font-extrabold text-brand-950">0</div>
                        </div>
                        <div class="p-2.5 bg-brand-50 text-brand-600 rounded-xl text-lg"><i class="fa-solid fa-users"></i></div>
                    </div>
                    <div class="bg-white border border-slate-200 p-4 rounded-2xl shadow-sm flex items-center justify-between">
                        <div>
                            <span class="text-[10px] text-slate-400 font-bold uppercase tracking-wider">Rata-Rata Skor</span>
                            <div id="dash-stat-avg" class="text-2xl font-extrabold text-brand-950">0.0</div>
                        </div>
                        <div class="p-2.5 bg-blue-50 text-brand-600 rounded-xl text-lg"><i class="fa-solid fa-chart-simple"></i></div>
                    </div>
                    <div class="bg-white border border-slate-200 p-4 rounded-2xl shadow-sm flex items-center justify-between">
                        <div>
                            <span class="text-[10px] text-slate-400 font-bold uppercase tracking-wider">Skor Tertinggi</span>
                            <div id="dash-stat-max" class="text-2xl font-extrabold text-vibrant-emerald">0</div>
                        </div>
                        <div class="p-2.5 bg-emerald-50 text-vibrant-emerald rounded-xl text-lg"><i class="fa-solid fa-trophy"></i></div>
                    </div>
                </div>

                <div class="bg-white border border-slate-200 rounded-2xl overflow-hidden shadow-sm">
                    <div class="px-5 py-4 border-b border-slate-100 flex items-center justify-between">
                        <h3 class="font-heading font-bold text-brand-950 text-sm">Daftar Hasil Pengerjaan Peserta</h3>
                        <div class="flex items-center gap-2">
                            <label class="text-[10px] font-bold text-slate-400 uppercase tracking-wide">Urutkan:</label>
                            <select id="sort-filter-peserta" onchange="renderTeacherPesertaTable()" class="px-2.5 py-1.5 text-xs border rounded-lg bg-slate-50 focus:outline-none">
                                <option value="skor-desc">Skor Tertinggi</option>
                                <option value="skor-asc">Skor Terendah</option>
                                <option value="absen">No. Absen</option>
                                <option value="nama">Nama (A-Z)</option>
                            </select>
                        </div>
                    </div>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left border-collapse text-xs sm:text-sm">
                            <thead>
                                <tr class="bg-slate-50 border-b border-slate-100 text-slate-500 text-[10px] font-bold uppercase tracking-wider">
                                    <th class="px-6 py-3">Nama</th>
                                    <th class="px-6 py-3">Kelas</th>
                                    <th class="px-6 py-3 text-center">Absen</th>
                                    <th class="px-6 py-3">Mulai</th>
                                    <th class="px-6 py-3">Selesai</th>
                                    <th class="px-6 py-3 text-center">Benar</th>
                                    <th class="px-6 py-3 text-center">Salah</th>
                                    <th class="px-6 py-3 text-center">Skor</th>
                                </tr>
                            </thead>
                            <tbody id="tbody-peserta-rows" class="divide-y divide-slate-100">
                                <!-- Dynamic rows -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- TEACHER TAB: REKAP BUTIR SOAL -->
            <div id="subview-tab-butir" class="hidden space-y-4">
                <div id="rekap-cards-container" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
                    <!-- Dynamic cards -->
                </div>
            </div>

            <!-- TEACHER TAB: ANALISIS SOAL -->
            <div id="subview-tab-analisis" class="hidden space-y-6">
                <div class="bg-white border border-slate-200 rounded-2xl p-5 shadow-sm">
                    <h3 class="font-heading font-bold text-brand-950 text-sm mb-3">Grafik Distribusi Jawaban Benar & Salah Per Soal</h3>
                    <div class="h-64 w-full relative">
                        <canvas id="analisisChart"></canvas>
                    </div>
                </div>

                <div class="bg-white border border-slate-200 rounded-2xl overflow-hidden shadow-sm">
                    <div class="px-5 py-4 border-b border-slate-100">
                        <h3 class="font-heading font-bold text-brand-950 text-sm">Urutan Kesulitan Soal (Diurutkan dari Paling Sulit)</h3>
                    </div>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left border-collapse text-xs sm:text-sm">
                            <thead>
                                <tr class="bg-slate-50 border-b border-slate-100 text-slate-500 text-[10px] font-bold uppercase tracking-wider">
                                    <th class="px-6 py-3">No Soal</th>
                                    <th class="px-6 py-3">Tingkat Kesulitan</th>
                                    <th class="px-6 py-3 text-center">Waktu Alokasi</th>
                                    <th class="px-6 py-3 text-center">Jumlah Benar</th>
                                    <th class="px-6 py-3 text-center">Jumlah Salah</th>
                                    <th class="px-6 py-3 text-center">% Benar</th>
                                    <th class="px-6 py-3 text-center">% Salah</th>
                                </tr>
                            </thead>
                            <tbody id="tbody-analisis-rows" class="divide-y divide-slate-100">
                                <!-- Dynamic rows -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- TEACHER TAB: MATRIKS JAWABAN -->
            <div id="subview-tab-matriks" class="hidden space-y-4">
                <div class="bg-white border border-slate-200 rounded-2xl overflow-hidden shadow-sm">
                    <div class="px-5 py-4 border-b border-slate-100">
                        <h3 class="font-heading font-bold text-brand-950 text-sm">Matriks Jawaban Seluruh Siswa</h3>
                    </div>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left border-collapse text-xs">
                            <thead id="thead-matriks">
                                <!-- Dynamic header -->
                            </thead>
                            <tbody id="tbody-matriks-rows" class="divide-y divide-slate-100">
                                <!-- Dynamic rows -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- TEACHER TAB: SOAL & TIMER EDITOR -->
            <div id="subview-tab-soal-editor" class="hidden space-y-6">
                
                <!-- TOTAL DURATION SETTINGS CARD (PENGATURAN WAKTU KESELURUHAN) -->
                <div class="bg-gradient-to-r from-brand-900 via-indigo-900 to-slate-900 text-white p-5 rounded-2xl shadow-md border border-brand-800 space-y-4">
                    <div class="flex flex-col md:flex-row items-start md:items-center justify-between gap-4">
                        <div class="flex items-center gap-3">
                            <div class="p-3 bg-amber-400/20 border border-amber-300/30 rounded-2xl text-yellow-300 text-2xl">
                                <i class="fa-solid fa-clock-rotate-left"></i>
                            </div>
                            <div>
                                <h4 class="font-bold text-base text-white">Pengaturan Waktu Ujian Keseluruhan (Total Timer)</h4>
                                <p class="text-xs text-brand-200">Guru dapat menentukan sendiri total durasi waktu ujian untuk seluruh siswa.</p>
                            </div>
                        </div>
                        <div class="bg-white/10 p-3 rounded-xl border border-white/10 text-right">
                            <span class="text-[10px] text-brand-200 font-bold uppercase tracking-wider block">Kalkulasi Otomatis Soal</span>
                            <div id="total-calculated-time-sum" class="text-sm font-black text-amber-300">75 Menit (4500 dtk)</div>
                        </div>
                    </div>

                    <div class="bg-white/5 border border-white/10 p-4 rounded-xl flex flex-col sm:flex-row items-stretch sm:items-center justify-between gap-4">
                        <div class="flex items-center gap-3">
                            <label for="input-total-exam-mins" class="text-xs font-bold uppercase text-brand-200">Set Total Waktu Ujian (Menit):</label>
                            <input type="number" id="input-total-exam-mins" min="5" max="300" value="75" class="w-24 px-3 py-1.5 rounded-lg bg-white text-slate-900 font-extrabold text-sm focus:ring-2 focus:ring-amber-400 focus:outline-none">
                            <span class="text-xs font-semibold text-slate-300">Menit</span>
                        </div>
                        <div class="flex items-center gap-2">
                            <button onclick="saveTotalExamTime()" class="game-btn px-4 py-2 bg-gradient-to-r from-amber-500 to-amber-600 hover:from-amber-600 hover:to-amber-700 text-slate-950 font-bold rounded-xl text-xs flex items-center gap-1.5 shadow-md">
                                <i class="fa-solid fa-floppy-disk"></i> Simpan Total Waktu Ujian
                            </button>
                            <button onclick="useAutoCalculatedTime()" class="game-btn px-3 py-2 bg-white/10 hover:bg-white/20 text-white font-bold rounded-xl text-xs transition">
                                Pakai Sum Soal
                            </button>
                        </div>
                    </div>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
                    <!-- Form Editor Soal & Timer Per Soal -->
                    <div class="lg:col-span-4 bg-white border border-slate-200 p-5 rounded-2xl shadow-sm space-y-4">
                        <h3 class="font-heading font-bold text-brand-950 text-sm" id="editor-form-title">Edit Timer & Data Soal</h3>
                        <form id="form-edit-soal" onsubmit="saveSoalItem(event)" class="space-y-3 text-xs">
                            <input type="hidden" id="soal-edit-index" value="">
                            
                            <div class="grid grid-cols-2 gap-2">
                                <div>
                                    <label class="block font-bold text-slate-400 uppercase mb-1">Nomor Soal</label>
                                    <input type="number" id="edit-soal-nomor" required class="w-full px-3 py-1.5 border border-slate-200 rounded-lg focus:ring-1 focus:ring-brand-500">
                                </div>
                                <div>
                                    <label class="block font-bold text-slate-400 uppercase mb-1">Timer Soal (Detik)</label>
                                    <input type="number" id="edit-soal-waktu" min="30" max="600" required class="w-full px-3 py-1.5 border border-slate-200 rounded-lg focus:ring-1 focus:ring-brand-500 font-bold text-brand-600" placeholder="180">
                                </div>
                            </div>

                            <div class="grid grid-cols-2 gap-2">
                                <div>
                                    <label class="block font-bold text-slate-400 uppercase mb-1">Kategori / Topic</label>
                                    <input type="text" id="edit-soal-mapel" required class="w-full px-3 py-1.5 border border-slate-200 rounded-lg focus:ring-1 focus:ring-brand-500">
                                </div>
                                <div>
                                    <label class="block font-bold text-slate-400 uppercase mb-1">Tingkat Kesulitan</label>
                                    <select id="edit-soal-tingkat" required class="w-full px-3 py-1.5 border border-slate-200 rounded-lg bg-white">
                                        <option value="Mudah">Mudah</option>
                                        <option value="Sedang">Sedang</option>
                                        <option value="Sulit">Sulit</option>
                                    </select>
                                </div>
                            </div>

                            <div>
                                <label class="block font-bold text-slate-400 uppercase mb-1">Tipe Soal</label>
                                <select id="edit-soal-tipe" disabled class="w-full px-3 py-1.5 border border-slate-200 rounded-lg bg-slate-100 font-semibold text-slate-600">
                                    <option value="PG">Pilihan Ganda (Single Choice)</option>
                                    <option value="PGK_MCMA">Pilihan Ganda Kompleks (Banyak Jawaban)</option>
                                    <option value="PGK_BS">Pilihan Ganda Kompleks (Benar / Salah)</option>
                                </select>
                            </div>

                            <div>
                                <label class="block font-bold text-slate-400 uppercase mb-1">Stimulus / Narasi Teks</label>
                                <textarea id="edit-soal-stimulus" rows="3" required class="w-full px-3 py-1.5 border border-slate-200 rounded-lg focus:ring-1 focus:ring-brand-500" placeholder="Pisahkan antar paragraf dengan Enter..."></textarea>
                            </div>
                            
                            <div>
                                <label class="block font-bold text-slate-400 uppercase mb-1">Pertanyaan / Butir Soal</label>
                                <textarea id="edit-soal-teks" rows="2" required class="w-full px-3 py-1.5 border border-slate-200 rounded-lg focus:ring-1 focus:ring-brand-500"></textarea>
                            </div>

                            <div class="flex items-center gap-2 pt-2">
                                <button type="submit" class="flex-grow py-2 bg-brand-600 hover:bg-brand-700 text-white font-bold rounded-lg shadow-sm">Simpan Waktu & Soal</button>
                                <button type="button" onclick="clearEditorForm()" class="px-3 py-2 bg-slate-100 hover:bg-slate-200 text-slate-600 font-bold rounded-lg">Batal</button>
                            </div>
                        </form>
                    </div>

                    <!-- Live Question List with Timers -->
                    <div class="lg:col-span-8 bg-white border border-slate-200 p-5 rounded-2xl shadow-sm space-y-4">
                        <div class="flex items-center justify-between">
                            <h3 class="font-heading font-bold text-brand-950 text-sm">Daftar Soal & Alokasi Timer Per-Soal</h3>
                            <button onclick="resetQuestionsToDefault()" class="px-3 py-1 bg-brand-50 hover:bg-brand-100 border border-brand-100 text-brand-800 rounded-xl text-xs font-bold transition"><i class="fa-solid fa-rotate-left"></i> Reset Ke Standar 25 Soal MTK</button>
                        </div>
                        <div class="max-h-[500px] overflow-y-auto border border-slate-100 rounded-xl divide-y divide-slate-100">
                            <div id="editor-soal-list" class="divide-y divide-slate-100 text-xs">
                                <!-- Dynamic list -->
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

    </main>

    <footer class="bg-brand-950 border-t border-slate-900 py-5 text-slate-400 text-center text-xs">
        <div class="max-w-7xl mx-auto px-4">
            &copy; 2026 CBT TKA Matematika - Variasi PG & PGK (Benar/Salah & Multiple Choice) dengan Fitur Locked Question & Timer Kustom.
        </div>
    </footer>

    <!-- MODAL DIALOG CONTAINER -->
    <div id="custom-modal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-950/60 backdrop-blur-sm hidden">
        <div class="bg-white rounded-3xl border border-brand-100 max-w-sm w-full p-6 shadow-2xl space-y-4">
            <div class="flex items-start gap-3">
                <div id="modal-icon-bg" class="p-2.5 rounded-2xl text-lg flex items-center justify-center shadow-inner">
                    <i id="modal-icon" class="fa-solid"></i>
                </div>
                <div>
                    <h3 id="modal-title" class="font-heading font-extrabold text-base text-slate-900">Judul</h3>
                    <p id="modal-body" class="text-slate-500 text-xs sm:text-sm mt-1 leading-relaxed">Pesan modal...</p>
                </div>
            </div>
            <div class="flex items-center justify-end gap-2 pt-2" id="modal-actions">
                <button id="modal-btn-cancel" class="px-4 py-2 text-xs font-bold text-slate-500 hover:bg-slate-100 rounded-xl transition">Batal</button>
                <button id="modal-btn-confirm" class="px-4 py-2 text-xs font-bold text-white rounded-xl transition">Konfirmasi</button>
            </div>
        </div>
    </div>

    <script>
        const GameAudio = {
            ctx: null,
            enabled: true,
            init() {
                if (!this.ctx) {
                    this.ctx = new (window.AudioContext || window.webkitAudioContext)();
                }
            },
            playClick() {
                if (!this.enabled) return;
                this.init();
                if (this.ctx.state === 'suspended') this.ctx.resume();
                let osc = this.ctx.createOscillator();
                let gain = this.ctx.createGain();
                osc.connect(gain);
                gain.connect(this.ctx.destination);
                osc.type = 'sine';
                osc.frequency.setValueAtTime(800, this.ctx.currentTime);
                gain.gain.setValueAtTime(0.04, this.ctx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.001, this.ctx.currentTime + 0.1);
                osc.start();
                osc.stop(this.ctx.currentTime + 0.1);
            },
            playSlide() {
                if (!this.enabled) return;
                this.init();
                if (this.ctx.state === 'suspended') this.ctx.resume();
                let osc = this.ctx.createOscillator();
                let gain = this.ctx.createGain();
                osc.connect(gain);
                gain.connect(this.ctx.destination);
                osc.type = 'triangle';
                osc.frequency.setValueAtTime(400, this.ctx.currentTime);
                osc.frequency.exponentialRampToValueAtTime(750, this.ctx.currentTime + 0.15);
                gain.gain.setValueAtTime(0.03, this.ctx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.001, this.ctx.currentTime + 0.15);
                osc.start();
                osc.stop(this.ctx.currentTime + 0.15);
            },
            playLockAlert() {
                if (!this.enabled) return;
                this.init();
                if (this.ctx.state === 'suspended') this.ctx.resume();
                let osc = this.ctx.createOscillator();
                let gain = this.ctx.createGain();
                osc.connect(gain);
                gain.connect(this.ctx.destination);
                osc.type = 'sawtooth';
                osc.frequency.setValueAtTime(300, this.ctx.currentTime);
                osc.frequency.setValueAtTime(150, this.ctx.currentTime + 0.15);
                gain.gain.setValueAtTime(0.06, this.ctx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.001, this.ctx.currentTime + 0.3);
                osc.start();
                osc.stop(this.ctx.currentTime + 0.3);
            },
            playVictory() {
                if (!this.enabled) return;
                this.init();
                if (this.ctx.state === 'suspended') this.ctx.resume();
                let now = this.ctx.currentTime;
                let notes = [261.63, 329.63, 392.00, 523.25];
                notes.forEach((freq, idx) => {
                    let osc = this.ctx.createOscillator();
                    let gain = this.ctx.createGain();
                    osc.connect(gain);
                    gain.connect(this.ctx.destination);
                    osc.type = 'sine';
                    osc.frequency.setValueAtTime(freq, now + idx * 0.12);
                    gain.gain.setValueAtTime(0.05, now + idx * 0.12);
                    gain.gain.exponentialRampToValueAtTime(0.001, now + idx * 0.12 + 0.4);
                    osc.start(now + idx * 0.12);
                    osc.stop(now + idx * 0.12 + 0.4);
                });
            }
        };

        function toggleAudio() {
            GameAudio.enabled = !GameAudio.enabled;
            const icon = document.getElementById('sound-icon');
            const text = document.getElementById('sound-text');
            if (GameAudio.enabled) {
                icon.className = "fa-solid fa-volume-high";
                text.innerText = "Sound ON";
                GameAudio.playClick();
            } else {
                icon.className = "fa-solid fa-volume-xmark";
                text.innerText = "Sound OFF";
            }
        }
    </script>

    <script>
        const CONFIG = {
            TEACHER_PASSWORD: "adminTKA2026"
        };

        /*
            QUESTION TYPES:
            1. "PG": Single choice option radio buttons (A, B, C, D)
            2. "PGK_MCMA": Multiple Choice Multiple Answer (Centang opsi A, B, C, D - 1 atau lebih jawaban benar)
            3. "PGK_BS": Pilihan Ganda Kompleks Benar / Salah (Grid / Matriks Pernyataan)
        */
        const DEFAULT_MATHEMATICS_QUESTIONS = [
            {
                nomor: 1,
                mapel: "Aritmetika Sosial",
                tingkat: "Mudah",
                tipe: "PG",
                waktuDetik: 120, // 2 Min
                stimulus: [
                    "Pihak pengelola parkir di sebuah pusat perbelanjaan Kota Semarang menerapkan aturan tarif parkir progresif.",
                    "Aturan Tarif Parkir Mobil: Pada 1 jam pertama dikenakan biaya tetap sebesar Rp 5.000. Setiap tambahan 1 jam berikutnya (atau bagian dari jam) dikenakan tarif Rp 3.000/jam. Jika parkir lebih dari 5 jam, terdapat denda Rp 10.000.",
                    "Rudi memarkir mobilnya mulai pukul 08.15 pagi dan keluar dari gedung parkir pada pukul 14.30 di hari yang sama."
                ],
                soal: "Berapakah total biaya parkir progresif yang harus dibayarkan Rudi saat keluar parkir?",
                opsi: ["A. Rp 20.000", "B. Rp 23.000", "C. Rp 30.000", "D. Rp 33.000"],
                jawaban: "D"
            },
            {
                nomor: 2,
                mapel: "Aritmetika Sosial",
                tingkat: "Mudah",
                tipe: "PGK_MCMA", // Multiple Choice Multiple Answer
                waktuDetik: 120,
                stimulus: [
                    "Toko pakaian 'Gaya Siswa' memberikan diskon ganda untuk pembelian dua stel pakaian.",
                    "Diskon ganda berupa diskon 20% untuk pembelian pertama, serta diskon tambahan 10% dari harga sisa.",
                    "Harga label awal Pakaian A = Rp 150.000 dan Pakaian B = Rp 200.000."
                ],
                soal: "Pilihlah pernyataan yang BENAR mengenai analisis harga potongan pakaian di atas (Bisa memilih lebih dari 1 jawaban):",
                opsi: [
                    "A. Harga Pakaian A setelah diskon ganda adalah Rp 108.000",
                    "B. Total persentase diskon ganda yang didapat setara dengan diskon langsung 28%",
                    "C. Potongan total harga untuk Pakaian B setelah diskon ganda adalah Rp 56.000",
                    "D. Harga Pakaian B setelah diskon ganda adalah Rp 140.000"
                ],
                jawaban: ["A", "B", "C"]
            },
            {
                nomor: 3,
                mapel: "Aritmetika Sosial & PDAM",
                tingkat: "Sedang",
                tipe: "PGK_BS", // Benar / Salah Grid
                waktuDetik: 180,
                stimulus: [
                    "PDAM menetapkan tarif air berjenjang bulanan rumah tangga sebagai berikut:",
                    "- Blok I (0 - 10 m³ pertama): Rp 4.000 per m³\n- Blok II (11 - 20 m³): Rp 6.000 per m³\n- Blok III (Lebih dari 20 m³): Rp 9.000 per m³",
                    "Biaya pemeliharaan tetap adalah Rp 15.000/bulan. Keluarga Pak Budi mengonsumsi 25 m³ air."
                ],
                soal: "Tentukan kebenaran dari masing-masing pernyataan terkait tagihan air Pak Budi berikut:",
                pernyataan: [
                    "Biaya pemakaian air pada Blok I Pak Budi sebesar Rp 40.000",
                    "Biaya pemakaian air pada Blok III Pak Budi sebesar Rp 45.000",
                    "Total tagihan air Pak Budi termasuk biaya pemeliharaan adalah Rp 160.000"
                ],
                jawaban: ["Benar", "Benar", "Benar"]
            },
            {
                nomor: 4,
                mapel: "Statistika & Rasio",
                tingkat: "Sedang",
                tipe: "PG",
                waktuDetik: 180,
                stimulus: [
                    "Dinas Lingkungan Hidup mengumpulkan data rata-rata pembuangan sampah harian lima perumahan:",
                    "1. Perumahan Dahlia: Organik = 120 kg, Anorganik = 80 kg\n2. Perumahan Melati: Organik = 150 kg, Anorganik = 100 kg\n3. Perumahan Flamboyan: Organik = 90 kg, Anorganik = 110 kg\n4. Perumahan Cemara: Organik = 200 kg, Anorganik = 140 kg",
                    "Insentif diberikan kepada perumahan yang memiliki rasio volume sampah organik terhadap anorganik paling tinggi."
                ],
                soal: "Perumahan manakah yang berhak menerima penghargaan insentif lingkungan?",
                opsi: ["A. Perumahan Dahlia", "B. Perumahan Melati", "C. Perumahan Flamboyan", "D. Perumahan Cemara"],
                jawaban: "A"
            },
            {
                nomor: 5,
                mapel: "Fungsi Kuadrat",
                tingkat: "Sulit",
                tipe: "PGK_MCMA",
                waktuDetik: 240,
                stimulus: [
                    "Ketinggian suatu peluru mainan yang ditembakkan vertikal ke atas dalam t detik dimodelkan oleh fungsi kuadrat h(t) = 40t - 5t² (tinggi h dalam satuan meter).",
                    "Peluru bergerak naik hingga mencapai titik puncak maksimum sebelum jatuh kembali ke tanah."
                ],
                soal: "Manakah pernyataan di bawah ini yang BENAR mengenai lintasan peluru tersebut? (Pilih satu atau lebih):",
                opsi: [
                    "A. Peluru mencapai ketinggian maksimum pada t = 4 detik",
                    "B. Ketinggian maksimum yang dicapai peluru adalah 80 meter",
                    "C. Peluru kembali menyentuh tanah pada t = 8 detik",
                    "D. Pada detik ke-2, ketinggian peluru adalah 60 meter"
                ],
                jawaban: ["A", "B", "C"]
            },
            {
                nomor: 6,
                mapel: "Barisan & Deret",
                tingkat: "Sedang",
                tipe: "PG",
                waktuDetik: 180,
                stimulus: [
                    "Sebuah gedung pertunjukan seni disusun dengan barisan kursi yang bertambah secara teratur.",
                    "Baris pertama memiliki 15 kursi, baris kedua memuat 19 kursi, baris ketiga memuat 23 kursi, dan seterusnya mengikuti pola barisan aritmetika.",
                    "Gedung seni tersebut memiliki total 12 baris kursi penonton."
                ],
                soal: "Berapakah total kapasitas keseluruhan kursi penonton yang ada di gedung pertunjukan tersebut?",
                opsi: ["A. 420 kursi", "B. 444 kursi", "C. 480 kursi", "D. 504 kursi"],
                jawaban: "B"
            },
            {
                nomor: 7,
                mapel: "SPLDV",
                tingkat: "Sedang",
                tipe: "PGK_BS",
                waktuDetik: 180,
                stimulus: [
                    "Di toko 'Sembako Berkah', Ibu Aminah membeli 3 kg beras dan 2 kg gula pasir seharga Rp 65.000.",
                    "Pada toko yang sama, Ibu Ratna membeli 2 kg beras dan 3 kg gula pasir seharga Rp 70.000."
                ],
                soal: "Analisislah kebenaran pernyataan berikut berdasarkan sistem persamaan di atas:",
                pernyataan: [
                    "Harga 1 kg beras di toko tersebut adalah Rp 11.000",
                    "Harga 1 kg gula pasir di toko tersebut adalah Rp 16.000",
                    "Ibu Maya yang membeli 1 kg beras dan 1 kg gula pasir harus membayar Rp 27.000"
                ],
                jawaban: ["Benar", "Benar", "Benar"]
            },
            {
                nomor: 8,
                mapel: "Geometri / Pythagoras",
                tingkat: "Mudah",
                tipe: "PG",
                waktuDetik: 120,
                stimulus: [
                    "Sebuah tiang bendera setinggi 12 meter ditegakkan di atas tanah datar.",
                    "Sebuah kawat pemancang diikatkan pada ujung atas tiang bendera dan ditancapkan ke tanah pada jarak 9 meter dari pangkal bawah tiang."
                ],
                soal: "Berapakah panjang minimal kawat pemancang yang dibutuhkan tersebut?",
                opsi: ["A. 13 meter", "B. 15 meter", "C. 17 meter", "D. 21 meter"],
                jawaban: "B"
            },
            {
                nomor: 9,
                mapel: "Bangun Ruang",
                tingkat: "Sulit",
                tipe: "PG",
                waktuDetik: 240,
                stimulus: [
                    "Sebuah bak penampungan air berbentuk tabung dengan diameter alas 140 cm dan tinggi 100 cm (π = 22/7).",
                    "Bak tersebut awalnya terisi penuh air. Karena terdapat kebocoran kecil di dasar bak, air berkurang sebanyak 10 liter setiap jamnya."
                ],
                soal: "Berapa liter sisa air di dalam bak penampungan tersebut setelah 15 jam mengalami kebocoran? (1 liter = 1.000 cm³)",
                opsi: ["A. 1.390 liter", "B. 1.400 liter", "C. 1.450 liter", "D. 1.540 liter"],
                jawaban: "A"
            },
            {
                nomor: 10,
                mapel: "Statistika",
                tingkat: "Sedang",
                tipe: "PGK_BS",
                waktuDetik: 180,
                stimulus: [
                    "Nilai rata-rata ujian Matematika dari 20 siswa kelas 9A adalah 75.",
                    "Kemudian, 5 orang siswa susulan mengikuti ujian dan setelah nilai kelimanya digabungkan, nilai rata-rata keseluruhan kelas naik menjadi 78."
                ],
                soal: "Tentukan kebenaran analisis penggabungan nilai rata-rata berikut:",
                pernyataan: [
                    "Jumlah total nilai dari 20 siswa pertama adalah 1.500",
                    "Jumlah total nilai setelah digabung dengan 5 siswa susulan adalah 1.950",
                    "Nilai rata-rata dari 5 siswa susulan tersebut adalah 90"
                ],
                jawaban: ["Benar", "Benar", "Benar"]
            },
            {
                nomor: 11,
                mapel: "Peluang",
                tingkat: "Mudah",
                tipe: "PG",
                waktuDetik: 120,
                stimulus: [
                    "Dalam permainan papan edukasi, dua buah dadu bermata enam dilempar secara bersamaan satu kali."
                ],
                soal: "Berapakah peluang munculnya kedua mata dadu yang berjumlah 8?",
                opsi: ["A. 1/9", "B. 5/36", "C. 1/6", "D. 7/36"],
                jawaban: "B"
            },
            {
                nomor: 12,
                mapel: "Kesebangunan",
                tingkat: "Mudah",
                tipe: "PG",
                waktuDetik: 120,
                stimulus: [
                    "Seorang siswa setinggi 150 cm berdiri tegak pada siang hari dan memiliki panjang bayangan 200 cm di atas tanah datar.",
                    "Pada waktu yang sama, bayangan sebuah pohon yang berada tepat di samping sekolah diukur sepanjang 12 meter."
                ],
                soal: "Berapakah tinggi sebenarnya dari pohon tersebut?",
                opsi: ["A. 8 meter", "B. 9 meter", "C. 10 meter", "D. 11 meter"],
                jawaban: "B"
            },
            {
                nomor: 13,
                mapel: "Transformasi Geometri",
                tingkat: "Sedang",
                tipe: "PGK_MCMA",
                waktuDetik: 180,
                stimulus: [
                    "Posisi sebuah kapal laut terdeteksi pada koordinat A(3, -5) pada peta layar radar navigasi laut.",
                    "Kapal tersebut mengalami pergeseran translasi T(-4, 7), lalu posisinya dicerminkan (di-refleksi) terhadap garis sumbu y."
                ],
                soal: "Pilihlah pernyataan koordinat pergeseran kapal yang BENAR di bawah ini:",
                opsi: [
                    "A. Koordinat kapal setelah translasi T(-4, 7) adalah (-1, 2)",
                    "B. Koordinat titik akhir kapal setelah pencerminan terhadap sumbu y adalah (1, 2)",
                    "C. Jarak pergeseran horizontal kapal dari titik awal ke hasil translasi adalah -4 unit",
                    "D. Hasil bayangan refleksi terhadap sumbu y mengubah tanda koordinat ordinat (y)"
                ],
                jawaban: ["A", "B", "C"]
            },
            {
                nomor: 14,
                mapel: "Pertidaksamaan Linear",
                tingkat: "Sedang",
                tipe: "PG",
                waktuDetik: 180,
                stimulus: [
                    "Sebuah lift logistik di gedung perkantoran memiliki daya angkut beban maksimum tidak boleh melebihi 600 kg.",
                    "Operator lift yang memiliki berat badan 75 kg akan membawa sejumlah kotak barang homogen yang masing-masing berbobot 35 kg."
                ],
                soal: "Berapakah jumlah kotak barang paling banyak yang dapat diangkut dalam sekali jalan oleh lift tersebut?",
                opsi: ["A. 14 kotak", "B. 15 kotak", "C. 16 kotak", "D. 17 kotak"],
                jawaban: "B"
            },
            {
                nomor: 15,
                mapel: "Skala & Peta",
                tingkat: "Sedang",
                tipe: "PG",
                waktuDetik: 180,
                stimulus: [
                    "Sebuah denah lahan perkebunan berbentuk persegi panjang digambar dengan skala 1 : 500.",
                    "Ukuran panjang perkebunan pada gambar adalah 12 cm dan lebarnya 8 cm."
                ],
                soal: "Berapakah luas wilayah sebenarnya dari lahan perkebunan tersebut dalam satuan meter persegi (m²)?",
                opsi: ["A. 2.400 m²", "B. 3.000 m²", "C. 4.800 m²", "D. 6.000 m²"],
                jawaban: "A"
            },
            {
                nomor: 16,
                mapel: "Himpunan",
                tingkat: "Sedang",
                tipe: "PGK_BS",
                waktuDetik: 180,
                stimulus: [
                    "Dari hasil survei terhadap 40 siswa kelas 9, tercatat 25 siswa menyukai ekstrakurikuler Basket, 20 siswa menyukai Futsal, dan 5 siswa tidak menyukai keduanya."
                ],
                soal: "Berdasarkan Hukum Himpunan, tentukan kebenaran dari pernyataan berikut:",
                pernyataan: [
                    "Banyaknya siswa yang menyukai minimal salah satu ekstrakurikuler adalah 35 siswa",
                    "Banyaknya siswa yang menyukai KEDUA jenis ekstrakurikuler adalah 10 siswa",
                    "Siswa yang HANYA menyukai Basket berjumlah 15 siswa"
                ],
                jawaban: ["Benar", "Benar", "Benar"]
            },
            {
                nomor: 17,
                mapel: "Interpretasi Data",
                tingkat: "Mudah",
                tipe: "PG",
                waktuDetik: 120,
                stimulus: [
                    "Toko Buku 'Cerdas' mencatat penjualan buku matematika selama 5 hari berturut-turut:\nSenin: 24 eksemplar, Selasa: 30 eksemplar, Rabu: 18 eksemplar, Kamis: 36 eksemplar, Jumat: 42 eksemplar."
                ],
                soal: "Berapakah persentase penjualan buku pada hari Kamis dibandingkan total penjualan selama 5 hari tersebut?",
                opsi: ["A. 20%", "B. 24%", "C. 28%", "D. 30%"],
                jawaban: "B"
            },
            {
                nomor: 18,
                mapel: "Eksponen & Bentuk Akar",
                tingkat: "Sedang",
                tipe: "PG",
                waktuDetik: 180,
                stimulus: [
                    "Dalam laboratorium sains, peneliti menghitung hasil penyederhanaan ekspresi matematis dari operasi perpangkatan: (2³ × 2⁴) / 2⁵."
                ],
                soal: "Berapakah nilai hasil akhir sederhananya?",
                opsi: ["A. 2", "B. 4", "C. 8", "D. 16"],
                jawaban: "B"
            },
            {
                nomor: 19,
                mapel: "Persamaan Garis Lurus",
                tingkat: "Sedang",
                tipe: "PG",
                waktuDetik: 180,
                stimulus: [
                    "Sebuah garis lurus g melalui titik koordinat P(2, 5) dan Q(6, 13) pada bidang Kartesius."
                ],
                soal: "Berapakah nilai gradien (kemiringan m) dari garis lurus g tersebut?",
                opsi: ["A. 1,5", "B. 2", "C. 2,5", "D. 3"],
                jawaban: "B"
            },
            {
                nomor: 20,
                mapel: "Lingkaran",
                tingkat: "Sedang",
                tipe: "PGK_MCMA",
                waktuDetik: 180,
                stimulus: [
                    "Sebuah sepeda memiliki roda berbentuk lingkaran dengan jari-jari 35 cm (π = 22/7). Roda tersebut berputar sempurna sebanyak 500 kali di jalan lurus."
                ],
                soal: "Pilihlah analisis ukuran putaran roda berikut yang BENAR (Bisa memilih lebih dari 1):",
                opsi: [
                    "A. Keliling roda sepeda tersebut adalah 220 cm (2,2 meter)",
                    "B. Jarak tempuh total sepeda setelah 500 putaran adalah 1.100 meter",
                    "C. Jika roda berputar 1.000 kali, jarak tempuh sepedanya adalah 2,2 km",
                    "D. Diameter roda sepeda tersebut adalah 50 cm"
                ],
                jawaban: ["A", "B", "C"]
            },
            {
                nomor: 21,
                mapel: "Luas Permukaan Gabungan",
                tingkat: "Sulit",
                tipe: "PG",
                waktuDetik: 240,
                stimulus: [
                    "Sebuah tempat sampah terbuat dari kaleng berbentuk tabung tanpa tutup dengan diameter alas 28 cm dan tinggi 30 cm (π = 22/7)."
                ],
                soal: "Berapakah luas permukaan seng yang dibutuhkan untuk membuat tempat sampah tersebut?",
                opsi: ["A. 2.904 cm²", "B. 3.256 cm²", "C. 3.520 cm²", "D. 3.872 cm²"],
                jawaban: "B"
            },
            {
                nomor: 22,
                mapel: "Frekuensi Harapan",
                tingkat: "Sedang",
                tipe: "PG",
                waktuDetik: 180,
                stimulus: [
                    "Sebuah kantong berisi 5 bola merah, 3 bola kuning, dan 2 bola hijau. Sebuah bola diambil secara acak lalu dikembalikan lagi, dan percobaan diulang sebanyak 120 kali."
                ],
                soal: "Berapakah frekuensi harapan terambilnya bola berwarna merah?",
                opsi: ["A. 36 kali", "B. 48 kali", "C. 60 kali", "D. 72 kali"],
                jawaban: "C"
            },
            {
                nomor: 23,
                mapel: "Aljabar HOTS",
                tingkat: "Sulit",
                tipe: "PG",
                waktuDetik: 300,
                stimulus: [
                    "Dua buah pompa air A dan B bekerja mengisi sebuah kolam renang. Jika kedua pompa bekerja bersama-sama, kolam terisi penuh dalam waktu 4 jam.",
                    "Jika hanya pompa A yang bekerja sendirian, butuh waktu 6 jam untuk mengisi kolam hingga penuh."
                ],
                soal: "Berapa jam waktu yang dibutuhkan jika hanya pompa B yang bekerja sendirian mengisi kolam dari kosong hingga penuh?",
                opsi: ["A. 8 jam", "B. 10 jam", "C. 12 jam", "D. 14 jam"],
                jawaban: "C"
            },
            {
                nomor: 24,
                mapel: "Perbandingan Berbalik Nilai",
                tingkat: "Sedang",
                tipe: "PGK_BS",
                waktuDetik: 180,
                stimulus: [
                    "Sebuah proyek perbaikan jalan ditargetkan selesai dalam waktu 30 hari oleh 12 orang pekerja.",
                    "Setelah berjalan 10 hari, pengerjaan proyek terhenti selama 5 hari karena cuaca buruk."
                ],
                soal: "Evaluasilah kebenaran analisis penambahan pekerja proyek jalan di bawah ini:",
                pernyataan: [
                    "Sisa hari produktif pengerjaan proyek tersisa 15 hari setelah terhenti",
                    "Jumlah total pekerja yang dibutuhkan agar proyek selesai tepat waktu adalah 16 orang",
                    "Tambahan pekerja baru yang harus ditambah adalah 4 orang pekerja"
                ],
                jawaban: ["Benar", "Benar", "Benar"]
            },
            {
                nomor: 25,
                mapel: "Kombinatorika",
                tingkat: "Sedang",
                tipe: "PG",
                waktuDetik: 180,
                stimulus: [
                    "Kota A dan Kota B dihubungkan oleh 4 rute jalan bus. Kota B dan Kota C dihubungkan oleh 3 rute jalan bus."
                ],
                soal: "Berapakah banyaknya variasi rute perjalanan yang dapat ditempuh seseorang dari Kota A menuju Kota C melalui Kota B dan kembali lagi ke Kota A tanpa melewati rute bus yang sama?",
                opsi: ["A. 36 rute", "B. 72 rute", "C. 108 rute", "D. 144 rute"],
                jawaban: "B"
            }
        ];

        // GLOBAL APPLICATION STATE
        let questions = [];
        let currentQuestionIndex = 0;
        let activeStudent = null;
        
        // TIMERS & LOCK STATE
        let examTimerInterval = null;
        let totalExamTimeMinutes = 75; // Default 75 Mins (Editable by teacher)
        let examTimeLeftInSeconds = 75 * 60; 
        let questionTimeLeftInSeconds = 0; // Current Question Timer
        let lockedSaved = {}; // Track locked question indices
        
        let answersSaved = {};
        let doubtfulSaved = {}; 
        let examStartTimeStr = "";
        let analysisChartInstance = null;

        // TOOLBAR STATES
        let activeHighlighter = false;
        let activeReadingRuler = false;

        window.onload = function() {
            loadQuestions();
            loadConfigAndSubmissions();
            updateGateDisplayTime();
            switchView('student-gate');
        };

        function loadQuestions() {
            const stored = localStorage.getItem('tka_matematika_questions');
            if (stored) {
                try {
                    questions = JSON.parse(stored);
                } catch(e) {
                    questions = JSON.parse(JSON.stringify(DEFAULT_MATHEMATICS_QUESTIONS));
                }
            } else {
                questions = JSON.parse(JSON.stringify(DEFAULT_MATHEMATICS_QUESTIONS));
            }

            // Load configured total exam time
            const storedTime = localStorage.getItem('tka_total_exam_time_minutes');
            if (storedTime && !isNaN(parseInt(storedTime))) {
                totalExamTimeMinutes = parseInt(storedTime);
            } else {
                totalExamTimeMinutes = 75; // Default 75 Menit
            }
        }

        function updateGateDisplayTime() {
            const el = document.getElementById('gate-total-time-display');
            if (el) el.innerText = totalExamTimeMinutes;
            const inputEl = document.getElementById('input-total-exam-mins');
            if (inputEl) inputEl.value = totalExamTimeMinutes;
            updateCalculatedTimeSummary();
        }

        function updateCalculatedTimeSummary() {
            const totalSecs = questions.reduce((sum, q) => sum + (q.waktuDetik || 180), 0);
            const sumMins = Math.round(totalSecs / 60);
            const sumEl = document.getElementById('total-calculated-time-sum');
            if (sumEl) {
                sumEl.innerText = `${sumMins} Menit (${totalSecs} dtk)`;
            }
        }

        function saveTotalExamTime() {
            const inputVal = parseInt(document.getElementById('input-total-exam-mins').value);
            if (!inputVal || inputVal < 1 || inputVal > 300) {
                showModal("Input Tidak Valid", "Masukkan jumlah menit antara 1 sampai 300 menit.", "warning", "Oke", "Batal", null, null);
                return;
            }

            totalExamTimeMinutes = inputVal;
            localStorage.setItem('tka_total_exam_time_minutes', totalExamTimeMinutes);
            updateGateDisplayTime();
            showToast(`Total waktu ujian berhasil diubah menjadi ${totalExamTimeMinutes} Menit!`);
        }

        function useAutoCalculatedTime() {
            const totalSecs = questions.reduce((sum, q) => sum + (q.waktuDetik || 180), 0);
            const sumMins = Math.round(totalSecs / 60);
            document.getElementById('input-total-exam-mins').value = sumMins;
            saveTotalExamTime();
        }

        function loadConfigAndSubmissions() {
            if (!localStorage.getItem('tka_literasi_submissions')) {
                localStorage.setItem('tka_literasi_submissions', JSON.stringify([]));
            }
        }
    </script>

    <script>
        function switchView(viewId) {
            GameAudio.playClick();
            const views = ['student-gate', 'student-exam', 'student-results', 'teacher-login', 'teacher-dashboard'];
            views.forEach(v => {
                const el = document.getElementById(`view-${v}`);
                if (el) el.classList.add('hidden');
            });

            const tabStudent = document.getElementById('tab-student');
            if (tabStudent) {
                tabStudent.className = "px-3.5 py-2 text-xs sm:text-sm font-semibold rounded-xl transition-all " + 
                    (viewId.startsWith('student') ? 'bg-brand-600 text-white shadow-md' : 'text-brand-200 hover:text-white hover:bg-white/10');
            }
            const tabTeacher = document.getElementById('tab-teacher');
            if (tabTeacher) {
                tabTeacher.className = "px-3.5 py-2 text-xs sm:text-sm font-semibold rounded-xl transition-all " + 
                    (viewId.startsWith('teacher') ? 'bg-slate-900 text-white border border-brand-800' : 'text-brand-200 hover:text-white hover:bg-white/10');
            }

            const targetView = document.getElementById(`view-${viewId}`);
            if (targetView) targetView.classList.remove('hidden');
            
            if (!viewId.startsWith('student-exam') && examTimerInterval) {
                clearInterval(examTimerInterval);
            }
        }

        /* 
           PERBAIKAN FITUR STABILO (BLOK TEKS) 
           Memungkinkan siswa melakukan seleksi/blok kata/kalimat di area stimulus/soal
        */
        function toggleHighlighter() {
            activeHighlighter = !activeHighlighter;
            const btn = document.getElementById('btn-highlighter');
            const label = document.getElementById('label-highlighter-status');
            
            if (activeHighlighter) {
                btn.className = "px-3 py-1.5 text-xs font-semibold rounded-lg bg-amber-400 text-slate-950 shadow-md flex items-center gap-1.5 transition font-bold";
                if (label) label.innerText = "Stabilo Teks (ON)";
                showToast("Stabilo Aktif: Blok/seleksi teks yang ingin ditandai!");
            } else {
                btn.className = "px-3 py-1.5 text-xs font-semibold rounded-lg bg-white border text-slate-700 hover:bg-brand-50 flex items-center gap-1.5 transition";
                if (label) label.innerText = "Stabilo Teks (Off)";
            }
            setupTextHighlighterEvent();
        }

        function setupTextHighlighterEvent() {
            const stimulusContainer = document.getElementById('display-stimulus-container');
            const soalTextElement = document.getElementById('display-soal-text');

            const handleSelection = function() {
                if (!activeHighlighter) return;
                const sel = window.getSelection();
                if (!sel || sel.isCollapsed || sel.rangeCount === 0) return;

                const selectedText = sel.toString().trim();
                if (selectedText.length < 1) return;

                try {
                    const range = sel.getRangeAt(0);
                    // Check if selection is inside container
                    const span = document.createElement('span');
                    span.className = 'highlighted-text';
                    range.surroundContents(span);
                    sel.removeAllRanges();
                    GameAudio.playClick();
                } catch(e) {
                    // Fallback for complex cross-node selection
                    highlightSelectionFallback(sel);
                }
            };

            if (activeHighlighter) {
                stimulusContainer.onmouseup = handleSelection;
                soalTextElement.onmouseup = handleSelection;
                stimulusContainer.ontouchend = handleSelection;
                soalTextElement.ontouchend = handleSelection;
            } else {
                stimulusContainer.onmouseup = null;
                soalTextElement.onmouseup = null;
                stimulusContainer.ontouchend = null;
                soalTextElement.ontouchend = null;
            }
        }

        function highlightSelectionFallback(sel) {
            try {
                const range = sel.getRangeAt(0);
                const documentFragment = range.extractContents();
                const span = document.createElement('span');
                span.className = 'highlighted-text';
                span.appendChild(documentFragment);
                range.insertNode(span);
                sel.removeAllRanges();
                GameAudio.playClick();
            } catch(err) {
                console.log("Highlight fallback skipped due to non-text node boundary", err);
            }
        }

        function clearHighlights() {
            const highlights = document.querySelectorAll('.highlighted-text');
            highlights.forEach(el => {
                const parent = el.parentNode;
                while (el.firstChild) {
                    parent.insertBefore(el.firstChild, el);
                }
                parent.removeChild(el);
            });
            GameAudio.playClick();
            showToast("Seluruh tanda stabilo telah dibersihkan.");
        }

        function toggleReadingRuler() {
            activeReadingRuler = !activeReadingRuler;
            const btn = document.getElementById('btn-ruler');
            const panel = document.getElementById('panel-stimulus');
            
            if (activeReadingRuler) {
                btn.className = "px-3 py-1.5 text-xs font-semibold rounded-lg bg-brand-600 border border-brand-700 text-white flex items-center gap-1.5 transition shadow";
                panel.classList.add('ruler-focus-active');
                showToast("Mistar Fokus Aktif: Klik baris paragraf!");
            } else {
                btn.className = "px-3 py-1.5 text-xs font-semibold rounded-lg bg-white border text-slate-700 hover:bg-brand-50 flex items-center gap-1.5 transition";
                panel.classList.remove('ruler-focus-active');
                const lines = panel.querySelectorAll('p');
                lines.forEach(l => l.classList.remove('focused-line'));
            }
        }

        function triggerLineFocus(element) {
            if (!activeReadingRuler) return;
            const panel = document.getElementById('panel-stimulus');
            const lines = panel.querySelectorAll('p');
            lines.forEach(l => l.classList.remove('focused-line'));
            element.classList.add('focused-line');
            GameAudio.playClick();
        }

        function toggleScratchpad() {
            const panel = document.getElementById('scratchpad-panel');
            panel.classList.toggle('hidden');
        }

        function showModal(title, text, type, confirmText, cancelText, onConfirm, onCancel) {
            const modal = document.getElementById('custom-modal');
            const iconBg = document.getElementById('modal-icon-bg');
            const icon = document.getElementById('modal-icon');
            
            document.getElementById('modal-title').innerText = title;
            document.getElementById('modal-body').innerHTML = text;

            if (type === 'danger') {
                iconBg.className = "p-2.5 rounded-2xl text-lg bg-rose-50 text-vibrant-rose shadow-inner";
                icon.className = "fa-solid fa-triangle-exclamation";
                document.getElementById('modal-btn-confirm').className = "px-4 py-2 text-xs font-bold text-white bg-vibrant-rose hover:bg-rose-600 rounded-xl transition";
            } else if (type === 'warning') {
                iconBg.className = "p-2.5 rounded-2xl text-lg bg-amber-50 text-vibrant-amber shadow-inner";
                icon.className = "fa-solid fa-circle-exclamation";
                document.getElementById('modal-btn-confirm').className = "px-4 py-2 text-xs font-bold text-white bg-vibrant-amber hover:bg-amber-600 rounded-xl transition";
            } else {
                iconBg.className = "p-2.5 rounded-2xl text-lg bg-emerald-50 text-vibrant-emerald shadow-inner";
                icon.className = "fa-solid fa-circle-check";
                document.getElementById('modal-btn-confirm').className = "px-4 py-2 text-xs font-bold text-white bg-vibrant-emerald hover:bg-emerald-600 rounded-xl transition";
            }

            document.getElementById('modal-btn-confirm').innerText = confirmText;
            document.getElementById('modal-btn-cancel').innerText = cancelText;

            const btnConfirm = document.getElementById('modal-btn-confirm');
            const btnCancel = document.getElementById('modal-btn-cancel');

            const newConfirm = btnConfirm.cloneNode(true);
            const newCancel = btnCancel.cloneNode(true);
            btnConfirm.replaceWith(newConfirm);
            btnCancel.replaceWith(newCancel);

            newConfirm.addEventListener('click', () => {
                modal.classList.add('hidden');
                GameAudio.playClick();
                if (onConfirm) onConfirm();
            });

            newCancel.addEventListener('click', () => {
                modal.classList.add('hidden');
                GameAudio.playClick();
                if (onCancel) onCancel();
            });

            modal.classList.remove('hidden');
        }

        function showToast(text) {
            const toast = document.createElement('div');
            toast.className = "fixed bottom-4 left-4 z-50 bg-slate-900 text-white text-xs py-2.5 px-4 rounded-xl shadow-lg border border-slate-700 animate-bounce flex items-center gap-1.5";
            toast.innerHTML = `<i class="fa-solid fa-clock text-amber-400"></i> ${text}`;
            document.body.appendChild(toast);
            setTimeout(() => { toast.remove(); }, 3500);
        }
    </script>

    <script>
        function startExam(e) {
            e.preventDefault();

            const nama = document.getElementById('input-nama').value.trim();
            const kelas = document.getElementById('input-kelas').value;
            const absen = document.getElementById('input-absen').value.trim();

            if (!nama || !kelas || !absen) {
                showModal("Lengkapi Identitas", "Silakan isi seluruh kolom identitas terlebih dahulu.", "warning", "Oke", "Batal", null, null);
                return;
            }

            const submissions = JSON.parse(localStorage.getItem('tka_literasi_submissions') || '[]');
            const duplicate = submissions.some(sub => 
                sub.nama.toLowerCase() === nama.toLowerCase() && 
                sub.kelas === kelas && 
                parseInt(sub.absen) === parseInt(absen)
            );

            if (duplicate) {
                showModal("Identitas Terpakai", "Identitas ini sudah menyelesaikan ujian TKA.", "danger", "Ganti Identitas", "Batal", null, null);
                return;
            }

            activeStudent = { nama, kelas, absen };
            answersSaved = {};
            doubtfulSaved = {};
            lockedSaved = {}; // Reset locks
            currentQuestionIndex = 0;

            // Calculate overall exam duration in seconds based on teacher setting (default 75 mins)
            examTimeLeftInSeconds = totalExamTimeMinutes * 60;

            const now = new Date();
            examStartTimeStr = `${String(now.getHours()).padStart(2, '0')}:${String(now.getMinutes()).padStart(2, '0')}`;

            document.getElementById('display-student-name').innerText = nama;
            document.getElementById('display-student-class').innerText = kelas;
            document.getElementById('display-student-absen').innerText = String(absen).padStart(2, '0');

            switchView('student-exam');
            renderGridIndicators();
            showQuestion(0);
            startMasterCountdown();
        }

        // DUAL TIMERS TICKER WITH PER-QUESTION LOCK
        function startMasterCountdown() {
            if (examTimerInterval) clearInterval(examTimerInterval);

            examTimerInterval = setInterval(() => {
                // 1. Overall Exam Timer Countdown
                if (examTimeLeftInSeconds <= 0) {
                    clearInterval(examTimerInterval);
                    document.getElementById('exam-timer').innerText = "00:00:00";
                    forceEndExam();
                    return;
                }
                examTimeLeftInSeconds--;

                const hours = Math.floor(examTimeLeftInSeconds / 3600);
                const minutes = Math.floor((examTimeLeftInSeconds % 3600) / 60);
                const seconds = examTimeLeftInSeconds % 60;
                document.getElementById('exam-timer').innerText = 
                    `${String(hours).padStart(2, '0')}:${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;

                // 2. Per-Question Timer Countdown (if current question not locked)
                const qNum = questions[currentQuestionIndex].nomor;
                if (!lockedSaved[qNum] && questionTimeLeftInSeconds > 0) {
                    questionTimeLeftInSeconds--;
                    const qMin = Math.floor(questionTimeLeftInSeconds / 60);
                    const qSec = questionTimeLeftInSeconds % 60;
                    document.getElementById('question-timer').innerText = 
                        `${String(qMin).padStart(2, '0')}:${String(qSec).padStart(2, '0')}`;

                    if (questionTimeLeftInSeconds <= 0) {
                        // PER-QUESTION TIMER EXPIRED! LOCK QUESTION
                        lockedSaved[qNum] = true; // Lock this question!
                        GameAudio.playLockAlert();
                        showToast(`Waktu Soal No. ${qNum} Habis! Jawaban Soal Ini DILOCK.`);

                        // Refresh view to apply lock overlay
                        showQuestion(currentQuestionIndex);

                        // Auto advance to next unlocked question after short delay
                        setTimeout(() => {
                            if (currentQuestionIndex < questions.length - 1) {
                                goToQuestion(currentQuestionIndex + 1);
                            }
                        }, 1200);
                    }
                }
            }, 1000);
        }

        function showQuestion(index) {
            if (index < 0 || index >= questions.length) return;
            currentQuestionIndex = index;

            const q = questions[index];
            const isLocked = lockedSaved[q.nomor] === true;

            document.getElementById('current-question-num').innerText = q.nomor;
            document.getElementById('total-questions-num').innerText = questions.length;
            document.getElementById('display-mapel').innerText = q.mapel || "TKA MTK";
            document.getElementById('display-soal-text').innerText = q.soal;
            document.getElementById('label-quest-title').innerText = `Level ${q.nomor} Challenge (${q.tingkat || 'Sedang'})`;
            document.getElementById('display-difficulty-badge').innerText = q.tingkat || 'Sedang';

            // Question Type Badge
            const typeBadge = document.getElementById('display-question-type-badge');
            if (q.tipe === 'PGK_MCMA') {
                typeBadge.innerText = "PG Kompleks (Jawaban > 1)";
                typeBadge.className = "px-2.5 py-1 bg-purple-100 text-purple-800 text-[10px] font-extrabold rounded-lg uppercase tracking-wider";
            } else if (q.tipe === 'PGK_BS') {
                typeBadge.innerText = "PG Kompleks (Benar / Salah)";
                typeBadge.className = "px-2.5 py-1 bg-amber-100 text-amber-900 text-[10px] font-extrabold rounded-lg uppercase tracking-wider";
            } else {
                typeBadge.innerText = "Pilihan Ganda";
                typeBadge.className = "px-2.5 py-1 bg-indigo-50 text-indigo-700 text-[10px] font-extrabold rounded-lg uppercase tracking-wider";
            }

            // Lock banner UI
            const lockBanner = document.getElementById('locked-question-banner');
            const timerCard = document.getElementById('question-timer-card');
            const timerLabel = document.getElementById('question-timer-label');
            const timerDisplay = document.getElementById('question-timer');

            if (isLocked) {
                lockBanner.classList.remove('hidden');
                timerCard.className = "bg-red-50 border border-red-200 px-3 py-1.5 rounded-xl text-right";
                timerLabel.innerHTML = `<i class="fa-solid fa-lock text-red-500"></i> Status Soal`;
                timerDisplay.innerText = "TERLOCK";
                timerDisplay.className = "text-xs font-mono font-black text-red-600 uppercase";
            } else {
                lockBanner.classList.add('hidden');
                timerCard.className = "bg-amber-50 border border-amber-200 px-3 py-1.5 rounded-xl text-right";
                timerLabel.innerHTML = `<i class="fa-solid fa-hourglass-half text-amber-500"></i> Timer Soal Ini`;
                
                // Set/reset per-question timer count if not locked
                questionTimeLeftInSeconds = q.waktuDetik || 180;
                const qMin = Math.floor(questionTimeLeftInSeconds / 60);
                const qSec = questionTimeLeftInSeconds % 60;
                timerDisplay.innerText = `${String(qMin).padStart(2, '0')}:${String(qSec).padStart(2, '0')}`;
                timerDisplay.className = "text-sm font-mono font-black text-amber-800";
            }

            // Render Stimulus Text
            const stimulusContainer = document.getElementById('display-stimulus-container');
            stimulusContainer.innerHTML = "";
            if (Array.isArray(q.stimulus)) {
                q.stimulus.forEach(para => {
                    const p = document.createElement('p');
                    p.innerText = para;
                    p.setAttribute('onclick', 'triggerLineFocus(this)');
                    stimulusContainer.appendChild(p);
                });
            } else {
                const p = document.createElement('p');
                p.innerText = q.stimulus;
                p.setAttribute('onclick', 'triggerLineFocus(this)');
                stimulusContainer.appendChild(p);
            }

            // Setup text highlighter binding
            setupTextHighlighterEvent();

            // Render Options Container
            renderOptionsPanel(q, isLocked);

            // Action Buttons Visibility
            document.getElementById('btn-prev-question').disabled = (index === 0);
            if (index === questions.length - 1) {
                document.getElementById('btn-next-question').classList.add('hidden');
                document.getElementById('btn-finish-exam').classList.remove('hidden');
            } else {
                document.getElementById('btn-next-question').classList.remove('hidden');
                document.getElementById('btn-finish-exam').classList.add('hidden');
            }

            // Update Doubtful Button UI
            const isDoubt = doubtfulSaved[q.nomor] === true;
            const btnDoubt = document.getElementById('btn-doubtful-toggle');
            const iconDoubt = document.getElementById('icon-doubtful');
            if (isDoubt) {
                btnDoubt.className = "game-btn px-3.5 py-2.5 text-xs font-bold rounded-xl flex items-center justify-center gap-1.5 transition border border-amber-500 bg-amber-500 text-white shadow-md";
                iconDoubt.className = "fa-solid fa-square-check";
            } else {
                btnDoubt.className = "game-btn px-3.5 py-2.5 text-xs font-bold rounded-xl flex items-center justify-center gap-1.5 transition border border-amber-300 bg-amber-50 text-amber-700 hover:bg-amber-100";
                iconDoubt.className = "fa-regular fa-square";
            }

            renderGridIndicators();
            updateProgressBar();
        }

        function renderOptionsPanel(q, isLocked) {
            const container = document.getElementById('display-opsi-container');
            container.innerHTML = "";

            const savedAns = answersSaved[q.nomor];

            if (q.tipe === "PG") {
                // Single Choice Radio Options
                q.opsi.forEach((optStr, idx) => {
                    const letter = String.fromCharCode(65 + idx); // A, B, C, D
                    const optId = `opt-${q.nomor}-${letter}`;
                    const isChecked = savedAns === letter;

                    const wrapper = document.createElement('div');
                    wrapper.className = "option-card relative";

                    wrapper.innerHTML = `
                        <input type="radio" id="${optId}" name="question-${q.nomor}" value="${letter}" ${isChecked ? 'checked' : ''} ${isLocked ? 'disabled' : ''} onchange="selectRadioAnswer(${q.nomor}, '${letter}')" class="hidden">
                        <label for="${optId}" class="flex items-center p-3 sm:p-3.5 border-2 border-slate-200 rounded-xl cursor-pointer hover:border-brand-300 transition ${isLocked ? 'opacity-60 cursor-not-allowed' : ''}">
                            <span class="w-7 h-7 flex items-center justify-center rounded-lg border-2 border-slate-300 font-extrabold text-xs mr-3 shrink-0 text-slate-500">${letter}</span>
                            <span class="text-xs sm:text-sm font-semibold text-slate-800 leading-snug">${optStr.replace(/^[A-D]\.\s*/, '')}</span>
                        </label>
                    `;
                    container.appendChild(wrapper);
                });
            } 
            else if (q.tipe === "PGK_MCMA") {
                // Multiple Choice Multiple Answer Checkboxes
                const currentArr = Array.isArray(savedAns) ? savedAns : [];

                q.opsi.forEach((optStr, idx) => {
                    const letter = String.fromCharCode(65 + idx);
                    const optId = `opt-${q.nomor}-${letter}`;
                    const isChecked = currentArr.includes(letter);

                    const wrapper = document.createElement('div');
                    wrapper.className = "option-card relative";

                    wrapper.innerHTML = `
                        <input type="checkbox" id="${optId}" value="${letter}" ${isChecked ? 'checked' : ''} ${isLocked ? 'disabled' : ''} onchange="toggleCheckboxAnswer(${q.nomor}, '${letter}')" class="hidden">
                        <label for="${optId}" class="flex items-center p-3 sm:p-3.5 border-2 border-slate-200 rounded-xl cursor-pointer hover:border-brand-300 transition ${isLocked ? 'opacity-60 cursor-not-allowed' : ''}">
                            <span class="w-7 h-7 flex items-center justify-center rounded-lg border-2 border-slate-300 font-extrabold text-xs mr-3 shrink-0 text-slate-500">${letter}</span>
                            <span class="text-xs sm:text-sm font-semibold text-slate-800 leading-snug">${optStr.replace(/^[A-D]\.\s*/, '')}</span>
                        </label>
                    `;
                    container.appendChild(wrapper);
                });
            }
            else if (q.tipe === "PGK_BS") {
                // Benar / Salah Table Grid
                const savedMap = (savedAns && typeof savedAns === 'object') ? savedAns : {};

                const table = document.createElement('div');
                table.className = "border border-slate-200 rounded-xl overflow-hidden text-xs shadow-sm bg-white";

                let rowsHtml = `
                    <div class="grid grid-cols-12 bg-slate-100 p-2.5 font-bold text-slate-600 border-b border-slate-200 text-[11px] uppercase tracking-wider">
                        <div class="col-span-8">Pernyataan</div>
                        <div class="col-span-2 text-center">Benar</div>
                        <div class="col-span-2 text-center">Salah</div>
                    </div>
                `;

                q.pernyataan.forEach((stmt, pIdx) => {
                    const val = savedMap[pIdx] || "";
                    const isB = val === "Benar";
                    const isS = val === "Salah";

                    rowsHtml += `
                        <div class="grid grid-cols-12 p-3 items-center border-b border-slate-100 hover:bg-slate-50 transition">
                            <div class="col-span-8 pr-2 font-medium text-slate-800 text-xs sm:text-sm leading-relaxed">${stmt}</div>
                            <div class="col-span-2 text-center">
                                <label class="inline-flex items-center cursor-pointer p-1">
                                    <input type="radio" name="bs-${q.nomor}-${pIdx}" value="Benar" ${isB ? 'checked' : ''} ${isLocked ? 'disabled' : ''} onchange="setBSAnswer(${q.nomor}, ${pIdx}, 'Benar')" class="w-4 h-4 text-emerald-600 focus:ring-emerald-500">
                                </label>
                            </div>
                            <div class="col-span-2 text-center">
                                <label class="inline-flex items-center cursor-pointer p-1">
                                    <input type="radio" name="bs-${q.nomor}-${pIdx}" value="Salah" ${isS ? 'checked' : ''} ${isLocked ? 'disabled' : ''} onchange="setBSAnswer(${q.nomor}, ${pIdx}, 'Salah')" class="w-4 h-4 text-rose-600 focus:ring-rose-500">
                                </label>
                            </div>
                        </div>
                    `;
                });

                table.innerHTML = rowsHtml;
                container.appendChild(table);
            }
        }

        function selectRadioAnswer(qNum, letter) {
            if (lockedSaved[qNum]) return;
            answersSaved[qNum] = letter;
            GameAudio.playClick();
            renderGridIndicators();
            updateProgressBar();
        }

        function toggleCheckboxAnswer(qNum, letter) {
            if (lockedSaved[qNum]) return;
            let current = answersSaved[qNum];
            if (!Array.isArray(current)) current = [];

            if (current.includes(letter)) {
                current = current.filter(x => x !== letter);
            } else {
                current.push(letter);
            }

            answersSaved[qNum] = current.sort();
            GameAudio.playClick();
            renderGridIndicators();
            updateProgressBar();
        }

        function setBSAnswer(qNum, pIdx, choice) {
            if (lockedSaved[qNum]) return;
            let current = answersSaved[qNum];
            if (!current || typeof current !== 'object') current = {};

            current[pIdx] = choice;
            answersSaved[qNum] = current;
            GameAudio.playClick();
            renderGridIndicators();
            updateProgressBar();
        }

        function toggleDoubtful() {
            const q = questions[currentQuestionIndex];
            if (lockedSaved[q.nomor]) return;

            doubtfulSaved[q.nomor] = !doubtfulSaved[q.nomor];
            GameAudio.playClick();
            showQuestion(currentQuestionIndex);
        }

        function goToQuestion(index) {
            if (index < 0 || index >= questions.length) return;
            GameAudio.playSlide();
            showQuestion(index);
        }

        function renderGridIndicators() {
            const grid = document.getElementById('student-grid-indicators');
            grid.innerHTML = "";

            questions.forEach((q, idx) => {
                const btn = document.createElement('button');
                const isCurrent = idx === currentQuestionIndex;
                const isLocked = lockedSaved[q.nomor] === true;
                const isDoubtful = doubtfulSaved[q.nomor] === true;
                const hasAnswer = isQuestionAnswered(q.nomor);

                let baseCls = "w-9 h-9 sm:w-10 sm:h-10 rounded-xl font-extrabold text-xs transition flex items-center justify-center relative ";

                if (isLocked) {
                    baseCls += "bg-rose-600 text-white shadow-sm border-2 border-rose-700";
                } else if (isDoubtful) {
                    baseCls += "bg-amber-500 text-white shadow-md border-2 border-amber-600";
                } else if (hasAnswer) {
                    baseCls += "bg-emerald-600 text-white shadow-md border-2 border-emerald-700";
                } else {
                    baseCls += "bg-slate-100 text-slate-700 border border-slate-300 hover:bg-slate-200";
                }

                if (isCurrent) {
                    baseCls += " ring-2 ring-brand-500 ring-offset-2 scale-105 z-10";
                }

                btn.className = baseCls;
                btn.innerHTML = isLocked ? `<i class="fa-solid fa-lock text-[10px]"></i>` : q.nomor;
                btn.onclick = () => goToQuestion(idx);

                grid.appendChild(btn);
            });
        }

        function isQuestionAnswered(qNum) {
            const ans = answersSaved[qNum];
            if (!ans) return false;
            if (Array.isArray(ans)) return ans.length > 0;
            if (typeof ans === 'object') return Object.keys(ans).length > 0;
            return true;
        }

        function updateProgressBar() {
            let answeredCount = 0;
            questions.forEach(q => {
                if (isQuestionAnswered(q.nomor)) answeredCount++;
            });

            const pct = Math.round((answeredCount / questions.length) * 100);
            document.getElementById('percent-quest-progress').innerText = `${pct}%`;
            document.getElementById('quest-progress-bar').style.width = `${pct}%`;
        }
    </script>

    <script>
        function confirmEndExam() {
            let unanswered = 0;
            questions.forEach(q => {
                if (!isQuestionAnswered(q.nomor)) unanswered++;
            });

            let msg = "Apakah Anda yakin ingin menyelesaikan dan mengirimkan seluruh jawaban ujian TKA?";
            if (unanswered > 0) {
                msg = `Masih terdapat <strong>${unanswered} soal</strong> yang belum dijawab. Yakin ingin mengakhiri sekarang?`;
            }

            showModal("Konfirmasi Kirim Ujian", msg, unanswered > 0 ? "warning" : "success", "Ya, Kirim Sekarang", "Batal", () => {
                forceEndExam();
            }, null);
        }

        function forceEndExam() {
            if (examTimerInterval) clearInterval(examTimerInterval);

            const now = new Date();
            const finishTimeStr = `${String(now.getHours()).padStart(2, '0')}:${String(now.getMinutes()).padStart(2, '0')}`;

            // Calculate Score
            let correctCount = 0;
            let incorrectCount = 0;

            questions.forEach(q => {
                const userAns = answersSaved[q.nomor];
                const key = q.jawaban;

                if (q.tipe === "PG") {
                    if (userAns === key) correctCount++;
                    else incorrectCount++;
                } 
                else if (q.tipe === "PGK_MCMA") {
                    // Check array match
                    if (Array.isArray(userAns) && Array.isArray(key)) {
                        const isMatch = userAns.length === key.length && userAns.every(v => key.includes(v));
                        if (isMatch) correctCount++;
                        else incorrectCount++;
                    } else {
                        incorrectCount++;
                    }
                }
                else if (q.tipe === "PGK_BS") {
                    // Check statement object match
                    if (userAns && typeof userAns === 'object' && Array.isArray(key)) {
                        let allCorrect = true;
                        key.forEach((expVal, idx) => {
                            if (userAns[idx] !== expVal) allCorrect = false;
                        });
                        if (allCorrect) correctCount++;
                        else incorrectCount++;
                    } else {
                        incorrectCount++;
                    }
                }
            });

            const finalScore = Number(((correctCount / questions.length) * 100).toFixed(2));

            const submissionData = {
                id: Date.now(),
                nama: activeStudent.nama,
                kelas: activeStudent.kelas,
                absen: parseInt(activeStudent.absen),
                jamMulai: examStartTimeStr,
                jamSelesai: finishTimeStr,
                benar: correctCount,
                salah: incorrectCount,
                skor: finalScore,
                detailJawaban: answersSaved
            };

            const submissions = JSON.parse(localStorage.getItem('tka_literasi_submissions') || '[]');
            submissions.push(submissionData);
            localStorage.setItem('tka_literasi_submissions', JSON.stringify(submissions));

            // Display Results Page
            document.getElementById('res-student-name').innerText = activeStudent.nama;
            document.getElementById('res-student-class').innerText = `${activeStudent.kelas} / ${activeStudent.absen}`;
            document.getElementById('res-total-correct').innerText = correctCount;
            document.getElementById('res-total-incorrect').innerText = incorrectCount;
            document.getElementById('res-final-score').innerText = finalScore.toFixed(2);

            GameAudio.playVictory();
            switchView('student-results');
        }
    </script>

    <script>
        function openTeacherLogin() {
            switchView('teacher-login');
        }

        function verifyTeacherLogin(e) {
            e.preventDefault();
            const pwd = document.getElementById('input-teacher-pwd').value;
            const err = document.getElementById('error-pwd-msg');

            if (pwd === CONFIG.TEACHER_PASSWORD) {
                err.classList.add('hidden');
                document.getElementById('input-teacher-pwd').value = "";
                switchView('teacher-dashboard');
                switchTeacherTab('tab-peserta');
            } else {
                err.classList.remove('hidden');
                GameAudio.playLockAlert();
            }
        }

        function switchTeacherTab(tabName) {
            GameAudio.playClick();
            const tabs = ['tab-peserta', 'tab-butir', 'tab-analisis', 'tab-matriks', 'tab-soal-editor'];
            
            tabs.forEach(t => {
                const subView = document.getElementById(`subview-${t}`);
                if (subView) subView.classList.add('hidden');

                const btn = document.getElementById(`btn-${t}`);
                if (btn) {
                    btn.className = "px-3 py-1.5 text-xs font-semibold rounded-lg text-slate-600 hover:bg-slate-100 transition";
                }
            });

            const targetSubView = document.getElementById(`subview-${tabName}`);
            if (targetSubView) targetSubView.classList.remove('hidden');

            const activeBtn = document.getElementById(`btn-${tabName}`);
            if (activeBtn) {
                activeBtn.className = "px-3 py-1.5 text-xs font-semibold rounded-lg bg-brand-600 text-white shadow-sm";
            }

            if (tabName === 'tab-peserta') renderTeacherPesertaTable();
            if (tabName === 'tab-butir') renderTeacherRekapButir();
            if (tabName === 'tab-analisis') renderTeacherAnalisis();
            if (tabName === 'tab-matriks') renderTeacherMatriks();
            if (tabName === 'tab-soal-editor') renderTeacherSoalEditor();
        }

        function renderTeacherPesertaTable() {
            const submissions = JSON.parse(localStorage.getItem('tka_literasi_submissions') || '[]');
            const tbody = document.getElementById('tbody-peserta-rows');
            tbody.innerHTML = "";

            if (submissions.length === 0) {
                tbody.innerHTML = `<tr><td colspan="10" class="text-center py-6 text-slate-400 font-medium">Belum ada peserta yang menyelesaikan ujian.</td></tr>`;
                document.getElementById('dash-stat-total').innerText = "0";
                document.getElementById('dash-stat-avg').innerText = "0.0";
                document.getElementById('dash-stat-max').innerText = "0";
                return;
            }

            const sortVal = document.getElementById('sort-filter-peserta').value;
            submissions.sort((a, b) => {
                if (sortVal === 'skor-desc') return b.skor - a.skor;
                if (sortVal === 'skor-asc') return a.skor - b.skor;
                if (sortVal === 'absen') return a.absen - b.absen;
                if (sortVal === 'nama') return a.nama.localeCompare(b.nama);
                return 0;
            });

            const totalScore = submissions.reduce((sum, s) => sum + s.skor, 0);
            const maxScore = Math.max(...submissions.map(s => s.skor));

            document.getElementById('dash-stat-total').innerText = submissions.length;
            document.getElementById('dash-stat-avg').innerText = (totalScore / submissions.length).toFixed(1);
            document.getElementById('dash-stat-max').innerText = maxScore.toFixed(0);

            submissions.forEach(sub => {
                const tr = document.createElement('tr');
                tr.className = "hover:bg-slate-50 border-b border-slate-100 transition";
                tr.innerHTML = `
                    <td class="px-6 py-3.5 font-bold text-slate-900">${sub.nama}</td>
                    <td class="px-6 py-3.5 text-slate-600">${sub.kelas}</td>
                    <td class="px-6 py-3.5 text-center font-bold text-slate-500">${sub.absen}</td>
                    <td class="px-6 py-3.5 text-slate-600">${sub.jamMulai || '-'}</td>
                    <td class="px-6 py-3.5 text-slate-600">${sub.jamSelesai || '-'}</td>
                    <td class="px-6 py-3.5 text-center font-bold text-emerald-600">${sub.benar}</td>
                    <td class="px-6 py-3.5 text-center font-bold text-rose-500">${sub.salah}</td>
                    <td class="px-6 py-3.5 text-center font-black text-brand-600 text-base">${sub.skor.toFixed(1)}</td>
                `;
                tbody.appendChild(tr);
            });
        }

        function renderTeacherRekapButir() {
            const container = document.getElementById('rekap-cards-container');
            container.innerHTML = "";

            questions.forEach(q => {
                const card = document.createElement('div');
                card.className = "bg-white border border-slate-200 rounded-2xl p-4 shadow-sm space-y-2 text-xs";

                let keyStr = q.jawaban;
                if (Array.isArray(keyStr)) keyStr = keyStr.join(", ");

                card.innerHTML = `
                    <div class="flex justify-between items-center border-b pb-2">
                        <span class="font-extrabold text-brand-600">Soal #${q.nomor} (${q.mapel})</span>
                        <span class="px-2 py-0.5 bg-slate-100 text-slate-600 rounded font-bold text-[10px]"><i class="fa-solid fa-clock"></i> ${q.waktuDetik || 180}s</span>
                    </div>
                    <p class="font-bold text-slate-800 line-clamp-2">${q.soal}</p>
                    <div class="p-2 bg-emerald-50 border border-emerald-100 rounded-lg text-emerald-900 font-bold">
                        Kunci Jawaban: <span class="text-emerald-700">${keyStr}</span>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        function renderTeacherAnalisis() {
            const submissions = JSON.parse(localStorage.getItem('tka_literasi_submissions') || '[]');
            const tbody = document.getElementById('tbody-analisis-rows');
            tbody.innerHTML = "";

            let stats = questions.map(q => ({
                nomor: q.nomor,
                waktu: q.waktuDetik || 180,
                tingkat: q.tingkat,
                benar: 0,
                salah: 0
            }));

            submissions.forEach(sub => {
                const det = sub.detailJawaban || {};
                questions.forEach((q, idx) => {
                    const uAns = det[q.nomor];
                    const key = q.jawaban;
                    let isRight = false;

                    if (q.tipe === "PG" && uAns === key) isRight = true;
                    if (q.tipe === "PGK_MCMA" && Array.isArray(uAns) && Array.isArray(key) && uAns.length === key.length && uAns.every(v => key.includes(v))) isRight = true;
                    if (q.tipe === "PGK_BS" && uAns && typeof uAns === 'object' && Array.isArray(key)) {
                        let all = true;
                        key.forEach((exp, pI) => { if (uAns[pI] !== exp) all = false; });
                        if (all) isRight = true;
                    }

                    if (isRight) stats[idx].benar++;
                    else stats[idx].salah++;
                });
            });

            // Render Chart.js
            const ctx = document.getElementById('analisisChart').getContext('2d');
            if (analysisChartInstance) analysisChartInstance.destroy();

            analysisChartInstance = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: questions.map(q => `S#${q.nomor}`),
                    datasets: [
                        { label: 'Benar', data: stats.map(s => s.benar), backgroundColor: '#059669' },
                        { label: 'Salah', data: stats.map(s => s.salah), backgroundColor: '#e11d48' }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: { y: { beginAtZero: true } }
                }
            });

            // Sort by difficulty (most incorrect first)
            stats.sort((a, b) => a.benar - b.benar);

            stats.forEach(st => {
                const total = st.benar + st.salah;
                const pctBenar = total > 0 ? ((st.benar / total) * 100).toFixed(1) : "0.0";
                const pctSalah = total > 0 ? ((st.salah / total) * 100).toFixed(1) : "0.0";

                const tr = document.createElement('tr');
                tr.className = "hover:bg-slate-50 border-b border-slate-100";
                tr.innerHTML = `
                    <td class="px-6 py-3 font-bold text-brand-950">Soal Nomor ${st.nomor}</td>
                    <td class="px-6 py-3 font-semibold text-slate-600">${st.tingkat}</td>
                    <td class="px-6 py-3 text-center font-mono">${st.waktu} dtk</td>
                    <td class="px-6 py-3 text-center font-bold text-emerald-600">${st.benar}</td>
                    <td class="px-6 py-3 text-center font-bold text-rose-500">${st.salah}</td>
                    <td class="px-6 py-3 text-center font-bold text-emerald-700">${pctBenar}%</td>
                    <td class="px-6 py-3 text-center font-bold text-rose-700">${pctSalah}%</td>
                `;
                tbody.appendChild(tr);
            });
        }

        function renderTeacherMatriks() {
            const submissions = JSON.parse(localStorage.getItem('tka_literasi_submissions') || '[]');
            const thead = document.getElementById('thead-matriks');
            const tbody = document.getElementById('tbody-matriks-rows');

            let headHtml = `<tr class="bg-slate-100 border-b border-slate-200 text-[10px] font-bold uppercase"><th class="p-2">Nama Siswa</th>`;
            questions.forEach(q => {
                headHtml += `<th class="p-2 text-center">S#${q.nomor}</th>`;
            });
            headHtml += `<th class="p-2 text-center">Skor</th></tr>`;
            thead.innerHTML = headHtml;

            tbody.innerHTML = "";
            if (submissions.length === 0) {
                tbody.innerHTML = `<tr><td colspan="${questions.length + 2}" class="text-center py-6 text-slate-400 font-medium">Belum ada data matriks.</td></tr>`;
                return;
            }

            submissions.forEach(sub => {
                const det = sub.detailJawaban || {};
                let rowHtml = `<tr class="border-b border-slate-100 hover:bg-slate-50"><td class="p-2 font-bold text-slate-900">${sub.nama}</td>`;

                questions.forEach(q => {
                    const uAns = det[q.nomor];
                    let disp = "-";
                    if (uAns) {
                        if (typeof uAns === 'string') disp = uAns;
                        else if (Array.isArray(uAns)) disp = uAns.join('');
                        else if (typeof uAns === 'object') disp = 'BS';
                    }
                    rowHtml += `<td class="p-2 text-center font-mono text-[11px]">${disp}</td>`;
                });

                rowHtml += `<td class="p-2 text-center font-bold text-brand-600">${sub.skor.toFixed(0)}</td></tr>`;
                tbody.innerHTML += rowHtml;
            });
        }

        function renderTeacherSoalEditor() {
            updateGateDisplayTime();
            const listContainer = document.getElementById('editor-soal-list');
            listContainer.innerHTML = "";

            questions.forEach((q, idx) => {
                const item = document.createElement('div');
                item.className = "p-3 sm:p-4 hover:bg-slate-50 transition flex items-center justify-between gap-3";

                item.innerHTML = `
                    <div class="space-y-1">
                        <div class="flex items-center gap-2">
                            <span class="px-2 py-0.5 bg-brand-100 text-brand-800 font-extrabold rounded text-[10px]">#${q.nomor}</span>
                            <span class="font-bold text-slate-900">${q.mapel}</span>
                            <span class="text-slate-400">•</span>
                            <span class="text-slate-500 font-semibold">${q.tingkat}</span>
                        </div>
                        <p class="text-slate-700 font-medium line-clamp-1">${q.soal}</p>
                    </div>

                    <div class="flex items-center gap-3 shrink-0">
                        <div class="text-right">
                            <span class="text-[9px] text-slate-400 block font-bold uppercase">Timer Soal</span>
                            <span class="font-mono font-extrabold text-amber-700 bg-amber-50 px-2 py-1 rounded border border-amber-200">${q.waktuDetik || 180} dtk</span>
                        </div>
                        <button onclick="editSoalForm(${idx})" class="p-2 text-brand-600 hover:bg-brand-50 rounded-lg font-bold text-xs"><i class="fa-solid fa-pen-to-square text-base"></i></button>
                    </div>
                `;
                listContainer.appendChild(item);
            });
        }

        function editSoalForm(idx) {
            const q = questions[idx];
            document.getElementById('soal-edit-index').value = idx;
            document.getElementById('edit-soal-nomor').value = q.nomor;
            document.getElementById('edit-soal-waktu').value = q.waktuDetik || 180;
            document.getElementById('edit-soal-mapel').value = q.mapel;
            document.getElementById('edit-soal-tingkat').value = q.tingkat;
            document.getElementById('edit-soal-tipe').value = q.tipe;
            document.getElementById('edit-soal-stimulus').value = Array.isArray(q.stimulus) ? q.stimulus.join('\n\n') : q.stimulus;
            document.getElementById('edit-soal-teks').value = q.soal;

            document.getElementById('editor-form-title').innerText = `Edit Soal & Timer No #${q.nomor}`;
            GameAudio.playClick();
        }

        function clearEditorForm() {
            document.getElementById('soal-edit-index').value = "";
            document.getElementById('form-edit-soal').reset();
            document.getElementById('editor-form-title').innerText = "Edit Timer & Data Soal";
        }

        function saveSoalItem(e) {
            e.preventDefault();
            const idxStr = document.getElementById('soal-edit-index').value;
            if (idxStr === "") {
                showModal("Pilih Soal", "Silakan klik tombol edit pada salah satu daftar soal.", "warning", "Oke", "Batal", null, null);
                return;
            }

            const idx = parseInt(idxStr);
            questions[idx].nomor = parseInt(document.getElementById('edit-soal-nomor').value);
            questions[idx].waktuDetik = parseInt(document.getElementById('edit-soal-waktu').value);
            questions[idx].mapel = document.getElementById('edit-soal-mapel').value;
            questions[idx].tingkat = document.getElementById('edit-soal-tingkat').value;
            questions[idx].soal = document.getElementById('edit-soal-teks').value;

            const stimText = document.getElementById('edit-soal-stimulus').value;
            questions[idx].stimulus = stimText.split('\n\n').filter(p => p.trim() !== '');

            localStorage.setItem('tka_matematika_questions', JSON.stringify(questions));
            clearEditorForm();
            renderTeacherSoalEditor();
            showToast("Data soal dan timer berhasil diperbarui!");
        }

        function resetQuestionsToDefault() {
            showModal("Reset Soal?", "Apakah Anda yakin ingin mengembalikan seluruh soal ke standar awal 25 Soal Matematika?", "danger", "Ya, Reset", "Batal", () => {
                questions = JSON.parse(JSON.stringify(DEFAULT_MATHEMATICS_QUESTIONS));
                localStorage.setItem('tka_matematika_questions', JSON.stringify(questions));
                renderTeacherSoalEditor();
                showToast("Soal berhasil di-reset ke standar awal!");
            }, null);
        }

        function clearAllData() {
            showModal("Reset Seluruh Data?", "Ini akan menghapus seluruh data hasil jawaban siswa dan mengembalikan pengaturan awal.", "danger", "Ya, Hapus Semua", "Batal", () => {
                localStorage.removeItem('tka_literasi_submissions');
                localStorage.removeItem('tka_matematika_questions');
                localStorage.removeItem('tka_total_exam_time_minutes');
                loadQuestions();
                updateGateDisplayTime();
                renderTeacherPesertaTable();
                showToast("Seluruh data pengerjaan berhasil dibersihkan!");
            }, null);
        }
    </script>
</body>
</html>
