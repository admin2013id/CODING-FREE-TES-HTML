<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pro HTML Studio | Premium Builder</title>
    <!-- Mengambil Font Inter dan Fira Code untuk tampilan profesional -->
    <link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;500&family=Inter:wght@300;400;600&display=swap" rel="stylesheet">
    <!-- Mengambil Ikon dari FontAwesome (CDN) -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        :root {
            --bg-body: #0f172a;
            --bg-panel: #1e293b;
            --bg-editor: #0f172a;
            --accent-primary: #3b82f6; /* Blue */
            --accent-glow: rgba(59, 130, 246, 0.5);
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --border-color: #334155;
            --success: #10b981;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            outline: none;
        }

        body {
            background-color: var(--bg-body);
            color: var(--text-main);
            font-family: 'Inter', sans-serif;
            height: 100vh;
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }

        /* --- Header Premium --- */
        header {
            height: 60px;
            background: rgba(15, 23, 42, 0.85);
            backdrop-filter: blur(12px);
            border-bottom: 1px solid var(--border-color);
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 25px;
            z-index: 10;
        }

        .brand {
            display: flex;
            align-items: center;
            gap: 12px;
            font-weight: 600;
            font-size: 1.2rem;
            letter-spacing: -0.5px;
        }

        .brand i {
            color: var(--accent-primary);
            font-size: 1.4rem;
            text-shadow: 0 0 15px var(--accent-glow);
        }

        .header-actions button {
            background: linear-gradient(135deg, var(--accent-primary), #2563eb);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
            font-weight: 500;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(37, 99, 235, 0.3);
        }

        .header-actions button:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(37, 99, 235, 0.5);
        }

        /* --- Main Layout --- */
        .workspace {
            display: flex;
            flex: 1;
            height: calc(100vh - 60px);
        }

        /* --- Editor Section --- */
        .editor-container {
            width: 50%;
            display: flex;
            flex-direction: column;
            border-right: 1px solid var(--border-color);
            background-color: var(--bg-editor);
            position: relative;
        }

        .panel-label {
            background-color: var(--bg-panel);
            padding: 8px 15px;
            font-size: 0.75rem;
            text-transform: uppercase;
            letter-spacing: 1px;
            color: var(--text-muted);
            border-bottom: 1px solid var(--border-color);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .code-wrapper {
            position: relative;
            flex: 1;
            overflow: hidden;
        }

        textarea#code-editor {
            width: 100%;
            height: 100%;
            background-color: var(--bg-editor);
            color: #e2e8f0;
            border: none;
            padding: 20px;
            font-family: 'Fira Code', monospace;
            font-size: 14px;
            line-height: 1.6;
            resize: none;
            z-index: 2;
            position: relative;
        }

        /* Scrollbar Customization */
        ::-webkit-scrollbar {
            width: 10px;
            height: 10px;
        }
        ::-webkit-scrollbar-track {
            background: var(--bg-body);
        }
        ::-webkit-scrollbar-thumb {
            background: var(--border-color);
            border-radius: 5px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #475569;
        }

        /* --- Preview Section --- */
        .preview-container {
            width: 50%;
            display: flex;
            flex-direction: column;
            background-color: #ffffff; /* White bg for accurate preview */
        }

        iframe#preview-frame {
            width: 100%;
            height: 100%;
            border: none;
        }

        /* --- Tutorial Modal (Glassmorphism) --- */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.6);
            backdrop-filter: blur(8px);
            z-index: 1000;
            display: flex;
            justify-content: center;
            align-items: center;
            opacity: 0;
            visibility: hidden;
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .modal-overlay.active {
            opacity: 1;
            visibility: visible;
        }

        .modal-card {
            background: rgba(30, 41, 59, 0.95);
            border: 1px solid rgba(255, 255, 255, 0.1);
            width: 90%;
            max-width: 650px;
            border-radius: 16px;
            padding: 0;
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
            transform: scale(0.95);
            transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            overflow: hidden;
            display: flex;
            flex-direction: column;
            max-height: 85vh;
        }

        .modal-overlay.active .modal-card {
            transform: scale(1);
        }

        .modal-header {
            padding: 20px 30px;
            background: linear-gradient(to right, #1e293b, #0f172a);
            border-bottom: 1px solid var(--border-color);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .modal-title h2 {
            font-size: 1.5rem;
            color: white;
        }
        .modal-title p {
            color: var(--text-muted);
            font-size: 0.9rem;
            margin-top: 5px;
        }

        .close-modal {
            background: none;
            border: none;
            color: var(--text-muted);
            font-size: 1.5rem;
            cursor: pointer;
            transition: color 0.2s;
        }
        .close-modal:hover { color: white; }

        .modal-body {
            padding: 30px;
            overflow-y: auto;
        }

        .tutorial-step {
            display: flex;
            gap: 15px;
            margin-bottom: 25px;
        }

        .step-number {
            background: var(--accent-primary);
            color: white;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-weight: bold;
            flex-shrink: 0;
            box-shadow: 0 0 10px var(--accent-glow);
        }

        .step-content h3 {
            color: var(--text-main);
            margin-bottom: 8px;
            font-size: 1.1rem;
        }

        .step-content p {
            color: var(--text-muted);
            font-size: 0.95rem;
            line-height: 1.5;
            margin-bottom: 10px;
        }

        .code-block {
            background: #000;
            padding: 10px 15px;
            border-radius: 6px;
            font-family: 'Fira Code', monospace;
            font-size: 0.85rem;
            color: #a5b4fc;
            border-left: 3px solid var(--accent-primary);
        }

        .modal-footer {
            padding: 20px 30px;
            background: var(--bg-panel);
            border-top: 1px solid var(--border-color);
            text-align: right;
        }

        .btn-primary {
            background: var(--accent-primary);
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
        }

        .btn-primary:hover {
            background: #2563eb;
            box-shadow: 0 0 15px var(--accent-glow);
        }

        /* Responsive */
        @media (max-width: 768px) {
            .workspace { flex-direction: column; }
            .editor-container, .preview-container { width: 100%; height: 50%; }
            .modal-card { width: 95%; }
        }
    </style>
</head>
<body>

    <!-- Header -->
    <header>
        <div class="brand">
            <i class="fa-solid fa-code"></i>
            <span>Pro HTML Studio</span>
        </div>
        <div class="header-actions">
            <button onclick="openTutorial()">
                <i class="fa-solid fa-graduation-cap"></i> Tutorial
            </button>
        </div>
    </header>

    <!-- Main Workspace -->
    <div class="workspace">
        
        <!-- Editor Panel -->
        <div class="editor-container">
            <div class="panel-label">
                <span><i class="fa-solid fa-file-code"></i> Source Code</span>
                <span style="font-size: 10px; color: var(--success);">● Ready</span>
            </div>
            <div class="code-wrapper">
                <textarea id="code-editor" spellcheck="false" placeholder="Ketik kodemu di sini..."></textarea>
            </div>
        </div>

        <!-- Preview Panel -->
        <div class="preview-container">
            <div class="panel-label" style="background: #f1f5f9; color: #475569; border-bottom: 1px solid #cbd5e1;">
                <span><i class="fa-solid fa-desktop"></i> Live Browser Preview</span>
                <span style="font-size: 10px;">Localhost Simulation</span>
            </div>
            <iframe id="preview-frame"></iframe>
        </div>
    </div>

    <!-- Tutorial Modal -->
    <div class="modal-overlay" id="tutorialModal">
        <div class="modal-card">
            <div class="modal-header">
                <div class="modal-title">
                    <h2>Panduan Memulai</h2>
                    <p>Cara cepat membuat website pertama Anda</p>
                </div>
                <button class="close-modal" onclick="closeTutorial()">&times;</button>
            </div>
            
            <div class="modal-body">
                <div class="tutorial-step">
                    <div class="step-number">1</div>
                    <div class="step-content">
                        <h3>Struktur Dasar</h3>
                        <p>Setiap website membutuhkan kerangka dasar. Ketik struktur berikut di panel kiri:</p>
                        <div class="code-block">&lt;!DOCTYPE html&gt;<br>&lt;html&gt;<br>  &lt;body&gt;<br>    ...konten...<br>  &lt;/body&gt;<br>&lt;/html&gt;</div>
                    </div>
                </div>

                <div class="tutorial-step">
                    <div class="step-number">2</div>
                    <div class="step-content">
                        <h3>Menambahkan Konten</h3>
                        <p>Gunakan tag <code>&lt;h1&gt;</code> untuk judul besar dan <code>&lt;p&gt;</code> untuk paragraf.</p>
                        <div class="code-block">&lt;h1&gt;Halo Dunia&lt;/h1&gt;<br>&lt;p&gt;Ini website pertamaku.&lt;/p&gt;</div>
                    </div>
                </div>

                <div class="tutorial-step">
                    <div class="step-number">3</div>
                    <div class="step-content">
                        <h3>Memberi Gaya (CSS)</h3>
                        <p>Buat tampilan menarik dengan menambahkan atribut style atau tag style.</p>
                        <div class="code-block">&lt;h1 style="color: blue;"&gt;Judul Biru&lt;/h1&gt;</div>
                    </div>
                </div>
                
                <div class="tutorial-step">
                    <div class="step-number">4</div>
                    <div class="step-content">
                        <h3>Real-time Preview</h3>
                        <p>Panel sebelah kanan akan otomatis memperbarui hasil koding Anda secara langsung (Live Reload).</p>
                    </div>
                </div>
            </div>

            <div class="modal-footer">
                <button class="btn-primary" onclick="startCoding()">Mulai Coding Sekarang</button>
            </div>
        </div>
    </div>

    <script>
        // Kode Default yang Estetik
        const defaultCode = `<!DOCTYPE html>
<html>
<head>
    <style>
        body {
            font-family: 'Segoe UI', sans-serif;
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 0;
        }
        .card {
            background: white;
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.1);
            text-align: center;
            max-width: 400px;
        }
        h1 { color: #333; margin-bottom: 10px; }
        p { color: #666; line-height: 1.6; }
        .btn {
            display: inline-block;
            margin-top: 20px;
            padding: 10px 25px;
            background: #3b82f6;
            color: white;
            text-decoration: none;
            border-radius: 50px;
            font-weight: bold;
            transition: transform 0.2s;
        }
        .btn:hover { transform: scale(1.05); }
    </style>
</head>
<body>

    <div class="card">
        <h1>Selamat Datang!</h1>
        <p>Anda berhasil menjalankan Pro HTML Studio. Coba ubah teks ini atau ganti warnanya di panel sebelah kiri.</p>
        <a href="#" class="btn" onclick="alert('Hebat!')">Klik Saya</a>
    </div>

</body>
</html>`;

        const editor = document.getElementById('code-editor');
        const preview = document.getElementById('preview-frame');
        const modal = document.getElementById('tutorialModal');

        // Fungsi Update Preview
        function updatePreview() {
            const code = editor.value;
            const iframeDoc = preview.contentDocument || preview.contentWindow.document;
            iframeDoc.open();
            iframeDoc.write(code);
            iframeDoc.close();
        }

        // Event Listener
        editor.addEventListener('input', updatePreview);

        // Inisialisasi
        editor.value = defaultCode;
        updatePreview();

        // Kontrol Modal
        function openTutorial() {
            modal.classList.add('active');
        }

        function closeTutorial() {
            modal.classList.remove('active');
        }

        function startCoding() {
            closeTutorial();
            editor.focus();
        }

        // Auto-open tutorial saat load
        window.onload = function() {
            setTimeout(() => {
                openTutorial();
            }, 800);
        };
    </script>
</body>
</html>
