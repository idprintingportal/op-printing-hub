<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Skillo ID Print Solutions</title>
    
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans:wght@400;700&display=swap" rel="stylesheet">
    
    <!-- External JS Libraries -->
    <script defer src="https://cdn.jsdelivr.net/npm/pdfjs-dist@2.16.105/build/pdf.min.js"></script>
    <script defer src="https://cdn.jsdelivr.net/npm/pdf-lib@1.17.1/dist/pdf-lib.min.js"></script>
    <script defer src="https://cdn.jsdelivr.net/npm/jspdf@2.5.1/dist/jspdf.umd.min.js"></script>
    <script defer src="https://cdn.jsdelivr.net/npm/jszip@3.10.1/dist/jszip.min.js"></script>
    
    <!-- Cropper.js -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/cropperjs@1.5.13/dist/cropper.min.css"/>
    <script defer src="https://cdn.jsdelivr.net/npm/cropperjs@1.5.13/dist/cropper.min.js"></script>

    <style>
        :root {
            --bg-gradient: linear-gradient(135deg, #0f172a 0%, #1e1b4b 50%, #0f172a 100%);
            --card-bg: rgba(30, 41, 59, 0.88);
            --accent-blue: #38bdf8;
            --btn-add: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);
            --btn-download: linear-gradient(135deg, #10b981 0%, #059669 100%);
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --border-color: rgba(255, 255, 255, 0.1);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Poppins', sans-serif;
        }

        body {
            background: var(--bg-gradient);
            min-height: 100vh;
            padding: 20px 10px;
            display: flex;
            flex-direction: column;
            align-items: center;
            color: var(--text-main);
        }

        .portal-main-heading {
            font-size: 26px;
            font-weight: 800;
            letter-spacing: 1.5px;
            text-transform: uppercase;
            background: linear-gradient(135deg, #38bdf8 0%, #a855f7 50%, #f43f5e 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 20px;
            text-align: center;
        }

        #mainApp {
            width: 100%;
            max-width: 1100px;
        }

        .container {
            background: var(--card-bg);
            backdrop-filter: blur(16px);
            border: 1px solid var(--border-color);
            padding: 25px 20px;
            border-radius: 20px;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.4);
            width: 100%;
            text-align: center;
        }

        .upload-section {
            display: flex;
            gap: 15px;
            justify-content: center;
            margin: 20px 0;
            flex-wrap: wrap;
        }

        .upload-box {
            border: 2px dashed rgba(56, 189, 248, 0.4);
            padding: 25px;
            border-radius: 14px;
            cursor: pointer;
            background: rgba(15, 23, 42, 0.6);
            flex: 1;
            min-width: 250px;
            transition: 0.3s;
        }

        .upload-box:hover {
            border-color: var(--accent-blue);
            background: rgba(56, 189, 248, 0.08);
        }

        input[type="file"] {
            display: none;
        }

        .control-panel {
            background: rgba(15, 23, 42, 0.7);
            border: 1px solid var(--border-color);
            border-radius: 14px;
            padding: 16px;
            max-width: 500px;
            margin: 20px auto;
        }

        .qty-select-group {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            margin-top: 10px;
        }

        .qty-input {
            width: 80px;
            padding: 6px;
            border-radius: 8px;
            background: rgba(15, 23, 42, 0.9);
            border: 1px solid var(--accent-blue);
            color: #fff;
            font-size: 15px;
            text-align: center;
        }

        .quick-qty-btn {
            padding: 6px 14px;
            background: #334155;
            border: 1px solid rgba(255, 255, 255, 0.1);
            color: #fff;
            border-radius: 6px;
            font-size: 12px;
            cursor: pointer;
        }

        .btn-group {
            display: flex;
            gap: 12px;
            justify-content: center;
            margin-top: 20px;
        }

        .action-btn {
            padding: 12px 28px;
            font-size: 14px;
            font-weight: 600;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            color: #fff;
            transition: 0.3s;
        }

        .btn-add { background: var(--btn-add); }
        .btn-reset { 
            background: rgba(239, 68, 68, 0.2); 
            border: 1px solid rgba(239, 68, 68, 0.4); 
            color: #fca5a5; 
        }

        .file-gallery-list {
            display: flex;
            flex-wrap: wrap;
            gap: 14px;
            justify-content: center;
            margin: 15px 0;
            min-height: 50px;
            padding: 14px;
            background: rgba(15, 23, 42, 0.6);
            border-radius: 12px;
        }
    </style>
</head>
<body>

    <h1 class="portal-main-heading">Skillo ID Print Solutions</h1>

    <!-- Directly Accessible Main App -->
    <div id="mainApp">
        <div class="container">
            <h2 style="font-size: 20px; color: var(--accent-blue);">ID Card Printing Suite</h2>
            <p style="color: var(--text-muted); font-size: 13px;">Aapki hosting par chalne wala standalone print tool.</p>

            <div class="upload-section">
                <div class="upload-box" onclick="document.getElementById('fileInput').click()">
                    <h3 style="font-size: 15px; color: var(--accent-blue);">Upload File / Image</h3>
                    <p style="font-size: 12px; color: var(--text-muted); margin-top: 4px;">PDF, JPG, ya PNG files select karein</p>
                    <input type="file" id="fileInput" accept="application/pdf,image/*" multiple>
                </div>
            </div>

            <div class="file-gallery-list" id="fileGalleryList">
                <p style="color: var(--text-muted); font-size: 12px;">Koyi file select nahi hui hai.</p>
            </div>

            <div class="control-panel">
                <label style="font-size: 13px; font-weight: 600; color: var(--accent-blue);">Quantity Select Karein</label>
                <div class="qty-select-group">
                    <button class="quick-qty-btn" onclick="setQuantity(1)">Single</button>
                    <button class="quick-qty-btn" onclick="setQuantity(5)">5 Batch</button>
                    <button class="quick-qty-btn" onclick="setQuantity(10)">10 Batch</button>
                    <input type="number" id="cardQuantity" class="qty-input" value="1" min="1" max="100">
                </div>
            </div>

            <div class="btn-group">
                <button class="action-btn btn-add" id="processBtn">Generate Print Layout</button>
                <button class="action-btn btn-reset" id="resetBtn">Clear All</button>
            </div>

            <div class="preview-container" id="previewContainer" style="margin-top: 20px;"></div>
        </div>
    </div>

    <script>
        function setQuantity(val) {
            document.getElementById('cardQuantity').value = val;
        }

        // Basic File Selection Handler
        document.getElementById('fileInput').addEventListener('change', function(e) {
            const list = document.getElementById('fileGalleryList');
            list.innerHTML = '';
            
            if (this.files.length === 0) {
                list.innerHTML = '<p style="color: var(--text-muted); font-size: 12px;">Koyi file select nahi hui hai.</p>';
                return;
            }

            Array.from(this.files).forEach(file => {
                const item = document.createElement('div');
                item.style.cssText = "background: #0f172a; padding: 8px 12px; border-radius: 6px; font-size: 12px; border: 1px solid var(--accent-blue);";
                item.innerText = file.name;
                list.appendChild(item);
            });
        });

        document.getElementById('resetBtn').addEventListener('click', function() {
            document.getElementById('fileInput').value = '';
            document.getElementById('fileGalleryList').innerHTML = '<p style="color: var(--text-muted); font-size: 12px;">Koyi file select nahi hui hai.</p>';
            document.getElementById('previewContainer').innerHTML = '';
        });
    </script>
</body>
</html>
