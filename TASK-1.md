<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>LocalShare — P2P File & Media Sharing</title>
  <meta name="description" content="LocalShare is a responsive local network file and media sharing interface." />
  <meta http-equiv="Content-Security-Policy" content="default-src 'self' https: data:; img-src 'self' https: data:; style-src 'self' 'unsafe-inline' https:; font-src https: data:; script-src 'self' 'unsafe-inline' https:;" />
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&family=Montserrat:wght@600;700&display=swap" rel="stylesheet" />
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/tabler-icons.min.css" />

  <style>
    *, *::before, *::after {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    :root {
      --mocha: #A5856E;
      --mocha-light: #F5EDE6;
      --mocha-mid: #C9A891;
      --mocha-dark: #6B4F3A;
      --blue: #A0D4E0;
      --blue-light: #E8F6FA;
      --blue-dark: #2E7D9A;
      --grey: #F2F0EA;
      --grey-mid: #B4B2A9;
      --grey-dark: #444441;
      --grey-border: #D3D1C7;
      --green: #1D9E75;
      --white: #FFFFFF;
      --text: #2C2C2A;
      --text-muted: #888780;
      --radius: 12px;
      --radius-sm: 8px;
      --radius-pill: 20px;
      --font-display: 'Montserrat', sans-serif;
      --font-body: 'Inter', sans-serif;
    }

    html { scroll-behavior: smooth; }

    body {
      font-family: var(--font-body);
      background: var(--grey);
      color: var(--text);
      font-size: clamp(14px, 1.2vw, 16px);
      line-height: 1.6;
      min-height: 100vh;
    }

    nav {
      background: var(--white);
      border-bottom: 0.5px solid var(--grey-border);
      padding: 0 clamp(16px, 3vw, 24px);
      min-height: 60px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      position: sticky;
      top: 0;
      z-index: 50;
    }

    .logo {
      font-family: var(--font-display);
      font-weight: 700;
      font-size: 1.125rem;
      color: var(--mocha-dark);
      display: flex;
      align-items: center;
      gap: 9px;
      text-decoration: none;
    }

    .logo-icon {
      width: 32px;
      height: 32px;
      background: var(--mocha);
      border-radius: var(--radius-sm);
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .logo-icon i {
      font-size: 18px;
      color: var(--white);
    }

    .nav-right {
      display: flex;
      align-items: center;
      gap: 14px;
      flex-wrap: wrap;
      justify-content: flex-end;
    }

    .status-pill {
      display: flex;
      align-items: center;
      gap: 7px;
      background: var(--blue-light);
      border: 0.5px solid var(--blue);
      border-radius: var(--radius-pill);
      padding: 5px 14px;
      font-size: 12px;
      color: var(--blue-dark);
      font-weight: 500;
    }

    .status-dot {
      width: 7px;
      height: 7px;
      background: var(--green);
      border-radius: 50%;
      flex-shrink: 0;
      animation: pulse 2s ease-in-out infinite;
    }

    @keyframes pulse {
      0%, 100% { opacity: 1; }
      50% { opacity: 0.3; }
    }

    .peer-count {
      font-size: 12px;
      color: var(--text-muted);
      white-space: nowrap;
    }

    main {
      max-width: 960px;
      margin: 0 auto;
      padding: 28px 20px 60px;
    }

    .section-label {
      font-size: 11px;
      font-weight: 600;
      letter-spacing: 0.09em;
      color: var(--text-muted);
      text-transform: uppercase;
      margin-bottom: 12px;
    }

    .drop-zone {
      background: var(--white);
      border: 2px dashed var(--mocha-mid);
      border-radius: var(--radius);
      padding: clamp(28px, 5vw, 48px) 24px;
      text-align: center;
      cursor: pointer;
      transition: background 0.2s ease, border-color 0.2s ease, transform 0.2s ease;
      margin-bottom: 24px;
      position: relative;
      outline: none;
    }

    .drop-zone:hover,
    .drop-zone.drag-over,
    .drop-zone:focus-visible {
      background: var(--mocha-light);
      border-color: var(--mocha-dark);
      transform: translateY(-1px);
    }

    .drop-zone input[type="file"] {
      position: absolute;
      inset: 0;
      opacity: 0;
      cursor: pointer;
      width: 100%;
      height: 100%;
    }

    .drop-icon {
      width: 64px;
      height: 64px;
      background: var(--mocha-light);
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      margin: 0 auto 16px;
      border: 1px solid var(--mocha-mid);
    }

    .drop-icon i {
      font-size: 30px;
      color: var(--mocha);
    }

    .drop-zone h2 {
      font-family: var(--font-display);
      font-size: clamp(16px, 2vw, 18px);
      font-weight: 700;
      color: var(--mocha-dark);
      margin-bottom: 6px;
    }

    .drop-zone p {
      font-size: 13px;
      color: var(--text-muted);
      max-width: 340px;
      margin: 0 auto;
    }

    .drop-tags {
      display: flex;
      justify-content: center;
      gap: 8px;
      margin-top: 16px;
      flex-wrap: wrap;
    }

    .drop-tag {
      background: var(--grey);
      border: 0.5px solid var(--grey-border);
      border-radius: var(--radius-pill);
      padding: 3px 10px;
      font-size: 11px;
      color: var(--text-muted);
      font-weight: 500;
    }

    .grid-2 {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 16px;
      margin-bottom: 28px;
    }

    .card {
      background: var(--white);
      border: 0.5px solid var(--grey-border);
      border-radius: var(--radius);
      padding: 18px;
    }

    .card-title {
      font-family: var(--font-display);
      font-size: 13px;
      font-weight: 700;
      color: var(--mocha-dark);
      margin-bottom: 14px;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .card-title i {
      font-size: 16px;
      color: var(--mocha);
    }

    .peer-list {
      display: flex;
      flex-direction: column;
      gap: 9px;
    }

    .peer-item {
      display: flex;
      align-items: center;
      gap: 11px;
      padding: 9px 10px;
      background: var(--grey);
      border-radius: var(--radius-sm);
      transition: background 0.15s;
    }

    .peer-item:hover {
      background: var(--mocha-light);
    }

    .peer-avatar {
      width: 36px;
      height: 36px;
      border-radius: 50%;
      background: var(--blue-light);
      border: 0.5px solid var(--blue);
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 12px;
      font-weight: 600;
      color: var(--blue-dark);
      flex-shrink: 0;
    }

    .peer-info {
      flex: 1;
      min-width: 0;
    }

    .peer-name, .transfer-name {
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
    }

    .peer-name {
      font-size: 13px;
      font-weight: 500;
      color: var(--text);
    }

    .peer-sub {
      font-size: 11px;
      color: var(--text-muted);
      margin-top: 1px;
    }

    .peer-action {
      background: var(--mocha-light);
      border: 0.5px solid var(--mocha-mid);
      border-radius: var(--radius-sm);
      padding: 5px 12px;
      font-size: 12px;
      font-weight: 500;
      color: var(--mocha-dark);
      cursor: pointer;
      transition: background 0.15s, color 0.15s;
      white-space: nowrap;
      font-family: var(--font-body);
    }

    .peer-action:hover {
      background: var(--mocha);
      color: var(--white);
      border-color: var(--mocha);
    }

    .peer-action:focus-visible,
    .btn:focus-visible,
    .media-thumb:focus-visible {
      outline: 2px solid var(--mocha);
      outline-offset: 2px;
    }

    .media-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 9px;
    }

    @media (max-width: 480px) {
      .media-grid {
        grid-template-columns: repeat(2, 1fr);
      }
    }

    .media-thumb {
      aspect-ratio: 1 / 1;
      background: var(--grey);
      border: 0.5px solid var(--grey-border);
      border-radius: var(--radius-sm);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      position: relative;
      overflow: hidden;
      transition: border-color 0.15s;
      outline: none;
    }

    .media-thumb:hover {
      border-color: var(--mocha-mid);
    }

    .media-thumb i {
      font-size: 22px;
      color: var(--text-muted);
    }

    .thumb-name {
      font-size: 10px;
      color: var(--text-muted);
      margin-top: 5px;
      text-align: center;
      padding: 0 6px;
      line-height: 1.3;
      word-break: break-word;
    }

    .thumb-overlay {
      position: absolute;
      inset: 0;
      background: rgba(165, 133, 110, 0.18);
      display: flex;
      align-items: center;
      justify-content: center;
      opacity: 0;
      transition: opacity 0.2s;
    }

    .thumb-overlay i {
      font-size: 22px;
      color: var(--mocha-dark);
    }

    .media-thumb:hover .thumb-overlay,
    .media-thumb:focus-visible .thumb-overlay {
      opacity: 1;
    }

    .media-thumb.add-more {
      border-style: dashed;
      cursor: default;
    }

    .transfers-list {
      display: flex;
      flex-direction: column;
      gap: 10px;
      margin-bottom: 28px;
    }

    .transfer-item {
      background: var(--white);
      border: 0.5px solid var(--grey-border);
      border-radius: var(--radius-sm);
      padding: 14px 16px;
    }

    .transfer-top {
      display: flex;
      align-items: center;
      gap: 12px;
      margin-bottom: 10px;
    }

    .transfer-icon {
      width: 38px;
      height: 38px;
      background: var(--blue-light);
      border-radius: var(--radius-sm);
      display: flex;
      align-items: center;
      justify-content: center;
      flex-shrink: 0;
    }

    .transfer-icon i {
      font-size: 18px;
      color: var(--blue-dark);
    }

    .transfer-info {
      flex: 1;
      min-width: 0;
    }

    .transfer-name {
      font-size: 13px;
      font-weight: 500;
      color: var(--text);
    }

    .transfer-meta {
      font-size: 11px;
      color: var(--text-muted);
      margin-top: 2px;
    }

    .transfer-pct {
      font-size: 13px;
      font-weight: 600;
      color: var(--mocha-dark);
      margin-left: auto;
      min-width: 36px;
      text-align: right;
    }

    .transfer-pct.done {
      color: var(--green);
    }

    .bar-track {
      height: 5px;
      background: var(--grey);
      border-radius: 4px;
      overflow: hidden;
    }

    .bar-fill {
      height: 100%;
      border-radius: 4px;
      background: var(--mocha);
      transition: width 0.35s ease;
    }

    .bar-fill.done {
      background: var(--green);
    }

    .bottom-bar {
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
    }

    .btn {
      display: inline-flex;
      align-items: center;
      gap: 7px;
      padding: 10px 18px;
      border-radius: var(--radius-sm);
      font-family: var(--font-body);
      font-size: 13px;
      font-weight: 500;
      cursor: pointer;
      border: 0.5px solid var(--grey-border);
      background: var(--white);
      color: var(--text);
      transition: background 0.15s, border-color 0.15s;
      text-decoration: none;
    }

    .btn:hover {
      background: var(--grey);
      border-color: var(--grey-mid);
    }

    .btn-primary {
      background: var(--mocha);
      border-color: var(--mocha);
      color: var(--white);
    }

    .btn-primary:hover {
      background: var(--mocha-dark);
      border-color: var(--mocha-dark);
    }

    .empty-state {
      text-align: center;
      padding: 28px 16px;
      color: var(--text-muted);
      font-size: 13px;
    }

    .empty-state i {
      font-size: 32px;
      display: block;
      margin-bottom: 8px;
      color: var(--grey-mid);
    }

    .toast {
      position: fixed;
      bottom: 28px;
      left: 50%;
      transform: translateX(-50%) translateY(12px);
      background: var(--mocha-dark);
      color: var(--white);
      padding: 11px 20px;
      border-radius: var(--radius-pill);
      font-size: 13px;
      font-weight: 500;
      z-index: 999;
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.25s ease, transform 0.25s ease;
      white-space: nowrap;
      max-width: calc(100vw - 40px);
      overflow: hidden;
      text-overflow: ellipsis;
    }

    .toast.visible {
      opacity: 1;
      transform: translateX(-50%) translateY(0);
    }

    @media (max-width: 480px) {
      nav { padding: 0 16px; }
      .peer-count { display: none; }
      main { padding: 20px 14px 60px; }
      .drop-zone { padding: 36px 16px; }
      .bottom-bar { flex-direction: column; }
      .btn { width: 100%; justify-content: center; }
    }
  </style>
</head>

<body>
  <nav aria-label="Main navigation">
    <a href="#" class="logo" aria-label="LocalShare home">
      <div class="logo-icon" aria-hidden="true">
        <i class="ti ti-share"></i>
      </div>
      LocalShare
    </a>

    <div class="nav-right">
      <div class="status-pill" role="status" aria-live="polite">
        <span class="status-dot" aria-hidden="true"></span>
        Connected to LAN
      </div>
      <span class="peer-count" id="peerLabel">3 peers nearby</span>
    </div>
  </nav>

  <main>
    <p class="section-label">Send a file</p>

    <div class="drop-zone" id="dropZone" role="region" aria-label="File drop zone" tabindex="0">
      <input
        type="file"
        multiple
        id="fileInput"
        aria-label="Choose files to share"
      />

      <div class="drop-icon" aria-hidden="true">
        <i class="ti ti-cloud-upload"></i>
      </div>

      <h2>Drop files here or tap to browse</h2>
      <p>No size limit · Stays on your local network · Blazing-fast local speeds</p>

      <div class="drop-tags" aria-hidden="true">
        <span class="drop-tag">Videos</span>
        <span class="drop-tag">Images</span>
        <span class="drop-tag">Documents</span>
        <span class="drop-tag">ZIP / Archives</span>
        <span class="drop-tag">Any format</span>
      </div>
    </div>

    <div class="grid-2">
      <section class="card" aria-labelledby="peers-heading">
        <div class="card-title" id="peers-heading">
          <i class="ti ti-wifi" aria-hidden="true"></i>
          Nearby peers
        </div>

        <div class="peer-list" id="peerList" role="list">
          <div class="peer-item" role="listitem">
            <div class="peer-avatar" aria-hidden="true">AN</div>
            <div class="peer-info">
              <div class="peer-name">Ananya's Mac</div>
              <div class="peer-sub">192.168.1.12 · 2.4 MB/s</div>
            </div>
            <button class="peer-action" type="button" data-peer="Ananya's Mac">Send</button>
          </div>

          <div class="peer-item" role="listitem">
            <div class="peer-avatar" style="background:#E8F6FA;color:#2E7D9A" aria-hidden="true">RK</div>
            <div class="peer-info">
              <div class="peer-name">Rohan's Laptop</div>
              <div class="peer-sub">192.168.1.18 · 5.1 MB/s</div>
            </div>
            <button class="peer-action" type="button" data-peer="Rohan's Laptop">Send</button>
          </div>

          <div class="peer-item" role="listitem">
            <div class="peer-avatar" style="background:#F5EDE6;color:#6B4F3A" aria-hidden="true">PS</div>
            <div class="peer-info">
              <div class="peer-name">Priya's Phone</div>
              <div class="peer-sub">192.168.1.25 · 1.8 MB/s</div>
            </div>
            <button class="peer-action" type="button" data-peer="Priya's Phone">Send</button>
          </div>
        </div>
      </section>

      <section class="card" aria-labelledby="media-heading">
        <div class="card-title" id="media-heading">
          <i class="ti ti-photo" aria-hidden="true"></i>
          Shared media
        </div>

        <div class="media-grid" role="list">
          <div class="media-thumb" role="button" tabindex="0" data-file="demo_reel.mp4" aria-label="Preview demo_reel.mp4">
            <i class="ti ti-video" aria-hidden="true"></i>
            <span class="thumb-name">demo_reel.mp4</span>
            <div class="thumb-overlay" aria-hidden="true"><i class="ti ti-player-play"></i></div>
          </div>

          <div class="media-thumb" role="button" tabindex="0" data-file="wireframe_v2.png" aria-label="Preview wireframe_v2.png">
            <i class="ti ti-photo" aria-hidden="true"></i>
            <span class="thumb-name">wireframe_v2.png</span>
            <div class="thumb-overlay" aria-hidden="true"><i class="ti ti-eye"></i></div>
          </div>

          <div class="media-thumb" role="button" tabindex="0" data-file="bgm_track.mp3" aria-label="Play bgm_track.mp3">
            <i class="ti ti-music" aria-hidden="true"></i>
            <span class="thumb-name">bgm_track.mp3</span>
            <div class="thumb-overlay" aria-hidden="true"><i class="ti ti-player-play"></i></div>
          </div>

          <div class="media-thumb" role="button" tabindex="0" data-file="project_brief.pdf" aria-label="Open project_brief.pdf">
            <i class="ti ti-file-type-pdf" aria-hidden="true"></i>
            <span class="thumb-name">project_brief.pdf</span>
            <div class="thumb-overlay" aria-hidden="true"><i class="ti ti-eye"></i></div>
          </div>

          <div class="media-thumb" role="button" tabindex="0" data-file="assets_bundle.zip" aria-label="Download assets_bundle.zip">
            <i class="ti ti-file-zip" aria-hidden="true"></i>
            <span class="thumb-name">assets_bundle.zip</span>
            <div class="thumb-overlay" aria-hidden="true"><i class="ti ti-download"></i></div>
          </div>

          <div class="media-thumb add-more" role="listitem" aria-label="Add more files">
            <i class="ti ti-plus" aria-hidden="true"></i>
            <span class="thumb-name" style="color:var(--grey-mid)">Add more</span>
          </div>
        </div>
      </section>
    </div>

    <p class="section-label">Active transfers</p>

    <div class="transfers-list" id="transfersList" role="list" aria-live="polite" aria-label="File transfer progress">
      <div class="transfer-item" role="listitem">
        <div class="transfer-top">
          <div class="transfer-icon" aria-hidden="true">
            <i class="ti ti-file-zip"></i>
          </div>
          <div class="transfer-info">
            <div class="transfer-name">assets_bundle.zip</div>
            <div class="transfer-meta" id="meta-demo1">To Rohan's Laptop · 48 MB of 120 MB</div>
          </div>
          <div class="transfer-pct" id="pct-demo1">40%</div>
        </div>
        <div class="bar-track" role="progressbar" aria-valuenow="40" aria-valuemin="0" aria-valuemax="100" aria-label="assets_bundle.zip transfer progress">
          <div class="bar-fill" id="bar-demo1" style="width:40%"></div>
        </div>
      </div>

      <div class="transfer-item" role="listitem">
        <div class="transfer-top">
          <div class="transfer-icon" aria-hidden="true">
            <i class="ti ti-video"></i>
          </div>
          <div class="transfer-info">
            <div class="transfer-name">demo_reel.mp4</div>
            <div class="transfer-meta">From Ananya's Mac · Complete</div>
          </div>
          <div class="transfer-pct done">Done</div>
        </div>
        <div class="bar-track" role="progressbar" aria-valuenow="100" aria-valuemin="0" aria-valuemax="100" aria-label="demo_reel.mp4 transfer complete">
          <div class="bar-fill done" style="width:100%"></div>
        </div>
      </div>
    </div>

    <div class="bottom-bar">
      <button class="btn btn-primary" type="button" id="startBtn">
        <i class="ti ti-rocket" aria-hidden="true"></i>
        Start building
      </button>
      <button class="btn" type="button" id="scanBtn">
        <i class="ti ti-refresh" aria-hidden="true"></i>
        Scan for peers
      </button>
      <button class="btn" type="button" id="settingsBtn">
        <i class="ti ti-settings" aria-hidden="true"></i>
        Settings
      </button>
    </div>
  </main>

  <div class="toast" id="toast" role="status" aria-live="polite" aria-atomic="true"></div>

  <script>
    var dropZone = document.getElementById('dropZone');
    var fileInput = document.getElementById('fileInput');
    var toastTimer;

    function safeToast(message) {
      showToast(String(message).slice(0, 120));
    }

    dropZone.addEventListener('dragover', function (e) {
      e.preventDefault();
      dropZone.classList.add('drag-over');
    });

    dropZone.addEventListener('dragleave', function (e) {
      e.preventDefault();
      dropZone.classList.remove('drag-over');
    });

    dropZone.addEventListener('drop', function (e) {
      e.preventDefault();
      dropZone.classList.remove('drag-over');
      handleFiles(e.dataTransfer.files);
    });

    dropZone.addEventListener('keydown', function (e) {
      if (e.key === 'Enter' || e.key === ' ') fileInput.click();
    });

    fileInput.addEventListener('change', function () {
      handleFiles(this.files);
      this.value = '';
    });

    document.querySelectorAll('.peer-action').forEach(function (btn) {
      btn.addEventListener('click', function () {
        sendFile(btn.getAttribute('data-peer') || 'peer');
      });
    });

    document.querySelectorAll('.media-thumb[role="button"]').forEach(function (thumb) {
      thumb.addEventListener('click', function () {
        previewFile(thumb.getAttribute('data-file') || 'file');
      });
      thumb.addEventListener('keydown', function (e) {
        if (e.key === 'Enter' || e.key === ' ') {
          e.preventDefault();
          thumb.click();
        }
      });
    });

    document.getElementById('startBtn').addEventListener('click', function () {
      showToast('Open your IDE and create index.html — you\'re the architect!');
    });

    document.getElementById('scanBtn').addEventListener('click', function () {
      showToast('Scanning for peers on your network…');
    });

    document.getElementById('settingsBtn').addEventListener('click', function () {
      showToast('Settings panel coming in next sprint!');
    });

    function handleFiles(files) {
      if (!files || files.length === 0) return;
      Array.from(files).forEach(function (file) {
        if (isAllowedFile(file)) addTransferItem(file);
        else safeToast('Blocked unsupported file: ' + file.name);
      });
    }

    function isAllowedFile(file) {
      var allowedMaxMB = 250;
      var sizeMB = file.size / (1024 * 1024);
      return sizeMB <= allowedMaxMB;
    }

    function addTransferItem(file) {
      var list = document.getElementById('transfersList');
      var sizeMB = (file.size / (1024 * 1024)).toFixed(1);
      var icon = 'ti-file';

      if (file.type.indexOf('video/') === 0) icon = 'ti-video';
      else if (file.type.indexOf('image/') === 0) icon = 'ti-photo';
      else if (file.type.indexOf('audio/') === 0) icon = 'ti-music';
      else if (file.type === 'application/pdf') icon = 'ti-file-type-pdf';
      else if (/\.(zip|rar|7z)$/i.test(file.name)) icon = 'ti-file-zip';

      var uid = 'tf-' + Date.now() + '-' + Math.floor(Math.random() * 1000);

      var item = document.createElement('div');
      item.className = 'transfer-item';
      item.setAttribute('role', 'listitem');
      item.innerHTML =
        '<div class="transfer-top">' +
          '<div class="transfer-icon" aria-hidden="true"><i class="ti ' + icon + '"></i></div>' +
          '<div class="transfer-info">' +
            '<div class="transfer-name">' + escapeHTML(file.name) + '</div>' +
            '<div class="transfer-meta" id="meta-' + uid + '">Queued · ' + sizeMB + ' MB</div>' +
          '</div>' +
          '<div class="transfer-pct" id="pct-' + uid + '">0%</div>' +
        '</div>' +
        '<div class="bar-track" role="progressbar" aria-valuenow="0" aria-valuemin="0" aria-valuemax="100" aria-label="' + escapeHTML(file.name) + ' transfer progress">' +
          '<div class="bar-fill" id="bar-' + uid + '" style="width:0%"></div>' +
        '</div>';

      list.insertBefore(item, list.firstChild);
      showToast('"' + file.name + '" added to transfer queue');
      simulateProgress(uid, file.name);
    }

    function simulateProgress(uid, fileName) {
      var bar = document.getElementById('bar-' + uid);
      var pct = document.getElementById('pct-' + uid);
      var meta = document.getElementById('meta-' + uid);
      var track = bar ? bar.parentElement : null;
      var progress = 0;

      if (!bar || !pct || !meta) return;

      meta.textContent = 'Transferring…';

      var interval = setInterval(function () {
        var increment = Math.floor(Math.random() * 9) + 3;
        progress = Math.min(100, progress + increment);

        bar.style.width = progress + '%';
        pct.textContent = progress + '%';

        if (track) track.setAttribute('aria-valuenow', progress);

        if (progress >= 100) {
          clearInterval(interval);
          bar.classList.add('done');
          pct.classList.add('done');
          pct.textContent = 'Done';
          meta.textContent = 'Transfer complete';
          showToast('"' + fileName + '" sent successfully!');
        }
      }, 300);
    }

    function sendFile(peerName) {
      safeToast('Connecting to ' + peerName + '… Select a file to send.');
      fileInput.click();
    }

    function previewFile(fileName) {
      showToast('Streaming "' + fileName + '" from local network…');
    }

    function showToast(message) {
      var toast = document.getElementById('toast');
      toast.textContent = message;
      toast.classList.add('visible');
      clearTimeout(toastTimer);
      toastTimer = setTimeout(function () {
        toast.classList.remove('visible');
      }, 2600);
    }

    function escapeHTML(str) {
      var div = document.createElement('div');
      div.appendChild(document.createTextNode(str));
      return div.innerHTML;
    }

    window.addEventListener('load', function () {
      var demoBar = document.getElementById('bar-demo1');
      var demoPct = document.getElementById('pct-demo1');
      var demoMeta = document.getElementById('meta-demo1');
      var demoProgress = 40;

      if (!demoBar || !demoPct || !demoMeta) return;

      var demoInterval = setInterval(function () {
        demoProgress = Math.min(100, demoProgress + Math.floor(Math.random() * 6) + 2);
        demoBar.style.width = demoProgress + '%';
        demoPct.textContent = demoProgress + '%';

        if (demoProgress >= 100) {
          clearInterval(demoInterval);
          demoBar.classList.add('done');
          demoPct.classList.add('done');
          demoPct.textContent = 'Done';
          demoMeta.textContent = 'To Rohan\'s Laptop · Complete';
        }
      }, 400);
    });
  </script>
</body>
</html>
