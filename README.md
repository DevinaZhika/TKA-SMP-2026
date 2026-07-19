<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TKA Adventure - Game Edukasi Modern</title>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;600;700;800&family=Poppins:wght@400;500;600;700&display=swap" rel="stylesheet">
    <!-- Tailwind CSS untuk Layouting Cepat & Glassmorphism -->
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <!-- GSAP untuk Animasi Perjalanan Peta yang Halus -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
    <!-- Canvas Confetti untuk Efek Victory Akhir -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <!-- Chart.js untuk Dashboard Guru -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    
    <style>
        body {
            font-family: 'Nunito', 'Poppins', sans-serif;
            overflow-x: hidden;
            background: linear-gradient(180deg, #bae6fd 0%, #e0f2fe 40%, #f0fdf4 100%);
        }
        .glass-panel {
            background: rgba(255, 255, 255, 0.75);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.5);
        }
        .text-glow {
            text-shadow: 0 0 10px rgba(59, 130, 246, 0.5);
        }
        /* Animasi Awan Bergerak Perlahan */
        @keyframes moveClouds {
            0% { transform: translateX(-10%); }
            100% { transform: translateX(110%); }
        }
        .animate-cloud-slow {
            animation: moveClouds 60s linear infinite;
        }
        .animate-cloud-fast {
            animation: moveClouds 35s linear infinite;
        }
        /* Gaya Highlighter Stabilo Kuning Bersih murni tanpa box/border aneh */
        .hl-active ::selection {
            background-color: rgba(250, 204, 21, 0.5) !important;
            color: inherit;
        }
        .hl-active *::selection {
            background-color: rgba(250, 204, 21, 0.5) !important;
            color: inherit;
        }
        /* Custom Scrollbar Ringan */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f5f9;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 9999px;
        }
    </style>
