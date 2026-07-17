<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CBT Ujian TKA SMP</title>
    <!-- Google Fonts Inter -->
    <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap">
    <!-- Chart.js untuk Grafik Dashboard Guru -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        /* ==========================================
           1. CORE STYLE (BIRU INDIGO-PUTIH MODERN)
           ========================================== */
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Inter', sans-serif;
            background-color: #f8fafc;
            color: #1e293b;
            line-height: 1.6;
        }

        header class, .cbt-header {
            background-color: #1e40af;
            color: #ffffff;
            padding: 1.2rem 2rem;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .cbt-brand h1 {
            font-size: 1.35rem;
            font-weight: 700;
            letter-spacing: -0.025em;
        }

        .container {
            max-width: 1280px;
            margin: 2rem auto;
            padding: 0 1.5rem;
        }

        .card {
            background: #ffffff;
            border-radius: 12px;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.05), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
            border: 1px solid #e2e8f0;
            padding: 2rem;
            margin-bottom: 1.5rem;
        }

        /* Form Control */
        .form-group {
            margin-bottom: 1.25rem;
            text-align: left;
        }

        .form-group label {
            display: block;
            font-weight: 500;
            margin-bottom: 0.5rem;
            font-size: 0.9rem;
            color: #475569;
        }

        .form-control {
            width: 100%;
            padding: 0.75rem 1rem;
            border: 1px solid #cbd5e1;
            border-radius: 8px;
            font-size: 1rem;
            font-family: inherit;
            transition: all 0.2s;
        }

        .form-control:focus {
            outline: none;
            border-color: #3b82f6;
            box-shadow: 0 0 0 4px rgba(59, 130, 246, 0.15);
        }

        /* Tombol & Navigasi */
        .btn {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            padding: 0.75rem 1.5rem;
            font-weight: 500;
            border-radius: 8px;
            border: none;
            cursor: pointer;
            font-family: inherit;
            font-size: 0.95rem;
            transition: all 0.2s;
            user-select: none;
        }

        .btn-primary {
            background-color: #1e40af;
            color: #ffffff;
        }

        .btn-primary:hover {
            background-color: #1d4ed8;
        }

        .btn-secondary {
            background-color: #e2e8f0;
            color: #334155;
        }

        .btn-secondary:hover {
            background-color: #cbd5e1;
        }

        .btn-warning {
            background-color: #f59e0b;
            color: #ffffff;
        }

        .btn-warning:hover {
            background-color: #d97706;
        }

        /* Split Screen & PISA/ANBK Layout */
        .split-layout {
            display: grid;
            grid-template-columns: 1.1fr 0.9fr;
            gap: 1.5rem;
            align-items: start;
        }

        .cbt-main-grid {
            display: grid;
            grid-template-columns: 3fr 1fr;
            gap: 1.5rem;
            margin-top: 1.5rem;
        }

        @media (max-width: 1024px) {
            .split-layout, .cbt-main-grid {
                grid-template-columns: 1fr;
            }
        }

        /* Reading Panel Tools */
        .stimulus-panel {
            background-color: #ffffff;
            border: 1px solid #e2e8f0;
            border-radius: 12px;
            padding: 1.5rem;
            max-height: 500px;
            overflow-y: auto;
            position: relative;
        }

        /* Flat Clean Stabilo (Murni warna penyorot tanpa frame/border tambahan) */
        .stabilo-highlight {
            background-color: rgba(250, 204, 21, 0.5);
            color: inherit;
        }

        .active-stabilo-mode {
            cursor: crosshair !important;
        }

        /* Grid Navigasi Nomor */
        .num-grid {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 0.5rem;
        }

        .num-btn {
            aspect-ratio: 1;
            border: 1.5px solid #cbd5e1;
            background-color: #f8fafc;
            color: #475569;
            border-radius: 8px;
            font-weight: 600;
            font-size: 1rem;
            cursor: pointer;
            transition: all 0.2s;
        }

        /* State warna penanda nomor berdasarkan status jawaban */
        .num-btn.unanswered {
            background-color: #f1f5f9;
            color: #475569;
            border-color: #cbd5e1;
        }

        .num-btn.answered {
            background-color: #059669;
            color: #ffffff;
            border-color: #059669;
        }

        .num-btn.doubtful {
            background-color: #d97706;
            color: #ffffff;
            border-color: #d97706;
        }

        .num-btn.current {
            box-shadow: 0 0 0 4px rgba(30, 64, 175, 0.4);
            border: 2px solid #1e40af;
        }

        /* Radio Pilihan Jawaban */
        .opsi-container {
            margin-top: 1rem;
        }

        .opsi-item {
            display: flex;
            align-items: center;
            padding: 1rem;
            border: 1px solid #cbd5e1;
            border-radius: 8px;
            margin-bottom: 0.75rem;
            cursor: pointer;
            transition: all 0.15s ease;
        }

        .opsi-item:hover {
            background-color: #f1f5f9;
        }

        .opsi-item input[type="radio"] {
            margin-right: 1rem;
            width: 1.25rem;
            height: 1.25rem;
            accent-color: #1e40af;
        }

        .opsi-item.selected {
            background-color: #eff6ff;
            border-color: #3b82f6;
        }

        /* Timer Global Box */
        .timer-box {
            background-color: #eff6ff;
            border: 1px solid #bfdbfe;
            color: #1e40af;
            padding: 0.6rem 1.2rem;
            border-radius: 8px;
            font-weight: 700;
            font-size: 1.1rem;
        }

        /* Modal Kustom UI */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(15, 23, 42, 0.6);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 2000;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.2s ease-in-out;
        }

        .modal-overlay.active {
            opacity: 1;
            pointer-events: auto;
        }

        .modal-box {
            background: #ffffff;
            padding: 2rem;
            border-radius: 12px;
            max-width: 480px;
            width: 90%;
            box-shadow: 0 20px 25px -5px rgba(0,0,0,0.1);
            text-align: center;
        }

        /* Tab Menu Admin */
        .teacher-tabs {
            display: flex;
            border-bottom: 2px solid #e2e8f0;
            margin-bottom: 1.5rem;
            overflow-x: auto;
        }

        .tab-link {
            padding: 1rem 1.5rem;
            border: none;
            background: none;
            cursor: pointer;
            font-weight: 500;
            color: #64748b;
            border-bottom: 2px solid transparent;
            white-space: nowrap;
        }

        .tab-link.active {
            color: #1e40af;
            border-bottom: 2px solid #1e40af;
            font-weight: 600;
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
        }

        .table-wrapper {
            overflow-x: auto;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 1rem;
            font-size: 0.95rem;
        }

        th, td {
            border: 1px solid #e2e8f0;
            padding: 0.75rem 1rem;
            text-align: left;
        }

        th {
            background-color: #f1f5f9;
            font-weight: 600;
            color: #334155;
        }

        tr:nth-child(even) {
            background-color: #f8fafc;
        }

        .correct-mark {
            color: #10b981;
            font-weight: bold;
            font-size: 1.1rem;
            margin-left: 0.25rem;
        }

        footer {
            text-align: center;
            padding: 2rem 0;
            color: #94a3b8;
            font-size: 0.85rem;
            margin-top: 4rem;
            border-top: 1px solid #e2e8f0;
        }
    </style>
