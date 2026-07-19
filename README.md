<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TKA Adventure - CBT System</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts Nunito, Poppins & Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Nunito:wght@400;600;700;800;900&family=Poppins:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Chart.js CDN -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- GSAP CDN for smooth animations -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
    <!-- Canvas Confetti CDN -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>

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

        /* Pure flat yellow highlighter (no padding, no curves, no margins) */
        .highlighted-text {
            background-color: rgba(250, 204, 21, 0.65) !important; 
            color: #1e293b !important;
            padding: 0 !important;
            border-radius: 0 !important;
            box-shadow: none !important;
            border: none !important;
        }

        /* Active Option Box (Vibrant green feedback upon selection) */
        .option-card input[type="radio"]:checked + label {
            border-color: #10b981 !important; /* Tailwind emerald-500 */
            background-color: #ecfdf5 !important; /* Tailwind emerald-50 */
            color: #065f46 !important; /* Tailwind emerald-800 */
            box-shadow: 0 4px 15px -1px rgba(16, 185, 129, 0.25) !important;
            transform: scale(1.02);
            transition: all 0.2s ease;
        }
        .option-card input[type="radio"]:checked + label span:first-child {
            background-color: #10b981 !important;
            color: #ffffff !important;
            border-color: #10b981 !important;
        }

        /* Reading Ruler Focus Overlay */
        .ruler-focus-active .reading-stimulus p:not(.focused-line) {
            opacity: 0.15;
            filter: blur(1px);
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
            transform: scale(1.03);
        }
        .game-btn:active {
            transform: scale(0.97);
        }

        /* Dynamic Clouds Move Background */
        @keyframes moveClouds {
            0% { transform: translateX(-10%); }
            50% { transform: translateX(10%); }
            100% { transform: translateX(-10%); }
        }
        .animated-clouds {
            animation: moveClouds 35s ease-in-out infinite;
        }

        /* Slide Transition Engine */
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

        /* Confetti particle setup */
        .confetti-particle {
            position: absolute;
            z-index: 100;
            animation: confettiFall 4s linear forwards;
        }
        @keyframes confettiFall {
            0% { transform: translateY(-50px) rotate(0deg); opacity: 1; }
            100% { transform: translateY(100vh) rotate(360deg); opacity: 0; }
        }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 font-sans min-h-screen flex flex-col justify-between overflow-x-hidden">

    <div class="fixed inset-0 -z-50 overflow-hidden pointer-events-none select-none">
        <!-- Sky Gradient -->
        <div class="absolute inset-0 bg-gradient-to-b from-sky-300 via-blue-100 to-indigo-50"></div>
        
        <!-- Sun Glow -->
        <div class="absolute top-12 right-12 w-48 h-48 rounded-full bg-yellow-200 opacity-20 blur-3xl animate-pulse"></div>
        
        <!-- Cloud Layer 1 -->
        <div class="absolute inset-0 animated-clouds opacity-40">
            <svg class="absolute top-16 left-[5%] w-32 h-12 fill-white opacity-85" viewBox="0 0 100 40"><path d="M10 30 Q15 15 30 20 Q45 10 60 25 Q75 15 90 30 Z"/></svg>
            <svg class="absolute top-36 left-[55%] w-48 h-16 fill-white opacity-90" viewBox="0 0 100 40"><path d="M10 30 Q15 15 30 20 Q45 10 60 25 Q75 15 90 30 Z"/></svg>
        </div>

        <!-- Landscape Backdrop Vectors (Hills) -->
        <svg class="absolute bottom-0 left-0 w-full h-[35vh] fill-emerald-100/30 opacity-70" viewBox="0 0 1440 320" preserveAspectRatio="none">
            <path d="M0,224L120,202.7C240,181,480,139,720,144C960,149,1200,203,1320,229.3L1440,256L1440,320L0,320Z"></path>
        </svg>
        <svg class="absolute bottom-0 left-0 w-full h-[22vh] fill-emerald-200/40 opacity-80" viewBox="0 0 1440 320" preserveAspectRatio="none">
            <path d="M0,256L120,240C240,224,480,192,720,202.7C960,213,1200,267,1320,293.3L1440,320L1440,320L0,320Z"></path>
        </svg>

        <!-- Dynamic Math/Science Floating Vector Icons -->
        <div class="absolute top-1/4 left-10 w-12 h-12 opacity-15 text-brand-800 rotate-12 animate-bounce"><i class="fa-solid fa-square-root-variable text-5xl"></i></div>
        <div class="absolute top-1/3 right-16 w-12 h-12 opacity-15 text-brand-800 -rotate-12 animate-bounce"><i class="fa-solid fa-atom text-5xl"></i></div>
        <div class="absolute bottom-1/3 left-1/4 w-12 h-12 opacity-10 text-brand-800 rotate-45"><i class="fa-solid fa-calculator text-5xl"></i></div>
    </div>

    <header class="bg-gradient-to-r from-brand-950 via-blue-950 to-slate-900 border-b border-brand-800 sticky top-0 z-40 shadow-md">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center gap-3">
                <div class="bg-gradient-to-tr from-brand-500 to-cyan-400 text-white p-2.5 rounded-xl flex items-center justify-center shadow-lg shadow-brand-500/20">
                    <i class="fa-solid fa-trophy text-lg"></i>
                </div>
                <div>
                    <h1 class="font-heading font-extrabold text-sm sm:text-base text-white tracking-wide">TKA ADVENTURE</h1>
                </div>
            </div>
            
            <div class="flex items-center gap-2">
                <!-- AUDIO CONTROLLER TOGGLE -->
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

        <!-- MICRO-LOADING SYSTEM OVERLAY -->
        <div id="mission-loader" class="hidden absolute inset-0 z-50 bg-slate-50/90 backdrop-blur-sm flex flex-col items-center justify-center gap-3">
            <div class="w-12 h-12 border-4 border-brand-500 border-t-transparent rounded-full animate-spin"></div>
            <p class="font-heading font-bold text-sm text-brand-950 uppercase tracking-widest animate-pulse">Loading Next Mission...</p>
        </div>

        <!-- MOTIVATIONAL TOAST MILESTONES -->
        <div id="motivation-popup" class="hidden fixed top-24 left-1/2 -translate-x-1/2 z-50 bg-brand-600 border border-brand-400 text-white font-heading font-black px-6 py-4 rounded-3xl shadow-glow-success scale-90 transition-transform duration-300 flex items-center gap-3">
            <span class="text-2xl" id="motivation-emoji">🎉</span>
            <div>
                <h4 class="text-sm tracking-wide" id="motivation-title">Hebat!</h4>
                <p class="text-xs text-brand-100 font-medium font-sans" id="motivation-desc">Kamu menyelesaikan tantangan.</p>
            </div>
        </div>

        <!-- STUDENT LOG GATEWAY (QUEST LOBBY) -->
        <div id="view-student-gate" class="max-w-md mx-auto my-8 bg-white/70 backdrop-blur-md rounded-3xl border border-blue-50 p-6 sm:p-8 shadow-premium slide-fade-in relative overflow-hidden">
            <!-- Game Adventure Visual Elements -->
            <div class="absolute -top-12 -left-12 w-32 h-32 bg-blue-100/50 rounded-full blur-2xl pointer-events-none"></div>
            <div class="absolute -bottom-12 -right-12 w-32 h-32 bg-indigo-100/50 rounded-full blur-2xl pointer-events-none"></div>
            
            <div class="text-center mb-6 z-10 relative">
                <!-- CUSTOM FLAT ILLUSTRATION: ADVENTURER AT THE GATE -->
                <div class="inline-flex mb-4">
                    <svg class="w-64 h-52 mx-auto drop-shadow-xl" viewBox="0 0 300 240" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <!-- BACKGROUND PORTAL ARCH/GATEWAY -->
                        <!-- Left Stone Pillar -->
                        <rect x="40" y="80" width="24" height="140" rx="6" fill="#4B5563" />
                        <rect x="36" y="210" width="32" height="12" rx="3" fill="#1F2937" />
                        <!-- Right Stone Pillar -->
                        <rect x="236" y="80" width="24" height="140" rx="6" fill="#4B5563" />
                        <rect x="232" y="210" width="32" height="12" rx="3" fill="#1F2937" />
                        <!-- Arch Gate Arc -->
                        <path d="M40 90 Q150 10 260 90" stroke="#374151" stroke-width="14" fill="none" stroke-linecap="round" />
                        <!-- Glowing Blue Gate Banner Base -->
                        <path d="M48 85 Q150 18 252 85" stroke="#1D4ED8" stroke-width="24" fill="none" stroke-linecap="round" />
                        <!-- Text on Arch Banner -->
                        <text x="150" y="58" font-family="'Poppins', 'Plus Jakarta Sans', sans-serif" font-weight="900" font-size="12" fill="#FFFFFF" text-anchor="middle" letter-spacing="1.5">TKA ADVENTURE</text>

                        <!-- CHARACTER DETAILED FLAT SHAPE -->
                        <!-- Backpack showing behind shoulder sides -->
                        <rect x="132" y="128" width="36" height="50" rx="8" fill="#D97706" />
                        <circle cx="150" cy="115" r="4" fill="#4B5563" /> 

                        <!-- Boy Body Base & Green Explorer Uniform -->
                        <path d="M128 135 H172 V195 H128 Z" fill="#059669" />
                        <!-- Orange Backpack Straps -->
                        <path d="M134 135 V195 M166 135 V195" stroke="#B45309" stroke-width="4.5" />
                        <!-- Inner Cream T-shirt collar -->
                        <path d="M142 135 L150 145 L158 135" stroke="#FDBA74" stroke-width="3" fill="none" stroke-linecap="round" />

                        <!-- Dark Grey Pants & Walking Boots -->
                        <rect x="134" y="195" width="12" height="22" fill="#374151" />
                        <rect x="154" y="195" width="12" height="22" fill="#374151" />
                        <path d="M130 215 H146 V223 H130 Z" fill="#111827" />
                        <path d="M154 215 H170 V223 H154 Z" fill="#111827" />

                        <!-- Face & Cute Round Hair -->
                        <circle cx="150" cy="116" r="18" fill="#FDBA74" />
                        <path d="M132 116 C132 102 168 102 168 116 Z" fill="#451A03" /> <!-- Dark hair -->
                        
                        <!-- Flat Explorer Hat with Yellow Ribbon -->
                        <path d="M128 102 C128 84, 172 84, 172 102 Z" fill="#92400E" /> <!-- Dome -->
                        <ellipse cx="150" cy="102" rx="30" ry="6" fill="#78350F" /> <!-- Brim -->
                        <rect x="136" y="96" width="28" height="4" fill="#F59E0B" /> <!-- Ribbon -->

                        <!-- Minimalist Flat Eyes & Warm Smile -->
                        <circle cx="144" cy="115" r="2" fill="#111827" />
                        <circle cx="156" cy="115" r="2" fill="#111827" />
                        <path d="M146 122 Q150 126 154 122" stroke="#111827" stroke-width="2" fill="none" stroke-linecap="round" />

                        <!-- Left Hand holding Red Math Book -->
                        <path d="M128 142 Q105 152 112 175" stroke="#FDBA74" stroke-width="8" stroke-linecap="round" fill="none" />
                        <!-- Red Book Graphics with Spine line -->
                        <rect x="94" y="160" width="24" height="32" rx="3" fill="#E11D48" transform="rotate(-15 106 176)" />
                        <rect x="99" y="162" width="19" height="28" fill="#FFFFFF" transform="rotate(-15 106 176)" />
                        <line x1="102" y1="168" x2="114" y2="168" stroke="#E2E8F0" stroke-width="2.5" transform="rotate(-15 106 176)" />
                        <line x1="102" y1="174" x2="114" y2="174" stroke="#E2E8F0" stroke-width="2.5" transform="rotate(-15 106 176)" />
                        <rect x="94" y="160" width="4" height="32" fill="#9F1239" transform="rotate(-15 106 176)" />

                        <!-- Right Hand holding Silver Mathematical Compass (Jangka) -->
                        <path d="M172 142 Q195 152 188 175" stroke="#FDBA74" stroke-width="8" stroke-linecap="round" fill="none" />
                        <!-- Mathematical Divider / Compass Instrument -->
                        <circle cx="192" cy="165" r="3.5" fill="#64748B" /> <!-- Joint -->
                        <line x1="192" y1="165" x2="183" y2="190" stroke="#94A3B8" stroke-width="3.5" stroke-linecap="round" /> <!-- Leg 1 -->
                        <line x1="192" y1="165" x2="201" y2="190" stroke="#94A3B8" stroke-width="3.5" stroke-linecap="round" /> <!-- Leg 2 with Blue pencil -->
                        <line x1="183" y1="190" x2="181" y2="195" stroke="#475569" stroke-width="1.5" /> <!-- Metal Tip -->
                        <line x1="201" y1="190" x2="204" y2="195" stroke="#2563EB" stroke-width="3.5" stroke-linecap="round" /> <!-- Pencil body -->
                        <polygon points="204,195 205,198 202,197" fill="#000000" /> <!-- Pencil tip graphite -->

                        <!-- GAME PARTICLE FLAMBOYANT SPARKLES -->
                        <path d="M85 125 L87 128 L92 130 L87 132 L85 137 L83 132 L78 130 L83 128 Z" fill="#F59E0B" /> <!-- Gold Spark -->
                        <path d="M215 110 L217 113 L222 115 L217 117 L215 122 L213 117 L208 115 L213 113 Z" fill="#06B6D4" /> <!-- Cyan Spark -->
                        <path d="M70 170 A 50 50 0 0 1 100 200" stroke="#BFDBFE" stroke-width="2.5" stroke-dasharray="4,4" fill="none" /> <!-- Blueprint Math Arc -->
                    </svg>
                </div>
                <h2 class="font-heading font-extrabold text-2xl text-brand-950 font-game">🏆 TKA Adventure</h2>
                <p class="text-slate-500 text-sm mt-1 leading-relaxed">Selesaikan seluruh tantangan untuk mencapai garis akhir.</p>
            </div>

            <!-- Path Graphics on Lobby -->
            <div class="h-16 w-full relative mb-6 overflow-hidden bg-slate-50 rounded-2xl border border-slate-100 flex items-center justify-center">
                <!-- Stars and Space Background instead of "Cloud Text Placeholder" -->
                <div class="absolute inset-0 opacity-20 bg-gradient-to-r from-blue-500 to-indigo-600 animate-pulse"></div>
                <div class="absolute left-6 text-brand-500 animate-pulse">
                    <i class="fa-solid fa-rocket text-xl rotate-45"></i>
                </div>
                
                <!-- Adventure Map Line -->
                <div class="w-4/5 h-1 bg-gradient-to-r from-blue-500 to-indigo-500 rounded-full relative flex justify-between items-center">
                    <div class="w-4 h-4 rounded-full bg-brand-600 border-4 border-white shadow animate-ping"></div>
                    <div class="w-3 h-3 rounded-full bg-slate-300 border-2 border-white"></div>
                    <div class="w-3 h-3 rounded-full bg-slate-300 border-2 border-white"></div>
                    <div class="w-3 h-3 rounded-full bg-slate-300 border-2 border-white"></div>
                    <div class="w-6 h-6 rounded-full bg-slate-800 border-2 border-white flex items-center justify-center shadow"><i class="fa-solid fa-flag-checkered text-[10px] text-white"></i></div>
                </div>
            </div>

            <form id="form-login-siswa" onsubmit="startExam(event)" class="space-y-4 z-10 relative">
                <div>
                    <label class="block text-xs font-bold uppercase text-slate-400 mb-1 tracking-wider" for="input-nama">Nama Lengkap</label>
                    <div class="relative">
                        <span class="absolute inset-y-0 left-0 flex items-center pl-3.5 text-slate-400">
                            <i class="fa-solid fa-user text-sm"></i>
                        </span>
                        <input type="text" id="input-nama" required class="w-full pl-10 pr-4 py-2.5 border border-slate-200 rounded-xl focus:ring-2 focus:ring-brand-500 focus:border-brand-500 text-sm font-medium transition bg-white/80" placeholder="Contoh: Andi Wijaya">
                    </div>
                </div>
                
                <div class="grid grid-cols-2 gap-4">
                    <div>
                        <label class="block text-xs font-bold uppercase text-slate-400 mb-1 tracking-wider" for="input-kelas">Kelas</label>
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
                        <label class="block text-xs font-bold uppercase text-slate-400 mb-1 tracking-wider" for="input-absen">Nomor Absen</label>
                        <div class="relative">
                            <span class="absolute inset-y-0 left-0 flex items-center pl-3.5 text-slate-400">
                                <i class="fa-solid fa-hashtag text-sm"></i>
                            </span>
                            <input type="number" id="input-absen" min="1" max="45" required class="w-full pl-10 pr-4 py-2.5 border border-slate-200 rounded-xl focus:ring-2 focus:ring-brand-500 text-sm font-medium transition bg-white/80" placeholder="1">
                        </div>
                    </div>
                </div>

                <div class="p-4 bg-brand-50 border border-brand-100 rounded-2xl text-xs text-brand-900 space-y-1.5">
                    <div class="font-bold flex items-center gap-2 text-brand-800">
                        <i class="fa-solid fa-circle-info text-brand-600"></i> Petunjuk:
                    </div>
                    <p class="leading-relaxed text-slate-600">
                        Gunakan tombol bantuan <strong class="text-brand-700">Stabilo</strong> dan <strong class="text-brand-700">Mistar Fokus</strong> di atas teks bacaan digital untuk mempermudah teknik membaca cepat (*skimming & scanning*).
                    </p>
                </div>

                <button type="submit" class="game-btn w-full py-3.5 px-4 bg-gradient-to-r from-brand-600 to-indigo-600 hover:from-brand-700 hover:to-indigo-700 text-white font-bold rounded-xl shadow-lg shadow-brand-600/20 flex items-center justify-center gap-2 text-sm">
                    🚀 Mulai Petualangan
                </button>
            </form>
        </div>

        <div id="view-student-exam" class="hidden flex flex-col gap-4 slide-fade-in">
            
            <!-- Top Bar Panel: Timer, Progress & Toolbar -->
            <div class="bg-white border border-slate-200 rounded-2xl p-4 shadow-sm flex flex-col gap-4">
                
                <div class="flex flex-col sm:flex-row gap-4 items-center justify-between">
                    <div class="flex items-center gap-3 w-full sm:w-auto">
                        <div class="bg-brand-50 border border-brand-100 px-4 py-2 rounded-xl text-xs w-full sm:w-auto">
                            <span class="text-brand-400 block font-bold uppercase text-[9px] tracking-wider">Petualang Terdaftar</span>
                            <strong id="display-student-name" class="text-brand-950 text-sm">Siswa</strong>
                            <span class="text-brand-600 ml-1 font-semibold">(Kelas <span id="display-student-class">9A</span> / Absen <span id="display-student-absen">01</span>)</span>
                        </div>

                        <!-- Cosmetic Badge Visualizer -->
                        <div class="bg-indigo-950 text-white px-3 py-2 rounded-xl text-xs flex items-center gap-1.5 font-bold shadow-sm">
                            <span id="display-badge-icon">⭐</span> <span id="display-badge-text">Explorer</span>
                        </div>
                    </div>

                    <!-- PROGRESS BAR AND PERCENTAGE -->
                    <div class="flex flex-col w-full sm:w-72">
                        <div class="flex justify-between items-center text-[10px] font-bold text-slate-400 uppercase mb-1">
                            <span id="label-quest-progress">Level Progress</span>
                            <span id="percent-quest-progress" class="text-brand-600 font-extrabold">0%</span>
                        </div>
                        <div class="w-full bg-slate-100 rounded-full h-3 border overflow-hidden">
                            <div id="quest-progress-bar" class="bg-gradient-to-r from-brand-500 to-emerald-500 h-full w-0 transition-all duration-500"></div>
                        </div>
                    </div>

                    <div class="flex items-center gap-3">
                        <div class="text-right">
                            <span class="text-[9px] text-slate-400 block font-bold uppercase tracking-wider">⏳ Sisa Waktu</span>
                            <div id="exam-timer" class="text-base font-mono font-black text-vibrant-rose animate-pulse">02:00:00</div>
                        </div>
                    </div>
                </div>

                <!-- ASSISTIVE READ TOOLBAR -->
                <div class="flex flex-wrap items-center gap-2 bg-slate-50 p-2 rounded-xl border border-slate-200">
                    <span class="text-[10px] font-bold text-slate-400 px-2 uppercase tracking-wide">Bantuan Membaca Cepat:</span>
                    <button onclick="toggleHighlighter()" id="btn-highlighter" class="px-3 py-1.5 text-xs font-semibold rounded-lg bg-white border text-slate-700 hover:bg-brand-50 flex items-center gap-1.5 transition">
                        <i class="fa-solid fa-marker text-brand-500"></i> Stabilo Teks (Kuning)
                    </button>
                    <button onclick="toggleReadingRuler()" id="btn-ruler" class="px-3 py-1.5 text-xs font-semibold rounded-lg bg-white border text-slate-700 hover:bg-brand-50 flex items-center gap-1.5 transition">
                        <i class="fa-solid fa-grip-lines text-brand-500"></i> Mistar Fokus
                    </button>
                    <button onclick="toggleScratchpad()" class="px-3 py-1.5 text-xs font-semibold rounded-lg bg-white border text-slate-700 hover:bg-brand-50 flex items-center gap-1.5 transition">
                        <i class="fa-solid fa-feather-pointed text-brand-500"></i> Papan Coretan
                    </button>
                </div>
            </div>

            <!-- Workspace: Split Screen layout matching standard ANBK/PISA -->
            <div class="grid grid-cols-1 lg:grid-cols-12 gap-4">
                
                <!-- STIMULUS PANEL (Left Side: Paragraf Bacaan) -->
                <div id="panel-stimulus" class="lg:col-span-6 bg-white border border-slate-200 rounded-2xl p-5 shadow-sm flex flex-col justify-between max-h-[600px] overflow-y-auto">
                    <div>
                        <div class="flex items-center justify-between border-b border-slate-100 pb-3 mb-4">
                            <span class="text-xs font-bold text-brand-600 uppercase tracking-wider"><i class="fa-solid fa-file-invoice"></i> Dokumen Stimulus Kasus</span>
                            <span class="text-[10px] bg-brand-50 text-brand-700 px-2.5 py-1 rounded-full font-bold">Quest Challenge</span>
                        </div>
                        
                        <!-- Content Teks Stimulus -->
                        <div id="display-stimulus-container" class="reading-stimulus text-slate-700 text-sm sm:text-base space-y-4 leading-relaxed">
                            <!-- Rendered dynamically -->
                        </div>
                    </div>
                </div>

                <!-- QUESTION & OPTIONS PANEL (Right Side: Quest and Choices) -->
                <div id="panel-soal" class="lg:col-span-6 bg-white border border-slate-200 rounded-2xl p-5 shadow-sm flex flex-col justify-between min-h-[450px]">
                    <div>
                        <div class="flex items-center justify-between border-b border-slate-100 pb-3 mb-4">
                            <span class="px-3 py-1 bg-brand-50 text-brand-700 text-xs font-bold rounded-lg" id="display-mapel">
                                Pelajaran
                            </span>
                            <span class="text-xs font-semibold text-slate-500">
                                Misi <strong id="current-question-num" class="text-brand-600">1</strong> dari <span id="total-questions-num">5</span>
                            </span>
                        </div>

                        <!-- Level Quest / Question Text -->
                        <div class="space-y-4">
                            <h3 class="text-xs uppercase font-extrabold text-slate-400 tracking-wider" id="label-quest-title">Level Challenge</h3>
                            <p id="display-soal-text" class="text-brand-950 font-bold text-sm sm:text-base leading-relaxed">
                                Loading soal...
                            </p>

                            <!-- Choices -->
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
                        
                        <!-- Ragu-ragu Toggle Button -->
                        <button id="btn-doubtful-toggle" onclick="toggleDoubtful()" class="game-btn px-4 py-2.5 text-xs font-bold rounded-xl flex items-center justify-center gap-1.5 transition border border-amber-300 bg-amber-50 text-amber-700 hover:bg-amber-100">
                            <i class="fa-regular fa-square"></i> Ragu-Ragu
                        </button>

                        <button id="btn-next-question" onclick="goToQuestion(currentQuestionIndex + 1)" class="game-btn px-3 sm:px-4 py-2.5 text-xs font-bold text-white bg-brand-600 hover:bg-brand-700 rounded-xl flex items-center gap-1.5 transition shadow">
                            Selanjutnya <i class="fa-solid fa-chevron-right"></i>
                        </button>

                        <button id="btn-finish-exam" onclick="confirmEndExam()" class="game-btn hidden px-5 sm:px-6 py-2.5 text-xs font-bold text-white bg-vibrant-emerald hover:bg-emerald-600 rounded-xl flex items-center gap-1.5 transition shadow-md">
                            <i class="fa-solid fa-paper-plane"></i> Selesai
                        </button>
                    </div>
                </div>

            </div>

            <!-- Bottom Circular Level Badges Panel (Game Map) -->
            <div class="bg-white border border-slate-200 rounded-2xl p-5 shadow-sm">
                <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-3 mb-3">
                    <h4 class="font-heading font-bold text-xs text-brand-950 uppercase tracking-widest">Peta Level Petualangan</h4>
                    <div class="flex flex-wrap items-center gap-4 text-[10px] font-bold uppercase tracking-wider">
                        <div class="flex items-center gap-1.5"><span class="w-3.5 h-3.5 rounded bg-slate-200 border border-slate-300 inline-block"></span> Belum Dibuka</div>
                        <div class="flex items-center gap-1.5"><span class="w-3.5 h-3.5 rounded bg-emerald-600 inline-block"></span> Sudah Dijawab</div>
                        <div class="flex items-center gap-1.5"><span class="w-3.5 h-3.5 rounded bg-amber-500 inline-block"></span> Ragu-Ragu</div>
                    </div>
                </div>
                <!-- Circles mapping grid -->
                <div id="student-grid-indicators" class="flex flex-wrap gap-3">
                    <!-- Dynamic generated circles -->
                </div>
            </div>

        </div>

        <div id="scratchpad-panel" class="hidden fixed right-4 bottom-4 z-50 bg-white border border-brand-100 w-80 rounded-2xl shadow-2xl p-4 space-y-3 slide-fade-in">
            <div class="flex items-center justify-between border-b pb-2">
                <span class="text-xs font-bold text-brand-950 uppercase"><i class="fa-solid fa-feather-pointed text-brand-500"></i> Papan Coretan Digital</span>
                <button onclick="toggleScratchpad()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
            </div>
            
            <div>
                <label class="block text-[10px] uppercase font-bold text-slate-400 mb-1">Coretan Analisis Mandiri</label>
                <textarea id="scratchpad-text" rows="8" class="w-full text-xs p-3 border border-slate-200 rounded-xl focus:ring-2 focus:ring-brand-500 focus:outline-none" placeholder="Tuliskan analisis hitungan atau rangkuman data bacaan Anda di sini..."></textarea>
            </div>
        </div>

        <!-- STUDENT SCORE SCREEN -->
        <div id="view-student-results" class="hidden max-w-lg mx-auto bg-white border border-brand-50 rounded-3xl p-6 sm:p-8 shadow-premium slide-fade-in">
            <div class="text-center mb-6">
                <div class="inline-flex p-4 bg-emerald-50 text-vibrant-emerald rounded-full mb-4 shadow-inner">
                    <i class="fa-solid fa-circle-check text-4xl"></i>
                </div>
                <h2 class="font-heading font-extrabold text-2xl text-brand-950">🎉 Ujian Selesai!</h2>
                <p class="text-slate-500 text-xs mt-1">Hasil petualangan Anda telah berhasil direkam ke database utama secara aman.</p>
            </div>

            <!-- Identity Display Block -->
            <div class="bg-slate-50 rounded-2xl p-4 border border-slate-100 mb-6 space-y-2">
                <div class="flex justify-between text-xs">
                    <span class="text-slate-500">Nama Petualang</span>
                    <strong id="res-student-name" class="text-brand-950">Andi</strong>
                </div>
                <div class="flex justify-between text-xs">
                    <span class="text-slate-500">Kelas / Absen</span>
                    <strong id="res-student-class" class="text-brand-950">9A / 12</strong>
                </div>
            </div>

            <!-- Score board -->
            <div class="bg-brand-50 border border-brand-100 rounded-2xl p-5 text-center space-y-4 shadow-inner mb-6">
                <p class="text-brand-800 text-xs uppercase tracking-widest font-extrabold">Hasil Akhir Petualangan</p>
                
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
                    <span class="text-[11px] text-brand-500 font-semibold uppercase block mb-1">Skor Akhir</span>
                    <div id="res-final-score" class="text-6xl font-black text-brand-600 tracking-tight">00.00</div>
                </div>
            </div>

            <div class="p-3 bg-slate-50 border border-slate-200 rounded-xl text-xs text-slate-500 text-center flex items-center justify-center gap-1.5">
                <i class="fa-solid fa-lock text-slate-400"></i> Kunci jawaban dan pembahasan tidak dipublikasikan untuk menjaga objektivitas tes.
            </div>
        </div>

        <!-- TEACHER AUTHENTICATION BARRIER -->
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
                <p id="error-pwd-msg" class="text-vibrant-rose text-xs text-center font-semibold hidden"><i class="fa-solid fa-circle-exclamation"></i> Password salah, coba lagi!</p>
                <button type="submit" class="game-btn w-full py-2.5 bg-brand-950 hover:bg-slate-900 text-white font-semibold rounded-xl text-sm transition-all duration-150">
                    Masuk ke Dashboard
                </button>
            </form>
        </div>

        <!-- TEACHER DASHBOARD VIEW (COMPREHENSIVE) -->
        <div id="view-teacher-dashboard" class="hidden space-y-6 slide-fade-in">
            
            <!-- Dashboard Subheader Menu -->
            <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between border-b border-slate-200 pb-4 gap-4">
                <div>
                    <h2 class="font-heading font-extrabold text-xl text-brand-950">Dashboard Analisis & Monitor Guru</h2>
                    <p class="text-slate-500 text-xs">Pantau hasil analisis butir soal, matriks jawaban, dan tingkat kesulitan soal secara profesional.</p>
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
                <div class="p-3 bg-brand-50 border border-brand-100 rounded-xl flex items-center gap-2 text-xs text-brand-900 font-semibold">
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
                            <p class="text-[10px] text-slate-400 mt-0.5">Jawaban benar ditandai dengan tanda centang kecil (<span class="text-vibrant-emerald font-bold">✔</span>) untuk memudahkan analisis kualitatif.</p>
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
                            <button onclick="resetQuestionsToDefault()" class="px-3 py-1 bg-brand-50 hover:bg-brand-100 border border-brand-100 text-brand-800 rounded-xl text-xs font-bold transition"><i class="fa-solid fa-rotate-left"></i> Reset ke Standar</button>
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
        <div class="bg-white rounded-3xl border border-brand-100 max-w-sm w-full p-6 shadow-2xl space-y-4">
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

    <!-- JS SCRIPTS LOGIC -->
    <script>
        // WEB AUDIO API SYNTHESIZER (No external sound files, completely client-side)
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
                // Frequency sweep up
                osc.frequency.setValueAtTime(400, this.ctx.currentTime);
                osc.frequency.exponentialRampToValueAtTime(750, this.ctx.currentTime + 0.15);
                gain.gain.setValueAtTime(0.03, this.ctx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.001, this.ctx.currentTime + 0.15);
                osc.start();
                osc.stop(this.ctx.currentTime + 0.15);
            },
            playVictory() {
                if (!this.enabled) return;
                this.init();
                if (this.ctx.state === 'suspended') this.ctx.resume();
                let now = this.ctx.currentTime;
                // Harmonic arpeggio (C Major)
                let notes = [261.63, 329.63, 392.00, 523.25]; // C4, E4, G4, C5
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

        // AUDIO TOGGLE SWITCH HANDLER
        function toggleAudio() {
            GameAudio.enabled = !GameAudio.enabled;
            const btn = document.getElementById('btn-sound-toggle');
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
        // GOOGLE APPS SCRIPT DATABASE ENDPOINT
        const CONFIG = {
            API_URL: "https://script.google.com/macros/s/AKfycbxxxxxxxxx/exec", 
            TEACHER_PASSWORD: "adminTKA2026"
        };

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

        // NO PARTICIPANT INITIAL STATE
        const MOCK_PARTICIPANTS = [];

        // GLOBAL APPLICATION STATE
        let questions = [];
        let currentQuestionIndex = 0;
        let activeStudent = null;
        let examTimerInterval = null;
        let examTimeLeftInSeconds = 120 * 60; // 120 Minutes
        let answersSaved = {};
        let doubtfulSaved = {}; 
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

        // LOADING QUESTS
        async function loadQuestions() {
            try {
                const response = await fetch("questions.json");
                questions = await response.json();
            } catch (err) {
                console.warn("Using self-contained internal quest database.");
                questions = [...DEFAULT_QUESTIONS];
            }
        }

        function loadConfigAndSubmissions() {
            const submissions = localStorage.getItem('tka_literasi_submissions');
            if (!submissions) {
                localStorage.setItem('tka_literasi_submissions', JSON.stringify(MOCK_PARTICIPANTS));
            }
        }
    </script>

    <script>
        // NAVIGATION VIEW ENGINE
        function switchView(viewId) {
            GameAudio.playClick();
            const views = ['student-gate', 'student-exam', 'student-results', 'teacher-login', 'teacher-dashboard'];
            views.forEach(v => {
                const el = document.getElementById(`view-${v}`);
                if (el) el.classList.add('hidden');
            });

            // Update Header Tab status visually
            const tabStudent = document.getElementById('tab-student');
            if (tabStudent) {
                tabStudent.className = "px-3.5 py-2 text-xs sm:text-sm font-semibold rounded-xl transition-all duration-255 " + 
                    (viewId.startsWith('student') ? 'bg-brand-600 text-white shadow-md shadow-brand-500/10' : 'text-brand-200 hover:text-white hover:bg-white/15');
            }
            const tabTeacher = document.getElementById('tab-teacher');
            if (tabTeacher) {
                tabTeacher.className = "px-3.5 py-2 text-xs sm:text-sm font-semibold rounded-xl transition-all duration-255 " + 
                    (viewId.startsWith('teacher') ? 'bg-slate-900 text-white border border-brand-800' : 'text-brand-200 hover:text-white hover:bg-white/15');
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
                btn.className = "px-3 py-1.5 text-xs font-semibold rounded-lg bg-yellow-100 border border-yellow-300 text-yellow-950 flex items-center gap-1.5 transition";
                showToast("Stabilo Aktif: Blok kata/angka di teks kiri untuk menandai!");
            } else {
                btn.className = "px-3 py-1.5 text-xs font-semibold rounded-lg bg-white border text-slate-700 hover:bg-brand-50 flex items-center gap-1.5 transition";
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
                        GameAudio.playClick();
                    }
                };
            } else {
                container.onmouseup = null;
            }
        }

        // Mistar fokus toggle
        function toggleReadingRuler() {
            activeReadingRuler = !activeReadingRuler;
            const btn = document.getElementById('btn-ruler');
            const panel = document.getElementById('panel-stimulus');
            
            if (activeReadingRuler) {
                btn.className = "px-3 py-1.5 text-xs font-semibold rounded-lg bg-brand-600 border border-brand-700 text-white flex items-center gap-1.5 transition shadow";
                panel.classList.add('ruler-focus-active');
                showToast("Mistar Fokus Aktif: Klik baris paragraf agar pandangan terfokus!");
            } else {
                btn.className = "px-3 py-1.5 text-xs font-semibold rounded-lg bg-white border text-slate-700 hover:bg-brand-50 flex items-center gap-1.5 transition";
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
            GameAudio.playClick();
        }

        // SCRATCHPAD UTILITY
        function toggleScratchpad() {
            const panel = document.getElementById('scratchpad-panel');
            panel.classList.toggle('hidden');
        }

        // CUSTOM MODALS SYSTEM (Zero default popups)
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
            toast.innerHTML = `<i class="fa-solid fa-star text-amber-400"></i> ${text}`;
            document.body.appendChild(toast);
            setTimeout(() => { toast.remove(); }, 4000);
        }
    </script>

    <script>
        // STUDENT QUEST INITIATOR
        function startExam(e) {
            e.preventDefault();

            const nama = document.getElementById('input-nama').value.trim();
            const kelas = document.getElementById('input-kelas').value;
            const absen = document.getElementById('input-absen').value.trim();

            if (!nama || !kelas || !absen) {
                showModal("Lengkapi Identitas", "Silakan lengkapi seluruh formulir identitas petualangan.", "warning", "Oke", "Batal", null, null);
                return;
            }

            // Duplication check to enforce single submission TKA rules
            const submissions = JSON.parse(localStorage.getItem('tka_literasi_submissions') || '[]');
            const duplicate = submissions.some(sub => 
                sub.nama.toLowerCase() === nama.toLowerCase() && 
                sub.kelas === kelas && 
                parseInt(sub.absen) === parseInt(absen)
            );

            if (duplicate) {
                showModal(
                    "Identitas Sudah Terpakai", 
                    "Sistem mencatat identitas Anda telah menyelesaikan misi petualangan ini. Satu siswa hanya diperbolehkan mengirim satu kali.", 
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
                showToast("Melanjutkan petualangan yang terputus!");
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

        // GLOBAL COUNTDOWN TIMER
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

                    // AutoSave draft backup to prevent data loss
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

        // MAP GRID NODE GENERATOR (CIRCLES GAME MAP)
        function renderGridIndicators() {
            const container = document.getElementById('student-grid-indicators');
            if (container) {
                container.innerHTML = "";
            }

            questions.forEach((q, idx) => {
                const isAnswered = answersSaved[q.nomor] !== undefined && answersSaved[q.nomor] !== "";
                const isDoubtful = doubtfulSaved[q.nomor] === true;
                const isActive = idx === currentQuestionIndex;

                // Level Node styling
                let btnClass = "w-10 h-10 text-xs font-bold rounded-full transition-all duration-150 flex items-center justify-center border-2 shadow-inner ";
                
                if (isActive) {
                    btnClass += "bg-blue-100 text-brand-800 border-brand-500 ring-4 ring-brand-500/50 scale-105 font-black";
                } else if (isDoubtful) {
                    btnClass += "bg-amber-500 text-white border-amber-400 hover:bg-amber-600";
                } else if (isAnswered) {
                    btnClass += "bg-emerald-700 text-white border-emerald-600 hover:bg-emerald-800";
                } else {
                    btnClass += "bg-slate-200 text-slate-500 border-slate-300 hover:bg-slate-300";
                }

                const btn = document.createElement('button');
                btn.className = btnClass;
                btn.innerText = q.nomor;
                btn.onclick = () => goToQuestion(idx);
                if (container) {
                    container.appendChild(btn);
                }
            });

            // UPDATE PROGRESS BAR
            updateProgress();
        }

        // MILITARY PROGRESS TRACKER & MILESTONES
        function updateProgress() {
            const total = questions.length;
            if (total === 0) return;
            
            let answeredCount = 0;
            questions.forEach(q => {
                if (answersSaved[q.nomor] !== undefined && answersSaved[q.nomor] !== "") {
                    answeredCount++;
                }
            });

            const percent = Math.round((answeredCount / total) * 100);
            const progressBar = document.getElementById('quest-progress-bar');
            const progressText = document.getElementById('percent-quest-progress');
            const progressLabel = document.getElementById('label-quest-progress');

            progressBar.style.width = `${percent}%`;
            progressText.innerText = `${percent}%`;
            progressLabel.innerText = `Misi ${answeredCount} / ${total}`;

            // Update Dynamic Tier badges cosmetically based on percentage
            const badgeIcon = document.getElementById('display-badge-icon');
            const badgeText = document.getElementById('display-badge-text');
            if (percent < 30) {
                badgeIcon.innerText = "⭐";
                badgeText.innerText = "Explorer";
            } else if (percent < 80) {
                badgeIcon.innerText = "🏆";
                badgeText.innerText = "Challenger";
            } else {
                badgeIcon.innerText = "👑";
                badgeText.innerText = "Master";
            }
        }

        // POP MILESTONE MOTIVATIONS
        function checkQuestMilestone(answeredCount) {
            const total = questions.length;
            const ratio = answeredCount / total;

            let trigger = false;
            let title = "Luar Biasa!";
            let desc = `Kamu menyelesaikan ${answeredCount} tantangan.`;
            let emoji = "🎉";

            if (ratio === 0.25 || answeredCount === 10) {
                trigger = true;
                title = "Awal yang Bagus!";
                emoji = "🚀";
            } else if (ratio === 0.50 || answeredCount === 20) {
                trigger = true;
                title = "Hebat!";
                emoji = "⭐";
            } else if (ratio === 0.75 || answeredCount === 30) {
                trigger = true;
                title = "Hampir Selesai!";
                emoji = "🔥";
            } else if (ratio === 1.00) {
                trigger = true;
                title = "Misi Tercapai!";
                emoji = "👑";
            }

            if (trigger) {
                const pop = document.getElementById('motivation-popup');
                document.getElementById('motivation-emoji').innerText = emoji;
                document.getElementById('motivation-title').innerText = title;
                document.getElementById('motivation-desc').innerText = desc;

                pop.classList.remove('hidden');
                setTimeout(() => {
                    pop.classList.add('hidden');
                }, 2000);
            }
        }
    </script>

    <script>
        // DISPLAY QUEST PAGE
        function showQuestion(index) {
            if (index < 0 || index >= questions.length) return;
            currentQuestionIndex = index;

            const q = questions[index];
            document.getElementById('current-question-num').innerText = q.nomor;
            document.getElementById('total-questions-num').innerText = questions.length;
            document.getElementById('display-mapel').innerText = q.mapel || "Quest";
            document.getElementById('display-soal-text').innerText = q.soal;
            document.getElementById('label-quest-title').innerText = `Level ${q.nomor} Challenge`;

            // Left Stimulus Reading Content
            const stimulusContainer = document.getElementById('display-stimulus-container');
            stimulusContainer.innerHTML = "";
            
            const paragraphs = q.stimulus || ["Tidak ada dokumen pendukung tambahan untuk level ini."];
            paragraphs.forEach(pText => {
                const p = document.createElement('p');
                p.className = "mb-3 leading-relaxed hover:bg-slate-50 p-2 rounded-xl transition duration-150";
                p.innerText = pText;
                p.onclick = () => triggerLineFocus(p);
                stimulusContainer.appendChild(p);
            });

            // Enable highlighter handler if active
            setupTextHighlighterEvent();

            // Right Options Choice
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

            // Update Doubtful Toggle UI state
            updateDoubtfulButtonUI();

            // Navigations visibility
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
                btn.className = "game-btn px-4 py-2.5 text-xs font-bold rounded-xl flex items-center gap-1.5 transition border border-amber-500 bg-amber-500 text-white shadow-md shadow-amber-500/10";
                btn.innerHTML = `<i class="fa-solid fa-square-check"></i> Ragu-Ragu`;
            } else {
                btn.className = "game-btn px-4 py-2.5 text-xs font-bold rounded-xl flex items-center gap-1.5 transition border border-amber-300 bg-amber-50 text-amber-700 hover:bg-amber-100";
                btn.innerHTML = `<i class="fa-regular fa-square"></i> Ragu-Ragu`;
            }
        }

        function toggleDoubtful() {
            const q = questions[currentQuestionIndex];
            doubtfulSaved[q.nomor] = !doubtfulSaved[q.nomor];
            GameAudio.playClick();
            updateDoubtfulButtonUI();
            renderGridIndicators();
        }

        // TRIGGER SHORT MICRO-LOADING OVERLAY TRANSITION
        function goToQuestion(index) {
            const loader = document.getElementById('mission-loader');
            loader.classList.remove('hidden');
            GameAudio.playSlide();

            setTimeout(() => {
                showQuestion(index);
                loader.classList.add('hidden');
            }, 350);
        }

        function registerAnswer(qNum, letter) {
            const wasAnswered = answersSaved[qNum] !== undefined && answersSaved[qNum] !== "";
            answersSaved[qNum] = letter;
            GameAudio.playClick();
            renderGridIndicators();

            if (!wasAnswered) {
                let currentCount = 0;
                questions.forEach(q => {
                    if (answersSaved[q.nomor] !== undefined && answersSaved[q.nomor] !== "") {
                        currentCount++;
                    }
                });
                checkQuestMilestone(currentCount);
            }
        }

        // CONFIRM END OF TKA QUEST ADVENTURE
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
            let msg = `Anda telah menjawab ${answeredCount} dari ${questions.length} butir level tantangan.`;
            
            if (doubtfulCount > 0) {
                msg += ` Masih terdapat ${doubtfulCount} level dengan status Ragu-Ragu. Silakan matikan tanda Ragu-Ragu bila Anda sudah merasa yakin.`;
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
                msg += ` Masih terdapat ${unanswered} level tantangan yang terlewat! Apakah Anda yakin ingin menyelesaikan ujian?`;
                showModal(
                    "Tantangan Belum Lengkap!", 
                    msg, 
                    "danger", 
                    "Kirim Sekarang", 
                    "Periksa Kembali", 
                    () => executeFinalSubmit(), 
                    null
                );
            } else {
                msg += " Apakah Anda yakin ingin mengakhiri petualangan dan mengirim jawaban?";
                showModal(
                    "Misi Selesai?", 
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
                "Batas waktu petualangan Anda telah habis. Lembar jawab Anda dikirim otomatis.", 
                "danger", 
                "Lihat Hasil", 
                "Tutup", 
                () => executeFinalSubmit(true), 
                () => executeFinalSubmit(true)
            );
        }
    </script>

    <script>
        // DATA POST TO SPREADSHEETS & PERSIST RESETS
        async function executeFinalSubmit(isForced = false) {
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

            // Build payload
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

            // Post to Sheets
            try {
                // Formatting payload keys to match Sheets expectations dynamically
                const spreadData = {
                    "Nama": activeStudent.nama,
                    "Kelas": activeStudent.kelas,
                    "Nomor Absen": parseInt(activeStudent.absen),
                    "Tanggal": dateStr,
                    "Jam Mulai": examStartTimeStr,
                    "Jam Selesai": formatEnd,
                    "Durasi": elapsedSecStr,
                    "Jumlah Benar": correctCount,
                    "Jumlah Salah": incorrectCount,
                    "Skor": parseFloat(score.toFixed(1))
                };
                questions.forEach(q => {
                    spreadData[`Jawaban Nomor ${q.nomor}`] = answersSaved[q.nomor] || "-";
                });

                await fetch(CONFIG.API_URL, {
                    method: "POST",
                    mode: "no-cors",
                    body: JSON.stringify(spreadData)
                });
            } catch (err) {
                console.error("Sheets connectivity failure, fallback locally:", err);
            }

            // Sync with local backups
            const submissions = JSON.parse(localStorage.getItem('tka_literasi_submissions') || '[]');
            submissions.push(submission);
            localStorage.setItem('tka_literasi_submissions', JSON.stringify(submissions));

            // Reset autosave drafts
            localStorage.removeItem(`lite_autosave_${activeStudent.nama}_${activeStudent.kelas}_${activeStudent.absen}`);

            // Update UI results
            document.getElementById('res-student-name').innerText = activeStudent.nama;
            document.getElementById('res-student-class').innerText = `${activeStudent.kelas} / Absen ${activeStudent.absen}`;
            document.getElementById('res-total-correct').innerText = correctCount;
            document.getElementById('res-total-incorrect').innerText = incorrectCount;
            document.getElementById('res-final-score').innerText = score.toFixed(1);

            triggerConfetti();
            GameAudio.playVictory();
            switchView('student-results');
            activeStudent = null;
        }

        // PROCEDURAL HTML/SVG CONFETTI GENERATOR
        function triggerConfetti() {
            const colors = ['#3b82f6', '#06b6d4', '#10b981', '#f59e0b', '#e11d48', '#8b5cf6'];
            const container = document.body;

            for (let i = 0; i < 75; i++) {
                const particle = document.createElement('div');
                particle.className = 'confetti-particle';
                
                const size = Math.random() * 8 + 6;
                particle.style.width = `${size}px`;
                particle.style.height = `${size * (Math.random() * 0.5 + 0.8)}px`;
                particle.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                particle.style.left = `${Math.random() * 100}vw`;
                particle.style.animationDelay = `${Math.random() * 1.5}s`;
                particle.style.animationDuration = `${Math.random() * 2 + 2}s`;
                
                container.appendChild(particle);

                // Auto remove
                setTimeout(() => {
                    particle.remove();
                }, 4000);
            }
        }
    </script>

    <script>
        // PORTAL GURU LOGIC
        function openTeacherLogin() {
            switchView('teacher-login');
            document.getElementById('input-teacher-pwd').value = "";
            document.getElementById('error-pwd-msg').classList.add('hidden');
        }

        function verifyTeacherLogin(e) {
            e.preventDefault();
            const pass = document.getElementById('input-teacher-pwd').value;
            if (pass === CONFIG.TEACHER_PASSWORD) {
                switchView('teacher-dashboard');
                switchTeacherTab('tab-peserta');
            } else {
                document.getElementById('error-pwd-msg').classList.remove('hidden');
            }
        }

        function switchTeacherTab(tabId) {
            GameAudio.playClick();
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

        // TAB 1: RENDER PARTICIPANTS TABLE
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

        // TAB 2: DETAILED REKAP PER NOMOR
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
                            ${empty > 0 ? `<div class="text-[9px] text-vibrant-rose italic font-semibold">Kosong: ${empty} siswa</div>` : ''}
                        </div>
                    </div>

                    <div class="pt-2.5 border-t border-slate-100 grid grid-cols-2 gap-2 text-center text-[10px]">
                        <div class="bg-emerald-50/50 border border-emerald-100 rounded-xl py-1.5">
                            <span class="block text-[8px] text-vibrant-emerald font-extrabold uppercase tracking-wide">Benar</span>
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

        // TAB 3: DIFFICULTY SUMMARY WITH CHART.JS
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
                    diffText = "Sedang";
                    diffColor = "bg-amber-50 text-amber-800 border border-amber-200";
                } else if (pCorrect < 85) {
                    diffText = "Mudah";
                    diffColor = "bg-brand-50 text-brand-800 border border-brand-200";
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
                            label: 'Siswa Benar',
                            data: dataCorrect,
                            backgroundColor: '#10b981',
                            borderRadius: 6
                        },
                        {
                            label: 'Siswa Salah',
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

        // TAB 4: PLAYER ANSWER MATRIX WITH MATCH CHECK (✔)
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

        // TAB 5: QUEST DATABASE MANAGEMENT
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
            document.getElementById('editor-form-title').innerText = "Tambah Level Soal";
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
            document.getElementById('editor-form-title').innerText = "Edit Level " + q.nomor;
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
            showModal("Soal Tersimpan", "Perubahan butir tingkat level tersimpan sukses ke database.", "success", "Oke", "Tutup", null, null);
            
            clearEditorForm();
            renderSoalEditorList();
        }

        function deleteSoalClick(idx) {
            showModal(
                "Hapus Level?", 
                `Apakah Anda yakin ingin menghapus level ${questions[idx].nomor} ini dari database?`, 
                "danger", 
                "Hapus Permanen", 
                "Batal", 
                () => {
                    questions.splice(idx, 1);
                    localStorage.setItem('tka_literasi_questions', JSON.stringify(questions));
                    renderSoalEditorList();
                    showToast("Level berhasil terhapus!");
                }, 
                null
            );
        }

        function resetQuestionsToDefault() {
            showModal(
                "Reset Database Soal?", 
                "Tindakan ini akan memulihkan butir level standar bawaan program.", 
                "warning", 
                "Kembalikan Standar", 
                "Batal", 
                () => {
                    questions = [...DEFAULT_QUESTIONS];
                    localStorage.setItem('tka_literasi_questions', JSON.stringify(questions));
                    renderSoalEditorList();
                    showToast("Misi quest telah di-reset ke standar.");
                }, 
                null
            );
        }

        function clearAllData() {
            showModal(
                "Reset Semua Hasil?", 
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
                    showToast("Semua riwayat hasil petualangan dibersihkan.");
                }, 
                null
            );
        }
    </script>
</body>
</html>
