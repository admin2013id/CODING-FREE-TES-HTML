<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pro HTML Studio | Premium Builder</title>
    <!-- Font & Icons -->
    <link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;500&family=Inter:wght@300;400;600&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        :root {
            --bg-body: #0f172a;
            --bg-panel: #1e293b;
            --bg-editor: #0f172a;
            --accent-primary: #3b82f6;
            --accent-glow: rgba(59, 130, 246, 0.5);
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --border-color: #334155;
            --success: #10b981;
            --wa-color: #25D366;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; outline: none; }

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
            background: rgba(15, 23, 42, 0.95);
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

        .brand i { color: var(--accent-primary); text-shadow: 0 0 15px var(--accent-glow); }

        /* Device Switcher Styles */
        .device-switcher {
            background: var(--bg-panel);
            padding: 4px;
            border-radius: 8px;
            display: flex;
            gap: 5px;
            border: 1px solid var(--border-color);
        }

        .device-btn {
            background: transparent;
            border: none;
            color: var(--text-muted);
            padding: 6px 12px;
            border-radius: 6px;
            cursor: pointer;
            transition: all 0.2s ease;
            font-size: 0.9rem;
        }

        .device-btn:hover { color: white; background: rgba(255,255,255,0.05); }

        .device-btn.active {
            background: var(--accent-primary);
            color: white;
            box-shadow: 0 2px 10px rgba(59, 130, 246, 0.3);
        }

        /* Action Buttons Group */
        .header-actions {
            display: flex;
            gap: 10px;
        }

        .btn {
            border: none;
            padding: 8px 16px;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
            transition: all 0.3s ease;
            font-size: 0.9rem;
        }

        /* Tombol Create Website (Gradient Purple-Pink) */
        .btn-create {
            background: linear-gradient(135deg, #8b5cf6, #ec4899);
            color: white;
            box-shadow: 0 4px 15px rgba(236, 72, 153, 0.3);
        }

        .btn-create:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(236, 72, 153, 0.5);
        }

        /* Tombol Tutorial (Blue) */
        .btn-tutorial {
            background: linear-gradient(135deg, var(--accent-primary), #2563eb);
            color: white;
            box-shadow: 0 4px 15px rgba(37, 99, 235, 0.3);
        }

        .btn-tutorial:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(37, 99, 235, 0.5);
        }

        /* --- Main Layout --- */
        .workspace {
            display: flex;
            flex: 1;
            height: calc(100vh - 60px);
            position: relative;
        }

        /* --- Editor Section --- */
        .editor-container {
            width: 50%;
            display: flex;
            flex-direction: column;
            border-right: 1px solid var(--border-color);
            background-color: var(--bg-editor);
            z-index: 5;
        }

        .panel-label {
            background-color: var(--bg-panel);
            padding: 10px 15px;
            font-size: 0.75rem;
            text-transform: uppercase;
            letter-spacing: 1px;
            color: var(--text-muted);
            border-bottom: 1px solid var(--border-color);
            display: flex;
            justify-content: space-between;
            align-items: center;
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
        }

        /* --- Preview Section --- */
        .preview-wrapper {
            width: 50%;
            background-color: #cbd5e1;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            overflow: auto;
            position: relative;
        }

        #device-frame {
            background-color: #ffffff;
            transition: all 0.5s cubic-bezier(0.25, 0.8, 0.25, 1);
            box-shadow: 0 20px 50px rgba(0,0,0,0.2);
            position: relative;
            overflow: hidden;
            border-radius: 4px;
        }

        #device-frame.mode-desktop { width: 100%; height: 100%; border-radius: 0; }
        #device-frame.mode-tablet { width: 768px; height: 1024px; max-height: 90%; max-width: 90%; border: 12px solid #333; border-radius: 20px; }
        #device-frame.mode-mobile { width: 375px; height: 667px; max-height: 90%; border: 12px solid #333; border-radius: 30px; }

        /* Notch simulation */
        #device-frame.mode-mobile::before {
            content: ''; position: absolute; top: 0; left: 50%; transform: translateX(-50%);
            width: 40%; height: 20px; background: #333;
            border-bottom-left-radius: 12px; border-bottom-right-radius: 12px; z-index: 10;
        }

        iframe#preview-frame { width: 100%; height: 100%; border: none; background: white; display: block; }

        /* --- Modal Tutorial --- */
        .modal-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0, 0, 0, 0.6); backdrop-filter: blur(8px);
            z-index: 1000; display: flex; justify-content: center; align-items: center;
            opacity: 0; visibility: hidden; transition: all 0.4s ease;
        }
        .modal-overlay.active { opacity: 1; visibility: visible; }
        .modal-card {
            background: var(--bg-panel); border: 1px solid var(--border-color);
            width: 90%; max-width: 600px; border-radius: 16px;
            box-shadow: 0 25px 50px rgba(0,0,0,0.5); overflow: hidden;
            transform: scale(0.95); transition: transform 0.4s ease;
            display: flex; flex-direction: column; max-height: 85vh;
        }
        .modal-overlay.active .modal-card { transform: scale(1); }
        .modal-header { padding: 20px; border-bottom: 1px solid var(--border-color); display: flex; justify-content: space-between; align-items: center; }
        .modal-body { padding: 20px; overflow-y: auto; color: var(--text-muted); }
        .step-item { margin-bottom: 15px; padding-left: 15px; border-left: 2px solid var(--accent-primary); }
        .btn-start { width: 100%; padding: 15px; background: var(--accent-primary); color: white; border: none; cursor: pointer; font-weight: bold; }

        /* Scrollbar */
        ::-webkit-scrollbar { width: 8px; height: 8px; }
        ::-webkit-scrollbar-track { background: var(--bg-body); }
        ::-webkit-scrollbar-thumb { background: var(--border-color); border-radius: 4px; }
    </style>