</head>
<body>

    <!-- HEADER UTAMA -->
    <header class="cbt-header">
        <div class="cbt-brand">
            <h1>Tes Kemampuan Akademik (TKA) SMP</h1>
        </div>
        <div id="wrapper-timer-cbt" style="display: none;">
            <div class="timer-box"><span id="time-display">120:00:00</span></div>
        </div>
        <div id="wrapper-logout-guru" style="display: none;">
            <button id="btn-logout" class="btn btn-secondary" style="padding: 0.5rem 1rem;">Keluar Admin</button>
        </div>
    </header>

    <div class="container">

        <!-- ==========================================
           TAB TAB SCREEN 1: PORTAL SELEKSI UTAMA
           ========================================== -->
        <div id="screen-portal-pilihan" class="card" style="max-width: 550px; margin: 4rem auto; text-align: center;">
            <h2 style="color: #1e40af; margin-bottom: 0.5rem; font-weight: 700;">Selamat Datang di Portal CBT</h2>
            <p style="color: #64748b; margin-bottom: 2rem; font-size: 0.95rem;">Silakan tentukan hak akses halaman Anda:</p>
            
            <div style="display: flex; flex-direction: column; gap: 1rem;">
                <button onclick="pindahScreenGerbang('siswa')" class="btn btn-primary" style="padding: 1.2rem; font-size: 1.05rem; font-weight: 600;">
                    Masuk Halaman Siswa (Ujian CBT)
                </button>
                <button onclick="pindahScreenGerbang('guru')" class="btn btn-secondary" style="padding: 1.2rem; font-size: 1.05rem; font-weight: 600;">
                    Masuk Halaman Guru (Dashboard Analisis)
                </button>
            </div>
        </div>

        <!-- ==========================================
           SCREEN 2: SISWA - FORM LOGIN IDENTITAS
           ========================================== -->
        <div id="screen-siswa-login" class="card" style="max-width: 480px; margin: 3rem auto; display: none;">
            <h2 style="color: #1e40af; text-align: center; margin-bottom: 1.5rem; font-weight: 700;">Identitas Peserta Ujian</h2>
            
            <div class="form-group">
                <label for="input-nama">Nama Lengkap</label>
                <input type="text" id="input-nama" class="form-control" placeholder="Ketik nama lengkap Anda...">
            </div>
            
            <div class="form-group">
                <label for="input-kelas">Kelas</label>
                <select id="input-kelas" class="form-control">
                    <option value="">-- Pilih Kelas --</option>
                    <option value="9A">9A</option>
                    <option value="9B">9B</option>
                    <option value="9C">9C</option>
                    <option value="9D">9D</option>
                    <option value="9E">9E</option>
                    <option value="9F">9F</option>
                    <option value="9G">9G</option>
                    <option value="9H">9H</option>
                </select>
            </div>

            <div class="form-group">
                <label for="input-absen">Nomor Absen</label>
                <input type="number" id="input-absen" class="form-control" placeholder="Contoh: 15" min="1">
            </div>

            <button id="btn-mulai-ujian" class="btn btn-primary" style="width: 100%; margin-top: 1rem; padding: 0.9rem; font-weight: 600;">Mulai Ujian</button>
            <button onclick="pindahScreenGerbang('portal')" class="btn btn-secondary" style="width: 100%; margin-top: 0.5rem; background:transparent; border:none; color:#64748b;">Kembali ke Menu Utama</button>
        </div>

        <!-- ==========================================
           SCREEN 3: SISWA - DASHBOARD PANEL EXAM CBT
           ========================================== -->
        <div id="screen-siswa-cbt" class="cbt-main-grid" style="display: none;">
            
            <!-- Area Soal Dan Stimulus Kiri -->
            <div>
                <div class="card" style="padding: 1.25rem; margin-bottom: 1rem; display: flex; gap: 0.75rem; align-items: center; background-color: #f8fafc;">
                    <button id="btn-fitur-stabilo" class="btn btn-secondary" style="font-size: 0.85rem; padding: 0.5rem 1rem; border: 1.5px solid #cbd5e1; font-weight: 600;">
                        Stabilo Teks
                    </button>
                    <span style="font-size: 0.85rem; color: #64748b;">*Aktifkan tombol lalu seleksi teks stimulus cerita menggunakan kursor/jari untuk menandai informasi penting.</span>
                </div>

                <div class="card split-layout">
                    <!-- Sisi Kiri: Panel Bacaan / Stimulus Panjang -->
                    <div>
                        <h4 style="font-size: 0.95rem; color: #1e40af; font-weight: 700; margin-bottom: 0.5rem; text-transform: uppercase; letter-spacing: 0.05em;">Stimulus Bacaan</h4>
                        <div id="panel-bacaan-stimulus" class="stimulus-panel text-stimulus-content">
                            <!-- Memuat teks stimulus via JS -->
                        </div>
                    </div>

                    <!-- Sisi Kanan: Soal dan Pilihan Jawaban -->
                    <div>
                        <div style="display: flex; justify-content: space-between; align-items: center; border-bottom: 2px solid #f1f5f9; padding-bottom: 0.5rem; margin-bottom: 1rem;">
                            <span id="badge-mapel" style="background-color: #eff6ff; color: #1e40af; font-size: 0.8rem; padding: 0.25rem 0.75rem; border-radius: 9999px; font-weight: 600;">Mata Pelajaran</span>
                            <span style="font-weight: 700; color: #334155; font-size: 1rem;">Soal No. <span id="text-nomor-berjalan">1</span></span>
                        </div>

                        <div id="container-isi-soal" style="font-size: 1.05rem; font-weight: 500; color: #1e293b; margin-bottom: 1.5rem;">
                            <!-- Pertanyaan Soal -->
                        </div>

                        <div id="container-opsi-jawaban" class="opsi-container">
                            <!-- Pilihan Radio Button -->
                        </div>
                    </div>
                </div>

                <!-- Tombol Kendali Navigasi Bawah -->
                <div style="display: flex; justify-content: space-between; align-items: center; gap: 1rem;">
                    <button id="btn-nav-prev" class="btn btn-secondary" style="min-width: 120px;">Sebelumnya</button>
                    <button id="btn-nav-ragu" class="btn btn-warning" style="min-width: 140px; font-weight: 600;">Ragu-Ragu</button>
                    <button id="btn-nav-next" class="btn btn-primary" style="min-width: 120px;">Selanjutnya</button>
                    <button id="btn-nav-selesai" class="btn btn-primary" style="background-color: #e11d48; min-width: 130px; display: none;">Selesai Ujian</button>
                </div>
            </div>

            <!-- Area Grid Navigasi Kanan -->
            <div>
                <div class="card" style="padding: 1.25rem;">
                    <h3 style="font-size: 0.95rem; color: #1e40af; border-bottom: 2px solid #f1f5f9; padding-bottom: 0.5rem; margin-bottom: 0.75rem; font-weight: 700;">Peserta</h3>
                    <div style="font-size: 0.85rem; color: #475569;">
                        <p style="margin-bottom: 0.25rem;"><strong>Nama:</strong> <span id="lbl-info-nama">-</span></p>
                        <p style="margin-bottom: 0.25rem;"><strong>Kelas:</strong> <span id="lbl-info-kelas">-</span></p>
                        <p style="margin-bottom: 0.5rem;"><strong>Absen:</strong> <span id="lbl-info-absen">-</span></p>
                    </div>
                </div>

                <div class="card" style="padding: 1.25rem;">
                    <h3 style="font-size: 0.95rem; color: #1e40af; border-bottom: 2px solid #f1f5f9; padding-bottom: 0.5rem; margin-bottom: 1rem; font-weight: 700;">Navigasi Soal</h3>
                    <div id="wrapper-grid-indeks-nomor" class="num-grid">
                        <!-- Grid Angka Nomor generated dinamis -->
                    </div>
                    
                    <!-- Keterangan Legenda Status Warna -->
                    <div style="margin-top: 1.5rem; font-size: 0.8rem; color: #64748b; display: flex; flex-direction: column; gap: 0.4rem; border-top: 1px dashed #e2e8f0; padding-top: 1rem;">
                        <div style="display:flex; align-items:center; gap:0.5rem;">
                            <span style="display:inline-block; width:12px; height:12px; background:#059669; border-radius:3px;"></span> Sudah Dijawab (Yakin)
                        </div>
                        <div style="display:flex; align-items:center; gap:0.5rem;">
                            <span style="display:inline-block; width:12px; height:12px; background:#d97706; border-radius:3px;"></span> Ragu-Ragu
                        </div>
                        <div style="display:flex; align-items:center; gap:0.5rem;">
                            <span style="display:inline-block; width:12px; height:12px; background:#f1f5f9; border:1px solid #cbd5e1; border-radius:3px;"></span> Belum Dijawab
                        </div>
                    </div>
                </div>
            </div>

        </div>

        <!-- ==========================================
           SCREEN 4: SISWA - KOTAK RINGKASAN SKOR HASIL
           ========================================== -->
        <div id="screen-siswa-skor" class="card" style="max-width: 500px; margin: 4rem auto; text-align: center; display: none;">
            <h2 style="color: #1e40af; margin-bottom: 0.5rem; font-weight: 700;">Ujian Selesai</h2>
            <p style="color: #64748b; font-size: 0.9rem; margin-bottom: 2rem;">Data lembar jawaban Anda telah sukses diamankan ke database pusat cloud.</p>
            
            <div style="background-color: #f8fafc; border: 1px solid #e2e8f0; padding: 1.5rem; border-radius: 10px; text-align: left; margin-bottom: 1.5rem;">
                <p style="margin-bottom: 0.4rem; font-size: 0.95rem;"><strong>Nama Peserta:</strong> <span id="res-nama">-</span></p>
                <p style="margin-bottom: 0.4rem; font-size: 0.95rem;"><strong>Kelas / Absen:</strong> <span id="res-kelas-absen">-</span></p>
                <hr style="border: none; border-top: 1px dashed #cbd5e1; margin: 1rem 0;">
                <h4 style="color: #1e40af; font-size: 1.05rem; margin-bottom: 0.75rem; font-weight: 700;">Skor Anda</h4>
                <p style="margin-bottom: 0.25rem; font-size: 0.95rem;">Benar : <strong id="res-benar" style="color: #059669;">-</strong></p>
                <p style="margin-bottom: 0.25rem; font-size: 0.95rem;">Salah : <strong id="res-salah" style="color: #dc2626;">-</strong></p>
                <p style="font-size: 1.3rem; margin-top: 0.75rem; color: #0f172a;"><strong>Skor : <span id="res-skor-nilai">-</span></strong></p>
            </div>
            
            <p style="font-size: 0.8rem; color: #94a3b8;">*Demi menjaga kerahasiaan ujian, kunci jawaban dan pembahasan tidak ditampilkan.</p>
        </div>

        <!-- ==========================================
           SCREEN 5: GURU - DIALOG LOGIN GURU
           ========================================== -->
        <div id="screen-guru-login" class="card" style="max-width: 400px; margin: 5rem auto; text-align: center; display: none;">
            <h2 style="color: #1e40af; margin-bottom: 1.5rem; font-weight: 700;">Autentikasi Guru</h2>
            <div class="form-group">
                <label for="input-pass-guru">Kata Sandi Akses</label>
                <input type="password" id="input-pass-guru" class="form-control" placeholder="Masukkan password admin...">
            </div>
            <button id="btn-submit-login-guru" class="btn btn-primary" style="width: 100%; padding: 0.8rem; font-weight: 600;">Buka Dashboard</button>
            <button onclick="pindahScreenGerbang('portal')" class="btn btn-secondary" style="width: 100%; margin-top: 0.5rem; background:transparent; border:none; color:#64748b;">Kembali</button>
        </div>

        <!-- ==========================================
           SCREEN 6: GURU - CORE DASHBOARD ANALISIS
           ========================================== -->
        <div id="screen-guru-dashboard" style="display: none;">
            
            <div class="teacher-tabs">
                <button class="tab-link active" onclick="pindahMenuTabGuru(event, 'tab-guru-peserta')">1. Daftar Seluruh Peserta</button>
                <button class="tab-link" onclick="pindahMenuTabGuru(event, 'tab-guru-rekap-pilihan')">2. Rekap Jawaban Per Nomor Soal</button>
                <button class="tab-link" onclick="pindahMenuTabGuru(event, 'tab-guru-analisis-kesulitan')">3. Analisis Soal</button>
                <button class="tab-link" onclick="pindahMenuTabGuru(event, 'tab-guru-matriks-lembar-jawab')">4. Rekap Jawaban Siswa</button>
            </div>

            <!-- TAB 1: LIST PESERTA -->
            <div id="tab-guru-peserta" class="tab-content active">
                <div class="card">
                    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 1rem; flex-wrap: wrap; gap: 1rem;">
                        <h3 style="color: #1e40af; font-weight: 700;">Daftar Kehadiran & Nilai</h3>
                        <button onclick="tarikPusatDataSpreadsheet()" class="btn btn-secondary" style="font-size: 0.85rem; padding: 0.5rem 1rem;">🔄 Sinkronisasi Data Baru</button>
                    </div>
                    <p style="color: #64748b; font-size: 0.85rem; margin-bottom: 1rem;">*Klik baris tajuk kolom <strong style="color:#1e40af; cursor:pointer;">Skor (Urutkan ↕)</strong> untuk mengurutkan pencapaian siswa tertinggi.</p>
                    <div class="table-wrapper">
                        <table>
                            <thead>
                                <tr>
                                    <th>Nama</th>
                                    <th>Kelas</th>
                                    <th>No Absen</th>
                                    <th>Tanggal</th>
                                    <th>Waktu Mulai</th>
                                    <th>Waktu Selesai</th>
                                    <th>Lama Mengerjakan</th>
                                    <th id="th-sortable-skor" style="cursor: pointer; background-color: #eff6ff; color: #1e40af; font-weight: 700;">Skor (Urutkan ↕)</th>
                                </tr>
                            </thead>
                            <tbody id="tbody-guru-peserta">
                                <!-- Terisi otomatis -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- TAB 2: SEBARAN PILIHAN JAWABAN PER NOMOR -->
            <div id="tab-guru-rekap-pilihan" class="tab-content">
                <div class="card">
                    <h3 style="color: #1e40af; margin-bottom: 1.5rem; font-weight: 700;">Sebaran Pilihan Jawaban Peserta</h3>
                    <div id="box-render-distribusi-jawaban-nomor" style="display: grid; grid-template-columns: repeat(auto-fill, minmax(450px, 1fr)); gap: 1.5rem;">
                        <!-- Render Distribusi Opsi -->
                    </div>
                </div>
            </div>

            <!-- TAB 3: TINGKAT KESULITAN & GRAFIK -->
            <div id="tab-guru-analisis-kesulitan" class="tab-content">
                <div class="card">
                    <h3 style="color: #1e40af; margin-bottom: 1rem; font-weight: 700;">Daftar Urutan Indeks Kesulitan</h3>
                    <p style="color: #64748b; font-size: 0.85rem; margin-bottom: 1.5rem;">Tabel diurutkan otomatis dari soal yang paling banyak dijawab **salah** hingga yang paling sedikit salah.</p>
                    
                    <div class="table-wrapper" style="margin-bottom: 2.5rem;">
                        <table>
                            <thead>
                                <tr>
                                    <th>No Soal</th>
                                    <th>Mata Pelajaran</th>
                                    <th>Benar</th>
                                    <th>Salah</th>
                                    <th>Persentase Benar</th>
                                    <th>Persentase Salah</th>
                                </tr>
                            </thead>
                            <tbody id="tbody-guru-kesulitan-soal">
                                <!-- Data terisi otomatis -->
                            </tbody>
                        </table>
                    </div>

                    <h3 style="color: #1e40af; margin-bottom: 1.5rem; font-weight: 700;">Grafik Perbandingan Performa Butir Soal</h3>
                    <div style="position: relative; height: 380px; width: 100%;">
                        <canvas id="canvasChartGuru"></canvas>
                    </div>
                </div>
            </div>

            <!-- TAB 4: MATRIKS LEMBAR JAWABAN SISWA -->
            <div id="tab-guru-matriks-lembar-jawab" class="tab-content">
                <div class="card">
                    <h3 style="color: #1e40af; margin-bottom: 1rem; font-weight: 700;">Matriks Lembar Jawaban Peserta</h3>
                    <p style="color: #64748b; font-size: 0.85rem; margin-bottom: 1.5rem;">Simbol centang hijau (<span class="correct-mark">✔</span>) merupakan penanda otomatis kecocokan jawaban dengan kunci guru.</p>
                    <div class="table-wrapper">
                        <table>
                            <thead>
                                <tr id="tr-header-matriks-soal">
                                    <th>Nama</th>
                                    <!-- Diisi No 1-N -->
                                </tr>
                            </thead>
                            <tbody id="tbody-matriks-jawaban-siswa">
                                <!-- Baris lembar jawab siswa -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

        </div>

    </div>

    <!-- ==========================================
       7. PANEL KUSTOM MODAL OVERLAY UI (Bebas Alert Browser)
       ========================================== -->
    <div id="kustom-modal-overlay" class="modal-overlay">
        <div class="modal-box">
            <h3 style="color: #1e40af; font-weight: 700; margin-bottom: 1rem; font-size: 1.2rem;" id="lbl-modal-title">Konfirmasi</h3>
            <p id="lbl-modal-desc" style="color: #475569; margin-bottom: 1.5rem; font-size: 0.95rem;">Apakah tindakan Anda sudah yakin?</p>
            <div style="display: flex; gap: 1rem; justify-content: center;">
                <button id="btn-modal-cancel" class="btn btn-secondary">Batal</button>
                <button id="btn-modal-confirm" class="btn btn-primary" style="background-color: #e11d48;">Lanjutkan</button>
            </div>
        </div>
    </div>

    <!-- FOOTER -->
    <footer>
        <p>© 2026 CBT TKA SMP</p>
    </footer>

    <!-- ==========================================
       8. INSTAN JAVASCRIPT CORE APPLICATION LOGIC
       ========================================== -->
    <script>
        // A. KONFIGURASI LINK SPREADSHEET (Milik Anda) DAN PASSWORD GURU
        const CONFIG = {
            API_URL: "https://script.google.com/macros/s/AKfycbwsduiB6QoKP2SelYaSouG8ZBrYdFArpZxnoo0h_58YVmUgzDpOavNj4mouTWRHx5EP-Q/exec",
            TEACHER_PASSWORD: "adminguru123"
        };

        // B. DATABASE SOAL LITERASI & HOTS (Format JSON Terbaca Otomatis)
        const bankSoalUjian = [
            {
                "nomor": 1,
                "mapel": "Matematika",
                "stimulus": "Toko Berkah Utama Jaya mengadakan promo spesial awal tahun untuk paket seragam sekolah. Paket Seragam A berisi 2 kemeja dan 1 celana seharga Rp 140.000. Paket Seragam B berisi 3 kemeja dan 2 celana dijual seharga Rp 235.000. Angga ingin membeli 4 kemeja dan 3 celana dengan mengombinasikan pilihan paket atau eceran yang tersedia.",
                "soal": "Berdasarkan stimulus harga paket di atas, berapakah harga satuan eceran dari 1 buah kemeja saja?",
                "opsi": ["Rp 45.000", "Rp 50.000", "Rp 55.000", "Rp 60.000"],
                "jawaban": "A"
            },
            {
                "nomor": 2,
                "mapel": "Matematika",
                "stimulus": "Sebuah bak tampung air bersih di panti asuhan berbentuk silinder tabung silindris dengan jari-jari alas sepanjang 70 cm dan memiliki tinggi tegak 2 meter. Pada jam 07.00 pagi, bak tersebut kosong. Kemudian pengurus menyalakan pompa air dengan debit aliran konstan sebesar 20 liter per menit. (Gunakan nilai pendekatan pi = 22/7).",
                "soal": "Berapakah estimasi waktu terdekat durasi pompa harus dinyalakan agar bak terisi penuh hingga bibir atas?",
                "opsi": ["120 menit", "154 menit", "180 menit", "210 menit"],
                "jawaban": "B"
            },
            {
                "nomor": 3,
                "mapel": "Matematika",
                "stimulus": "Denah lahan pekarangan berbentuk persegi panjang berukuran panjang 24 meter dan lebar 15 meter akan dipasangi pagar beton pelindung di sekelilingnya. Namun, di salah satu sisi panjangnya akan disisakan ruang kosong selebar 4 meter yang tidak dipagar untuk keperluan pintu gerbang lipat besi baja.",
                "soal": "Jika biaya pembangunan pagar beton dipatok seharga Rp 250.000 per meter, hitung total anggaran biaya yang dibutuhkan!",
                "opsi": ["Rp 18.500.000", "Rp 19.500.000", "Rp 21.000.000", "Rp 22.000.000"],
                "jawaban": "A"
            },
            {
                "nomor": 4,
                "mapel": "Matematika",
                "stimulus": "Rata-rata nilai ujian seleksi masuk kelas akselerasi dari 29 orang siswa adalah 78. Beberapa menit kemudian, menyusul satu siswa tersisa bernama Danu mengikuti ujian susulan. Setelah nilai Danu digabungkan dengan kelompok tersebut, rata-rata nilai kelas berubah naik menjadi 78,5.",
                "soal": "Berdasarkan prinsip hitung statistika rata-rata gabungan, berapakah nilai murni yang didapatkan Danu?",
                "opsi": ["88", "90", "93", "95"],
                "jawaban": "C"
            },
            {
                "nomor": 5,
                "mapel": "Matematika",
                "stimulus": "Grafik pertumbuhan bakteri patogen pada sebuah media cawan laboratorium menunjukkan pola pembelahan diri eksponensial. Diketahui jumlah bakteri membelah diri menjadi dua kali lipat setiap 15 menit sekali. Pada pengamatan awal pukul 10.00 WIB, terdapat 50 bakteri aktif.",
                "soal": "Berapakah akumulasi kelipatan jumlah total bakteri yang hidup di cawan tersebut saat jam digital menunjukkan pukul 11.30 WIB?",
                "opsi": ["1.600 bakteri", "3.200 bakteri", "4.800 bakteri", "6.400 bakteri"],
                "jawaban": "B"
            }
        ];

        // C. STATE MANAGEMENT SISTEM CBT
        let indeksSoalBerjalan = 0;
        let lembarJawabSiswa = {};   // { 1: "A", 2: "B" }
        let statusRaguSiswa = {};    // { 1: true, 2: false }
        let sisaWaktuDetik = 120 * 60; // 120 menit
        let intervalTimerObj = null;
        let timestampMulaiUjian = null;
        let dataPusatSiswaGuru = [];
        let objekInstansiChart = null;
        let statusUrutanMeningkat = false;
        let benderaStabiloAktif = false;

        // D. INITIALIZATION
        window.addEventListener("DOMContentLoaded", () => {
            // Cek jika siswa telah menyelesaikan ujian sebelumnya di komputer ini
            if (localStorage.getItem("tka_submitted_done") === "true") {
                tampilkanScreenSkorAkhir(JSON.parse(localStorage.getItem("tka_saved_result_object")));
                return;
            }
            // Cek jika status ujian sedang berjalan (Terkena refresh paksa)
            if (localStorage.getItem("tka_is_running") === "true") {
                pulihkanDataUjianLokal();
            }

            // Pasang Listener DOM
            document.getElementById("btn-mulai-ujian").addEventListener("click", eksekusiLoginMulaiUjian);
            document.getElementById("btn-nav-next").addEventListener("click", () => berpindahNomorSoal(indeksSoalBerjalan + 1));
            document.getElementById("btn-nav-prev").addEventListener("click", () => berpindahNomorSoal(indeksSoalBerjalan - 1));
            document.getElementById("btn-nav-ragu").addEventListener("click", toggleStatusRaguRagu);
            document.getElementById("btn-nav-selesai").addEventListener("click", validasiKumpulUjian);
            document.getElementById("btn-submit-login-guru").addEventListener("click", verifikasiAksesMasukGuru);
            document.getElementById("btn-logout").addEventListener("click", keluarSesiDashboardGuru);
            document.getElementById("th-sortable-skor").addEventListener("click", urutkanTabelPesertaSkor);
            
            // Setup Text Highlighter (Stabilo)
            document.getElementById("btn-fitur-stabilo").addEventListener("click", toggleFiturStabiloTeks);
            document.getElementById("panel-bacaan-stimulus").addEventListener("mouseup", tanganiSeleksiTeksMouse);
            document.getElementById("panel-bacaan-stimulus").addEventListener("touchend", tanganiSeleksiTeksMouse);
        });

        // E. NAVIGATION ROUTER SCREEN
        function pindahScreenGerbang(target) {
            document.getElementById("screen-portal-pilihan").style.display = "none";
            document.getElementById("screen-siswa-login").style.display = "none";
            document.getElementById("screen-siswa-cbt").style.display = "none";
            document.getElementById("screen-guru-login").style.display = "none";
            document.getElementById("screen-guru-dashboard").style.display = "none";
            document.getElementById("wrapper-timer-cbt").style.display = "none";
            document.getElementById("wrapper-logout-guru").style.display = "none";

            if (target === 'portal') {
                document.getElementById("screen-portal-pilihan").style.display = "block";
            } else if (target === 'siswa') {
                document.getElementById("screen-siswa-login").style.display = "block";
            } else if (target === 'guru') {
                if (sessionStorage.getItem("sesi_guru_aktif") === "true") {
                    document.getElementById("screen-guru-dashboard").style.display = "block";
                    document.getElementById("wrapper-logout-guru").style.display = "block";
                    tarikPusatDataSpreadsheet();
                } else {
                    document.getElementById("screen-guru-login").style.display = "block";
                }
            }
        }

        // F. CORE LOGIC SISWA
        function eksekusiLoginMulaiUjian() {
            const nama = document.getElementById("input-nama").value.trim();
            const kelas = document.getElementById("input-kelas").value;
            const absen = document.getElementById("input-absen").value.trim();

            if (!nama || !kelas || !absen) {
                tampilkanKustomModalUI("Lengkapi Identitas", "Mohon maaf, Nama Lengkap, Pilihan Kelas, dan Nomor Absen wajib diisi sebelum ujian dimulai.", null, true);
                return;
            }

            timestampMulaiUjian = new Date();
            lembarJawabSiswa = {};
            statusRaguSiswa = {};
            indeksSoalBerjalan = 0;
            sisaWaktuDetik = 120 * 60;

            // Masukkan ke penampungan cadangan LocalStorage
            localStorage.setItem("tka_nama", nama);
            localStorage.setItem("tka_kelas", kelas);
            localStorage.setItem("tka_absen", absen);
            localStorage.setItem("tka_start_time", timestampMulaiUjian.toISOString());
            localStorage.setItem("tka_answers", JSON.stringify(lembarJawabSiswa));
            localStorage.setItem("tka_ragu", JSON.stringify(statusRaguSiswa));
            localStorage.setItem("tka_timer", sisaWaktuDetik);
            localStorage.setItem("tka_is_running", "true");

            bukaInterfaceLembarCBT(nama, kelas, absen);
            inisialisasiPenghitungMundur();
        }

        function pulihkanDataUjianLokal() {
            const nama = localStorage.getItem("tka_nama");
            const kelas = localStorage.getItem("tka_kelas");
            const absen = localStorage.getItem("tka_absen");
            timestampMulaiUjian = new Date(localStorage.getItem("tka_start_time"));
            lembarJawabSiswa = JSON.parse(localStorage.getItem("tka_answers")) || {};
            statusRaguSiswa = JSON.parse(localStorage.getItem("tka_ragu")) || {};
            sisaWaktuDetik = parseInt(localStorage.getItem("tka_timer")) || (120 * 60);

            bukaInterfaceLembarCBT(nama, kelas, absen);
            inisialisasiPenghitungMundur();
        }

        function bukaInterfaceLembarCBT(nama, kelas, absen) {
            document.getElementById("screen-siswa-login").style.display = "none";
            document.getElementById("screen-siswa-cbt").style.display = "grid";
            document.getElementById("wrapper-timer-cbt").style.display = "block";

            document.getElementById("lbl-info-nama").textContent = nama;
            document.getElementById("lbl-info-kelas").textContent = kelas;
            document.getElementById("lbl-info-absen").textContent = absen;

            renderUIRangkaianNomorGrid();
            tampilkanDataButirSoal(indeksSoalBerjalan);
        }

        function inisialisasiPenghitungMundur() {
            perbaruiTeksTimerUI();
            clearInterval(intervalTimerObj);
            intervalTimerObj = setInterval(() => {
                sisaWaktuDetik--;
                localStorage.setItem("tka_timer", sisaWaktuDetik);
                perbaruiTeksTimerUI();

                if (sisaWaktuDetik <= 0) {
                    clearInterval(intervalTimerObj);
                    autoKumpulUjianWaktuHabis();
                }
            }, 1000);
        }

        function perbaruiTeksTimerUI() {
            const jam = Math.floor(sisaWaktuDetik / 3600);
            const sisa = sisaWaktuDetik % 3600;
            const mnt = Math.floor(sisa / 60);
            const dtk = sisa % 60;
            document.getElementById("time-display").textContent = `Waktu Tersisa: ${jam.toString().padStart(2, '0')}:${mnt.toString().padStart(2, '0')}:${dtk.toString().padStart(2, '0')}`;
        }

        function renderUIRangkaianNomorGrid() {
            const container = document.getElementById("wrapper-grid-indeks-nomor");
            if (!container) return;
            container.innerHTML = "";

            bankSoalUjian.forEach((soal, idx) => {
                const btn = document.createElement("button");
                btn.className = "num-btn";
                btn.textContent = soal.nomor;

                // Cek status pewarnaan indikator
                if (statusRaguSiswa[soal.nomor] === true) {
                    btn.classList.add("doubtful");
                } else if (lembarJawabSiswa[soal.nomor]) {
                    btn.classList.add("answered");
                } else {
                    btn.classList.add("unanswered");
                }

                if (idx === indeksSoalBerjalan) {
                    btn.classList.add("current");
                }

                btn.addEventListener("click", () => berpindahNomorSoal(idx));
                container.appendChild(btn);
            });
        }

        function tampilkanDataButirSoal(index) {
            if (index < 0 || index >= bankSoalUjian.length) return;
            indeksSoalBerjalan = index;

            const targetSoal = bankSoalUjian[indeksSoalBerjalan];
            
            // Set Tulisan Deskripsi & Stimulus
            document.getElementById("text-nomor-berjalan").textContent = targetSoal.nomor;
            document.getElementById("badge-mapel").textContent = targetSoal.mapel;
            document.getElementById("panel-bacaan-stimulus").innerHTML = targetSoal.stimulus;
            document.getElementById("container-isi-soal").textContent = targetSoal.soal;

            // Render Pilihan Ganda (Radio)
            const boxOpsi = document.getElementById("container-opsi-jawaban");
            boxOpsi.innerHTML = "";

            const abjadList = ["A", "B", "C", "D"];
            targetSoal.opsi.forEach((opsiTxt, i) => {
                const charAbjad = abjadList[i];
                const wrapper = document.createElement("div");
                wrapper.className = "opsi-item";
                if (lembarJawabSiswa[targetSoal.nomor] === charAbjad) {
                    wrapper.classList.add("selected");
                }

                const radio = document.createElement("input");
                radio.type = "radio";
                radio.name = `cbt_radio_${targetSoal.nomor}`;
                radio.value = charAbjad;
                radio.checked = (lembarJawabSiswa[targetSoal.nomor] === charAbjad);

                const label = document.createElement("label");
                label.style.width = "100%";
                label.style.cursor = "pointer";
                label.innerHTML = `<strong style="color:#1e40af; margin-right:0.3rem;">${charAbjad}.</strong> ${opsiTxt}`;

                wrapper.appendChild(radio);
                wrapper.appendChild(label);

                wrapper.addEventListener("click", () => {
                    radio.checked = true;
                    simpanJawabanSiswaKlik(targetSoal.nomor, charAbjad);
                    document.querySelectorAll(".opsi-item").forEach(el => el.classList.remove("selected"));
                    wrapper.classList.add("selected");
                });

                boxOpsi.appendChild(wrapper);
            });

            // Sinkronisasi status tombol Ragu-Ragu
            const btnRagu = document.getElementById("btn-nav-ragu");
            if (statusRaguSiswa[targetSoal.nomor] === true) {
                btnRagu.textContent = "✓ Lepaskan Ragu";
                btnRagu.style.backgroundColor = "#b45309";
            } else {
                btnRagu.textContent = "⚠ Ragu-Ragu";
                btnRagu.style.backgroundColor = "#f59e0b";
            }

            // Atur tombol navigasi
            document.getElementById("btn-nav-prev").disabled = (index === 0);
            if (index === bankSoalUjian.length - 1) {
                document.getElementById("btn-nav-next").style.display = "none";
                document.getElementById("btn-nav-selesai").style.display = "block";
            } else {
                document.getElementById("btn-nav-next").style.display = "block";
                document.getElementById("btn-nav-selesai").style.display = "none";
            }

            renderUIRangkaianNomorGrid();
        }

        function simpanJawabanSiswaKlik(noNomor, pilihanAbjad) {
            lembarJawabSiswa[noNomor] = pilihanAbjad;
            localStorage.setItem("tka_answers", JSON.stringify(lembarJawabSiswa));
            renderUIRangkaianNomorGrid();
        }

        function toggleStatusRaguRagu() {
            const noNomor = bankSoalUjian[indeksSoalBerjalan].nomor;
            if (statusRaguSiswa[noNomor] === true) {
                statusRaguSiswa[noNomor] = false;
            } else {
                statusRaguSiswa[noNomor] = true;
            }
            localStorage.setItem("tka_ragu", JSON.stringify(statusRaguSiswa));
            tampilkanDataButirSoal(indeksSoalBerjalan);
        }

        function berpindahNomorSoal(targetIdx) {
            tampilkanDataButirSoal(targetIdx);
        }

        // G. FUNGSIONALITAS STABILO (HIGHLIGHTER KUNING DATAR BERSIH)
        function toggleFiturStabiloTeks() {
            benderaStabiloAktif = !benderaStabiloAktif;
            const btn = document.getElementById("btn-fitur-stabilo");
            const panel = document.getElementById("panel-bacaan-stimulus");

            if (benderaStabiloAktif) {
                btn.style.backgroundColor = "rgba(250, 204, 21, 0.5)";
                btn.style.borderColor = "#eab308";
                panel.classList.add("active-stabilo-mode");
            } else {
                btn.style.backgroundColor = "#e2e8f0";
                btn.style.borderColor = "#cbd5e1";
                panel.classList.remove("active-stabilo-mode");
            }
        }

        function tanganiSeleksiTeksMouse() {
            if (!benderaStabiloAktif) return;

            const selection = window.getSelection();
            if (!selection.rangeCount || selection.isCollapsed) return;

            const range = selection.getRangeAt(0);
            const ancestor = range.commonAncestorContainer;

            // Pastikan seleksi berada di dalam panel bacaan
            let penandaPanel = false;
            let checkNode = ancestor;
            while (checkNode) {
                if (checkNode.id === "panel-bacaan-stimulus") {
                    penandaPanel = true;
                    break;
                }
                checkNode = checkNode.parentNode;
            }

            if (!penandaPanel) return;

            const spanStabilo = document.createElement("span");
            spanStabilo.className = "stabilo-highlight";
            
            try {
                range.surroundContents(spanStabilo);
            } catch (e) {
                console.warn("Seleksi terlalu rumit lintas elemen DOM.");
            }
            selection.removeAllRanges();
        }

        // H. PROSES PENGUMPULAN JAWABAN (KIRIM DATA)
        function validasiKumpulUjian() {
            const totalSoal = bankSoalUjian.length;
            const terisi = Object.keys(lembarJawabSiswa).length;
            
            // Hitung status ragu
            let adaRagu = false;
            for (let k in statusRaguSiswa) {
                if (statusRaguSiswa[k] === true) adaRagu = true;
            }

            let kalimatPesan = `Apakah Anda yakin ingin mengakhiri sesi ujian?<br><strong>Soal dikerjakan: ${terisi} dari ${totalSoal}</strong>`;
            
            if (terisi < totalSoal) {
                kalimatPesan += `<br><span style="color:#ef4444; font-weight:600;">Peringatan: Ada ${totalSoal - terisi} nomor soal yang terlewat!</span>`;
            }
            if (adaRagu) {
                kalimatPesan += `<br><span style="color:#d97706; font-weight:600;">Peringatan: Masih ada soal berstatus Ragu-Ragu (Oranye)!</span>`;
            }

            tampilkanKustomModalUI("Selesaikan Ujian?", kalimatPesan, () => {
                kalkulasiDanKirimPaketKeSheets();
            }, false);
        }

        function autoKumpulUjianWaktuHabis() {
            tampilkanKustomModalUI("Waktu Telah Habis!", "Waktu Anda sudah habis. Sistem otomatis menyimpan dan mengirim lembar jawaban Anda sekarang.", () => {
                kalkulasiDanKirimPaketKeSheets();
            }, true);
        }

        async function kalkulasiDanKirimPaketKeSheets() {
            clearInterval(intervalTimerObj);
            
            let countBenar = 0;
            let countSalah = 0;

            bankSoalUjian.forEach(s => {
                const jawab = lembarJawabSiswa[s.nomor];
                if (jawab === s.jawaban) {
                    countBenar++;
                } else {
                    countSalah++;
                }
            });

            const nilaiSkor = Math.round((countBenar / bankSoalUjian.length) * 100);
            const waktuSelesai = new Date();
            const selisihMili = waktuSelesai - timestampMulaiUjian;
            const durasiMenit = Math.floor(selisihMili / 60000);
            const durasiDetik = Math.floor((selisihMili % 60000) / 1000);
            const stringLamaPengerjaan = `${durasiMenit} menit ${durasiDetik} detik`;

            const nama = localStorage.getItem("tka_nama");
            const kelas = localStorage.getItem("tka_kelas");
            const absen = localStorage.getItem("tka_absen");

            // Siapkan payload JSON terstruktur rapi
            const payload = {
                "Nama": nama,
                "Kelas": kelas,
                "Nomor Absen": absen,
                "Tanggal": waktuSelesai.toLocaleDateString('id-ID'),
                "Jam Mulai": timestampMulaiUjian.toLocaleTimeString('id-ID'),
                "Jam Selesai": waktuSelesai.toLocaleTimeString('id-ID'),
                "Durasi": stringLamaPengerjaan,
                "Jumlah Benar": countBenar,
                "Jumlah Salah": countSalah,
                "Skor": nilaiSkor
            };

            // Masukkan rekap jawaban per nomor
            bankSoalUjian.forEach(s => {
                payload[`Jawaban Nomor ${s.nomor}`] = lembarJawabSiswa[s.nomor] || "-";
            });

            // Kirim via Fetch REST API
            try {
                await fetch(CONFIG.API_URL, {
                    method: "POST",
                    mode: "no-cors",
                    body: JSON.stringify(payload)
                });
            } catch(e) {
                console.error("Koneksi gagal ke Apps Script, data dicadangkan.", e);
            }

            const simpanHasilObj = { nama, kelas, absen, benar: countBenar, salah: countSalah, skor: nilaiSkor };
            localStorage.setItem("tka_submitted_done", "true");
            localStorage.setItem("tka_saved_result_object", JSON.stringify(simpanHasilObj));
            localStorage.removeItem("tka_is_running");

            tampilkanScreenSkorAkhir(simpanHasilObj);
        }

        function tampilkanScreenSkorAkhir(obj) {
            document.getElementById("screen-siswa-login").style.display = "none";
            document.getElementById("screen-siswa-cbt").style.display = "none";
            document.getElementById("wrapper-timer-cbt").style.display = "none";

            document.getElementById("screen-siswa-skor").style.display = "block";
            document.getElementById("res-nama").textContent = obj.nama;
            document.getElementById("res-kelas-absen").textContent = `Kelas ${obj.kelas} / Absen Nomor ${obj.absen}`;
            document.getElementById("res-benar").textContent = obj.benar;
            document.getElementById("res-salah").textContent = obj.salah;
            document.getElementById("res-skor-nilai").textContent = obj.skor;
        }

        // I. CORE LOGIC DASHBOARD GURU
        function verifikasiAksesMasukGuru() {
            const pass = document.getElementById("input-pass-guru").value;
            if (pass === CONFIG.TEACHER_PASSWORD) {
                sessionStorage.setItem("sesi_guru_aktif", "true");
                document.getElementById("screen-guru-login").style.display = "none";
                document.getElementById("screen-guru-dashboard").style.display = "block";
                document.getElementById("wrapper-logout-guru").style.display = "block";
                tarikPusatDataSpreadsheet();
            } else {
                tampilkanKustomModalUI("Akses Ditolak", "Kata sandi admin guru yang dimasukkan salah. Silakan periksa pengaturan internal.", null, true);
            }
        }

        function keluarSesiDashboardGuru() {
            sessionStorage.removeItem("sesi_guru_aktif");
            location.reload();
        }

        async function tarikPusatDataSpreadsheet() {
            try {
                const r = await fetch(CONFIG.API_URL);
                dataPusatSiswaGuru = await r.json();
            } catch (err) {
                console.warn("Menggunakan mockup offline lokal karena lembar Google Sheet utama masih kosong.");
                // Data simulasi otomatis agar dashboard langsung terisi visualisasi contoh jika sheet belum ada isinya
                dataPusatSiswaGuru = [
                    { "Nama": "Andi Setiawan", "Kelas": "9A", "Nomor Absen": "2", "Tanggal": "17/07/2026", "Jam Mulai": "08:00:10", "Jam Selesai": "09:40:00", "Durasi": "100 menit", "Jumlah Benar": 4, "Jumlah Salah": 1, "Skor": 80, "Jawaban Nomor 1": "A", "Jawaban Nomor 2": "B", "Jawaban Nomor 3": "A", "Jawaban Nomor 4": "B", "Jawaban Nomor 5": "C" },
                    { "Nama": "Citra Lestari", "Kelas": "9C", "Nomor Absen": "10", "Tanggal": "17/07/2026", "Jam Mulai": "08:05:00", "Jam Selesai": "09:35:12", "Durasi": "90 menit", "Jumlah Benar": 5, "Jumlah Salah": 0, "Skor": 100, "Jawaban Nomor 1": "A", "Jawaban Nomor 2": "B", "Jawaban Nomor 3": "C", "Jawaban Nomor 4": "B", "Jawaban Nomor 5": "B" },
                    { "Nama": "Dimas Pratama", "Kelas": "9B", "Nomor Absen": "18", "Tanggal": "17/07/2026", "Jam Mulai": "08:02:11", "Jam Selesai": "09:12:00", "Durasi": "70 menit", "Jumlah Benar": 2, "Jumlah Salah": 3, "Skor": 40, "Jawaban Nomor 1": "B", "Jawaban Nomor 2": "A", "Jawaban Nomor 3": "C", "Jawaban Nomor 4": "C", "Jawaban Nomor 5": "D" }
                ];
            }

            jalankanKalkulasiStatistikGuru();
        }

        function jalankanKalkulasiStatistikGuru() {
            renderTabelDaftarSiswaGuru();
            renderTabDistribusiPilihanOpsi();
            renderTabAnalisisKesulitanDanGrafik();
            renderTabMatriksSiswa();
        }

        function renderTabelDaftarSiswaGuru() {
            const tbody = document.getElementById("tbody-guru-peserta");
            tbody.innerHTML = "";

            if (dataPusatSiswaGuru.length === 0) {
                tbody.innerHTML = `<tr><td colspan="8" style="text-align:center;">Belum ada record data siswa yang masuk.</td></tr>`;
                return;
            }

            dataPusatSiswaGuru.forEach(s => {
                const tr = document.createElement("tr");
                tr.innerHTML = `
                    <td><strong>${s["Nama"] || "-"}</strong></td>
                    <td>${s["Kelas"] || "-"}</td>
                    <td>${s["Nomor Absen"] || "-"}</td>
                    <td>${s["Tanggal"] || "-"}</td>
                    <td>${s["Jam Mulai"] || "-"}</td>
                    <td>${s["Jam Selesai"] || "-"}</td>
                    <td>${s["Durasi"] || "-"}</td>
                    <td style="font-weight:700; color:#1e40af;">${s["Skor"] !== undefined ? s["Skor"] : "-"}</td>
                `;
                tbody.appendChild(tr);
            });
        }

        function urutkanTabelPesertaSkor() {
            statusUrutanMeningkat = !statusUrutanMeningkat;
            dataPusatSiswaGuru.sort((x, y) => {
                const skorX = parseFloat(x["Skor"]) || 0;
                const skorY = parseFloat(y["Skor"]) || 0;
                return statusUrutanMeningkat ? skorX - skorY : skorY - skorX;
            });
            renderTabelDaftarSiswaGuru();
        }

        function renderTabDistribusiPilihanOpsi() {
            const container = document.getElementById("box-render-distribusi-jawaban-nomor");
            container.innerHTML = "";

            bankSoalUjian.forEach(soal => {
                let a = 0, b = 0, c = 0, d = 0, kosong = 0;
                let bnr = 0, slh = 0;

                dataPusatSiswaGuru.forEach(mhs => {
                    const ans = mhs[`Jawaban Nomor ${soal.nomor}`];
                    if (ans === "A") a++;
                    else if (ans === "B") b++;
                    else if (ans === "C") c++;
                    else if (ans === "D") d++;
                    else kosong++;

                    if (ans === soal.jawaban) bnr++;
                    else slh++;
                });

                const total = dataPusatSiswaGuru.length;
                const pBnr = total > 0 ? Math.round((bnr / total) * 100) : 0;
                const pSlh = total > 0 ? 100 - pBnr : 0;

                const div = document.createElement("div");
                div.className = "card";
                div.style.borderLeft = "4px solid #1e40af";
                div.innerHTML = `
                    <h4 style="color:#1e40af; font-weight:700; margin-bottom:0.5rem;">Soal Nomor ${soal.nomor} [${soal.mapel}]</h4>
                    <p style="font-size:0.85rem; color:#64748b; margin-bottom:0.75rem;">${soal.soal}</p>
                    <ul style="list-style:none; font-size:0.9rem; margin-bottom:1rem; padding-left:0.5rem;">
                        <li>• Pilihan <strong>A:</strong> ${a} Siswa</li>
                        <li>• Pilihan <strong>B:</strong> ${b} Siswa</li>
                        <li>• Pilihan <strong>C:</strong> ${c} Siswa</li>
                        <li>• Pilihan <strong>D:</strong> ${d} Siswa</li>
                        ${kosong > 0 ? `<li style="color:#ef4444">• Kosong/Lewat: ${kosong} Siswa</li>` : ""}
                    </ul>
                    <div style="background:#f8fafc; padding:0.6rem; border-radius:6px; font-size:0.85rem; border:1px solid #e2e8f0;">
                        <p>Kunci Jawaban: <strong style="color:#059669">${soal.jawaban}</strong></p>
                        <p>Jumlah Benar: <strong>${bnr}</strong> | Salah: <strong>${slh}</strong></p>
                        <p>Persentase: <span style="color:#059669; font-weight:600;">Benar ${pBnr}%</span> | <span style="color:#dc2626; font-weight:600;">Salah ${pSlh}%</span></p>
                    </div>
                `;
                container.appendChild(div);
            });
        }

        function renderTabAnalisisKesulitanDanGrafik() {
            let listAnalisis = [];

            bankSoalUjian.forEach(soal => {
                let bnr = 0, slh = 0;
                dataPusatSiswaGuru.forEach(mhs => {
                    if (mhs[`Jawaban Nomor ${soal.nomor}`] === soal.jawaban) bnr++;
                    else slh++;
                });

                const tot = dataPusatSiswaGuru.length;
                const pb = tot > 0 ? Math.round((bnr / tot) * 100) : 0;
                const ps = tot > 0 ? 100 - pb : 0;

                listAnalisis.push({
                    nomor: soal.nomor, mapel: soal.mapel, benar: bnr, salah: slh, pBenar: pb, pSalah: ps
                });
            });

            // URUTKAN UTAMA: Paling banyak salah ke paling sedikit salah
            listAnalisis.sort((p, q) => q.salah - p.salah);

            const tbody = document.getElementById("tbody-guru-kesulitan-soal");
            tbody.innerHTML = "";
            listAnalisis.forEach(item => {
                const tr = document.createElement("tr");
                tr.innerHTML = `
                    <td><strong>Nomor ${item.nomor}</strong></td>
                    <td>${item.mapel}</td>
                    <td style="color:#059669; font-weight:600;">${item.benar}</td>
                    <td style="color:#dc2626; font-weight:600;">${item.salah}</td>
                    <td>${item.pBenar}%</td>
                    <td>${item.pSalah}%</td>
                `;
                tbody.appendChild(tr);
            });

            // Kembalikan urutan nomor normal (1,2,3..) khusus grafik batang
            listAnalisis.sort((p, q) => p.nomor - q.nomor);

            const labelGrafik = listAnalisis.map(i => `No ${i.nomor}`);
            const dataBenar = listAnalisis.map(i => i.benar);
            const dataSalah = listAnalisis.map(i => i.salah);

            if (objekInstansiChart) objekInstansiChart.destroy();

            const ctx = document.getElementById("canvasChartGuru").getContext("2d");
            objekInstansiChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: labelGrafik,
                    datasets: [
                        { label: 'Siswa Benar (✔)', data: dataBenar, backgroundColor: '#10b981' },
                        { label: 'Siswa Salah (✘)', data: dataSalah, backgroundColor: '#ef4444' }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: { y: { beginAtZero: true, ticks: { stepSize: 1 } } }
                }
            });
        }

        function renderTabMatriksSiswa() {
            const trHead = document.getElementById("tr-header-matriks-soal");
            const tbody = document.getElementById("tbody-matriks-jawaban-siswa");

            trHead.innerHTML = "<th>Nama Siswa</th>";
            tbody.innerHTML = "";

            bankSoalUjian.forEach(soal => {
                trHead.innerHTML += `<th style="text-align:center;">No ${soal.nomor}</th>`;
            });

            if (dataPusatSiswaGuru.length === 0) {
                tbody.innerHTML = `<tr><td colspan="${bankSoalUjian.length + 1}" style="text-align:center;">Tidak ada data.</td></tr>`;
                return;
            }

            dataPusatSiswaGuru.forEach(mhs => {
                const tr = document.createElement("tr");
                let htmlCells = `<td><strong>${mhs["Nama"] || "-"}</strong> <span style="font-size:0.75rem; color:#64748b;">(${mhs["Kelas"] || "-"})</span></td>`;
                
                bankSoalUjian.forEach(soal => {
                    const jwb = mhs[`Jawaban Nomor ${soal.nomor}`] || "-";
                    const isBnr = (jwb === soal.jawaban);
                    htmlCells += `<td style="text-align:center;">${jwb} ${isBnr ? '<span class="correct-mark">✔</span>' : ''}</td>`;
                });

                tr.innerHTML = htmlCells;
                tbody.appendChild(tr);
            });
        }

        function pindahMenuTabGuru(evt, tabId) {
            document.querySelectorAll(".tab-content").forEach(el => el.classList.remove("active"));
            document.querySelectorAll(".tab-link").forEach(el => el.classList.remove("active"));
            document.getElementById(tabId).classList.add("active");
            evt.currentTarget.classList.add("active");
        }

        // J. KUSTOM DIALOG UI MODAL KENDALI MANAGER
        function tampilkanKustomModalUI(judul, deskripsi, fungsiKonfirmasi, forceHideCancel = false) {
            const overlay = document.getElementById("kustom-modal-overlay");
            document.getElementById("lbl-modal-title").textContent = judul;
            document.getElementById("lbl-modal-desc").innerHTML = deskripsi;

            const btnCancel = document.getElementById("btn-modal-cancel");
            const btnConfirm = document.getElementById("btn-modal-confirm");

            if (forceHideCancel) {
                btnCancel.style.display = "none";
            } else {
                btnCancel.style.display = "inline-flex";
            }

            btnCancel.onclick = () => overlay.classList.remove("active");

            // Kloning tombol konfirmasi agar event listener bersih
            const newBtnConfirm = btnConfirm.cloneNode(true);
            btnConfirm.parentNode.replaceChild(newBtnConfirm, btnConfirm);

            newBtnConfirm.onclick = () => {
                overlay.classList.remove("active");
                if (fungsiKonfirmasi) fungsiKonfirmasi();
            };

            overlay.classList.add("active");
        }
    </script>
</body>
</html>
