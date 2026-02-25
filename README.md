<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>LaporPMR</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Nunito:wght@400;600;700;800&display=swap" rel="stylesheet">
<style>
  :root {
    --red: #D0021B; --red-dark: #A50016; --red-light: #FF1A35; --red-pale: #FFF0F2;
    --white: #FFFFFF; --gray: #F5F5F5; --gray-2: #E8E8E8; --gray-3: #D0D0D0;
    --text: #1A1A1A; --text-muted: #777;
    --shadow: 0 4px 24px rgba(208,2,27,0.13);
  }
  * { margin:0; padding:0; box-sizing:border-box; }
  body { font-family:'Nunito',sans-serif; background:#fafafa; min-height:100vh; color:var(--text); }

  /* VIEWS */
  .view { display:none; }
  .view.active { display:block; }

  /* ========== SISWA ========== */
  #view-siswa { min-height:100vh; position:relative; }
  #view-siswa::before { content:''; position:fixed; inset:0; background:radial-gradient(ellipse at 0% 0%,rgba(208,2,27,.07) 0%,transparent 60%),radial-gradient(ellipse at 100% 100%,rgba(208,2,27,.05) 0%,transparent 60%); pointer-events:none; z-index:0; }

  .app-wrapper { position:relative; z-index:1; min-height:100vh; display:flex; flex-direction:column; align-items:center; padding:20px 16px 40px; }

  header { width:100%; max-width:520px; display:flex; align-items:center; justify-content:space-between; padding:18px 0 8px; animation:fadeDown .5s ease; }
  .header-left { display:flex; align-items:center; gap:14px; }

  .logo-cross { width:48px; height:48px; position:relative; flex-shrink:0; }
  .logo-cross::before,.logo-cross::after { content:''; position:absolute; background:var(--red); border-radius:3px; }
  .logo-cross::before { width:16px; height:48px; left:50%; transform:translateX(-50%); }
  .logo-cross::after  { height:16px; width:48px; top:50%; transform:translateY(-50%); }

  .header-text h1 { font-family:'Bebas Neue',sans-serif; font-size:2rem; letter-spacing:2px; color:var(--red); line-height:1; }
  .header-text p  { font-size:.75rem; color:var(--text-muted); font-weight:600; letter-spacing:.5px; margin-top:2px; }

  .btn-admin-link { padding:7px 14px; background:transparent; border:2px solid var(--gray-2); border-radius:8px; font-family:'Nunito',sans-serif; font-size:.75rem; font-weight:800; color:var(--text-muted); cursor:pointer; transition:all .2s; white-space:nowrap; }
  .btn-admin-link:hover { border-color:var(--red); color:var(--red); }

  /* PROGRESS */
  .progress-track { width:100%; max-width:520px; margin:20px 0 8px; animation:fadeIn .5s ease .1s both; }
  .steps { display:flex; justify-content:space-between; align-items:center; position:relative; }
  .steps::before { content:''; position:absolute; height:2px; background:var(--gray-2); left:20px; right:20px; top:50%; transform:translateY(-50%); z-index:0; }
  .step-fill { position:absolute; height:2px; background:var(--red); left:20px; top:50%; transform:translateY(-50%); z-index:1; transition:width .5s ease; }
  .step-dot { width:36px; height:36px; border-radius:50%; background:var(--white); border:2px solid var(--gray-2); display:flex; align-items:center; justify-content:center; font-size:.75rem; font-weight:800; color:var(--text-muted); position:relative; z-index:2; transition:all .3s; flex-shrink:0; }
  .step-dot.active { border-color:var(--red); background:var(--red); color:white; box-shadow:0 0 0 4px rgba(208,2,27,.15); }
  .step-dot.done   { border-color:var(--red); background:var(--red-pale); color:var(--red); }
  .step-labels { display:flex; justify-content:space-between; margin-top:6px; }
  .step-labels span { font-size:.65rem; color:var(--text-muted); font-weight:700; width:60px; text-align:center; line-height:1.2; }
  .step-labels span.active-label { color:var(--red); }

  /* CARD */
  .card { width:100%; max-width:520px; background:white; border-radius:20px; padding:32px 28px; box-shadow:var(--shadow); margin-top:16px; animation:fadeUp .4s ease both; }
  .card-title { font-family:'Bebas Neue',sans-serif; font-size:1.6rem; letter-spacing:1.5px; color:var(--text); margin-bottom:4px; }
  .card-title span { color:var(--red); }
  .card-sub { font-size:.82rem; color:var(--text-muted); margin-bottom:24px; font-weight:600; }

  /* FORM */
  .form-group { margin-bottom:18px; }
  label { display:block; font-size:.78rem; font-weight:800; color:var(--text); letter-spacing:.5px; text-transform:uppercase; margin-bottom:6px; }
  input,select,textarea { width:100%; padding:12px 16px; border:2px solid var(--gray-2); border-radius:10px; font-family:'Nunito',sans-serif; font-size:.95rem; color:var(--text); background:var(--gray); outline:none; transition:all .2s; }
  input:focus,select:focus,textarea:focus { border-color:var(--red); background:white; box-shadow:0 0 0 3px rgba(208,2,27,.1); }
  textarea { resize:vertical; min-height:90px; }

  /* BUTTONS */
  .btn { width:100%; padding:14px; border:none; border-radius:12px; font-family:'Nunito',sans-serif; font-size:1rem; font-weight:800; cursor:pointer; transition:all .2s; letter-spacing:.5px; }
  .btn-primary { background:var(--red); color:white; box-shadow:0 4px 16px rgba(208,2,27,.3); margin-top:8px; }
  .btn-primary:hover { background:var(--red-dark); transform:translateY(-1px); box-shadow:0 6px 20px rgba(208,2,27,.4); }
  .btn-ghost { background:transparent; color:var(--text-muted); border:2px solid var(--gray-2); margin-top:10px; }
  .btn-ghost:hover { border-color:var(--red); color:var(--red); }

  /* MENU */
  .menu-grid { display:grid; grid-template-columns:1fr 1fr; gap:14px; margin-top:8px; }
  .menu-card { background:var(--gray); border:2px solid var(--gray-2); border-radius:16px; padding:24px 16px; text-align:center; cursor:pointer; transition:all .25s; display:flex; flex-direction:column; align-items:center; gap:12px; }
  .menu-card:hover { border-color:var(--red); background:var(--red-pale); transform:translateY(-3px); box-shadow:var(--shadow); }
  .menu-icon { width:60px; height:60px; border-radius:50%; background:var(--red-pale); border:2px solid rgba(208,2,27,.2); display:flex; align-items:center; justify-content:center; font-size:1.8rem; transition:all .25s; }
  .menu-card:hover .menu-icon { background:var(--red); border-color:var(--red); transform:scale(1.1); }
  .menu-card:hover .menu-icon span { filter:grayscale(1) brightness(10); }
  .menu-label { font-size:.85rem; font-weight:800; color:var(--text); line-height:1.3; }
  .menu-card:hover .menu-label { color:var(--red-dark); }

  /* CHECK */
  .check-group { display:flex; flex-direction:column; gap:8px; }
  .check-item { display:flex; align-items:center; gap:10px; padding:10px 14px; border:2px solid var(--gray-2); border-radius:10px; cursor:pointer; transition:all .2s; background:var(--gray); }
  .check-item:hover { border-color:var(--red); background:var(--red-pale); }
  .check-item input[type="checkbox"],.check-item input[type="radio"] { width:18px; height:18px; accent-color:var(--red); cursor:pointer; flex-shrink:0; }
  .check-item label { font-size:.88rem; font-weight:700; text-transform:none; letter-spacing:0; margin:0; cursor:pointer; color:var(--text); }

  /* KONFIRMASI */
  .confirm-card { background:var(--red-pale); border:2px solid rgba(208,2,27,.2); border-radius:14px; padding:20px; margin-bottom:20px; }
  .confirm-row { display:flex; justify-content:space-between; align-items:flex-start; padding:8px 0; border-bottom:1px solid rgba(208,2,27,.12); gap:12px; }
  .confirm-row:last-child { border-bottom:none; }
  .confirm-key { font-size:.75rem; font-weight:800; text-transform:uppercase; color:var(--red); letter-spacing:.5px; flex-shrink:0; }
  .confirm-val { font-size:.88rem; font-weight:700; color:var(--text); text-align:right; }

  /* SUKSES */
  .success-icon { width:80px; height:80px; background:var(--red); border-radius:50%; display:flex; align-items:center; justify-content:center; font-size:2.2rem; margin:0 auto 20px; animation:popIn .5s cubic-bezier(.34,1.56,.64,1) both; box-shadow:0 8px 24px rgba(208,2,27,.35); }
  .success-title { font-family:'Bebas Neue',sans-serif; font-size:2rem; color:var(--red); text-align:center; letter-spacing:2px; margin-bottom:6px; }
  .success-sub { text-align:center; color:var(--text-muted); font-size:.85rem; font-weight:600; margin-bottom:24px; }

  /* RIWAYAT */
  .riwayat-section { width:100%; max-width:520px; margin-top:20px; animation:fadeUp .4s ease .2s both; }
  .riwayat-title { font-family:'Bebas Neue',sans-serif; font-size:1.2rem; letter-spacing:1.5px; color:var(--text); margin-bottom:10px; display:flex; align-items:center; gap:8px; }
  .riwayat-title::after { content:''; flex:1; height:2px; background:var(--gray-2); }
  .riwayat-item { background:white; border-radius:14px; padding:14px 18px; margin-bottom:10px; box-shadow:0 2px 12px rgba(0,0,0,.06); border-left:4px solid var(--red); }
  .riwayat-item-top { display:flex; justify-content:space-between; align-items:center; margin-bottom:6px; }
  .riwayat-name { font-weight:800; font-size:.9rem; }
  .riwayat-time { font-size:.72rem; color:var(--text-muted); font-weight:600; }
  .riwayat-badge { display:inline-block; padding:3px 10px; border-radius:20px; font-size:.72rem; font-weight:800; background:var(--red-pale); color:var(--red); margin-bottom:4px; }
  .riwayat-detail { font-size:.78rem; color:var(--text-muted); font-weight:600; }
  .kelas-badge { display:inline-block; font-size:.72rem; font-weight:800; color:var(--text-muted); background:var(--gray); padding:2px 8px; border-radius:20px; margin-left:6px; }

  /* USER BANNER */
  .user-banner { background:linear-gradient(135deg,var(--red),var(--red-light)); border-radius:12px; padding:12px 18px; margin-bottom:20px; display:flex; align-items:center; gap:10px; color:white; }
  .user-banner-icon { font-size:1.4rem; }
  .user-banner-name { font-weight:800; font-size:.95rem; }
  .user-banner-kelas { font-size:.78rem; opacity:.85; }

  /* ERROR */
  .error-msg { color:var(--red); font-size:.78rem; font-weight:700; margin-top:4px; display:none; }
  .error-msg.show { display:block; }
  input.error,select.error,textarea.error { border-color:var(--red); }

  /* PAGE */
  .page { display:none; }
  .page.active { display:block; }

  /* NOTIF BANNER */
  .notif-banner { position:fixed; top:-120px; left:0; right:0; z-index:9999; display:flex; justify-content:center; padding:0 16px; transition:top .5s cubic-bezier(.34,1.56,.64,1); }
  .notif-banner.show { top:16px; }
  .notif-inner { background:white; border-radius:16px; padding:16px 20px; box-shadow:0 8px 32px rgba(208,2,27,.25),0 2px 8px rgba(0,0,0,.1); display:flex; align-items:center; gap:14px; width:100%; max-width:520px; border-left:5px solid var(--red); position:relative; overflow:hidden; }
  .notif-icon { width:44px; height:44px; background:var(--red); border-radius:12px; display:flex; align-items:center; justify-content:center; font-size:1.3rem; flex-shrink:0; }
  .notif-body { flex:1; min-width:0; }
  .notif-title { font-weight:800; font-size:.88rem; color:var(--text); margin-bottom:3px; }
  .notif-title span { color:var(--red); }
  .notif-meta { font-size:.74rem; color:var(--text-muted); font-weight:600; display:flex; flex-wrap:wrap; gap:8px; }
  .notif-close { background:none; border:none; cursor:pointer; color:var(--text-muted); font-size:1.1rem; padding:4px 6px; border-radius:6px; flex-shrink:0; transition:all .2s; line-height:1; }
  .notif-close:hover { background:var(--gray); }
  .notif-progress { position:absolute; bottom:0; left:0; height:3px; background:var(--red); width:100%; animation:shrink 4s linear forwards; }

  /* ========== ADMIN ========== */
  #view-admin { min-height:100vh; background:#f0f0f0; }
  .admin-layout { display:flex; min-height:100vh; }

  .sidebar { width:240px; background:var(--red-dark); display:flex; flex-direction:column; position:fixed; top:0; left:0; bottom:0; z-index:100; }
  .sidebar-brand { padding:28px 24px 20px; border-bottom:1px solid rgba(255,255,255,.1); display:flex; align-items:center; gap:12px; }
  .sidebar-cross { width:36px; height:36px; position:relative; flex-shrink:0; }
  .sidebar-cross::before,.sidebar-cross::after { content:''; position:absolute; background:white; border-radius:2px; }
  .sidebar-cross::before { width:12px; height:36px; left:50%; transform:translateX(-50%); }
  .sidebar-cross::after  { height:12px; width:36px; top:50%; transform:translateY(-50%); }
  .sidebar-brand-text h2 { font-family:'Bebas Neue',sans-serif; font-size:1.4rem; letter-spacing:2px; color:white; line-height:1; }
  .sidebar-brand-text p  { font-size:.65rem; color:rgba(255,255,255,.6); font-weight:700; letter-spacing:.5px; margin-top:2px; }
  .sidebar-menu { padding:16px 12px; flex:1; }
  .sidebar-label { font-size:.62rem; font-weight:800; color:rgba(255,255,255,.4); letter-spacing:1.5px; text-transform:uppercase; padding:0 12px; margin:16px 0 8px; }
  .sidebar-item { display:flex; align-items:center; gap:10px; padding:10px 14px; border-radius:10px; cursor:pointer; color:rgba(255,255,255,.7); font-size:.88rem; font-weight:700; transition:all .2s; margin-bottom:2px; }
  .sidebar-item:hover,.sidebar-item.active { background:rgba(255,255,255,.15); color:white; }
  .sidebar-item .icon { font-size:1rem; width:20px; text-align:center; }
  .sidebar-footer { padding:16px 12px; border-top:1px solid rgba(255,255,255,.1); }
  .sidebar-back { display:flex; align-items:center; gap:10px; padding:10px 14px; border-radius:10px; color:rgba(255,255,255,.6); font-size:.82rem; font-weight:700; cursor:pointer; transition:all .2s; background:none; border:none; font-family:'Nunito',sans-serif; width:100%; }
  .sidebar-back:hover { background:rgba(255,255,255,.1); color:white; }

  .admin-main { margin-left:240px; flex:1; display:flex; flex-direction:column; }

  .topbar { background:white; padding:16px 28px; display:flex; align-items:center; justify-content:space-between; box-shadow:0 1px 0 var(--gray-2); position:sticky; top:0; z-index:50; }
  .topbar-title { font-family:'Bebas Neue',sans-serif; font-size:1.4rem; letter-spacing:1.5px; }
  .topbar-title span { color:var(--red); }
  .topbar-right { display:flex; align-items:center; gap:12px; }
  .topbar-date { font-size:.78rem; color:var(--text-muted); font-weight:700; }
  .btn-refresh { display:flex; align-items:center; gap:6px; padding:8px 16px; background:var(--red); color:white; border:none; border-radius:8px; font-family:'Nunito',sans-serif; font-size:.82rem; font-weight:800; cursor:pointer; transition:all .2s; }
  .btn-refresh:hover { background:var(--red-dark); transform:translateY(-1px); }

  .admin-content { padding:28px; }

  .stat-grid { display:grid; grid-template-columns:repeat(4,1fr); gap:16px; margin-bottom:24px; }
  .stat-card { background:white; border-radius:16px; padding:20px; box-shadow:0 4px 24px rgba(0,0,0,.06); display:flex; align-items:center; gap:14px; animation:fadeUp .4s ease both; }
  .stat-card:nth-child(2){animation-delay:.05s} .stat-card:nth-child(3){animation-delay:.1s} .stat-card:nth-child(4){animation-delay:.15s}
  .stat-icon { width:48px; height:48px; border-radius:12px; display:flex; align-items:center; justify-content:center; font-size:1.4rem; flex-shrink:0; }
  .stat-icon.red{background:var(--red-pale)} .stat-icon.blue{background:#EEF4FF} .stat-icon.green{background:#EDFFF4} .stat-icon.orange{background:#FFF7ED}
  .stat-num { font-family:'Bebas Neue',sans-serif; font-size:1.8rem; line-height:1; color:var(--text); letter-spacing:1px; }
  .stat-label { font-size:.72rem; font-weight:800; color:var(--text-muted); text-transform:uppercase; letter-spacing:.5px; margin-top:2px; }

  .filter-bar { background:white; border-radius:16px; padding:16px 20px; box-shadow:0 4px 24px rgba(0,0,0,.06); margin-bottom:20px; display:flex; align-items:center; gap:12px; flex-wrap:wrap; animation:fadeUp .4s ease .2s both; }
  .filter-bar label { font-size:.72rem; font-weight:800; text-transform:uppercase; letter-spacing:.5px; color:var(--text-muted); white-space:nowrap; }
  .filter-bar input[type="date"],.filter-bar select { padding:8px 12px; border:2px solid var(--gray-2); border-radius:8px; font-family:'Nunito',sans-serif; font-size:.85rem; color:var(--text); background:var(--gray); outline:none; cursor:pointer; transition:all .2s; font-weight:700; }
  .filter-bar input[type="date"]:focus,.filter-bar select:focus { border-color:var(--red); background:white; }
  .filter-sep { width:1px; height:28px; background:var(--gray-2); }
  .btn-reset-filter { padding:8px 14px; border:2px solid var(--gray-2); background:transparent; border-radius:8px; font-family:'Nunito',sans-serif; font-size:.8rem; font-weight:800; color:var(--text-muted); cursor:pointer; transition:all .2s; white-space:nowrap; }
  .btn-reset-filter:hover { border-color:var(--red); color:var(--red); }
  .filter-count { margin-left:auto; font-size:.78rem; font-weight:800; color:var(--text-muted); white-space:nowrap; }
  .filter-count span { color:var(--red); }

  .table-wrap { background:white; border-radius:16px; box-shadow:0 4px 24px rgba(0,0,0,.06); overflow:hidden; animation:fadeUp .4s ease .25s both; }
  .table-header { padding:16px 20px; border-bottom:1px solid var(--gray-2); display:flex; align-items:center; justify-content:space-between; }
  .table-header h3 { font-family:'Bebas Neue',sans-serif; font-size:1.1rem; letter-spacing:1px; }
  .btn-hapus-semua { padding:7px 14px; background:transparent; border:2px solid #ffcdd2; color:var(--red); border-radius:8px; font-family:'Nunito',sans-serif; font-size:.78rem; font-weight:800; cursor:pointer; transition:all .2s; }
  .btn-hapus-semua:hover { background:var(--red); color:white; border-color:var(--red); }

  table { width:100%; border-collapse:collapse; }
  thead tr { background:var(--gray); border-bottom:2px solid var(--gray-2); }
  thead th { padding:12px 16px; text-align:left; font-size:.7rem; font-weight:800; text-transform:uppercase; letter-spacing:.8px; color:var(--text-muted); white-space:nowrap; }
  tbody tr { border-bottom:1px solid var(--gray-2); transition:background .15s; }
  tbody tr:last-child { border-bottom:none; }
  tbody tr:hover { background:var(--gray); }
  tbody td { padding:14px 16px; font-size:.85rem; font-weight:600; color:var(--text); vertical-align:middle; }
  .td-no { font-weight:800; color:var(--text-muted); font-size:.78rem; width:40px; }
  .td-nama { font-weight:800; }
  .td-detail { font-size:.8rem; color:var(--text-muted); max-width:220px; white-space:nowrap; overflow:hidden; text-overflow:ellipsis; }
  .td-waktu { font-size:.75rem; color:var(--text-muted); white-space:nowrap; }
  .layanan-badge { display:inline-flex; align-items:center; gap:4px; padding:4px 10px; border-radius:20px; font-size:.75rem; font-weight:800; white-space:nowrap; }
  .layanan-badge.uks  { background:#EEF4FF; color:#2563EB; }
  .layanan-badge.obat { background:#EDFFF4; color:#16A34A; }
  .btn-hapus-row { padding:5px 12px; background:transparent; border:2px solid var(--gray-2); color:var(--text-muted); border-radius:7px; font-family:'Nunito',sans-serif; font-size:.75rem; font-weight:800; cursor:pointer; transition:all .2s; white-space:nowrap; }
  .btn-hapus-row:hover { border-color:var(--red); color:var(--red); background:var(--red-pale); }

  .empty-state { text-align:center; padding:56px 24px; color:var(--text-muted); }
  .empty-icon { font-size:3rem; margin-bottom:12px; }
  .empty-title { font-family:'Bebas Neue',sans-serif; font-size:1.3rem; letter-spacing:1px; color:var(--gray-3); margin-bottom:6px; }
  .empty-sub { font-size:.82rem; font-weight:600; }

  /* MODAL */
  .modal-overlay { position:fixed; inset:0; background:rgba(0,0,0,.4); z-index:99999; display:none; align-items:center; justify-content:center; padding:16px; backdrop-filter:blur(4px); }
  .modal-overlay.show { display:flex; }
  .modal-box { background:white; border-radius:20px; padding:32px 28px; max-width:360px; width:100%; box-shadow:0 20px 60px rgba(0,0,0,.2); animation:popIn .3s cubic-bezier(.34,1.56,.64,1); }
  .modal-icon { width:56px; height:56px; background:var(--red-pale); border-radius:50%; display:flex; align-items:center; justify-content:center; font-size:1.6rem; margin:0 auto 16px; }
  .modal-title { font-family:'Bebas Neue',sans-serif; font-size:1.4rem; letter-spacing:1px; text-align:center; margin-bottom:6px; }
  .modal-sub { text-align:center; font-size:.82rem; color:var(--text-muted); font-weight:600; margin-bottom:24px; }
  .modal-actions { display:flex; gap:10px; }
  .btn-cancel { flex:1; padding:12px; border:2px solid var(--gray-2); background:transparent; border-radius:10px; font-family:'Nunito',sans-serif; font-size:.9rem; font-weight:800; color:var(--text-muted); cursor:pointer; transition:all .2s; }
  .btn-cancel:hover { border-color:var(--gray-3); color:var(--text); }
  .btn-hapus-confirm { flex:1; padding:12px; border:none; background:var(--red); border-radius:10px; font-family:'Nunito',sans-serif; font-size:.9rem; font-weight:800; color:white; cursor:pointer; transition:all .2s; }
  .btn-hapus-confirm:hover { background:var(--red-dark); }

  @keyframes spin     { to{transform:rotate(360deg)} }
  @keyframes shake    { 0%,100%{transform:translateX(0)} 20%{transform:translateX(-8px)} 40%{transform:translateX(8px)} 60%{transform:translateX(-6px)} 80%{transform:translateX(6px)} }
  @keyframes fadeDown { from{opacity:0;transform:translateY(-16px)} to{opacity:1;transform:translateY(0)} }
  @keyframes fadeUp   { from{opacity:0;transform:translateY(20px)}  to{opacity:1;transform:translateY(0)} }
  @keyframes fadeIn   { from{opacity:0} to{opacity:1} }
  @keyframes popIn    { from{opacity:0;transform:scale(.4)} to{opacity:1;transform:scale(1)} }
  @keyframes shrink   { from{width:100%} to{width:0%} }

  @media(max-width:1100px){.stat-grid{grid-template-columns:repeat(2,1fr)}}
  @media(max-width:400px){.menu-grid{grid-template-columns:1fr}.card{padding:24px 18px}}
</style>
</head>
<body>

<!-- LOADING OVERLAY -->
<div id="loadingOverlay" style="display:none;position:fixed;inset:0;background:rgba(255,255,255,0.75);z-index:99999;align-items:center;justify-content:center;flex-direction:column;gap:14px;backdrop-filter:blur(3px);">
  <div style="width:48px;height:48px;border:4px solid var(--gray-2);border-top-color:var(--red);border-radius:50%;animation:spin 0.8s linear infinite;"></div>
  <div style="font-size:0.85rem;font-weight:800;color:var(--text-muted);">Menghubungkan ke server...</div>
</div>

<!-- NOTIF BANNER -->
<div class="notif-banner" id="notifBanner">
  <div class="notif-inner">
    <div class="notif-icon">✓</div>
    <div class="notif-body">
      <div class="notif-title">Laporan <span id="notif-layanan">-</span> Terkirim!</div>
      <div class="notif-meta">
        <div>👤 <span id="notif-nama">-</span></div>
        <div>🏫 <span id="notif-kelas">-</span></div>
        <div>🕐 <span id="notif-waktu">-</span></div>
      </div>
    </div>
    <button class="notif-close" onclick="tutupNotif()">✕</button>
    <div class="notif-progress" id="notifProgress"></div>
  </div>
</div>

<!-- MODAL HAPUS -->
<div class="modal-overlay" id="modalOverlay">
  <div class="modal-box">
    <div class="modal-icon">🗑️</div>
    <div class="modal-title" id="modalTitle">Hapus Laporan?</div>
    <div class="modal-sub" id="modalSub">Laporan ini akan dihapus permanen.</div>
    <div class="modal-actions">
      <button class="btn-cancel" onclick="tutupModal()">Batal</button>
      <button class="btn-hapus-confirm" id="modalConfirmBtn">Hapus</button>
    </div>
  </div>
</div>

<!-- ===== VIEW SISWA ===== -->
<div id="view-siswa" class="view active">
  <div class="app-wrapper">
    <header>
      <div class="header-left">
        <div class="logo-cross"></div>
        <div class="header-text"><h1>LaporPMR</h1><p>SISTEM LAPORAN KESEHATAN SISWA</p></div>
      </div>
      <button class="btn-admin-link" onclick="bukaAdmin()">⚙️ Admin</button>
    </header>

    <div class="progress-track" id="progressTrack">
      <div class="steps">
        <div class="step-fill" id="stepFill" style="width:0%"></div>
        <div class="step-dot active" id="dot1">1</div>
        <div class="step-dot" id="dot2">2</div>
        <div class="step-dot" id="dot3">3</div>
        <div class="step-dot" id="dot4">4</div>
      </div>
      <div class="step-labels">
        <span class="active-label" id="lbl1">Data Siswa</span>
        <span id="lbl2">Pilih Layanan</span>
        <span id="lbl3">Detail</span>
        <span id="lbl4">Konfirmasi</span>
      </div>
    </div>

    <!-- PAGE 1 -->
    <div class="card page active" id="page1">
      <div class="card-title">Data <span>Siswa</span></div>
      <div class="card-sub">Isi nama dan kelas kamu terlebih dahulu</div>
      <div class="form-group">
        <label>Nama Lengkap</label>
        <input type="text" id="nama" placeholder="Contoh: Budi Santoso" autocomplete="off">
        <div class="error-msg" id="err-nama">Nama tidak boleh kosong</div>
      </div>
      <div class="form-group">
        <label>Kelas</label>
        <select id="kelas">
          <option value="">-- Pilih Kelas --</option>
          <optgroup label="Kelas X"><option>X-1</option><option>X-2</option><option>X-3</option><option>X-4</option><option>X-5</option><option>X-6</option></optgroup>
          <optgroup label="Kelas XI"><option>XI-1</option><option>XI-2</option><option>XI-3</option><option>XI-4</option><option>XI-5</option><option>XI-6</option></optgroup>
          <optgroup label="Kelas XII"><option>XII-1</option><option>XII-2</option><option>XII-3</option><option>XII-4</option><option>XII-5</option><option>XII-6</option></optgroup>
        </select>
        <div class="error-msg" id="err-kelas">Kelas harus dipilih</div>
      </div>
      <button class="btn btn-primary" onclick="goToPage2()">Lanjut →</button>
    </div>

    <!-- PAGE 2 -->
    <div class="card page" id="page2">
      <div class="card-title">Pilih <span>Layanan</span></div>
      <div class="card-sub">Kamu butuh layanan apa hari ini?</div>
      <div class="user-banner">
        <div class="user-banner-icon">👤</div>
        <div><div class="user-banner-name" id="banner-name">-</div><div class="user-banner-kelas" id="banner-kelas">-</div></div>
      </div>
      <div class="menu-grid">
        <div class="menu-card" onclick="pilihLayanan('uks')"><div class="menu-icon"><span>🏥</span></div><div class="menu-label">Menggunakan Ruang UKS</div></div>
        <div class="menu-card" onclick="pilihLayanan('obat')"><div class="menu-icon"><span>💊</span></div><div class="menu-label">Pengambilan Obat</div></div>
      </div>
      <button class="btn btn-ghost" onclick="goTo(1)">← Kembali</button>
    </div>

    <!-- PAGE 3A UKS -->
    <div class="card page" id="page3uks">
      <div class="card-title">Detail <span>Ruang UKS</span></div>
      <div class="card-sub">Ceritakan kondisimu saat ini</div>
      <div class="form-group">
        <label>Keluhan Utama</label>
        <select id="keluhan">
          <option value="">-- Pilih Keluhan --</option>
          <option>Pusing / Sakit Kepala</option><option>Mual / Muntah</option><option>Demam</option>
          <option>Sakit Perut</option><option>Luka / Cedera</option><option>Pingsan / Lemas</option>
          <option>Sesak Napas</option><option>Lainnya</option>
        </select>
        <div class="error-msg" id="err-keluhan">Keluhan harus dipilih</div>
      </div>
      <div class="form-group">
        <label>Keterangan Tambahan (Opsional)</label>
        <textarea id="ket-uks" placeholder="Ceritakan lebih lanjut kondisimu..."></textarea>
      </div>
      <div class="form-group">
        <label>Sudah minum obat sebelumnya?</label>
        <div class="check-group">
          <div class="check-item"><input type="radio" name="minum-obat" id="mo-ya" value="Ya" onchange="toggleObatKonsumsi()"><label for="mo-ya">Ya, sudah minum obat</label></div>
          <div class="check-item"><input type="radio" name="minum-obat" id="mo-tidak" value="Tidak" checked onchange="toggleObatKonsumsi()"><label for="mo-tidak">Belum minum obat</label></div>
        </div>
      </div>
      <div class="form-group" id="obat-konsumsi-group" style="display:none;">
        <label>Obat yang sudah dikonsumsi</label>
        <input type="text" id="obat-konsumsi" placeholder="Contoh: Paracetamol, Antasida...">
        <div class="error-msg" id="err-obat-konsumsi">Mohon isi obat yang sudah dikonsumsi</div>
      </div>
      <button class="btn btn-primary" onclick="goToKonfirmasi()">Lanjut →</button>
      <button class="btn btn-ghost" onclick="goTo(2)">← Kembali</button>
    </div>

    <!-- PAGE 3B OBAT -->
    <div class="card page" id="page3obat">
      <div class="card-title">Detail <span>Pengambilan Obat</span></div>
      <div class="card-sub">Pilih obat yang dibutuhkan</div>
      <div class="form-group">
        <label>Jenis Obat yang Dibutuhkan</label>
        <div class="check-group" id="obat-list">
          <div class="check-item"><input type="checkbox" id="ob1" value="Tolak Angin"><label for="ob1">Tolak Angin</label></div>
          <div class="check-item"><input type="checkbox" id="ob2" value="Betadine"><label for="ob2">Betadine</label></div>
          <div class="check-item"><input type="checkbox" id="ob3" value="Tolak Angin Cair"><label for="ob3">Tolak Angin Cair</label></div>
          <div class="check-item"><input type="checkbox" id="ob4" value="Plester / Perban"><label for="ob4">Plester / Perban</label></div>
          <div class="check-item"><input type="checkbox" id="ob5" value="Alkohol"><label for="ob5">Alkohol</label></div>
        </div>
        <div class="error-msg" id="err-obat">Pilih minimal satu obat</div>
      </div>
      <div class="form-group">
        <label>Keterangan Keluhan</label>
        <textarea id="ket-obat" placeholder="Tuliskan keluhanmu untuk obat ini..."></textarea>
        <div class="error-msg" id="err-ket-obat">Keterangan tidak boleh kosong</div>
      </div>
      <button class="btn btn-primary" onclick="goToKonfirmasi()">Lanjut →</button>
      <button class="btn btn-ghost" onclick="goTo(2)">← Kembali</button>
    </div>

    <!-- PAGE 4 KONFIRMASI -->
    <div class="card page" id="page4">
      <div class="card-title">Konfirmasi <span>Laporan</span></div>
      <div class="card-sub">Periksa kembali data laporanmu</div>
      <div class="confirm-card" id="confirm-content"></div>
      <button class="btn btn-primary" onclick="submitLaporan()">✓ Kirim Laporan</button>
      <button class="btn btn-ghost" onclick="backFromKonfirmasi()">← Kembali</button>
    </div>

    <!-- PAGE 5 SUKSES -->
    <div class="card page" id="page5">
      <div class="success-icon">✓</div>
      <div class="success-title">Laporan Terkirim!</div>
      <div class="success-sub">Petugas PMR akan segera menanganimu. Tetap tenang ya!</div>
      <button class="btn btn-primary" onclick="buatLaporanBaru()">+ Buat Laporan Baru</button>
    </div>

    <!-- RIWAYAT -->
    <div class="riwayat-section" id="riwayatSection" style="display:none;">
      <div class="riwayat-title">📋 Riwayat Laporan</div>
      <div id="riwayat-list"></div>
    </div>
  </div>
</div>

<!-- ===== VIEW LOGIN ADMIN ===== -->
<div id="view-login" class="view">
  <div class="app-wrapper">
    <header>
      <div class="header-left">
        <div class="logo-cross"></div>
        <div class="header-text"><h1>LaporPMR</h1><p>SISTEM LAPORAN KESEHATAN SISWA</p></div>
      </div>
    </header>
    <div class="card" style="margin-top:40px;max-width:400px;">
      <div style="text-align:center;margin-bottom:24px;">
        <div style="width:64px;height:64px;background:var(--red-pale);border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:1.8rem;margin:0 auto 14px;">🔒</div>
        <div class="card-title" style="text-align:center;">Akses <span>Admin</span></div>
        <div class="card-sub" style="margin-bottom:0;">Masukkan password untuk melanjutkan</div>
      </div>
      <div class="form-group">
        <label>Password</label>
        <div style="position:relative;">
          <input type="password" id="inputPassword" placeholder="Masukkan password..." onkeydown="if(event.key==='Enter')cekPassword()">
          <button onclick="togglePassword()" id="btnToggle" style="position:absolute;right:12px;top:50%;transform:translateY(-50%);background:none;border:none;cursor:pointer;font-size:1.1rem;color:var(--text-muted);">👁️</button>
        </div>
        <div id="err-password-wrap" style="display:none;">
          <div style="color:var(--red);font-size:.78rem;font-weight:700;margin-top:6px;padding:8px 12px;background:var(--red-pale);border-radius:8px;border-left:3px solid var(--red);">⚠️ Password salah. Coba lagi.</div>
        </div>
      </div>
      <button class="btn btn-primary" onclick="cekPassword()">🔓 Masuk ke Panel Admin</button>
      <button class="btn btn-ghost" onclick="switchView('view-siswa')">← Kembali</button>
    </div>
  </div>
</div>

<!-- ===== VIEW ADMIN ===== -->
<div id="view-admin" class="view">
  <div class="admin-layout">
    <aside class="sidebar">
      <div class="sidebar-brand">
        <div class="sidebar-cross"></div>
        <div class="sidebar-brand-text"><h2>LaporPMR</h2><p>PANEL ADMIN</p></div>
      </div>
      <nav class="sidebar-menu">
        <div class="sidebar-label">Menu</div>
        <div class="sidebar-item active"><span class="icon">📋</span> Rekap Laporan</div>
      </nav>
      <div class="sidebar-footer">
        <button class="sidebar-back" onclick="kembaliKeSiswa()">← Kembali ke Aplikasi</button>
      </div>
    </aside>

    <main class="admin-main">
      <div class="topbar">
        <div class="topbar-title">Rekap <span>Laporan</span></div>
        <div class="topbar-right">
          <div class="topbar-date" id="topbarDate"></div>
          <button class="btn-refresh" onclick="adminLoadData()">↻ Refresh</button>
        </div>
      </div>
      <div class="admin-content">
        <div class="stat-grid">
          <div class="stat-card"><div class="stat-icon red">📋</div><div><div class="stat-num" id="stat-total">0</div><div class="stat-label">Total Laporan</div></div></div>
          <div class="stat-card"><div class="stat-icon blue">🏥</div><div><div class="stat-num" id="stat-uks">0</div><div class="stat-label">Ruang UKS</div></div></div>
          <div class="stat-card"><div class="stat-icon green">💊</div><div><div class="stat-num" id="stat-obat">0</div><div class="stat-label">Pengambilan Obat</div></div></div>
          <div class="stat-card"><div class="stat-icon orange">📅</div><div><div class="stat-num" id="stat-hari">0</div><div class="stat-label">Laporan Hari Ini</div></div></div>
        </div>
        <div class="filter-bar">
          <label>Tanggal</label>
          <input type="date" id="filterTanggal" onchange="applyFilter()">
          <div class="filter-sep"></div>
          <label>Layanan</label>
          <select id="filterLayanan" onchange="applyFilter()">
            <option value="">Semua Layanan</option>
            <option value="uks">🏥 Ruang UKS</option>
            <option value="obat">💊 Pengambilan Obat</option>
          </select>
          <button class="btn-reset-filter" onclick="resetFilter()">✕ Reset Filter</button>
          <div class="filter-count">Menampilkan <span id="filterCount">0</span> laporan</div>
        </div>
        <div class="table-wrap">
          <div class="table-header">
            <h3>📄 Daftar Laporan Masuk</h3>
            <button class="btn-hapus-semua" onclick="konfirmasiHapusSemua()">🗑️ Hapus Semua</button>
          </div>
          <div id="tableContent"></div>
        </div>
      </div>
    </main>
  </div>
</div>

<script>
  // ===== SUPABASE CONFIG =====
  const SUPA_URL = 'https://eeeukqxbhlavlsoawlzs.supabase.co';
  const SUPA_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImVlZXVrcXhiaGxhdmxzb2F3bHpzIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzE5NjU3ODYsImV4cCI6MjA4NzU0MTc4Nn0.IvZI0dTBUVdEU6a6JnNN2nfw-XqJhTB1UxWef2DvBHw';

  async function sbFetch(path, options={}) {
    const url = SUPA_URL + '/rest/v1/' + path;
    const headers = {
      'Content-Type': 'application/json',
      'apikey': SUPA_KEY,
      'Authorization': 'Bearer ' + SUPA_KEY,
    };
    if (options.prefer) headers['Prefer'] = options.prefer;

    const res = await fetch(url, {
      method: options.method || 'GET',
      headers,
      body: options.body || undefined,
    });

    if (!res.ok) {
      const err = await res.text();
      throw new Error('Supabase error ' + res.status + ': ' + err);
    }
    const text = await res.text();
    return text ? JSON.parse(text) : null;
  }

  // ===== DATA =====
  let laporanData = [];
  let state = { nama:'', kelas:'', layanan:'' };
  let riwayat = [];

  // Muat semua data dari Supabase
  async function muatData() {
    tampilLoading(true);
    try {
      const data = await sbFetch('laporan?select=*&order=timestamp.desc');
      laporanData = data || [];
      riwayat = [...laporanData];
      renderRiwayat();
    } catch(e) {
      console.error('Gagal memuat data:', e);
    }
    tampilLoading(false);
  }

  // Simpan satu laporan baru ke Supabase
  async function simpanLaporan(entry) {
    await sbFetch('laporan', {
      method: 'POST',
      prefer: 'return=minimal',
      body: JSON.stringify(entry)
    });
  }

  async function hapusDariDB(id) {
    await sbFetch('laporan?id=eq.' + id, { method: 'DELETE' });
  }

  async function hapusSemuaDariDB() {
    await sbFetch('laporan?timestamp=gte.0', { method: 'DELETE' });
  }

  // Loading overlay helper
  function tampilLoading(show) {
    document.getElementById('loadingOverlay').style.display = show ? 'flex' : 'none';
  }

  // ===== NAVIGASI =====
  function switchView(id) {
    document.querySelectorAll('.view').forEach(v => v.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    window.scrollTo({ top:0, behavior:'smooth' });
  }

  function toggleObatKonsumsi() {
    const yaChecked = document.getElementById('mo-ya').checked;
    const group = document.getElementById('obat-konsumsi-group');
    group.style.display = yaChecked ? 'block' : 'none';
    if (!yaChecked) {
      document.getElementById('obat-konsumsi').value = '';
      document.getElementById('err-obat-konsumsi').classList.remove('show');
    }
  }

  function bukaAdmin() {
    document.getElementById('inputPassword').value = '';
    document.getElementById('err-password-wrap').style.display = 'none';
    switchView('view-login');
  }

  function cekPassword() {
    const input = document.getElementById('inputPassword').value;
    const errWrap = document.getElementById('err-password-wrap');
    if (input === '87654321') {
      errWrap.style.display = 'none';
      document.getElementById('topbarDate').textContent = new Date().toLocaleDateString('id-ID',{weekday:'long',day:'numeric',month:'long',year:'numeric'});
      adminLoadData();
      switchView('view-admin');
      document.getElementById('inputPassword').value = '';
    } else {
      errWrap.style.display = 'block';
      document.getElementById('inputPassword').focus();
      const inp = document.getElementById('inputPassword');
      inp.style.animation = 'none'; inp.offsetHeight;
      inp.style.animation = 'shake .4s ease';
    }
  }

  function togglePassword() {
    const inp = document.getElementById('inputPassword');
    const btn = document.getElementById('btnToggle');
    if (inp.type === 'password') { inp.type = 'text'; btn.textContent = '🙈'; }
    else { inp.type = 'password'; btn.textContent = '👁️'; }
  }

  function kembaliKeSiswa() { switchView('view-siswa'); }

  // ===== PROGRESS =====
  function updateProgress(step) {
    const fills=[0,0,33,66,100];
    document.getElementById('stepFill').style.width=fills[step]+'%';
    for(let i=1;i<=4;i++){
      const dot=document.getElementById('dot'+i), lbl=document.getElementById('lbl'+i);
      dot.className='step-dot'; lbl.className='';
      if(i<step){dot.classList.add('done');dot.innerHTML='✓';}
      else if(i===step){dot.classList.add('active');dot.innerHTML=i;lbl.className='active-label';}
      else{dot.innerHTML=i;}
    }
  }

  function showPage(id) {
    document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    window.scrollTo({top:0,behavior:'smooth'});
  }

  function goTo(n) {
    if(n===1){showPage('page1');updateProgress(1);}
    else if(n===2){showPage('page2');updateProgress(2);}
  }

  // ===== FORM SISWA =====
  function goToPage2() {
    const nama=document.getElementById('nama').value.trim();
    const kelas=document.getElementById('kelas').value;
    let ok=true;
    ['err-nama','err-kelas'].forEach(id=>document.getElementById(id).classList.remove('show'));
    ['nama','kelas'].forEach(id=>document.getElementById(id).classList.remove('error'));
    if(!nama){document.getElementById('err-nama').classList.add('show');document.getElementById('nama').classList.add('error');ok=false;}
    if(!kelas){document.getElementById('err-kelas').classList.add('show');document.getElementById('kelas').classList.add('error');ok=false;}
    if(!ok)return;
    state.nama=nama; state.kelas=kelas;
    document.getElementById('banner-name').textContent=nama;
    document.getElementById('banner-kelas').textContent='Kelas '+kelas;
    showPage('page2'); updateProgress(2);
  }

  function pilihLayanan(l) {
    state.layanan=l;
    showPage(l==='uks'?'page3uks':'page3obat');
    updateProgress(3);
  }

  function goToKonfirmasi() {
    if(state.layanan==='uks'){
      const keluhan=document.getElementById('keluhan').value;
      if(!keluhan){document.getElementById('err-keluhan').classList.add('show');document.getElementById('keluhan').classList.add('error');return;}
      document.getElementById('err-keluhan').classList.remove('show');document.getElementById('keluhan').classList.remove('error');
      const ket=document.getElementById('ket-uks').value.trim();
      const minum=document.querySelector('input[name="minum-obat"]:checked')?.value||'Tidak';
      const obatKonsumsi=document.getElementById('obat-konsumsi').value.trim();
      if(minum==='Ya' && !obatKonsumsi){
        document.getElementById('err-obat-konsumsi').classList.add('show');
        document.getElementById('obat-konsumsi').classList.add('error');
        return;
      }
      document.getElementById('err-obat-konsumsi').classList.remove('show');
      document.getElementById('obat-konsumsi').classList.remove('error');
      document.getElementById('confirm-content').innerHTML=`
        <div class="confirm-row"><span class="confirm-key">Nama</span><span class="confirm-val">${state.nama}</span></div>
        <div class="confirm-row"><span class="confirm-key">Kelas</span><span class="confirm-val">${state.kelas}</span></div>
        <div class="confirm-row"><span class="confirm-key">Layanan</span><span class="confirm-val">🏥 Ruang UKS</span></div>
        <div class="confirm-row"><span class="confirm-key">Keluhan</span><span class="confirm-val">${keluhan}</span></div>
        <div class="confirm-row"><span class="confirm-key">Sudah Minum Obat?</span><span class="confirm-val">${minum}</span></div>
        ${minum==='Ya'?`<div class="confirm-row"><span class="confirm-key">Obat Dikonsumsi</span><span class="confirm-val">${obatKonsumsi}</span></div>`:''}
        ${ket?`<div class="confirm-row"><span class="confirm-key">Keterangan</span><span class="confirm-val">${ket}</span></div>`:''}`;
    } else {
      const checked=[...document.querySelectorAll('#obat-list input:checked')];
      const ket=document.getElementById('ket-obat').value.trim();
      let ok=true;
      document.getElementById('err-obat').classList.remove('show');
      document.getElementById('err-ket-obat').classList.remove('show');
      if(!checked.length){document.getElementById('err-obat').classList.add('show');ok=false;}
      if(!ket){document.getElementById('err-ket-obat').classList.add('show');ok=false;}
      if(!ok)return;
      document.getElementById('confirm-content').innerHTML=`
        <div class="confirm-row"><span class="confirm-key">Nama</span><span class="confirm-val">${state.nama}</span></div>
        <div class="confirm-row"><span class="confirm-key">Kelas</span><span class="confirm-val">${state.kelas}</span></div>
        <div class="confirm-row"><span class="confirm-key">Layanan</span><span class="confirm-val">💊 Pengambilan Obat</span></div>
        <div class="confirm-row"><span class="confirm-key">Obat</span><span class="confirm-val">${checked.map(c=>c.value).join(', ')}</span></div>
        <div class="confirm-row"><span class="confirm-key">Keluhan</span><span class="confirm-val">${ket}</span></div>`;
    }
    showPage('page4'); updateProgress(4);
  }

  function backFromKonfirmasi() {
    showPage(state.layanan==='uks'?'page3uks':'page3obat');
    updateProgress(3);
  }

  async function submitLaporan() {
    const now=new Date();
    const timeStr=now.toLocaleTimeString('id-ID',{hour:'2-digit',minute:'2-digit'})+' · '+now.toLocaleDateString('id-ID',{day:'numeric',month:'short',year:'numeric'});
    let badge='', detail='';
    if(state.layanan==='uks'){
      badge='🏥 Ruang UKS';
      const keluhan=document.getElementById('keluhan').value;
      const minum=document.querySelector('input[name="minum-obat"]:checked')?.value||'Tidak';
      const obatKonsumsi=document.getElementById('obat-konsumsi').value.trim();
      detail=keluhan+(minum==='Ya' && obatKonsumsi ? ' | Obat: '+obatKonsumsi : '');
    } else {
      badge='💊 Pengambilan Obat';
      detail=[...document.querySelectorAll('#obat-list input:checked')].map(c=>c.value).join(', ');
    }
    const entry={ id:Date.now(), nama:state.nama, kelas:state.kelas, badge, detail, time:timeStr, timestamp:Date.now() };

    // Simpan ke Supabase
    tampilLoading(true);
    try {
      await simpanLaporan(entry);
      laporanData.unshift(entry);
      riwayat.unshift(entry);
      renderRiwayat();
      document.getElementById('progressTrack').style.display='none';
      showPage('page5');
      tampilkanNotif(badge, state.nama, state.kelas, timeStr);
    } catch(e) {
      alert('Gagal mengirim laporan. Cek koneksi internet dan coba lagi.');
      console.error(e);
    }
    tampilLoading(false);
  }

  function renderRiwayat() {
    const sec=document.getElementById('riwayatSection');
    if(!riwayat.length){sec.style.display='none';return;}
    sec.style.display='block';
    document.getElementById('riwayat-list').innerHTML=riwayat.map(r=>`
      <div class="riwayat-item">
        <div class="riwayat-item-top">
          <div><span class="riwayat-name">${r.nama}</span><span class="kelas-badge">${r.kelas}</span></div>
          <span class="riwayat-time">${r.time}</span>
        </div>
        <div class="riwayat-badge">${r.badge}</div>
        <div class="riwayat-detail">${r.detail}</div>
      </div>`).join('');
  }

  function buatLaporanBaru() {
    document.getElementById('nama').value='';
    document.getElementById('kelas').value='';
    document.getElementById('keluhan').value='';
    document.getElementById('ket-uks').value='';
    document.getElementById('ket-obat').value='';
    document.getElementById('obat-konsumsi').value='';
    document.getElementById('obat-konsumsi-group').style.display='none';
    document.querySelectorAll('#obat-list input').forEach(cb=>cb.checked=false);
    document.querySelector('#mo-tidak').checked=true;
    state={nama:'',kelas:'',layanan:''};
    document.getElementById('progressTrack').style.display='block';
    updateProgress(1); showPage('page1'); renderRiwayat();
  }

  // ===== NOTIFIKASI =====
  let notifTimer=null;
  function tampilkanNotif(layanan,nama,kelas,waktu){
    document.getElementById('notif-layanan').textContent=layanan;
    document.getElementById('notif-nama').textContent=nama;
    document.getElementById('notif-kelas').textContent='Kelas '+kelas;
    document.getElementById('notif-waktu').textContent=waktu;
    const prog=document.getElementById('notifProgress');
    prog.style.animation='none'; prog.offsetHeight;
    prog.style.animation='shrink 4s linear forwards';
    document.getElementById('notifBanner').classList.add('show');
    if(notifTimer)clearTimeout(notifTimer);
    notifTimer=setTimeout(()=>tutupNotif(),4000);
  }
  function tutupNotif(){
    document.getElementById('notifBanner').classList.remove('show');
    if(notifTimer)clearTimeout(notifTimer);
  }

  // ===== ADMIN =====
  let adminFiltered=[];

  async function adminLoadData(){
    tampilLoading(true);
    try {
      const data = await sbFetch('laporan?select=*&order=timestamp.desc');
      laporanData = data || [];
    } catch(e) {
      console.error('Gagal memuat data admin:', e);
    }
    tampilLoading(false);
    updateAdminStats();
    applyFilter();
  }

  function updateAdminStats(){
    const today=new Date().toLocaleDateString('id-ID',{day:'numeric',month:'short',year:'numeric'});
    document.getElementById('stat-total').textContent=laporanData.length;
    document.getElementById('stat-uks').textContent=laporanData.filter(d=>d.badge.includes('UKS')).length;
    document.getElementById('stat-obat').textContent=laporanData.filter(d=>d.badge.includes('Obat')).length;
    document.getElementById('stat-hari').textContent=laporanData.filter(d=>d.time.includes(today)).length;
  }

  function applyFilter(){
    const tgl=document.getElementById('filterTanggal').value;
    const lay=document.getElementById('filterLayanan').value;
    adminFiltered=laporanData.filter(d=>{
      let m=true;
      if(tgl){const fd=new Date(tgl).toLocaleDateString('id-ID',{day:'numeric',month:'short',year:'numeric'});m=m&&d.time.includes(fd);}
      if(lay==='uks') m=m&&d.badge.includes('UKS');
      if(lay==='obat')m=m&&d.badge.includes('Obat');
      return m;
    });
    document.getElementById('filterCount').textContent=adminFiltered.length;
    renderTable();
  }

  function resetFilter(){
    document.getElementById('filterTanggal').value='';
    document.getElementById('filterLayanan').value='';
    applyFilter();
  }

  function renderTable(){
    const c=document.getElementById('tableContent');
    if(!adminFiltered.length){
      c.innerHTML=`<div class="empty-state"><div class="empty-icon">📭</div><div class="empty-title">Belum Ada Laporan</div><div class="empty-sub">Laporan yang masuk akan tampil di sini</div></div>`;
      return;
    }
    c.innerHTML=`<table><thead><tr><th>#</th><th>Nama Siswa</th><th>Layanan</th><th>Detail</th><th>Waktu</th><th>Aksi</th></tr></thead><tbody>`+
      adminFiltered.map((d,i)=>`<tr>
        <td class="td-no">${i+1}</td>
        <td class="td-nama">${d.nama}<span class="kelas-badge">${d.kelas}</span></td>
        <td><span class="layanan-badge ${d.badge.includes('UKS')?'uks':'obat'}">${d.badge}</span></td>
        <td class="td-detail" title="${d.detail}">${d.detail}</td>
        <td class="td-waktu">${d.time}</td>
        <td><button class="btn-hapus-row" onclick="konfirmasiHapus(${d.id},'${d.nama.replace(/'/g,"\\'")}')">🗑️ Hapus</button></td>
      </tr>`).join('')+`</tbody></table>`;
  }

  // ===== MODAL =====
  function konfirmasiHapus(id,nama){
    document.getElementById('modalTitle').textContent='Hapus Laporan?';
    document.getElementById('modalSub').textContent=`Laporan atas nama "${nama}" akan dihapus permanen.`;
    document.getElementById('modalConfirmBtn').onclick=()=>hapusLaporan(id);
    document.getElementById('modalOverlay').classList.add('show');
  }
  function konfirmasiHapusSemua(){
    if(!laporanData.length)return;
    document.getElementById('modalTitle').textContent='Hapus Semua Laporan?';
    document.getElementById('modalSub').textContent=`Seluruh ${laporanData.length} laporan akan dihapus permanen.`;
    document.getElementById('modalConfirmBtn').onclick=()=>hapusSemua();
    document.getElementById('modalOverlay').classList.add('show');
  }
  function tutupModal(){document.getElementById('modalOverlay').classList.remove('show');}

  async function hapusLaporan(id){
    tampilLoading(true);
    try {
      await hapusDariDB(id);
      laporanData=laporanData.filter(d=>d.id!==id);
      riwayat=riwayat.filter(d=>d.id!==id);
      renderRiwayat();
    } catch(e) { alert('Gagal menghapus. Coba lagi.'); console.error(e); }
    tampilLoading(false);
    tutupModal(); updateAdminStats(); applyFilter();
  }

  async function hapusSemua(){
    tampilLoading(true);
    try {
      await hapusSemuaDariDB();
      laporanData=[]; riwayat=[];
      renderRiwayat();
    } catch(e) { alert('Gagal menghapus semua. Coba lagi.'); console.error(e); }
    tampilLoading(false);
    tutupModal(); updateAdminStats(); applyFilter();
  }

  document.getElementById('modalOverlay').addEventListener('click',function(e){if(e.target===this)tutupModal();});

  // ===== INIT =====
  updateProgress(1);
  muatData(); // muat data dari Supabase saat halaman dibuka
</script>
</body>
</html>