</head>
<body>

    <!-- Header with Device Switcher & Actions -->
    <header>
        <div class="brand">
            <i class="fa-solid fa-layer-group"></i>
            <span>Pro Studio</span>
        </div>

        <!-- Device Switcher -->
        <div class="device-switcher">
            <button class="device-btn active" onclick="setDevice('desktop')" title="Desktop View">
                <i class="fa-solid fa-desktop"></i>
            </button>
            <button class="device-btn" onclick="setDevice('tablet')" title="Tablet View">
                <i class="fa-solid fa-tablet-screen-button"></i>
            </button>
            <button class="device-btn" onclick="setDevice('mobile')" title="Mobile View">
                <i class="fa-solid fa-mobile-screen-button"></i>
            </button>
        </div>

        <!-- Action Buttons -->
        <div class="header-actions">
            <!-- Tombol Create Website (Baru) -->
            <button class="btn btn-create" id="btnCreate" onclick="sendToWhatsApp()">
                <i class="fa-brands fa-whatsapp"></i> Create Website Anda
            </button>
            
            <!-- Tombol Tutorial -->
            <button class="btn btn-tutorial" onclick="openTutorial()">
                <i class="fa-solid fa-book-open"></i> Tutorial
            </button>
        </div>
    </header>

    <!-- Main Workspace -->
    <div class="workspace">
        
        <!-- Editor Panel -->
        <div class="editor-container">
            <div class="panel-label">
                <span><i class="fa-solid fa-code"></i> HTML/CSS Editor</span>
                <span style="color: var(--success);"><i class="fa-solid fa-circle"></i> Live</span>
            </div>
            <textarea id="code-editor" spellcheck="false"></textarea>
        </div>

        <!-- Preview Panel -->
        <div class="preview-wrapper">
            <div id="device-frame" class="mode-desktop">
                <iframe id="preview-frame"></iframe>
            </div>
        </div>
    </div>

    <!-- Tutorial Modal -->
    <div class="modal-overlay" id="tutorialModal">
        <div class="modal-card">
            <div class="modal-header">
                <h3>Panduan Responsif</h3>
                <button onclick="closeTutorial()" style="background:none;border:none;color:white;font-size:1.2rem;cursor:pointer">&times;</button>
            </div>
            <div class="modal-body">
                <div class="step-item">
                    <strong>1. Pilih Perangkat</strong><br>
                    Gunakan tombol ikon (Desktop/Tablet/HP) di menu atas untuk melihat bagaimana website Anda terlihat di berbagai ukuran layar.
                </div>
                <div class="step-item">
                    <strong>2. Edit Kode</strong><br>
                    Ketik kode HTML di panel kiri. Perubahan akan langsung muncul di "layar HP" jika mode mobile dipilih.
                </div>
                <div class="step-item">
                    <strong>3. Kirim Hasil</strong><br>
                    Jika sudah selesai, klik tombol ungu <b>"Create Website Anda"</b> di pojok kanan atas. Kode akan otomatis terkirim ke WhatsApp admin.
                </div>
            </div>
            <button class="btn-start" onclick="startCoding()">Mengerti, Mulai!</button>
        </div>
    </div>

    <script>
        // Default Code
        const defaultCode = `<!DOCTYPE html>
<html>
<head>
    <style>
        body {
            font-family: sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f0f9ff;
            text-align: center;
        }
        .card {
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
            max-width: 400px;
            margin: 50px auto;
        }
        h1 { color: #3b82f6; }
        p { color: #64748b; }
        button {
            background: #3b82f6;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
            margin-top: 15px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="card">
        <h1>Halo Dunia!</h1>
        <p>Website ini dibuat dengan Pro HTML Studio.</p>
        <button onclick="alert('Berhasil!')">Klik Saya</button>
    </div>
</body>
</html>`;

        const editor = document.getElementById('code-editor');
        const previewFrame = document.getElementById('preview-frame');
        const deviceFrame = document.getElementById('device-frame');
        const modal = document.getElementById('tutorialModal');
        const btns = document.querySelectorAll('.device-btn');
        const btnCreate = document.getElementById('btnCreate');

        // Fungsi Update Preview
        function updatePreview() {
            const code = editor.value;
            const doc = previewFrame.contentDocument || previewFrame.contentWindow.document;
            doc.open();
            doc.write(code);
            doc.close();
        }

        // Fungsi Ganti Device
        function setDevice(type) {
            deviceFrame.className = '';
            if(type === 'mobile') deviceFrame.classList.add('mode-mobile');
            else if (type === 'tablet') deviceFrame.classList.add('mode-tablet');
            else deviceFrame.classList.add('mode-desktop');

            btns.forEach(btn => btn.classList.remove('active'));
            event.currentTarget.classList.add('active');
        }

        // --- FUNGSI KIRIM KE WHATSAPP ---
        function sendToWhatsApp() {
            const code = editor.value;
            
            // Ubah tampilan tombol jadi loading
            const originalText = btnCreate.innerHTML;
            btnCreate.innerHTML = '<i class="fa-solid fa-spinner fa-spin"></i> Memproses...';
            
            setTimeout(() => {
                // Nomor Tujuan (Format Internasional tanpa +)
                const phoneNumber = "6285882382854"; 
                
                // Membuat pesan
                const message = `Halo, saya ingin membuat website. Berikut adalah kode HTML yang telah saya buat:\n\n${code}`;
                
                // Encode pesan agar aman untuk URL
                const encodedMessage = encodeURIComponent(message);
                
                // Buka WhatsApp
                const waURL = `https://wa.me/${phoneNumber}?text=${encodedMessage}`;
                window.open(waURL, '_blank');
                
                // Kembalikan tombol ke semula
                btnCreate.innerHTML = originalText;
            }, 800); // Delay sedikit agar terasa ada proses
        }

        // Event Listeners
        editor.addEventListener('input', updatePreview);

        // Init
        editor.value = defaultCode;
        updatePreview();

        // Modal Logic
        function openTutorial() { modal.classList.add('active'); }
        function closeTutorial() { modal.classList.remove('active'); }
        function startCoding() { closeTutorial(); editor.focus(); }
        
        window.onload = () => setTimeout(openTutorial, 500);
    </script>
</body>
</html>
