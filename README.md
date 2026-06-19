[gesin-tyd-bank (1).html](https://github.com/user-attachments/files/29136497/gesin-tyd-bank.1.html)
<!DOCTYPE html>
<html lang="af">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
<title>Ons Gesin se Tyd-bank</title>
<style>
  :root{
    --bg-deep:#1F2B2F;
    --bg:#28363B;
    --bg-soft:#324349;
    --paper:#F7EFE0;
    --paper-line:#E2D4B0;
    --ink:#28363B;
    --ink-soft:#4B5C5C;
    --cream:#F2E9D8;
    --muted:#9FB0AC;
    --gold:#D9A441;
    --gold-deep:#B8852E;
    --sage:#7A9471;
    --sage-deep:#56705A;
    --clay:#C1572C;
    --clay-deep:#9C4520;
    --shadow:rgba(15,20,22,0.4);
    --radius:16px;
    --font-display:'Fraunces', serif;
    --font-body:'Figtree', sans-serif;
    --font-mono:'Space Mono', monospace;
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;}
  body{
    font-family:var(--font-body);
    background:
      radial-gradient(circle at 15% 8%, rgba(217,164,65,0.07), transparent 40%),
      radial-gradient(circle at 85% 92%, rgba(122,148,113,0.08), transparent 45%),
      var(--bg-deep);
    color:var(--cream);
    min-height:100vh;
    -webkit-font-smoothing:antialiased;
  }
  #app{
    max-width:560px;
    margin:0 auto;
    min-height:100vh;
    padding:18px 16px 48px;
    position:relative;
  }
  .hidden{display:none !important;}
  .eyebrow{
    font-family:var(--font-mono);
    font-size:11px;
    letter-spacing:2.5px;
    text-transform:uppercase;
    color:var(--gold);
    display:block;
    margin-bottom:6px;
  }
  h1,h2,h3{font-family:var(--font-display);margin:0;font-weight:600;}
  button{font-family:var(--font-body);cursor:pointer;}
  input,select,textarea{font-family:var(--font-body);}
  ::selection{background:var(--gold);color:var(--ink);}

  /* ---------- loading ---------- */
  #loading-screen{
    display:flex;flex-direction:column;align-items:center;justify-content:center;
    min-height:80vh;gap:14px;text-align:center;
  }
  .pin-spinner{
    width:34px;height:34px;border-radius:50%;
    border:3px solid rgba(217,164,65,0.25);
    border-top-color:var(--gold);
    animation:spin 0.9s linear infinite;
  }
  @keyframes spin{to{transform:rotate(360deg);}}
  #loading-text{color:var(--muted);font-size:14px;}

  /* ---------- board header ---------- */
  .board-header{text-align:center;padding:18px 6px 22px;}
  .board-header h1{font-size:clamp(26px,6.5vw,38px);color:var(--cream);line-height:1.1;}
  .date-sub{color:var(--muted);font-size:13px;margin-top:8px;font-family:var(--font-mono);}

  /* ---------- pinned card base ---------- */
  .card{
    background:var(--paper);
    color:var(--ink);
    border-radius:var(--radius);
    padding:22px 18px 18px;
    margin-bottom:18px;
    position:relative;
    box-shadow:0 10px 24px var(--shadow), 0 1px 0 rgba(255,255,255,0.06) inset;
  }
  .card::before{
    content:"";
    position:absolute; top:-7px; left:50%; transform:translateX(-50%);
    width:14px;height:14px;border-radius:50%;
    background:radial-gradient(circle at 35% 30%, #fff8 0%, var(--gold) 45%, var(--gold-deep) 100%);
    box-shadow:0 3px 5px rgba(0,0,0,0.45);
  }
  .card .eyebrow{color:var(--gold-deep);}

  /* ---------- profile select ---------- */
  .profile-grid{display:flex;flex-direction:column;gap:14px;}
  .profile-card{
    background:var(--paper);color:var(--ink);
    border-radius:var(--radius);
    padding:18px 18px 16px;
    display:flex;align-items:center;justify-content:space-between;
    border:none; width:100%; text-align:left;
    box-shadow:0 8px 18px var(--shadow);
    transition:transform 0.15s ease, box-shadow 0.15s ease;
    position:relative;
    overflow:hidden;
  }
  .profile-card:hover{transform:translateY(-2px);box-shadow:0 12px 22px var(--shadow);}
  .profile-card:active{transform:translateY(0px) scale(0.99);}
  .profile-card .stripe{
    position:absolute; left:0; top:0; bottom:0; width:6px;
  }
  .profile-card .pc-name{font-family:var(--font-display);font-size:21px;font-weight:600;margin-bottom:2px;}
  .profile-card .pc-age{color:var(--ink-soft);font-size:13px;font-family:var(--font-mono);}
  .profile-card .pc-balance{font-family:var(--font-mono);font-size:13px;font-weight:700;text-align:right;}
  .profile-card .pc-balance .num{font-size:20px;display:block;}
  .parent-link{
    display:block; width:100%; margin-top:8px;
    background:none; border:1.5px dashed rgba(242,233,216,0.35);
    color:var(--cream); border-radius:12px; padding:14px;
    font-size:14px; letter-spacing:0.3px;
    transition:border-color 0.15s ease, background 0.15s ease;
  }
  .parent-link:hover{border-color:var(--gold);background:rgba(217,164,65,0.08);}

  /* ---------- top nav ---------- */
  .topbar{display:flex;align-items:center;gap:12px;margin-bottom:14px;}
  .topbar button{
    background:none;border:1px solid rgba(242,233,216,0.3);color:var(--cream);
    border-radius:10px;padding:8px 12px;font-size:13px;
  }
  .topbar button:hover{border-color:var(--gold);color:var(--gold);}
  .topbar .kid-title{font-family:var(--font-display);font-size:20px;color:var(--cream);}

  /* ---------- bank card / timer ---------- */
  .bank-card{text-align:center;}
  .bank-readout{
    font-family:var(--font-mono); font-weight:700;
    font-size:clamp(40px,11vw,58px);
    letter-spacing:1px; line-height:1;
    margin:6px 0 2px;
    color:var(--ink);
  }
  .bank-readout.running{color:var(--clay-deep);}
  .bank-sub{color:var(--ink-soft);font-size:13px;margin-bottom:14px;}
  .btn-primary{
    background:var(--gold); color:var(--ink); border:none;
    border-radius:12px; padding:13px 22px; font-weight:600; font-size:15px;
    width:100%; transition:transform 0.12s ease, background 0.15s ease;
  }
  .btn-primary:hover{background:var(--gold-deep);}
  .btn-primary:active{transform:scale(0.98);}
  .btn-primary.stop{background:var(--clay);}
  .btn-primary.stop:hover{background:var(--clay-deep);}
  .btn-primary:disabled{background:#cdbfa0;color:#7a7263;cursor:not-allowed;}
  .session-log{margin-top:14px;text-align:left;font-size:12.5px;color:var(--ink-soft);}
  .session-log .s-row{display:flex;justify-content:space-between;padding:4px 2px;border-bottom:1px dotted var(--paper-line);font-family:var(--font-mono);}
  .session-log .s-empty{font-style:italic;color:var(--ink-soft);font-family:var(--font-body);}

  /* ---------- ledger rows ---------- */
  .ledger-row{
    display:flex;align-items:center;gap:12px;
    padding:13px 2px;
    border-bottom:1px dashed var(--paper-line);
    position:relative;
    cursor:pointer;
    user-select:none;
  }
  .ledger-row:last-child{border-bottom:none;}
  .ledger-row input[type="checkbox"]{
    width:21px;height:21px;flex-shrink:0;accent-color:var(--sage-deep);cursor:pointer;
  }
  .ledger-row .task-name{flex:1;font-size:15px;line-height:1.3;}
  .ledger-amount{flex-shrink:0;}
  .la-stack{display:flex;flex-direction:column;align-items:flex-end;gap:1px;}
  .la-min{font-family:var(--font-mono);font-weight:700;font-size:14px;color:var(--gold-deep);}
  .la-extra{font-family:var(--font-mono);font-size:10.5px;color:var(--ink-soft);}
  .ledger-row.done .task-name{text-decoration:line-through;opacity:0.5;}
  .ledger-row.done .ledger-amount{opacity:0.45;}
  .stamp{
    font-family:var(--font-mono); font-size:10px; letter-spacing:1.5px;
    color:var(--sage-deep); border:2px solid var(--sage-deep); border-radius:4px;
    padding:2px 7px; transform:rotate(-9deg);
    position:absolute; right:8px; top:50%; margin-top:-22px;
    opacity:0; pointer-events:none;
  }
  .stamp.show{animation:stamp-in 0.4s ease-out forwards;}
  @keyframes stamp-in{
    0%{transform:rotate(-9deg) scale(2.2);opacity:0;}
    60%{opacity:0.95;}
    100%{transform:rotate(-9deg) scale(1);opacity:0.9;}
  }

  /* ---------- affirmation card ---------- */
  .affirmation-card{text-align:center;background:linear-gradient(160deg, #FBF4E3 0%, var(--paper) 100%);}
  .affirmation-text{
    font-family:var(--font-display); font-size:19px; line-height:1.4; font-style:italic;
    margin:6px 4px 8px; color:var(--ink);
  }
  .affirmation-ref{font-family:var(--font-mono);font-size:12px;color:var(--gold-deep);letter-spacing:0.5px;}

  /* ---------- bible card ---------- */
  .bible-card .bible-ref{
    font-family:var(--font-display); font-size:22px; font-weight:600;
    margin:2px 0 12px;
  }
  .bible-question{font-size:13.5px;color:var(--ink-soft);margin:10px 2px 8px;font-style:italic;}
  textarea#bible-answer{
    width:100%; min-height:64px; border-radius:10px; border:1px solid var(--paper-line);
    background:#FFFCF5; padding:10px 12px; font-size:14px; color:var(--ink);
    resize:vertical;
  }
  textarea#bible-answer:focus, input:focus, select:focus{outline:2px solid var(--gold-deep); outline-offset:1px;}

  /* ---------- date nav (parent) ---------- */
  .date-nav{display:flex;align-items:center;gap:8px;margin-bottom:16px;}
  .date-nav button{
    background:var(--bg-soft);border:1px solid rgba(242,233,216,0.25);color:var(--cream);
    width:38px;height:38px;border-radius:10px;font-size:16px;
  }
  .date-nav input[type="date"]{
    flex:1; background:var(--paper); color:var(--ink); border:none; border-radius:10px;
    padding:10px 12px; font-family:var(--font-mono); font-size:14px;
  }

  /* ---------- parent summary ---------- */
  .kid-summary{margin-bottom:16px;}
  .kid-summary-head{display:flex;justify-content:space-between;align-items:baseline;margin-bottom:4px;}
  .kid-summary-head .ks-name{font-family:var(--font-display);font-size:19px;}
  .kid-summary-head .ks-stats{font-family:var(--font-mono);font-size:13px;color:var(--gold-deep);}
  .ks-balance-row{display:flex;justify-content:space-between;font-family:var(--font-mono);font-size:12px;color:var(--ink-soft);margin:0 0 10px;}
  .ks-balance-row .ks-pending{color:var(--clay-deep);font-weight:700;}
  .ks-task-row{display:flex;align-items:center;gap:8px;padding:6px 2px;font-size:13.5px;border-bottom:1px dotted var(--paper-line);}
  .ks-task-row:last-child{border-bottom:none;}
  .ks-dot{width:9px;height:9px;border-radius:50%;flex-shrink:0;}
  .ks-dot.on{background:var(--sage-deep);}
  .ks-dot.off{background:#cfc2a0;}
  .ks-task-row .ks-tname.off{color:var(--ink-soft);}
  .ks-bible-answer{margin-top:8px;font-size:13px;font-style:italic;color:var(--ink-soft);background:#FFFCF5;border-radius:8px;padding:8px 10px;}
  .ks-reset{
    margin-top:0;background:none;border:1px solid #cfc2a0;color:var(--clay-deep);
    border-radius:8px;padding:6px 10px;font-size:12px;
  }
  .ks-deduct{
    background:none;border:1px solid var(--clay);color:var(--clay-deep);
    border-radius:8px;padding:6px 10px;font-size:12px;
  }
  .ks-actions-row{display:flex;gap:8px;margin-top:10px;}
  .ks-live{font-size:11px;color:var(--clay-deep);font-family:var(--font-mono);margin-left:6px;}

  .parent-actions{display:flex;flex-direction:column;gap:10px;margin-top:6px;}
  .btn-secondary{
    background:var(--bg-soft); color:var(--cream); border:1px solid rgba(242,233,216,0.25);
    border-radius:12px;padding:13px 16px;font-size:14.5px;text-align:left;
    display:flex;justify-content:space-between;align-items:center;
  }
  .btn-secondary:hover{border-color:var(--gold);color:var(--gold);}
  .btn-secondary .badge-count{font-family:var(--font-mono);font-size:11px;color:var(--clay);}

  /* ---------- manage / editor views ---------- */
  .editor-row{
    background:#FFFCF5;border:1px solid var(--paper-line);border-radius:12px;
    padding:14px;margin-bottom:12px;
  }
  .editor-row label{display:block;font-size:11.5px;color:var(--ink-soft);margin-bottom:4px;font-family:var(--font-mono);letter-spacing:0.5px;}
  .editor-row input[type="text"], .editor-row input[type="number"], .editor-row select{
    width:100%;padding:9px 10px;border-radius:8px;border:1px solid var(--paper-line);
    background:#fff;color:var(--ink);font-size:14px;margin-bottom:10px;
  }
  .editor-row .erow-2col{display:grid;grid-template-columns:1fr 1fr;gap:10px;}
  .editor-row .erow-3col{display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;}
  .editor-row .erow-bottom{display:flex;justify-content:space-between;align-items:center;}
  .editor-row .erow-active{display:flex;align-items:center;gap:6px;font-size:13px;color:var(--ink-soft);}
  .erow-delete{background:none;border:none;color:var(--clay-deep);font-size:13px;text-decoration:underline;}
  .erow-bible-tag{font-size:11px;color:var(--sage-deep);font-family:var(--font-mono);margin-bottom:8px;}

  .btn-add{
    width:100%;background:none;border:1.5px dashed rgba(242,233,216,0.4);color:var(--cream);
    border-radius:12px;padding:13px;font-size:14px;margin-bottom:14px;
  }
  .btn-add:hover{border-color:var(--gold);color:var(--gold);}
  .btn-save-bar{
    background:var(--gold);color:var(--ink);border:none;border-radius:12px;
    padding:14px;font-weight:600;font-size:15px;width:100%;
  }
  .btn-save-bar:hover{background:var(--gold-deep);}

  .rotation-preview{margin-top:18px;}
  .rotation-preview .rp-row{display:flex;justify-content:space-between;font-size:12.5px;padding:5px 2px;border-bottom:1px dotted var(--paper-line);font-family:var(--font-mono);}

  /* ---------- auth (PIN + parent password) ---------- */
  .auth-wrap{display:flex;flex-direction:column;align-items:center;justify-content:center;min-height:62vh;text-align:center;gap:4px;}
  .auth-icon{font-size:32px;margin-bottom:4px;}
  .auth-hint{color:var(--muted);font-size:13.5px;margin-top:4px;}
  .pin-dots{display:flex;gap:14px;justify-content:center;margin:22px 0;}
  .pin-dot{width:16px;height:16px;border-radius:50%;border:2px solid var(--gold);background:transparent;transition:background 0.15s ease, transform 0.15s ease, border-color 0.15s ease;}
  .pin-dot.filled{background:var(--gold);transform:scale(1.1);}
  .pin-dot.error{border-color:var(--clay);background:var(--clay);}
  .keypad{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;max-width:260px;margin:0 auto;width:100%;}
  .keypad button{background:var(--bg-soft);color:var(--cream);border:1px solid rgba(242,233,216,0.2);border-radius:14px;font-size:22px;font-family:var(--font-mono);padding:16px 0;}
  .keypad button:hover{border-color:var(--gold);color:var(--gold);}
  .keypad button.kp-empty{background:none;border:none;visibility:hidden;}
  .keypad button.kp-back{font-size:17px;}

  .parent-auth-form{max-width:320px;margin:18px auto 0;width:100%;}
  .parent-auth-form input{width:100%;padding:13px 14px;border-radius:10px;border:1px solid rgba(242,233,216,0.25);background:rgba(247,239,224,0.06);color:var(--cream);font-size:16px;margin-bottom:12px;text-align:center;letter-spacing:1px;}
  .parent-auth-form input::placeholder{color:var(--muted);}
  .forgot-link{background:none;border:none;color:var(--muted);font-size:12.5px;text-decoration:underline;margin-top:14px;}
  .forgot-link:hover{color:var(--gold);}
  #forgot-password-box{max-width:320px;margin:18px auto 0;width:100%;}
  #forgot-password-box input{width:100%;padding:11px;border-radius:8px;border:1px solid rgba(242,233,216,0.25);background:rgba(247,239,224,0.06);color:var(--cream);margin-top:8px;text-align:center;}

  /* ---------- rewards / sakgeld ---------- */
  .balance-stats{display:flex;gap:12px;margin-bottom:4px;}
  .balance-stat{flex:1;background:#FFFCF5;border:1px solid var(--paper-line);border-radius:14px;padding:16px 12px;text-align:center;}
  .balance-stat .bs-num{font-family:var(--font-mono);font-weight:700;font-size:26px;color:var(--ink);}
  .balance-stat .bs-label{font-size:10.5px;color:var(--ink-soft);letter-spacing:1px;text-transform:uppercase;font-family:var(--font-mono);margin-top:2px;}

  .reward-row{display:flex;align-items:center;gap:10px;padding:12px 2px;border-bottom:1px dashed var(--paper-line);}
  .reward-row:last-child{border-bottom:none;}
  .reward-row .rw-name{flex:1;font-size:14.5px;}
  .reward-row .rw-cost{font-family:var(--font-mono);font-size:12.5px;color:var(--gold-deep);font-weight:700;}
  .reward-row button{background:var(--sage-deep);color:#fff;border:none;border-radius:8px;padding:9px 13px;font-size:12.5px;flex-shrink:0;}
  .reward-row button:disabled{background:#cfc2a0;color:#7a7263;}

  .payout-box{display:flex;gap:8px;margin-top:4px;}
  .payout-box input{flex:1;padding:10px;border-radius:8px;border:1px solid var(--paper-line);font-family:var(--font-mono);font-size:14px;}
  .payout-box button{background:var(--clay);color:#fff;border:none;border-radius:8px;padding:10px 16px;font-size:13px;flex-shrink:0;}
  .payout-box button:disabled{background:#cfc2a0;color:#7a7263;}

  .my-requests .mr-row{display:flex;justify-content:space-between;align-items:center;padding:8px 2px;border-bottom:1px dotted var(--paper-line);font-size:13px;}
  .my-requests .mr-row:last-child{border-bottom:none;}
  .badge{font-family:var(--font-mono);font-size:10px;padding:3px 9px;border-radius:20px;letter-spacing:0.5px;flex-shrink:0;}
  .badge.pending{background:#EFE0B8;color:var(--gold-deep);}
  .badge.approved{background:#D7E3CF;color:var(--sage-deep);}
  .badge.declined{background:#EFD2C4;color:var(--clay-deep);}

  .req-row{display:flex;align-items:center;gap:10px;padding:12px 2px;border-bottom:1px dashed var(--paper-line);}
  .req-row:last-child{border-bottom:none;}
  .req-info{flex:1;}
  .req-info .ri-kid{font-family:var(--font-mono);font-size:11px;color:var(--ink-soft);text-transform:uppercase;letter-spacing:0.5px;}
  .req-info .ri-detail{font-size:14.5px;}
  .req-actions{display:flex;gap:6px;flex-shrink:0;}
  .req-actions button{border:none;border-radius:8px;padding:9px 11px;font-size:12px;}
  .req-approve{background:var(--sage-deep);color:#fff;}
  .req-decline{background:var(--clay);color:#fff;}

  .kid-bank-link{display:block;width:100%;text-align:center;background:var(--bg-soft);border:1px solid rgba(242,233,216,0.25);border-radius:12px;padding:13px;color:var(--cream);font-size:13.5px;margin-bottom:18px;}
  .kid-bank-link:hover{border-color:var(--gold);color:var(--gold);}

  /* ---------- toast ---------- */
  .toast{
    position:fixed;bottom:22px;left:50%;transform:translateX(-50%) translateY(20px);
    background:var(--bg-soft);color:var(--cream);padding:12px 18px;border-radius:10px;
    font-size:13.5px;box-shadow:0 8px 20px rgba(0,0,0,0.4);
    opacity:0;pointer-events:none;transition:opacity 0.25s ease, transform 0.25s ease;
    z-index:50;max-width:90%;text-align:center;border:1px solid rgba(217,164,65,0.4);
  }
  .toast.show{opacity:1;transform:translateX(-50%) translateY(0);}

  /* ---------- setup ---------- */
  .setup-intro{text-align:center;margin-bottom:20px;}
  .setup-intro p{color:var(--muted);font-size:14px;line-height:1.5;margin-top:8px;}
  .field-label{font-size:11.5px;color:var(--ink-soft);margin-bottom:4px;font-family:var(--font-mono);letter-spacing:0.5px;display:block;}
  .plain-input{width:100%;padding:10px;border-radius:8px;border:1px solid var(--paper-line);background:#fff;color:var(--ink);font-size:14px;margin:4px 0 12px;}
  .card-note{font-size:13px;color:var(--ink-soft);margin:6px 2px 14px;line-height:1.4;}

  @media (prefers-reduced-motion:reduce){
    *{animation-duration:0.001ms !important;transition-duration:0.001ms !important;}
  }
</style>
</head>
<body>

<div id="toast" class="toast"></div>

<div id="app">

  <div id="loading-screen">
    <div class="pin-spinner"></div>
    <div id="loading-text">Laai...</div>
  </div>

  <!-- ============ SETUP (first run) ============ -->
  <div id="view-setup" class="view hidden">
    <div class="board-header">
      <span class="eyebrow">EERSTE OPSTELLING</span>
      <h1>Welkom by die Tyd-bank</h1>
    </div>
    <div class="card">
      <div class="setup-intro">
        <h3>Stel julle drie kinders op</h3>
        <p>Gee elke kind 'n naam en 'n eie 4-syfer PIN, sodat hulle net hulle eie ruimte kan oopmaak.</p>
      </div>
      <div id="setup-kid-inputs"></div>
    </div>
    <div class="card">
      <span class="eyebrow">OUER-BEVEILIGING</span>
      <p class="card-note">Hierdie wagwoord beskerm die Ouer-oorsig, sodat net jy take, minute en goedkeurings kan verander.</p>
      <label class="field-label">OUER-WAGWOORD</label>
      <input type="text" id="setup-parent-pw" class="plain-input" placeholder="Ten minste 4 karakters">
      <label class="field-label">SEKURITEITSVRAAG (vir as jy die wagwoord vergeet)</label>
      <input type="text" id="setup-parent-sq" class="plain-input" placeholder="bv. Wat is ons hond se naam?">
      <label class="field-label">ANTWOORD</label>
      <input type="text" id="setup-parent-sa" class="plain-input">
    </div>
    <button class="btn-save-bar" id="setup-save-btn">Stoor en begin</button>
  </div>

  <!-- ============ SECURITY-ONLY SETUP (migration) ============ -->
  <div id="view-security-setup" class="view hidden">
    <div class="board-header">
      <span class="eyebrow">BEVEILIG JULLE APP</span>
      <h1>Stel wagwoorde op</h1>
      <p class="date-sub">Eenmalig nodig &mdash; dit beskerm elke kind se eie ruimte en die ouer-oorsig.</p>
    </div>
    <div class="card">
      <span class="eyebrow">KINDERS SE PIN-KODES</span>
      <div id="security-setup-kid-inputs"></div>
    </div>
    <div class="card">
      <span class="eyebrow">OUER-WAGWOORD</span>
      <label class="field-label">OUER-WAGWOORD</label>
      <input type="text" id="secsetup-parent-pw" class="plain-input" placeholder="Ten minste 4 karakters">
      <label class="field-label">SEKURITEITSVRAAG</label>
      <input type="text" id="secsetup-parent-sq" class="plain-input" placeholder="bv. Wat is ons hond se naam?">
      <label class="field-label">ANTWOORD</label>
      <input type="text" id="secsetup-parent-sa" class="plain-input">
    </div>
    <button class="btn-save-bar" id="security-setup-save-btn">Stoor en gaan voort</button>
  </div>

  <!-- ============ PROFILE SELECT ============ -->
  <div id="view-select" class="view hidden">
    <div class="board-header">
      <span class="eyebrow">FAMILIE TYD-BANK</span>
      <h1>Wie is jy vandag?</h1>
      <p class="date-sub" id="today-date-label"></p>
    </div>
    <div class="profile-grid" id="profile-grid"></div>
    <button class="parent-link" id="btn-open-parent">Ouer-oorsig &rarr;</button>
  </div>

  <!-- ============ PIN ENTRY (kid) ============ -->
  <div id="view-pin-entry" class="view hidden">
    <nav class="topbar">
      <button id="btn-back-from-pin">&larr; Terug</button>
      <div class="kid-title" id="pin-kid-title"></div>
    </nav>
    <div class="auth-wrap">
      <div class="auth-icon">&#128274;</div>
      <p class="auth-hint">Tik jou 4-syfer kode in</p>
      <div class="pin-dots" id="pin-dots"></div>
      <div class="keypad" id="pin-keypad"></div>
    </div>
  </div>

  <!-- ============ PARENT PASSWORD GATE ============ -->
  <div id="view-parent-auth" class="view hidden">
    <nav class="topbar">
      <button id="btn-back-from-parent-auth">&larr; Terug</button>
      <div class="kid-title">Ouer-oorsig</div>
    </nav>
    <div class="auth-wrap">
      <div class="auth-icon">&#128272;</div>
      <p class="auth-hint">Voer die ouer-wagwoord in</p>
      <div class="parent-auth-form">
        <input type="password" id="parent-password-input" placeholder="Wagwoord" autocomplete="off">
        <button class="btn-primary" id="btn-parent-auth-submit">Gaan in</button>
        <button class="forgot-link" id="btn-forgot-password">Wagwoord vergeet?</button>
      </div>
      <div id="forgot-password-box" class="hidden">
        <p class="auth-hint" id="security-question-display"></p>
        <input type="text" id="security-answer-input" placeholder="Jou antwoord">
        <button class="btn-primary" id="btn-verify-security-answer" style="margin-top:10px;">Bevestig antwoord</button>
      </div>
    </div>
  </div>

  <!-- ============ KID VIEW ============ -->
  <div id="view-kid" class="view hidden">
    <nav class="topbar">
      <button id="btn-back-from-kid">&larr; Terug</button>
      <div class="kid-title" id="kid-title"></div>
    </nav>

    <section class="card affirmation-card" id="affirmation-card">
      <span class="eyebrow">&#10024; VANDAG SE BEVESTIGING</span>
      <div class="affirmation-text" id="affirmation-text"></div>
      <div class="affirmation-ref" id="affirmation-ref"></div>
    </section>

    <section class="card bank-card" id="bank-card">
      <span class="eyebrow">SKERMTYD-BANK</span>
      <div class="bank-readout" id="bank-readout">0 min</div>
      <div class="bank-sub" id="bank-sub">minute beskikbaar vandag</div>
      <button class="btn-primary" id="btn-toggle-timer">Begin Skermtyd</button>
      <div class="session-log" id="session-log"></div>
    </section>

    <button class="kid-bank-link" id="btn-open-rewards">&#128176; Sakgeld &amp; Belonings &rarr;</button>

    <section class="card bible-card" id="bible-card">
      <span class="eyebrow">&#128214; BYBELSTUDIE VANDAG</span>
      <div class="bible-ref" id="bible-ref-text"></div>
      <div class="ledger-row" id="bible-row">
        <input type="checkbox" id="bible-checkbox">
        <span class="task-name">Ek het dit gelees en oordink</span>
        <span class="ledger-amount la-stack">
          <span class="la-min" id="bible-amount-min"></span>
          <span class="la-extra" id="bible-amount-extra"></span>
        </span>
        <span class="stamp" id="bible-stamp">GEDOEN</span>
      </div>
      <div class="bible-question" id="bible-question-text"></div>
      <textarea id="bible-answer" placeholder="Skryf hier wat jy geleer het (opsioneel)..."></textarea>
    </section>

    <section class="card" id="tasks-card">
      <span class="eyebrow">VANDAG SE TAKE</span>
      <div id="task-list"></div>
    </section>
  </div>

  <!-- ============ REWARDS / SAKGELD (kid) ============ -->
  <div id="view-rewards" class="view hidden">
    <nav class="topbar">
      <button id="btn-back-from-rewards">&larr; Terug</button>
      <div class="kid-title" id="rewards-kid-title"></div>
    </nav>
    <div class="card">
      <span class="eyebrow">MY SALDO</span>
      <div class="balance-stats">
        <div class="balance-stat"><div class="bs-num" id="rewards-points-num">0</div><div class="bs-label">Punte</div></div>
        <div class="balance-stat"><div class="bs-num" id="rewards-rand-num">R0</div><div class="bs-label">Sakgeld</div></div>
      </div>
    </div>
    <div class="card">
      <span class="eyebrow">BELONINGS</span>
      <div id="rewards-list"></div>
    </div>
    <div class="card">
      <span class="eyebrow">VRA SAKGELD UIT</span>
      <p class="card-note">Vra vir 'n deel of al jou opgespaarde sakgeld. Jou ouer moet dit eers goedkeur.</p>
      <div class="payout-box">
        <input type="number" id="payout-amount-input" min="1" step="0.50" placeholder="Bedrag (R)">
        <button id="btn-request-payout">Vra</button>
      </div>
    </div>
    <div class="card">
      <span class="eyebrow">MY VERSOEKE</span>
      <div class="my-requests" id="my-requests-list"></div>
    </div>
    <div class="card">
      <span class="eyebrow">ONLANGSE AANPASSINGS</span>
      <div class="my-requests" id="my-deductions-list"></div>
    </div>
  </div>

  <!-- ============ PARENT DASHBOARD ============ -->
  <div id="view-parent" class="view hidden">
    <nav class="topbar">
      <button id="btn-back-from-parent">&larr; Terug</button>
      <div class="kid-title">Ouer-oorsig</div>
    </nav>
    <div class="date-nav">
      <button id="date-prev">&lsaquo;</button>
      <input type="date" id="date-picker">
      <button id="date-next">&rsaquo;</button>
    </div>
    <div id="parent-summary"></div>
    <div class="parent-actions">
      <button class="btn-secondary" id="btn-manage-tasks"><span>Take bestuur</span><span>&rarr;</span></button>
      <button class="btn-secondary" id="btn-requests"><span>Versoeke hanteer</span><span class="badge-count" id="pending-badge">&rarr;</span></button>
      <button class="btn-secondary" id="btn-manage-rewards"><span>Belonings bestuur</span><span>&rarr;</span></button>
      <button class="btn-secondary" id="btn-manage-bible"><span>Bybel vooruit beplan</span><span>&rarr;</span></button>
      <button class="btn-secondary" id="btn-manage-affirmations"><span>Bevestigings vooruit beplan</span><span>&rarr;</span></button>
      <button class="btn-secondary" id="btn-manage-kids"><span>Kinders &amp; wagwoorde</span><span>&rarr;</span></button>
    </div>
  </div>

  <!-- ============ REQUESTS (parent) ============ -->
  <div id="view-requests" class="view hidden">
    <nav class="topbar">
      <button id="btn-back-from-requests">&larr; Terug</button>
      <div class="kid-title">Versoeke</div>
    </nav>
    <div class="card">
      <span class="eyebrow">WAG VIR GOEDKEURING</span>
      <div id="pending-requests-list"></div>
    </div>
    <div class="card">
      <span class="eyebrow">ONLANGSE BESLUITE</span>
      <div id="resolved-requests-list"></div>
    </div>
  </div>

  <!-- ============ MANAGE REWARDS (parent) ============ -->
  <div id="view-manage-rewards" class="view hidden">
    <nav class="topbar">
      <button id="btn-back-from-rewards-manage">&larr; Terug</button>
      <div class="kid-title">Belonings bestuur</div>
    </nav>
    <div id="rewards-editor-list"></div>
    <button class="btn-add" id="btn-add-reward">+ Voeg nuwe beloning by</button>
    <button class="btn-save-bar" id="btn-save-rewards">Stoor veranderinge</button>
  </div>

  <!-- ============ MANAGE TASKS ============ -->
  <div id="view-manage-tasks" class="view hidden">
    <nav class="topbar">
      <button id="btn-back-from-tasks">&larr; Terug</button>
      <div class="kid-title">Take bestuur</div>
    </nav>
    <div id="tasks-editor-list"></div>
    <button class="btn-add" id="btn-add-task">+ Voeg nuwe taak by</button>
    <button class="btn-save-bar" id="btn-save-tasks">Stoor veranderinge</button>
  </div>

  <!-- ============ MANAGE BIBLE ============ -->
  <div id="view-manage-bible" class="view hidden">
    <nav class="topbar">
      <button id="btn-back-from-bible">&larr; Terug</button>
      <div class="kid-title">Bybel vooruit beplan</div>
    </nav>
    <div class="card">
      <span class="eyebrow">KIES 'N DATUM</span>
      <input type="date" id="bible-date-picker" class="plain-input" style="margin-top:6px;">
      <div style="margin-top:4px;">
        <label class="field-label">SKRIFVERWYSING</label>
        <input type="text" id="bible-ref-input" class="plain-input" placeholder="bv. Psalm 23">
        <label class="field-label">BESPREKINGSVRAAG</label>
        <textarea id="bible-q-input" style="width:100%;min-height:60px;padding:10px;border-radius:8px;border:1px solid var(--paper-line);margin-top:4px;"></textarea>
      </div>
      <div style="display:flex;gap:10px;margin-top:14px;">
        <button class="btn-save-bar" id="btn-save-bible-override" style="flex:1;">Stoor hierdie datum</button>
      </div>
      <button class="ks-reset" id="btn-reset-bible-override" style="margin-top:10px;width:100%;">Gebruik outomatiese rotasie weer</button>
    </div>
    <div class="card rotation-preview">
      <span class="eyebrow">VOORUITSKOU &mdash; VOLGENDE 7 DAE</span>
      <div id="bible-rotation-list"></div>
    </div>
  </div>

  <!-- ============ MANAGE AFFIRMATIONS ============ -->
  <div id="view-manage-affirmations" class="view hidden">
    <nav class="topbar">
      <button id="btn-back-from-affirmations">&larr; Terug</button>
      <div class="kid-title">Bevestigings vooruit beplan</div>
    </nav>
    <div class="card">
      <span class="eyebrow">KIES 'N DATUM</span>
      <input type="date" id="affirmation-date-picker" class="plain-input" style="margin-top:6px;">
      <div style="margin-top:4px;">
        <label class="field-label">BEVESTIGING</label>
        <input type="text" id="affirmation-text-input" class="plain-input" placeholder="bv. Ek is wonderbaar gemaak deur God.">
        <label class="field-label">SKRIFVERWYSING</label>
        <input type="text" id="affirmation-ref-input" class="plain-input" placeholder="bv. Psalm 139:14">
      </div>
      <div style="display:flex;gap:10px;margin-top:14px;">
        <button class="btn-save-bar" id="btn-save-affirmation-override" style="flex:1;">Stoor hierdie datum</button>
      </div>
      <button class="ks-reset" id="btn-reset-affirmation-override" style="margin-top:10px;width:100%;">Gebruik outomatiese rotasie weer</button>
    </div>
    <div class="card rotation-preview">
      <span class="eyebrow">VOORUITSKOU &mdash; VOLGENDE 7 DAE</span>
      <div id="affirmation-rotation-list"></div>
    </div>
  </div>

  <!-- ============ DEDUCT (parent consequence) ============ -->
  <div id="view-deduct" class="view hidden">
    <nav class="topbar">
      <button id="btn-back-from-deduct">&larr; Terug</button>
      <div class="kid-title" id="deduct-title">Trek af</div>
    </nav>
    <div class="card">
      <span class="eyebrow">TREK AF</span>
      <p class="card-note">Trek skermtyd-minute, punte, en/of sakgeld af as gevolg vir wangedrag. Los velde op 0 as dit nie van toepassing is nie. Die rede sal vir die kind wys.</p>
      <div class="erow-3col">
        <div>
          <label class="field-label">MINUTE</label>
          <input type="number" id="deduct-minutes" class="plain-input" min="0" value="0">
        </div>
        <div>
          <label class="field-label">PUNTE</label>
          <input type="number" id="deduct-points" class="plain-input" min="0" value="0">
        </div>
        <div>
          <label class="field-label">SAKGELD (R)</label>
          <input type="number" id="deduct-rand" class="plain-input" min="0" step="0.50" value="0">
        </div>
      </div>
      <label class="field-label">REDE (opsioneel)</label>
      <input type="text" id="deduct-reason" class="plain-input" placeholder="bv. Nie geluister nie by ete-tyd">
      <button class="btn-save-bar" id="btn-confirm-deduct">Trek af</button>
    </div>
    <div class="card">
      <span class="eyebrow">ONLANGSE AANPASSINGS</span>
      <div class="my-requests" id="deduct-history-list"></div>
    </div>
  </div>

  <!-- ============ MANAGE KIDS & PASSWORDS ============ -->
  <div id="view-manage-kids" class="view hidden">
    <nav class="topbar">
      <button id="btn-back-from-kids">&larr; Terug</button>
      <div class="kid-title">Kinders &amp; wagwoorde</div>
    </nav>
    <div id="kids-editor-list"></div>
    <div class="card">
      <span class="eyebrow">OUER-WAGWOORD</span>
      <label class="field-label">NUWE WAGWOORD (los leeg om huidige te behou)</label>
      <input type="text" id="parent-pw-new" class="plain-input" placeholder="Onveranderd">
      <label class="field-label">SEKURITEITSVRAAG</label>
      <input type="text" id="parent-sq" class="plain-input">
      <label class="field-label">ANTWOORD</label>
      <input type="text" id="parent-sa" class="plain-input">
    </div>
    <button class="btn-save-bar" id="btn-save-kids">Stoor veranderinge</button>
  </div>

</div>

<script type="module">
/* =====================================================================
   FIREBASE STORAGE SHIM
   Vervang die Claude-artifact se window.storage met 'n Firestore-weergawe
   wat presies dieselfde get/set/delete/list-koppelvlak bied, sodat die
   res van die app ongeskonde bly.
   ===================================================================== */
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.13.0/firebase-app.js";
import {
  getFirestore, doc, getDoc, setDoc, deleteDoc, collection, getDocs
} from "https://www.gstatic.com/firebasejs/10.13.0/firebase-firestore.js";

const firebaseConfig = {
  apiKey: "AIzaSyA8cwucL4RQo_qZsUv_hzJOfpwiBZ3G_tM",
  authDomain: "gesin-tyd-bank.firebaseapp.com",
  projectId: "gesin-tyd-bank",
  storageBucket: "gesin-tyd-bank.firebasestorage.app",
  messagingSenderId: "895685100105",
  appId: "1:895685100105:web:64d6f6d41226aa79a73598"
};

const fbApp = initializeApp(firebaseConfig);
const db = getFirestore(fbApp);
const COLLECTION = 'tydbank';

window.storage = {
  async get(key, shared = true){
    try{
      const snap = await getDoc(doc(db, COLLECTION, key));
      if(!snap.exists()) return null;
      return { key, value: snap.data().value, shared: !!shared };
    }catch(e){
      console.error('storage.get failed', key, e);
      return null;
    }
  },
  async set(key, value, shared = true){
    try{
      await setDoc(doc(db, COLLECTION, key), { value, updatedAt: Date.now() });
      return { key, value, shared: !!shared };
    }catch(e){
      console.error('storage.set failed', key, e);
      return null;
    }
  },
  async delete(key, shared = true){
    try{
      await deleteDoc(doc(db, COLLECTION, key));
      return { key, deleted:true, shared: !!shared };
    }catch(e){
      console.error('storage.delete failed', key, e);
      return null;
    }
  },
  async list(prefix = '', shared = true){
    try{
      const snap = await getDocs(collection(db, COLLECTION));
      const keys = [];
      snap.forEach(d => { if(!prefix || d.id.startsWith(prefix)) keys.push(d.id); });
      return { keys, prefix, shared: !!shared };
    }catch(e){
      console.error('storage.list failed', e);
      return null;
    }
  }
};
</script>

<script type="module">
/* =====================================================================
   ONS GESIN SE TYD-BANK
   Family task / Bible-study / screen-time / rewards tracker
   Data scope: all keys shared=true (gestoor in Firebase Firestore,
   sigbaar vir almal wat hierdie web-app se skakel oopmaak)
   ===================================================================== */

const KID_COLORS = ['var(--gold)', 'var(--sage)', 'var(--clay)'];

const KEY_PROFILES = 'profiles';
const KEY_TASKS = 'tasks';
const KEY_BIBLE_OVERRIDES = 'bible-overrides';
const KEY_PINS = 'pins';
const KEY_PARENT_AUTH = 'parent-auth';
const KEY_BALANCES = 'balances';
const KEY_REWARDS = 'rewards';
const KEY_REQUESTS = 'requests';
const KEY_AFFIRMATION_OVERRIDES = 'affirmation-overrides';
const KEY_DEDUCTIONS = 'deductions';
const dayKey = (date, kidId) => `day:${date}:${kidId}`;

const DEFAULT_TASKS = [
  { id:'bybel', name:'Bybelstudie', minutes:15, points:10, rand:2, assignedTo:'all', active:true, isBible:true },
  { id:'huiswerk', name:'Skoolhuiswerk klaar', minutes:30, points:10, rand:3, assignedTo:'all', active:true },
  { id:'bed', name:'Maak jou bed op', minutes:10, points:5, rand:1, assignedTo:'all', active:true },
  { id:'kamer', name:'Pak jou kamer op', minutes:15, points:5, rand:2, assignedTo:'all', active:true },
  { id:'skottelgoed', name:'Pak die vaatwasser uit of in', minutes:15, points:8, rand:3, assignedTo:'all', active:true },
  { id:'lees', name:'Lees 20 minute (\u2019n boek, nie skerm nie)', minutes:20, points:8, rand:2, assignedTo:'all', active:true },
  { id:'huistaak', name:'Help met \u2019n huistaak (vee, was hond, ens.)', minutes:15, points:8, rand:3, assignedTo:'all', active:true }
];

const DEFAULT_REWARDS = [
  { id:'rwd1', name:'Kies die fliek vir gesin-aand', pointsCost:40, active:true },
  { id:'rwd2', name:'Ekstra 30 minute skermtyd', pointsCost:25, active:true },
  { id:'rwd3', name:'Speel-datum met \u2019n vriend', pointsCost:60, active:true },
  { id:'rwd4', name:'Spesiale nagereg kies', pointsCost:20, active:true }
];

const BIBLE_ROTATION = [
  { ref:'Psalm 23', q:'Wat leer hierdie psalm jou oor hoe God na jou omsien?' },
  { ref:'Spreuke 3:5-6', q:'Wat beteken dit om met jou hele hart op die Here te vertrou?' },
  { ref:'Filippense 4:6-7', q:'Waaroor is jy deesdae bekommerd, en hoe kan jy dit aan God gee?' },
  { ref:'Johannes 15:1-5', q:'Wat beteken dit om in Jesus te \u201cbly\u201d?' },
  { ref:'Romeine 12:1-2', q:'Hoe kan jy vandag jou gedagtes vernuwe?' },
  { ref:'1 Korinti\u00ebrs 13:4-7', q:'Welke eienskap van liefde is die moeilikste vir jou?' },
  { ref:'Josua 1:9', q:'Waarvoor is jy bang, en wat s\u00ea hierdie vers daaroor?' },
  { ref:'Jesaja 41:10', q:'Hoe verander dit jou dag om te weet God is by jou?' },
  { ref:'Matteus 6:33', q:'Wat beteken dit om eerste die Koninkryk van God te soek?' },
  { ref:'Galasi\u00ebrs 5:22-23', q:'Welke vrugte van die Gees wil jy meer in jou lewe sien?' },
  { ref:'Psalm 139:13-14', q:'Hoe verander dit hoe jy oor jouself dink?' },
  { ref:'Spreuke 16:3', q:'Watter plan wil jy vandag aan die Here toevertrou?' },
  { ref:'Kolossense 3:23', q:'Hoe kan jy vandag jou take doen asof dit vir die Here is?' },
  { ref:'Jakobus 1:19', q:'Wanneer was dit vandag moeilik om gou te luister en stadig te praat?' }
];

const AFFIRMATION_ROTATION = [
  { text:'Ek is wonderbaar gemaak deur God.', ref:'Psalm 139:14' },
  { text:'Ek hoef nie bang te wees nie, want God is by my.', ref:'Jesaja 41:10' },
  { text:'Ek kan alles doen deur Hom wat my krag gee.', ref:'Filippense 4:13' },
  { text:'God het \u2019n goeie plan vir my lewe.', ref:'Jeremia 29:11' },
  { text:'Ek is lief gehad, net soos ek is.', ref:'Romeine 5:8' },
  { text:'Ek is \u2019n kind van God.', ref:'Johannes 1:12' },
  { text:'God se genade is genoeg vir my.', ref:'2 Korinti\u00ebrs 12:9' },
  { text:'Ek kan sterk en moedig wees.', ref:'Josua 1:9' },
  { text:'God sal my nooit verlaat nie.', ref:'Hebree\u00ebrs 13:5' },
  { text:'Ek is geskep met \u2019n doel.', ref:'Efesi\u00ebrs 2:10' },
  { text:'Ek hoef nie bekommerd te wees nie; ek kan alles aan God gee.', ref:'Filippense 4:6-7' },
  { text:'God se liefde vir my verander nooit nie.', ref:'Romeine 8:38-39' },
  { text:'Ek kan vergewe soos God my vergewe het.', ref:'Efesi\u00ebrs 4:32' },
  { text:'Ek is sout en lig in hierdie w\u00eareld.', ref:'Matteus 5:13-14' }
];

/* ---------------- state ---------------- */
let profiles = null;
let tasks = null;
let bibleOverrides = null;
let pins = null;
let parentAuth = null;
let balances = null;
let rewards = null;
let requests = null;
let affirmationOverrides = null;
let deductions = null;
let deductTargetKidId = null;
let currentKidId = null;
let currentDayRecord = null;
let parentDateStr = null;
let timerInterval = null;
let pendingPinKidId = null;
let pinBuffer = '';

/* ---------------- date helpers ---------------- */
function formatDate(d){
  const y = d.getFullYear();
  const m = String(d.getMonth()+1).padStart(2,'0');
  const day = String(d.getDate()).padStart(2,'0');
  return `${y}-${m}-${day}`;
}
function todayStr(){ return formatDate(new Date()); }
function dayOfYear(dateStr){
  const d = new Date(dateStr + 'T00:00:00');
  const start = new Date(d.getFullYear(),0,0);
  const diff = d - start;
  return Math.floor(diff / (1000*60*60*24));
}
const AF_MONTHS = ['Jan','Feb','Mrt','Apr','Mei','Jun','Jul','Aug','Sep','Okt','Nov','Des'];
const AF_WEEKDAYS = ['Sondag','Maandag','Dinsdag','Woensdag','Donderdag','Vrydag','Saterdag'];
function prettyDate(dateStr){
  const d = new Date(dateStr + 'T00:00:00');
  return `${AF_WEEKDAYS[d.getDay()]}, ${d.getDate()} ${AF_MONTHS[d.getMonth()]} ${d.getFullYear()}`;
}
function addDays(dateStr, n){
  const d = new Date(dateStr + 'T00:00:00');
  d.setDate(d.getDate()+n);
  return formatDate(d);
}
function formatMMSS(totalSeconds){
  totalSeconds = Math.max(0, Math.round(totalSeconds));
  const m = Math.floor(totalSeconds/60);
  const s = totalSeconds % 60;
  return `${m}:${String(s).padStart(2,'0')}`;
}
function formatRand(amount){
  amount = Math.round((amount||0)*100)/100;
  return Number.isInteger(amount) ? `${amount}` : amount.toFixed(2);
}

/* ---------------- storage helpers ---------------- */
async function getJSON(key, shared=true){
  try{
    const res = await window.storage.get(key, shared);
    if(!res) return null;
    return JSON.parse(res.value);
  }catch(e){
    return null;
  }
}
async function setJSON(key, value, shared=true){
  try{
    const res = await window.storage.set(key, JSON.stringify(value), shared);
    return !!res;
  }catch(e){
    console.error('Storage set failed', key, e);
    showToast('Kon nie stoor nie \u2014 probeer asseblief weer.');
    return false;
  }
}

function emptyDayRecord(){
  return { completed:{}, bibleAnswer:'', minutesUsed:0, sessions:[], activeSessionStart:null };
}
async function loadDayRecord(date, kidId){
  const rec = await getJSON(dayKey(date,kidId));
  return rec || emptyDayRecord();
}
async function saveDayRecord(date, kidId, rec){
  await saveDayRecordInner(date, kidId, rec);
}
async function saveDayRecordInner(date, kidId, rec){
  await setJSON(dayKey(date,kidId), rec);
}

/* ---------------- toast ---------------- */
let toastTimer = null;
function showToast(msg){
  const el = document.getElementById('toast');
  el.textContent = msg;
  el.classList.add('show');
  clearTimeout(toastTimer);
  toastTimer = setTimeout(()=>el.classList.remove('show'), 2600);
}

/* ---------------- view switching ---------------- */
function showView(id){
  document.querySelectorAll('.view').forEach(v=>v.classList.add('hidden'));
  document.getElementById('loading-screen').classList.add('hidden');
  document.getElementById(id).classList.remove('hidden');
  window.scrollTo(0,0);
}

/* ---------------- balances ---------------- */
function ensureBalanceEntry(kidId){
  if(!balances[kidId]) balances[kidId] = { points:0, rand:0 };
}
function adjustBalance(task, isNowDone){
  if(!task) return;
  ensureBalanceEntry(currentKidId);
  const bal = balances[currentKidId];
  const sign = isNowDone ? 1 : -1;
  bal.points = Math.max(0, bal.points + sign*(task.points||0));
  bal.rand = Math.max(0, Math.round((bal.rand + sign*(task.rand||0))*100)/100);
  setJSON(KEY_BALANCES, balances);
}
function updatePendingBadge(){
  const pendingCount = requests.filter(q=>q.status==='pending').length;
  const badgeEl = document.getElementById('pending-badge');
  if(badgeEl) badgeEl.textContent = pendingCount > 0 ? `${pendingCount} wag` : '\u2192';
}
function updateRewardsLinkLabel(){
  ensureBalanceEntry(currentKidId);
  const bal = balances[currentKidId];
  const btn = document.getElementById('btn-open-rewards');
  if(btn) btn.innerHTML = `&#128176; Sakgeld &amp; Belonings &mdash; ${bal.points} pt &middot; R${formatRand(bal.rand)} &rarr;`;
}

/* ---------------- task helpers ---------------- */
function tasksForKid(kidId){
  return tasks.filter(t => t.active && (t.assignedTo === 'all' || t.assignedTo === kidId));
}
function getBibleTask(){
  return tasks.find(t => t.isBible);
}
function recomputeEarned(kidId, completed){
  return tasksForKid(kidId).reduce((sum,t)=>{
    return sum + (completed[t.id] ? t.minutes : 0);
  }, 0);
}
function effectiveBibleEntry(dateStr){
  if(bibleOverrides && bibleOverrides[dateStr]) return bibleOverrides[dateStr];
  return BIBLE_ROTATION[dayOfYear(dateStr) % BIBLE_ROTATION.length];
}
function effectiveAffirmation(dateStr){
  if(affirmationOverrides && affirmationOverrides[dateStr]) return affirmationOverrides[dateStr];
  return AFFIRMATION_ROTATION[dayOfYear(dateStr) % AFFIRMATION_ROTATION.length];
}
function rewardLineHtml(t){
  const parts = [];
  if(t.points) parts.push(`+${t.points} pt`);
  if(t.rand) parts.push(`R${formatRand(t.rand)}`);
  return parts.join(' &middot; ');
}

/* ===================================================================
   INIT
   =================================================================== */
async function init(){
  document.getElementById('loading-text').textContent = 'Laai julle data...';
  profiles = await getJSON(KEY_PROFILES);
  if(!profiles || !profiles.setupDone){
    renderSetup();
    showView('view-setup');
    return;
  }
  tasks = await getJSON(KEY_TASKS);
  if(!tasks){
    tasks = JSON.parse(JSON.stringify(DEFAULT_TASKS));
    await setJSON(KEY_TASKS, tasks);
  }
  bibleOverrides = await getJSON(KEY_BIBLE_OVERRIDES);
  if(!bibleOverrides) bibleOverrides = {};
  affirmationOverrides = await getJSON(KEY_AFFIRMATION_OVERRIDES);
  if(!affirmationOverrides) affirmationOverrides = {};
  deductions = await getJSON(KEY_DEDUCTIONS);
  if(!deductions) deductions = [];

  pins = await getJSON(KEY_PINS);
  parentAuth = await getJSON(KEY_PARENT_AUTH);
  balances = await getJSON(KEY_BALANCES);
  if(!balances) balances = {};
  rewards = await getJSON(KEY_REWARDS);
  if(!rewards){
    rewards = JSON.parse(JSON.stringify(DEFAULT_REWARDS));
    await setJSON(KEY_REWARDS, rewards);
  }
  requests = await getJSON(KEY_REQUESTS);
  if(!requests) requests = [];

  if(!pins || !parentAuth){
    renderSecuritySetup();
    showView('view-security-setup');
    return;
  }

  parentDateStr = todayStr();
  renderSelectScreen();
  showView('view-select');
}

/* ===================================================================
   SETUP VIEW (fresh install)
   =================================================================== */
function renderSetup(){
  const defaults = [
    {age:10, placeholder:'Naam vir jou 10-jarige'},
    {age:12, placeholder:'Naam vir jou 12-jarige'},
    {age:16, placeholder:'Naam vir jou 16-jarige'}
  ];
  const wrap = document.getElementById('setup-kid-inputs');
  wrap.innerHTML = defaults.map((d,i)=>`
    <div class="editor-row">
      <label>NAAM</label>
      <input type="text" id="setup-name-${i}" placeholder="${d.placeholder}">
      <div class="erow-2col">
        <div>
          <label>OUDERDOM</label>
          <input type="number" id="setup-age-${i}" value="${d.age}" min="1" max="25">
        </div>
        <div>
          <label>4-SYFER PIN</label>
          <input type="text" id="setup-pin-${i}" maxlength="4" inputmode="numeric" pattern="[0-9]*" placeholder="bv. 1234">
        </div>
      </div>
    </div>
  `).join('');

  document.getElementById('setup-save-btn').onclick = async () => {
    const kids = [];
    const newPins = {};
    for(let i=0;i<3;i++){
      const name = document.getElementById(`setup-name-${i}`).value.trim();
      const age = parseInt(document.getElementById(`setup-age-${i}`).value, 10) || 0;
      const pin = document.getElementById(`setup-pin-${i}`).value.trim();
      if(!name){
        showToast('Gee asseblief vir elke kind \u2019n naam.');
        return;
      }
      if(!/^\d{4}$/.test(pin)){
        showToast(`Gee \u2019n geldige 4-syfer PIN vir kind ${i+1}.`);
        return;
      }
      const id = `kid${i+1}`;
      kids.push({ id, name, age });
      newPins[id] = pin;
    }
    const pw = document.getElementById('setup-parent-pw').value.trim();
    const sq = document.getElementById('setup-parent-sq').value.trim();
    const sa = document.getElementById('setup-parent-sa').value.trim();
    if(pw.length < 4){ showToast('Die ouer-wagwoord moet ten minste 4 karakters wees.'); return; }
    if(!sq || !sa){ showToast('Vul asseblief \u2019n sekuriteitsvraag en antwoord in.'); return; }

    profiles = { kids, setupDone:true };
    tasks = JSON.parse(JSON.stringify(DEFAULT_TASKS));
    bibleOverrides = {};
    affirmationOverrides = {};
    pins = newPins;
    parentAuth = { password:pw, question:sq, answer:sa };
    balances = {};
    rewards = JSON.parse(JSON.stringify(DEFAULT_REWARDS));
    requests = [];
    deductions = [];

    await Promise.all([
      setJSON(KEY_PROFILES, profiles),
      setJSON(KEY_TASKS, tasks),
      setJSON(KEY_BIBLE_OVERRIDES, bibleOverrides),
      setJSON(KEY_AFFIRMATION_OVERRIDES, affirmationOverrides),
      setJSON(KEY_PINS, pins),
      setJSON(KEY_PARENT_AUTH, parentAuth),
      setJSON(KEY_BALANCES, balances),
      setJSON(KEY_REWARDS, rewards),
      setJSON(KEY_REQUESTS, requests),
      setJSON(KEY_DEDUCTIONS, deductions)
    ]);

    parentDateStr = todayStr();
    renderSelectScreen();
    showView('view-select');
    showToast('Alles is reg \u2014 welkom!');
  };
}

/* ===================================================================
   SECURITY-ONLY SETUP (migration for existing families)
   =================================================================== */
function renderSecuritySetup(){
  const wrap = document.getElementById('security-setup-kid-inputs');
  wrap.innerHTML = profiles.kids.map((k,i)=>`
    <div class="editor-row">
      <label>${escapeHtml(k.name)} (${k.age}) &mdash; 4-SYFER PIN</label>
      <input type="text" id="secsetup-pin-${i}" maxlength="4" inputmode="numeric" pattern="[0-9]*" placeholder="bv. 1234">
    </div>
  `).join('');

  document.getElementById('security-setup-save-btn').onclick = async () => {
    const newPins = {};
    for(let i=0;i<profiles.kids.length;i++){
      const val = document.getElementById(`secsetup-pin-${i}`).value.trim();
      if(!/^\d{4}$/.test(val)){
        showToast(`Gee \u2019n geldige 4-syfer PIN vir ${profiles.kids[i].name}.`);
        return;
      }
      newPins[profiles.kids[i].id] = val;
    }
    const pw = document.getElementById('secsetup-parent-pw').value.trim();
    const sq = document.getElementById('secsetup-parent-sq').value.trim();
    const sa = document.getElementById('secsetup-parent-sa').value.trim();
    if(pw.length < 4){ showToast('Die ouer-wagwoord moet ten minste 4 karakters wees.'); return; }
    if(!sq || !sa){ showToast('Vul asseblief \u2019n sekuriteitsvraag en antwoord in.'); return; }

    pins = newPins;
    parentAuth = { password:pw, question:sq, answer:sa };
    if(!balances) balances = {};
    if(!rewards) rewards = JSON.parse(JSON.stringify(DEFAULT_REWARDS));
    if(!requests) requests = [];

    await Promise.all([
      setJSON(KEY_PINS, pins),
      setJSON(KEY_PARENT_AUTH, parentAuth),
      setJSON(KEY_BALANCES, balances),
      setJSON(KEY_REWARDS, rewards),
      setJSON(KEY_REQUESTS, requests)
    ]);

    parentDateStr = todayStr();
    renderSelectScreen();
    showView('view-select');
    showToast('Beveiliging is gestoor!');
  };
}

/* ===================================================================
   PROFILE SELECT VIEW
   =================================================================== */
async function renderSelectScreen(){
  document.getElementById('today-date-label').textContent = prettyDate(todayStr());
  const grid = document.getElementById('profile-grid');
  grid.innerHTML = profiles.kids.map((k,i)=>`
    <button class="profile-card" data-kid="${k.id}">
      <span class="stripe" style="background:${KID_COLORS[i % KID_COLORS.length]}"></span>
      <span>
        <span class="pc-name">${escapeHtml(k.name)}</span><br>
        <span class="pc-age">${k.age} jaar oud</span>
      </span>
      <span class="pc-balance" id="pc-balance-${k.id}">&hellip;</span>
    </button>
  `).join('');

  grid.querySelectorAll('.profile-card').forEach(btn=>{
    btn.addEventListener('click', ()=> requestPin(btn.dataset.kid));
  });

  for(const k of profiles.kids){
    loadDayRecord(todayStr(), k.id).then(rec=>{
      const earned = recomputeEarned(k.id, rec.completed);
      const available = Math.max(0, earned - rec.minutesUsed);
      const el = document.getElementById(`pc-balance-${k.id}`);
      if(el) el.innerHTML = `<span class="num">${available}</span>min beskikbaar`;
    });
  }
}
document.getElementById('btn-open-parent').onclick = () => {
  document.getElementById('parent-password-input').value = '';
  document.getElementById('forgot-password-box').classList.add('hidden');
  showView('view-parent-auth');
};
function escapeHtml(s){
  return String(s).replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
}

/* ===================================================================
   PIN ENTRY (kid)
   =================================================================== */
function requestPin(kidId){
  pendingPinKidId = kidId;
  pinBuffer = '';
  const kid = profiles.kids.find(k=>k.id===kidId);
  document.getElementById('pin-kid-title').textContent = kid.name;
  renderPinKeypad();
  updatePinDots(false);
  showView('view-pin-entry');
}
function renderPinKeypad(){
  const kp = document.getElementById('pin-keypad');
  const keys = ['1','2','3','4','5','6','7','8','9','','0','back'];
  kp.innerHTML = keys.map(k=>{
    if(k === '') return `<button class="kp-empty" tabindex="-1"></button>`;
    if(k === 'back') return `<button class="kp-back" data-key="back">&larr;</button>`;
    return `<button data-key="${k}">${k}</button>`;
  }).join('');
  kp.querySelectorAll('button[data-key]').forEach(btn=>{
    btn.addEventListener('click', ()=>{
      const k = btn.dataset.key;
      if(k === 'back'){
        pinBuffer = pinBuffer.slice(0,-1);
        updatePinDots(false);
      } else if(pinBuffer.length < 4){
        pinBuffer += k;
        updatePinDots(false);
        if(pinBuffer.length === 4) setTimeout(checkPin, 180);
      }
    });
  });
}
function updatePinDots(errorState){
  const dotsEl = document.getElementById('pin-dots');
  let html = '';
  for(let i=0;i<4;i++){
    const filled = i < pinBuffer.length;
    html += `<div class="pin-dot ${filled?'filled':''} ${errorState?'error':''}"></div>`;
  }
  dotsEl.innerHTML = html;
}
function checkPin(){
  if(pins[pendingPinKidId] === pinBuffer){
    const kidId = pendingPinKidId;
    pendingPinKidId = null;
    pinBuffer = '';
    openKidView(kidId);
  } else {
    updatePinDots(true);
    showToast('Verkeerde PIN, probeer weer.');
    setTimeout(()=>{ pinBuffer=''; updatePinDots(false); }, 500);
  }
}
document.getElementById('btn-back-from-pin').onclick = () => {
  pendingPinKidId = null;
  pinBuffer = '';
  renderSelectScreen();
  showView('view-select');
};

/* ===================================================================
   PARENT PASSWORD GATE
   =================================================================== */
document.getElementById('btn-parent-auth-submit').onclick = () => {
  const val = document.getElementById('parent-password-input').value;
  if(parentAuth && val === parentAuth.password){
    openParentView();
  } else {
    showToast('Verkeerde wagwoord.');
  }
};
document.getElementById('parent-password-input').addEventListener('keyup', (e)=>{
  if(e.key === 'Enter') document.getElementById('btn-parent-auth-submit').click();
});
document.getElementById('btn-forgot-password').onclick = () => {
  document.getElementById('security-question-display').textContent = parentAuth.question;
  document.getElementById('security-answer-input').value = '';
  document.getElementById('forgot-password-box').classList.remove('hidden');
};
document.getElementById('btn-verify-security-answer').onclick = () => {
  const val = document.getElementById('security-answer-input').value.trim().toLowerCase();
  if(parentAuth && val === parentAuth.answer.trim().toLowerCase()){
    showToast('Korrek! Dalk wil jy jou wagwoord opdateer onder Kinders & wagwoorde.');
    openParentView();
  } else {
    showToast('Nie heeltemal reg nie, probeer weer.');
  }
};
document.getElementById('btn-back-from-parent-auth').onclick = () => {
  renderSelectScreen();
  showView('view-select');
};

/* ===================================================================
   KID VIEW
   =================================================================== */
async function openKidView(kidId){
  currentKidId = kidId;
  const kid = profiles.kids.find(k=>k.id===kidId);
  document.getElementById('kid-title').textContent = `${kid.name} (${kid.age})`;
  showView('view-kid');
  document.getElementById('bank-readout').textContent = '\u2026';
  document.getElementById('task-list').innerHTML = '<p style="color:var(--ink-soft);font-size:13px;">Laai take...</p>';

  ensureBalanceEntry(kidId);
  currentDayRecord = await loadDayRecord(todayStr(), kidId);
  renderAffirmationCard();
  renderBibleCard();
  renderTaskList();
  renderBankCard();
  updateRewardsLinkLabel();

  if(currentDayRecord.activeSessionStart){
    startTickInterval();
  }
}

function renderAffirmationCard(){
  const a = effectiveAffirmation(todayStr());
  document.getElementById('affirmation-text').textContent = `\u201c${a.text}\u201d`;
  document.getElementById('affirmation-ref').textContent = a.ref;
}

function renderBibleCard(){
  const entry = effectiveBibleEntry(todayStr());
  const bTask = getBibleTask();
  document.getElementById('bible-ref-text').textContent = entry.ref;
  document.getElementById('bible-question-text').textContent = entry.q || '';
  document.getElementById('bible-amount-min').textContent = bTask ? `+${bTask.minutes} min` : '';
  document.getElementById('bible-amount-extra').innerHTML = bTask ? rewardLineHtml(bTask) : '';
  const checkbox = document.getElementById('bible-checkbox');
  const row = document.getElementById('bible-row');
  const isDone = !!(bTask && currentDayRecord.completed[bTask.id]);
  checkbox.checked = isDone;
  row.classList.toggle('done', isDone);
  document.getElementById('bible-answer').value = currentDayRecord.bibleAnswer || '';

  const toggleBible = () => {
    if(!bTask) return;
    const newVal = !currentDayRecord.completed[bTask.id];
    currentDayRecord.completed[bTask.id] = newVal;
    checkbox.checked = newVal;
    row.classList.toggle('done', newVal);
    if(newVal) triggerStamp(document.getElementById('bible-stamp'));
    adjustBalance(bTask, newVal);
    saveDayRecord(todayStr(), currentKidId, currentDayRecord);
    renderBankCard();
    updateRewardsLinkLabel();
  };
  checkbox.addEventListener('click', (e)=>{ e.stopPropagation(); toggleBible(); });
  row.addEventListener('click', (e)=>{
    if(e.target.tagName.toLowerCase() === 'input') return;
    toggleBible();
  });
  document.getElementById('bible-answer').onblur = (e) => {
    currentDayRecord.bibleAnswer = e.target.value;
    saveDayRecord(todayStr(), currentKidId, currentDayRecord);
  };
}

function triggerStamp(el){
  el.classList.remove('show');
  void el.offsetWidth;
  el.classList.add('show');
}

function renderTaskList(){
  const list = tasksForKid(currentKidId).filter(t => !t.isBible);
  const container = document.getElementById('task-list');
  if(list.length === 0){
    container.innerHTML = '<p style="color:var(--ink-soft);font-size:13px;">Geen take is vir jou ingestel nie. Vra jou ouer om \u2019n taak by te voeg.</p>';
    return;
  }
  container.innerHTML = list.map(t=>{
    const done = !!currentDayRecord.completed[t.id];
    return `
      <div class="ledger-row ${done?'done':''}" data-task="${t.id}">
        <input type="checkbox" ${done?'checked':''} data-task-checkbox="${t.id}">
        <span class="task-name">${escapeHtml(t.name)}</span>
        <span class="ledger-amount la-stack">
          <span class="la-min">+${t.minutes} min</span>
          <span class="la-extra">${rewardLineHtml(t)}</span>
        </span>
        <span class="stamp" data-stamp="${t.id}">GEDOEN</span>
      </div>
    `;
  }).join('');

  container.querySelectorAll('.ledger-row').forEach(row=>{
    const id = row.dataset.task;
    const task = list.find(x=>x.id===id);
    const checkbox = row.querySelector('input[type="checkbox"]');
    const toggle = () => {
      const newVal = !currentDayRecord.completed[id];
      currentDayRecord.completed[id] = newVal;
      checkbox.checked = newVal;
      row.classList.toggle('done', newVal);
      if(newVal) triggerStamp(row.querySelector('.stamp'));
      adjustBalance(task, newVal);
      saveDayRecord(todayStr(), currentKidId, currentDayRecord);
      renderBankCard();
      updateRewardsLinkLabel();
    };
    checkbox.addEventListener('click', (e)=>{ e.stopPropagation(); toggle(); });
    row.addEventListener('click', (e)=>{
      if(e.target.tagName.toLowerCase() === 'input') return;
      toggle();
    });
  });
}

function currentEarnedMinutes(){
  return recomputeEarned(currentKidId, currentDayRecord.completed);
}
function currentAvailableMinutes(){
  return Math.max(0, currentEarnedMinutes() - currentDayRecord.minutesUsed);
}

function renderBankCard(){
  const readout = document.getElementById('bank-readout');
  const sub = document.getElementById('bank-sub');
  const btn = document.getElementById('btn-toggle-timer');
  const available = currentAvailableMinutes();

  if(currentDayRecord.activeSessionStart){
    readout.classList.add('running');
    sub.textContent = 'tans aan die loop \u2014 tik om te stop';
    btn.textContent = 'Stop Skermtyd';
    btn.classList.add('stop');
    btn.disabled = false;
  } else {
    readout.classList.remove('running');
    readout.textContent = `${available} min`;
    sub.textContent = 'minute beskikbaar vandag';
    btn.textContent = 'Begin Skermtyd';
    btn.classList.remove('stop');
    btn.disabled = available <= 0;
  }
  renderSessionLog();
  btn.onclick = onToggleTimer;
}

function renderSessionLog(){
  const log = document.getElementById('session-log');
  const sessions = currentDayRecord.sessions || [];
  if(sessions.length === 0){
    log.innerHTML = '<div class="s-empty">Nog geen skermtyd vandag gebruik nie.</div>';
    return;
  }
  log.innerHTML = sessions.map(s=>{
    const start = new Date(s.start);
    const hh = String(start.getHours()).padStart(2,'0');
    const mm = String(start.getMinutes()).padStart(2,'0');
    return `<div class="s-row"><span>${hh}:${mm}</span><span>${s.minutes} min</span></div>`;
  }).join('');
}

function onToggleTimer(){
  if(currentDayRecord.activeSessionStart){
    stopSession(false);
  } else {
    if(currentAvailableMinutes() <= 0){
      showToast('Geen minute beskikbaar nie \u2014 voltooi eers \u2019n taak!');
      return;
    }
    currentDayRecord.activeSessionStart = Date.now();
    saveDayRecord(todayStr(), currentKidId, currentDayRecord);
    startTickInterval();
    renderBankCard();
  }
}

function startTickInterval(){
  clearInterval(timerInterval);
  tick();
  timerInterval = setInterval(tick, 1000);
}

function tick(){
  if(!currentDayRecord.activeSessionStart){
    clearInterval(timerInterval);
    return;
  }
  const elapsedSec = Math.floor((Date.now() - currentDayRecord.activeSessionStart)/1000);
  const earned = currentEarnedMinutes();
  const totalAllowedSec = Math.max(0, (earned - currentDayRecord.minutesUsed) * 60);
  const remainingSec = totalAllowedSec - elapsedSec;
  const readout = document.getElementById('bank-readout');
  if(!readout) { clearInterval(timerInterval); return; }
  if(remainingSec <= 0){
    stopSession(true);
    return;
  }
  readout.textContent = formatMMSS(remainingSec);
}

function stopSession(autoStopped){
  clearInterval(timerInterval);
  timerInterval = null;
  const start = currentDayRecord.activeSessionStart;
  const elapsedSec = Math.max(0, Math.floor((Date.now() - start)/1000));
  const usedMin = Math.max(0, Math.round(elapsedSec/60));
  currentDayRecord.minutesUsed += usedMin;
  if(usedMin > 0){
    currentDayRecord.sessions.push({ start, end:Date.now(), minutes:usedMin });
  }
  currentDayRecord.activeSessionStart = null;
  saveDayRecord(todayStr(), currentKidId, currentDayRecord);
  renderBankCard();
  if(autoStopped) showToast('Skermtyd is op vir vandag \u2014 mooi werk!');
}

document.getElementById('btn-back-from-kid').onclick = () => {
  clearInterval(timerInterval);
  timerInterval = null;
  renderSelectScreen();
  showView('view-select');
};

/* ===================================================================
   REWARDS / SAKGELD (kid)
   =================================================================== */
document.getElementById('btn-open-rewards').onclick = () => {
  const kid = profiles.kids.find(k=>k.id===currentKidId);
  document.getElementById('rewards-kid-title').textContent = kid ? kid.name : '';
  renderRewardsView();
  showView('view-rewards');
};
document.getElementById('btn-back-from-rewards').onclick = () => {
  showView('view-kid');
};

function renderRewardsView(){
  ensureBalanceEntry(currentKidId);
  const bal = balances[currentKidId];
  document.getElementById('rewards-points-num').textContent = bal.points;
  document.getElementById('rewards-rand-num').textContent = `R${formatRand(bal.rand)}`;

  const activeRewards = rewards.filter(r=>r.active);
  const list = document.getElementById('rewards-list');
  if(activeRewards.length === 0){
    list.innerHTML = '<p style="font-size:13px;color:var(--ink-soft);">Nog geen belonings ingestel nie.</p>';
  } else {
    list.innerHTML = activeRewards.map(r=>{
      const affordable = bal.points >= r.pointsCost;
      const hasPending = requests.some(q=>q.kidId===currentKidId && q.type==='reward' && q.rewardId===r.id && q.status==='pending');
      return `<div class="reward-row">
        <span class="rw-name">${escapeHtml(r.name)}</span>
        <span class="rw-cost">${r.pointsCost} pt</span>
        <button data-reward="${r.id}" ${(!affordable || hasPending) ? 'disabled' : ''}>${hasPending ? 'Wag...' : 'Versoek'}</button>
      </div>`;
    }).join('');
    list.querySelectorAll('[data-reward]').forEach(btn=>{
      btn.addEventListener('click', async ()=>{
        const r = rewards.find(x=>x.id===btn.dataset.reward);
        if(!r) return;
        requests.push({
          id:'req_'+Date.now(), kidId:currentKidId, type:'reward',
          rewardId:r.id, rewardName:r.name, pointsCost:r.pointsCost,
          status:'pending', createdAt:Date.now()
        });
        await setJSON(KEY_REQUESTS, requests);
        showToast('Versoek gestuur! Wag vir goedkeuring.');
        renderRewardsView();
      });
    });
  }

  const hasPendingPayout = requests.some(q=>q.kidId===currentKidId && q.type==='payout' && q.status==='pending');
  const payoutBtn = document.getElementById('btn-request-payout');
  payoutBtn.disabled = bal.rand <= 0 || hasPendingPayout;
  payoutBtn.textContent = hasPendingPayout ? 'Wag...' : 'Vra';

  renderMyRequests();
  renderMyDeductions();
}

document.getElementById('btn-request-payout').onclick = async () => {
  const input = document.getElementById('payout-amount-input');
  const amount = Math.round((parseFloat(input.value) || 0) * 100) / 100;
  ensureBalanceEntry(currentKidId);
  const bal = balances[currentKidId];
  const hasPendingPayout = requests.some(q=>q.kidId===currentKidId && q.type==='payout' && q.status==='pending');
  if(hasPendingPayout){ showToast('Jy het al \u2019n versoek wat wag.'); return; }
  if(!amount || amount <= 0){ showToast('Gee \u2019n geldige bedrag.'); return; }
  if(amount > bal.rand){ showToast('Jy het nie genoeg sakgeld nie.'); return; }
  requests.push({
    id:'req_'+Date.now(), kidId:currentKidId, type:'payout',
    amount, status:'pending', createdAt:Date.now()
  });
  await setJSON(KEY_REQUESTS, requests);
  input.value = '';
  showToast('Versoek vir sakgeld is gestuur!');
  renderRewardsView();
};

function renderMyRequests(){
  const list = document.getElementById('my-requests-list');
  const mine = requests.filter(q=>q.kidId===currentKidId).sort((a,b)=>b.createdAt-a.createdAt).slice(0,8);
  if(mine.length === 0){
    list.innerHTML = '<p style="font-size:13px;color:var(--ink-soft);font-style:italic;">Nog geen versoeke nie.</p>';
    return;
  }
  list.innerHTML = mine.map(q=>{
    const label = q.type === 'reward' ? q.rewardName : `Sakgeld: R${formatRand(q.amount)}`;
    const badgeText = q.status === 'pending' ? 'Wag' : (q.status === 'approved' ? 'Goedgekeur' : 'Afgekeur');
    return `<div class="mr-row"><span>${escapeHtml(label)}</span><span class="badge ${q.status}">${badgeText}</span></div>`;
  }).join('');
}
function renderMyDeductions(){
  const list = document.getElementById('my-deductions-list');
  const mine = deductions.filter(d=>d.kidId===currentKidId).sort((a,b)=>b.createdAt-a.createdAt).slice(0,5);
  if(mine.length === 0){
    list.innerHTML = '<p style="font-size:13px;color:var(--ink-soft);font-style:italic;">Nog geen aanpassings nie.</p>';
    return;
  }
  list.innerHTML = mine.map(d=>{
    const parts = [];
    if(d.minutes) parts.push(`-${d.minutes} min`);
    if(d.points) parts.push(`-${d.points} pt`);
    if(d.rand) parts.push(`-R${formatRand(d.rand)}`);
    return `<div class="mr-row"><span>${escapeHtml(d.reason || 'Geen rede gegee')}</span><span style="font-family:var(--font-mono);font-size:11.5px;color:var(--clay-deep);">${parts.join(' &middot; ')}</span></div>`;
  }).join('');
}

/* ===================================================================
   PARENT DASHBOARD
   =================================================================== */
function openParentView(){
  parentDateStr = todayStr();
  document.getElementById('date-picker').value = parentDateStr;
  renderParentSummary();
  showView('view-parent');
}
document.getElementById('btn-back-from-parent').onclick = () => {
  renderSelectScreen();
  showView('view-select');
};
document.getElementById('date-picker').onchange = (e) => {
  parentDateStr = e.target.value;
  renderParentSummary();
};
document.getElementById('date-prev').onclick = () => {
  parentDateStr = addDays(parentDateStr, -1);
  document.getElementById('date-picker').value = parentDateStr;
  renderParentSummary();
};
document.getElementById('date-next').onclick = () => {
  parentDateStr = addDays(parentDateStr, 1);
  document.getElementById('date-picker').value = parentDateStr;
  renderParentSummary();
};

async function renderParentSummary(){
  const container = document.getElementById('parent-summary');
  container.innerHTML = `<p style="color:var(--muted);font-size:13px;">Laai ${prettyDate(parentDateStr)}...</p>`;

  updatePendingBadge();

  const blocks = [];
  for(let i=0;i<profiles.kids.length;i++){
    const kid = profiles.kids[i];
    const rec = await loadDayRecord(parentDateStr, kid.id);
    const list = tasksForKid(kid.id);
    const earned = recomputeEarned(kid.id, rec.completed);
    const available = Math.max(0, earned - rec.minutesUsed);
    const doneCount = list.filter(t=>rec.completed[t.id]).length;
    ensureBalanceEntry(kid.id);
    const bal = balances[kid.id];
    const kidPendingCount = requests.filter(q=>q.kidId===kid.id && q.status==='pending').length;

    const rows = list.map(t=>{
      const isDone = !!rec.completed[t.id];
      const label = t.isBible ? `${t.name} (${effectiveBibleEntry(parentDateStr).ref})` : t.name;
      return `
        <div class="ks-task-row">
          <span class="ks-dot ${isDone?'on':'off'}"></span>
          <span class="ks-tname ${isDone?'':'off'}" style="flex:1;">${escapeHtml(label)}</span>
          <span style="font-family:var(--font-mono);font-size:12px;color:var(--ink-soft);">${isDone? '+'+t.minutes+'m' : '\u2014'}</span>
        </div>`;
    }).join('');

    const bibleAnswerBlock = rec.bibleAnswer ? `<div class="ks-bible-answer">\u201c${escapeHtml(rec.bibleAnswer)}\u201d</div>` : '';
    const liveTag = rec.activeSessionStart ? `<span class="ks-live">\u25cf besig met skermtyd</span>` : '';

    blocks.push(`
      <div class="card kid-summary">
        <div class="kid-summary-head">
          <span class="ks-name">${escapeHtml(kid.name)}${liveTag}</span>
          <span class="ks-stats">${doneCount}/${list.length} take &middot; ${available} min oor</span>
        </div>
        <div class="ks-balance-row">
          <span>&#128142; ${bal.points} pt &middot; R${formatRand(bal.rand)} sakgeld</span>
          ${kidPendingCount > 0 ? `<span class="ks-pending">${kidPendingCount} versoek${kidPendingCount>1?'e':''} wag</span>` : ''}
        </div>
        ${rows}
        ${bibleAnswerBlock}
        <div class="ks-actions-row">
          <button class="ks-deduct" data-deduct-kid="${kid.id}">Trek tyd / sakgeld af</button>
          <button class="ks-reset" data-reset-kid="${kid.id}">Herstel hierdie dag</button>
        </div>
      </div>
    `);
  }
  container.innerHTML = blocks.join('');

  container.querySelectorAll('[data-deduct-kid]').forEach(btn=>{
    btn.addEventListener('click', () => openDeductView(btn.dataset.deductKid));
  });
  container.querySelectorAll('[data-reset-kid]').forEach(btn=>{
    btn.addEventListener('click', async () => {
      const kidId = btn.dataset.resetKid;
      const kid = profiles.kids.find(k=>k.id===kidId);
      if(confirm(`Is jy seker jy wil ${kid.name} se data vir ${prettyDate(parentDateStr)} uitvee?`)){
        await saveDayRecord(parentDateStr, kidId, emptyDayRecord());
        renderParentSummary();
        showToast('Dag is herstel.');
      }
    });
  });
}

document.getElementById('btn-manage-tasks').onclick = () => { renderManageTasks(); showView('view-manage-tasks'); };
document.getElementById('btn-manage-bible').onclick = () => { renderManageBible(); showView('view-manage-bible'); };
document.getElementById('btn-manage-affirmations').onclick = () => { renderManageAffirmations(); showView('view-manage-affirmations'); };
document.getElementById('btn-manage-kids').onclick = () => { renderManageKids(); showView('view-manage-kids'); };
document.getElementById('btn-requests').onclick = () => { renderRequestsView(); showView('view-requests'); };
document.getElementById('btn-manage-rewards').onclick = () => { renderManageRewards(); showView('view-manage-rewards'); };
document.getElementById('btn-back-from-tasks').onclick = () => { showView('view-parent'); };
document.getElementById('btn-back-from-bible').onclick = () => { showView('view-parent'); };
document.getElementById('btn-back-from-affirmations').onclick = () => { showView('view-parent'); };
document.getElementById('btn-back-from-kids').onclick = () => { showView('view-parent'); };
document.getElementById('btn-back-from-requests').onclick = () => { showView('view-parent'); };
document.getElementById('btn-back-from-rewards-manage').onclick = () => { showView('view-parent'); };

/* ===================================================================
   REQUESTS (parent: approve / decline)
   =================================================================== */
function renderRequestsView(){
  const pendingList = requests.filter(q=>q.status==='pending').sort((a,b)=>a.createdAt-b.createdAt);
  const pendingContainer = document.getElementById('pending-requests-list');
  if(pendingList.length === 0){
    pendingContainer.innerHTML = '<p style="font-size:13px;color:var(--ink-soft);">Geen oop versoeke nie.</p>';
  } else {
    pendingContainer.innerHTML = pendingList.map(q=>{
      const kid = profiles.kids.find(k=>k.id===q.kidId);
      const detail = q.type === 'reward' ? `${q.rewardName} (${q.pointsCost} pt)` : `Sakgeld: R${formatRand(q.amount)}`;
      return `<div class="req-row">
        <div class="req-info"><div class="ri-kid">${escapeHtml(kid?kid.name:'?')}</div><div class="ri-detail">${escapeHtml(detail)}</div></div>
        <div class="req-actions">
          <button class="req-approve" data-approve="${q.id}">Goedkeur</button>
          <button class="req-decline" data-decline="${q.id}">Wegwys</button>
        </div>
      </div>`;
    }).join('');
    pendingContainer.querySelectorAll('[data-approve]').forEach(btn=>{
      btn.addEventListener('click', ()=>resolveRequest(btn.dataset.approve, 'approved'));
    });
    pendingContainer.querySelectorAll('[data-decline]').forEach(btn=>{
      btn.addEventListener('click', ()=>resolveRequest(btn.dataset.decline, 'declined'));
    });
  }

  const resolvedList = requests.filter(q=>q.status!=='pending').sort((a,b)=>b.createdAt-a.createdAt).slice(0,10);
  const resolvedContainer = document.getElementById('resolved-requests-list');
  if(resolvedList.length === 0){
    resolvedContainer.innerHTML = '<p style="font-size:13px;color:var(--ink-soft);">Nog geen besluite nie.</p>';
  } else {
    resolvedContainer.innerHTML = resolvedList.map(q=>{
      const kid = profiles.kids.find(k=>k.id===q.kidId);
      const detail = q.type === 'reward' ? q.rewardName : `Sakgeld: R${formatRand(q.amount)}`;
      const badgeText = q.status === 'approved' ? 'Goedgekeur' : 'Afgekeur';
      return `<div class="req-row"><div class="req-info"><div class="ri-kid">${escapeHtml(kid?kid.name:'?')}</div><div class="ri-detail">${escapeHtml(detail)}</div></div><span class="badge ${q.status}">${badgeText}</span></div>`;
    }).join('');
  }
}

async function resolveRequest(id, newStatus){
  const q = requests.find(x=>x.id===id);
  if(!q) return;
  q.status = newStatus;
  q.resolvedAt = Date.now();
  if(newStatus === 'approved'){
    ensureBalanceEntry(q.kidId);
    if(q.type === 'reward'){
      balances[q.kidId].points = Math.max(0, balances[q.kidId].points - q.pointsCost);
    } else if(q.type === 'payout'){
      balances[q.kidId].rand = Math.max(0, Math.round((balances[q.kidId].rand - q.amount)*100)/100);
    }
    await setJSON(KEY_BALANCES, balances);
  }
  await setJSON(KEY_REQUESTS, requests);
  renderRequestsView();
  updatePendingBadge();
  showToast(newStatus === 'approved' ? 'Goedgekeur!' : 'Versoek afgekeur.');
}

/* ===================================================================
   MANAGE REWARDS
   =================================================================== */
function renderManageRewards(){
  const container = document.getElementById('rewards-editor-list');
  container.innerHTML = rewards.map((r)=>`
    <div class="editor-row" data-id="${r.id}">
      <label>BELONING</label>
      <input type="text" class="r-name" value="${escapeHtml(r.name)}">
      <label>PUNTE NODIG</label>
      <input type="number" class="r-cost" value="${r.pointsCost}" min="1">
      <div class="erow-bottom">
        <label class="erow-active"><input type="checkbox" class="r-active" ${r.active?'checked':''}> Aktief</label>
        <button class="erow-delete" data-delete>Verwyder</button>
      </div>
    </div>
  `).join('');
  container.querySelectorAll('[data-delete]').forEach(btn=>{
    btn.addEventListener('click', () => btn.closest('.editor-row').remove());
  });
}
document.getElementById('btn-add-reward').onclick = () => {
  const container = document.getElementById('rewards-editor-list');
  const newId = 'reward_' + Date.now();
  const div = document.createElement('div');
  div.className = 'editor-row';
  div.dataset.id = newId;
  div.innerHTML = `
    <label>BELONING</label>
    <input type="text" class="r-name" value="" placeholder="Nuwe beloning">
    <label>PUNTE NODIG</label>
    <input type="number" class="r-cost" value="20" min="1">
    <div class="erow-bottom">
      <label class="erow-active"><input type="checkbox" class="r-active" checked> Aktief</label>
      <button class="erow-delete">Verwyder</button>
    </div>
  `;
  div.querySelector('.erow-delete').addEventListener('click', ()=>div.remove());
  container.appendChild(div);
};
document.getElementById('btn-save-rewards').onclick = async () => {
  const rows = document.querySelectorAll('#rewards-editor-list .editor-row');
  const newRewards = [];
  rows.forEach(row=>{
    const id = row.dataset.id;
    const name = row.querySelector('.r-name').value.trim() || 'Beloning';
    const pointsCost = parseInt(row.querySelector('.r-cost').value, 10) || 1;
    const active = row.querySelector('.r-active').checked;
    newRewards.push({ id, name, pointsCost, active });
  });
  rewards = newRewards;
  await setJSON(KEY_REWARDS, rewards);
  showToast('Belonings is gestoor.');
};

/* ===================================================================
   MANAGE TASKS
   =================================================================== */
function kidOptionsHtml(selected){
  let opts = `<option value="all" ${selected==='all'?'selected':''}>Almal</option>`;
  profiles.kids.forEach(k=>{
    opts += `<option value="${k.id}" ${selected===k.id?'selected':''}>${escapeHtml(k.name)}</option>`;
  });
  return opts;
}
function renderManageTasks(){
  const container = document.getElementById('tasks-editor-list');
  container.innerHTML = tasks.map((t, idx)=>`
    <div class="editor-row" data-idx="${idx}" data-id="${t.id}">
      ${t.isBible ? '<div class="erow-bible-tag">\u2693 Bybelstudie-taak (skakel met Bybel-bladsy)</div>' : ''}
      <label>TAAKNAAM</label>
      <input type="text" class="t-name" value="${escapeHtml(t.name)}">
      <div class="erow-3col">
        <div>
          <label>MINUTE</label>
          <input type="number" class="t-minutes" value="${t.minutes}" min="0">
        </div>
        <div>
          <label>PUNTE</label>
          <input type="number" class="t-points" value="${t.points||0}" min="0">
        </div>
        <div>
          <label>SAKGELD (R)</label>
          <input type="number" class="t-rand" value="${t.rand||0}" min="0" step="0.50">
        </div>
      </div>
      <label>VIR WIE</label>
      <select class="t-assigned">${kidOptionsHtml(t.assignedTo)}</select>
      <div class="erow-bottom">
        <label class="erow-active"><input type="checkbox" class="t-active" ${t.active?'checked':''}> Aktief</label>
        ${t.isBible ? '' : '<button class="erow-delete" data-delete="'+idx+'">Verwyder</button>'}
      </div>
    </div>
  `).join('');

  container.querySelectorAll('[data-delete]').forEach(btn=>{
    btn.addEventListener('click', () => {
      btn.closest('.editor-row').remove();
    });
  });
}
document.getElementById('btn-add-task').onclick = () => {
  const container = document.getElementById('tasks-editor-list');
  const newId = 'task_' + Date.now();
  const div = document.createElement('div');
  div.className = 'editor-row';
  div.dataset.id = newId;
  div.innerHTML = `
    <label>TAAKNAAM</label>
    <input type="text" class="t-name" value="" placeholder="Nuwe taak">
    <div class="erow-3col">
      <div>
        <label>MINUTE</label>
        <input type="number" class="t-minutes" value="10" min="0">
      </div>
      <div>
        <label>PUNTE</label>
        <input type="number" class="t-points" value="5" min="0">
      </div>
      <div>
        <label>SAKGELD (R)</label>
        <input type="number" class="t-rand" value="1" min="0" step="0.50">
      </div>
    </div>
    <label>VIR WIE</label>
    <select class="t-assigned">${kidOptionsHtml('all')}</select>
    <div class="erow-bottom">
      <label class="erow-active"><input type="checkbox" class="t-active" checked> Aktief</label>
      <button class="erow-delete">Verwyder</button>
    </div>
  `;
  div.querySelector('.erow-delete').addEventListener('click', ()=>div.remove());
  container.appendChild(div);
};
document.getElementById('btn-save-tasks').onclick = async () => {
  const rows = document.querySelectorAll('#tasks-editor-list .editor-row');
  const newTasks = [];
  rows.forEach(row=>{
    const id = row.dataset.id;
    const name = row.querySelector('.t-name').value.trim() || 'Taak';
    const minutes = parseInt(row.querySelector('.t-minutes').value, 10) || 0;
    const points = parseInt(row.querySelector('.t-points').value, 10) || 0;
    const rand = parseFloat(row.querySelector('.t-rand').value) || 0;
    const assignedTo = row.querySelector('.t-assigned').value;
    const active = row.querySelector('.t-active').checked;
    const existing = tasks.find(t=>t.id===id);
    newTasks.push({ id, name, minutes, points, rand, assignedTo, active, isBible: existing ? !!existing.isBible : false });
  });
  tasks = newTasks;
  await setJSON(KEY_TASKS, tasks);
  showToast('Take is gestoor.');
};

/* ===================================================================
   MANAGE BIBLE
   =================================================================== */
function loadBibleDateIntoForm(dateStr){
  const entry = effectiveBibleEntry(dateStr);
  document.getElementById('bible-ref-input').value = entry.ref;
  document.getElementById('bible-q-input').value = entry.q || '';
}
function renderManageBible(){
  const picker = document.getElementById('bible-date-picker');
  picker.value = todayStr();
  loadBibleDateIntoForm(picker.value);
  renderBibleRotationPreview();
}
document.getElementById('bible-date-picker').onchange = (e) => {
  loadBibleDateIntoForm(e.target.value);
};
document.getElementById('btn-save-bible-override').onclick = async () => {
  const dateStr = document.getElementById('bible-date-picker').value;
  const ref = document.getElementById('bible-ref-input').value.trim();
  const q = document.getElementById('bible-q-input').value.trim();
  if(!ref){ showToast('Gee asseblief \u2019n skrifverwysing.'); return; }
  bibleOverrides[dateStr] = { ref, q };
  await setJSON(KEY_BIBLE_OVERRIDES, bibleOverrides);
  showToast(`Bybelgedeelte gestoor vir ${prettyDate(dateStr)}.`);
  renderBibleRotationPreview();
};
document.getElementById('btn-reset-bible-override').onclick = async () => {
  const dateStr = document.getElementById('bible-date-picker').value;
  delete bibleOverrides[dateStr];
  await setJSON(KEY_BIBLE_OVERRIDES, bibleOverrides);
  loadBibleDateIntoForm(dateStr);
  showToast('Terug na outomatiese rotasie.');
  renderBibleRotationPreview();
};
function renderBibleRotationPreview(){
  const list = document.getElementById('bible-rotation-list');
  let html = '';
  for(let i=0;i<7;i++){
    const d = addDays(todayStr(), i);
    const entry = effectiveBibleEntry(d);
    html += `<div class="rp-row"><span>${prettyDate(d).split(',')[0]} ${d.slice(8,10)}/${d.slice(5,7)}</span><span>${escapeHtml(entry.ref)}</span></div>`;
  }
  list.innerHTML = html;
}

/* ===================================================================
   MANAGE AFFIRMATIONS
   =================================================================== */
function loadAffirmationDateIntoForm(dateStr){
  const entry = effectiveAffirmation(dateStr);
  document.getElementById('affirmation-text-input').value = entry.text;
  document.getElementById('affirmation-ref-input').value = entry.ref || '';
}
function renderManageAffirmations(){
  const picker = document.getElementById('affirmation-date-picker');
  picker.value = todayStr();
  loadAffirmationDateIntoForm(picker.value);
  renderAffirmationRotationPreview();
}
document.getElementById('affirmation-date-picker').onchange = (e) => {
  loadAffirmationDateIntoForm(e.target.value);
};
document.getElementById('btn-save-affirmation-override').onclick = async () => {
  const dateStr = document.getElementById('affirmation-date-picker').value;
  const text = document.getElementById('affirmation-text-input').value.trim();
  const ref = document.getElementById('affirmation-ref-input').value.trim();
  if(!text){ showToast('Gee asseblief \u2019n bevestiging.'); return; }
  affirmationOverrides[dateStr] = { text, ref };
  await setJSON(KEY_AFFIRMATION_OVERRIDES, affirmationOverrides);
  showToast(`Bevestiging gestoor vir ${prettyDate(dateStr)}.`);
  renderAffirmationRotationPreview();
};
document.getElementById('btn-reset-affirmation-override').onclick = async () => {
  const dateStr = document.getElementById('affirmation-date-picker').value;
  delete affirmationOverrides[dateStr];
  await setJSON(KEY_AFFIRMATION_OVERRIDES, affirmationOverrides);
  loadAffirmationDateIntoForm(dateStr);
  showToast('Terug na outomatiese rotasie.');
  renderAffirmationRotationPreview();
};
function renderAffirmationRotationPreview(){
  const list = document.getElementById('affirmation-rotation-list');
  let html = '';
  for(let i=0;i<7;i++){
    const d = addDays(todayStr(), i);
    const entry = effectiveAffirmation(d);
    html += `<div class="rp-row"><span>${prettyDate(d).split(',')[0]} ${d.slice(8,10)}/${d.slice(5,7)}</span><span>${escapeHtml(entry.text)}</span></div>`;
  }
  list.innerHTML = html;
}

/* ===================================================================
   DEDUCT (parent consequence)
   =================================================================== */
function openDeductView(kidId){
  deductTargetKidId = kidId;
  const kid = profiles.kids.find(k=>k.id===kidId);
  document.getElementById('deduct-title').textContent = `Trek af: ${kid ? kid.name : ''}`;
  document.getElementById('deduct-minutes').value = 0;
  document.getElementById('deduct-points').value = 0;
  document.getElementById('deduct-rand').value = 0;
  document.getElementById('deduct-reason').value = '';
  renderDeductHistory();
  showView('view-deduct');
}
function renderDeductHistory(){
  const list = document.getElementById('deduct-history-list');
  const mine = deductions.filter(d=>d.kidId===deductTargetKidId).sort((a,b)=>b.createdAt-a.createdAt).slice(0,8);
  if(mine.length === 0){
    list.innerHTML = '<p style="font-size:13px;color:var(--ink-soft);font-style:italic;">Nog geen aanpassings nie.</p>';
    return;
  }
  list.innerHTML = mine.map(d=>{
    const parts = [];
    if(d.minutes) parts.push(`-${d.minutes} min`);
    if(d.points) parts.push(`-${d.points} pt`);
    if(d.rand) parts.push(`-R${formatRand(d.rand)}`);
    return `<div class="mr-row"><span>${prettyDate(d.date).split(',')[0]}: ${escapeHtml(d.reason || 'Geen rede gegee')}</span><span style="font-family:var(--font-mono);font-size:11.5px;color:var(--clay-deep);">${parts.join(' &middot; ')}</span></div>`;
  }).join('');
}
document.getElementById('btn-confirm-deduct').onclick = async () => {
  const minutes = Math.max(0, parseInt(document.getElementById('deduct-minutes').value, 10) || 0);
  const points = Math.max(0, parseInt(document.getElementById('deduct-points').value, 10) || 0);
  const rand = Math.max(0, parseFloat(document.getElementById('deduct-rand').value) || 0);
  const reason = document.getElementById('deduct-reason').value.trim();
  if(minutes <= 0 && points <= 0 && rand <= 0){
    showToast('Gee \u2019n bedrag om af te trek.');
    return;
  }
  if(minutes > 0){
    const rec = await loadDayRecord(parentDateStr, deductTargetKidId);
    rec.minutesUsed += minutes;
    await saveDayRecord(parentDateStr, deductTargetKidId, rec);
  }
  if(points > 0 || rand > 0){
    ensureBalanceEntry(deductTargetKidId);
    balances[deductTargetKidId].points = Math.max(0, balances[deductTargetKidId].points - points);
    balances[deductTargetKidId].rand = Math.max(0, Math.round((balances[deductTargetKidId].rand - rand) * 100) / 100);
    await setJSON(KEY_BALANCES, balances);
  }
  deductions.push({
    id:'ded_' + Date.now(), kidId:deductTargetKidId, date:parentDateStr,
    minutes, points, rand, reason, createdAt:Date.now()
  });
  await setJSON(KEY_DEDUCTIONS, deductions);
  showToast('Afgetrek.');
  document.getElementById('deduct-minutes').value = 0;
  document.getElementById('deduct-points').value = 0;
  document.getElementById('deduct-rand').value = 0;
  document.getElementById('deduct-reason').value = '';
  renderDeductHistory();
  renderParentSummary();
};
document.getElementById('btn-back-from-deduct').onclick = () => {
  showView('view-parent');
};

/* ===================================================================
   MANAGE KIDS & PASSWORDS
   =================================================================== */
function renderManageKids(){
  const container = document.getElementById('kids-editor-list');
  container.innerHTML = profiles.kids.map((k,i)=>`
    <div class="editor-row" data-idx="${i}">
      <label>NAAM</label>
      <input type="text" class="k-name" value="${escapeHtml(k.name)}">
      <div class="erow-2col">
        <div>
          <label>OUDERDOM</label>
          <input type="number" class="k-age" value="${k.age}" min="1" max="25">
        </div>
        <div>
          <label>4-SYFER PIN</label>
          <input type="text" class="k-pin" value="${pins[k.id]||''}" maxlength="4" inputmode="numeric" pattern="[0-9]*">
        </div>
      </div>
    </div>
  `).join('');
  document.getElementById('parent-pw-new').value = '';
  document.getElementById('parent-sq').value = parentAuth.question || '';
  document.getElementById('parent-sa').value = parentAuth.answer || '';
}
document.getElementById('btn-save-kids').onclick = async () => {
  const rows = document.querySelectorAll('#kids-editor-list .editor-row');
  let pinError = false;
  rows.forEach((row, i)=>{
    const name = row.querySelector('.k-name').value.trim();
    const age = parseInt(row.querySelector('.k-age').value, 10) || profiles.kids[i].age;
    const pin = row.querySelector('.k-pin').value.trim();
    if(name) profiles.kids[i].name = name;
    profiles.kids[i].age = age;
    if(/^\d{4}$/.test(pin)){
      pins[profiles.kids[i].id] = pin;
    } else {
      pinError = true;
    }
  });
  if(pinError){
    showToast('Elke PIN moet presies 4 syfers wees \u2014 nie alles is gestoor nie.');
  }
  const newPw = document.getElementById('parent-pw-new').value.trim();
  const sq = document.getElementById('parent-sq').value.trim();
  const sa = document.getElementById('parent-sa').value.trim();
  if(newPw.length > 0){
    if(newPw.length < 4){ showToast('Nuwe wagwoord moet ten minste 4 karakters wees.'); return; }
    parentAuth.password = newPw;
  }
  if(sq) parentAuth.question = sq;
  if(sa) parentAuth.answer = sa;

  await Promise.all([
    setJSON(KEY_PROFILES, profiles),
    setJSON(KEY_PINS, pins),
    setJSON(KEY_PARENT_AUTH, parentAuth)
  ]);
  if(!pinError) showToast('Kinders en wagwoorde is gestoor.');
};

/* ===================================================================
   GO
   =================================================================== */
init();
</script>
</body>
</html>
