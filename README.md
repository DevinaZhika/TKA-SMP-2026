<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CBT TKA SMP</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts Inter & Plus Jakarta Sans -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
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
                        heading: ['Plus Jakarta Sans', 'sans-serif'],
                    },
                    colors: {
                        brand: {
                            50: '#f0f3ff',
                            100: '#e1e7fe',
                            200: '#cbd5fe',
                            300: '#a5b4fc',
                            400: '#818cf8',
                            500: '#6366f1',
                            600: '#4f46e5', // Indigo Accent
                            700: '#4338ca', 
                            800: '#3730a3',
                            950: '#0f172a', // Deep Slate Dark
                        },
                        vibrant: {
                            cyan: '#06b6d4',
                            emerald: '#10b981',
                            rose: '#f43f5e',
                            amber: '#f59e0b'
                        }
                    },
                    boxShadow: {
                        'glow': '0 0 15px -3px rgba(99, 102, 241, 0.3)',
                        'premium': '0 20px 25px -5px rgba(15, 23, 42, 0.05), 0 8px 10px -6px rgba(15, 23, 42, 0.05)',
                    }
                }
            }
        }
    </script>
    <style>
        /* Modern Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f5f9;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 99px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #a5b4fc;
        }
        
        /* Interactive Highlight styles (Pure yellow highlight, no brackets or margins) */
        .highlighted-text {
            background-color: #fef08a !important; /* Tailwind yellow-200 */
            color: #1e1b4b !important;
            padding: 0px 2px !important;
            border-radius: 0px !important;
            box-shadow: none !important;
            border: none !important;
        }
        
        /* Reading Ruler Focus Overlay */
        .ruler-focus-active .reading-stimulus p:not(.focused-line) {
            opacity: 0.15;
            filter: blur(1.5px);
            transition: all 0.25s ease;
        }
        .reading-stimulus p {
            transition: all 0.25s ease;
            cursor: pointer;
            border-left: 3px solid transparent;
            padding-left: 8px;
        }
        .reading-stimulus p:hover {
            background-color: #f8fafc;
            border-left-color: #cbd5fe;
        }
        .focused-line {
            border-left-color: #6366f1 !important;
            background-color: #f0f3ff !important;
            font-weight: 500;
            color: #1e1b4b !important;
            opacity: 1 !important;
            filter: none !important;
            transform: scale(1.01);
        }

        /* Option box unchecked custom focus styling */
        .option-card input[type="radio"]:checked + label {
            border-color: #6366f1;
            background-color: #f0f3ff;
            color: #3730a3;
            font-weight: 600;
            box-shadow: 0 4px 12px -1px rgba(99, 102, 241, 0.15);
        }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 font-sans min-h-screen flex flex-col justify-between">

    <!-- HEADER BAR -->
    <header class="bg-gradient-to-r from-brand-950 via-indigo-950 to-slate-900 border-b border-indigo-900 sticky top-0 z-40 shadow-md">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center gap-3">
                <div class="bg-gradient-to-tr from-brand-500 to-vibrant-cyan text-white p-2.5 rounded-xl flex items-center justify-center shadow-lg shadow-indigo-500/20">
                    <i class="fa-solid fa-graduation-cap text-lg"></i>
                </div>
                <div>
                    <h1 class="font-heading font-extrabold text-sm sm:text-base text-white tracking-wide">CBT TKA SMP</h1>
                </div>
            </div>
            
            <div class="flex items-center gap-2">
                <button onclick="switchView('student-gate')" id="tab-student" class="px-3 py-1.5 text-xs sm:text-sm font-semibold rounded-lg transition-all duration-200 bg-brand-600 text-white shadow-md flex items-center gap-1.5">
                    <i class="fa-solid fa-user-pen"></i> <span>Siswa</span>
                </button>
                <button onclick="openTeacherLogin()" id="tab-teacher" class="px-3 py-1.5 text-xs sm:text-sm font-semibold rounded-lg transition-all duration-200 text-brand-200 hover:text-white hover:bg-white/10 flex items-center gap-1.5">
                    <i class="fa-solid fa-user-tie"></i> <span>Portal Guru</span>
                </button>
            </div>
        </div>
    </header>

    <!-- MAIN CONTENT -->
    <main class="flex-grow max-w-7xl w-full mx-auto p-4 sm:p-6 lg:p-8">

        <!-- STUDENT LOG GATEWAY -->
        <div id="view-student-gate" class="max-w-md mx-auto my-8 bg-white rounded-3xl border border-indigo-50 p-6 sm:p-8 shadow-premium transition-all">
            <div class="text-center mb-8">
                <div class="inline-flex p-4 bg-brand-50 text-brand-600 rounded-3xl mb-4 shadow-inner">
                    <i class="fa-solid fa-brain text-4xl"></i>
                </div>
                <h2 class="font-heading font-extrabold text-2xl text-brand-950">Tes Kemampuan Akademik</h2>
            </div>

            <form id="form-login-siswa" onsubmit="startExam(event)" class="space-y-5">
                <div>
                    <label class="block text-xs font-bold uppercase text-slate-400 mb-1.5 tracking-wider" for="input-nama">Nama Lengkap</label>
                    <div class="relative">
                        <span class="absolute inset-y-0 left-0 flex items-center pl-3.5 text-slate-400">
                            <i class="fa-solid fa-user text-sm"></i>
                        </span>
                        <input type="text" id="input-nama" required class="w-full pl-10 pr-4 py-2.5 border border-slate-200 rounded-xl focus:ring-2 focus:ring-brand-500 focus:border-brand-500 text-sm font-medium transition" placeholder="Contoh: Andi Wijaya">
                    </div>
                </div>
                <div class="grid grid-cols-2 gap-4">
                    <div>
                        <label class="block text-xs font-bold uppercase text-slate-400 mb-1.5 tracking-wider" for="input-kelas">Kelas</label>
                        <select id="input-kelas" required class="w-full px-3.5 py-2.5 border border-slate-200 rounded-xl focus:ring-2 focus:ring-brand-500 focus:border-brand-500 text-sm font-medium bg-white transition">
                            <option value="">Pilih...</option>
                            <option value="9A">Kelas 9A</option>
                            <option value="9B">Kelas 9B</option>
                            <option value="9C">Kelas 9C</option>
                            <option value="9D">Kelas 9D</option>
                            <option value="9E">Kelas 9E</option>
                            <option value="9F">Kelas 9F</option>
                            <option value="9G">Kelas 9G</option>
                            <option value="9H">Kelas 9H</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-xs font-bold uppercase text-slate-400 mb-1.5 tracking-wider" for="input-absen">Nomor Absen</label>
                        <div class="relative">
                            <span class="absolute inset-y-0 left-0 flex items-center pl-3.5 text-slate-400">
                                <i class="fa-solid fa-hashtag text-sm"></i>
                            </span>
                            <input type="number" id="input-absen" min="1" max="45" required class="w-full pl-10 pr-4 py-2.5 border border-slate-200 rounded-xl focus:ring-2 focus:ring-brand-500 text-sm font-medium transition" placeholder="1">
                        </div>
                    </div>
                </div>

                <div class="p-4 bg-brand-50/50 border border-indigo-100 rounded-2xl text-xs text-brand-900 space-y-1.5">
                    <div class="font-bold flex items-center gap-2 text-brand-800">
                        <i class="fa-solid fa-circle-info text-brand-600"></i> Petunjuk:
                    </div>
                    <p class="leading-relaxed text-slate-600">
                        Gunakan tombol bantuan <strong class="text-brand-700">Stabilo</strong> dan <strong class="text-brand-700">Mistar Fokus</strong> di atas kertas soal digital untuk mempermudah teknik membaca cepat (*skimming & scanning*).
                    </p>
                </div>

                <button type="submit" class="w-full py-3.5 px-4 bg-gradient-to-r from-brand-600 to-indigo-600 hover:from-brand-700 hover:to-indigo-700 text-white font-semibold rounded-xl shadow-lg shadow-indigo-600/20 hover:shadow-xl transition-all duration-200 flex items-center justify-center gap-2 text-sm">
                    Mulai Ujian <i class="fa-solid fa-arrow-right-to-bracket"></i>
                </button>
            </form>
        </div>

        <!-- CBT STUDENT EXAM VIEW (SPLIT SCREEN LAYOUT) -->
        <div id="view-student-exam" class="hidden flex flex-col gap-4">
            
            <!-- Top Bar Panel: Timer, Profil & Toolbar -->
            <div class="bg-white border border-slate-150 rounded-2xl p-4 shadow-sm flex flex-col sm:flex-row gap-4 items-center justify-between">
                <div class="flex items-center gap-3">
                    <div class="bg-indigo-50/70 border border-indigo-100 px-4 py-2 rounded-xl text-xs">
                        <span class="text-indigo-400 block font-bold uppercase text-[9px] tracking-wider">Siswa Terdaftar</span>
                        <strong id="display-student-name" class="text-brand-950 text-sm">Siswa</strong>
                        <span class="text-indigo-600 ml-1 font-semibold">(Kelas <span id="display-student-class">9A</span> / <span id="display-student-absen">01</span>)</span>
                    </div>
                </div>

                <!-- TOOLBAR ALAT BANTU LITERASI -->
                <div class="flex flex-wrap items-center gap-2 bg-slate-50 p-2 rounded-xl border border-slate-200">
                    <span class="text-[10px] font-bold text-slate-400 px-2 uppercase tracking-wide">Bantuan Membaca Cepat:</span>
                    <button onclick="toggleHighlighter()" id="btn-highlighter" class="px-3 py-1.5 text-xs font-semibold rounded-lg bg-white border text-slate-700 hover:bg-indigo-50 flex items-center gap-1.5 transition">
                        <i class="fa-solid fa-marker text-brand-500"></i> Stabilo Teks
                    </button>
                    <button onclick="toggleReadingRuler()" id="btn-ruler" class="px-3 py-1.5 text-xs font-semibold rounded-lg bg-white border text-slate-700 hover:bg-indigo-50 flex items-center gap-1.5 transition">
                        <i class="fa-solid fa-grip-lines text-brand-500"></i> Mistar Fokus
                    </button>
                    <button onclick="toggleScratchpad()" class="px-3 py-1.5 text-xs font-semibold rounded-lg bg-white border text-slate-700 hover:bg-indigo-50 flex items-center gap-1.5 transition">
                        <i class="fa-solid fa-feather-pointed text-brand-500"></i> Papan Coretan
                    </button>
                </div>

                <div class="flex items-center gap-3">
                    <div class="text-right">
                        <span class="text-[9px] text-slate-400 block font-bold uppercase tracking-wider">Sisa Waktu</span>
                        <div id="exam-timer" class="text-base font-mono font-bold text-vibrant-rose animate-pulse">02:00:00</div>
                    </div>
                </div>
            </div>

            <!-- Main Workspace: Split Screen -->
            <div class="grid grid-cols-1 lg:grid-cols-12 gap-4">
                
                <!-- STIMULUS PANEL (Kiri: Berisi Teks Bacaan Panjang, Tabel, Grafik) -->
                <div id="panel-stimulus" class="lg:col-span-6 bg-white border border-slate-200 rounded-2xl p-6 shadow-sm flex flex-col justify-between max-h-[600px] overflow-y-auto">
                    <div>
                        <div class="flex items-center justify-between border-b border-slate-100 pb-3 mb-4">
                            <span class="text-xs font-bold text-brand-500 uppercase tracking-wider"><i class="fa-solid fa-file-invoice"></i> Teks Stimulus Kasus</span>
                            <span class="text-[10px] bg-indigo-50 text-indigo-700 px-2.5 py-1 rounded-full font-bold">Standard TKA / HOTS</span>
                        </div>
                        
                        <!-- Content Teks Stimulus -->
                        <div id="display-stimulus-container" class="reading-stimulus text-slate-700 text-sm sm:text-base space-y-4 leading-relaxed">
                            <!-- Rendered dynamically -->
                        </div>
                    </div>
                </div>

                <!-- QUESTION & OPTIONS PANEL (Kanan: Butir pertanyaan & Opsi Jawaban) -->
                <div id="panel-soal" class="lg:col-span-6 bg-white border border-slate-200 rounded-2xl p-6 shadow-sm flex flex-col justify-between min-h-[450px]">
                    <div>
                        <div class="flex items-center justify-between border-b border-slate-100 pb-3 mb-5">
                            <span class="px-3 py-1 bg-brand-50 text-brand-700 text-xs font-bold rounded-lg" id="display-mapel">
                                Matematika
                            </span>
                            <span class="text-xs font-semibold text-slate-500">
                                Soal <strong id="current-question-num" class="text-brand-600">1</strong> dari <span id="total-questions-num">5</span>
                            </span>
                        </div>

                        <!-- Question Text (No Yellow Highlight) -->
                        <div class="space-y-5">
                            <p id="display-soal-text" class="text-brand-950 font-bold text-sm sm:text-base leading-relaxed">
                                Loading soal...
                            </p>

                            <!-- Radio Options Cards Wrapper -->
                            <div id="display-opsi-container" class="grid grid-cols-1 gap-3">
                                <!-- Rendered dynamically -->
                            </div>
                        </div>
                    </div>

                    <!-- Action Buttons -->
                    <div class="mt-6 pt-4 border-t border-slate-100 flex items-center justify-between gap-2">
                        <button id="btn-prev-question" onclick="goToQuestion(currentQuestionIndex - 1)" class="px-3 sm:px-4 py-2.5 text-xs font-bold text-slate-600 bg-slate-100 hover:bg-slate-200 rounded-xl flex items-center gap-1.5 transition">
                            <i class="fa-solid fa-chevron-left"></i> Sebelumnya
                        </button>
                        
                        <!-- Ragu-ragu Toggle Button -->
                        <button id="btn-doubtful-toggle" onclick="toggleDoubtful()" class="px-4 py-2.5 text-xs font-bold rounded-xl flex items-center justify-center gap-1.5 transition border border-amber-300 bg-amber-50 text-amber-700 hover:bg-amber-100">
                            <i class="fa-regular fa-square"></i> Ragu-Ragu
                        </button>

                        <button id="btn-next-question" onclick="goToQuestion(currentQuestionIndex + 1)" class="px-3 sm:px-4 py-2.5 text-xs font-bold text-white bg-brand-600 hover:bg-brand-700 rounded-xl flex items-center gap-1.5 transition shadow">
                            Selanjutnya <i class="fa-solid fa-chevron-right"></i>
                        </button>

                        <button id="btn-finish-exam" onclick="confirmEndExam()" class="hidden px-5 sm:px-6 py-2.5 text-xs font-bold text-white bg-vibrant-emerald hover:bg-emerald-600 rounded-xl flex items-center gap-1.5 transition shadow-md">
                            <i class="fa-solid fa-paper-plane"></i> Selesai
                        </button>
                    </div>
                </div>

            </div>

            <!-- Bottom Indicator Navigation Panel -->
            <div class="bg-white border border-slate-200 rounded-2xl p-5 shadow-sm">
                <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-3 mb-3">
                    <h4 class="font-heading font-bold text-xs text-brand-950 uppercase tracking-widest">Navigasi Lembar Jawab Cepat</h4>
                    <div class="flex flex-wrap items-center gap-4 text-[10px] font-bold uppercase tracking-wider">
                        <div class="flex items-center gap-1.5"><span class="w-3.5 h-3.5 rounded bg-slate-100 border border-slate-200 inline-block"></span> Belum Terjawab</div>
                        <div class="flex items-center gap-1.5"><span class="w-3.5 h-3.5 rounded bg-emerald-600 inline-block"></span> Sudah Terjawab</div>
                        <div class="flex items-center gap-1.5"><span class="w-3.5 h-3.5 rounded bg-amber-500 inline-block"></span> Ragu-Ragu</div>
                    </div>
                </div>
                <div id="student-grid-indicators" class="flex flex-wrap gap-2">
                    <!-- Dynamic generated grid -->
                </div>
            </div>

        </div>

        <!-- INTERACTIVE SCRATCHPAD FLOATING PANEL -->
        <div id="scratchpad-panel" class="hidden fixed right-4 bottom-4 z-50 bg-white border border-brand-100 w-80 rounded-2xl shadow-2xl p-4 space-y-3">
            <div class="flex items-center justify-between border-b pb-2">
                <span class="text-xs font-bold text-brand-950 uppercase"><i class="fa-solid fa-feather-pointed text-brand-500"></i> Papan Coretan Digital</span>
                <button onclick="toggleScratchpad()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
            </div>
            
            <!-- Simple Memo pad -->
            <div>
                <label class="block text-[10px] uppercase font-bold text-slate-400 mb-1">Coretan / Catatan Membaca</label>
                <textarea id="scratchpad-text" rows="8" class="w-full text-xs p-3 border border-slate-200 rounded-xl focus:ring-2 focus:ring-brand-500 focus:outline-none" placeholder="Tuliskan analisis hitungan atau rangkuman data bacaan Anda di sini agar tidak lupa..."></textarea>
            </div>
        </div>

        <!-- STUDENT SCORE SCREEN -->
        <div id="view-student-results" class="hidden max-w-lg mx-auto bg-white border border-brand-50 rounded-3xl p-6 sm:p-8 shadow-premium transition-all">
            <div class="text-center mb-6">
                <div class="inline-flex p-4 bg-brand-50 text-brand-600 rounded-full mb-4 shadow-inner">
                    <i class="fa-solid fa-square-poll-vertical text-4xl"></i>
                </div>
                <h2 class="font-heading font-extrabold text-2xl text-brand-950">Ujian Telah Selesai!</h2>
                <p class="text-slate-500 text-xs mt-1">Hasil ujian Anda telah berhasil direkam ke database utama secara aman.</p>
            </div>

            <!-- Identity Display Block -->
            <div class="bg-slate-50 rounded-2xl p-4 border border-slate-100 mb-6 space-y-2">
                <div class="flex justify-between text-xs">
                    <span class="text-slate-500">Nama Siswa</span>
                    <strong id="res-student-name" class="text-brand-950">Andi</strong>
                </div>
                <div class="flex justify-between text-xs">
                    <span class="text-slate-500">Kelas / Absen</span>
                    <strong id="res-student-class" class="text-brand-950">9A / 12</strong>
                </div>
            </div>

            <!-- Pure Score Board -->
            <div class="bg-brand-50/50 border border-indigo-100 rounded-2xl p-5 text-center space-y-4 shadow-inner mb-6">
                <p class="text-brand-800 text-xs uppercase tracking-widest font-extrabold">Hasil Ujian Kompetensi</p>
                
                <div class="grid grid-cols-2 gap-4 border-b border-indigo-100 pb-4">
                    <div>
                        <span class="text-[11px] text-indigo-500 font-semibold uppercase">Benar</span>
                        <div id="res-total-correct" class="text-2xl font-black text-emerald-600">0</div>
                    </div>
                    <div>
                        <span class="text-[11px] text-indigo-500 font-semibold uppercase">Salah</span>
                        <div id="res-total-incorrect" class="text-2xl font-black text-vibrant-rose">0</div>
                    </div>
                </div>

                <div>
                    <span class="text-[11px] text-indigo-500 font-semibold uppercase block mb-1">Skor Akhir</span>
                    <div id="res-final-score" class="text-6xl font-black text-brand-600 tracking-tight">00.00</div>
                </div>
            </div>

            <div class="p-3 bg-slate-50 border border-slate-200 rounded-xl text-xs text-slate-500 text-center flex items-center justify-center gap-1.5">
                <i class="fa-solid fa-lock text-slate-400"></i> Kunci jawaban dan pembahasan tidak dipublikasikan untuk menjaga objektivitas tes.
            </div>
        </div>

        <!-- TEACHER AUTHENTICATION BARRIER -->
        <div id="view-teacher-login" class="hidden max-w-sm mx-auto my-12 bg-white border border-slate-200 rounded-3xl p-6 shadow-premium">
            <div class="text-center mb-6">
                <div class="inline-flex p-3 bg-indigo-50 text-brand-600 rounded-2xl mb-2">
                    <i class="fa-solid fa-user-shield text-2xl"></i>
                </div>
                <h3 class="font-heading font-bold text-lg text-brand-950">Portal Keamanan Guru</h3>
                <p class="text-slate-500 text-xs">Masukkan kata sandi guru untuk mengakses dashboard.</p>
            </div>
            
            <form onsubmit="verifyTeacherLogin(event)" class="space-y-4">
                <div>
                    <input type="password" id="input-teacher-pwd" class="w-full px-4 py-2.5 border border-slate-200 rounded-xl focus:ring-2 focus:ring-brand-500 text-sm text-center font-mono" placeholder="Password Guru" required>
                </div>
                <p id="error-pwd-msg" class="text-vibrant-rose text-xs text-center font-semibold hidden"><i class="fa-solid fa-circle-exclamation"></i> Password salah, coba lagi!</p>
                <div class="p-2.5 bg-slate-50 border rounded-xl text-[10px] text-slate-500 text-center">
                    Password standar guru: <strong class="font-mono bg-white px-1 py-0.5 rounded border">adminTKA2026</strong>
                </div>
                <button type="submit" class="w-full py-2.5 bg-brand-950 hover:bg-slate-900 text-white font-semibold rounded-xl text-sm transition-all duration-150">
                    Masuk ke Dashboard
                </button>
            </form>
        </div>

        <!-- TEACHER DASHBOARD VIEW (COMPREHENSIVE) -->
        <div id="view-teacher-dashboard" class="hidden space-y-6">
            
            <!-- Dashboard Subheader Menu -->
            <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between border-b border-slate-200 pb-4 gap-4">
                <div>
                    <h2 class="font-heading font-extrabold text-xl text-brand-950">Dashboard Analisis & Monitor Guru</h2>
                    <p class="text-slate-500 text-xs">Pantau hasil analisis butir soal, matriks jawaban, dan tingkat kesulitan soal.</p>
                </div>
                <div class="flex flex-wrap items-center gap-2">
                    <button onclick="switchTeacherTab('tab-peserta')" id="btn-tab-peserta" class="px-3 py-1.5 text-xs font-semibold rounded-lg bg-brand-600 text-white shadow-sm">Daftar Peserta</button>
                    <button onclick="switchTeacherTab('tab-butir')" id="btn-tab-butir" class="px-3 py-1.5 text-xs font-semibold rounded-lg text-slate-600 hover:bg-slate-100 transition">Rekap Soal</button>
                    <button onclick="switchTeacherTab('tab-analisis')" id="btn-tab-analisis" class="px-3 py-1.5 text-xs font-semibold rounded-lg text-slate-600 hover:bg-slate-100 transition">Analisis Soal</button>
                    <button onclick="switchTeacherTab('tab-matriks')" id="btn-tab-matriks" class="px-3 py-1.5 text-xs font-semibold rounded-lg text-slate-600 hover:bg-slate-100 transition">Matriks Jawaban</button>
                    <button onclick="switchTeacherTab('tab-soal-editor')" id="btn-tab-soal" class="px-3 py-1.5 text-xs font-semibold rounded-lg text-brand-600 hover:bg-brand-50 transition">Atur Soal</button>
                    <button onclick="clearAllData()" class="px-2.5 py-1.5 text-xs font-bold text-vibrant-rose hover:bg-rose-50 rounded-lg ml-auto sm:ml-0 transition"><i class="fa-solid fa-trash-can"></i> Reset</button>
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
                        <div class="p-2.5 bg-indigo-50 text-brand-600 rounded-xl text-lg"><i class="fa-solid fa-users"></i></div>
                    </div>
                    <div class="bg-white border border-slate-200 p-4 rounded-2xl shadow-sm flex items-center justify-between">
                        <div>
                            <span class="text-[10px] text-slate-400 font-bold uppercase tracking-wider">Rata-Rata Skor</span>
                            <div id="dash-stat-avg" class="text-2xl font-extrabold text-brand-950">0.0</div>
                        </div>
                        <div class="p-2.5 bg-blue-50 text-indigo-600 rounded-xl text-lg"><i class="fa-solid fa-chart-simple"></i></div>
                    </div>
                    <div class="bg-white border border-slate-200 p-4 rounded-2xl shadow-sm flex items-center justify-between">
                        <div>
                            <span class="text-[10px] text-slate-400 font-bold uppercase tracking-wider">Skor Tertinggi</span>
                            <div id="dash-stat-max" class="text-2xl font-extrabold text-emerald-600">0</div>
                        </div>
                        <div class="p-2.5 bg-emerald-50 text-emerald-600 rounded-xl text-lg"><i class="fa-solid fa-trophy"></i></div>
                    </div>
                </div>

                <div class="bg-white border border-slate-200 rounded-2xl overflow-hidden shadow-sm">
                    <div class="px-5 py-4 border-b border-slate-100 flex items-center justify-between">
                        <h3 class="font-heading font-bold text-brand-950 text-sm">Urutan Prestasi Peserta</h3>
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
                                    <th class="px-6 py-3">Jam Mulai</th>
                                    <th class="px-6 py-3">Jam Selesai</th>
                                    <th class="px-6 py-3 text-center">Durasi</th>
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
                <div class="p-3 bg-brand-50 border border-indigo-100 rounded-xl flex items-center gap-2 text-xs text-brand-900 font-semibold">
                    <i class="fa-solid fa-circle-info text-brand-600"></i>
                    Informasi mengenai distribusi pilihan jawaban siswa (A, B, C, D) untuk mendeteksi keefektifan opsi pengecoh (*distractor analysis*).
                </div>
                <div id="rekap-cards-container" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
                    <!-- Dynamic question stats cards -->
                </div>
            </div>

            <!-- TEACHER TAB: ANALISIS SOAL (DIFFICULTY RATING + CHART) -->
            <div id="subview-tab-analisis" class="hidden space-y-6">
                <!-- Bar Chart Wrapper -->
                <div class="bg-white border border-slate-200 rounded-2xl p-5 shadow-sm">
                    <h3 class="font-heading font-bold text-brand-950 text-sm mb-3">Grafik Distribusi Jawaban Benar & Salah Per Soal</h3>
                    <div class="h-64 w-full relative">
                        <canvas id="analisisChart"></canvas>
                    </div>
                </div>

                <!-- Difficulty analysis table sorted from hardest -->
                <div class="bg-white border border-slate-200 rounded-2xl overflow-hidden shadow-sm">
                    <div class="px-5 py-4 border-b border-slate-100">
                        <h3 class="font-heading font-bold text-brand-950 text-sm">Urutan Tingkat Kesulitan Soal</h3>
                        <p class="text-[10px] text-slate-400 mt-0.5">Daftar soal diurutkan otomatis dari soal dengan **persentase salah terbanyak (paling sulit/butuh intervensi guru)** hingga paling mudah.</p>
                    </div>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left border-collapse text-xs sm:text-sm">
                            <thead>
                                <tr class="bg-slate-50 border-b border-slate-100 text-slate-500 text-[10px] font-bold uppercase tracking-wider">
                                    <th class="px-6 py-3">No Soal</th>
                                    <th class="px-6 py-3">Mata Pelajaran</th>
                                    <th class="px-6 py-3 text-center">Jumlah Benar</th>
                                    <th class="px-6 py-3 text-center">Jumlah Salah</th>
                                    <th class="px-6 py-3 text-center">Persentase Benar</th>
                                    <th class="px-6 py-3 text-center">Persentase Salah</th>
                                    <th class="px-6 py-3">Tingkat Kesulitan</th>
                                </tr>
                            </thead>
                            <tbody id="tbody-analisis-rows" class="divide-y divide-slate-100">
                                <!-- Dynamic rows -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- TEACHER TAB: MATRIKS REKAP JAWABAN SISWA -->
            <div id="subview-tab-matriks" class="hidden space-y-4">
                <div class="bg-white border border-slate-200 rounded-2xl overflow-hidden shadow-sm">
                    <div class="px-5 py-4 border-b border-slate-100 flex items-center justify-between">
                        <div>
                            <h3 class="font-heading font-bold text-brand-950 text-sm">Matriks Lembar Jawab Seluruh Siswa</h3>
                            <p class="text-[10px] text-slate-400 mt-0.5">Jawaban benar ditandai dengan tanda centang kecil (<span class="text-emerald-600 font-bold">✔</span>) untuk memudahkan analisis kualitatif.</p>
                        </div>
                    </div>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left border-collapse text-xs">
                            <thead id="thead-matriks">
                                <!-- Dynamic table headers based on count -->
                            </thead>
                            <tbody id="tbody-matriks-rows" class="divide-y divide-slate-100">
                                <!-- Dynamic rows of students answers -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- TEACHER TAB: SOAL EDITOR (JSON MANAGEMENT) -->
            <div id="subview-tab-soal-editor" class="hidden space-y-6">
                <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
                    <!-- Form Tambah/Ubah Soal -->
                    <div class="lg:col-span-4 bg-white border border-slate-200 p-5 rounded-2xl shadow-sm space-y-4">
                        <h3 class="font-heading font-bold text-brand-950 text-sm" id="editor-form-title">Tambah/Edit Soal</h3>
                        <form id="form-edit-soal" onsubmit="saveSoalItem(event)" class="space-y-3 text-xs">
                            <input type="hidden" id="soal-edit-index" value="">
                            <div>
                                <label class="block font-bold text-slate-400 uppercase mb-1">Nomor Soal</label>
                                <input type="number" id="edit-soal-nomor" required class="w-full px-3 py-1.5 border border-slate-200 rounded-lg focus:ring-1 focus:ring-brand-500 focus:outline-none">
                            </div>
                            <div>
                                <label class="block font-bold text-slate-400 uppercase mb-1">Mata Pelajaran</label>
                                <input type="text" id="edit-soal-mapel" placeholder="Matematika / IPA / dll." required class="w-full px-3 py-1.5 border border-slate-200 rounded-lg focus:ring-1 focus:ring-brand-500 focus:outline-none">
                            </div>
                            <div>
                                <label class="block font-bold text-slate-400 uppercase mb-1">Stimulus / Bacaan Pendukung</label>
                                <textarea id="edit-soal-stimulus" rows="4" required class="w-full px-3 py-1.5 border border-slate-200 rounded-lg focus:ring-1 focus:ring-brand-500 focus:outline-none" placeholder="Ketik narasi/kasus teks panjang pendukung di sini... (Pisahkan paragraf dengan enter)"></textarea>
                            </div>
                            <div>
                                <label class="block font-bold text-slate-400 uppercase mb-1">Pertanyaan / Butir Soal</label>
                                <textarea id="edit-soal-teks" rows="3" required class="w-full px-3 py-1.5 border border-slate-200 rounded-lg focus:ring-1 focus:ring-brand-500 focus:outline-none" placeholder="Ketik butir soal..."></textarea>
                            </div>
                            <div class="space-y-1.5">
                                <label class="block font-bold text-slate-400 uppercase">Opsi Jawaban (A, B, C, D)</label>
                                <input type="text" id="edit-soal-opsiA" required class="w-full px-3 py-1.5 border border-slate-200 rounded-lg focus:ring-1 focus:ring-brand-500 focus:outline-none" placeholder="Opsi A">
                                <input type="text" id="edit-soal-opsiB" required class="w-full px-3 py-1.5 border border-slate-200 rounded-lg focus:ring-1 focus:ring-brand-500 focus:outline-none" placeholder="Opsi B">
                                <input type="text" id="edit-soal-opsiC" required class="w-full px-3 py-1.5 border border-slate-200 rounded-lg focus:ring-1 focus:ring-brand-500 focus:outline-none" placeholder="Opsi C">
                                <input type="text" id="edit-soal-opsiD" required class="w-full px-3 py-1.5 border border-slate-200 rounded-lg focus:ring-1 focus:ring-brand-500 focus:outline-none" placeholder="Opsi D">
                            </div>
                            <div>
                                <label class="block font-bold text-slate-400 uppercase mb-1">Jawaban Benar</label>
                                <select id="edit-soal-jawaban" required class="w-full px-3 py-1.5 border border-slate-200 rounded-lg bg-white focus:ring-1 focus:ring-brand-500 focus:outline-none">
                                    <option value="A">A</option>
                                    <option value="B">B</option>
                                    <option value="C">C</option>
                                    <option value="D">D</option>
                                </select>
                            </div>
                            <div class="flex items-center gap-2 pt-2">
                                <button type="submit" class="flex-grow py-2 bg-brand-600 hover:bg-brand-700 text-white font-bold rounded-lg shadow-sm">Simpan Soal</button>
                                <button type="button" onclick="clearEditorForm()" class="px-3 py-2 bg-slate-100 hover:bg-slate-200 text-slate-600 font-bold rounded-lg">Batal</button>
                            </div>
                        </form>
                    </div>

                    <!-- Live Question List (JSON Format) -->
                    <div class="lg:col-span-8 bg-white border border-slate-200 p-5 rounded-2xl shadow-sm space-y-4">
                        <div class="flex items-center justify-between">
                            <h3 class="font-heading font-bold text-brand-950 text-sm">Daftar Soal Aktif (Database JSON)</h3>
                            <button onclick="resetQuestionsToDefault()" class="px-3 py-1 bg-brand-50 hover:bg-brand-100 border border-indigo-100 text-brand-800 rounded-xl text-xs font-bold transition"><i class="fa-solid fa-rotate-left"></i> Reset ke Standar</button>
                        </div>
                        <div class="max-h-[500px] overflow-y-auto border border-slate-100 rounded-xl divide-y divide-slate-100">
                            <div id="editor-soal-list" class="divide-y divide-slate-100 text-xs">
                                <!-- Dynamic soal items edit row -->
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

    </main>

    <!-- FOOTER STYLED -->
    <footer class="bg-brand-950 border-t border-slate-900 py-6 mt-8 text-slate-400">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex flex-col sm:flex-row items-center justify-between gap-4">
            <span class="text-xs">
                &copy; 2026 CBT TKA SMP.
            </span>
        </div>
    </footer>

    <!-- CUSTOM IN-APP MODAL SYSTEM -->
    <div id="custom-modal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-950/60 backdrop-blur-sm hidden">
        <div class="bg-white rounded-3xl border border-brand-50 max-w-sm w-full p-6 shadow-2xl space-y-4">
            <div class="flex items-start gap-3">
                <div id="modal-icon-bg" class="p-2.5 rounded-2xl text-lg flex items-center justify-center shadow-inner">
                    <i id="modal-icon" class="fa-solid"></i>
                </div>
                <div>
                    <h3 id="modal-title" class="font-heading font-extrabold text-base text-slate-900">Judul</h3>
                    <p id="modal-body" class="text-slate-500 text-xs sm:text-sm mt-1 leading-relaxed">Pesan detail di sini...</p>
                </div>
            </div>
            <div class="flex items-center justify-end gap-2 pt-2" id="modal-actions">
                <button id="modal-btn-cancel" class="px-4 py-2 text-xs font-bold text-slate-500 hover:bg-slate-150 rounded-xl transition">Batal</button>
                <button id="modal-btn-confirm" class="px-4 py-2 text-xs font-bold text-white rounded-xl transition">Konfirmasi</button>
            </div>
        </div>
    </div>

    <script>
        // DEFAULT HOTS-BASED MATHEMATICAL LITERACY QUESTIONS
        const DEFAULT_QUESTIONS = [
            {
                "nomor": 1,
                "mapel": "Numerasi (HOTS)",
                "stimulus": [
                    "Berdasarkan hasil pemantauan tarif parkir progresif di sebuah pusat perbelanjaan di Kota Semarang, pihak pengelola menerapkan aturan perhitungan sebagai berikut untuk menertibkan area parkir kendaraan mobil.",
                    "Aturan Tarif Parkir Mobil: Pada 1 jam pertama dikenakan biaya tetap sebesar Rp 5.000. Setiap tambahan jam berikutnya (atau bagian dari jam tersebut) dikenakan biaya tambahan progresif sebesar Rp 3.000 per jam. Selain itu, jika parkir lebih dari 5 jam, akan dikenakan denda ketertiban sebesar Rp 10.000.",
                    "Rudi memarkir mobilnya mulai pukul 08.15 pagi untuk menghadiri pameran buku sekolah dan baru kembali mengambil mobilnya pada pukul 14.30 di hari yang sama."
                ],
                "soal": "Berdasarkan informasi di atas, berapakah total biaya parkir progresif yang harus dibayarkan Rudi saat keluar dari area parkir?",
                "opsi": [
                    "A. Rp 20.000",
                    "B. Rp 23.000",
                    "C. Rp 30.000",
                    "D. Rp 33.000"
                ],
                "jawaban": "D"
            },
            {
                "nomor": 2,
                "mapel": "Aljabar (HOTS)",
                "stimulus": [
                    "Menjelang liburan sekolah, sebuah toko pakaian 'Gaya Siswa' memberikan penawaran promosi potongan harga berlipat ganda untuk menarik pembeli.",
                    "Penawaran Promo Ganda: Setiap pembelian satu seragam sekolah akan mendapatkan potongan harga diskon langsung sebesar 20%, kemudian setelah harga dipotong 20% tersebut, pembeli berhak mendapatkan diskon tambahan lagi sebesar 10% dari sisa harga potongan tadi (Diskon Ganda: 20% + 10%).",
                    "Sebuah seragam sekolah yang diincar Doni memiliki harga banderol awal sebesar Rp 150.000."
                ],
                "soal": "Berapakah total harga yang harus dibayarkan Doni untuk membeli satu seragam sekolah setelah seluruh promo diskon ganda diterapkan?",
                "opsi": [
                    "A. Rp 105.000",
                    "B. Rp 108.000",
                    "C. Rp 112.500",
                    "D. Rp 120.000"
                ],
                "jawaban": "B"
            },
            {
                "nomor": 3,
                "mapel": "Geometri & Data (HOTS)",
                "stimulus": [
                    "Perusahaan PDAM Kota Cerdas memberlakukan perhitungan tagihan bulanan berjenjang untuk konsumsi air bersih rumah tangga guna membatasi pemborosan sumber daya air.",
                    "Skema Tarif Berjenjang PDAM:\n- Blok I (0 - 10 m³ pertama): Tarif tetap Rp 4.000 per m³\n- Blok II (11 - 20 m³): Tarif Rp 6.000 per m³\n- Blok III (Lebih dari 20 m³): Tarif Rp 9.000 per m³\n\nSelain biaya volume air tersebut, setiap pelanggan dikenakan biaya administrasi langganan bulanan wajib sebesar Rp 15.000.",
                    "Rumah tangga keluarga Pak Budi mengonsumsi air bersih bersih sebanyak 25 m³ selama bulan Juli."
                ],
                "soal": "Berapakah total tagihan pembayaran PDAM yang harus diselesaikan oleh Pak Budi pada bulan tersebut?",
                "opsi": [
                    "A. Rp 145.000",
                    "B. Rp 155.000",
                    "C. Rp 160.000",
                    "D. Rp 175.000"
                ],
                "jawaban": "C"
            },
            {
                "nomor": 4,
                "mapel": "Statistika (HOTS)",
                "stimulus": [
                    "Dinas Lingkungan Hidup mengamati data rata-rata volume pembuangan sampah organik dan anorganik dari lima perumahan padat penduduk selama satu minggu.",
                    "Tabel Catatan Volume Sampah Mingguan:\n1. Perumahan Dahlia: Organik = 120 kg, Anorganik = 80 kg\n2. Perumahan Melati: Organik = 150 kg, Anorganik = 100 kg\n3. Perumahan Flamboyan: Organik = 90 kg, Anorganik = 110 kg\n4. Perumahan Cemara: Organik = 200 kg, Anorganik = 140 kg\n5. Perumahan Anggrek: Organik = 110 kg, Anorganik = 90 kg",
                    "Pemerintah kota berencana memberikan insentif penghargaan kebersihan lingkungan hanya untuk perumahan yang memiliki nilai perbandingan (rasio) volume sampah organik terhadap anorganik paling tinggi."
                ],
                "soal": "Berdasarkan prinsip rasio di atas, perumahan manakah yang berhak mendapatkan penghargaan insentif kebersihan lingkungan tersebut?",
                "opsi": [
                    "A. Perumahan Dahlia",
                    "B. Perumahan Melati",
                    "C. Perumahan Cemara",
                    "D. Perumahan Anggrek"
                ],
                "jawaban": "A"
            },
            {
                "nomor": 5,
                "mapel": "Pemodelan (HOTS)",
                "stimulus": [
                    "Dalam fisika gerak dan pemodelan kuadrat matematika, tinggi suatu peluru mainan yang ditembakkan vertikal ke atas dalam waktu t detik dimodelkan dengan fungsi rumus matematika h(t) = 40t - 5t² (tinggi dalam satuan meter).",
                    "Pemahaman Konsep: Peluru akan bergerak terus naik hingga mencapai titik ketinggian maksimum ketika kecepatannya menjadi nol, lalu peluru perlahan-lahan jatuh kembali ke permukaan tanah."
                ],
                "soal": "Berdasarkan model fungsi kuadrat di atas, pada detik keberapakah peluru tersebut akan mencapai ketinggian puncak maksimumnya?",
                "opsi": [
                    "A. 4 detik",
                    "B. 5 detik",
                    "C. 8 detik",
                    "D. 10 detik"
                ],
                "jawaban": "A"
            }
        ];

        // INITIAL MOCK DB DATA
        const MOCK_PARTICIPANTS = [
            {
                nama: "Rian Aditya", kelas: "9A", absen: "12", 
                tanggal: "2026-07-16", jamMulai: "08:00", jamSelesai: "09:45", durasi: "1 jam 45 menit",
                benar: 4, salah: 1, skor: 80,
                jawabanSiswa: { 1: "D", 2: "B", 3: "A", 4: "A", 5: "A" }
            },
            {
                nama: "Siti Maulida", kelas: "9B", absen: "30", 
                tanggal: "2026-07-16", jamMulai: "08:15", jamSelesai: "09:30", durasi: "1 jam 15 menit",
                benar: 5, salah: 0, skor: 100,
                jawabanSiswa: { 1: "D", 2: "B", 3: "C", 4: "A", 5: "A" }
            },
            {
                nama: "Hendra Wijaya", kelas: "9C", absen: "7", 
                tanggal: "2026-07-16", jamMulai: "08:05", jamSelesai: "09:55", durasi: "1 jam 50 menit",
                benar: 3, salah: 2, skor: 60,
                jawabanSiswa: { 1: "C", 2: "B", 3: "C", 4: "B", 5: "C" }
            }
        ];

        // GLOBAL APPLICATION STATE
        let questions = [];
        let currentQuestionIndex = 0;
        let activeStudent = null;
        let examTimerInterval = null;
        let examTimeLeftInSeconds = 120 * 60; // 120 Minutes
        let answersSaved = {};
        let doubtfulSaved = {}; // New doubtful tracker
        let examStartTimeStr = "";
        let analysisChartInstance = null;

        // TOOLBAR ASSISTIVE STATES
        let activeHighlighter = false;
        let activeReadingRuler = false;

        // ON LOAD INITIALIZER
        window.onload = function() {
            loadQuestions();
            loadConfigAndSubmissions();
            switchView('student-gate');
        };

        function loadQuestions() {
            const localQ = localStorage.getItem('tka_literasi_questions');
            if (localQ) {
                questions = JSON.parse(localQ);
            } else {
                questions = [...DEFAULT_QUESTIONS];
                localStorage.setItem('tka_literasi_questions', JSON.stringify(questions));
            }
        }

        function loadConfigAndSubmissions() {
            const submissions = localStorage.getItem('tka_literasi_submissions');
            if (!submissions) {
                localStorage.setItem('tka_literasi_submissions', JSON.stringify(MOCK_PARTICIPANTS));
            }
        }

        // NAVIGATION VIEW ENGINE
        function switchView(viewId) {
            const views = ['student-gate', 'student-exam', 'student-results', 'teacher-login', 'teacher-dashboard'];
            views.forEach(v => {
                const el = document.getElementById(`view-${v}`);
                if (el) el.classList.add('hidden');
            });

            // Update Header Tab status visually
            const tabStudent = document.getElementById('tab-student');
            if (tabStudent) {
                tabStudent.className = "px-3.5 py-2 text-xs sm:text-sm font-semibold rounded-xl transition-all duration-255 " + 
                    (viewId.startsWith('student') ? 'bg-brand-600 text-white shadow-md shadow-indigo-600/10' : 'text-brand-200 hover:text-white hover:bg-white/15');
            }
            const tabTeacher = document.getElementById('tab-teacher');
            if (tabTeacher) {
                tabTeacher.className = "px-3.5 py-2 text-xs sm:text-sm font-semibold rounded-xl transition-all duration-255 " + 
                    (viewId.startsWith('teacher') ? 'bg-slate-900 text-white border border-indigo-900' : 'text-brand-200 hover:text-white hover:bg-white/15');
            }

            const targetView = document.getElementById(`view-${viewId}`);
            if (targetView) targetView.classList.remove('hidden');
            
            if (!viewId.startsWith('student-exam') && examTimerInterval) {
                clearInterval(examTimerInterval);
            }
        }

        // TOOLBAR READING ASSIST ENGINE
        function toggleHighlighter() {
            activeHighlighter = !activeHighlighter;
            const btn = document.getElementById('btn-highlighter');
            if (activeHighlighter) {
                btn.className = "px-3 py-1.5 text-xs font-semibold rounded-lg bg-yellow-100 border border-yellow-300 text-yellow-900 flex items-center gap-1.5 transition";
                showToast("Stabilo Aktif: Blok kata/angka di teks kiri untuk menandai!");
            } else {
                btn.className = "px-3 py-1.5 text-xs font-semibold rounded-lg bg-white border text-slate-700 hover:bg-indigo-50 flex items-center gap-1.5 transition";
            }
            setupTextHighlighterEvent();
        }

        function setupTextHighlighterEvent() {
            const container = document.getElementById('display-stimulus-container');
            if (activeHighlighter) {
                container.onmouseup = function() {
                    const sel = window.getSelection();
                    if (!sel.isCollapsed && sel.rangeCount > 0) {
                        const range = sel.getRangeAt(0);
                        const span = document.createElement('span');
                        span.className = 'highlighted-text';
                        span.appendChild(range.extractContents());
                        range.insertNode(span);
                        sel.removeAllRanges();
                    }
                };
            } else {
                container.onmouseup = null;
            }
        }

        function toggleReadingRuler() {
            activeReadingRuler = !activeReadingRuler;
            const btn = document.getElementById('btn-ruler');
            const panel = document.getElementById('panel-stimulus');
            
            if (activeReadingRuler) {
                btn.className = "px-3 py-1.5 text-xs font-semibold rounded-lg bg-indigo-600 border border-indigo-700 text-white flex items-center gap-1.5 transition shadow";
                panel.classList.add('ruler-focus-active');
                showToast("Mistar Fokus Aktif: Klik baris paragraf agar pandangan terfokus!");
            } else {
                btn.className = "px-3 py-1.5 text-xs font-semibold rounded-lg bg-white border text-slate-700 hover:bg-indigo-50 flex items-center gap-1.5 transition";
                panel.classList.remove('ruler-focus-active');
                
                // Clear focused marks
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
        }

        // SCRATCHPAD UTILITY
        function toggleScratchpad() {
            const panel = document.getElementById('scratchpad-panel');
            panel.classList.toggle('hidden');
        }

        // MODALS AND CUSTOM NOTIFICATIONS (NO ALERT / NO CONFIRM)
        function showModal(title, text, type, confirmText, cancelText, onConfirm, onCancel) {
            const modal = document.getElementById('custom-modal');
            const iconBg = document.getElementById('modal-icon-bg');
            const icon = document.getElementById('modal-icon');
            
            document.getElementById('modal-title').innerText = title;
            document.getElementById('modal-body').innerText = text;

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
                if (onConfirm) onConfirm();
            });

            newCancel.addEventListener('click', () => {
                modal.classList.add('hidden');
                if (onCancel) onCancel();
            });

            modal.classList.remove('hidden');
        }

        function showToast(text) {
            const toast = document.createElement('div');
            toast.className = "fixed bottom-4 left-4 z-50 bg-slate-900 text-white text-xs py-2.5 px-4 rounded-xl shadow-lg border border-slate-700 animate-bounce flex items-center gap-1.5";
            toast.innerHTML = `<i class="fa-solid fa-bell text-brand-400"></i> ${text}`;
            document.body.appendChild(toast);
            setTimeout(() => { toast.remove(); }, 4000);
        }

        // STUDENT EXAMINATION INIT
        function startExam(e) {
            e.preventDefault();

            const nama = document.getElementById('input-nama').value.trim();
            const kelas = document.getElementById('input-kelas').value;
            const absen = document.getElementById('input-absen').value.trim();

            if (!nama || !kelas || !absen) {
                showModal("Lengkapi Data", "Silakan lengkapi seluruh formulir identitas.", "warning", "Oke", "Batal", null, null);
                return;
            }

            // Duplication check to enforce TKA validity
            const submissions = JSON.parse(localStorage.getItem('tka_literasi_submissions') || '[]');
            const duplicate = submissions.some(sub => 
                sub.nama.toLowerCase() === nama.toLowerCase() && 
                sub.kelas === kelas && 
                parseInt(sub.absen) === parseInt(absen)
            );

            if (duplicate) {
                showModal(
                    "Anda Sudah Mengerjakan!", 
                    "Sistem mencatat identitas Anda telah menuntaskan ujian. Satu siswa hanya diperbolehkan mengirim satu kali untuk menjaga validitas PPDB.", 
                    "danger", 
                    "Ganti Identitas", 
                    "Kembali", 
                    null, 
                    null
                );
                return;
            }

            activeStudent = { nama, kelas, absen };
            answersSaved = {};
            doubtfulSaved = {};
            currentQuestionIndex = 0;
            examTimeLeftInSeconds = 120 * 60; // Reset timer 120 Mins

            const now = new Date();
            examStartTimeStr = `${String(now.getHours()).padStart(2, '0')}:${String(now.getMinutes()).padStart(2, '0')}`;

            // Restore from automatic crash-recover if exists
            const autosaved = localStorage.getItem(`lite_autosave_${nama}_${kelas}_${absen}`);
            if (autosaved) {
                const parsed = JSON.parse(autosaved);
                answersSaved = parsed.answers || {};
                doubtfulSaved = parsed.doubtful || {};
                examTimeLeftInSeconds = parsed.timeLeft || examTimeLeftInSeconds;
                showToast("Berhasil memulihkan progres ujian Anda!");
            }

            // Build student UI profiles
            document.getElementById('display-student-name').innerText = nama;
            document.getElementById('display-student-class').innerText = kelas;
            document.getElementById('display-student-absen').innerText = String(absen).padStart(2, '0');

            switchView('student-exam');
            renderGridIndicators();
            showQuestion(0);
            startCountdown();
        }

        // EXAMINATION COUNTDOWN CONTROLLER
        function startCountdown() {
            if (examTimerInterval) clearInterval(examTimerInterval);
            const display = document.getElementById('exam-timer');
            
            examTimerInterval = setInterval(() => {
                if (examTimeLeftInSeconds <= 0) {
                    clearInterval(examTimerInterval);
                    display.innerText = "00:00:00";
                    forceEndExam();
                } else {
                    examTimeLeftInSeconds--;
                    const hours = Math.floor(examTimeLeftInSeconds / 3600);
                    const minutes = Math.floor((examTimeLeftInSeconds % 3600) / 60);
                    const seconds = examTimeLeftInSeconds % 60;

                    display.innerText = 
                        `${String(hours).padStart(2, '0')}:${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;

                    // AutoSave draft backup to prevent refresh data losses
                    if (examTimeLeftInSeconds % 10 === 0 && activeStudent) {
                        localStorage.setItem(`lite_autosave_${activeStudent.nama}_${activeStudent.kelas}_${activeStudent.absen}`, JSON.stringify({
                            answers: answersSaved,
                            doubtful: doubtfulSaved,
                            timeLeft: examTimeLeftInSeconds
                        }));
                    }
                }
            }, 1000);
        }

        // RENDER INDICATOR GRID (CBT NAVIGATORS)
        function renderGridIndicators() {
            const container = document.getElementById('student-grid-indicators');
            const inlineNavigator = document.getElementById('inline-navigator');
            
            if (container) {
                container.innerHTML = "";
            }
            if (inlineNavigator) {
                inlineNavigator.innerHTML = "";
            }

            questions.forEach((q, idx) => {
                const isAnswered = answersSaved[q.nomor] !== undefined && answersSaved[q.nomor] !== "";
                const isDoubtful = doubtfulSaved[q.nomor] === true;
                const isActive = idx === currentQuestionIndex;

                // Main Nav Box
                let btnClass = "w-11 h-11 text-xs font-bold rounded-2xl transition-all duration-150 flex items-center justify-center border ";
                
                if (isDoubtful) {
                    btnClass += "bg-amber-500 text-white border-amber-400 shadow-md shadow-amber-500/10 hover:bg-amber-600";
                } else if (isAnswered) {
                    btnClass += "bg-emerald-600 text-white border-emerald-500 shadow-md shadow-emerald-600/10 hover:bg-emerald-700";
                } else {
                    btnClass += "bg-slate-100 text-slate-500 border-slate-200 hover:bg-slate-200";
                }

                if (isActive) {
                    btnClass += " ring-4 ring-brand-500/30 border-brand-600 scale-105 font-black";
                }

                const btn = document.createElement('button');
                btn.className = btnClass;
                btn.innerText = q.nomor;
                btn.onclick = () => goToQuestion(idx);
                if (container) {
                    container.appendChild(btn);
                }

                // Small Inline Circle Dot Indicator (Mobile Friendly)
                if (inlineNavigator) {
                    let dotClass = "w-2.5 h-2.5 rounded-full transition-all ";
                    if (isActive) {
                        dotClass += "bg-brand-600 w-4";
                    } else if (isDoubtful) {
                        dotClass += "bg-amber-500";
                    } else if (isAnswered) {
                        dotClass += "bg-emerald-500";
                    } else {
                        dotClass += "bg-slate-300";
                    }
                    const dot = document.createElement('span');
                    dot.className = dotClass;
                    inlineNavigator.appendChild(dot);
                }
            });
        }

        // DISPLAY MAIN QUESTION & ASSIGNED TEXT STIMULUS (ANBK STYLE)
        function showQuestion(index) {
            if (index < 0 || index >= questions.length) return;
            currentQuestionIndex = index;

            const q = questions[index];
            document.getElementById('current-question-num').innerText = q.nomor;
            document.getElementById('total-questions-num').innerText = questions.length;
            document.getElementById('display-mapel').innerText = q.mapel || "TKA";
            document.getElementById('display-soal-text').innerText = q.soal;

            // Render Split Screen Stimulus on the Left
            const stimulusContainer = document.getElementById('display-stimulus-container');
            stimulusContainer.innerHTML = "";
            
            const paragraphs = q.stimulus || ["Tidak ada teks stimulus tambahan untuk nomor ini."];
            paragraphs.forEach(pText => {
                const p = document.createElement('p');
                p.className = "mb-3 leading-relaxed hover:bg-slate-50 p-2 rounded-xl transition duration-150";
                p.innerText = pText;
                p.onclick = () => triggerLineFocus(p);
                stimulusContainer.appendChild(p);
            });

            // Set highlighter behavior if selected
            setupTextHighlighterEvent();

            // Render Answers Options Cards on the Right
            const optionsContainer = document.getElementById('display-opsi-container');
            optionsContainer.innerHTML = "";

            const optLetters = ['A', 'B', 'C', 'D'];
            q.opsi.forEach((optionTxt, optIdx) => {
                const letter = optLetters[optIdx];
                const cleanTxt = optionTxt.replace(/^[A-D]\.\s*/, '');
                const isChecked = answersSaved[q.nomor] === letter;

                const wrapper = document.createElement('div');
                wrapper.className = "option-card relative";
                wrapper.innerHTML = `
                    <input type="radio" name="exam-option" id="opt-${letter}" value="${letter}" ${isChecked ? 'checked' : ''} class="sr-only" onchange="registerAnswer(${q.nomor}, '${letter}')">
                    <label for="opt-${letter}" class="flex items-center gap-3 px-4 py-3.5 border border-slate-200 rounded-xl cursor-pointer hover:bg-slate-50 transition text-xs sm:text-sm text-slate-700">
                        <span class="w-8 h-8 rounded-lg bg-slate-100 flex items-center justify-center font-bold text-slate-500 border border-slate-200 uppercase">${letter}</span>
                        <span>${cleanTxt}</span>
                    </label>
                `;
                optionsContainer.appendChild(wrapper);
            });

            // Update Doubtful (Ragu-Ragu) Toggle UI
            updateDoubtfulButtonUI();

            // Handle button visibility
            document.getElementById('btn-prev-question').style.visibility = (index === 0) ? 'hidden' : 'visible';
            
            if (index === questions.length - 1) {
                document.getElementById('btn-next-question').classList.add('hidden');
                document.getElementById('btn-finish-exam').classList.remove('hidden');
            } else {
                document.getElementById('btn-next-question').classList.remove('hidden');
                document.getElementById('btn-finish-exam').classList.add('hidden');
            }

            renderGridIndicators();
        }

        function updateDoubtfulButtonUI() {
            const q = questions[currentQuestionIndex];
            const btn = document.getElementById('btn-doubtful-toggle');
            if (doubtfulSaved[q.nomor] === true) {
                btn.className = "px-4 py-2.5 text-xs font-bold rounded-xl flex items-center gap-1.5 transition border border-amber-500 bg-amber-500 text-white shadow-md shadow-amber-500/10";
                btn.innerHTML = `<i class="fa-solid fa-square-check"></i> Ragu-Ragu`;
            } else {
                btn.className = "px-4 py-2.5 text-xs font-bold rounded-xl flex items-center gap-1.5 transition border border-amber-300 bg-amber-50 text-amber-700 hover:bg-amber-100";
                btn.innerHTML = `<i class="fa-regular fa-square"></i> Ragu-Ragu`;
            }
        }

        function toggleDoubtful() {
            const q = questions[currentQuestionIndex];
            doubtfulSaved[q.nomor] = !doubtfulSaved[q.nomor];
            updateDoubtfulButtonUI();
            renderGridIndicators();
        }

        function goToQuestion(index) {
            showQuestion(index);
        }

        function registerAnswer(qNum, letter) {
            answersSaved[qNum] = letter;
            renderGridIndicators();
        }

        // CONFIRMATION DIALOG BEFORE SUBMISSION
        function confirmEndExam() {
            let answeredCount = 0;
            let doubtfulCount = 0;
            questions.forEach(q => {
                if (answersSaved[q.nomor] !== undefined && answersSaved[q.nomor] !== "") {
                    answeredCount++;
                }
                if (doubtfulSaved[q.nomor] === true) {
                    doubtfulCount++;
                }
            });

            const unanswered = questions.length - answeredCount;
            let msg = `Anda telah menjawab ${answeredCount} dari ${questions.length} butir soal.`;
            
            if (doubtfulCount > 0) {
                msg += ` Masih terdapat ${doubtfulCount} soal dengan status Ragu-Ragu. Silakan matikan tanda Ragu-Ragu bila Anda sudah merasa yakin.`;
                showModal(
                    "Masih Ada Ragu-Ragu!", 
                    msg, 
                    "warning", 
                    "Tetap Kirim", 
                    "Periksa Kembali", 
                    () => executeFinalSubmit(), 
                    null
                );
            } else if (unanswered > 0) {
                msg += ` Masih terdapat ${unanswered} soal yang terlewat! Apakah Anda yakin ingin menyelesaikan ujian?`;
                showModal(
                    "Soal Belum Lengkap!", 
                    msg, 
                    "danger", 
                    "Kirim Sekarang", 
                    "Periksa Kembali", 
                    () => executeFinalSubmit(), 
                    null
                );
            } else {
                msg += " Apakah Anda yakin ingin mengakhiri dan mengirim jawaban?";
                showModal(
                    "Ujian Selesai?", 
                    msg, 
                    "success", 
                    "Ya, Kirim", 
                    "Periksa Kembali", 
                    () => executeFinalSubmit(), 
                    null
                );
            }
        }

        function forceEndExam() {
            showModal(
                "Waktu Selesai!", 
                "Batas waktu Anda telah habis. Lembar jawab Anda dikirim otomatis.", 
                "danger", 
                "Lihat Hasil", 
                "Tutup", 
                () => executeFinalSubmit(true), 
                () => executeFinalSubmit(true)
            );
        }

        // MAIN TRANSMISSION LOGIC (CALCULATE BENAR-SALAH AND TRANSMIT TO LOCAL STORAGE)
        function executeFinalSubmit(isForced = false) {
            if (examTimerInterval) clearInterval(examTimerInterval);

            let correctCount = 0;
            let incorrectCount = 0;

            questions.forEach(q => {
                const ans = answersSaved[q.nomor] || "-";
                if (ans === q.jawaban) {
                    correctCount++;
                } else {
                    incorrectCount++;
                }
            });

            const score = (correctCount / questions.length) * 100;
            const elapsed = (120 * 60) - examTimeLeftInSeconds;
            const elapsedMin = Math.floor(elapsed / 60);
            const elapsedSecStr = `${elapsedMin} menit`;

            const endT = new Date();
            const formatEnd = `${String(endT.getHours()).padStart(2, '0')}:${String(endT.getMinutes()).padStart(2, '0')}`;
            const dateStr = endT.toISOString().split('T')[0];

            // Build Payload
            const submission = {
                nama: activeStudent.nama,
                kelas: activeStudent.kelas,
                absen: parseInt(activeStudent.absen),
                tanggal: dateStr,
                jamMulai: examStartTimeStr,
                jamSelesai: formatEnd,
                durasi: elapsedSecStr,
                benar: correctCount,
                salah: incorrectCount,
                skor: parseFloat(score.toFixed(1)),
                jawabanSiswa: answersSaved
            };

            // Save to Local Data Storage
            const submissions = JSON.parse(localStorage.getItem('tka_literasi_submissions') || '[]');
            submissions.push(submission);
            localStorage.setItem('tka_literasi_submissions', JSON.stringify(submissions));

            // Remove crash recovers
            localStorage.removeItem(`lite_autosave_${activeStudent.nama}_${activeStudent.kelas}_${activeStudent.absen}`);

            // Display Results
            document.getElementById('res-student-name').innerText = activeStudent.nama;
            document.getElementById('res-student-class').innerText = `${activeStudent.kelas} / Absen ${activeStudent.absen}`;
            document.getElementById('res-total-correct').innerText = correctCount;
            document.getElementById('res-total-incorrect').innerText = incorrectCount;
            document.getElementById('res-final-score').innerText = score.toFixed(1);

            switchView('student-results');
            activeStudent = null;
        }

        // TEACHER AUTH GATES
        function openTeacherLogin() {
            switchView('teacher-login');
            document.getElementById('input-teacher-pwd').value = "";
            document.getElementById('error-pwd-msg').classList.add('hidden');
        }

        function verifyTeacherLogin(e) {
            e.preventDefault();
            const pass = document.getElementById('input-teacher-pwd').value;
            if (pass === "adminTKA2026") {
                switchView('teacher-dashboard');
                switchTeacherTab('tab-peserta');
            } else {
                document.getElementById('error-pwd-msg').classList.remove('hidden');
            }
        }

        function switchTeacherTab(tabId) {
            const tabs = ['tab-peserta', 'tab-butir', 'tab-analisis', 'tab-matriks', 'tab-soal-editor'];
            tabs.forEach(t => {
                document.getElementById(`subview-${t}`).classList.add('hidden');
                
                let realBtnId = "";
                if(t === 'tab-peserta') realBtnId = "btn-tab-peserta";
                if(t === 'tab-butir') realBtnId = "btn-tab-butir";
                if(t === 'tab-analisis') realBtnId = "btn-tab-analisis";
                if(t === 'tab-matriks') realBtnId = "btn-tab-matriks";
                if(t === 'tab-soal-editor') realBtnId = "btn-tab-soal";

                const btn = document.getElementById(realBtnId);
                if (btn) {
                    if (t === tabId) {
                        btn.className = "px-3.5 py-1.5 text-xs font-semibold rounded-lg bg-brand-600 text-white shadow-sm";
                    } else if (t === 'tab-soal-editor') {
                        btn.className = "px-3.5 py-1.5 text-xs font-semibold rounded-lg text-brand-600 hover:bg-brand-50 transition";
                    } else {
                        btn.className = "px-3.5 py-1.5 text-xs font-semibold rounded-lg text-slate-600 hover:bg-slate-100 transition";
                    }
                }
            });

            document.getElementById(`subview-${tabId}`).classList.remove('hidden');

            if (tabId === 'tab-peserta') {
                renderTeacherPesertaTable();
            } else if (tabId === 'tab-butir') {
                renderRekapButirCards();
            } else if (tabId === 'tab-analisis') {
                renderDifficultyAnalysis();
            } else if (tabId === 'tab-matriks') {
                renderAnswerMatrix();
            } else if (tabId === 'tab-soal-editor') {
                renderSoalEditorList();
            }
        }

        // GURU TAB 1: RENDER PARTICIPANTS DETAILS
        function renderTeacherPesertaTable() {
            const submissions = JSON.parse(localStorage.getItem('tka_literasi_submissions') || '[]');
            const tbody = document.getElementById('tbody-peserta-rows');
            tbody.innerHTML = "";

            const filter = document.getElementById('sort-filter-peserta').value;
            let sorted = [...submissions];

            if (filter === 'skor-desc') {
                sorted.sort((a, b) => b.skor - a.skor);
            } else if (filter === 'skor-asc') {
                sorted.sort((a, b) => a.skor - b.skor);
            } else if (filter === 'absen') {
                sorted.sort((a, b) => a.absen - b.absen);
            } else if (filter === 'nama') {
                sorted.sort((a, b) => a.nama.localeCompare(b.nama));
            }

            const total = sorted.length;
            let avg = 0;
            let maxVal = 0;

            if (total > 0) {
                const sum = sorted.reduce((s, x) => s + x.skor, 0);
                avg = (sum / total).toFixed(1);
                maxVal = Math.max(...sorted.map(x => x.skor));
            }

            document.getElementById('dash-stat-total').innerText = total;
            document.getElementById('dash-stat-avg').innerText = avg;
            document.getElementById('dash-stat-max').innerText = maxVal.toFixed(1);

            if (total === 0) {
                tbody.innerHTML = `<tr><td colspan="9" class="px-6 py-8 text-center text-slate-400">Belum ada siswa yang terekam mengirim lembar jawab.</td></tr>`;
                return;
            }

            sorted.forEach(item => {
                const tr = document.createElement('tr');
                tr.className = "hover:bg-slate-50/50 transition";
                tr.innerHTML = `
                    <td class="px-6 py-3 font-semibold text-slate-900">${item.nama}</td>
                    <td class="px-6 py-3 text-slate-500">${item.kelas}</td>
                    <td class="px-6 py-3 text-center text-slate-600 font-mono font-bold">${item.absen}</td>
                    <td class="px-6 py-3 text-slate-500 font-mono text-[10px]">${item.tanggal || '-'}</td>
                    <td class="px-6 py-3 text-slate-500 font-mono text-[10px]">${item.jamMulai || '-'}</td>
                    <td class="px-6 py-3 text-slate-500 font-mono text-[10px]">${item.jamSelesai || '-'}</td>
                    <td class="px-6 py-3 text-center text-slate-500 font-mono text-[10px]">${item.durasi || '-'}</td>
                    <td class="px-6 py-3 text-center font-semibold text-emerald-600">${item.benar}</td>
                    <td class="px-6 py-3 text-center font-semibold text-rose-600">${item.salah}</td>
                    <td class="px-6 py-3 text-center font-bold text-brand-600">${item.skor}</td>
                `;
                tbody.appendChild(tr);
            });
        }

        // GURU TAB 2: RENDER REKAP JAWABAN PER NOMOR SOAL
        function renderRekapButirCards() {
            const submissions = JSON.parse(localStorage.getItem('tka_literasi_submissions') || '[]');
            const container = document.getElementById('rekap-cards-container');
            container.innerHTML = "";

            if (questions.length === 0) {
                container.innerHTML = `<div class="col-span-full py-8 text-center text-slate-400">Belum ada soal terkonfigurasi.</div>`;
                return;
            }

            questions.forEach(q => {
                let a = 0, b = 0, c = 0, d = 0, empty = 0;

                submissions.forEach(sub => {
                    const ans = sub.jawabanSiswa ? sub.jawabanSiswa[q.nomor] : null;
                    if (ans === 'A') a++;
                    else if (ans === 'B') b++;
                    else if (ans === 'C') c++;
                    else if (ans === 'D') d++;
                    else empty++;
                });

                const total = submissions.length;
                let correctCount = 0;
                if (q.jawaban === 'A') correctCount = a;
                if (q.jawaban === 'B') correctCount = b;
                if (q.jawaban === 'C') correctCount = c;
                if (q.jawaban === 'D') correctCount = d;

                const incorrectCount = total - correctCount;
                const percentCorrect = total > 0 ? ((correctCount / total) * 100).toFixed(0) : 0;
                const percentIncorrect = total > 0 ? (100 - percentCorrect).toFixed(0) : 0;

                const card = document.createElement('div');
                card.className = "bg-white border border-slate-200 rounded-2xl p-4 shadow-sm flex flex-col justify-between space-y-3";
                card.innerHTML = `
                    <div>
                        <div class="flex items-center justify-between mb-1.5">
                            <span class="text-[10px] font-bold text-slate-400 uppercase tracking-wide">Soal Nomor ${q.nomor}</span>
                            <span class="text-[9px] bg-slate-100 px-2 py-0.5 rounded-full text-slate-500 font-bold">${q.mapel}</span>
                        </div>
                        <p class="text-slate-800 text-xs font-semibold line-clamp-2 mb-2" title="${q.soal}">${q.soal}</p>
                        
                        <div class="space-y-1.5 text-xs">
                            <div class="flex justify-between py-1 px-1.5 rounded-lg ${q.jawaban === 'A' ? 'bg-emerald-50 text-emerald-800 font-bold' : ''}">
                                <span>A : ${a} siswa</span>
                                ${q.jawaban === 'A' ? '<span class="text-[10px] font-bold">✔ Kunci</span>' : ''}
                            </div>
                            <div class="flex justify-between py-1 px-1.5 rounded-lg ${q.jawaban === 'B' ? 'bg-emerald-50 text-emerald-800 font-bold' : ''}">
                                <span>B : ${b} siswa</span>
                                ${q.jawaban === 'B' ? '<span class="text-[10px] font-bold">✔ Kunci</span>' : ''}
                            </div>
                            <div class="flex justify-between py-1 px-1.5 rounded-lg ${q.jawaban === 'C' ? 'bg-emerald-50 text-emerald-800 font-bold' : ''}">
                                <span>C : ${c} siswa</span>
                                ${q.jawaban === 'C' ? '<span class="text-[10px] font-bold">✔ Kunci</span>' : ''}
                            </div>
                            <div class="flex justify-between py-1 px-1.5 rounded-lg ${q.jawaban === 'D' ? 'bg-emerald-50 text-emerald-800 font-bold' : ''}">
                                <span>D : ${d} siswa</span>
                                ${q.jawaban === 'D' ? '<span class="text-[10px] font-bold">✔ Kunci</span>' : ''}
                            </div>
                            ${empty > 0 ? `<div class="text-[9px] text-vibrant-rose italic">Terlewat: ${empty} siswa</div>` : ''}
                        </div>
                    </div>

                    <div class="pt-2.5 border-t border-slate-100 grid grid-cols-2 gap-2 text-center text-[10px]">
                        <div class="bg-emerald-50/50 border border-emerald-100 rounded-xl py-1.5">
                            <span class="block text-[8px] text-emerald-600 font-extrabold uppercase tracking-wide">Benar</span>
                            <span class="font-extrabold text-emerald-800 text-xs">${correctCount} (${percentCorrect}%)</span>
                        </div>
                        <div class="bg-rose-50/50 border border-rose-100 rounded-xl py-1.5">
                            <span class="block text-[8px] text-rose-600 font-extrabold uppercase tracking-wide">Salah</span>
                            <span class="font-extrabold text-rose-800 text-xs">${incorrectCount} (${percentIncorrect}%)</span>
                        </div>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        // GURU TAB 3: DIFFICULTY SUMMARY & BARCHART RENDER
        function renderDifficultyAnalysis() {
            const submissions = JSON.parse(localStorage.getItem('tka_literasi_submissions') || '[]');
            const tbody = document.getElementById('tbody-analisis-rows');
            tbody.innerHTML = "";

            const statsList = [];
            const labels = [];
            const dataCorrect = [];
            const dataIncorrect = [];

            questions.forEach(q => {
                let correctCount = 0;
                let incorrectCount = 0;

                submissions.forEach(sub => {
                    const ans = sub.jawabanSiswa ? sub.jawabanSiswa[q.nomor] : null;
                    if (ans === q.jawaban) {
                        correctCount++;
                    } else {
                        incorrectCount++;
                    }
                });

                const total = submissions.length;
                const pCorrect = total > 0 ? Math.round((correctCount / total) * 100) : 0;
                const pIncorrect = total > 0 ? Math.round((incorrectCount / total) * 100) : 0;

                let diffText = "Sangat Mudah";
                let diffColor = "bg-emerald-50 text-emerald-800 border border-emerald-200";
                
                if (pCorrect < 30) {
                    diffText = "Sangat Sulit";
                    diffColor = "bg-rose-50 text-rose-800 border border-rose-200";
                } else if (pCorrect < 60) {
                    diffText = "Sedang / Cukup Sulit";
                    diffColor = "bg-amber-50 text-amber-800 border border-amber-200";
                } else if (pCorrect < 85) {
                    diffText = "Mudah";
                    diffColor = "bg-indigo-50 text-indigo-800 border border-indigo-200";
                }

                statsList.push({
                    no: q.nomor,
                    mapel: q.mapel,
                    benar: correctCount,
                    salah: incorrectCount,
                    pCorrect,
                    pIncorrect,
                    diffText,
                    diffColor
                });

                labels.push(`S${q.nomor}`);
                dataCorrect.push(correctCount);
                dataIncorrect.push(incorrectCount);
            });

            // Sort from hardest to easiest (Percentage Incorrect Descending)
            statsList.sort((a, b) => b.pIncorrect - a.pIncorrect);

            statsList.forEach(item => {
                const tr = document.createElement('tr');
                tr.className = "hover:bg-slate-50 transition text-xs";
                tr.innerHTML = `
                    <td class="px-6 py-3 font-bold text-slate-800">Soal ${item.no}</td>
                    <td class="px-6 py-3 text-slate-500 font-medium">${item.mapel}</td>
                    <td class="px-6 py-3 text-center font-bold text-emerald-600">${item.benar}</td>
                    <td class="px-6 py-3 text-center font-bold text-rose-600">${item.salah}</td>
                    <td class="px-6 py-3 text-center font-semibold text-emerald-600">${item.pCorrect}%</td>
                    <td class="px-6 py-3 text-center font-semibold text-rose-600">${item.pIncorrect}%</td>
                    <td class="px-6 py-3">
                        <span class="px-2 py-0.5 rounded-lg text-[10px] font-semibold ${item.diffColor}">${item.diffText}</span>
                    </td>
                `;
                tbody.appendChild(tr);
            });

            // Re-render Chart.js
            const ctx = document.getElementById('analisisChart').getContext('2d');
            if (analysisChartInstance) {
                analysisChartInstance.destroy();
            }

            analysisChartInstance = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: labels,
                    datasets: [
                        {
                            label: 'Jumlah Siswa Benar',
                            data: dataCorrect,
                            backgroundColor: '#10b981',
                            borderRadius: 6
                        },
                        {
                            label: 'Jumlah Siswa Salah',
                            data: dataIncorrect,
                            backgroundColor: '#f43f5e',
                            borderRadius: 6
                        }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true,
                            ticks: { stepSize: 1 }
                        }
                    },
                    plugins: {
                        legend: { position: 'bottom' }
                    }
                }
            });
        }

        // GURU TAB 4: MATRIKS REKAP JAWABAN SISWA
        function renderAnswerMatrix() {
            const submissions = JSON.parse(localStorage.getItem('tka_literasi_submissions') || '[]');
            const thead = document.getElementById('thead-matriks');
            const tbody = document.getElementById('tbody-matriks-rows');

            thead.innerHTML = "";
            tbody.innerHTML = "";

            if (questions.length === 0) return;

            const trHead = document.createElement('tr');
            trHead.className = "bg-slate-50 border-b border-slate-100 text-slate-500 font-bold text-[9px] uppercase tracking-wider";
            
            let headings = `
                <th class="px-4 py-3.5">Nama Peserta</th>
                <th class="px-3 py-3.5 text-center">Kls</th>
                <th class="px-3 py-3.5 text-center">Abs</th>
            `;

            questions.forEach(q => {
                headings += `<th class="px-2 py-3.5 text-center font-bold" title="${q.mapel}">S${q.nomor}</th>`;
            });

            headings += `<th class="px-4 py-3.5 text-center">Skor</th>`;
            trHead.innerHTML = headings;
            thead.appendChild(trHead);

            if (submissions.length === 0) {
                tbody.innerHTML = `<tr><td colspan="${questions.length + 4}" class="px-6 py-6 text-center text-slate-400">Belum ada siswa yang terekam.</td></tr>`;
                return;
            }

            submissions.forEach(sub => {
                const tr = document.createElement('tr');
                tr.className = "hover:bg-slate-50/50 transition border-b border-slate-100 text-xs";

                let tds = `
                    <td class="px-4 py-2.5 font-bold text-slate-900 truncate max-w-[120px]" title="${sub.nama}">${sub.nama}</td>
                    <td class="px-3 py-2.5 text-slate-500 text-center">${sub.kelas}</td>
                    <td class="px-3 py-2.5 text-slate-600 text-center font-mono font-semibold">${sub.absen}</td>
                `;

                questions.forEach(q => {
                    const studentAns = sub.jawabanSiswa ? sub.jawabanSiswa[q.nomor] : null;
                    const isCorrect = studentAns === q.jawaban;

                    if (studentAns) {
                        tds += `
                            <td class="px-1 py-2.5 text-center font-mono">
                                ${studentAns}
                                ${isCorrect ? '<span class="text-[10px] text-emerald-600 font-bold ml-0.5" title="Kunci Cocok">✔</span>' : ''}
                            </td>
                        `;
                    } else {
                        tds += `<td class="px-1 py-2.5 text-center text-slate-300">-</td>`;
                    }
                });

                tds += `<td class="px-4 py-2.5 text-center font-bold text-brand-600">${sub.skor}</td>`;
                tr.innerHTML = tds;
                tbody.appendChild(tr);
            });
        }

        // GURU TAB 5: DATABASE EDIT VIEW
        function renderSoalEditorList() {
            const container = document.getElementById('editor-soal-list');
            container.innerHTML = "";

            if (questions.length === 0) {
                container.innerHTML = `<div class="p-4 text-center text-slate-400">Tidak ada soal aktif. Klik reset ke standar untuk memuat contoh.</div>`;
                return;
            }

            questions.forEach((q, idx) => {
                const item = document.createElement('div');
                item.className = "p-3 hover:bg-slate-50/50 flex flex-col sm:flex-row sm:items-center justify-between gap-3 transition";
                item.innerHTML = `
                    <div>
                        <div class="flex items-center gap-1.5 mb-1">
                            <span class="px-1.5 py-0.5 bg-slate-100 text-slate-700 rounded font-bold text-[9px]">No. ${q.nomor}</span>
                            <span class="px-1.5 py-0.5 bg-indigo-50 text-indigo-800 rounded text-[9px] font-semibold">${q.mapel}</span>
                            <span class="text-[9px] font-bold text-emerald-600">Jawaban: ${q.jawaban}</span>
                        </div>
                        <p class="text-slate-800 text-[11px] font-semibold line-clamp-1 mb-0.5">${q.soal}</p>
                        <p class="text-[9px] text-slate-400">Opsi: A. ${q.opsi[0]} | B. ${q.opsi[1]} | C. ${q.opsi[2]} | D. ${q.opsi[3]}</p>
                    </div>
                    <div class="flex items-center gap-1 self-end sm:self-auto">
                        <button onclick="editSoalClick(${idx})" class="px-2 py-1 bg-blue-50 hover:bg-blue-100 text-blue-700 font-bold rounded-lg text-[10px] transition"><i class="fa-solid fa-pencil"></i></button>
                        <button onclick="deleteSoalClick(${idx})" class="px-2 py-1 bg-rose-50 hover:bg-rose-100 text-rose-700 font-bold rounded-lg text-[10px] transition"><i class="fa-solid fa-trash"></i></button>
                    </div>
                `;
                container.appendChild(item);
            });
        }

        function clearEditorForm() {
            document.getElementById('soal-edit-index').value = "";
            document.getElementById('editor-form-title').innerText = "Tambah Soal Baru";
            document.getElementById('edit-soal-nomor').value = questions.length + 1;
            document.getElementById('edit-soal-mapel').value = "";
            document.getElementById('edit-soal-stimulus').value = "";
            document.getElementById('edit-soal-teks').value = "";
            document.getElementById('edit-soal-opsiA').value = "";
            document.getElementById('edit-soal-opsiB').value = "";
            document.getElementById('edit-soal-opsiC').value = "";
            document.getElementById('edit-soal-opsiD').value = "";
            document.getElementById('edit-soal-jawaban').value = "A";
        }

        function editSoalClick(idx) {
            const q = questions[idx];
            document.getElementById('soal-edit-index').value = idx;
            document.getElementById('editor-form-title').innerText = "Edit Soal Nomor " + q.nomor;
            document.getElementById('edit-soal-nomor').value = q.nomor;
            document.getElementById('edit-soal-mapel').value = q.mapel || "Literasi";
            document.getElementById('edit-soal-stimulus').value = q.stimulus ? q.stimulus.join('\n\n') : "";
            document.getElementById('edit-soal-teks').value = q.soal;
            
            document.getElementById('edit-soal-opsiA').value = q.opsi[0].replace(/^[A]\.\s*/, '');
            document.getElementById('edit-soal-opsiB').value = q.opsi[1].replace(/^[B]\.\s*/, '');
            document.getElementById('edit-soal-opsiC').value = q.opsi[2].replace(/^[C]\.\s*/, '');
            document.getElementById('edit-soal-opsiD').value = q.opsi[3].replace(/^[D]\.\s*/, '');
            
            document.getElementById('edit-soal-jawaban').value = q.jawaban;
            
            document.getElementById('form-edit-soal').scrollIntoView({ behavior: 'smooth' });
        }

        function saveSoalItem(e) {
            e.preventDefault();

            const idxVal = document.getElementById('soal-edit-index').value;
            const nomor = parseInt(document.getElementById('edit-soal-nomor').value);
            const mapel = document.getElementById('edit-soal-mapel').value.trim();
            const rawStimulus = document.getElementById('edit-soal-stimulus').value.trim();
            const soalText = document.getElementById('edit-soal-teks').value.trim();
            const valA = document.getElementById('edit-soal-opsiA').value.trim();
            const valB = document.getElementById('edit-soal-opsiB').value.trim();
            const valC = document.getElementById('edit-soal-opsiC').value.trim();
            const valD = document.getElementById('edit-soal-opsiD').value.trim();
            const jawaban = document.getElementById('edit-soal-jawaban').value;

            // Split raw stimulus paragraph text via breakline double spaces
            const stimulusArray = rawStimulus.split(/\n\s*\n/).map(p => p.trim()).filter(p => p !== "");

            const structuredOpsi = [
                `A. ${valA}`,
                `B. ${valB}`,
                `C. ${valC}`,
                `D. ${valD}`
            ];

            const updatedObject = {
                nomor, mapel, stimulus: stimulusArray, soal: soalText, opsi: structuredOpsi, jawaban
            };

            if (idxVal !== "") {
                questions[parseInt(idxVal)] = updatedObject;
            } else {
                questions.push(updatedObject);
            }

            questions.sort((a, b) => a.nomor - b.nomor);

            localStorage.setItem('tka_literasi_questions', JSON.stringify(questions));
            showModal("Soal Tersimpan", "Perubahan butir soal tersimpan sukses ke database lokal.", "success", "Oke", "Tutup", null, null);
            
            clearEditorForm();
            renderSoalEditorList();
        }

        function deleteSoalClick(idx) {
            showModal(
                "Hapus Soal?", 
                `Apakah Anda yakin ingin menghapus Soal Nomor ${questions[idx].nomor} ini dari database?`, 
                "danger", 
                "Hapus Permanen", 
                "Batal", 
                () => {
                    questions.splice(idx, 1);
                    localStorage.setItem('tka_literasi_questions', JSON.stringify(questions));
                    renderSoalEditorList();
                    showToast("Soal berhasil terhapus!");
                }, 
                null
            );
        }

        function resetQuestionsToDefault() {
            showModal(
                "Reset Database Soal?", 
                "Tindakan ini akan memulihkan butir soal standar bawaan program.", 
                "warning", 
                "Kembalikan Standar", 
                "Batal", 
                () => {
                    questions = [...DEFAULT_QUESTIONS];
                    localStorage.setItem('tka_literasi_questions', JSON.stringify(questions));
                    renderSoalEditorList();
                    showToast("Soal telah di-reset ke standar.");
                }, 
                null
            );
        }

        function clearAllData() {
            showModal(
                "Reset Semua Hasil Ujian?", 
                "Langkah ini menghapus permanen seluruh riwayat hasil peserta ujian siswa dari dashboard lokal Anda.", 
                "danger", 
                "Hapus Semua", 
                "Batal", 
                () => {
                    localStorage.setItem('tka_literasi_submissions', JSON.stringify([]));
                    renderTeacherPesertaTable();
                    renderRekapButirCards();
                    renderDifficultyAnalysis();
                    renderAnswerMatrix();
                    showToast("Semua riwayat hasil ujian telah dibersihkan.");
                }, 
                null
            );
        }
    </script>
</body>
</html>
