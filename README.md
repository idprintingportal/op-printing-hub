<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Skillo ID Print Solutions - Standalone</title>
    
    <!-- Fonts & Libraries -->
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/2.16.105/pdf.min.js"></script>
    <script>pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/2.16.105/pdf.worker.min.js';</script>

    <style>
        :root {
            --bg: #0f172a;
            --card-bg: rgba(30, 41, 59, 0.9);
            --accent: #38bdf8;
            --accent-hover: #0284c7;
            --success: #10b981;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --border: rgba(255, 255, 255, 0.12);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Poppins', sans-serif;
        }

        body {
            background: radial-gradient(circle at top, #1e1b4b 0%, #0f172a 100%);
            min-height: 100vh;
            padding: 20px;
            color: var(--text-main);
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .header-title {
            font-size: 28px;
            font-weight: 800;
            letter-spacing: 1px;
            background: linear-gradient(135deg, #38bdf8 0%, #a855f7 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 24px;
            text-align: center;
        }

        .app-container {
            width: 100%;
            max-width: 900px;
            background: var(--card-bg);
            border: 1px solid var(--border);
            border-radius: 20px;
            padding: 25px;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.5);
            backdrop-filter: blur(10px);
        }

        .upload-area {
            border: 2px dashed var(--accent);
            border-radius: 14px;
            padding: 30px 20px;
            text-align: center;
            background: rgba(15, 23, 42, 0.5);
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .upload-area:hover {
            background: rgba(56, 189, 248, 0.1);
            border-color: #60a5fa;
        }

        .file-input { display: none; }

        .controls-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin: 20px 0;
            align-items: center;
        }

        .control-box {
            background: rgba(15, 23, 42, 0.7);
            padding: 12px 16px;
            border-radius: 10px;
            border: 1px solid var(--border);
        }

        .control-box label {
            font-size: 12px;
            color: var(--text-muted);
            display: block;
            margin-bottom: 6px;
        }

        .quick-btn-group {
            display: flex;
            gap: 8px;
        }

        .q-btn {
            background: #334155;
            border: none;
            color: #fff;
            padding: 6px 12px;
            border-radius: 6px;
            font-size: 12px;
            cursor: pointer;
            flex: 1;
        }

        .q-btn:hover { background: var(--accent-hover); }

        .btn-group {
            display: flex;
            gap: 15px;
            margin-top: 10px;
        }

        .btn {
            flex: 1;
            padding: 14px;
            border: none;
            border-radius: 10px;
            font-weight: 600;
            cursor: pointer;
            color: #fff;
            transition: 0.2s;
            font-size: 14px;
        }

        .btn-process { background: linear-gradient(135deg, #38bdf8 0%, #0284c7 100%); }
        .btn-process:hover { opacity: 0.9; }

        .btn-print { background: linear-gradient(135deg, #10b981 0%, #059669 100%); display: none; }
        .btn-print:hover { opacity: 0.9; }

        .btn-reset { background: rgba(239, 68, 68, 0.2); border: 1px solid rgba(239, 68, 68, 0.4); color: #fca5a5; }

        /* Print Sheet Layout */
        #printArea {
            margin-top: 30px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .a4-sheet {
            width: 210mm;
            min-height: 297mm;
            background: #ffffff;
            padding: 10mm;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            border-radius: 4px;
            display: grid;
            grid-template-columns: repeat(2, 85.6mm);
            grid-auto-rows: 53.9mm;
            gap: 5mm 8mm;
            justify-content: center;
            align-content: start;
        }

        .card-frame {
            width: 85.6mm;
            height: 53.9mm;
            border: 1px dashed #ccc;
            border-radius: 4mm;
            overflow: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
            background: #fff;
        }

        .card-frame canvas {
            width: 100%;
            height: 100%;
            object-fit: contain;
        }

        /* Direct Browser Print Styling */
        @media print {
            body * { visibility: hidden; }
            #printArea, #printArea * { visibility: visible; }
            #printArea {
                position: absolute;
                left: 0;
                top: 0;
                width: 100%;
            }
            .a4-sheet {
                box-shadow: none;
                margin: 0;
                padding: 10mm;
            }
        }
    </style>
</head>
<body>

    <h1 class="header-title">Skillo ID Print Solutions</h1>

    <div class="app-container">
        <!-- File Uploader -->
        <div class="upload-area" onclick="document.getElementById('fileInput').click()">
            <h3 style="font-size: 16px; color: var(--accent);">PDF ya Image Files Upload Karein</h3>
            <p style="font-size: 12px; color: var(--text-muted); margin-top: 4px;">Click karke files chunein (PDF, JPG, PNG)</p>
            <input type="file" id="fileInput" class="file-input" accept="application/pdf,image/*" multiple>
        </div>

        <div id="fileList" style="margin-top: 10px; font-size: 12px; color: var(--text-muted);"></div>

        <!-- Controls -->
        <div class="controls-grid">
            <div class="control-box">
                <label>Cards Per Page (Batch Size)</label>
                <div class="quick-btn-group">
                    <button class="q-btn" onclick="setBatch(2)">2 Cards</button>
                    <button class="q-btn" onclick="setBatch(5)">5 Cards</button>
                    <button class="q-btn" onclick="setBatch(10)">10 Cards</button>
                </div>
            </div>
            <div class="control-box">
                <label>Manual Quantity</label>
                <input type="number" id="cardLimit" value="10" min="1" max="20" style="width: 100%; background: #0f172a; border: 1px solid var(--border); color: #fff; padding: 6px; border-radius: 6px;">
            </div>
        </div>

        <!-- Action Buttons -->
        <div class="btn-group">
            <button class="btn btn-process" id="processBtn" onclick="processFiles()">Layout Process Karein</button>
            <button class="btn btn-print" id="printBtn" onclick="window.print()">A4 Sheet Print Karein</button>
            <button class="btn btn-reset" onclick="resetApp()">Reset</button>
        </div>

        <!-- Printable Layout -->
        <div id="printArea">
            <div class="a4-sheet" id="a4Page"></div>
        </div>
    </div>

    <script>
        let uploadedFiles = [];

        document.getElementById('fileInput').addEventListener('change', function(e) {
            uploadedFiles = Array.from(e.target.files);
            const listDiv = document.getElementById('fileList');
            if(uploadedFiles.length > 0) {
                listDiv.innerHTML = `Selected Files: <b>${uploadedFiles.length}</b> file(s)`;
            } else {
                listDiv.innerHTML = '';
            }
        });

        function setBatch(num) {
            document.getElementById('cardLimit').value = num;
        }

        async function processFiles() {
            if (uploadedFiles.length === 0) {
                alert("Kripya pehle file upload karein!");
                return;
            }

            const sheet = document.getElementById('a4Page');
            sheet.innerHTML = '';
            const limit = parseInt(document.getElementById('cardLimit').value) || 10;
            let currentCount = 0;

            for (let file of uploadedFiles) {
                if (currentCount >= limit) break;

                if (file.type === "application/pdf") {
                    const arrayBuffer = await file.arrayBuffer();
                    const pdf = await pdfjsLib.getDocument({ data: arrayBuffer }).promise;

                    for (let pageNum = 1; pageNum <= pdf.numPages; pageNum++) {
                        if (currentCount >= limit) break;
                        const page = await pdf.getPage(pageNum);
                        const canvas = await renderPdfPageToCanvas(page);
                        addCanvasToSheet(canvas);
                        currentCount++;
                    }
                } else if (file.type.startsWith("image/")) {
                    const canvas = await renderImageToCanvas(file);
                    addCanvasToSheet(canvas);
                    currentCount++;
                }
            }

            if (currentCount > 0) {
                document.getElementById('printBtn').style.display = 'block';
            }
        }

        function renderPdfPageToCanvas(page) {
            return new Promise((resolve) => {
                const viewport = page.getViewport({ scale: 2 });
                const canvas = document.createElement('canvas');
                const ctx = canvas.getContext('2d');
                canvas.width = viewport.width;
                canvas.height = viewport.height;

                page.render({ canvasContext: ctx, viewport: viewport }).promise.then(() => {
                    resolve(canvas);
                });
            });
        }

        function renderImageToCanvas(file) {
            return new Promise((resolve) => {
                const reader = new FileReader();
                reader.onload = function(e) {
                    const img = new Image();
                    img.onload = function() {
                        const canvas = document.createElement('canvas');
                        const ctx = canvas.getContext('2d');
                        canvas.width = img.width;
                        canvas.height = img.height;
                        ctx.drawImage(img, 0, 0);
                        resolve(canvas);
                    };
                    img.src = e.target.result;
                };
                reader.readAsDataURL(file);
            });
        }

        function addCanvasToSheet(canvas) {
            const sheet = document.getElementById('a4Page');
            const frame = document.createElement('div');
            frame.className = 'card-frame';
            frame.appendChild(canvas);
            sheet.appendChild(frame);
        }

        function resetApp() {
            uploadedFiles = [];
            document.getElementById('fileInput').value = '';
            document.getElementById('fileList').innerHTML = '';
            document.getElementById('a4Page').innerHTML = '';
            document.getElementById('printBtn').style.display = 'none';
        }
    </script>
</body>
</html>