</head>
<body class="min-h-screen relative text-slate-800">

    <!-- ======================================================== -->
    <!-- BACKGROUND ANIMASI BERLAPIS (PARALLAX GAME ENVIRONMENT) -->
    <!-- ======================================================== -->
    <div class="fixed inset-0 pointer-events-none z-0 overflow-hidden">
        <!-- Layer 1: Sinar Matahari / Sunburst Gradasi di pojok kanan atas -->
        <div class="absolute top-0 right-0 w-[500px] h-[500px] bg-amber-200/30 rounded-full filter blur-3xl opacity-60 transform translate-x-1/4 -translate-y-1/4"></div>
        
        <!-- Layer 2: Awan-Awan Bergerak Vektor SVG -->
        <div class="absolute top-[10%] left-0 w-32 opacity-40 animate-cloud-slow">
            <svg viewBox="0 0 100 40" fill="#ffffff"><path d="M20 30c-5 0-9-4-9-9s4-9 9-9c1 0 2 0 3 .2C25 7 30 4 36 4c8 0 14 6 15 13.3 2-.8 4-1.3 6-1.3 7 0 13 6 13 13s-6 13-13 13H20z"/></svg>
        </div>
        <div class="absolute top-[22%] left-0 w-48 opacity-25 animate-cloud-fast" style="animation-delay: -15s;">
            <svg viewBox="0 0 100 40" fill="#ffffff"><path d="M20 30c-5 0-9-4-9-9s4-9 9-9c1 0 2 0 3 .2C25 7 30 4 36 4c8 0 14 6 15 13.3 2-.8 4-1.3 6-1.3 7 0 13 6 13 13s-6 13-13 13H20z"/></svg>
        </div>

        <!-- Floating Math & Science Icons (Background Vibe) -->
        <div class="absolute top-1/4 left-10 text-sky-300/40 text-5xl font-extrabold select-none">√x</div>
        <div class="absolute top-1/3 right-12 text-indigo-300/30 select-none animate-bounce" style="animation-duration: 6s;">
            <svg class="w-16 h-16" fill="currentColor" viewBox="0 0 24 24"><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm1 17h-2v-2h2v2zm2.07-7.75l-.9.92C13.45 12.9 13 13.5 13 15h-2v-.5c0-1.1.45-2.1 1.17-2.83l1.24-1.26c.37-.36.59-.86.59-1.41 0-1.1-.9-2-2-2s-2 .9-2 2H7c0-2.76 2.24-5 5-5s5 2.24 5 5c0 1.04-.42 1.99-1.07 2.75z"/></svg>
        </div>
        <div class="absolute bottom-1/3 left-16 text-emerald-300/30 select-none">
            <svg class="w-12 h-12" fill="currentColor" viewBox="0 0 24 24"><path d="M7 2v11h3v9l7-12h-4l4-8z"/></svg>
        </div>

        <!-- Layer 3-5: Perbukitan & Vegetasi Bawah Tanah Sederhana Menggunakan Gradasi CSS Bentuk Gelombang -->
        <div class="absolute bottom-0 left-0 right-0 h-44 bg-gradient-to-t from-emerald-600/20 to-transparent clip-path-hill opacity-70"></div>
        <div class="absolute bottom-0 left-0 right-0 h-28 bg-gradient-to-t from-green-500/30 to-transparent rounded-t-[100px] transform translate-y-6"></div>
    </div>

    <!-- ======================================================== -->
    <!-- HEADER NAVIGASI GAME ATAS                                -->
    <!-- ======================================================== -->
    <header class="sticky top-0 z-50 px-4 py-3 bg-slate-900 text-white shadow-xl border-b-4 border-indigo-600 flex justify-between items-center">
        <div class="flex items-center gap-3">
            <div class="w-10 h-10 bg-indigo-500 rounded-xl flex items-center justify-content-center shadow-lg transform rotate-3">
                <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.747 0 3.332.477 4.5 1.253v13C19.832 18.477 18.247 18 16.5 18c-1.746 0-3.332.477-4.5 1.253"></path></svg>
            </div>
            <div>
                <h1 class="font-black text-xl tracking-wider uppercase bg-gradient-to-r from-amber-400 to-orange-400 bg-clip-text text-transparent">TKA Adventure</h1>
            </div>
        </div>
        <div class="flex items-center gap-4">
            <!-- Audio Toggle Control -->
            <button id="btn-audio-toggle" class="bg-slate-800 hover:bg-slate-700 px-3 py-1.5 rounded-lg text-xs font-bold flex items-center gap-2 border border-slate-700 cursor-pointer transition active:scale-95">
                <span id="audio-icon">🔊</span> <span id="audio-text">Sound ON</span>
            </button>
            <div id="badge-container" class="hidden md:flex bg-indigo-950 px-3 py-1 rounded-full border border-indigo-800 items-center gap-2">
                <span class="text-sm">🏅 Rank:</span>
                <span id="txt-badge-rank" class="text-xs font-black uppercase text-amber-400">Explorer</span>
            </div>
            <!-- Global Timer Box -->
            <div id="game-timer-wrapper" class="hidden bg-rose-600 px-4 py-1.5 rounded-xl border-b-4 border-rose-800 font-extrabold text-base tracking-widest text-white shadow-inner animate-pulse">
                ⏰ <span id="global-timer-display">120:00:00</span>
            </div>
            <button id="nav-btn-siswa" class="bg-indigo-600 px-3 py-1.5 rounded-lg text-xs font-bold transition active:scale-95 hidden">Siswa</button>
            <button id="nav-btn-guru" onclick="switchPortalView('guru')" class="bg-slate-800 hover:bg-slate-700 border border-slate-700 px-3 py-1.5 rounded-lg text-xs font-bold text-slate-300 cursor-pointer flex items-center gap-1">👤 Portal Guru</button>
        </div>
    </header>

    <!-- CONTAINER UTAMA APLIKASI -->
    <main class="relative z-10 max-w-7xl mx-auto px-4 py-6">

        <!-- ======================================================== -->
        <!-- PORTAL 1: HALAMAN LOGIN / MENU GAME SISWA                 -->
        <!-- ======================================================== -->
        <section id="panel-siswa-login" class="block max-w-xl mx-auto mt-6">
            <div class="glass-panel rounded-3xl p-8 shadow-2xl border-b-8 border-slate-300 text-center relative overflow-hidden">
                
                <!-- ILUSTRASI VEKTOR FLAT CUSTOM: PETUALANG DI DEPAN GERBANG -->
                <div class="flex justify-center mb-6">
                    <svg class="w-64 h-52 filter drop-shadow-md transform hover:scale-105 transition duration-300" viewBox="0 0 240 200" xmlns="http://www.w3.org/2000/svg">
                        <!-- Langit Mini Belakang -->
                        <circle cx="120" cy="110" r="75" fill="#f0fdfa"/>
                        <path d="M75 120 C90 90, 150 90, 165 120 Z" fill="#e0f2fe" opacity="0.6"/>
                        <!-- Blueprint Dashed Arc Matematika -->
                        <path d="M60 130 A 70 70 0 0 1 180 130" fill="none" stroke="#93c5fd" stroke-width="2" stroke-dasharray="4 4"/>
                        <circle cx="120" cy="60" r="3" fill="#3b82f6"/>
                        
                        <!-- GERBANG BATU (TKA ADVENTURE ARCH) -->
                        <rect x="50" y="100" width="16" height="75" rx="3" fill="#475569"/>
                        <rect x="174" y="100" width="16" height="75" rx="3" fill="#475569"/>
                        <!-- Top Plinth Gerbang -->
                        <path d="M44 100 L196 100 L184 85 L56 85 Z" fill="#334155"/>
                        <!-- Plakat Lengkung Biru Utama -->
                        <path d="M50 85 Q120 45 190 85" fill="none" stroke="#1d4ed8" stroke-width="12" stroke-linecap="round"/>
                        <!-- Teks Papan Gerbang -->
                        <path id="archTextPath" d="M54 82 Q120 48 186 82" fill="none" stroke="transparent"/>
                        <text font-family="'Poppins', sans-serif" font-size="8" font-weight="900" fill="#ffffff" text-anchor="middle">
                            <textPath href="#archTextPath" startOffset="50%">TKA ADVENTURE</textPath>
                        </text>
                        
                        <!-- Bintang Sparkle Kejayaan -->
                        <path d="M68 90 L70 94 L74 95 L70 96 L68 100 L66 96 L62 95 L66 94 Z" fill="#fbbf24"/>
                        <path d="M172 88 L174 92 L178 93 L174 94 L172 98 L170 94 L166 93 L170 92 Z" fill="#22d3ee"/>

                        <!-- KARAKTER PETUALANG (FLAT DESIGN) -->
                        <!-- Kaki & Sepatu -->
                        <rect x="106" y="165" width="10" height="15" fill="#1e293b"/>
                        <rect x="124" y="165" width="10" height="15" fill="#1e293b"/>
                        <rect x="102" y="176" width="15" height="6" rx="2" fill="#0f172a"/>
                        <rect x="123" y="176" width="15" height="6" rx="2" fill="#0f172a"/>
                        <!-- Celana -->
                        <rect x="106" y="150" width="28" height="18" fill="#475569"/>
                        <!-- Tubuh / Baju Dinas Hijau Penjelajah -->
                        <rect x="100" y="115" width="40" height="38" rx="4" fill="#065f46"/>
                        <rect x="110" y="115" width="4" height="38" fill="#047857"/> <!-- Garis Kancing -->
                        <circle cx="112" cy="125" r="1.5" fill="#fbbf24"/>
                        <circle cx="112" cy="135" r="1.5" fill="#fbbf24"/>
                        <!-- Kantong Baju -->
                        <rect x="104" y="122" width="5" height="6" fill="#047857"/>
                        <rect x="131" y="122" width="5" height="6" fill="#047857"/>

                        <!-- Leher & Kepala -->
                        <rect x="114" y="108" width="12" height="8" fill="#fdba74"/>
                        <circle cx="120" cy="95" r="16" fill="#fdba74"/>
                        <!-- Rambut & Muka -->
                        <path d="M104 90 Q120 80 136 90 Q120 86 104 90" fill="#78350f"/>
                        <circle cx="113" cy="95" r="2" fill="#0f172a"/> <!-- Mata Kiri -->
                        <circle cx="127" cy="95" r="2" fill="#0f172a"/> <!-- Mata Kanan -->
                        <path d="M116 102 Q120 106 124 102" fill="none" stroke="#78350f" stroke-width="2" stroke-linecap="round"/> <!-- Senyum -->

                        <!-- Topi Petualang (Explorer Hat) -->
                        <ellipse cx="120" cy="82" rx="26" ry="4" fill="#b45309"/> <!-- Pinggiran Topi -->
                        <path d="M104 81 C104 70, 136 70, 136 81 Z" fill="#d97706"/> <!-- Kubah Topi -->
                        <rect x="105" y="78" width="30" height="3" fill="#78350f"/> <!-- Pita Sabuk Topi -->

                        <!-- TANGAN KIRI MEMELUK BUKU MATEMATIKA -->
                        <path d="M140 120 Q152 125 146 138" fill="none" stroke="#fdba74" stroke-width="6" stroke-linecap="round"/>
                        <!-- Buku Merah Tua -->
                        <rect x="144" y="124" width="16" height="22" rx="2" transform="rotate(15 144 124)" fill="#991b1b"/>
                        <rect x="148" y="123" width="11" height="22" rx="1" transform="rotate(15 144 124)" fill="#f87171"/> <!-- Aksen Cover -->
                        <line x1="152" y1="134" x2="158" y2="136" stroke="#ffffff" stroke-width="2"/> <!-- Lambang Simbol Buku -->
                        
                        <!-- TANGAN KANAN MEMEGANG JANGKA (KOMPAS MATEMATIKA) -->
                        <path d="M100 120 Q86 126 92 140" fill="none" stroke="#fdba74" stroke-width="6" stroke-linecap="round"/>
                        <!-- Vektor Jangka Perak -->
                        <path d="M90 136 L84 152 M90 136 L96 152" stroke="#94a3b8" stroke-width="2" stroke-linecap="round"/>
                        <circle cx="90" cy="136" r="2" fill="#475569"/>
                        <circle cx="84" cy="152" r="1" fill="#3b82f6"/> <!-- Ujung Pensil Biru Jangka -->
                    </svg>
                </div>

                <h2 class="text-3xl font-extrabold tracking-tight text-indigo-950 mb-2">🏆 TKA Adventure</h2>
                <p class="text-sm text-slate-500 font-medium mb-6">Selesaikan seluruh tantangan untuk mencapai garis akhir.</p>
                
                <div class="space-y-4 text-left max-w-sm mx-auto">
                    <div>
                        <label class="block text-xs font-bold text-slate-600 uppercase tracking-wider mb-1">Nama Lengkap</label>
                        <input type="text" id="game-input-nama" class="w-full px-4 py-3 rounded-xl bg-white/90 border-2 border-slate-200 font-semibold focus:outline-none focus:border-indigo-500 shadow-inner text-base transition-colors" placeholder="Masukkan nama petualang...">
                    </div>
                    
                    <div class="grid grid-cols-2 gap-4">
                        <div>
                            <label class="block text-xs font-bold text-slate-600 uppercase tracking-wider mb-1">Kelas Ujian</label>
                            <select id="game-input-kelas" class="w-full px-4 py-3 rounded-xl bg-white/90 border-2 border-slate-200 font-semibold focus:outline-none focus:border-indigo-500 shadow-inner transition-colors">
                                <option value="">-- Pilih --</option>
                                <option value="9A">Kelas 9-A</option>
                                <option value="9B">Kelas 9-B</option>
                                <option value="9C">Kelas 9-C</option>
                                <option value="9D">Kelas 9-D</option>
                                <option value="9E">Kelas 9-E</option>
                                <option value="9F">Kelas 9-F</option>
                                <option value="9G">Kelas 9-G</option>
                                <option value="9H">Kelas 9-H</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-xs font-bold text-slate-600 uppercase tracking-wider mb-1">No Absen</label>
                            <input type="number" id="game-input-absen" min="1" max="50" class="w-full px-4 py-3 rounded-xl bg-white/90 border-2 border-slate-200 font-semibold focus:outline-none focus:border-indigo-500 shadow-inner transition-colors" placeholder="Absen">
                        </div>
                    </div>
                </div>

                <!-- Petunjuk Box Minimalis -->
                <div class="mt-6 text-left max-w-sm mx-auto p-4 bg-amber-50 rounded-2xl border border-amber-200/70 text-xs text-amber-900 leading-relaxed">
                    <h4 class="font-bold mb-1">📋 Petunjuk:</h4>
                    Siswa akan menjawab soal terintegrasi berurutan. Klik tombol ragu-ragu jika masih belum yakin. Jawaban tersimpan otomatis secara berkala.
                </div>

                <button id="game-btn-start" class="mt-6 px-8 py-4 bg-gradient-to-r from-amber-500 via-orange-500 to-yellow-500 text-white font-black text-lg rounded-2xl shadow-xl border-b-4 border-orange-700 uppercase tracking-widest hover:brightness-110 active:scale-95 transition transform cursor-pointer w-full max-w-sm animate-pulse">
                    Mulai Berpetualang 🚀
                </button>
            </div>
        </section>

        <!-- ======================================================== -->
        <!-- PORTAL 2: ADVENTURE MAP (PETA JALUR PERSINGGAHAN SOAL)   -->
        <!-- ======================================================== -->
        <section id="panel-siswa-map" class="hidden max-w-4xl mx-auto">
            <div class="glass-panel rounded-3xl p-6 shadow-xl mb-6 flex flex-col items-center">
                <div class="w-full flex justify-between items-center border-b border-slate-200 pb-3 mb-4">
                    <div>
                        <h3 class="font-black text-xl text-slate-900">🗺️ Peta Perjalanan</h3>
                        <p class="text-xs text-slate-500">Pilih salah satu nomor node level untuk berteleportasi ke soal.</p>
                    </div>
                    <button id="btn-map-to-exam" class="px-5 py-2.5 bg-indigo-600 text-white font-bold text-sm rounded-xl border-b-4 border-indigo-800 shadow-md hover:bg-indigo-500 active:scale-95 transition cursor-pointer">
                        Masuk Level Aktif ➔
                    </button>
                </div>

                <!-- Canvas / Jalur Kontainer Peta -->
                <div class="w-full bg-sky-950/10 rounded-2xl p-8 relative overflow-x-auto min-h-[300px] border border-slate-200 shadow-inner flex items-center justify-center">
                    <div id="map-track-container" class="relative w-[800px] h-[160px] mx-auto">
                        <!-- SVG Jalur Penghubung Melengkung Relatif -->
                        <svg class="absolute inset-0 w-full h-full pointer-events-none" id="svg-map-line">
                            <path id="quest-path" d="" fill="none" stroke="#6366f1" stroke-width="6" stroke-dasharray="10 6" stroke-linecap="round" opacity="0.6"/>
                        </svg>

                        <!-- Node-node petualangan akan disuntikkan secara dinamis di sini -->
                        <div id="map-nodes-layer" class="absolute inset-0 z-10 pointer-events-auto"></div>

                        <!-- Karakter Avatar Mini Berjalan di Atas Jalur -->
                        <div id="map-avatar" class="absolute w-10 h-10 z-20 pointer-events-none transform -translate-x-1/2 -translate-y-1/2 transition-all duration-300">
                            <!-- SVG Mini Karakter Penjelajah Helm Oranye -->
                            <svg viewBox="0 0 40 40" class="w-full h-full filter drop-shadow">
                                <circle cx="20" cy="20" r="14" fill="#fdba74"/>
                                <path d="M6 20 C6 10, 34 10, 34 20 Z" fill="#ea580c"/>
                                <rect x="12" y="14" width="16" height="3" fill="#1e293b" rx="1"/>
                                <circle cx="16" cy="22" r="2" fill="#0f172a"/>
                                <circle cx="24" cy="22" r="2" fill="#0f172a"/>
                                <path d="M17 27 Q20 30 23 27" fill="none" stroke="#9a3412" stroke-width="2"/>
                            </svg>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- ======================================================== -->
        <!-- PORTAL 3: SCREEN DISPLAY SOAL (LEVEL MISSION CARD)       -->
        <!-- ======================================================== -->
        <section id="panel-siswa-ujian" class="hidden">
            
            <!-- Soal Progress Top Bar -->
            <div class="glass-panel rounded-2xl p-4 shadow-md mb-6 flex flex-col md:flex-row justify-between items-center gap-4 border-b-4 border-slate-300">
                <div class="flex items-center gap-3 w-full md:w-auto">
                    <div class="bg-indigo-600 text-white font-black px-4 py-2 rounded-xl text-sm border-b-2 border-indigo-900 shadow">
                        MISSION <span id="lbl-mission-current">1</span> / <span id="lbl-mission-total">5</span>
                    </div>
                    <div class="text-sm font-bold text-slate-600">
                        Mapel: <span id="lbl-mission-mapel" class="text-indigo-700 bg-indigo-50 px-2 py-0.5 rounded-md font-extrabold text-xs">Matematika</span>
                    </div>
                </div>

                <!-- Bar Progress Dengan Mini Avatar Berjalan -->
                <div class="relative w-full md:w-1/2 bg-slate-200 h-5 rounded-full shadow-inner border border-slate-300 overflow-visible">
                    <div id="exam-progress-bar" class="bg-gradient-to-r from-indigo-500 to-emerald-500 h-full rounded-full transition-all duration-300" style="width: 20%;"></div>
                    <!-- Mini Token Karakter di Atas Progress Bar -->
                    <div id="exam-progress-token" class="absolute top-1/2 -translate-y-1/2 -ml-3 transition-all duration-300 pointer-events-none" style="left: 20%;">
                        🏃‍♂️
                    </div>
                </div>

                <div>
                    <button id="btn-back-to-map" class="px-4 py-1.5 bg-slate-800 hover:bg-slate-700 text-white rounded-xl text-xs font-bold border border-slate-700 transition cursor-pointer">
                        🗺️ Lihat Peta
                    </button>
                </div>
            </div>

            <!-- Main Split-Screen Layout (Khas PISA/ANBK) -->
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-6 items-start">
                
                <!-- Kolom Kiri: Teks Stimulus Panjang / Studi Kasus Literasi (Span 2) -->
                <div class="lg:col-span-2 glass-panel rounded-3xl p-6 shadow-xl border-b-4 border-slate-300 min-h-[300px] flex flex-col justify-between">
                    <div>
                        <div class="flex justify-between items-center border-b border-slate-200 pb-2 mb-4">
                            <h4 class="font-extrabold text-base text-slate-800 uppercase tracking-wide">📖 Lembar Stimulus Soal</h4>
                            <!-- Fitur Stabilo Kuning -->
                            <div class="flex items-center gap-2">
                                <span class="text-xs font-bold text-slate-500">Mode Stabilo:</span>
                                <button id="btn-toggle-stabilo" onclick="toggleStabiloMode()" class="px-3 py-1 bg-amber-400 text-slate-900 text-xs font-black rounded-lg shadow-sm border border-amber-500 cursor-pointer active:scale-95 transition">
                                    🟡 Stabilo Kuning
                                </button>
                            </div>
                        </div>

                        <!-- Konten teks bacaan / Soal Utama -->
                        <div id="game-box-stimulus" class="hl-active text-base md:text-lg text-slate-800 leading-relaxed font-medium select-text whitespace-pre-line">
                            Memuat naskah misi petualangan...
                        </div>
                    </div>

                    <!-- Tombol Navigasi Bawah -->
                    <div class="flex justify-between items-center mt-8 border-t border-slate-100 pt-4">
                        <button id="game-btn-prev" class="px-5 py-3 bg-slate-200 hover:bg-slate-300 text-slate-700 font-bold rounded-xl border-b-4 border-slate-400 disabled:opacity-30 disabled:cursor-not-allowed transition active:scale-95 cursor-pointer">
                            ◀ Sebelumnya
                        </button>
                        
                        <!-- Tombol Ragu-Ragu -->
                        <button id="game-btn-ragu" class="px-6 py-3 bg-amber-500 hover:bg-amber-400 text-white font-extrabold rounded-xl border-b-4 border-amber-700 transition active:scale-95 cursor-pointer text-sm">
                            🤔 Ragu-Ragu
                        </button>

                        <button id="game-btn-next" class="px-5 py-3 bg-indigo-600 hover:bg-indigo-500 text-white font-bold rounded-xl border-b-4 border-indigo-800 transition active:scale-95 cursor-pointer">
                            Selanjutnya ▶
                        </button>
                        <button id="game-btn-submit" class="hidden px-6 py-3 bg-rose-600 hover:bg-rose-500 text-white font-black rounded-xl border-b-4 border-rose-800 shadow-lg animate-bounce cursor-pointer">
                            🏁 Selesai Misi
                        </button>
                    </div>
                </div>

                <!-- Kolom Kanan: Pilihan Jawaban & Grid Status Ujian -->
                <div class="space-y-6">
                    <!-- Opsi Kelompok Jawaban Berbentuk Tombol Game -->
                    <div class="glass-panel rounded-3xl p-6 shadow-xl border-b-4 border-slate-300">
                        <h4 class="font-extrabold text-sm text-slate-500 uppercase tracking-wider mb-4">🎯 Pilihlah Jawaban Anda:</h4>
                        <div id="game-box-options" class="space-y-3">
                            <!-- Opsi Tombol Dimuat Secara Dinamis Melalui Javascript -->
                        </div>
                    </div>

                    <!-- Info Siswa & Status Panel Nomor Mini -->
                    <div class="glass-panel rounded-3xl p-5 shadow-md text-xs text-slate-600 space-y-3 border border-slate-200">
                        <div class="border-b border-slate-200 pb-2">
                            <p><strong>Petualang:</strong> <span id="lbl-status-nama">-</span> (<span id="lbl-status-kelas">-</span>)</p>
                        </div>
                        <div>
                            <p class="font-bold mb-2 uppercase text-slate-500 text-[10px] tracking-widest">Indikator Petualangan:</p>
                            <div class="grid grid-cols-5 gap-2" id="game-grid-nav-box">
                                <!-- Kotak mini nomor ujian dinamis -->
                            </div>
                        </div>
                    </div>
                </div>

            </div>
        </section>

        <!-- ======================================================== -->
        <!-- PORTAL 4: KOTAK HASIL AKHIR RECOMPENSE (SCORE BOARD)    -->
        <!-- ======================================================== -->
        <section id="panel-siswa-hasil" class="hidden max-w-lg mx-auto mt-10">
            <div class="glass-panel rounded-3xl p-8 shadow-2xl text-center border-t-8 border-indigo-600 relative overflow-hidden">
                <div class="text-6xl mb-3">🎉</div>
                <h2 class="text-3xl font-black text-slate-900 mb-1">Misi Selesai!</h2>
                <p class="text-sm text-slate-500 font-medium mb-6">Hasil catatan jurnal petualangan Anda berhasil direkam.</p>

                <div class="bg-slate-900 text-white rounded-2xl p-6 text-left shadow-inner space-y-3 border-b-4 border-slate-950">
                    <p class="text-xs text-slate-400 uppercase tracking-wider">Identitas Karakter</p>
                    <div class="text-base font-bold border-b border-slate-800 pb-2 mb-2">
                        <p>Nama: <span id="res-nama" class="text-indigo-400">-</span></p>
                        <p>Kelas: <span id="res-kelas" class="text-indigo-400">-</span></p>
                    </div>

                    <p class="text-xs text-slate-400 uppercase tracking-wider">Pencapaian Ujian</p>
                    <div class="space-y-1 text-sm font-semibold">
                        <p>Jumlah Jawaban Benar : <span id="res-benar" class="text-emerald-400 font-bold">0</span></p>
                        <p>Jumlah Jawaban Salah : <span id="res-salah" class="text-rose-400 font-bold">0</span></p>
                    </div>
                    
                    <div class="pt-3 border-t border-slate-800 text-center">
                        <p class="text-xs text-slate-400 uppercase tracking-wider mb-1">Skor Akhir</p>
                        <div class="text-5xl font-black text-amber-400 tracking-wider" id="res-skor">0</div>
                    </div>
                </div>

                <p class="mt-6 text-xs text-slate-400">*Halaman rekapitulasi mandiri. Kunci jawaban dan pembahasan tidak dipublikasikan.</p>
            </div>
        </section>

        <!-- ======================================================== -->
        <!-- PORTAL 5: DASHBOARD KHUSUS GURU (TIDAK BERTEMA GAME)     -->
        <!-- ======================================================== -->
        <section id="panel-guru-core" class="hidden">
            <div class="bg-white rounded-2xl p-6 shadow-xl border border-slate-200">
                
                <!-- Login Box Guru -->
                <div id="guru-login-card" class="max-w-md mx-auto py-8 text-center">
                    <h3 class="text-2xl font-bold text-slate-800 mb-4">🔐 Autentikasi Dashboard Guru</h3>
                    <div class="mb-4 text-left">
                        <label class="block text-sm font-semibold text-slate-600 mb-1">Masukkan Sandi Rahasia</label>
                        <input type="password" id="txt-pass-guru" class="w-full px-4 py-2 border border-slate-300 rounded-xl font-medium focus:outline-none focus:border-indigo-600 shadow-inner">
                    </div>
                    <button onclick="prosesLoginGuru()" class="w-full py-3 bg-slate-900 hover:bg-slate-800 text-white font-bold rounded-xl shadow cursor-pointer transition">
                        Masuk Dashboard Guru
                    </button>
                </div>

                <!-- Konten Utama Dashboard Guru setelah Login -->
                <div id="guru-dashboard-content" class="hidden space-y-6">
                    <div class="flex flex-col md:flex-row justify-between items-center border-b border-slate-200 pb-4">
                        <div>
                            <h2 class="text-2xl font-black text-slate-900">📊 Analisis Hasil Belajar Siswa (TKA SMP)</h2>
                            <p class="text-xs text-slate-500">Sinkronisasi data terintegrasi real-time dari Google Sheets.</p>
                        </div>
                        <div class="flex items-center gap-2 mt-3 md:mt-0">
                            <button onclick="fetchDataDariSheets()" class="px-4 py-2 bg-indigo-600 hover:bg-indigo-500 text-white text-xs font-bold rounded-xl shadow cursor-pointer">🔄 Segarkan Data</button>
                            <button onclick="resetDataLocalLengkap()" class="px-4 py-2 bg-rose-600 hover:bg-rose-500 text-white text-xs font-bold rounded-xl shadow cursor-pointer">⚠️ Reset Penyimpanan</button>
                            <button onclick="switchPortalView('siswa')" class="px-4 py-2 bg-slate-200 hover:bg-slate-300 text-slate-700 text-xs font-bold rounded-xl shadow cursor-pointer">➔ Portal Siswa</button>
                        </div>
                    </div>

                    <!-- Pilihan Tab Navigasi Dashboard -->
                    <div class="flex border-b border-slate-200 gap-2 overflow-x-auto">
                        <button class="px-4 py-2 text-sm font-bold text-indigo-600 border-b-2 border-indigo-600 focus:outline-none" id="btn-tab-1" onclick="switchTabGuru(1)">1. Daftar Peserta</button>
                        <button class="px-4 py-2 text-sm font-medium text-slate-600 hover:text-indigo-600 focus:outline-none" id="btn-tab-2" onclick="switchTabGuru(2)">2. Rekap Jawaban / Nomor</button>
                        <button class="px-4 py-2 text-sm font-medium text-slate-600 hover:text-indigo-600 focus:outline-none" id="btn-tab-3" onclick="switchTabGuru(3)">3. Analisis Butir Soal</button>
                        <button class="px-4 py-2 text-sm font-medium text-slate-600 hover:text-indigo-600 focus:outline-none" id="btn-tab-4" onclick="switchTabGuru(4)">4. Matriks Jawaban Siswa</button>
                    </div>

                    <!-- TAB KONTEN GURU 1: DAFTAR SELURUH PESERTA -->
                    <div id="panel-tab-guru-1" class="block">
                        <div class="overflow-x-auto">
                            <table class="w-full text-left border-collapse text-sm">
                                <thead>
                                    <tr class="bg-slate-100 border-b border-slate-200 text-slate-700 font-bold">
                                        <th class="p-3">Nama Lengkap</th>
                                        <th class="p-3">Kelas</th>
                                        <th class="p-3 text-center">No Absen</th>
                                        <th class="p-3">Tanggal Ujian</th>
                                        <th class="p-3">Jam Mulai</th>
                                        <th class="p-3">Jam Selesai</th>
                                        <th class="p-3">Durasi</th>
                                        <th class="p-3 text-center cursor-pointer bg-indigo-50 text-indigo-700" onclick="sortDataSiswaBerdasarkanSkor()">Skor Akhir (Click ↕)</th>
                                    </tr>
                                </thead>
                                <tbody id="table-body-peserta" class="divide-y divide-slate-100">
                                    <tr><td colspan="8" class="p-4 text-center text-slate-400">Belum ada lembar jawab masuk.</td></tr>
                                </tbody>
                            </table>
                        </div>
                    </div>

                    <!-- TAB KONTEN GURU 2: REKAP JAWABAN PER NOMOR SOAL -->
                    <div id="panel-tab-guru-2" class="hidden">
                        <div id="grid-rekap-distribusi-jawaban" class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <!-- Injeksi Dinamis Berdasarkan Hasil -->
                        </div>
                    </div>

                    <!-- TAB KONTEN GURU 3: TABEL ANALISIS SOAL & GRAFIK -->
                    <div id="panel-tab-guru-3" class="hidden space-y-6">
                        <div class="overflow-x-auto">
                            <table class="w-full text-left border-collapse text-sm">
                                <thead>
                                    <tr class="bg-slate-100 border-b border-slate-200 font-bold">
                                        <th class="p-3">Nomor Soal</th>
                                        <th class="p-3">Mata Pelajaran</th>
                                        <th class="p-3 text-emerald-600">Siswa Benar</th>
                                        <th class="p-3 text-rose-600">Siswa Salah</th>
                                        <th class="p-3">Persentase Benar</th>
                                        <th class="p-3">Persentase Salah</th>
                                    </tr>
                                </thead>
                                <tbody id="table-body-analisis-kesulitan" class="divide-y divide-slate-100">
                                    <!-- Diurutkan dari yang terbanyak salah -->
                                </tbody>
                            </table>
                        </div>
                        <div class="bg-slate-50 p-4 rounded-xl border border-slate-200 h-[350px] relative">
                            <canvas id="guruChartAnalisis"></canvas>
                        </div>
                    </div>

                    <!-- TAB KONTEN GURU 4: REKAP MATRIKS JAWABAN SISWA -->
                    <div id="panel-tab-guru-4" class="hidden">
                        <div class="overflow-x-auto">
                            <table class="w-full text-left border-collapse text-xs">
                                <thead>
                                    <tr id="table-head-matriks" class="bg-slate-100 border-b border-slate-200 font-bold">
                                        <th class="p-3 min-w-[150px]">Nama Peserta</th>
                                        <!-- Angka nomor dimasukkan lewat JS -->
                                    </tr>
                                </thead>
                                <tbody id="table-body-matriks" class="divide-y divide-slate-100">
                                    <!-- Matriks ✔ dan huruf opsi -->
                                </tbody>
                            </table>
                        </div>
                    </div>

                </div>
            </div>
        </section>

    </main>

    <!-- ======================================================== -->
    <!-- KUSTOM INTERAKTIF MODAL POPUP (SPRING ANIMATION MECHANIC) -->
    <!-- ======================================================== -->
    <div id="game-custom-modal" class="fixed inset-0 z-50 flex items-center justify-center bg-slate-950/60 opacity-0 pointer-events-none transition-opacity duration-200 p-4">
        <div id="game-modal-box" class="glass-panel w-full max-w-sm rounded-3xl p-6 text-center shadow-2xl border-b-8 border-indigo-900 transform scale-75 transition-transform duration-300">
            <h3 id="game-modal-title" class="text-2xl font-black text-slate-900 mb-2">Pemberitahuan</h3>
            <p id="game-modal-desc" class="text-sm text-slate-600 font-semibold mb-6">Isi deskripsi modal di sini.</p>
            <div class="flex gap-3 justify-center" id="game-modal-actions">
                <button id="game-modal-btn-cancel" class="px-5 py-2.5 bg-slate-200 text-slate-700 font-bold rounded-xl cursor-pointer">Batal</button>
                <button id="game-modal-btn-confirm" class="px-5 py-2.5 bg-rose-600 text-white font-black rounded-xl border-b-4 border-rose-800 cursor-pointer">Lanjutkan</button>
            </div>
        </div>
    </div>

    <!-- Footer Hak Cipta Minimalis -->
    <footer class="text-center py-6 text-xs text-slate-400 font-medium select-none relative z-10">
        &copy; 2026 CBT TKA SMP
    </footer>

    <!-- ======================================================== -->
    <!-- LOGIKA CORE ENGINE CONFIG & JAVASCRIPT SYSTEM            -->
    <!-- ======================================================== -->
    <script>
        // 1. GLOBAL CONFIGURATION DATABASE & CREDENTIAL
        const CONFIG = {
            API_URL: "https://script.google.com/macros/s/AKfycbxxxxxxxxx/exec", // Ganti dengan URL deployment Web App Apps Script Anda
            TEACHER_PASSWORD: "adminTKA2026"
        };

        // 2. STATE VARIABEL UJIAN & AUDIO GAME
        let bankSoal = [];
        let indexSoalAktif = 0;
        let lembarJawabSiswa = {}; 
        let statusRaguSiswa = {}; 
        let durasiDetikUjian = 120 * 60; // 120 Menit total global
        let intervalTimerGlobal = null;
        let waktuMulaiUjian = null;
        let modeStabiloAktif = false;
        let databaseGuruSiswa = [];
        let sortGuruAscending = false;
        let instanceGrafikGuru = null;
        let soundSystemEnabled = true;

        // WEB AUDIO API SYNTHESIZER (8-Bit Retro Sound Generator Bebas Resource Eksternal)
        const audioContext = new (window.AudioContext || window.webkitAudioContext)();
        function playSoundEffect(type) {
            if (!soundSystemEnabled) return;
            try {
                const osc = audioContext.createOscillator();
                const gain = audioContext.createGain();
                osc.connect(gain);
                gain.connect(audioContext.destination);

                const now = audioContext.currentTime;

                if (type === 'click') {
                    osc.type = 'sine';
                    osc.frequency.setValueAtTime(400, now);
                    osc.frequency.exponentialRampToValueAtTime(800, now + 0.08);
                    gain.gain.setValueAtTime(0.3, now);
                    gain.gain.linearRampToValueAtTime(0.01, now + 0.08);
                    osc.start(now);
                    osc.stop(now + 0.08);
                } else if (type === 'level') {
                    osc.type = 'triangle';
                    osc.frequency.setValueAtTime(300, now);
                    osc.frequency.linearRampToValueAtTime(600, now + 0.15);
                    gain.gain.setValueAtTime(0.2, now);
                    gain.gain.linearRampToValueAtTime(0.01, now + 0.15);
                    osc.start(now);
                    osc.stop(now + 0.15);
                } else if (type === 'reward') {
                    osc.type = 'square';
                    osc.frequency.setValueAtTime(523.25, now); // C5
                    osc.frequency.setValueAtTime(659.25, now + 0.08); // E5
                    osc.frequency.setValueAtTime(783.99, now + 0.16); // G5
                    osc.frequency.setValueAtTime(1046.50, now + 0.24); // C6
                    gain.gain.setValueAtTime(0.15, now);
                    gain.gain.linearRampToValueAtTime(0.01, now + 0.4);
                    osc.start(now);
                    osc.stop(now + 0.4);
                } else if (type === 'victory') {
                    osc.type = 'sine';
                    osc.frequency.setValueAtTime(261.63, now); // C4
                    osc.frequency.linearRampToValueAtTime(1000, now + 0.8);
                    gain.gain.setValueAtTime(0.2, now);
                    gain.gain.linearRampToValueAtTime(0.01, now + 1.0);
                    osc.start(now);
                    osc.stop(now + 1.0);
                }
            } catch (e) { console.log("Audio not supported yet."); }
        }

        // INITIALIZER KETIKA DOM SELESAI DI-LOAD
        window.addEventListener("DOMContentLoaded", async () => {
            // Audio switch handler
            document.getElementById("btn-audio-toggle").addEventListener("click", () => {
                soundSystemEnabled = !soundSystemEnabled;
                document.getElementById("audio-icon").textContent = soundSystemEnabled ? "🔊" : "🔇";
                document.getElementById("audio-text").textContent = soundSystemEnabled ? "Sound ON" : "Sound OFF";
            });

            // Ambil berkas JSON Soal
            try {
                const response = await fetch("questions.json");
                bankSoal = await response.json();
            } catch (err) {
                // Mockup soal default jika questions.json tidak ditemukan
                bankSoal = [
                    { "nomor": 1, "mapel": "Matematika", "soal": "Perhatikan denah petualangan. Skala peta adalah 1 : 20.000. Jika jarak pos 1 ke pos 2 pada peta adalah 7 cm, berapakah jarak sebenarnya dalam satuan kilometer?", "opsi": ["1,4 km", "14 km", "0,14 km", "140 km"], "jawaban": "A" },
                    { "nomor": 2, "mapel": "Matematika", "soal": "Seorang penjelajah gua memiliki persediaan beras untuk 8 orang selama 15 hari. Jika anggota tim bertambah menjadi 10 orang, maka persediaan makanan tersebut akan habis dalam waktu...", "opsi": ["12 hari", "10 hari", "14 hari", "9 hari"], "jawaban": "A" },
                    { "nomor": 3, "mapel": "Matematika", "soal": "Hasil perhitungan dari ekspresi aljabar 4(2x - 3) - 2(x + 5) adalah...", "opsi": ["6x - 22", "6x - 2", "8x - 22", "6x + 2"], "jawaban": "A" },
                    { "nomor": 4, "mapel": "Matematika", "soal": "Sebuah menara pandang berbentuk tabung memiliki diameter 7 meter dan tinggi 10 meter. Berapakah volume ruang udara di dalam menara tersebut? (Gunakan pi = 22/7)", "opsi": ["385 m³", "770 m³", "1.540 m³", "220 m³"], "jawaban": "A" },
                    { "nomor": 5, "mapel": "Matematika", "soal": "Nilai rata-rata tes kemampuan akademik kelompok A yang beranggotakan 4 siswa adalah 80. Jika digabung dengan Andi yang mendapat skor 90, berapakah nilai rata-rata gabungan sekarang?", "opsi": ["82", "84", "85", "81"], "jawaban": "A" }
                ];
            }

            // Validasi Status Penyimpanan Caching Browser
            if (localStorage.getItem("tka_game_submitted") === "true") {
                renderTampilanHasilAkhir(JSON.parse(localStorage.getItem("tka_game_student_result")));
                return;
            }
            if (localStorage.getItem("tka_game_running") === "true") {
                restoreSesiGameSiswa();
            }

            // Tombol Mulai Aksi
            document.getElementById("game-btn-start").addEventListener("click", triggerMulaiGameCBT);
            document.getElementById("btn-map-to-exam").addEventListener("click", () => {
                playSoundEffect('click');
                switchPortalView('ujian');
            });
            document.getElementById("btn-back-to-map").addEventListener("click", () => {
                playSoundEffect('click');
                switchPortalView('map');
            });

            // Navigasi Pindah Level Soal
            document.getElementById("game-btn-next").addEventListener("click", () => pindahMisiSoal(indexSoalAktif + 1));
            document.getElementById("game-btn-prev").addEventListener("click", () => pindahMisiSoal(indexSoalAktif - 1));
            document.getElementById("game-btn-ragu").addEventListener("click", toggleStatusRaguJawaban);
            document.getElementById("game-btn-submit").addEventListener("click", validasiSebelumKumpulMisi);
        });

        // FUNGSI INTI LOGIN & STATE MANAGEMENT GAME
        function triggerMulaiGameCBT() {
            playSoundEffect('reward');
            const nama = document.getElementById("game-input-nama").value.trim();
            const kelas = document.getElementById("game-input-kelas").value;
            const absen = document.getElementById("game-input-absen").value.trim();

            if (!nama || !kelas || !absen) {
                openCustomModal("Data Tidak Lengkap", "Silakan ketik nama, pilih kelas, dan nomor absen untuk memulai petualangan Anda!", false);
                return;
            }

            waktuMulaiUjian = new Date();
            lembarJawabSiswa = {};
            statusRaguSiswa = {};
            indexSoalAktif = 0;

            // Simpan State Ke Cache Cepat
            localStorage.setItem("tka_student_nama", nama);
            localStorage.setItem("tka_student_kelas", kelas);
            localStorage.setItem("tka_student_absen", absen);
            localStorage.setItem("tka_student_start", waktuMulaiUjian.toISOString());
            localStorage.setItem("tka_game_running", "true");
            localStorage.setItem("tka_game_answers", JSON.stringify(lembarJawabSiswa));
            localStorage.setItem("tka_game_ragu", JSON.stringify(statusRaguSiswa));
            localStorage.setItem("tka_game_duration", durasiDetikUjian);

            inisialisasiDashboardUjianSiswa(nama, kelas, absen);
            mulaiTimerMundurGlobal();
            switchPortalView('map');
        }

        function restoreSesiGameSiswa() {
            const nama = localStorage.getItem("tka_student_nama");
            const kelas = localStorage.getItem("tka_student_kelas");
            const absen = localStorage.getItem("tka_student_absen");
            waktuMulaiUjian = new Date(localStorage.getItem("tka_student_start"));
            lembarJawabSiswa = JSON.parse(localStorage.getItem("tka_game_answers")) || {};
            statusRaguSiswa = JSON.parse(localStorage.getItem("tka_game_ragu")) || {};
            durasiDetikUjian = parseInt(localStorage.getItem("tka_game_duration")) || (120 * 60);

            inisialisasiDashboardUjianSiswa(nama, kelas, absen);
            mulaiTimerMundurGlobal();
            switchPortalView('map');
        }

        function inisialisasiDashboardUjianSiswa(nama, kelas, absen) {
            document.getElementById("lbl-status-nama").textContent = nama;
            document.getElementById("lbl-status-kelas").textContent = kelas;
            document.getElementById("game-timer-wrapper").classList.remove("hidden");
            
            document.getElementById("lbl-mission-total").textContent = bankSoal.length;

            renderAdventureMapTrack();
            renderGridNomorKecilUjian();
            tampilkanKontenMisiSoal(indexSoalAktif);
        }

        function mulaiTimerMundurGlobal() {
            if (intervalTimerGlobal) clearInterval(intervalTimerGlobal);
            
            updateDisplayTimerUI();
            intervalTimerGlobal = setInterval(() => {
                durasiDetikUjian--;
                localStorage.setItem("tka_game_duration", durasiDetikUjian);
                updateDisplayTimerUI();

                if (durasiDetikUjian <= 0) {
                    clearInterval(intervalTimerGlobal);
                    forceSubmitOtomatisSelesaiUjian();
                }
            }, 1000);
        }

        function updateDisplayTimerUI() {
            const h = Math.floor(durasiDetikUjian / 3600);
            const m = Math.floor((durasiDetikUjian % 3600) / 60);
            const s = durasiDetikUjian % 60;
            document.getElementById("global-timer-display").textContent = 
                `${h.toString().padStart(2,'0')}:${m.toString().padStart(2,'0')}:${s.toString().padStart(2,'0')}`;
        }

        // SWAP VIEW MANAGER (SPA PATTERN)
        function switchPortalView(target) {
            document.getElementById("panel-siswa-login").classList.add("hidden");
            document.getElementById("panel-siswa-map").classList.add("hidden");
            document.getElementById("panel-siswa-ujian").classList.add("hidden");
            document.getElementById("panel-siswa-hasil").classList.add("hidden");
            document.getElementById("panel-guru-core").classList.add("hidden");

            if (target === 'siswa') document.getElementById("panel-siswa-login").classList.remove("hidden");
            else if (target === 'map') {
                document.getElementById("panel-siswa-map").classList.remove("hidden");
                reanimateAvatarPositionOnMap();
            }
            else if (target === 'ujian') document.getElementById("panel-siswa-ujian").classList.remove("hidden");
            else if (target === 'hasil') document.getElementById("panel-siswa-hasil").classList.remove("hidden");
            else if (target === 'guru') document.getElementById("panel-guru-core").classList.remove("hidden");
        }

        // ENGINE PETA ADVENTURE (DYNAMIC GSAP QUEST PATH)
        function renderAdventureMapTrack() {
            const nodeLayer = document.getElementById("map-nodes-layer");
            nodeLayer.innerHTML = "";
            
            const totalNodes = bankSoal.length;
            const containerWidth = 800;
            let pathD = `M 40 80`;

            for (let i = 0; i < totalNodes; i++) {
                const ratio = i / (totalNodes - 1 || 1);
                const x = 40 + ratio * (containerWidth - 100);
                const y = 80 + Math.sin(i * 1.5) * 50; // Gelombang melengkung sinusoidal game

                if (i > 0) pathD += ` L ${x} ${y}`;

                // Buat Node Elemen Lingkaran
                const node = document.createElement("button");
                node.style.left = `${x}px`;
                node.style.top = `${y}px`;
                node.className = `absolute w-9 h-9 rounded-full font-black text-xs border-2 shadow-md transform -translate-x-1/2 -translate-y-1/2 cursor-pointer transition flex items-center justify-center pointer-events-auto select-none `;
                node.textContent = bankSoal[i].nomor;

                // Hitung Status Pewarnaan Node Berdasarkan Jawaban
                updateSingleNodeColor(node, bankSoal[i].nomor, i);

                node.addEventListener("click", () => {
                    playSoundEffect('click');
                    pindahMisiSoal(i);
                    switchPortalView('ujian');
                });

                nodeLayer.appendChild(node);
            }

            // Garis Finish Bendera Vektor di Ujung Akhir Jalur
            const finishRatio = 1;
            const fx = 40 + finishRatio * (containerWidth - 100) + 35;
            const fy = 80 + Math.sin((totalNodes - 1) * 1.5) * 50 - 15;
            const flag = document.createElement("div");
            flag.style.left = `${fx}px`;
            flag.style.top = `${fy}px`;
            flag.className = "absolute text-2xl transform -translate-x-1/2 -translate-y-1/2 select-none pointer-events-none";
            flag.innerHTML = "🏁";
            nodeLayer.appendChild(flag);

            document.getElementById("quest-path").setAttribute("d", pathD);
        }

        function updateSingleNodeColor(nodeElement, nomorSoal, idx) {
            nodeElement.classList.remove("bg-white", "bg-emerald-600", "bg-amber-500", "text-slate-800", "text-white", "ring-4", "ring-indigo-600", "animate-pulse");
            
            if (idx === indexSoalAktif) {
                nodeElement.classList.add("ring-4", "ring-indigo-600", "animate-pulse");
            }

            if (statusRaguSiswa[nomorSoal]) {
                nodeElement.className += " bg-amber-500 text-white border-amber-700 shadow-amber-400/50";
            } else if (lembarJawabSiswa[nomorSoal]) {
                nodeElement.className += " bg-emerald-600 text-white border-emerald-800 shadow-emerald-500/40";
            } else {
                nodeElement.className += " bg-white text-slate-800 border-slate-300";
            }
        }

        function reanimateAvatarPositionOnMap() {
            const totalNodes = bankSoal.length;
            const containerWidth = 800;
            const ratio = indexSoalAktif / (totalNodes - 1 || 1);
            const targetX = 40 + ratio * (containerWidth - 100);
            const targetY = 80 + Math.sin(indexSoalAktif * 1.5) * 50;

            gsap.to("#map-avatar", {
                x: targetX,
                y: targetY,
                duration: 0.6,
                ease: "back.out(1.7)"
            });
        }

        // INTERAKSI SOAL BERBASIS LEVEL CARD MISSION
        function tampilkanKontenMisiSoal(index) {
            if (index < 0 || index >= bankSoal.length) return;
            indexSoalAktif = index;

            const data = bankSoal[indexSoalAktif];
            document.getElementById("lbl-mission-current").textContent = indexSoalAktif + 1;
            document.getElementById("lbl-mission-mapel").textContent = data.mapel;
            document.getElementById("game-box-stimulus").innerHTML = `<strong>Pertanyaan Nomor ${data.nomor}:</strong><br>${data.soal}`;

            // Render Opsi Berbentuk Tombol Game Tanpa Bocoran Benar/Salah
            const boxOptions = document.getElementById("game-box-options");
            boxOptions.innerHTML = "";
            
            const abjad = ["A", "B", "C", "D"];
            data.opsi.forEach((opsiText, i) => {
                const charCode = abjad[i];
                const btn = document.createElement("button");
                btn.className = "w-full text-left p-4 rounded-2xl border-2 font-bold transition flex items-center gap-3 cursor-pointer group transform active:scale-[0.98] ";
                
                // Cek status kecocokan pilihan untuk mewarnai tombol (Berubah menjadi Hijau Emerald Lembut saat Terpilih)
                if (lembarJawabSiswa[data.nomor] === charCode) {
                    btn.className += " bg-emerald-50 border-emerald-500 text-emerald-900 shadow-md ring-2 ring-emerald-500/30 scale-[1.01] font-extrabold";
                } else {
                    btn.className += " bg-white/80 hover:bg-slate-50 border-slate-200 text-slate-800 hover:border-indigo-300 hover:shadow";
                }

                btn.innerHTML = `
                    <span class="w-8 h-8 rounded-xl flex items-center justify-center text-xs font-black transition-colors ${lembarJawabSiswa[data.nomor] === charCode ? 'bg-emerald-600 text-white' : 'bg-slate-100 group-hover:bg-indigo-600 group-hover:text-white text-slate-500'}">${charCode}</span>
                    <span class="text-sm tracking-wide flex-1">${opsiText}</span>
                `;

                btn.addEventListener("click", () => {
                    pilihJawabanOpsiMisi(data.nomor, charCode);
                });
                boxOptions.appendChild(btn);
            });

            // Sinkronisasi Visibilitas Aksi Navigasi Tombol
            document.getElementById("game-btn-prev").disabled = (indexSoalAktif === 0);
            if (indexSoalAktif === bankSoal.length - 1) {
                document.getElementById("game-btn-next").classList.add("hidden");
                document.getElementById("game-btn-submit").classList.remove("hidden");
            } else {
                document.getElementById("game-btn-next").classList.remove("hidden");
                document.getElementById("game-btn-submit").classList.add("hidden");
            }

            // Sync Ragu Button visual indicator state
            const rBtn = document.getElementById("game-btn-ragu");
            if (statusRaguSiswa[data.nomor]) {
                rBtn.className = "px-6 py-3 bg-amber-600 text-white font-black rounded-xl border-b-4 border-amber-950 transition cursor-pointer text-sm shadow-inner";
                rBtn.textContent = "🤔 Ragu-Ragu (ON)";
            } else {
                rBtn.className = "px-6 py-3 bg-amber-500 hover:bg-amber-400 text-white font-extrabold rounded-xl border-b-4 border-amber-700 transition cursor-pointer text-sm shadow";
                rBtn.textContent = "🤔 Ragu-Ragu";
            }

            // Update bar progress linier
            const progressPercent = ((indexSoalAktif + 1) / bankSoal.length) * 100;
            document.getElementById("exam-progress-bar").style.width = `${progressPercent}%`;
            document.getElementById("exam-progress-token").style.left = `${progressPercent}%`;

            renderGridNomorKecilUjian();
            renderAdventureMapTrack();
        }

        function pilihJawabanOpsiMisi(nomorSoal, pilihanHuruf) {
            playSoundEffect('click');
            lembarJawabSiswa[nomorSoal] = pilihanHuruf;
            
            // Auto Save ke Cache Browser
            localStorage.setItem("tka_game_answers", JSON.stringify(lembarJawabSiswa));
            
            // Jika siswa menjawab yakin, secara otomatis hilangkan flag ragu-ragu
            if (statusRaguSiswa[nomorSoal]) {
                statusRaguSiswa[nomorSoal] = false;
                localStorage.setItem("tka_game_ragu", JSON.stringify(statusRaguSiswa));
            }

            // REWARD POPUP GIMMICK: Setiap 10 nomor soal berhasil diisi
            const totalTerjawab = Object.keys(lembarJawabSiswa).length;
            if (totalTerjawab > 0 && totalTerjawab % 10 === 0 && !localStorage.getItem(`reward_milestone_${totalTerjawab}`)) {
                localStorage.setItem(`reward_milestone_${totalTerjawab}`, "true");
                playSoundEffect('reward');
                openCustomModal("LEVEL COMPLETE! 🌟", `Luar biasa! Anda telah berhasil menaklukkan ${totalTerjawab} tantangan petualangan akademik. Tetap fokus!`, false);
            }

            tampilkanKontenMisiSoal(indexSoalAktif);
        }

        function toggleStatusRaguJawaban() {
            playSoundEffect('click');
            const num = bankSoal[indexSoalAktif].nomor;
            statusRaguSiswa[num] = !statusRaguSiswa[num];
            localStorage.setItem("tka_game_ragu", JSON.stringify(statusRaguSiswa));
            tampilkanKontenMisiSoal(indexSoalAktif);
        }

        function pindahMisiSoal(targetIndex) {
            if (targetIndex < 0 || targetIndex >= bankSoal.length) return;
            playSoundEffect('level');
            tampilkanKontenMisiSoal(targetIndex);
        }

        function renderGridNomorKecilUjian() {
            const grid = document.getElementById("game-grid-nav-box");
            grid.innerHTML = "";

            bankSoal.forEach((soal, idx) => {
                const box = document.createElement("button");
                box.className = "w-8 h-8 rounded-lg font-bold text-xs border cursor-pointer flex items-center justify-center transition ";
                box.textContent = soal.nomor;

                // Hitung Status Warna Grid Kecil Khas CBT
                if (idx === indexSoalAktif) {
                    box.className += " ring-4 ring-indigo-600 font-black";
                }

                if (statusRaguSiswa[soal.nomor]) {
                    box.className += " bg-amber-500 text-white border-amber-600"; // Ragu-ragu (Oranye)
                } else if (lembarJawabSiswa[soal.nomor]) {
                    box.className += " bg-emerald-600 text-white border-emerald-700"; // Sudah terjawab (Hijau Emerald)
                } else {
                    box.className += " bg-slate-100 text-slate-500 border-slate-200"; // Belum terjawab (Abu-abu)
                }

                box.addEventListener("click", () => pindahMisiSoal(idx));
                grid.appendChild(box);
            });
        }

        // STABILO MODE TOGGLER (MURNI HIGHLIGHT KUNING FLAT BERSIH)
        function toggleStabiloMode() {
            playSoundEffect('click');
            modeStabiloAktif = !modeStabiloAktif;
            const btn = document.getElementById("btn-toggle-stabilo");
            const box = document.getElementById("game-box-stimulus");
            
            if (modeStabiloAktif) {
                btn.className = "px-3 py-1 bg-yellow-500 text-white text-xs font-black rounded-lg shadow-inner border border-yellow-600 cursor-pointer";
                box.classList.add("hl-active");
            } else {
                btn.className = "px-3 py-1 bg-amber-400 text-slate-900 text-xs font-black rounded-lg shadow-sm border border-amber-500 cursor-pointer";
                box.classList.remove("hl-active");
            }
        }

        // VALIDASI SEBELUM KUMPUL MISI AKHIR
        function validasiSebelumKumpulMisi() {
            const total = bankSoal.length;
            const diisi = Object.keys(lembarJawabSiswa).length;
            const bolong = total - diisi;

            // Hitung sisa ragu-ragu
            let jumlahRagu = 0;
            for(let key in statusRaguSiswa) {
                if(statusRaguSiswa[key] === true) jumlahRagu++;
            }

            let textDeskripsi = `Apakah Anda yakin ingin menyelesaikan ekspedisi ujian?<br><strong>Misi diselesaikan: ${diisi} dari ${total} soal.</strong>`;
            
            if (jumlahRagu > 0) {
                textDeskripsi += `<br><span class="text-amber-600 font-bold">⚠️ Perhatian: Anda memiliki ${jumlahRagu} nomor soal yang masih bertanda Ragu-Ragu!</span>`;
            }
            if (bolong > 0) {
                textDeskripsi += `<br><span class="text-rose-600 font-bold">⚠️ Peringatan: Masih ada ${bolong} soal kosong yang terlewat!</span>`;
            }

            openCustomModal("Selesaikan Petualangan?", textDeskripsi, true, () => {
                kalkulasiHasilAkhirDanPostKeSheets();
            });
        }

        function forceSubmitOtomatisSelesaiUjian() {
            openCustomModal("Waktu Ekspedisi Habis!", "Mengunci lembar jawaban secara otomatis dan merekam skor akhir...", false, () => {
                kalkulasiHasilAkhirDanPostKeSheets();
            });
        }

        // SINKRONISASI PENGIRIMAN GOOGLE SHEETS
        async function kalkulasiHasilAkhirDanPostKeSheets() {
            clearInterval(intervalTimerGlobal);
            
            let jumlahBenar = 0;
            let jumlahSalah = 0;

            bankSoal.forEach(soal => {
                const ans = lembarJawabSiswa[soal.nomor];
                if (ans === soal.jawaban) jumlahBenar++;
                else jumlahSalah++;
            });

            const skorFinal = Math.round((jumlahBenar / bankSoal.length) * 100);
            const waktuSelesai = new Date();
            const hitungMs = waktuSelesai - waktuMulaiUjian;
            const totalMenit = Math.floor(hitungMs / 60000);
            const totalDetik = Math.floor((hitungMs % 60000) / 1000);
            const durasiString = `${totalMenit} menit ${totalDetik} detik`;

            const nama = localStorage.getItem("tka_student_nama");
            const kelas = localStorage.getItem("tka_student_kelas");
            const absen = localStorage.getItem("tka_student_absen");

            // Bentuk JSON Payload untuk Google Sheets API
            const payload = {
                "Nama": nama,
                "Kelas": kelas,
                "Nomor Absen": absen,
                "Tanggal": waktuSelesai.toLocaleDateString('id-ID'),
                "Jam Mulai": waktuMulaiUjian.toLocaleTimeString('id-ID'),
                "Jam Selesai": waktuSelesai.toLocaleTimeString('id-ID'),
                "Durasi": durasiString,
                "Jumlah Benar": jumlahBenar,
                "Jumlah Salah": jumlahSalah,
                "Skor": skorFinal
            };

            // Masukkan Lembar Jawab tiap-tiap nomor
            bankSoal.forEach(soal => {
                payload[`Jawaban Nomor ${soal.nomor}`] = lembarJawabSiswa[soal.nomor] || "-";
            });

            // Kirim Menggunakan Fetch API Mode Asinkronus no-cors bebas kendala CORS preflight
            try {
                await fetch(CONFIG.API_URL, {
                    method: "POST",
                    mode: "no-cors",
                    body: JSON.stringify(payload)
                });
            } catch (err) { console.error("Sheets sync error:", err); }

            const finalResObj = { nama, kelas, benar: jumlahBenar, salah: jumlahSalah, skor: skorFinal };
            
            localStorage.setItem("tka_game_submitted", "true");
            localStorage.setItem("tka_game_student_result", JSON.stringify(finalResObj));
            
            // Bersihkan flag ujian sedang berjalan
            localStorage.removeItem("tka_game_running");

            // Mainkan Confetti & Suara Menang
            playSoundEffect('victory');
            confetti({ particleCount: 150, spread: 80, origin: { y: 0.6 } });

            renderTampilanHasilAkhir(finalResObj);
        }

        function renderTampilanHasilAkhir(res) {
            document.getElementById("game-timer-wrapper").classList.add("hidden");
            switchPortalView('hasil');

            document.getElementById("res-nama").textContent = res.nama;
            document.getElementById("res-kelas").textContent = res.kelas;
            document.getElementById("res-benar").textContent = res.benar;
            document.getElementById("res-salah").textContent = res.salah;
            document.getElementById("res-skor").textContent = res.skor;
        }

        // REUSABLE SPRING MODAL UI CUSTOM (BEBAS POPUP ALERT DEFAULT BROWSER)
        function openCustomModal(title, desc, showCancel = false, onConfirm = null) {
            const overlay = document.getElementById("game-custom-modal");
            const box = document.getElementById("game-modal-box");
            
            document.getElementById("game-modal-title").textContent = title;
            document.getElementById("game-modal-desc").innerHTML = desc;

            const cBtn = document.getElementById("game-modal-btn-cancel");
            const yBtn = document.getElementById("game-modal-btn-confirm");

            cBtn.style.display = showCancel ? "block" : "none";

            // Klon tombol konfirmasi agar tidak terjadi duplikasi penumpukan event listener
            const newYBtn = yBtn.cloneNode(true);
            yBtn.parentNode.replaceChild(newYBtn, yBtn);

            newYBtn.onclick = () => {
                overlay.classList.remove("opacity-100");
                overlay.classList.add("opacity-0", "pointer-events-none");
                box.classList.remove("scale-100");
                box.classList.add("scale-75");
                if (onConfirm) onConfirm();
            };

            cBtn.onclick = () => {
                overlay.classList.remove("opacity-100");
                overlay.classList.add("opacity-0", "pointer-events-none");
                box.classList.remove("scale-100");
                box.classList.add("scale-75");
            };

            overlay.classList.remove("opacity-0", "pointer-events-none");
            overlay.classList.add("opacity-100");
            box.classList.remove("scale-75");
            box.classList.add("scale-100");
        }


        // ======================================================== -->
        // CORE LOGIKA PORTAL GURU/ADMIN                             -->
        // ======================================================== -->
        function prosesLoginGuru() {
            const pass = document.getElementById("txt-pass-guru").value;
            if (pass === CONFIG.TEACHER_PASSWORD) {
                sessionStorage.setItem("guru_logged_in", "true");
                document.getElementById("guru-login-card").classList.add("hidden");
                document.getElementById("guru-dashboard-content").classList.remove("hidden");
                fetchDataDariSheets();
            } else {
                alert("Kata sandi guru salah!");
            }
        }

        async function fetchDataDariSheets() {
            try {
                const response = await fetch(CONFIG.API_URL);
                databaseGuruSiswa = await response.json();
            } catch(e) {
                // Inisialisasi KOSONG TOTAL sesuai arahan revisi (Tidak ada data dummy tiruan bawaan)
                databaseGuruSiswa = [];
            }
            kalkulasiSeluruhStatistikGuru();
        }

        function resetDataLocalLengkap() {
            if (confirm("Apakah Anda ingin mereset seluruh cache simulasi ujian lokal di peramban ini?")) {
                localStorage.clear();
                sessionStorage.clear();
                alert("Seluruh penyimpanan lokal dibersihkan!");
                location.reload();
            }
        }

        function kalkulasiSeluruhStatistikGuru() {
            renderDaftarPesertaGuru();
            hitungRekapJawabanPerNomorGuru();
            hitungAnalisisKesulitanDanGrafikGuru();
            renderMatriksJawabanSiswaGuru();
        }

        function renderDaftarPesertaGuru() {
            const tbody = document.getElementById("table-body-peserta");
            tbody.innerHTML = "";

            if (databaseGuruSiswa.length === 0) {
                tbody.innerHTML = `<tr><td colspan="8" class="p-4 text-center text-slate-400">Belum ada lembar jawab masuk.</td></tr>`;
                return;
            }

            databaseGuruSiswa.forEach(siswa => {
                const tr = document.createElement("tr");
                tr.innerHTML = `
                    <td class="p-3 font-bold text-slate-900">${siswa["Nama"]}</td>
                    <td class="p-3">${siswa["Kelas"]}</td>
                    <td class="p-3 text-center">${siswa["Nomor Absen"]}</td>
                    <td class="p-3">${siswa["Tanggal"]}</td>
                    <td class="p-3">${siswa["Jam Mulai"]}</td>
                    <td class="p-3">${siswa["Jam Selesai"]}</td>
                    <td class="p-3">${siswa["Durasi"]}</td>
                    <td class="p-3 text-center font-bold text-indigo-700 bg-indigo-50/50">${siswa["Skor"]}</td>
                `;
                tbody.appendChild(tr);
            });
        }

        function sortDataSiswaBerdasarkanSkor() {
            sortGuruAscending = !sortGuruAscending;
            databaseGuruSiswa.sort((a,b) => sortGuruAscending ? (a["Skor"] - b["Skor"]) : (b["Skor"] - a["Skor"]));
            renderDaftarPesertaGuru();
        }

        function hitungRekapJawabanPerNomorGuru() {
            const grid = document.getElementById("grid-rekap-distribusi-jawaban");
            grid.innerHTML = "";

            bankSoal.forEach(soal => {
                let a = 0, b = 0, c = 0, d = 0, kosong = 0;
                let benar = 0, salah = 0;

                databaseGuruSiswa.forEach(siswa => {
                    const jawab = siswa[`Jawaban Nomor ${soal.nomor}`];
                    if (jawab === "A") a++;
                    else if (jawab === "B") b++;
                    else if (jawab === "C") c++;
                    else if (jawab === "D") d++;
                    else kosong++;

                    if (jawab === soal.jawaban) benar++;
                    else salah++;
                });

                const total = databaseGuruSiswa.length;
                const pBenar = total > 0 ? Math.round((benar / total) * 100) : 0;
                const pSalah = total > 0 ? 100 - pBenar : 0;

                const card = document.createElement("div");
                card.className = "bg-slate-50 p-4 rounded-xl border border-slate-200 text-xs space-y-2";
                card.innerHTML = `
                    <h5 class="font-bold text-indigo-900 text-sm">Soal Nomor ${soal.nomor} (${soal.mapel})</h5>
                    <p class="text-slate-600 font-medium">${soal.soal}</p>
                    <ul class="grid grid-cols-2 gap-1 font-semibold text-slate-700">
                        <li>A: ${a} siswa</li>
                        <li>B: ${b} siswa</li>
                        <li>C: ${c} siswa</li>
                        <li>D: ${d} siswa</li>
                    </ul>
                    <div class="bg-white p-2.5 rounded-lg border border-slate-200 space-y-0.5">
                        <p>Jawaban Kunci: <span class="text-emerald-600 font-bold">${soal.jawaban}</span></p>
                        <p>Benar: <strong>${benar}</strong> | Salah: <strong>${salah}</strong></p>
                        <p>Persentase: <span class="text-emerald-600">✔ ${pBenar}%</span> | <span class="text-rose-600">✘ ${pSalah}%</span></p>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        function hitungAnalisisKesulitanDanGrafikGuru() {
            let listAnalisis = [];
            
            bankSoal.forEach(soal => {
                let benar = 0, salah = 0;
                databaseGuruSiswa.forEach(siswa => {
                    if (siswa[`Jawaban Nomor ${soal.nomor}`] === soal.jawaban) benar++;
                    else salah++;
                });

                const total = databaseGuruSiswa.length;
                const pBenar = total > 0 ? Math.round((benar / total) * 100) : 0;
                const pSalah = total > 0 ? 100 - pBenar : 0;

                listAnalisis.push({ nomor: soal.nomor, mapel: soal.mapel, benar, salah, pBenar, pSalah });
            });

            // URUTKAN DARI SOAL PALING BANYAK SALAH HINGGA PALING SEDIKIT SALAH
            listAnalisis.sort((a,b) => b.salah - a.salah);

            const tbody = document.getElementById("table-body-analisis-kesulitan");
            tbody.innerHTML = "";
            listAnalisis.forEach(item => {
                const tr = document.createElement("tr");
                tr.innerHTML = `
                    <td class="p-3 font-bold">Soal No ${item.nomor}</td>
                    <td class="p-3">${item.mapel}</td>
                    <td class="p-3 text-emerald-600 font-bold">${item.benar}</td>
                    <td class="p-3 text-rose-600 font-bold">${item.salah}</td>
                    <td class="p-3 font-semibold">${item.pBenar}%</td>
                    <td class="p-3 font-semibold">${item.pSalah}%</td>
                `;
                tbody.appendChild(tr);
            });

            // Kembalikan ke urutan nomor normal untuk keperluan visualisasi grafik batang
            listAnalisis.sort((a,b) => a.nomor - b.nomor);
            const labels = listAnalisis.map(i => `No ${i.nomor}`);
            const dataB = listAnalisis.map(i => i.benar);
            const dataS = listAnalisis.map(i => i.salah);

            if (instanceGrafikGuru) instanceGrafikGuru.destroy();
            const ctx = document.getElementById("guruChartAnalisis").getContext('2d');
            instanceGrafikGuru = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: labels,
                    datasets: [
                        { label: 'Benar (✔)', data: dataB, backgroundColor: '#10b981' },
                        { label: 'Salah (✘)', data: dataS, backgroundColor: '#ef4444' }
                    ]
                },
                options: { responsive: true,     maintainAspectRatio: false, scales: { y: { beginAtZero: true, ticks: { stepSize: 1 } } } }
            });
        }

        function renderMatriksJawabanSiswaGuru() {
            const trHead = document.getElementById("table-head-matriks");
            const tbody = document.getElementById("table-body-matriks");

            trHead.innerHTML = `<th class="p-3 min-w-[150px]">Nama Peserta</th>`;
            tbody.innerHTML = "";

            bankSoal.forEach(soal => {
                trHead.innerHTML += `<th class="p-3 text-center">No ${soal.nomor}</th>`;
            });

            if (databaseGuruSiswa.length === 0) {
                tbody.innerHTML = `<tr><td class="p-4 text-slate-400 text-center">Data kosong.</td></tr>`;
                return;
            }

            databaseGuruSiswa.forEach(siswa => {
                const tr = document.createElement("tr");
                let htmlSiswa = `<td class="p-3 font-bold text-slate-800">${siswa["Nama"]} <span class="text-[10px] text-slate-400 font-medium">(${siswa["Kelas"]})</span></td>`;
                
                bankSoal.forEach(soal => {
                    const jawab = siswa[`Jawaban Nomor ${soal.nomor}`] || "-";
                    const isBenar = (jawab === soal.jawaban);
                    htmlSiswa += `
                        <td class="p-3 text-center font-semibold">
                            ${jawab} ${isBenar ? '<span class="text-emerald-600 font-black ml-0.5" title="Cocok Kunci">✔</span>' : ''}
                        </td>
                    `;
                });
                tr.innerHTML = htmlSiswa;
                tbody.appendChild(tr);
            });
        }

        function switchTabGuru(index) {
            document.getElementById("panel-tab-guru-1").classList.add("hidden");
            document.getElementById("panel-tab-guru-2").classList.add("hidden");
            document.getElementById("panel-tab-guru-3").classList.add("hidden");
            document.getElementById("panel-tab-guru-4").classList.add("hidden");

            document.getElementById("btn-tab-1").className = "px-4 py-2 text-sm font-medium text-slate-600";
            document.getElementById("btn-tab-2").className = "px-4 py-2 text-sm font-medium text-slate-600";
            document.getElementById("btn-tab-3").className = "px-4 py-2 text-sm font-medium text-slate-600";
            document.getElementById("btn-tab-4").className = "px-4 py-2 text-sm font-medium text-slate-600";

            document.getElementById(`panel-tab-guru-${index}`).classList.remove("hidden");
            const actBtn = document.getElementById(`btn-tab-${index}`);
            actBtn.className = "px-4 py-2 text-sm font-bold text-indigo-600 border-b-2 border-indigo-600 focus:outline-none";
        }
    </script>
</body>
</html>
