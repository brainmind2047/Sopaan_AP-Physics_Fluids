<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Sopaan · Fluids</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,500;9..144,700&family=Source+Sans+3:wght@400;600;700&family=IBM+Plex+Mono:wght@500;600&display=swap">
<style>
  html,body{margin:0;} img{max-width:100%;} [hidden]{display:none !important;}
  :root{
    --navy:#16264A; --navy-2:#1F3B6B; --gold:#C79A3E; --gold-soft:#F3E7C9;
    --paper:#FBF9F4; --paper-2:#F1EAD8; --card:#FFFFFF;
    --ink:#211E1A; --ink-soft:#655D4C; --rule:#E4DCC8;
    --success:#2E8B57; --success-soft:#E1F2E7;
    --danger:#BF4B45; --danger-soft:#FAE3E1;
    --locked:#C7BEA9;
    --focus:#1F3B6B;
    --accent-text:#1F3B6B; --retry-text:#8A661F;
    color-scheme:light;
  }
  @media (prefers-color-scheme: dark){
    :root:not([data-theme="light"]){
      --navy:#0E1830; --navy-2:#16264A; --gold:#E0B75B; --gold-soft:#3A2F16;
      --paper:#141210; --paper-2:#1C1914; --card:#1C1914;
      --ink:#EDE7DA; --ink-soft:#B2A996; --rule:#3A342A;
      --success:#7BC79A; --success-soft:#1B2E22;
      --danger:#E38884; --danger-soft:#331D1B;
      --locked:#4A4436;
      --focus:#E0B75B;
      --accent-text:#E0B75B; --retry-text:#E0B75B;
      color-scheme:dark;
    }
  }
  :root[data-theme="dark"]{
    --navy:#0E1830; --navy-2:#16264A; --gold:#E0B75B; --gold-soft:#3A2F16;
    --paper:#141210; --paper-2:#1C1914; --card:#1C1914;
    --ink:#EDE7DA; --ink-soft:#B2A996; --rule:#3A342A;
    --success:#7BC79A; --success-soft:#1B2E22;
    --danger:#E38884; --danger-soft:#331D1B;
    --locked:#4A4436;
    --focus:#E0B75B;
    --accent-text:#E0B75B; --retry-text:#E0B75B;
    color-scheme:dark;
  }

  *{box-sizing:border-box;}
  body{background:var(--paper); color:var(--ink); font-family:'Source Sans 3',-apple-system,'Segoe UI',sans-serif; padding-inline:0; padding-block:0;}
  h1,h2,h3{font-family:'Fraunces',Georgia,serif; text-wrap:balance; margin:0;}
  .num{font-family:'IBM Plex Mono',ui-monospace,monospace; font-variant-numeric:tabular-nums;}

  header.brand{
    background:linear-gradient(155deg,var(--navy) 0%, var(--navy-2) 100%);
    color:#F4EFDF; padding-block:calc(20px + env(safe-area-inset-top,0px)) 18px; padding-inline:20px;
  }
  .brand-row{display:flex; align-items:center; gap:12px; max-width:900px; margin:0 auto;}
  .crest{
    width:42px; height:42px; border-radius:10px; background:var(--gold); color:var(--navy);
    display:flex; align-items:center; justify-content:center; font-family:'Fraunces',serif; font-weight:700; font-size:18px; flex-shrink:0;
  }
  .brand-name{font-size:12px; letter-spacing:.08em; text-transform:uppercase; color:var(--gold); font-weight:700;}
  .series-name{font-size:19px; font-weight:700; font-family:'Fraunces',serif;}
  .chapter-eyebrow{max-width:900px; margin:14px auto 0; font-size:12px; letter-spacing:.06em; text-transform:uppercase; color:#AEB9D6;}
  .chapter-title{font-size:28px; max-width:900px; margin:2px auto 0;}
  .chapter-sub{font-size:14.5px; color:var(--gold); font-weight:700; max-width:900px; margin:3px auto 0;}

  .chapter-progress{max-width:900px; margin:14px auto 0; display:flex; align-items:center; gap:10px;}
  .cp-track{flex:1; height:6px; border-radius:99px; background:rgba(255,255,255,.18); overflow:hidden;}
  .cp-fill{height:100%; background:var(--gold); border-radius:99px; transition:width .3s ease;}
  .cp-label{font-size:11.5px; color:#CFD7EA; white-space:nowrap;}

  .tabbar{position:sticky; top:env(safe-area-inset-top,0px); z-index:15; background:var(--paper); border-bottom:1px solid var(--rule); overflow-x:auto; white-space:nowrap;}
  .tabbar-inner{max-width:900px; margin:0 auto; display:flex; padding-inline:16px;}
  .tab-btn{font-family:inherit; font-size:14px; font-weight:600; color:var(--ink-soft); background:none; border:none; padding:13px 16px; cursor:pointer; position:relative; flex-shrink:0;}
  .tab-btn.active{color:var(--accent-text);}
  .tab-btn.active::after{content:''; position:absolute; left:12px; right:12px; bottom:0; height:3px; background:var(--gold); border-radius:3px 3px 0 0;}
  .tab-count{font-size:11px; color:var(--ink-soft); margin-left:5px;}

  .slide-progress{max-width:900px; margin:0 auto; padding:10px 16px 0; display:flex; align-items:center; gap:10px;}
  .sp-track{flex:1; height:5px; border-radius:99px; background:var(--rule); overflow:hidden;}
  .sp-fill{height:100%; background:var(--accent-text); border-radius:99px; transition:width .3s ease;}
  .sp-label{font-size:12px; color:var(--ink-soft); white-space:nowrap; font-weight:600;}

  .wrap{max-width:900px; margin:0 auto; padding:16px 16px calc(110px + env(safe-area-inset-bottom,0px));}

  .qcard{background:var(--card); border:1px solid var(--rule); border-radius:14px; padding:18px;}
  .qhead{display:flex; align-items:flex-start; gap:10px; margin-bottom:10px;}
  .qnum{width:32px; height:32px; border-radius:8px; background:var(--gold-soft); color:var(--accent-text); display:flex; align-items:center; justify-content:center; font-weight:700; font-family:'Fraunces',serif; flex-shrink:0; font-size:14px;}
  .qtext{font-size:16px; line-height:1.55; flex:1;}
  .qtag{font-size:10.5px; color:var(--gold); background:var(--gold-soft); padding:2px 7px; border-radius:99px; font-weight:700; margin-left:6px; white-space:nowrap;}
  .marks-pill{font-size:11px; font-weight:700; color:var(--ink-soft); border:1px solid var(--rule); padding:3px 9px; border-radius:99px; margin-left:auto; flex-shrink:0; white-space:nowrap;}
  .step-badge{font-size:11px; font-weight:700; color:var(--accent-text); background:var(--paper-2); border:1px solid var(--rule); padding:3px 9px; border-radius:99px; display:inline-block; margin-bottom:12px;}

  .options{display:flex; flex-direction:column; gap:8px; margin-top:10px;}
  .opt{display:flex; align-items:center; gap:10px; padding:11px 12px; border:1.5px solid var(--rule); border-radius:10px; cursor:pointer; font-size:15px; background:var(--paper);}
  .opt input{accent-color:var(--navy-2);}
  .opt.is-correct{border-color:var(--success); background:var(--success-soft);}
  .opt.is-wrong{border-color:var(--danger); background:var(--danger-soft);}
  .opt.locked{cursor:not-allowed;}

  .subpart-label{font-weight:700; font-size:12.5px; color:var(--accent-text); text-transform:uppercase; letter-spacing:.03em; margin:14px 0 6px;}
  .or-divider{text-align:center; font-size:11px; font-weight:700; letter-spacing:.08em; color:var(--ink-soft); margin:8px 0;}

  .steps{display:flex; flex-direction:column; gap:10px;}
  .step-line{font-size:14.5px; line-height:1.9; background:var(--paper); border:1px dashed var(--rule); border-radius:10px; padding:9px 12px;}
  .step-line.resolved{opacity:.9;}
  .blank-input{font-family:'IBM Plex Mono',monospace; font-size:14px; border:1.5px solid var(--rule); border-radius:6px; padding:3px 8px; width:120px; background:var(--card); color:var(--ink); margin:0 2px;}
  .blank-input:focus{outline:none; border-color:var(--focus); box-shadow:0 0 0 3px var(--gold-soft);}
  .blank-input.is-correct{border-color:var(--success); background:var(--success-soft);}
  .blank-input.is-wrong{border-color:var(--danger); background:var(--danger-soft);}
  .blank-input[disabled]{opacity:.85;}
  .reveal-note{font-size:12px; color:var(--danger); padding-left:2px; margin-top:-2px;}

  .feedback{font-size:13.5px; padding:10px 12px; border-radius:9px; margin-top:14px; display:none;}
  .feedback.show{display:block;}
  .feedback.ok{background:var(--success-soft); color:var(--success);}
  .feedback.retry{background:var(--gold-soft); color:var(--retry-text);}
  .feedback.reveal{background:var(--danger-soft); color:var(--danger);}
  .feedback.err{background:var(--danger-soft); color:var(--danger);}
  .attempts-dots{display:inline-flex; gap:4px; margin-left:2px;}
  .attempts-dots span{width:6px; height:6px; border-radius:50%; background:var(--ink-soft); opacity:.3; display:inline-block;}
  .attempts-dots span.used{opacity:1; background:var(--danger);}

  .ar-box{background:var(--paper-2); border-radius:10px; padding:10px 12px; margin-bottom:12px; font-size:13px; color:var(--ink-soft);}

  .navbar{
    position:fixed; left:0; right:0; bottom:0; z-index:30; background:var(--paper);
    border-top:1px solid var(--rule); padding:10px 16px calc(10px + env(safe-area-inset-bottom,0px));
  }
  .navbar-inner{max-width:900px; margin:0 auto; display:flex; gap:8px; flex-wrap:wrap; align-items:center;}
  .btn{font-family:inherit; font-size:13.5px; font-weight:700; padding:10px 14px; border-radius:9px; border:1.5px solid var(--rule); background:var(--card); color:var(--ink); cursor:pointer;}
  .btn:hover{border-color:var(--navy-2);}
  .btn:disabled{opacity:.4; cursor:not-allowed;}
  .btn-primary{background:var(--navy-2); color:#fff; border-color:var(--navy-2);}
  .navbar .spacer{flex:1;}

  .fab{position:fixed; right:16px; bottom:calc(74px + env(safe-area-inset-bottom,0px)); background:var(--gold); color:var(--navy); border:none; border-radius:999px; padding:11px 16px; font-family:inherit; font-weight:700; font-size:13px; display:flex; align-items:center; gap:7px; cursor:pointer; box-shadow:0 6px 16px rgba(0,0,0,.18); z-index:35;}
  .fab-badge{background:rgba(255,255,255,.55); border-radius:99px; padding:1px 7px; font-size:11px;}

  .overlay{position:fixed; inset:0; background:rgba(20,18,14,.45); z-index:50; display:none; align-items:flex-end; justify-content:center;}
  .overlay.show{display:flex;}
  .palette{background:var(--card); width:min(480px,100%); max-height:78vh; overflow-y:auto; border-radius:18px 18px 0 0; padding:18px 18px calc(18px + env(safe-area-inset-bottom,0px)); border:1px solid var(--rule); border-bottom:none;}
  @media (min-width:640px){ .overlay{align-items:center;} .palette{border-radius:18px; border-bottom:1px solid var(--rule); max-height:74vh;} }
  .palette-head{display:flex; align-items:center; justify-content:space-between; margin-bottom:6px;}
  .palette-head h2{font-size:16px;}
  .palette-close{background:none; border:none; font-size:20px; color:var(--ink-soft); cursor:pointer; padding:4px;}
  .palette-legend{display:flex; gap:12px; flex-wrap:wrap; font-size:11px; color:var(--ink-soft); margin:10px 0 14px;}
  .palette-legend span{display:inline-flex; align-items:center; gap:5px;}
  .dot{width:9px; height:9px; border-radius:50%; display:inline-block;}
  .dot.correct{background:var(--success);} .dot.revealed{background:var(--danger);}
  .dot.skipped{background:var(--gold);} .dot.locked{background:var(--locked);}
  .dot.current{background:var(--navy-2);}
  .chip-grid{display:grid; grid-template-columns:repeat(auto-fill,minmax(48px,1fr)); gap:8px;}
  .chip{border:1.5px solid var(--rule); border-radius:9px; padding:8px 4px; text-align:center; font-family:'IBM Plex Mono',monospace; font-size:12.5px; font-weight:600; cursor:pointer; background:var(--paper); color:var(--ink);}
  .chip[data-status="correct"]{border-color:var(--success); background:var(--success-soft); color:var(--success);}
  .chip[data-status="revealed"]{border-color:var(--danger); background:var(--danger-soft); color:var(--danger);}
  .chip[data-status="skipped"]{border-color:var(--gold); background:var(--gold-soft); color:var(--retry-text);}
  .chip[data-status="locked"]{border-color:var(--rule); color:var(--locked); cursor:not-allowed; background:var(--paper-2);}
  .chip[data-status="current"]{outline:2px solid var(--navy-2); outline-offset:1px;}

  .toast{position:fixed; left:50%; bottom:calc(140px + env(safe-area-inset-bottom,0px)); transform:translateX(-50%); background:var(--ink); color:var(--paper); padding:9px 16px; border-radius:99px; font-size:13px; opacity:0; pointer-events:none; transition:opacity .25s ease; z-index:60;}
  .toast.show{opacity:1;}

  .done-card{text-align:center; padding:36px 20px;}
  .done-card .big{font-size:38px; margin-bottom:6px;}
  .score-pills{display:flex; gap:10px; justify-content:center; flex-wrap:wrap; margin:16px 0;}
  .score-pill{padding:8px 16px; border-radius:99px; font-size:13px; font-weight:700;}

  footer.brandfoot{max-width:900px; margin:14px auto 0; padding:0 16px calc(110px + env(safe-area-inset-bottom,0px)); text-align:center; font-size:12px; color:var(--ink-soft);}

  .mode-pill{font-family:inherit; font-size:12.5px; font-weight:700; color:var(--navy); background:var(--gold); border:none; border-radius:99px; padding:6px 14px; cursor:pointer; margin-top:12px; display:inline-flex; align-items:center; gap:6px;}
  .mode-pick{display:flex; flex-direction:column; gap:14px; padding:8px 0 24px;}
  .mode-card{background:var(--card); border:1.5px solid var(--rule); border-radius:16px; padding:22px; cursor:pointer; text-align:left;}
  .mode-card:hover{border-color:var(--navy-2);}
  .mode-card .mode-icon{font-size:26px; margin-bottom:8px;}
  .mode-card h3{font-size:18px; margin-bottom:6px;}
  .mode-card p{font-size:13.5px; color:var(--ink-soft); line-height:1.5; margin:0;}
  .quiz-hint{font-size:12.5px; color:var(--ink-soft); background:var(--paper-2); border-radius:9px; padding:8px 12px; margin-bottom:14px;}
  .review-row{border:1px solid var(--rule); border-radius:10px; padding:11px 13px; margin-bottom:10px;}
  .review-tag{font-size:11.5px; font-weight:700; margin-bottom:4px; display:block;}
  .review-tag.ok{color:var(--success);} .review-tag.bad{color:var(--danger);} .review-tag.na{color:var(--ink-soft);}
  .review-q{font-size:13.5px; margin-bottom:6px; color:var(--ink-soft);}
  .review-ans{font-size:13px; margin-bottom:2px;}

  .who-row{max-width:900px; margin:12px auto 0; display:flex; flex-wrap:wrap; gap:8px; align-items:center;}
  .who-row .mode-pill{margin-top:0;}
  .who{display:inline-flex; flex-wrap:wrap; align-items:center; gap:6px; font-size:12.5px; color:#CFD7EA;}
  .who b{color:#F4EFDF;}
  .who button{font-family:inherit; font-size:12px; font-weight:700; color:#F4EFDF; background:rgba(255,255,255,.12); border:1px solid rgba(255,255,255,.22); border-radius:99px; padding:5px 11px; cursor:pointer;}
  .who button:hover{background:rgba(255,255,255,.2);}
  .login-card{max-width:460px; margin:8px auto 0; background:var(--card); border:1px solid var(--rule); border-radius:16px; padding:22px;}
  .login-card h2{font-size:21px; margin-bottom:4px;}
  .login-card p.lead{font-size:13.5px; color:var(--ink-soft); margin:0 0 16px; line-height:1.5;}
  .fld{display:flex; flex-direction:column; gap:5px; margin-bottom:12px;}
  .fld label{font-size:12px; font-weight:700; letter-spacing:.04em; text-transform:uppercase; color:var(--ink-soft);}
  .fld input{font-family:inherit; font-size:15px; padding:10px 12px; border:1.5px solid var(--rule); border-radius:9px; background:var(--paper); color:var(--ink);}
  .fld input:focus{outline:none; border-color:var(--focus); box-shadow:0 0 0 3px var(--gold-soft);}
  .fld-row{display:grid; grid-template-columns:1fr 1fr; gap:10px;}
  .login-err{font-size:13px; color:var(--danger); background:var(--danger-soft); border-radius:8px; padding:8px 10px; margin-bottom:12px;}
  .login-note{font-size:12px; color:var(--ink-soft); margin-top:12px; line-height:1.5;}
  .known{margin:0 0 16px; display:flex; flex-direction:column; gap:6px;}
  .known-label{font-size:12px; font-weight:700; letter-spacing:.04em; text-transform:uppercase; color:var(--ink-soft);}
  .known-btn{display:flex; justify-content:space-between; align-items:center; gap:10px; text-align:left; font-family:inherit; font-size:14.5px; padding:10px 12px; border:1.5px solid var(--rule); border-radius:10px; background:var(--paper); color:var(--ink); cursor:pointer;}
  .known-btn:hover{border-color:var(--navy-2);}
  .known-btn small{font-size:12px; color:var(--ink-soft);}
  .rec-card{background:var(--card); border:1px solid var(--rule); border-radius:14px; padding:18px; margin-bottom:14px;}
  .rec-card h2{font-size:19px; margin-bottom:10px;}
  .rec-card h3{font-size:15px; margin:4px 0 8px;}
  .rec-table-wrap{overflow-x:auto;}
  .rec-table{width:100%; border-collapse:collapse; font-size:13.5px; font-variant-numeric:tabular-nums;}
  .rec-table th{text-align:left; font-size:11.5px; text-transform:uppercase; letter-spacing:.04em; color:var(--ink-soft); padding:6px 8px; border-bottom:1px solid var(--rule); white-space:nowrap;}
  .rec-table td{padding:8px; border-bottom:1px solid var(--rule); white-space:nowrap;}
  .rec-bar{display:inline-block; width:70px; height:6px; border-radius:99px; background:var(--rule); overflow:hidden; vertical-align:middle; margin-right:6px;}
  .rec-bar i{display:block; height:100%; background:var(--success);}
  .rec-empty{font-size:13.5px; color:var(--ink-soft);}
  .sec-sub{max-width:900px; margin:0 auto; padding:10px 16px 0; font-size:12.5px; font-weight:700; color:var(--accent-text); letter-spacing:.02em;}
  .opt{flex-wrap:wrap;}
  .opt-l{font-family:'IBM Plex Mono',monospace; font-size:13px; font-weight:600; color:var(--ink-soft);}
  .opt-t{flex:1; min-width:0;}
  .opt.is-chosen:not(.is-correct):not(.is-wrong){border-color:var(--navy-2); background:var(--gold-soft);}
  .opt-tag{font-size:11px; font-weight:700; padding:2px 8px; border-radius:99px; background:var(--card); border:1px solid currentColor; white-space:nowrap;}
  .opt.is-correct .opt-tag{color:var(--success);} .opt.is-wrong .opt-tag{color:var(--danger);} .opt.is-chosen:not(.is-correct):not(.is-wrong) .opt-tag{color:var(--accent-text);}
  .chosen{font-size:13.5px; margin-top:10px; padding:8px 12px; border-radius:9px;}
  .chosen.ok{background:var(--success-soft); color:var(--success);} .chosen.bad{background:var(--danger-soft); color:var(--danger);}
  .chosen + .chosen{margin-top:6px;}
  .solution{margin-top:14px; border:1px solid var(--rule); border-left:4px solid var(--gold); background:var(--paper-2); border-radius:10px; padding:12px 14px;}
  .sol-h{font-family:'Fraunces',Georgia,serif; font-weight:700; font-size:14px; color:var(--accent-text); margin-bottom:6px;}
  .sol-line{font-size:14.5px; line-height:1.7;}
  .rev-sol summary{cursor:pointer; font-size:12.5px; font-weight:700; color:var(--accent-text); margin-top:6px;}
  .rev-sol .solution{margin-top:8px;}
  .chapter-credit{max-width:900px; margin:4px auto 0; font-size:12px; color:#CFD7EA;}
  footer.brandfoot a{color:inherit;}
  .blank-input.wide{width:260px; max-width:100%; font-family:'Source Sans 3',sans-serif;}
  .blank-input.expr{width:170px; max-width:100%;}
  /*fix-layout*/ .cp-fill,.sp-fill{width:0;} .fld{min-width:0;} .fld input{width:100%; min-width:0; box-sizing:border-box;}
  .fig{margin:6px 0 10px; display:flex; justify-content:center;}
  .figsvg{width:100%; max-width:340px; height:auto; overflow:visible;}
  .figsvg .ln,.figsvg .arm{stroke:var(--ink); stroke-width:1.6; fill:none;}
  .figsvg .arm{stroke:var(--accent-text); stroke-width:2;}
  .figsvg .pt{fill:var(--ink);}
  .figsvg .lb{fill:var(--ink); font:600 13px 'Source Sans 3',sans-serif;}
  .figsvg .al{fill:var(--accent-text); font:700 12px 'Source Sans 3',sans-serif;}
  .figsvg .wg{fill:var(--gold-soft); stroke:var(--gold); stroke-width:1.2;}
  .figsvg .wg2{fill:rgba(199,154,62,.35); stroke:var(--gold); stroke-width:1.2;}
  .figsvg .ra{fill:none; stroke:var(--ink); stroke-width:1.2;}
  .figsvg .ahd{fill:var(--ink);}
  .figsvg .pr{fill:var(--paper-2); stroke:var(--ink-soft); stroke-width:1.2;}
  .figsvg .tk{stroke:var(--ink-soft); stroke-width:.8;}
  .figsvg .po{fill:var(--ink); font:600 8.5px 'IBM Plex Mono',monospace;}
  .figsvg .pi{fill:var(--danger); font:600 7.5px 'IBM Plex Mono',monospace;}
  .figsvg .sh{fill:var(--gold-soft); stroke:var(--ink); stroke-width:1.5; stroke-linejoin:round;}
  .figsvg .sh2{fill:rgba(199,154,62,.38); stroke:var(--ink); stroke-width:1.5; stroke-linejoin:round;}
  .figsvg .sh3{fill:rgba(199,154,62,.22); stroke:var(--ink); stroke-width:1.5; stroke-linejoin:round;}
  .figsvg .none{fill:none;}
  .figsvg .hid{stroke-dasharray:5 4; fill:none;}
  .figsvg .tick{stroke:var(--ink); stroke-width:1.4; fill:none;}
  .figsvg .shd{fill:var(--accent-text); fill-opacity:.55;}
  .figsvg .cell{fill:var(--card); stroke:var(--ink); stroke-width:1.1;}
  .figsvg .dr{fill:var(--danger);} .figsvg .dw{fill:var(--card); stroke:var(--ink); stroke-width:1.2;}
  .figsvg .dotfill{fill:var(--danger);}
  .tt{border-collapse:collapse; font-size:13.5px; margin:4px auto; font-variant-numeric:tabular-nums;} .tt th,.tt td{border:1px solid var(--rule); padding:4px 9px; text-align:left;} .tt th{background:var(--paper-2); font-weight:700;} .ttw{overflow-x:auto; max-width:100%;}
  .fq{display:inline-flex; flex-direction:column; vertical-align:middle; text-align:center; font-size:.82em; line-height:1.12; margin:0 2px;}
  .fq>span:first-child{border-bottom:1.5px solid currentColor; padding:0 2px;}
  .fq>span:last-child{padding:0 2px;}
  .mx{white-space:nowrap;}
  .blank-input.fr{width:110px;}
  @media (prefers-reduced-motion:reduce){ *{transition:none !important;} }
.datline{display:block;margin-top:8px;padding:8px 10px;border-radius:8px;background:var(--paper-2);font:500 14px/1.7 'IBM Plex Mono',monospace;word-spacing:2px;overflow-wrap:anywhere;}

  .theory{display:flex;flex-direction:column;gap:16px;padding-bottom:40px;}
  .hub{display:grid;grid-template-columns:1fr;gap:12px;}
  @media (min-width:640px){ .hub{grid-template-columns:repeat(3,1fr);} }
  .hub-card{background:var(--card);border:1px solid var(--rule);border-radius:14px;padding:16px;display:flex;flex-direction:column;gap:8px;}
  .hub-card h3{font-family:'Fraunces',serif;font-size:18px;margin:0;color:var(--accent-text);}
  .hub-card p{margin:0;font-size:14px;color:var(--ink-soft);line-height:1.5;}
  .hub-btns{display:flex;flex-wrap:wrap;gap:8px;margin-top:auto;}
  .hub-btn{min-height:40px;border:1.5px solid var(--rule);background:var(--paper-2);color:var(--ink);border-radius:10px;padding:8px 12px;font:600 14px 'Source Sans 3',sans-serif;cursor:pointer;text-align:left;}
  .hub-btn:hover{border-color:var(--gold);}
  .hub-btn.primary{background:var(--navy);color:#F4EFDF;border-color:var(--navy);}
  .note{background:var(--card);border:1px solid var(--rule);border-radius:14px;padding:18px;scroll-margin-top:120px;}
  .note h2{font-family:'Fraunces',serif;font-size:22px;margin:0 0 4px;color:var(--ink);}
  .note .lt{font-size:13.5px;color:var(--ink-soft);margin:0 0 12px;}
  .note .lt b{color:var(--accent-text);}
  .note h4{font:700 15px 'Source Sans 3',sans-serif;margin:16px 0 6px;color:var(--accent-text);}
  .note p,.note li{font-size:15.5px;line-height:1.6;}
  .note ul{padding-left:20px;margin:6px 0;}
  .keybox{background:var(--gold-soft);border-left:4px solid var(--gold);border-radius:8px;padding:10px 12px;margin:10px 0;font-size:15px;line-height:1.6;}
  .keybox b{color:var(--ink);}
  .ex{background:var(--paper-2);border-radius:10px;padding:12px;margin:10px 0;}
  .ex .exh{font-family:'Fraunces',serif;font-weight:700;color:var(--accent-text);margin-bottom:4px;}
  .ex .exl{font-size:15px;line-height:1.7;}
  .ttab{width:100%;border-collapse:collapse;font-size:14.5px;margin:8px 0;}
  .ttab th,.ttab td{border:1px solid var(--rule);padding:7px 8px;text-align:left;vertical-align:top;}
  .ttab th{background:var(--paper-2);}
  .tscroll{overflow-x:auto;}
  .mono{font-family:'IBM Plex Mono',monospace;font-size:.92em;}
  @media (max-width:480px){ .ttab{font-size:13.5px;} .ttab th,.ttab td{padding:6px;} }
  .note .figsvg{max-width:100%;height:auto;display:block;margin:8px auto;}


  .rep-top{display:flex;flex-wrap:wrap;gap:18px;align-items:center;justify-content:center;margin-top:8px;}
  .rep-legend{flex:1;min-width:220px;display:flex;flex-direction:column;gap:8px;}
  .rep-cap{font:700 13px 'Source Sans 3',sans-serif;color:var(--ink-soft);text-transform:uppercase;letter-spacing:.05em;}
  .rep-li{display:flex;align-items:center;gap:6px;font-size:15px;}
  .rep-n{margin-left:auto;white-space:nowrap;padding-left:8px;font-family:'IBM Plex Mono',monospace;font-weight:600;}
  .sw{display:inline-block;width:12px;height:12px;border-radius:3px;flex:none;}
  .rep-grid{display:grid;grid-template-columns:1fr;gap:12px;}
  @media (min-width:640px){ .rep-grid{grid-template-columns:1fr 1fr;} }
  .rep-card{background:var(--card);border:1px solid var(--rule);border-radius:14px;padding:14px;display:flex;flex-direction:column;gap:10px;}
  .rep-h{display:flex;align-items:center;gap:8px;font:700 16px 'Source Sans 3',sans-serif;}
  .crit{display:inline-grid;place-items:center;width:28px;height:28px;border-radius:50%;color:var(--card);font:700 15px Fraunces,serif;flex:none;}
  .rep-row{display:flex;gap:14px;align-items:center;}
  .rep-stats{display:flex;flex-direction:column;gap:5px;font-size:14.5px;}
  .rep-stats div{display:flex;align-items:center;gap:6px;}
  .rep-lvl{margin-top:4px;color:var(--accent-text);} .rep-lvl span{color:var(--ink-soft);font-size:13px;}
  .rep-note{font-size:13px;color:var(--ink-soft);}


  .skip-chips{display:flex;flex-wrap:wrap;gap:8px;justify-content:center;margin:12px 0;}
  .skip-chips .chip{min-width:48px;min-height:40px;cursor:pointer;border:1.5px solid var(--gold);background:var(--gold-soft);color:var(--retry-text);border-radius:10px;font:600 14px 'IBM Plex Mono',monospace;}
  .skip-btns{display:flex;flex-wrap:wrap;gap:10px;justify-content:center;margin-top:12px;}


  .kb-toggle{border:none;background:transparent;font-size:15px;cursor:pointer;padding:0 2px;vertical-align:middle;opacity:.7;}
  .vkb{position:fixed;left:0;right:0;bottom:0;z-index:80;background:var(--paper-2);border-top:1px solid var(--rule);box-shadow:0 -6px 20px rgba(0,0,0,.12);padding:6px 6px 8px;display:none;}
  .vkb.show{display:block;}
  .vkb-top{display:flex;justify-content:space-between;align-items:center;max-width:640px;margin:0 auto 4px;font:600 12px 'Source Sans 3',sans-serif;color:var(--ink-soft);}
  .vkb-link{border:none;background:none;color:var(--accent-text);font:600 12px 'Source Sans 3',sans-serif;cursor:pointer;text-decoration:underline;}
  .vkb-row{display:flex;gap:5px;max-width:640px;margin:0 auto 5px;}
  .vkb-k{flex:1;min-height:42px;border:1px solid var(--rule);border-radius:8px;background:var(--card);color:var(--ink);font:600 17px 'IBM Plex Mono',monospace;cursor:pointer;padding:0;}
  .vkb-k.fn{font:600 13px 'Source Sans 3',sans-serif;background:var(--gold-soft);}
  .vkb-k.done{background:var(--navy);color:#F4EFDF;border-color:var(--navy);}
  .vkb-k:active{transform:scale(.96);}
  body.kb-open .wrap{padding-bottom:360px;}
  body.kb-open .fab{display:none;}
  .tool-bar{display:flex;gap:8px;flex-wrap:wrap;margin:-4px 0 10px;}
  .tool-btn{min-height:36px;border:1.5px solid var(--gold);background:var(--gold-soft);color:var(--ink);border-radius:18px;padding:4px 12px;font:600 13.5px 'Source Sans 3',sans-serif;cursor:pointer;}
  .tool-panel{position:fixed;z-index:85;background:var(--card);border:1px solid var(--rule);border-radius:14px;box-shadow:0 10px 30px rgba(0,0,0,.25);display:none;}
  .tool-panel.show{display:block;}
  .tp-head{display:flex;align-items:center;gap:8px;padding:8px 10px;border-bottom:1px solid var(--rule);font:600 14px 'Source Sans 3',sans-serif;}
  .tp-note{font-size:12px;color:var(--ink-soft);font-weight:500;}
  .tp-x{margin-left:auto;border:1px solid var(--rule);background:var(--paper-2);color:var(--ink);border-radius:8px;min-height:32px;padding:2px 10px;cursor:pointer;font:600 13px 'Source Sans 3',sans-serif;}
  .tp-x + .tp-x{margin-left:0;}
  .calc{right:12px;bottom:84px;width:min(330px,calc(100vw - 24px));}
  body.calc-open .wrap{padding-bottom:440px;}
  body.calc-open .fab{display:none;}
  @media (max-width:640px){ .calc{left:6px;right:6px;width:auto;} .calc-keys button{min-height:36px;} }
  .calc-disp{padding:8px 12px;text-align:right;background:var(--paper-2);}
  .calc-expr{font:500 13px 'IBM Plex Mono',monospace;color:var(--ink-soft);min-height:18px;word-break:break-all;}
  .calc-res{font:600 24px 'IBM Plex Mono',monospace;color:var(--ink);word-break:break-all;}
  .calc-keys{display:grid;grid-template-columns:repeat(6,1fr);gap:5px;padding:8px;}
  .calc-keys button{min-height:40px;border:1px solid var(--rule);border-radius:8px;background:var(--card);color:var(--ink);font:600 14px 'IBM Plex Mono',monospace;cursor:pointer;padding:0;}
  .calc-keys button.fn{background:var(--gold-soft);font-family:'Source Sans 3',sans-serif;font-size:13px;}
  .calc-keys button.eq{grid-column:span 2;background:var(--navy);color:#F4EFDF;border-color:var(--navy);}
  .desmos{left:50%;top:50%;transform:translate(-50%,-50%);width:min(760px,calc(100vw - 16px));height:min(560px,calc(100vh - 90px));flex-direction:column;}
  .desmos.show{display:flex;}
  #desmosBox{flex:1;min-height:0;border-radius:0 0 14px 14px;overflow:hidden;}
  .desmos-msg{padding:24px;text-align:center;color:var(--ink-soft);}
  .chip[data-status="skipped"]{cursor:pointer;}
  .chip[data-status="answered"]{border-color:var(--accent-text);color:var(--accent-text);}


  /* larger reading sizes */
  .chapter-eyebrow{font-size:13.5px;}
  .chapter-title{font-size:36px;line-height:1.15;}
  .chapter-sub{font-size:16.5px;}
  .tab-btn{font-size:15.5px;}
  .sec-sub{font-size:15px;}
  .qtext{font-size:19px;line-height:1.55;}
  .qnum{width:36px;height:36px;font-size:16px;}
  .opt{font-size:17.5px;padding:12px 14px;}
  .step-line{font-size:17.5px;line-height:2;}
  .blank-input{font-size:16px;}
  .sol-line{font-size:16.5px;}
  .feedback{font-size:15px;}
  .note h2{font-size:28px;}
  .note h4{font-size:19px;}
  .note p,.note li{font-size:17.5px;line-height:1.65;}
  .note .lt{font-size:15.5px;}
  .ex .exh{font-size:18px;} .ex .exl{font-size:16.5px;}
  .keybox{font-size:16.5px;}
  .ttab{font-size:15.5px;}
  .hub-card h3{font-size:21px;} .hub-card p{font-size:15.5px;} .hub-btn{font-size:15px;}
  @media (max-width:480px){ .chapter-title{font-size:30px;} .qtext{font-size:18px;} .opt,.step-line{font-size:16.5px;} .note h2{font-size:24px;} .note p,.note li{font-size:16.5px;} }
</style>
</head>
<body>
<header class="brand">
  <div class="brand-row">
    <div class="crest">BM</div>
    <div>
      <div class="brand-name">Brain &amp; Mind Academy</div>
      <div class="series-name">Sopaan <span style="font-weight:400;font-size:14px;color:#CFD7EA;">Practice Series</span></div>
    </div>
  </div>
  <div class="chapter-eyebrow">AP Physics 1 · Chapter 8</div>
  <div class="chapter-title">Fluids</div>
  <div class="chapter-sub">Theory Notes · Practice by Learning Objective · Tests A–D</div><div class="chapter-credit">Organised by AP Physics 1 CED learning objectives · Unit 8</div>
  <div class="chapter-progress">
    <div class="cp-track"><div class="cp-fill" id="cpFill"></div></div>
    <div class="cp-label" id="cpLabel">0% complete</div>
  </div>
  <div class="who-row"><button class="mode-pill" id="modePill" hidden>Choose a mode</button><span class="who" id="whoBar" hidden></span></div>
</header>

<nav class="tabbar"><div class="tabbar-inner" id="tabbar"></div></nav>
<div class="sec-sub" id="secSub"></div><div class="slide-progress"><div class="sp-track"><div class="sp-fill" id="spFill"></div></div><div class="sp-label" id="spLabel">Question 1 of 49</div></div>
<div class="wrap" id="wrap"></div>
<footer class="brandfoot">Brain &amp; Mind Academy · Sopaan Practice Series · AP Physics 1 · Chapter 8<br>Organised by the topics and learning objectives of the AP Physics 1 Course and Exam Description (College Board, 2024), Unit 8. Theory notes, questions, tests and worked solutions are written by Brain &amp; Mind Academy; no workbook or College Board questions are reproduced.</footer>

<div class="navbar"><div class="navbar-inner" id="navbarInner"></div></div>
<button class="fab" id="paletteFab"><span>Questions</span><span class="fab-badge" id="fabBadge">0/49</span></button>

<div class="overlay" id="overlay">
  <div class="palette" role="dialog" aria-label="Question palette">
    <div class="palette-head"><h2 id="paletteTitle">Question palette</h2><button class="palette-close" id="paletteClose">&times;</button></div>
    <div class="palette-legend">
      <span><i class="dot current"></i>Current</span><span><i class="dot correct"></i>Correct</span>
      <span><i class="dot revealed"></i>Revealed</span><span><i class="dot skipped"></i>Skipped</span>
      <span><i class="dot locked"></i>Locked</span>
    </div>
    <div class="chip-grid" id="paletteBody"></div>
  </div>
</div>
<div class="toast" id="toast"></div>

<script>
(function(){
"use strict";

/* ================= audio ================= */
var audioCtx=null;
function ensureAudio(){ if(!audioCtx){ try{ audioCtx=new (window.AudioContext||window.webkitAudioContext)(); }catch(e){} } return audioCtx; }
function playTone(freqs,dur,type){
  var ctx=ensureAudio(); if(!ctx) return;
  try{
    var t0=ctx.currentTime;
    freqs.forEach(function(f,i){
      var o=ctx.createOscillator(), g=ctx.createGain();
      o.type=type||'sine'; o.frequency.value=f;
      var start=t0+i*dur;
      g.gain.setValueAtTime(0.0001,start);
      g.gain.exponentialRampToValueAtTime(0.16,start+0.02);
      g.gain.exponentialRampToValueAtTime(0.0001,start+dur);
      o.connect(g); g.connect(ctx.destination);
      o.start(start); o.stop(start+dur+0.02);
    });
  }catch(e){}
}
function playSuccess(){ playTone([523.25,659.25,783.99],0.11,'sine'); }
function playWrong(){ playTone([220,185],0.14,'square'); }
function playReveal(){ playTone([300,220],0.16,'triangle'); }

/* ================= helpers ================= */
function norm(s){
  return String(s===undefined||s===null?'':s).trim().toLowerCase().replace(/\s+/g,'')
    .replace(/[×∗*·]/g,'x').replace(/÷/g,'/').replace(/–|—|−/g,'-')
    .replace(/[²]/g,'^2').replace(/[³]/g,'^3').replace(/[⁴]/g,'^4').replace(/[⁵]/g,'^5')
    .replace(/[⁶]/g,'^6').replace(/[⁷]/g,'^7').replace(/[⁸]/g,'^8').replace(/[⁹]/g,'^9')
    .replace(/\^/g,'');
}
function parseNum(s){
  if(s===undefined||s===null) return null;
  var t=String(s).trim().replace(/,/g,'').replace(/[−–—]/g,'-').replace(/\s+/g,''); if(t==='') return null;
  var neg=false; if(t[0]==='-'){neg=true;t=t.slice(1);}
  var m=t.match(/^(\d+)\/(\d+)$/);
  if(m){ var v=parseInt(m[1],10)/parseInt(m[2],10); return neg?-v:v; }
  if(/^\d+(\.\d+)?$/.test(t)){ var v2=parseFloat(t); return neg?-v2:v2; }
  return null;
}
/* ---- expression checker: compares answers like (P-2w)/2 and P/2-w at random values ---- */
function exprPrep(s){
  return String(s).toLowerCase().replace(/\s+/g,'').replace(/^[a-z]\(x\)=/i,'').replace(/^y=/i,'').replace(/[×∗·]/g,'*').replace(/÷/g,'/').replace(/[−–—]/g,'-')
    .replace(/²/g,'^2').replace(/³/g,'^3').replace(/⁴/g,'^4').replace(/⁵/g,'^5').replace(/⁶/g,'^6').replace(/⁷/g,'^7').replace(/⁸/g,'^8').replace(/⁹/g,'^9').replace(/π/g,'#').replace(/pi/gi,'#').replace(/½/g,'(1/2)');
}
function exprCompile(src){
  var s=exprPrep(src), i=0, toks=[], absDepth=0;
  while(i<s.length){
    var ch=s[i];
    if(/[0-9.]/.test(ch)){ var j=i; while(j<s.length && /[0-9.]/.test(s[j])) j++; toks.push({k:'n',v:parseFloat(s.slice(i,j))}); i=j; continue; }
    if(/[a-zA-Z#]/.test(ch)){ toks.push({k:'v',v:ch}); i++; continue; }
    if(ch==='|'){ var pv=toks[toks.length-1]; var opn=(absDepth===0)||!pv||('+-*/^(['.indexOf(pv.k)>=0); if(opn){ absDepth++; toks.push({k:'['}); } else { absDepth--; toks.push({k:']'}); } i++; continue; }
    if('+-*/^()'.indexOf(ch)>=0){ toks.push({k:ch}); i++; continue; }
    return null;
  }
  var out=[];
  for(var t=0;t<toks.length;t++){
    var a=toks[t], b=out[out.length-1];
    if(b && (b.k==='n'||b.k==='v'||b.k===')'||b.k===']') && (a.k==='n'||a.k==='v'||a.k==='('||a.k==='[')) out.push({k:'&'});
    out.push(a);
  }
  var p=0;
  function peek(){ return out[p]; }
  function parseE(){ var n=parseT(); while(peek() && (peek().k==='+'||peek().k==='-')){ var o=out[p++].k, r=parseT(); n=(function(l,r,o){return function(e){ return o==='+'?l(e)+r(e):l(e)-r(e); };})(n,r,o); } return n; }
  function parseI(){ var n=parseU(); while(peek() && peek().k==='&'){ p++; var r=parseP(); n=(function(l,r){return function(e){ return l(e)*r(e); };})(n,r); } return n; }
  function parseT(){ var n=parseI(); while(peek() && (peek().k==='*'||peek().k==='/')){ var o=out[p++].k, r=parseI(); n=(function(l,r,o){return function(e){ return o==='*'?l(e)*r(e):l(e)/r(e); };})(n,r,o); } return n; }
  function parseU(){ if(peek() && peek().k==='-'){ p++; var u=parseU(); return function(e){ return -u(e); }; } if(peek() && peek().k==='+'){ p++; return parseU(); } return parseP(); }
  function parseP(){ var b=parseA(); if(peek() && peek().k==='^'){ p++; var x=parseU(); return function(e){ return Math.pow(b(e),x(e)); }; } return b; }
  function parseA(){
    var t=out[p++]; if(!t) throw 0;
    if(t.k==='n') return function(){ return t.v; };
    if(t.k==='v') return t.v==='#' ? function(){ return Math.PI; } : function(e){ return e[t.v]; };
    if(t.k==='('){ var n=parseE(); if(!peek()||peek().k!==')') throw 0; p++; return n; }
    if(t.k==='['){ var m=parseE(); if(!peek()||peek().k!==']') throw 0; p++; return function(e){ return Math.abs(m(e)); }; }
    throw 0;
  }
  try{ var f=parseE(); if(p!==out.length) return null; return f; }catch(e){ return null; }
}
function exprEqual(input,answer){
  var f=exprCompile(input), g=exprCompile(answer); if(!f||!g) return false;
  var hits=0;
  for(var trial=0;trial<8;trial++){
    var env={}; 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('').forEach(function(c){ env[c]=1.3+Math.random()*4.1; });
    var x=f(env), y=g(env);
    if(!isFinite(x)||!isFinite(y)) continue;
    if(Math.abs(x-y)>1e-7*Math.max(1,Math.abs(x),Math.abs(y))) return false;
    hits++;
  }
  return hits>=3;
}
function wordsNorm(s){ return String(s||'').toLowerCase().replace(/\band\b/g,' ').replace(/[^a-z]/g,''); }
function listNorm(s){ return (String(s||'').replace(/[−–—]/g,'-').replace(/(\d) (?=\d{3}\b)/g,'$1').match(/-?\d+(\.\d+)?/g)||[]).join(','); }
function powNorm(s){ return String(s||'').toLowerCase().replace(/\s+/g,'').replace(/[×∗*·.]/g,'x').replace(/[⁰¹²³⁴⁵⁶⁷⁸⁹]+/g,function(m){ return '^'+m.split('').map(function(c){ return '⁰¹²³⁴⁵⁶⁷⁸⁹'.indexOf(c); }).join(''); }).replace(/\^1(?!\d)/g,''); }
function fr(s){ return String(s).replace(/\{(\d+) (\d+)\/(\d+)\}/g,'<span class="mx">$1<span class="fq"><span>$2</span><span>$3</span></span></span>').replace(/\{(\d+)\/(\d+)\}/g,'<span class="fq"><span>$1</span><span>$2</span></span>'); }
function gcdI(a,b){ a=Math.abs(a); b=Math.abs(b); while(b){ var t=a%b; a=b; b=t; } return a; }
function fracParse(s){ s=String(s===undefined||s===null?'':s).trim().replace(/[\u2044\u2215\u00f7]/g,'/').replace(/\s+/g,' ').replace(/\s*\/\s*/g,'/'); var m;
  if((m=s.match(/^(-?\d+)$/))) return {v:+m[1],form:'int',n:+m[1],d:1};
  if((m=s.match(/^(-?\d+)\/(\d+)$/))){ if(+m[2]===0) return null; return {v:m[1]/m[2],form:'frac',n:+m[1],d:+m[2]}; }
  if((m=s.match(/^(\d+)(?: |\+|-)(\d+)\/(\d+)$/))){ if(+m[3]===0) return null; return {v:+m[1]+m[2]/m[3],form:'mixed',w:+m[1],n:+m[2],d:+m[3]}; }
  if((m=s.match(/^-?\d*\.\d+$/))) return {v:parseFloat(s),form:'dec'};
  return null; }
function fracOK(mode,input,answer){
  if(mode==='flist'){ var A=String(input).split(/[,;]/).map(function(x){return x.trim();}).filter(Boolean), K=String(answer).split(/[,;]/).map(function(x){return x.trim();});
    if(A.length!==K.length) return false; return A.every(function(x,i){ var a=fracParse(x), k=fracParse(K[i]); return a&&k&&Math.abs(a.v-k.v)<1e-9; }); }
  var a=fracParse(input), k=fracParse(answer); if(!a||!k) return false;
  var same=Math.abs(a.v-k.v)<1e-9; if(!same) return false;
  if(mode==='fv') return true;
  if(mode==='dec') return a.form==='dec'||a.form==='int';
  if(mode==='fe') return (a.form==='frac'&&k.form==='frac'&&a.n===k.n&&a.d===k.d)||(a.form==='int'&&k.form==='int');
  if(mode==='fi') return a.form==='frac'||(a.form==='int'&&k.form==='int');
  if(mode==='fl') return a.form==='int'||(a.form==='frac'&&gcdI(a.n,a.d)===1)||(a.form==='mixed'&&a.n<a.d&&gcdI(a.n,a.d)===1);
  if(mode==='fm') return a.form==='int'||(a.form==='mixed'&&a.n>0&&a.n<a.d&&gcdI(a.n,a.d)===1);
  return false; }
function answerMatches(input,answer,accept,expr){
  if(expr==='dec'||expr==='fv'||expr==='fe'||expr==='fl'||expr==='fm'||expr==='fi'||expr==='flist'){ if(input===undefined||input===null||String(input).trim()==='') return false; return fracOK(expr,input,answer); }
  if(input===undefined||input===null||String(input).trim()==='') return false;
  if(expr==='words'){ return [answer].concat(accept||[]).some(function(a){ if(/\d/.test(a)) return norm(a)===norm(input); var w=wordsNorm(a); return w!=='' && w===wordsNorm(input); }); }
  if(expr==='list'){ return [answer].concat(accept||[]).some(function(a){ return listNorm(a)===listNorm(input); }); }
  if(expr==='pow'){ return [answer].concat(accept||[]).some(function(a){ return powNorm(a)===powNorm(input); }); }
  if(expr==='time'){ var tn=function(x){ var t=String(x).toLowerCase().replace(/[\s.]/g,'').replace(/[:h]/g,''); if(/^\d{3}(am|pm)?$/.test(t)) t='0'+t; return t; }; return [answer].concat(accept||[]).some(function(a){ return tn(a)===tn(input); }); }
  if(expr==='glist'){ var gn=function(x){ return String(x).toUpperCase().split(/[\s,;]+/).filter(Boolean).sort().join(','); }; return [answer].concat(accept||[]).some(function(a){ return gn(a)===gn(input); }); }
  if(expr==='coord'){ var cn=function(x){ return String(x).replace(/[\u2212\u2013\u2014]/g,'-').replace(/[\s()\[\]]/g,''); }; return [answer].concat(accept||[]).some(function(a){ return cn(a)===cn(input); }); }
  if(expr==='dlist'){ var dn=function(x){ return (String(x).replace(/[−–—]/g,'-').match(/-?\d*\.?\d+/g)||[]).map(Number).join(','); }; return [answer].concat(accept||[]).some(function(a){ return dn(a)===dn(input); }); }
  if(expr==='set'){ var sn=function(x){ return (String(x).match(/-?\d+/g)||[]).map(Number).sort(function(a,b){return a-b;}).join(','); }; return [answer].concat(accept||[]).some(function(a){ return sn(a)===sn(input); }); }
  if(expr==='primes'){ var pn=function(x){ var t=powNorm(x).replace(/[^0-9x^]/g,''); var out=[]; t.split('x').forEach(function(tok){ if(!tok) return; var m=tok.split('^'); var b=+m[0], e=m[1]?+m[1]:1; for(var i=0;i<e;i++) out.push(b); }); return out.sort(function(a,b){return a-b;}).join(','); }; return [answer].concat(accept||[]).some(function(a){ return pn(a)===pn(input); }); }
  if(expr==='angle'){ var an=function(x){ return String(x).toUpperCase().replace(/[^A-Z]/g,''); }; var k=an(answer), v=an(input); return v===k || v===k.split('').reverse().join(''); }
  if(expr==='trans'){ var tv=function(x){ var s=String(x).toLowerCase().replace(/[−–—]/g,'-').replace(/\b(units?|squares?|and|then|steps?|to|the|a)\b/g,' ').replace(/[,;.]/g,' '); var re=/(\d+)\s*(right|left|up|down|r|l|u|d)\b/g, m, dx=0, dy=0, n=0; while((m=re.exec(s))){ var v=+m[1], d=m[2][0]; if(d==='r')dx+=v; else if(d==='l')dx-=v; else if(d==='u')dy+=v; else dy-=v; n++; } if(!n||s.replace(re,'').replace(/\s+/g,'')!=='') return null; return dx+','+dy; }; var ti=tv(input); return ti!==null && [answer].concat(accept||[]).some(function(a){ return tv(a)===ti; }); }
  if(expr==='rot'){ var rv=function(x){ var s=String(x).toLowerCase().replace(/quarter[\s-]*turn/g,'90').replace(/half[\s-]*turn/g,'180').replace(/three[\s-]*quarter[\s-]*turn/g,'270'); var m=s.match(/\b(90|180|270)\b/); if(!m) return null; var a=+m[1]; if(a===180) return '180'; var dir=/anti|counter|acw|ccw/.test(s)?-1:(/clockwise|\bcw\b/.test(s)?1:0); if(!dir) return null; return String(((a*dir)%360+360)%360); }; var ri=rv(input); return ri!==null && ri===rv(answer); }
  if(expr==='expanded'){ var f=function(x){ return String(x).replace(/\s+/g,'').replace(/,/g,''); }; return [answer].concat(accept||[]).some(function(a){ return f(a)===f(input); }); }
  if(expr===true && input!==undefined && input!==null && String(input).trim()!==''){
    if(exprEqual(input,answer)) return true;
    var alt=String(input).replace(/\/\s*(\d+(?:\.\d+)?)\s*([a-zA-Z(])/g,'/$1*$2'); if(alt!==String(input) && exprEqual(alt,answer)) return true;
    return (accept||[]).some(function(a){ return exprEqual(input,a); });
  }
  if(input===undefined||input===null||String(input).trim()==='') return false;
  var n1=parseNum(input), n2=parseNum(answer);
  if(n1!==null && n2!==null){ if(Math.abs(n1-n2)<1e-3) return true; return (accept||[]).some(function(a){ var n3=parseNum(a); return n3!==null && Math.abs(n1-n3)<1e-3; }); }
  var cands=[answer].concat(accept||[]); var ni=norm(input);
  for(var i=0;i<cands.length;i++){ if(norm(cands[i])===ni) return true; }
  return false;
}
function esc(s){ return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;'); }

/* ================= DATA ================= */
var AR_OPTIONS = ["Both A and R are true, and R is the correct explanation of A","Both A and R are true, but R is NOT the correct explanation of A","A is true but R is false","A is false but R is true"];
var THEORY = "<div class=\"hub\"><div class=\"hub-card\"><h3>📖 Theory notes</h3><p>Notes for each CED topic, with the learning objectives, equations, diagrams and worked examples.</p><div class=\"hub-btns\"><button class=\"hub-btn\" data-jump=\"n81\">Topic 8.1</button><button class=\"hub-btn\" data-jump=\"n82\">Topic 8.2</button><button class=\"hub-btn\" data-jump=\"n83\">Topic 8.3</button><button class=\"hub-btn\" data-jump=\"n84\">Topic 8.4</button></div></div><div class=\"hub-card\"><h3>🎯 Practice by learning objective</h3><p>One practice sheet per learning objective: multiple choice first, then step-by-step blanks. 🧮 and 📈 appear where a calculator or graph helps.</p><div class=\"hub-btns\"><div class=\"hub-grp\">Topic 8.1 · Internal Structure and Density</div><button class=\"hub-btn\" data-go=\"s1\">8.1.A · Properties of fluids and density</button><div class=\"hub-grp\">Topic 8.2 · Pressure</div><button class=\"hub-btn\" data-go=\"s2\">8.2.A · Pressure from a force</button><button class=\"hub-btn\" data-go=\"s3\">8.2.B · Pressure in a fluid</button><div class=\"hub-grp\">Topic 8.3 · Fluids and Newton's Laws</div><button class=\"hub-btn\" data-go=\"s4\">8.3.A · Fluids and Newton's laws</button><button class=\"hub-btn\" data-go=\"s5\">8.3.B (i) · Buoyant force</button><button class=\"hub-btn\" data-go=\"s6\">8.3.B (ii) · Floating, sinking and apparent weight</button><div class=\"hub-grp\">Topic 8.4 · Fluids and Conservation Laws</div><button class=\"hub-btn\" data-go=\"s7\">8.4.A · Continuity: conservation of mass</button><button class=\"hub-btn\" data-go=\"s8\">8.4.B (i) · Bernoulli's equation</button><button class=\"hub-btn\" data-go=\"s9\">8.4.B (ii) · Torricelli's theorem and applications</button></div></div><div class=\"hub-card\"><h3>📝 Unit test</h3><p>Four tests, one per category. Take them in Quiz mode, then open the report for your pie charts.</p><div class=\"hub-btns\"><button class=\"hub-btn\" data-go=\"s10\">Test A · Knowing and understanding</button><button class=\"hub-btn\" data-go=\"s11\">Test B · Investigating patterns</button><button class=\"hub-btn\" data-go=\"s12\">Test C · Communicating</button><button class=\"hub-btn\" data-go=\"s13\">Test D · Applying physics in real-life contexts</button><button class=\"hub-btn primary\" data-go=\"report\">📊 View my report</button></div></div></div><style>.hub-grp{width:100%;font:700 12px 'Source Sans 3',sans-serif;color:var(--ink-soft);text-transform:uppercase;letter-spacing:.05em;margin-top:6px;}</style><section class=\"note\" id=\"nintro\"><h2>About this unit</h2><p>Unit 8 of AP Physics 1 is <b>fluids</b>: liquids and gases at rest and in motion. It uses ideas from the whole course (forces, Newton's laws, energy and conservation) applied to matter that flows. The practice tabs follow the College Board course framework, one tab for each learning objective (8.3.B and 8.4.B are large, so each has two tabs).</p><div class=\"tscroll\"><table class=\"ttab\"><tr><th>Topic</th><th>Learning objective</th><th>Practice tabs</th></tr><tr><td>8.1</td><td><b>8.1.A</b> Describe the properties of a fluid.</td><td>8.1.A</td></tr><tr><td>8.2</td><td><b>8.2.A</b> Describe the pressure exerted on a surface by a given force.</td><td>8.2.A</td></tr><tr><td>8.2</td><td><b>8.2.B</b> Describe the pressure exerted by a fluid.</td><td>8.2.B</td></tr><tr><td>8.3</td><td><b>8.3.A</b> Describe the conditions under which a fluid's velocity changes.</td><td>8.3.A</td></tr><tr><td>8.3</td><td><b>8.3.B</b> Describe the buoyant force exerted on an object interacting with a fluid.</td><td>8.3.B (i) · 8.3.B (ii)</td></tr><tr><td>8.4</td><td><b>8.4.A</b> Describe incompressible fluid flow through a cross-sectional area using mass conservation.</td><td>8.4.A</td></tr><tr><td>8.4</td><td><b>8.4.B</b> Describe fluid flow resulting from energy differences between locations.</td><td>8.4.B (i) · 8.4.B (ii)</td></tr></table></div><div class=\"tscroll\"><table class=\"ttab\"><tr><th>Equation</th><th>Meaning</th></tr><tr><td class=\"mono\">ρ&nbsp;=&nbsp;m/V</td><td>density</td></tr><tr><td class=\"mono\">P&nbsp;=&nbsp;F<sub>⊥</sub>/A</td><td>pressure on a surface</td></tr><tr><td class=\"mono\">P&nbsp;=&nbsp;P₀ + ρgh</td><td>absolute pressure at depth h</td></tr><tr><td class=\"mono\">P<sub>gauge</sub>&nbsp;=&nbsp;ρgh</td><td>gauge pressure of a fluid column</td></tr><tr><td class=\"mono\">F<sub>b</sub>&nbsp;=&nbsp;ρV<sub>disp</sub>g</td><td>buoyant force</td></tr><tr><td class=\"mono\">A₁v₁&nbsp;=&nbsp;A₂v₂</td><td>continuity (incompressible flow)</td></tr><tr><td class=\"mono\">P₁ + ρgy₁ + ½ρv₁²&nbsp;=&nbsp;P₂ + ρgy₂ + ½ρv₂²</td><td>Bernoulli's equation</td></tr><tr><td class=\"mono\">v&nbsp;=&nbsp;√(2gΔy)</td><td>Torricelli: speed of flow from an opening</td></tr></table></div><p>Use <b>g ≈ 10 m/s²</b>, water density <b>1000 kg/m³</b> and atmospheric pressure <b>P₀ = 1.0 × 10⁵ Pa</b> unless told otherwise. Fluids are ideal (incompressible, no viscosity). Rounded answers are accepted within about 1%.</p><div class=\"tscroll\"><table class=\"ttab\"><tr><th>Test</th><th>Category</th><th>What it checks</th></tr><tr><td>A</td><td>Knowing and understanding</td><td>Definitions and equations for density, pressure, buoyancy and flow.</td></tr><tr><td>B</td><td>Investigating patterns</td><td>Relationships in data: P against depth, F<sub>b</sub> against volume, v against area or depth.</td></tr><tr><td>C</td><td>Communicating</td><td>Units, gauge vs absolute, free-body diagrams, sig figs, spotting errors.</td></tr><tr><td>D</td><td>Applying physics in real-life contexts</td><td>Dams, ships, hydraulic brakes, drips, hoses; judging reasonableness.</td></tr></table></div><p><b>Tools:</b> every blank opens an on-screen keyboard (⌨️ brings it back). 🧮 opens a scientific calculator (degrees; Insert puts the result in the blank). 📈 opens a Desmos graph set up for the question. Type powers of ten as plain numbers, e.g. 150000.</p></section><section class=\"note\" id=\"n81\"><h2>Topic 8.1 · Internal Structure and Density</h2><p class=\"lt\"><b>Learning objectives</b></p><ul class=\"lt\"><li><b>8.1.A</b> Describe the properties of a fluid.</li></ul><p>Solids, liquids and gases differ because of how strongly their atoms and molecules interact. In a <b>solid</b> the particles are held in fixed positions. In a <b>liquid</b> they are close together but can slide past each other. In a <b>gas</b> they are far apart and interact only weakly, so a gas is easily compressed.</p><p>A <b>fluid</b> is a substance that has no fixed shape: it flows and takes the shape of its container. Liquids and gases are both fluids.</p><p>Fluids are characterised by their <b>density</b>, the ratio of mass to volume: <span class=\"mono\">ρ = m/V</span>, in kg/m³. Density is a property of the material, not of the sample: half a bucket of water has the same density as a full one.</p><div class=\"tscroll\"><table class=\"ttab\"><tr><th>Substance</th><th>ρ (kg/m³)</th><th>Substance</th><th>ρ (kg/m³)</th></tr><tr><td>air</td><td>1.2</td><td>ice</td><td>900</td></tr><tr><td>cooking oil</td><td>800–920</td><td>sea water</td><td>1030</td></tr><tr><td>fresh water</td><td>1000</td><td>aluminium</td><td>2700</td></tr><tr><td>mercury</td><td>13 600</td><td>iron</td><td>7900</td></tr></table></div><p>An <b>ideal fluid</b> is incompressible (its density never changes) and has no viscosity (no internal friction). AP Physics 1 uses this model.</p><div class=\"ex\"><div class=\"exh\">Worked example 1 · Density by displacement</div><div class=\"exl\">A stone of mass 0.54 kg makes the water in a measuring cylinder rise from 300 mL to 500 mL.<br>V = 200 mL = 200 cm³ = 2.0 × 10⁻⁴ m³, so ρ = 0.54 ÷ 2.0 × 10⁻⁴ = <b>2700 kg/m³</b>.</div></div><div class=\"ex\"><div class=\"exh\">Worked example 2 · Air in a room</div><div class=\"exl\">A room is 5.0 m × 4.0 m × 3.0 m = 60 m³.<br>m = ρV = 1.2 × 60 = <b>72 kg</b> of air — about the mass of an adult.</div></div><div class=\"keybox\"><b>Units:</b> 1 g/cm³ = 1000 kg/m³, 1 L = 1000 cm³ = 10⁻³ m³ and 1 cm³ = 10⁻⁶ m³. Water: 1 L has a mass of 1 kg.</div><div class=\"hub-btns\" style=\"margin-top:12px\"><button class=\"hub-btn primary\" data-go=\"s1\">Practise 8.1.A →</button></div></section><section class=\"note\" id=\"n82\"><h2>Topic 8.2 · Pressure</h2><p class=\"lt\"><b>Learning objectives</b></p><ul class=\"lt\"><li><b>8.2.A</b> Describe the pressure exerted on a surface by a given force.</li><li><b>8.2.B</b> Describe the pressure exerted by a fluid.</li></ul><p><b>Pressure</b> is the magnitude of the perpendicular force component exerted per unit area: <span class=\"mono\">P = F<sub>⊥</sub>/A</span>. Its unit is the pascal, 1 Pa = 1 N/m². Pressure is a <b>scalar</b>: at a point in a fluid it has no direction, but the force it produces on any surface acts perpendicular to that surface.</p><p>The same force spread over a larger area gives a smaller pressure (snowshoes, wide tyres); concentrated on a small area it gives a large pressure (knife edges, nails).</p><svg class=\"figsvg\" viewBox=\"0 0 300 160\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><path d=\"M40,60 L70,60 L70,116 L200,116 L200,40 L280,40 L280,146 L40,146 Z\" style=\"fill:var(--accent-text);fill-opacity:.16\"/><path d=\"M40,30 L40,146 L280,146 L280,20 M200,20 L200,116 L70,116 L70,30\" style=\"fill:none;stroke:var(--ink);stroke-width:2\"/><rect x=\"40\" y=\"54\" width=\"30\" height=\"8\" style=\"fill:var(--ink-soft)\"/><rect x=\"200\" y=\"34\" width=\"80\" height=\"8\" style=\"fill:var(--ink-soft)\"/><line style=\"stroke:var(--danger);stroke-width:2.2\" x1=\"55.0\" y1=\"14.0\" x2=\"55.0\" y2=\"50.0\" marker-end=\"url(#ah)\"/><text x=\"47.0\" y=\"20.0\" text-anchor=\"end\" dominant-baseline=\"middle\" style=\"fill:var(--danger);font:700 12px 'Source Sans 3',sans-serif\">F₁</text><line style=\"stroke:var(--success);stroke-width:2.2\" x1=\"240.0\" y1=\"30.0\" x2=\"240.0\" y2=\"4.0\" marker-end=\"url(#ah)\"/><text x=\"250.0\" y=\"12.0\" text-anchor=\"start\" dominant-baseline=\"middle\" style=\"fill:var(--success);font:700 12px 'Source Sans 3',sans-serif\">F₂</text><text class=\"lb\" x=\"55.0\" y=\"72.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">A₁</text><text class=\"lb\" x=\"240.0\" y=\"56.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">A₂</text></svg><p>In a <b>hydraulic lift</b> the pressure is the same everywhere at one level in the connected fluid, so F₁/A₁ = F₂/A₂: a small force on a small piston lifts a large load on a large piston (but the small piston moves further).</p><h4>Pressure in a fluid</h4><p>The <b>absolute pressure</b> at depth h below the surface is the reference (surface) pressure plus the pressure of the column above: <span class=\"mono\">P = P₀ + ρgh</span>. The <b>gauge pressure</b> is the extra part, <span class=\"mono\">P<sub>gauge</sub> = ρgh</span>. A tyre gauge or blood-pressure cuff reads gauge pressure.</p><svg class=\"figsvg\" viewBox=\"0 0 300 190\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><text class=\"lb\" x=\"150.0\" y=\"10.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">Open tank of liquid</text><rect x=\"60\" y=\"44.0\" width=\"180\" height=\"130.0\" style=\"fill:var(--accent-text);fill-opacity:.16\"/><polyline points=\"60,34 60,174 240,174 240,34\" style=\"fill:none;stroke:var(--ink);stroke-width:2\"/><line x1=\"60\" y1=\"44\" x2=\"240\" y2=\"44\" style=\"stroke:var(--accent-text);stroke-width:1.4\"/><circle cx=\"114.0\" cy=\"44.0\" r=\"3.5\" style=\"fill:var(--danger)\"/><text class=\"lb\" x=\"122.0\" y=\"44.0\" text-anchor=\"start\" dominant-baseline=\"middle\">P₀</text><circle cx=\"114.0\" cy=\"115.5\" r=\"3.5\" style=\"fill:var(--danger)\"/><text class=\"lb\" x=\"122.0\" y=\"115.5\" text-anchor=\"start\" dominant-baseline=\"middle\">P = P₀ + ρgh</text><line class=\"ln\" x1=\"48.0\" y1=\"44.0\" x2=\"48.0\" y2=\"115.5\" marker-end=\"url(#ah)\" marker-start=\"url(#ahs)\"/><text class=\"lb\" x=\"44.0\" y=\"79.8\" text-anchor=\"end\" dominant-baseline=\"middle\">h</text></svg><p>Pressure depends only on depth, not on the shape of the container, and it is the same at all points at the same level in one connected fluid at rest.</p><div class=\"ex\"><div class=\"exh\">Worked example 1 · Standing on one foot</div><div class=\"exl\">A 60 kg student stands on one foot of area 0.015 m².<br>P = 600 ÷ 0.015 = <b>4.0 × 10⁴ Pa</b>. On both feet the pressure halves.</div></div><div class=\"ex\"><div class=\"exh\">Worked example 2 · Swimming pool</div><div class=\"exl\">At the bottom of a pool 3.0 m deep: P<sub>gauge</sub> = 1000 × 10 × 3.0 = 3.0 × 10⁴ Pa.<br>P<sub>abs</sub> = 1.0 × 10⁵ + 3.0 × 10⁴ = <b>1.3 × 10⁵ Pa</b>.</div></div><div class=\"ex\"><div class=\"exh\">Worked example 3 · Hydraulic jack</div><div class=\"exl\">Pistons of area 4.0 cm² and 200 cm² support a 12 000 N load on the large one.<br>P = 12 000 ÷ 0.020 = 6.0 × 10⁵ Pa; F₁ = 6.0 × 10⁵ × 4.0 × 10⁻⁴ = <b>240 N</b>.</div></div><div class=\"keybox\"><b>Every 10 m of water adds about 1 atmosphere</b> (1000 × 10 × 10 = 10⁵ Pa). Doubling the depth doubles the gauge pressure, but not the absolute pressure.</div><div class=\"hub-btns\" style=\"margin-top:12px\"><button class=\"hub-btn primary\" data-go=\"s2\">Practise 8.2.A →</button><button class=\"hub-btn primary\" data-go=\"s3\">Practise 8.2.B →</button></div></section><section class=\"note\" id=\"n83\"><h2>Topic 8.3 · Fluids and Newton's Laws</h2><p class=\"lt\"><b>Learning objectives</b></p><ul class=\"lt\"><li><b>8.3.A</b> Describe the conditions under which a fluid's velocity changes.</li><li><b>8.3.B</b> Describe the buoyant force exerted on an object interacting with a fluid.</li></ul><p>Newton's laws apply to fluids. A small parcel of fluid is an object: if the net force on it is zero its velocity stays constant; if there is a net force its velocity changes. The forces come from <b>pressure differences</b> (and gravity). A fluid speeds up when it moves from high pressure to low pressure, and slows down when it moves towards higher pressure.</p><p>In a fluid at rest, each layer must be pushed up by the fluid below more strongly than it is pushed down by the fluid above, to support its weight. That is why pressure increases with depth: ΔP × A = ρ(AΔh)g gives ΔP = ρgΔh.</p><h4>Buoyant force</h4><p>The pressure on the bottom of a submerged object is greater than on its top, so the fluid exerts a net upward <b>buoyant force</b>. <b>Archimedes' principle:</b> its size equals the weight of fluid displaced, <span class=\"mono\">F<sub>b</sub> = ρ<sub>fluid</sub>V<sub>disp</sub>g</span>.</p><svg class=\"figsvg\" viewBox=\"0 0 280 190\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><rect x=\"30\" y=\"66\" width=\"220\" height=\"112\" style=\"fill:var(--accent-text);fill-opacity:.16\"/><line x1=\"30\" y1=\"66\" x2=\"250\" y2=\"66\" style=\"stroke:var(--accent-text);stroke-width:1.4\"/><rect x=\"100.0\" y=\"43.6\" width=\"80\" height=\"56\" style=\"fill:var(--gold-soft);stroke:var(--ink);stroke-width:1.5\"/><line style=\"stroke:var(--accent-text);stroke-width:2.2\" x1=\"112.0\" y1=\"71.6\" x2=\"112.0\" y2=\"21.6\" marker-end=\"url(#ah)\"/><text x=\"104.0\" y=\"21.6\" text-anchor=\"end\" dominant-baseline=\"middle\" style=\"fill:var(--accent-text);font:700 12px 'Source Sans 3',sans-serif\">F_b</text><line style=\"stroke:var(--danger);stroke-width:2.2\" x1=\"140.0\" y1=\"71.6\" x2=\"140.0\" y2=\"119.6\" marker-end=\"url(#ah)\"/><text x=\"148.0\" y=\"115.6\" text-anchor=\"start\" dominant-baseline=\"middle\" style=\"fill:var(--danger);font:700 12px 'Source Sans 3',sans-serif\">mg</text></svg><div class=\"tscroll\"><table class=\"ttab\"><tr><th>Situation</th><th>Result</th></tr><tr><td>ρ<sub>object</sub> &lt; ρ<sub>fluid</sub></td><td>floats; F<sub>b</sub> = mg; fraction submerged = ρ<sub>object</sub>/ρ<sub>fluid</sub></td></tr><tr><td>ρ<sub>object</sub> &gt; ρ<sub>fluid</sub></td><td>sinks; apparent weight = mg − F<sub>b</sub></td></tr><tr><td>ρ<sub>object</sub> = ρ<sub>fluid</sub></td><td>stays where it is (neutral buoyancy)</td></tr></table></div><div class=\"ex\"><div class=\"exh\">Worked example 1 · Stone on a string</div><div class=\"exl\">A 1.5 kg stone of volume 5.0 × 10⁻⁴ m³ hangs in water.<br>F<sub>b</sub> = 1000 × 5.0 × 10⁻⁴ × 10 = 5.0 N; tension = 15 − 5.0 = <b>10 N</b>.</div></div><div class=\"ex\"><div class=\"exh\">Worked example 2 · Floating wood</div><div class=\"exl\">A block of wood (ρ = 600 kg/m³) floats in water.<br>F<sub>b</sub> = mg gives ρ<sub>w</sub>V<sub>sub</sub>g = ρ<sub>wood</sub>Vg, so V<sub>sub</sub>/V = 600 ÷ 1000 = <b>0.60</b>: 60% is under water.</div></div><div class=\"ex\"><div class=\"exh\">Worked example 3 · A slug of water</div><div class=\"exl\">5.0 kg of water in a horizontal pipe of area 0.010 m² has a pressure 2000 Pa higher behind it than in front.<br>Net force = 2000 × 0.010 = 20 N, so a = 20 ÷ 5.0 = <b>4.0 m/s²</b>, towards the lower pressure.</div></div><div class=\"keybox\"><b>The buoyant force depends on the displaced volume and the fluid's density, not on the object's own density or depth</b> (once it is fully submerged). An iron ball and an aluminium ball of the same volume feel the same buoyant force.</div><div class=\"hub-btns\" style=\"margin-top:12px\"><button class=\"hub-btn primary\" data-go=\"s4\">Practise 8.3.A →</button><button class=\"hub-btn primary\" data-go=\"s5\">Practise 8.3.B (i) →</button><button class=\"hub-btn primary\" data-go=\"s6\">Practise 8.3.B (ii) →</button></div></section><section class=\"note\" id=\"n84\"><h2>Topic 8.4 · Fluids and Conservation Laws</h2><p class=\"lt\"><b>Learning objectives</b></p><ul class=\"lt\"><li><b>8.4.A</b> Describe incompressible fluid flow through a cross-sectional area using mass conservation.</li><li><b>8.4.B</b> Describe fluid flow resulting from energy differences between locations.</li></ul><h4>Conservation of mass: continuity</h4><p>For an incompressible fluid, the volume passing any cross-section per second (the <b>volume flow rate</b> A·v, in m³/s) is the same all along a pipe with no leaks: <span class=\"mono\">A₁v₁ = A₂v₂</span>. The mass flow rate is ρAv (kg/s). Where the pipe narrows, the fluid speeds up.</p><svg class=\"figsvg\" viewBox=\"0 0 320 140\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><path d=\"M20,28 L120,28 L180,48 L300,48 L300,76 L180,76 L120,96 L20,96 Z\" style=\"fill:var(--accent-text);fill-opacity:.16\"/><path d=\"M20,28 L120,28 L180,48 L300,48\" style=\"fill:none;stroke:var(--ink);stroke-width:2\"/><path d=\"M20,96 L120,96 L180,76 L300,76\" style=\"fill:none;stroke:var(--ink);stroke-width:2\"/><line style=\"stroke:var(--accent-text);stroke-width:2.2\" x1=\"40.0\" y1=\"62.0\" x2=\"95.0\" y2=\"62.0\" marker-end=\"url(#ah)\"/><text x=\"65.0\" y=\"48.0\" text-anchor=\"start\" dominant-baseline=\"middle\" style=\"fill:var(--accent-text);font:700 12px 'Source Sans 3',sans-serif\">v₁</text><line style=\"stroke:var(--accent-text);stroke-width:2.2\" x1=\"205.0\" y1=\"62.0\" x2=\"270.0\" y2=\"62.0\" marker-end=\"url(#ah)\"/><text x=\"236.0\" y=\"36.0\" text-anchor=\"start\" dominant-baseline=\"middle\" style=\"fill:var(--accent-text);font:700 12px 'Source Sans 3',sans-serif\">v₂</text><text class=\"lb\" x=\"70.0\" y=\"84.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">A₁</text><text class=\"lb\" x=\"240.0\" y=\"88.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">A₂</text></svg><h4>Conservation of energy: Bernoulli's equation</h4><p>For an ideal fluid in steady flow, the pressure, the gravitational potential energy per unit volume and the kinetic energy per unit volume add to a constant along the flow: <span class=\"mono\">P₁ + ρgy₁ + ½ρv₁² = P₂ + ρgy₂ + ½ρv₂²</span>. Work done by the pressure difference changes the fluid's kinetic and potential energy.</p><p>In a horizontal pipe, <b>where the speed is higher the pressure is lower</b>. That is how a narrow part of a pipe (a Venturi) measures flow, and why a strong wind over a roof can lift it.</p><h4>Torricelli's theorem</h4><p>Liquid flows out of an opening a depth Δy below the open surface of a large tank at <span class=\"mono\">v = √(2gΔy)</span> — the same speed as an object falling freely through Δy. Both the surface and the opening are at atmospheric pressure, and the surface moves very slowly.</p><div class=\"ex\"><div class=\"exh\">Worked example 1 · Continuity</div><div class=\"exl\">A pipe of area 0.020 m² carries water at 1.5 m/s into a section of area 0.0050 m².<br>v₂ = 0.020 × 1.5 ÷ 0.0050 = <b>6.0 m/s</b>; flow rate 0.030 m³/s = 30 kg/s.</div></div><div class=\"ex\"><div class=\"exh\">Worked example 2 · Venturi</div><div class=\"exl\">Water at 2.0 m/s and 2.0 × 10⁵ Pa enters a horizontal narrow section where v = 8.0 m/s.<br>P₂ = 2.0 × 10⁵ − ½ × 1000 × (64 − 4) = 2.0 × 10⁵ − 3.0 × 10⁴ = <b>1.7 × 10⁵ Pa</b>.</div></div><div class=\"ex\"><div class=\"exh\">Worked example 3 · Leaking tank</div><div class=\"exl\">A hole is 1.2 m below the surface of an open tank.<br>v = √(2 × 10 × 1.2) = √24 ≈ <b>4.9 m/s</b>. After leaving, the water is a horizontal projectile.</div></div><div class=\"keybox\"><b>Diameter vs area:</b> A = πr², so halving the diameter of a pipe makes the area ¼ and the speed 4 times as large. <b>Faster flow means lower pressure</b> (at the same height), not higher.</div><div class=\"hub-btns\" style=\"margin-top:12px\"><button class=\"hub-btn primary\" data-go=\"s7\">Practise 8.4.A →</button><button class=\"hub-btn primary\" data-go=\"s8\">Practise 8.4.B (i) →</button><button class=\"hub-btn primary\" data-go=\"s9\">Practise 8.4.B (ii) →</button></div></section><section class=\"note\" id=\"nsum\"><h2>Unit checklist</h2><ul><li><b>8.1.A</b> Properties of fluids and density: Describe the properties of a fluid.</li><li><b>8.2.A</b> Pressure from a force: Describe the pressure exerted on a surface by a given force.</li><li><b>8.2.B</b> Pressure in a fluid: Describe the pressure exerted by a fluid.</li><li><b>8.3.A</b> Fluids and Newton's laws: Describe the conditions under which a fluid's velocity changes.</li><li><b>8.3.B (i)</b> Buoyant force: Describe the buoyant force exerted on an object interacting with a fluid.</li><li><b>8.3.B (ii)</b> Floating, sinking and apparent weight: Describe the buoyant force exerted on an object interacting with a fluid: floating objects and apparent weight.</li><li><b>8.4.A</b> Continuity: conservation of mass: Describe incompressible fluid flow through a cross-sectional area using mass conservation.</li><li><b>8.4.B (i)</b> Bernoulli's equation: Describe fluid flow resulting from energy differences between locations.</li><li><b>8.4.B (ii)</b> Torricelli's theorem and applications: Describe fluid flow resulting from energy differences between locations: flow from an opening.</li></ul><div class=\"hub-btns\" style=\"margin-top:10px\"><button class=\"hub-btn\" data-go=\"s10\">Test A</button><button class=\"hub-btn\" data-go=\"s11\">Test B</button><button class=\"hub-btn\" data-go=\"s12\">Test C</button><button class=\"hub-btn\" data-go=\"s13\">Test D</button><button class=\"hub-btn primary\" data-go=\"report\">📊 Report</button></div></section>";
var REPORT = [["s10", "A", "Knowing and understanding"], ["s11", "B", "Investigating patterns"], ["s12", "C", "Communicating"], ["s13", "D", "Applying physics in real-life contexts"]];
var SECTIONS = [{"id": "s1", "label": "8.1.A", "sub": "Properties of fluids and density — LO 8.1.A: describe the properties of a fluid.", "slides": [{"kind": "mcq", "text": "Which of these are both fluids?", "opts": ["sand and ice", "steel and air", "ice and water", "air and water"], "correct": 3, "tag": "", "sol": "Liquids and gases flow and have no fixed shape."}, {"kind": "mcq", "text": "A fluid is best described as a substance that", "opts": ["is always a liquid", "has no fixed shape and can flow", "has no mass", "cannot be compressed"], "correct": 1, "tag": "", "sol": "Gases are fluids too; real fluids have mass."}, {"kind": "mcq", "text": "An object of mass 2.0 kg has a volume of 0.0025 m³. Its density is", "opts": ["1250 kg/m³", "800 kg/m³", "0.00125 kg/m³", "5.0 kg/m³"], "correct": 1, "tag": "", "sol": "ρ = m ÷ V = 2.0 ÷ 0.0025 = 800 kg/m³.", "tools": ["calc"]}, {"kind": "mcq", "text": "An ideal fluid is one that is", "opts": ["always a gas", "massless", "compressible and viscous", "incompressible and has no viscosity"], "correct": 3, "tag": "", "sol": "The AP model of an ideal fluid."}, {"kind": "mcq", "text": "A uniform iron bar is cut in half. The density of each half is", "opts": ["the same as the whole bar", "half that of the bar", "a quarter of that of the bar", "twice that of the bar"], "correct": 0, "tag": "", "sol": "Mass and volume both halve; ρ = m/V is unchanged."}, {"kind": "mcq", "text": "Why is a gas much easier to compress than a liquid?", "opts": ["Liquid molecules have no mass", "Its molecules are far apart and interact only weakly", "Its molecules are bigger", "Liquid molecules do not interact"], "correct": 1, "tag": "", "sol": "There is empty space between gas molecules to squeeze out."}, {"kind": "mcq", "text": "1.0 cm³ of water has a mass of 1.0 g. The density of water is", "opts": ["1.0 kg/m³", "0.001 kg/m³", "100 kg/m³", "1000 kg/m³"], "correct": 3, "tag": "", "sol": "1 g/cm³ = 10⁻³ kg ÷ 10⁻⁶ m³ = 1000 kg/m³."}, {"kind": "blank", "p": "A 0.78 kg stone is lowered into a measuring cylinder. The water level rises from 250 mL to 550 mL.", "tag": "", "marks": "", "flat": [{"t": "Volume of the stone = __B1__ m³", "a": {"B1": "0.0003"}, "accept": ["3e-4", "3*10^-4"]}, {"t": "Density of the stone = __B1__ kg/m³", "a": {"B1": "2600"}}, {"t": "Will it float in water? __B1__ (yes / no)", "a": {"B1": "no"}, "expr": "words", "accept": ["n"]}], "sol": "300 mL = 300 cm³ = 3.0 × 10⁻⁴ m³.\n0.78 ÷ 3.0 × 10⁻⁴ = 2600 kg/m³.\n2600 > 1000: it sinks.", "tools": ["calc"]}, {"kind": "blank", "p": "A classroom is 6.0 m × 5.0 m × 3.0 m. Air has a density of 1.2 kg/m³.", "tag": "", "marks": "", "flat": [{"t": "Volume of the room = __B1__ m³", "a": {"B1": "90"}}, {"t": "Mass of air in it = __B1__ kg", "a": {"B1": "108"}}, {"t": "Weight of that air = __B1__ N", "a": {"B1": "1080"}}], "sol": "6.0 × 5.0 × 3.0 = 90 m³.\n1.2 × 90 = 108 kg.\n108 × 10 = 1080 N.", "tools": ["calc"]}, {"kind": "blank", "p": "Cooking oil has a density of 800 kg/m³.", "tag": "", "marks": "", "flat": [{"t": "Mass of 2.0 L (0.0020 m³) of oil = __B1__ kg", "a": {"B1": "1.6"}}, {"t": "Volume of 3.0 kg of oil = __B1__ m³", "a": {"B1": "0.00375"}}, {"t": "Oil poured on water ends up on __B1__ (top / the bottom).", "a": {"B1": "top"}, "expr": "words", "accept": ["the top", "above"]}], "sol": "800 × 0.0020 = 1.6 kg.\n3.0 ÷ 800 = 0.00375 m³ (3.75 L).\nLess dense fluid floats on top.", "tools": ["calc"]}]}, {"id": "s2", "label": "8.2.A", "sub": "Pressure from a force — LO 8.2.A: describe the pressure exerted on a surface by a given force.", "slides": [{"kind": "mcq", "text": "Pressure is defined as", "opts": ["area ÷ force", "force × area", "force per unit volume", "the perpendicular force per unit area"], "correct": 3, "tag": "", "sol": "P = F⊥ ÷ A."}, {"kind": "mcq", "text": "Pressure is", "opts": ["a scalar", "a vector along the force", "a vector that always points up", "a vector that always points down"], "correct": 0, "tag": "", "sol": "Pressure has no direction; the force it produces on a surface is perpendicular to that surface."}, {"kind": "mcq", "text": "A force of 50 N acts perpendicularly on an area of 0.25 m². The pressure is", "opts": ["200 Pa", "0.005 Pa", "50.25 Pa", "12.5 Pa"], "correct": 0, "tag": "", "sol": "50 ÷ 0.25 = 200 Pa."}, {"kind": "mcq", "text": "The same force is spread over half the area. The pressure", "opts": ["quadruples", "halves", "stays the same", "doubles"], "correct": 3, "tag": "", "sol": "P ∝ 1/A."}, {"kind": "mcq", "text": "Why do snowshoes stop a walker sinking into soft snow?", "opts": ["They increase the pressure on the snow", "They reduce the walker's weight", "They make the snow denser", "They spread the weight over a larger area, reducing the pressure"], "correct": 3, "tag": "", "sol": "Same force, larger area, smaller pressure."}, {"kind": "mcq", "text": "A 45 kg student stands on one foot of area 0.015 m². The pressure on the floor is", "opts": ["3.0 × 10⁴ Pa", "3.0 × 10⁵ Pa", "3.0 × 10³ Pa", "6.75 Pa"], "correct": 0, "tag": "", "sol": "Weight 450 N: 450 ÷ 0.015 = 30 000 Pa.", "tools": ["calc"]}, {"kind": "mcq", "text": "A 100 N force pushes on a 0.50 m² surface at 30° to the surface. The pressure is", "opts": ["200 Pa", "100 Pa", "173 Pa", "50 Pa"], "correct": 1, "tag": "", "sol": "F⊥ = 100 sin 30° = 50 N; 50 ÷ 0.50 = 100 Pa.", "tools": ["calc"]}, {"kind": "mcq", "text": "A hydraulic lift has pistons of area 0.010 m² and 0.50 m². A 200 N push on the small piston can support", "opts": ["10 000 N", "4 N", "200 N", "100 N"], "correct": 0, "tag": "", "sol": "Same pressure: F₂ = 200 × 0.50 ÷ 0.010 = 10 000 N.", "fig": "<svg class=\"figsvg\" viewBox=\"0 0 300 160\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><path d=\"M40,60 L70,60 L70,116 L200,116 L200,40 L280,40 L280,146 L40,146 Z\" style=\"fill:var(--accent-text);fill-opacity:.16\"/><path d=\"M40,30 L40,146 L280,146 L280,20 M200,20 L200,116 L70,116 L70,30\" style=\"fill:none;stroke:var(--ink);stroke-width:2\"/><rect x=\"40\" y=\"54\" width=\"30\" height=\"8\" style=\"fill:var(--ink-soft)\"/><rect x=\"200\" y=\"34\" width=\"80\" height=\"8\" style=\"fill:var(--ink-soft)\"/><line style=\"stroke:var(--danger);stroke-width:2.2\" x1=\"55.0\" y1=\"14.0\" x2=\"55.0\" y2=\"50.0\" marker-end=\"url(#ah)\"/><text x=\"47.0\" y=\"20.0\" text-anchor=\"end\" dominant-baseline=\"middle\" style=\"fill:var(--danger);font:700 12px 'Source Sans 3',sans-serif\">F₁</text><line style=\"stroke:var(--success);stroke-width:2.2\" x1=\"240.0\" y1=\"30.0\" x2=\"240.0\" y2=\"4.0\" marker-end=\"url(#ah)\"/><text x=\"250.0\" y=\"12.0\" text-anchor=\"start\" dominant-baseline=\"middle\" style=\"fill:var(--success);font:700 12px 'Source Sans 3',sans-serif\">F₂</text><text class=\"lb\" x=\"55.0\" y=\"72.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">A₁</text><text class=\"lb\" x=\"240.0\" y=\"56.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">A₂</text></svg>"}, {"kind": "blank", "p": "A 2.0 kg brick measures 0.20 m × 0.10 m × 0.05 m.", "tag": "", "marks": "", "flat": [{"t": "Weight = __B1__ N", "a": {"B1": "20"}}, {"t": "Pressure when it rests on its largest face = __B1__ Pa", "a": {"B1": "1000"}}, {"t": "Pressure when it rests on its smallest face = __B1__ Pa", "a": {"B1": "4000"}}], "sol": "2.0 × 10 = 20 N.\n20 ÷ (0.20 × 0.10) = 1000 Pa.\n20 ÷ (0.10 × 0.05) = 4000 Pa.", "tools": ["calc"]}, {"kind": "blank", "p": "A car jack has pistons of area 5.0 cm² and 250 cm². The large piston supports 15 000 N.", "tag": "", "marks": "", "flat": [{"t": "Pressure in the oil = __B1__ Pa", "a": {"B1": "600000"}}, {"t": "Force needed on the small piston = __B1__ N", "a": {"B1": "300"}}, {"t": "The small piston must move __B1__ times as far as the large one.", "a": {"B1": "50"}}], "sol": "15 000 ÷ 0.025 = 6.0 × 10⁵ Pa.\n6.0 × 10⁵ × 5.0 × 10⁻⁴ = 300 N.\nEqual volumes move: 250 ÷ 5.0 = 50.", "fig": "<svg class=\"figsvg\" viewBox=\"0 0 300 160\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><path d=\"M40,60 L70,60 L70,116 L200,116 L200,40 L280,40 L280,146 L40,146 Z\" style=\"fill:var(--accent-text);fill-opacity:.16\"/><path d=\"M40,30 L40,146 L280,146 L280,20 M200,20 L200,116 L70,116 L70,30\" style=\"fill:none;stroke:var(--ink);stroke-width:2\"/><rect x=\"40\" y=\"54\" width=\"30\" height=\"8\" style=\"fill:var(--ink-soft)\"/><rect x=\"200\" y=\"34\" width=\"80\" height=\"8\" style=\"fill:var(--ink-soft)\"/><line style=\"stroke:var(--danger);stroke-width:2.2\" x1=\"55.0\" y1=\"14.0\" x2=\"55.0\" y2=\"50.0\" marker-end=\"url(#ah)\"/><text x=\"47.0\" y=\"20.0\" text-anchor=\"end\" dominant-baseline=\"middle\" style=\"fill:var(--danger);font:700 12px 'Source Sans 3',sans-serif\">F₁</text><line style=\"stroke:var(--success);stroke-width:2.2\" x1=\"240.0\" y1=\"30.0\" x2=\"240.0\" y2=\"4.0\" marker-end=\"url(#ah)\"/><text x=\"250.0\" y=\"12.0\" text-anchor=\"start\" dominant-baseline=\"middle\" style=\"fill:var(--success);font:700 12px 'Source Sans 3',sans-serif\">F₂</text><text class=\"lb\" x=\"55.0\" y=\"72.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">A₁</text><text class=\"lb\" x=\"240.0\" y=\"56.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">A₂</text></svg>", "tools": ["calc"]}, {"kind": "blank", "p": "A carpenter pushes a nail with 40 N. The tip has area 1.0 × 10⁻⁷ m²; the head has area 1.0 × 10⁻⁴ m².", "tag": "", "marks": "", "flat": [{"t": "Pressure at the tip = __B1__ Pa", "a": {"B1": "400000000"}, "accept": ["4e8", "4*10^8"]}, {"t": "Pressure on the thumb (head) = __B1__ Pa", "a": {"B1": "400000"}, "accept": ["4e5", "4*10^5"]}, {"t": "Tip pressure ÷ head pressure = __B1__", "a": {"B1": "1000"}}], "sol": "40 ÷ 1.0 × 10⁻⁷ = 4.0 × 10⁸ Pa.\n40 ÷ 1.0 × 10⁻⁴ = 4.0 × 10⁵ Pa.\nArea ratio 1000.", "tools": ["calc"]}]}, {"id": "s3", "label": "8.2.B", "sub": "Pressure in a fluid — LO 8.2.B: describe the pressure exerted by a fluid.", "slides": [{"kind": "mcq", "text": "What is the gauge pressure 5.0 m below the surface of a lake?", "opts": ["1.5 × 10⁵ Pa", "5.0 × 10⁴ Pa", "5.0 × 10³ Pa", "500 Pa"], "correct": 1, "tag": "", "sol": "ρgh = 1000 × 10 × 5.0 = 5.0 × 10⁴ Pa.", "tools": ["calc"]}, {"kind": "mcq", "text": "What is the absolute pressure 5.0 m below the surface of a lake (P₀ = 1.0 × 10⁵ Pa)?", "opts": ["5.0 × 10⁴ Pa", "1.0 × 10⁵ Pa", "5.0 × 10⁵ Pa", "1.5 × 10⁵ Pa"], "correct": 3, "tag": "", "sol": "P₀ + ρgh = 1.0 × 10⁵ + 0.5 × 10⁵.", "tools": ["calc"]}, {"kind": "mcq", "text": "Three open containers of different shapes are filled with water to the same depth. The pressure at the bottom is", "opts": ["greatest in the one with most water", "greatest in the narrowest", "greatest in the widest", "the same in all three"], "correct": 3, "tag": "", "sol": "Pressure depends only on depth (and ρ, g, P₀)."}, {"kind": "mcq", "text": "In the tank shown, how do the pressures at Y and Z compare?", "opts": ["greater at Y", "greater at Z", "it depends on the tank's width", "equal"], "correct": 3, "tag": "", "sol": "Same depth in the same connected fluid at rest.", "fig": "<svg class=\"figsvg\" viewBox=\"0 0 300 190\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><text class=\"lb\" x=\"150.0\" y=\"10.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">Open tank of water</text><rect x=\"60\" y=\"44.0\" width=\"180\" height=\"130.0\" style=\"fill:var(--accent-text);fill-opacity:.16\"/><polyline points=\"60,34 60,174 240,174 240,34\" style=\"fill:none;stroke:var(--ink);stroke-width:2\"/><line x1=\"60\" y1=\"44\" x2=\"240\" y2=\"44\" style=\"stroke:var(--accent-text);stroke-width:1.4\"/><circle cx=\"123.0\" cy=\"44.0\" r=\"3.5\" style=\"fill:var(--danger)\"/><text class=\"lb\" x=\"131.0\" y=\"44.0\" text-anchor=\"start\" dominant-baseline=\"middle\">X</text><circle cx=\"123.0\" cy=\"109.0\" r=\"3.5\" style=\"fill:var(--danger)\"/><text class=\"lb\" x=\"131.0\" y=\"109.0\" text-anchor=\"start\" dominant-baseline=\"middle\">Y</text><circle cx=\"195.0\" cy=\"109.0\" r=\"3.5\" style=\"fill:var(--danger)\"/><text class=\"lb\" x=\"203.0\" y=\"109.0\" text-anchor=\"start\" dominant-baseline=\"middle\">Z</text><circle cx=\"159.0\" cy=\"161.0\" r=\"3.5\" style=\"fill:var(--danger)\"/><text class=\"lb\" x=\"167.0\" y=\"161.0\" text-anchor=\"start\" dominant-baseline=\"middle\">W</text></svg>"}, {"kind": "mcq", "text": "The depth below the surface of a lake is doubled. The gauge pressure", "opts": ["doubles, but the absolute pressure less than doubles", "quadruples", "and the absolute pressure both double", "stays the same"], "correct": 0, "tag": "", "sol": "ρgh doubles; P₀ + ρgh does not."}, {"kind": "mcq", "text": "What is the gauge pressure 2.0 m down in oil of density 800 kg/m³?", "opts": ["8.0 × 10⁴ Pa", "1.6 × 10⁴ Pa", "1.6 × 10³ Pa", "2.0 × 10⁴ Pa"], "correct": 1, "tag": "", "sol": "800 × 10 × 2.0 = 16 000 Pa.", "tools": ["calc"]}, {"kind": "mcq", "text": "Why is a dam wall built thicker at the bottom?", "opts": ["The water is denser at the bottom", "The water pressure increases with depth", "Pressure is a vector pointing down", "The top holds more water"], "correct": 1, "tag": "", "sol": "P = P₀ + ρgh grows with h."}, {"kind": "mcq", "text": "In the tank shown, where is the pressure greatest?", "opts": ["Y", "W", "Z", "X"], "correct": 1, "tag": "", "sol": "W is deepest.", "fig": "<svg class=\"figsvg\" viewBox=\"0 0 300 190\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><text class=\"lb\" x=\"150.0\" y=\"10.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">Open tank of water</text><rect x=\"60\" y=\"44.0\" width=\"180\" height=\"130.0\" style=\"fill:var(--accent-text);fill-opacity:.16\"/><polyline points=\"60,34 60,174 240,174 240,34\" style=\"fill:none;stroke:var(--ink);stroke-width:2\"/><line x1=\"60\" y1=\"44\" x2=\"240\" y2=\"44\" style=\"stroke:var(--accent-text);stroke-width:1.4\"/><circle cx=\"123.0\" cy=\"44.0\" r=\"3.5\" style=\"fill:var(--danger)\"/><text class=\"lb\" x=\"131.0\" y=\"44.0\" text-anchor=\"start\" dominant-baseline=\"middle\">X</text><circle cx=\"123.0\" cy=\"109.0\" r=\"3.5\" style=\"fill:var(--danger)\"/><text class=\"lb\" x=\"131.0\" y=\"109.0\" text-anchor=\"start\" dominant-baseline=\"middle\">Y</text><circle cx=\"195.0\" cy=\"109.0\" r=\"3.5\" style=\"fill:var(--danger)\"/><text class=\"lb\" x=\"203.0\" y=\"109.0\" text-anchor=\"start\" dominant-baseline=\"middle\">Z</text><circle cx=\"159.0\" cy=\"161.0\" r=\"3.5\" style=\"fill:var(--danger)\"/><text class=\"lb\" x=\"167.0\" y=\"161.0\" text-anchor=\"start\" dominant-baseline=\"middle\">W</text></svg>"}, {"kind": "blank", "p": "A swimming pool is 2.5 m deep. P₀ = 1.0 × 10⁵ Pa.", "tag": "", "marks": "", "flat": [{"t": "Gauge pressure at the bottom = __B1__ Pa", "a": {"B1": "25000"}}, {"t": "Absolute pressure at the bottom = __B1__ Pa", "a": {"B1": "125000"}}, {"t": "Force of the water (gauge) on a 0.40 m² drain cover = __B1__ N", "a": {"B1": "10000"}}], "sol": "1000 × 10 × 2.5 = 25 000 Pa.\n100 000 + 25 000 = 125 000 Pa.\n25 000 × 0.40 = 10 000 N.", "tools": ["calc"]}, {"kind": "blank", "p": "A diver descends in sea water (ρ = 1030 kg/m³).", "tag": "", "marks": "", "flat": [{"t": "Gauge pressure at 20 m = __B1__ Pa", "a": {"B1": "206000"}}, {"t": "Absolute pressure at 20 m = __B1__ Pa", "a": {"B1": "306000"}}, {"t": "Depth where the absolute pressure is twice P₀ = __B1__ m", "a": {"B1": "9.71"}, "expr": "approx"}], "sol": "1030 × 10 × 20 = 206 000 Pa.\n100 000 + 206 000 = 306 000 Pa.\nρgh = 1.0 × 10⁵: h = 10⁵ ÷ 10 300 ≈ 9.71 m.", "tools": ["calc"]}, {"kind": "blank", "p": "A tank holds 1.2 m of water with 0.50 m of oil (ρ = 800 kg/m³) floating on top.", "tag": "", "marks": "", "flat": [{"t": "Gauge pressure at the oil–water boundary = __B1__ Pa", "a": {"B1": "4000"}}, {"t": "Gauge pressure at the bottom of the tank = __B1__ Pa", "a": {"B1": "16000"}}], "sol": "800 × 10 × 0.50 = 4000 Pa.\n4000 + 1000 × 10 × 1.2 = 16 000 Pa.", "fig": "<svg class=\"figsvg\" viewBox=\"0 0 300 190\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><text class=\"lb\" x=\"150.0\" y=\"10.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">Oil on water</text><rect x=\"60\" y=\"44.0\" width=\"180\" height=\"37.7\" style=\"fill:var(--gold);fill-opacity:.35\"/><text class=\"po\" x=\"232.0\" y=\"62.8\" text-anchor=\"end\" dominant-baseline=\"middle\">oil</text><rect x=\"60\" y=\"81.7\" width=\"180\" height=\"92.3\" style=\"fill:var(--accent-text);fill-opacity:.16\"/><text class=\"po\" x=\"232.0\" y=\"127.8\" text-anchor=\"end\" dominant-baseline=\"middle\">water</text><polyline points=\"60,34 60,174 240,174 240,34\" style=\"fill:none;stroke:var(--ink);stroke-width:2\"/><line x1=\"60\" y1=\"44\" x2=\"240\" y2=\"44\" style=\"stroke:var(--accent-text);stroke-width:1.4\"/></svg>", "tools": ["calc"]}]}, {"id": "s4", "label": "8.3.A", "sub": "Fluids and Newton's laws — LO 8.3.A: describe the conditions under which a fluid's velocity changes.", "slides": [{"kind": "mcq", "text": "Water flowing along a horizontal pipe speeds up. What must be true?", "opts": ["The pressure is the same everywhere", "The pressure in front is greater than behind", "No forces act on the water", "The pressure behind it is greater than the pressure in front"], "correct": 3, "tag": "", "sol": "A velocity change needs a net force; here it comes from a pressure difference."}, {"kind": "mcq", "text": "A small cube of water is at rest inside a tank. Which is true?", "opts": ["The pushes from above and below are equal", "The push from above is greater", "There are no forces on it", "The upward push from the water below is greater than the downward push from the water above"], "correct": 3, "tag": "", "sol": "The difference supports the cube's weight."}, {"kind": "mcq", "text": "Air in a horizontal tube has pressure 101 kPa at the left end and 100 kPa at the right. Initially at rest, the air", "opts": ["accelerates to the left", "moves upward", "stays at rest", "accelerates to the right"], "correct": 3, "tag": "", "sol": "The net force points from high to low pressure."}, {"kind": "mcq", "text": "An ideal fluid moves at constant velocity through a straight horizontal pipe of constant width. Then", "opts": ["the pressure is the same at both ends", "the pressure is higher at the far end", "the pressure must be zero", "the fluid must be accelerating"], "correct": 0, "tag": "", "sol": "Constant velocity: net force zero, so no pressure difference."}, {"kind": "mcq", "text": "A syringe plunger of area 2.0 × 10⁻⁴ m² is pushed with 6.0 N. The extra pressure in the liquid is", "opts": ["6.0 Pa", "3.0 × 10⁴ Pa", "1.2 × 10⁻³ Pa", "3.3 × 10⁻⁵ Pa"], "correct": 1, "tag": "", "sol": "6.0 ÷ 2.0 × 10⁻⁴ = 30 000 Pa.", "tools": ["calc"]}, {"kind": "mcq", "text": "Wind blows from regions of high air pressure towards low pressure because", "opts": ["high-pressure air has no mass", "the pressure difference produces a net force on the air", "air always moves downhill", "low pressure is heavier"], "correct": 1, "tag": "", "sol": "Newton's second law applied to a parcel of air."}, {"kind": "mcq", "text": "Water pushes on a dam with a force F. By Newton's third law, the dam pushes on the water with", "opts": ["a force F in the opposite direction", "zero force", "a force smaller than F", "a force larger than F"], "correct": 0, "tag": "", "sol": "Interaction forces are equal and opposite."}, {"kind": "mcq", "text": "A 0.020 kg parcel of fluid has an acceleration of 5.0 m/s². The net force on it is", "opts": ["250 N", "4.0 N", "0.10 N", "0.004 N"], "correct": 2, "tag": "", "sol": "F = ma = 0.020 × 5.0 = 0.10 N."}, {"kind": "blank", "p": "A cube of water of side 0.10 m (mass 1.0 kg) is at rest in a tank with its top face 0.20 m below the surface. Use gauge pressures.", "tag": "", "marks": "", "flat": [{"t": "Pressure on the top face = __B1__ Pa", "a": {"B1": "2000"}}, {"t": "Pressure on the bottom face = __B1__ Pa", "a": {"B1": "3000"}}, {"t": "Net upward force from the pressure difference = __B1__ N", "a": {"B1": "10"}}, {"t": "Does this balance the cube's weight? __B1__ (yes / no)", "a": {"B1": "yes"}, "expr": "words", "accept": ["y"]}], "sol": "1000 × 10 × 0.20 = 2000 Pa.\n1000 × 10 × 0.30 = 3000 Pa.\n(3000 − 2000) × 0.010 = 10 N.\nWeight = 1.0 × 10 = 10 N: yes, so the cube stays at rest.", "tools": ["calc"]}, {"kind": "blank", "p": "A 4.0 kg slug of water fills a horizontal pipe of area 0.0080 m². The pressure behind it is 1500 Pa greater than in front of it.", "tag": "", "marks": "", "flat": [{"t": "Net force on the slug = __B1__ N", "a": {"B1": "12"}}, {"t": "Its acceleration = __B1__ m/s²", "a": {"B1": "3"}}, {"t": "It accelerates towards the __B1__ pressure (higher / lower).", "a": {"B1": "lower"}, "expr": "words", "accept": ["low"]}], "sol": "1500 × 0.0080 = 12 N.\n12 ÷ 4.0 = 3.0 m/s².\nNet force points from high to low pressure.", "tools": ["calc"]}, {"kind": "blank", "p": "Water flows steadily along a horizontal pipe that narrows and then widens again.", "tag": "", "marks": "", "flat": [{"t": "In the narrow part the water is __B1__ (faster / slower).", "a": {"B1": "faster"}, "expr": "words", "accept": ["quicker"]}, {"t": "So between the wide and the narrow part it was pushed forward: the pressure in the narrow part is __B1__ (higher / lower).", "a": {"B1": "lower"}, "expr": "words", "accept": ["low", "less"]}, {"t": "Where it widens again it slows, so the pressure there is __B1__ (higher / lower) than in the narrow part.", "a": {"B1": "higher"}, "expr": "words", "accept": ["high", "greater", "more"]}], "sol": "The same volume per second passes a smaller area.\nSpeeding up needs a forward net force: lower pressure ahead.\nSlowing down needs a backward net force: higher pressure ahead."}]}, {"id": "s5", "label": "8.3.B (i)", "sub": "Buoyant force — LO 8.3.B: describe the buoyant force exerted on an object interacting with a fluid.", "slides": [{"kind": "mcq", "text": "Archimedes' principle says the buoyant force on an object equals", "opts": ["the weight of the object", "the pressure at its depth", "the object's volume times its density", "the weight of the fluid it displaces"], "correct": 3, "tag": "", "sol": "F_b = ρ_fluid V_disp g."}, {"kind": "mcq", "text": "What causes the buoyant force?", "opts": ["Surface tension", "The fluid pressure on the bottom of the object is greater than on its top", "The object's weight", "Air trapped in the fluid"], "correct": 1, "tag": "", "sol": "Pressure increases with depth, giving a net upward force."}, {"kind": "mcq", "text": "A block of volume 0.0020 m³ is completely under water. The buoyant force on it is", "opts": ["0.020 N", "2.0 N", "20 N", "200 N"], "correct": 2, "tag": "", "sol": "1000 × 0.0020 × 10 = 20 N.", "tools": ["calc"]}, {"kind": "mcq", "text": "An iron ball and an aluminium ball of the same volume are both fully under water. The buoyant force is", "opts": ["greater on the iron ball", "zero on the iron ball because it sinks", "greater on the aluminium ball", "the same on both"], "correct": 3, "tag": "", "sol": "Same displaced volume, same fluid."}, {"kind": "mcq", "text": "A fully submerged stone is lowered from 1 m to 3 m below the surface. The buoyant force", "opts": ["triples", "stays the same", "decreases", "increases a little"], "correct": 1, "tag": "", "sol": "Both top and bottom pressures rise equally; the difference (and ρVg) is unchanged."}, {"kind": "mcq", "text": "The same fully submerged object is moved from fresh water to salt water. The buoyant force", "opts": ["decreases", "becomes zero", "increases", "stays the same"], "correct": 2, "tag": "", "sol": "Salt water is denser: ρVg is larger."}, {"kind": "mcq", "text": "The buoyant force on an object always points", "opts": ["downward", "towards the side of the container", "upward, opposite to gravity", "in the direction of motion"], "correct": 2, "tag": "", "sol": "It is a net upward force."}, {"kind": "mcq", "text": "A 0.0040 m³ block floats with half its volume under water. The buoyant force is", "opts": ["20 N", "40 N", "2.0 N", "0.20 N"], "correct": 0, "tag": "", "sol": "V_disp = 0.0020 m³: 1000 × 0.0020 × 10 = 20 N.", "tools": ["calc"]}, {"kind": "blank", "p": "A 2.0 kg stone of volume 6.0 × 10⁻⁴ m³ hangs from a string, fully under water.", "tag": "", "marks": "", "flat": [{"t": "Weight = __B1__ N", "a": {"B1": "20"}}, {"t": "Buoyant force = __B1__ N", "a": {"B1": "6"}}, {"t": "Tension in the string = __B1__ N", "a": {"B1": "14"}}], "sol": "2.0 × 10 = 20 N.\n1000 × 6.0 × 10⁻⁴ × 10 = 6.0 N.\nEquilibrium: T + F_b = mg, T = 20 − 6.0 = 14 N.", "fig": "<svg class=\"figsvg\" viewBox=\"0 0 280 190\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><rect x=\"30\" y=\"66\" width=\"220\" height=\"112\" style=\"fill:var(--accent-text);fill-opacity:.16\"/><line x1=\"30\" y1=\"66\" x2=\"250\" y2=\"66\" style=\"stroke:var(--accent-text);stroke-width:1.4\"/><rect x=\"100.0\" y=\"96.0\" width=\"80\" height=\"56\" style=\"fill:var(--gold-soft);stroke:var(--ink);stroke-width:1.5\"/><line class=\"ln\" x1=\"140.0\" y1=\"10.0\" x2=\"140.0\" y2=\"96.0\"/><rect x=\"100.0\" y=\"4\" width=\"80\" height=\"6\" style=\"fill:var(--ink-soft)\"/><line style=\"stroke:var(--success);stroke-width:2.2\" x1=\"168.0\" y1=\"124.0\" x2=\"168.0\" y2=\"82.0\" marker-end=\"url(#ah)\"/><text x=\"176.0\" y=\"82.0\" text-anchor=\"start\" dominant-baseline=\"middle\" style=\"fill:var(--success);font:700 12px 'Source Sans 3',sans-serif\">T</text><line style=\"stroke:var(--accent-text);stroke-width:2.2\" x1=\"112.0\" y1=\"124.0\" x2=\"112.0\" y2=\"74.0\" marker-end=\"url(#ah)\"/><text x=\"104.0\" y=\"74.0\" text-anchor=\"end\" dominant-baseline=\"middle\" style=\"fill:var(--accent-text);font:700 12px 'Source Sans 3',sans-serif\">F_b</text><line style=\"stroke:var(--danger);stroke-width:2.2\" x1=\"140.0\" y1=\"124.0\" x2=\"140.0\" y2=\"172.0\" marker-end=\"url(#ah)\"/><text x=\"148.0\" y=\"168.0\" text-anchor=\"start\" dominant-baseline=\"middle\" style=\"fill:var(--danger);font:700 12px 'Source Sans 3',sans-serif\">mg</text></svg>", "tools": ["calc"]}, {"kind": "blank", "p": "A helium balloon of volume 0.012 m³ is released in still air (ρ = 1.2 kg/m³). The balloon and helium together have a mass of 0.010 kg.", "tag": "", "marks": "", "flat": [{"t": "Buoyant force = __B1__ N", "a": {"B1": "0.144"}, "expr": "approx"}, {"t": "Weight = __B1__ N", "a": {"B1": "0.1"}}, {"t": "Net upward force = __B1__ N", "a": {"B1": "0.044"}, "expr": "approx"}], "sol": "1.2 × 0.012 × 10 = 0.144 N.\n0.010 × 10 = 0.10 N.\n0.144 − 0.10 = 0.044 N upward.", "tools": ["calc"]}, {"kind": "blank", "p": "A cube of side 0.10 m is fully under water with its top face 0.30 m below the surface. Use gauge pressures.", "tag": "", "marks": "", "flat": [{"t": "Force on the top face = __B1__ N", "a": {"B1": "30"}}, {"t": "Force on the bottom face = __B1__ N", "a": {"B1": "40"}}, {"t": "Buoyant force = __B1__ N", "a": {"B1": "10"}}, {"t": "ρ_water V g = __B1__ N", "a": {"B1": "10"}}], "sol": "1000 × 10 × 0.30 × 0.010 = 30 N down.\n1000 × 10 × 0.40 × 0.010 = 40 N up.\n40 − 30 = 10 N up.\n1000 × 0.001 × 10 = 10 N: the two methods agree.", "tools": ["calc"]}]}, {"id": "s6", "label": "8.3.B (ii)", "sub": "Floating, sinking and apparent weight — LO 8.3.B: describe the buoyant force exerted on an object interacting with a fluid: floating objects and apparent weight.", "slides": [{"kind": "mcq", "text": "For an object floating at rest on water, the buoyant force is", "opts": ["less than its weight", "equal to the object's weight", "zero", "greater than its weight"], "correct": 1, "tag": "", "sol": "Floating in equilibrium: F_b = mg."}, {"kind": "mcq", "text": "A block of wood of density 700 kg/m³ floats in water. What fraction of it is under water?", "opts": ["0.70", "0.30", "1.4", "1.0"], "correct": 0, "tag": "", "sol": "ρ_object ÷ ρ_fluid = 700 ÷ 1000."}, {"kind": "mcq", "text": "An ice cube (900 kg/m³) floats in a glass of fresh water. What fraction of the cube is above the water?", "opts": ["0.090", "0.11", "0.10", "0.90"], "correct": 2, "tag": "", "sol": "Submerged fraction 900 ÷ 1000 = 0.90, so 0.10 is above."}, {"kind": "mcq", "text": "An object sinks in a fluid if", "opts": ["its mass is large", "it is made of metal", "its volume is small", "its average density is greater than the fluid's"], "correct": 3, "tag": "", "sol": "Compare densities, not masses."}, {"kind": "mcq", "text": "A steel ship floats although steel is denser than water because", "opts": ["the air pushes it up", "steel becomes lighter in water", "its hollow hull displaces a weight of water equal to the ship's weight", "sea water is denser than steel"], "correct": 2, "tag": "", "sol": "The ship's average density (steel + air inside) is less than water's."}, {"kind": "mcq", "text": "A spring scale reads 30 N for a metal block in air and 20 N when it is fully under water. The block's volume is", "opts": ["1.0 × 10⁻² m³", "3.0 × 10⁻³ m³", "2.0 × 10⁻³ m³", "1.0 × 10⁻³ m³"], "correct": 3, "tag": "", "sol": "F_b = 10 N = 1000 × V × 10.", "tools": ["calc"]}, {"kind": "mcq", "text": "A ship sails from a river (fresh water) into the sea (denser salt water). The ship", "opts": ["floats at the same level", "rises slightly higher in the water", "feels a smaller buoyant force", "sinks slightly lower"], "correct": 1, "tag": "", "sol": "F_b still equals its weight; denser water needs less displaced volume."}, {"kind": "mcq", "text": "Cargo is added to a boat, which still floats. The buoyant force on the boat", "opts": ["decreases", "increases, and the boat sits higher", "stays the same", "increases, and the boat sits lower"], "correct": 3, "tag": "", "sol": "F_b = new, larger weight, so more water is displaced."}, {"kind": "blank", "p": "A wooden block 0.20 m × 0.20 m × 0.10 m (density 600 kg/m³) floats with its 0.20 m × 0.20 m face horizontal.", "tag": "", "marks": "", "flat": [{"t": "Mass of the block = __B1__ kg", "a": {"B1": "2.4"}}, {"t": "Buoyant force = __B1__ N", "a": {"B1": "24"}}, {"t": "Volume under water = __B1__ m³", "a": {"B1": "0.0024"}}, {"t": "Depth of the block below the surface = __B1__ m", "a": {"B1": "0.06"}}], "sol": "600 × 0.004 = 2.4 kg.\nFloating: F_b = mg = 24 N.\n24 ÷ (1000 × 10) = 0.0024 m³.\n0.0024 ÷ 0.040 = 0.060 m.", "fig": "<svg class=\"figsvg\" viewBox=\"0 0 280 190\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><rect x=\"30\" y=\"66\" width=\"220\" height=\"112\" style=\"fill:var(--accent-text);fill-opacity:.16\"/><line x1=\"30\" y1=\"66\" x2=\"250\" y2=\"66\" style=\"stroke:var(--accent-text);stroke-width:1.4\"/><rect x=\"100.0\" y=\"43.6\" width=\"80\" height=\"56\" style=\"fill:var(--gold-soft);stroke:var(--ink);stroke-width:1.5\"/><line style=\"stroke:var(--accent-text);stroke-width:2.2\" x1=\"112.0\" y1=\"71.6\" x2=\"112.0\" y2=\"21.6\" marker-end=\"url(#ah)\"/><text x=\"104.0\" y=\"21.6\" text-anchor=\"end\" dominant-baseline=\"middle\" style=\"fill:var(--accent-text);font:700 12px 'Source Sans 3',sans-serif\">F_b</text><line style=\"stroke:var(--danger);stroke-width:2.2\" x1=\"140.0\" y1=\"71.6\" x2=\"140.0\" y2=\"119.6\" marker-end=\"url(#ah)\"/><text x=\"148.0\" y=\"115.6\" text-anchor=\"start\" dominant-baseline=\"middle\" style=\"fill:var(--danger);font:700 12px 'Source Sans 3',sans-serif\">mg</text></svg>", "tools": ["calc"]}, {"kind": "blank", "p": "A crown weighs 50.0 N in air and 46.8 N when hanging fully under water.", "tag": "", "marks": "", "flat": [{"t": "Buoyant force = __B1__ N", "a": {"B1": "3.2"}, "expr": "approx"}, {"t": "Volume of the crown = __B1__ m³", "a": {"B1": "0.00032"}, "expr": "approx"}, {"t": "Mass of the crown = __B1__ kg", "a": {"B1": "5"}}, {"t": "Density = __B1__ kg/m³", "a": {"B1": "15625"}, "expr": "approx"}, {"t": "Gold has density 19 300 kg/m³. Is the crown pure gold? __B1__ (yes / no)", "a": {"B1": "no"}, "expr": "words", "accept": ["n"]}], "sol": "50.0 − 46.8 = 3.2 N.\n3.2 ÷ (1000 × 10) = 3.2 × 10⁻⁴ m³.\n50.0 ÷ 10 = 5.0 kg.\n5.0 ÷ 3.2 × 10⁻⁴ ≈ 15 600 kg/m³.\n15 600 < 19 300: no.", "tools": ["calc"]}, {"kind": "blank", "p": "A raft is made from sealed plastic drums of total volume 0.40 m³. The raft's own mass is 60 kg.", "tag": "", "marks": "", "flat": [{"t": "Largest buoyant force (drums just fully under) = __B1__ N", "a": {"B1": "4000"}}, {"t": "Largest extra load it can carry = __B1__ kg", "a": {"B1": "340"}}], "sol": "1000 × 0.40 × 10 = 4000 N.\n4000 N supports 400 kg in total: 400 − 60 = 340 kg.", "tools": ["calc"]}]}, {"id": "s7", "label": "8.4.A", "sub": "Continuity: conservation of mass — LO 8.4.A: describe incompressible fluid flow through a cross-sectional area using mass conservation.", "slides": [{"kind": "mcq", "text": "The continuity equation A₁v₁ = A₂v₂ is a statement of the conservation of", "opts": ["pressure", "momentum", "energy", "mass"], "correct": 3, "tag": "", "sol": "For an incompressible fluid, mass in = mass out each second."}, {"kind": "mcq", "text": "A pipe's cross-sectional area halves. The speed of the water", "opts": ["stays the same", "quadruples", "halves", "doubles"], "correct": 3, "tag": "", "sol": "v ∝ 1/A."}, {"kind": "mcq", "text": "A pipe's diameter halves. The speed of the water", "opts": ["becomes 4 times as large", "doubles", "halves", "stays the same"], "correct": 0, "tag": "", "sol": "A ∝ d², so A becomes ¼."}, {"kind": "mcq", "text": "Water flows at 0.020 m³/s through a pipe of area 0.0040 m². Its speed is", "opts": ["5.0 m/s", "0.20 m/s", "50 m/s", "0.080 m/s"], "correct": 0, "tag": "", "sol": "v = 0.020 ÷ 0.0040 = 5.0 m/s.", "tools": ["calc"]}, {"kind": "mcq", "text": "Putting your thumb over the end of a garden hose makes the water squirt faster because", "opts": ["your thumb adds energy", "the water becomes denser", "the pressure in the tap rises", "the same flow rate must pass through a smaller area"], "correct": 3, "tag": "", "sol": "Av constant: smaller A, larger v."}, {"kind": "mcq", "text": "A smooth stream of water from a tap gets narrower as it falls because", "opts": ["water compresses as it falls", "air pressure squeezes it", "it speeds up, so its cross-section must shrink", "gravity pulls the sides inward"], "correct": 2, "tag": "", "sol": "Continuity: larger v, smaller A."}, {"kind": "mcq", "text": "A pipe splits into two identical branches, each with half the original area. In each branch the speed", "opts": ["is a quarter", "is half", "is the same as in the main pipe", "is double"], "correct": 2, "tag": "", "sol": "Total area unchanged: A·v = 2 × (A/2)·v."}, {"kind": "mcq", "text": "What is the unit of mass flow rate ρAv?", "opts": ["m³/s", "kg/s", "N/s", "kg/m³"], "correct": 1, "tag": "", "sol": "(kg/m³)(m²)(m/s) = kg/s."}, {"kind": "blank", "p": "Water flows through a pipe of area 0.030 m² at 1.2 m/s into a narrower section of area 0.0090 m².", "tag": "", "marks": "", "flat": [{"t": "Volume flow rate = __B1__ m³/s", "a": {"B1": "0.036"}}, {"t": "Speed in the narrow section = __B1__ m/s", "a": {"B1": "4"}}, {"t": "Mass flow rate = __B1__ kg/s", "a": {"B1": "36"}}], "sol": "0.030 × 1.2 = 0.036 m³/s.\n0.036 ÷ 0.0090 = 4.0 m/s.\n1000 × 0.036 = 36 kg/s.", "fig": "<svg class=\"figsvg\" viewBox=\"0 0 320 140\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><path d=\"M20,28 L120,28 L180,48 L300,48 L300,76 L180,76 L120,96 L20,96 Z\" style=\"fill:var(--accent-text);fill-opacity:.16\"/><path d=\"M20,28 L120,28 L180,48 L300,48\" style=\"fill:none;stroke:var(--ink);stroke-width:2\"/><path d=\"M20,96 L120,96 L180,76 L300,76\" style=\"fill:none;stroke:var(--ink);stroke-width:2\"/><line style=\"stroke:var(--accent-text);stroke-width:2.2\" x1=\"40.0\" y1=\"62.0\" x2=\"95.0\" y2=\"62.0\" marker-end=\"url(#ah)\"/><text x=\"65.0\" y=\"48.0\" text-anchor=\"start\" dominant-baseline=\"middle\" style=\"fill:var(--accent-text);font:700 12px 'Source Sans 3',sans-serif\">v₁</text><line style=\"stroke:var(--accent-text);stroke-width:2.2\" x1=\"205.0\" y1=\"62.0\" x2=\"270.0\" y2=\"62.0\" marker-end=\"url(#ah)\"/><text x=\"236.0\" y=\"36.0\" text-anchor=\"start\" dominant-baseline=\"middle\" style=\"fill:var(--accent-text);font:700 12px 'Source Sans 3',sans-serif\">v₂</text><text class=\"lb\" x=\"70.0\" y=\"84.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">A₁</text><text class=\"lb\" x=\"240.0\" y=\"88.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">A₂</text></svg>", "tools": ["calc"]}, {"kind": "blank", "p": "A garden hose of radius 1.0 cm carries water at 2.0 m/s.", "tag": "", "marks": "", "flat": [{"t": "Volume flow rate = __B1__ m³/s", "a": {"B1": "0.000628"}, "expr": "approx"}, {"t": "Time to fill a 20 L (0.020 m³) bucket = __B1__ s", "a": {"B1": "31.8"}, "expr": "approx"}, {"t": "Speed from a nozzle of radius 0.25 cm = __B1__ m/s", "a": {"B1": "32"}}], "sol": "π × 0.010² × 2.0 ≈ 6.28 × 10⁻⁴ m³/s.\n0.020 ÷ 6.28 × 10⁻⁴ ≈ 31.8 s.\nRadius ÷4, area ÷16: 2.0 × 16 = 32 m/s.", "tools": ["calc"]}, {"kind": "blank", "p": "Blood leaves the heart through the aorta (area 3.0 cm²) at 0.30 m/s. All the capillaries together have a cross-sectional area of 900 cm².", "tag": "", "marks": "", "flat": [{"t": "Flow rate = __B1__ cm³/s", "a": {"B1": "90"}}, {"t": "Average speed in the capillaries = __B1__ m/s", "a": {"B1": "0.001"}}, {"t": "The blood is __B1__ in the capillaries (faster / slower).", "a": {"B1": "slower"}, "expr": "words", "accept": ["slow"]}], "sol": "3.0 cm² × 30 cm/s = 90 cm³/s.\n0.30 × 3.0 ÷ 900 = 0.0010 m/s.\nMuch larger total area: slower.", "tools": ["calc"]}]}, {"id": "s8", "label": "8.4.B (i)", "sub": "Bernoulli's equation — LO 8.4.B: describe fluid flow resulting from energy differences between locations.", "slides": [{"kind": "mcq", "text": "Bernoulli's equation is a statement of the conservation of", "opts": ["mass in a flowing fluid", "momentum", "pressure", "energy in a flowing fluid"], "correct": 3, "tag": "", "sol": "Pressure work changes the kinetic and potential energy per unit volume."}, {"kind": "mcq", "text": "In a horizontal pipe, the pressure is lowest where", "opts": ["the fluid moves slowest", "the fluid is at rest", "the pipe is widest", "the fluid moves fastest"], "correct": 3, "tag": "", "sol": "P + ½ρv² is constant at one height."}, {"kind": "mcq", "text": "In Bernoulli's equation, the term ρgy represents", "opts": ["pressure due to speed", "mass per unit volume", "gravitational potential energy per unit volume", "kinetic energy per unit volume"], "correct": 2, "tag": "", "sol": "mgy ÷ V = ρgy."}, {"kind": "mcq", "text": "You blow gently between two sheets of paper hanging a few centimetres apart. The sheets", "opts": ["move apart", "stay still", "move towards each other", "both swing the same way as the air"], "correct": 2, "tag": "", "sol": "Fast-moving air between them has lower pressure than the still air outside."}, {"kind": "mcq", "text": "Water in a horizontal pipe speeds up from 2.0 m/s to 4.0 m/s. The pressure was 1.5 × 10⁵ Pa. It becomes", "opts": ["1.48 × 10⁵ Pa", "1.35 × 10⁵ Pa", "1.44 × 10⁵ Pa", "1.56 × 10⁵ Pa"], "correct": 2, "tag": "", "sol": "ΔP = ½ × 1000 × (16 − 4) = 6000 Pa lower.", "tools": ["calc"]}, {"kind": "mcq", "text": "Water flows at constant speed up a uniform pipe that rises 5.0 m. The pressure at the top is", "opts": ["5.0 × 10⁴ Pa lower than at the bottom", "5.0 × 10³ Pa lower", "5.0 × 10⁴ Pa higher", "the same"], "correct": 0, "tag": "", "sol": "v constant: ΔP = ρgΔy = 1000 × 10 × 5.0.", "tools": ["calc"]}, {"kind": "mcq", "text": "A strong wind can lift a roof off a house because", "opts": ["the fast air above the roof has lower pressure than the still air inside", "the air inside becomes denser", "the wind pushes the roof from below", "the wind makes the roof lighter"], "correct": 0, "tag": "", "sol": "Pressure difference × roof area = upward net force."}, {"kind": "mcq", "text": "Which assumptions are made when using Bernoulli's equation in AP Physics 1?", "opts": ["The fluid is compressible and viscous", "The pipe must be horizontal", "The fluid is a gas at rest", "The fluid is incompressible, non-viscous and in steady flow"], "correct": 3, "tag": "", "sol": "The ideal-fluid model; the pipe can change height."}, {"kind": "blank", "p": "Water enters a horizontal Venturi tube through area 0.012 m² at 1.5 m/s and 1.8 × 10⁵ Pa. The throat has area 0.0040 m².", "tag": "", "marks": "", "flat": [{"t": "Speed in the throat = __B1__ m/s", "a": {"B1": "4.5"}}, {"t": "Pressure drop = __B1__ Pa", "a": {"B1": "9000"}}, {"t": "Pressure in the throat = __B1__ Pa", "a": {"B1": "171000"}}], "sol": "0.012 × 1.5 ÷ 0.0040 = 4.5 m/s.\n½ × 1000 × (4.5² − 1.5²) = 9000 Pa.\n180 000 − 9000 = 171 000 Pa.", "fig": "<svg class=\"figsvg\" viewBox=\"0 0 320 140\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><path d=\"M20,28 L120,28 L180,48 L300,48 L300,76 L180,76 L120,96 L20,96 Z\" style=\"fill:var(--accent-text);fill-opacity:.16\"/><path d=\"M20,28 L120,28 L180,48 L300,48\" style=\"fill:none;stroke:var(--ink);stroke-width:2\"/><path d=\"M20,96 L120,96 L180,76 L300,76\" style=\"fill:none;stroke:var(--ink);stroke-width:2\"/><line style=\"stroke:var(--accent-text);stroke-width:2.2\" x1=\"40.0\" y1=\"62.0\" x2=\"95.0\" y2=\"62.0\" marker-end=\"url(#ah)\"/><text x=\"65.0\" y=\"48.0\" text-anchor=\"start\" dominant-baseline=\"middle\" style=\"fill:var(--accent-text);font:700 12px 'Source Sans 3',sans-serif\">v₁</text><line style=\"stroke:var(--accent-text);stroke-width:2.2\" x1=\"205.0\" y1=\"62.0\" x2=\"270.0\" y2=\"62.0\" marker-end=\"url(#ah)\"/><text x=\"236.0\" y=\"36.0\" text-anchor=\"start\" dominant-baseline=\"middle\" style=\"fill:var(--accent-text);font:700 12px 'Source Sans 3',sans-serif\">v₂</text><text class=\"lb\" x=\"70.0\" y=\"84.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">1</text><text class=\"lb\" x=\"240.0\" y=\"88.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">2</text></svg>", "tools": ["calc"]}, {"kind": "blank", "p": "Water enters a building at ground level at 3.0 m/s and 3.0 × 10⁵ Pa. On a floor 6.0 m higher the pipe is narrower and the speed is 4.0 m/s.", "tag": "", "marks": "", "flat": [{"t": "Pressure drop due to height = __B1__ Pa", "a": {"B1": "60000"}}, {"t": "Pressure drop due to speeding up = __B1__ Pa", "a": {"B1": "3500"}}, {"t": "Pressure on the upper floor = __B1__ Pa", "a": {"B1": "236500"}}], "sol": "ρgΔy = 1000 × 10 × 6.0 = 60 000 Pa.\n½ × 1000 × (16 − 9) = 3500 Pa.\n300 000 − 60 000 − 3500 = 236 500 Pa.", "fig": "<svg class=\"figsvg\" viewBox=\"0 0 320 160\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><path d=\"M20,48 L120,48 L180,28 L300,28 L300,56 L180,56 L120,116 L20,116 Z\" style=\"fill:var(--accent-text);fill-opacity:.16\"/><path d=\"M20,48 L120,48 L180,28 L300,28\" style=\"fill:none;stroke:var(--ink);stroke-width:2\"/><path d=\"M20,116 L120,116 L180,56 L300,56\" style=\"fill:none;stroke:var(--ink);stroke-width:2\"/><line style=\"stroke:var(--accent-text);stroke-width:2.2\" x1=\"40.0\" y1=\"82.0\" x2=\"95.0\" y2=\"82.0\" marker-end=\"url(#ah)\"/><text x=\"65.0\" y=\"68.0\" text-anchor=\"start\" dominant-baseline=\"middle\" style=\"fill:var(--accent-text);font:700 12px 'Source Sans 3',sans-serif\">v₁</text><line style=\"stroke:var(--accent-text);stroke-width:2.2\" x1=\"205.0\" y1=\"42.0\" x2=\"270.0\" y2=\"42.0\" marker-end=\"url(#ah)\"/><text x=\"236.0\" y=\"16.0\" text-anchor=\"start\" dominant-baseline=\"middle\" style=\"fill:var(--accent-text);font:700 12px 'Source Sans 3',sans-serif\">v₂</text><text class=\"lb\" x=\"70.0\" y=\"104.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">1</text><text class=\"lb\" x=\"240.0\" y=\"68.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">2</text></svg>", "tools": ["calc"]}, {"kind": "blank", "p": "Wind blows at 30 m/s over a flat roof of area 100 m². The air inside is still. Air density 1.2 kg/m³.", "tag": "", "marks": "", "flat": [{"t": "Pressure difference = __B1__ Pa", "a": {"B1": "540"}}, {"t": "Net upward force on the roof = __B1__ N", "a": {"B1": "54000"}}, {"t": "The pressure is lower __B1__ the roof (above / below).", "a": {"B1": "above"}, "expr": "words", "accept": ["over", "on top"]}], "sol": "½ × 1.2 × 30² = 540 Pa.\n540 × 100 = 54 000 N.\nFast air above: lower pressure above.", "tools": ["calc"]}]}, {"id": "s9", "label": "8.4.B (ii)", "sub": "Torricelli's theorem and applications — LO 8.4.B: describe fluid flow resulting from energy differences between locations: flow from an opening.", "slides": [{"kind": "mcq", "text": "Water leaves a small hole 5.0 m below the surface of a large open tank at", "opts": ["7.1 m/s", "10 m/s", "50 m/s", "100 m/s"], "correct": 1, "tag": "", "sol": "v = √(2 × 10 × 5.0) = 10 m/s.", "tools": ["calc"]}, {"kind": "mcq", "text": "The hole is moved to 4 times the depth below the surface. The outflow speed", "opts": ["stays the same", "doubles", "halves", "becomes 4 times as large"], "correct": 1, "tag": "", "sol": "v ∝ √Δy."}, {"kind": "mcq", "text": "Torricelli's speed √(2gΔy) is the same as the speed of", "opts": ["any object in the tank", "sound in water", "an object falling freely through Δy from rest", "the water surface as it falls"], "correct": 2, "tag": "", "sol": "Energy per unit volume: ρgΔy → ½ρv²."}, {"kind": "mcq", "text": "An open tank has two small holes, one near the top and one near the bottom. Water leaves", "opts": ["the lower hole faster", "the upper hole faster", "both at the same speed", "only the lower hole"], "correct": 0, "tag": "", "sol": "The lower hole is deeper below the surface."}, {"kind": "mcq", "text": "As an open tank drains through a hole in its side, the speed of the jet", "opts": ["becomes zero immediately", "stays constant", "increases", "decreases"], "correct": 3, "tag": "", "sol": "The depth of the hole below the surface decreases."}, {"kind": "mcq", "text": "Water and oil are each 2.0 m above a hole in two open tanks. Compared with the water, the oil leaves", "opts": ["at the same speed", "slower, because it is less dense", "faster, because it is less dense", "faster, because it is more viscous"], "correct": 0, "tag": "", "sol": "v = √(2gΔy) does not contain ρ."}, {"kind": "mcq", "text": "A water tank on a roof is 20 m above an open tap. Ignoring friction, the water leaves the tap at", "opts": ["14 m/s", "20 m/s", "400 m/s", "200 m/s"], "correct": 1, "tag": "", "sol": "√(2 × 10 × 20) = 20 m/s.", "tools": ["calc"]}, {"kind": "blank", "p": "A hole in the side of an open tank is 1.8 m below the water surface and 0.45 m above the floor.", "tag": "", "marks": "", "flat": [{"t": "Speed of the water leaving the hole = __B1__ m/s", "a": {"B1": "6"}}, {"t": "Time for the jet to fall to the floor = __B1__ s", "a": {"B1": "0.3"}}, {"t": "Distance from the tank to where the jet lands = __B1__ m", "a": {"B1": "1.8"}}], "sol": "√(2 × 10 × 1.8) = √36 = 6.0 m/s.\n0.45 = 5t², t = 0.30 s.\n6.0 × 0.30 = 1.8 m.", "fig": "<svg class=\"figsvg\" viewBox=\"0 0 300 200\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><rect x=\"40\" y=\"34\" width=\"90\" height=\"146\" style=\"fill:var(--accent-text);fill-opacity:.16\"/><polyline points=\"40,20 40,180 130,180 130,20\" style=\"fill:none;stroke:var(--ink);stroke-width:2\"/><line x1=\"40\" y1=\"34\" x2=\"130\" y2=\"34\" style=\"stroke:var(--accent-text);stroke-width:1.4\"/><line class=\"ln\" x1=\"20.0\" y1=\"180.0\" x2=\"294.0\" y2=\"180.0\"/><polyline points=\"130.0,120.0 131.5,120.0 133.0,120.0 134.5,120.1 136.0,120.1 137.5,120.2 139.0,120.2 140.5,120.3 142.0,120.4 143.5,120.6 145.0,120.7 146.5,120.8 148.0,121.0 149.5,121.2 151.0,121.3 152.5,121.5 154.0,121.8 155.5,122.0 157.0,122.2 158.5,122.5 160.0,122.8 161.5,123.0 163.0,123.3 164.5,123.6 166.0,124.0 167.5,124.3 169.0,124.7 170.5,125.0 172.0,125.4 173.5,125.8 175.0,126.2 176.5,126.6 178.0,127.1 179.5,127.5 181.0,128.0 182.5,128.4 184.0,128.9 185.5,129.4 187.0,129.9 188.5,130.5 190.0,131.0 191.5,131.6 193.0,132.2 194.5,132.7 196.0,133.3 197.5,133.9 199.0,134.6 200.5,135.2 202.0,135.9 203.5,136.5 205.0,137.2 206.5,137.9 208.0,138.6 209.5,139.3 211.0,140.1 212.5,140.8 214.0,141.6 215.5,142.4 217.0,143.2 218.5,144.0 220.0,144.8 221.5,145.6 223.0,146.5 224.5,147.3 226.0,148.2 227.5,149.1 229.0,150.0 230.5,150.9 232.0,151.8 233.5,152.8 235.0,153.8 236.5,154.7 238.0,155.7 239.5,156.7 241.0,157.7 242.5,158.7 244.0,159.8 245.5,160.8 247.0,161.9 248.5,163.0 250.0,164.1 251.5,165.2 253.0,166.3 254.5,167.4 256.0,168.6 257.5,169.8 259.0,170.9 260.5,172.1 262.0,173.3 263.5,174.6 265.0,175.8 266.5,177.0 268.0,178.3 269.5,179.6 271.0,180.9\" style=\"fill:none;stroke:var(--accent-text);stroke-width:3;stroke-dasharray:6 3\"/><line class=\"ln\" x1=\"58.0\" y1=\"34.0\" x2=\"58.0\" y2=\"120.0\" marker-end=\"url(#ah)\" marker-start=\"url(#ahs)\"/><text class=\"lb\" x=\"64.0\" y=\"77.0\" text-anchor=\"start\" dominant-baseline=\"middle\">1.8 m</text><line class=\"ln\" x1=\"144.0\" y1=\"120.0\" x2=\"144.0\" y2=\"180.0\" marker-end=\"url(#ah)\" marker-start=\"url(#ahs)\"/><text class=\"lb\" x=\"150.0\" y=\"160.0\" text-anchor=\"start\" dominant-baseline=\"middle\">0.45 m</text></svg>", "tools": ["calc", "desmos"], "desmos": ["y=0.45-5\\left(\\frac{x}{6}\\right)^2\\{0\\le x\\le1.8\\}"]}, {"kind": "blank", "p": "A hole of area 2.0 cm² is 0.80 m below the surface of a large open tank.", "tag": "", "marks": "", "flat": [{"t": "Outflow speed = __B1__ m/s", "a": {"B1": "4"}}, {"t": "Volume flow rate = __B1__ m³/s", "a": {"B1": "0.0008"}}, {"t": "Volume that flows out in one minute = __B1__ L", "a": {"B1": "48"}}], "sol": "√(2 × 10 × 0.80) = 4.0 m/s.\n2.0 × 10⁻⁴ × 4.0 = 8.0 × 10⁻⁴ m³/s.\n8.0 × 10⁻⁴ × 60 = 0.048 m³ = 48 L.", "tools": ["calc"]}, {"kind": "blank", "p": "A fountain nozzle shoots water straight up at 12 m/s.", "tag": "", "marks": "", "flat": [{"t": "Height the water reaches = __B1__ m", "a": {"B1": "7.2"}}, {"t": "Gauge pressure needed where the water is almost at rest at nozzle height = __B1__ Pa", "a": {"B1": "72000"}}], "sol": "v² = 2gh: 144 ÷ 20 = 7.2 m.\n½ρv² = ½ × 1000 × 144 = 72 000 Pa.", "tools": ["calc"]}]}, {"id": "s10", "label": "Test A", "sub": "Test A — Knowing and understanding", "slides": [{"kind": "mcq", "text": "Which statement about density is correct?", "opts": ["It is a property of the material, so a small and a large sample of pure water have the same density", "A larger sample of the same material has a larger density", "It is measured in kg/m²", "It is the weight of an object divided by its area"], "correct": 0, "tag": "", "sol": "ρ = m/V, in kg/m³; m and V scale together. [8.1.A]"}, {"kind": "mcq", "text": "A 3.0 kg liquid sample has a volume of 0.0025 m³. Its density is", "opts": ["0.83 kg/m³", "833 kg/m³", "1200 kg/m³", "7.5 × 10⁻³ kg/m³"], "correct": 2, "tag": "", "sol": "3.0 ÷ 0.0025 = 1200 kg/m³. [8.1.A]", "tools": ["calc"]}, {"kind": "mcq", "text": "The SI unit of pressure, the pascal, is equal to", "opts": ["kg/m³", "N·m", "J/s", "N/m²"], "correct": 3, "tag": "", "sol": "P = F ÷ A. [8.2.A]"}, {"kind": "mcq", "text": "What is the gauge pressure 12 m below the surface of fresh water?", "opts": ["1.2 × 10⁵ Pa", "1.2 × 10³ Pa", "2.2 × 10⁵ Pa", "1.2 × 10⁴ Pa"], "correct": 0, "tag": "", "sol": "1000 × 10 × 12. [8.2.B]", "tools": ["calc"]}, {"kind": "mcq", "text": "A fluid element's velocity changes only if", "opts": ["it is at rest", "the pressure is the same on all sides", "its density changes", "there is a net force on it, e.g. from a pressure difference"], "correct": 3, "tag": "", "sol": "Newton's second law. [8.3.A]"}, {"kind": "mcq", "text": "A 0.50 m³ object is fully submerged in sea water (1030 kg/m³). The buoyant force is", "opts": ["2060 N", "5150 N", "5000 N", "515 N"], "correct": 1, "tag": "", "sol": "1030 × 0.50 × 10. [8.3.B]", "tools": ["calc"]}, {"kind": "mcq", "text": "Water in a pipe of area 6.0 cm² moves at 2.0 m/s. In a section of area 2.0 cm² it moves at", "opts": ["2.0 m/s", "0.67 m/s", "6.0 m/s", "12 m/s"], "correct": 2, "tag": "", "sol": "6.0 × 2.0 ÷ 2.0. [8.4.A]"}, {"kind": "blank", "p": "Water at 3.0 m/s and 1.8 × 10⁵ Pa flows along a horizontal pipe into a section where its speed is 5.0 m/s.", "tag": "", "marks": "", "flat": [{"t": "Change in ½ρv² = __B1__ Pa", "a": {"B1": "8000"}}, {"t": "New pressure = __B1__ Pa", "a": {"B1": "172000"}}], "sol": "½ × 1000 × (25 − 9) = 8000 Pa.\n180 000 − 8000 = 172 000 Pa. [8.4.B]", "tools": ["calc"]}, {"kind": "blank", "p": "A 0.80 kg block of volume 1.0 × 10⁻³ m³ is placed in water.", "tag": "", "marks": "", "flat": [{"t": "Density of the block = __B1__ kg/m³", "a": {"B1": "800"}}, {"t": "It will __B1__ (float / sink).", "a": {"B1": "float"}, "expr": "words", "accept": ["floats"]}, {"t": "Buoyant force when it is at rest = __B1__ N", "a": {"B1": "8"}}, {"t": "Volume under water = __B1__ m³", "a": {"B1": "0.0008"}}], "sol": "0.80 ÷ 1.0 × 10⁻³ = 800 kg/m³.\n800 < 1000: it floats.\nFloating: F_b = mg = 8.0 N.\n8.0 ÷ (1000 × 10) = 8.0 × 10⁻⁴ m³. [8.3.B]", "tools": ["calc"]}]}, {"id": "s11", "label": "Test B", "sub": "Test B — Investigating patterns", "slides": [{"kind": "blank", "p": "A pressure sensor is lowered into an unknown liquid (absolute pressure).\ndepth h (m): 0, 0.5, 1.0, 1.5, 2.0   →   P (kPa): 100, 106, 112, 118, 124", "tag": "", "marks": "", "flat": [{"t": "Pressure increase per metre = __B1__ kPa/m", "a": {"B1": "12"}}, {"t": "Density of the liquid = __B1__ kg/m³", "a": {"B1": "1200"}}, {"t": "Predicted P at 3.0 m = __B1__ kPa", "a": {"B1": "136"}}], "sol": "(124 − 100) ÷ 2.0 = 12 kPa/m.\nρg = 12 000 Pa/m: ρ = 1200 kg/m³.\n100 + 12 × 3.0 = 136 kPa.", "tools": ["calc", "desmos"], "desmos": [{"type": "table", "columns": [{"latex": "x_1", "values": ["0", "0.5", "1", "1.5", "2"]}, {"latex": "y_1", "values": ["100", "106", "112", "118", "124"]}]}, "y_1\\sim mx_1+b"]}, {"kind": "blank", "p": "A block is lowered into water on a spring scale.\nsubmerged volume (cm³): 0, 100, 200, 300, 400   →   scale reading (N): 9.0, 8.0, 7.0, 6.0, 5.0", "tag": "", "marks": "", "flat": [{"t": "Buoyant force per 100 cm³ submerged = __B1__ N", "a": {"B1": "1"}}, {"t": "Scale reading when 250 cm³ is submerged = __B1__ N", "a": {"B1": "6.5"}}, {"t": "If the scale reads 5.0 N when fully submerged, the block's density = __B1__ kg/m³", "a": {"B1": "2250"}}], "sol": "Each 100 cm³ = 10⁻⁴ m³ displaces 1.0 N of water.\n9.0 − 2.5 = 6.5 N.\nm = 0.90 kg, V = 4.0 × 10⁻⁴ m³: 0.90 ÷ 4.0 × 10⁻⁴ = 2250 kg/m³.", "tools": ["calc"]}, {"kind": "mcq", "text": "Water speeds in a pipe of varying area: A = 8 cm² → 1.5 m/s, 4 cm² → 3.0 m/s, 2 cm² → 6.0 m/s. Which relationship fits?", "opts": ["v is proportional to A²", "v is inversely proportional to A", "v does not depend on A", "v is proportional to A"], "correct": 1, "tag": "", "sol": "A × v = 12 cm²·m/s every time."}, {"kind": "blank", "p": "Jet speeds from holes at different depths below the surface of an open tank:\nΔy (m): 0.2, 0.8, 1.8, 3.2   →   v (m/s): 2.0, 4.0, 6.0, 8.0", "tag": "", "marks": "", "flat": [{"t": "When Δy is multiplied by 4, v is multiplied by __B1__", "a": {"B1": "2"}}, {"t": "v² ÷ Δy = __B1__ m/s² for every row", "a": {"B1": "20"}}, {"t": "Predicted speed for Δy = 5.0 m = __B1__ m/s", "a": {"B1": "10"}}], "sol": "0.2 → 0.8 m: 2.0 → 4.0 m/s.\n4 ÷ 0.2 = 16 ÷ 0.8 = 20 = 2g.\nv = √(20 × 5.0) = 10 m/s.", "tools": ["calc", "desmos"], "desmos": [{"type": "table", "columns": [{"latex": "x_1", "values": ["0.2", "0.8", "1.8", "3.2"]}, {"latex": "y_1", "values": ["2", "4", "6", "8"]}]}, "y_1\\sim a\\sqrt{x_1}"]}, {"kind": "mcq", "text": "Blocks of different woods float in water. ρ = 400 → 40% submerged; 600 → 60%; 800 → 80%. The fraction submerged is", "opts": ["ρ_water ÷ ρ_block", "1 − ρ_block ÷ ρ_water", "ρ_block ÷ ρ_water", "always ½"], "correct": 2, "tag": "", "sol": "F_b = mg gives V_sub/V = ρ_block/ρ_water."}, {"kind": "mcq", "text": "Gauge pressure at 1 m depth: water 10 kPa, sea water 10.3 kPa, glycerine 12.6 kPa, mercury 136 kPa. The gauge pressure at a fixed depth is proportional to", "opts": ["the liquid's density", "the container's width", "the liquid's volume", "the liquid's viscosity"], "correct": 0, "tag": "", "sol": "ρgh with h fixed."}, {"kind": "mcq", "text": "A hydraulic press is tested with a 100 N push on the small piston. Area ratio A₂/A₁ = 5 → output 500 N; 10 → 1000 N; 20 → 2000 N. Predict the output for A₂/A₁ = 35.", "opts": ["35 N", "3500 N", "2100 N", "350 N"], "correct": 1, "tag": "", "sol": "F₂ = 100 N × (A₂/A₁): 100 × 35 = 3500 N."}, {"kind": "blank", "p": "A Venturi meter's pressure drop is measured at different entry speeds (area ratio 4 : 1).\nv₁ (m/s): 1.0, 2.0, 3.0   →   ΔP (kPa): 7.5, 30, 67.5", "tag": "", "marks": "", "flat": [{"t": "When v₁ doubles, ΔP is multiplied by __B1__", "a": {"B1": "4"}}, {"t": "ΔP ÷ v₁² = __B1__ kPa·s²/m²", "a": {"B1": "7.5"}}, {"t": "Predicted ΔP for v₁ = 4.0 m/s = __B1__ kPa", "a": {"B1": "120"}}], "sol": "7.5 → 30: ×4.\n7.5 ÷ 1 = 30 ÷ 4 = 7.5.\n7.5 × 16 = 120 kPa (½ρ(16 − 1)v₁² check: 500 × 15 × 16 = 120 kPa).", "tools": ["calc"]}]}, {"id": "s12", "label": "Test C", "sub": "Test C — Communicating", "slides": [{"kind": "mcq", "text": "Convert a density of 2.7 g/cm³ to kg/m³.", "opts": ["0.0027 kg/m³", "2700 kg/m³", "2.7 kg/m³", "27 kg/m³"], "correct": 1, "tag": "", "sol": "1 g/cm³ = 1000 kg/m³."}, {"kind": "mcq", "text": "A tyre gauge reads 2.0 × 10⁵ Pa. The absolute pressure of the air in the tyre is", "opts": ["3.0 × 10⁵ Pa", "1.0 × 10⁵ Pa", "2.0 × 10⁵ Pa", "2.0 × 10⁵ Pa minus 1 atm"], "correct": 0, "tag": "", "sol": "Gauges read pressure above atmospheric: P = P₀ + P_gauge."}, {"kind": "mcq", "text": "A student writes: \"In a horizontal pipe, the water is fastest where the pressure is highest.\" The correct statement is", "opts": ["Speed does not depend on pressure", "The water is fastest where the pipe is widest", "The statement is correct", "The water is fastest where the pressure is lowest"], "correct": 3, "tag": "", "sol": "Bernoulli: P + ½ρv² constant at one height."}, {"kind": "mcq", "text": "Which free-body diagram is correct for a block floating at rest?", "opts": ["mg down only", "F_b down, mg up", "F_b up, longer than mg", "F_b up and mg down, equal lengths"], "correct": 3, "tag": "", "sol": "Equilibrium: equal and opposite forces."}, {"kind": "mcq", "text": "A student says: \"The pipe diameter halves, so the speed doubles.\" What is the error?", "opts": ["No error", "Area depends on diameter squared: the speed becomes 4 times as large", "The speed halves", "Speed does not depend on area"], "correct": 1, "tag": "", "sol": "A = πd²/4."}, {"kind": "mcq", "text": "A student draws the force of the water on the vertical side wall of a tank as an arrow pointing straight down. The correct direction is", "opts": ["perpendicular to the wall, pointing outward", "straight up", "straight down, as drawn", "along the wall"], "correct": 0, "tag": "", "sol": "The force from fluid pressure on a surface is always perpendicular to that surface."}, {"kind": "mcq", "text": "ρ = 0.630 kg ÷ 2.50 × 10⁻⁴ m³. To three significant figures, ρ =", "opts": ["2.52 × 10³ kg/m³", "25.2 kg/m³", "2.5 × 10³ kg/m³", "2520.0 kg/m³"], "correct": 0, "tag": "", "sol": "0.630 ÷ 2.50 × 10⁻⁴ = 2520; three sig figs: 2.52 × 10³."}, {"kind": "blank", "p": "A student's work: \"Buoyant force on a 0.0030 m³ iron block (ρ = 7900 kg/m³) under water = ρVg = 7900 × 0.0030 × 10 = 237 N.\"", "tag": "", "marks": "", "flat": [{"t": "Correct buoyant force = __B1__ N", "a": {"B1": "30"}}, {"t": "The student used the density of the __B1__ (object / fluid) instead of the fluid.", "a": {"B1": "object"}, "expr": "words", "accept": ["iron", "block", "the object"]}], "sol": "1000 × 0.0030 × 10 = 30 N.\nF_b uses the fluid's density; 237 N is the block's weight.", "tools": ["calc"]}, {"kind": "blank", "p": "Give each quantity in SI units.", "tag": "", "marks": "", "flat": [{"t": "5.0 L = __B1__ m³", "a": {"B1": "0.005"}}, {"t": "20 cm² = __B1__ m²", "a": {"B1": "0.002"}}, {"t": "3.5 kPa = __B1__ Pa", "a": {"B1": "3500"}}, {"t": "250 cm³ of water has mass __B1__ kg", "a": {"B1": "0.25"}}], "sol": "1 L = 10⁻³ m³.\n1 cm² = 10⁻⁴ m².\n× 1000.\n1 cm³ of water = 1 g."}]}, {"id": "s13", "label": "Test D", "sub": "Test D — Applying physics in real-life contexts", "slides": [{"kind": "mcq", "text": "A student calculates the absolute pressure 10 m below the surface of a lake as 1.0 × 10⁷ Pa. Is this reasonable?", "opts": ["Yes: ρgh = 10⁷", "No: it should be 1.0 × 10⁴ Pa", "Yes: deep water is very high pressure", "No: P = 1.0 × 10⁵ + 1000 × 10 × 10 = 2.0 × 10⁵ Pa"], "correct": 3, "tag": "", "sol": "10⁷ Pa is 100 atmospheres, the pressure about 1 km down.", "tools": ["calc"]}, {"kind": "mcq", "text": "A car's hydraulic brake has a master piston of area 1.0 cm² and wheel pistons of area 10 cm². A 150 N push on the master piston gives each wheel piston a force of", "opts": ["150 N", "15 N", "15 000 N", "1500 N"], "correct": 3, "tag": "", "sol": "Same pressure: 150 × 10.", "tools": ["calc"]}, {"kind": "mcq", "text": "A hospital drip bag must give a gauge pressure of 1.3 × 10⁴ Pa at the needle. The fluid's density is 1000 kg/m³. The bag should hang about", "opts": ["0.13 m above", "13 m above", "1.3 m above the needle", "1.3 m below"], "correct": 2, "tag": "", "sol": "h = P ÷ ρg = 13 000 ÷ 10 000.", "tools": ["calc"]}, {"kind": "mcq", "text": "A submarine cruising fully under water pumps sea water into its ballast tanks. What happens?", "opts": ["Nothing changes, because the water stays inside the submarine", "Its weight increases while the buoyant force stays the same, so it sinks", "The buoyant force increases, so it rises", "The buoyant force decreases, so it sinks"], "correct": 1, "tag": "", "sol": "Its outside volume, and so F_b = ρVg, is unchanged; the extra water adds to its weight. [8.3.B]"}, {"kind": "blank", "p": "An iceberg (ρ = 900 kg/m³) floats in sea water (ρ = 1030 kg/m³). Its visible part has volume 2600 m³.", "tag": "", "marks": "", "flat": [{"t": "Fraction under water = __B1__", "a": {"B1": "0.874"}, "expr": "approx"}, {"t": "Total volume of the iceberg = __B1__ m³", "a": {"B1": "20600"}, "expr": "approx"}, {"t": "Mass of the iceberg = __B1__ kg", "a": {"B1": "18540000"}, "expr": "approx"}], "sol": "900 ÷ 1030 ≈ 0.874.\nVisible fraction 0.126: 2600 ÷ 0.126 ≈ 20 600 m³.\n900 × 20 600 ≈ 1.85 × 10⁷ kg.", "tools": ["calc"]}, {"kind": "blank", "p": "A fire hose of area 30 cm² carries water at 5.0 m/s to a nozzle of area 6.0 cm².", "tag": "", "marks": "", "flat": [{"t": "Speed at the nozzle = __B1__ m/s", "a": {"B1": "25"}}, {"t": "Flow rate = __B1__ L/s", "a": {"B1": "15"}}, {"t": "Gauge pressure in the hose (horizontal, nozzle at atmospheric pressure) = __B1__ Pa", "a": {"B1": "300000"}}], "sol": "30 × 5.0 ÷ 6.0 = 25 m/s.\n0.0030 × 5.0 = 0.015 m³/s = 15 L/s.\n½ × 1000 × (625 − 25) = 300 000 Pa.", "tools": ["calc"]}, {"kind": "blank", "p": "A dam holds back a reservoir 40 m deep.", "tag": "", "marks": "", "flat": [{"t": "Gauge pressure at the base of the dam = __B1__ Pa", "a": {"B1": "400000"}}, {"t": "Gauge pressure halfway down = __B1__ Pa", "a": {"B1": "200000"}}, {"t": "Speed of water from an opening at the base = __B1__ m/s", "a": {"B1": "28.3"}, "expr": "approx"}], "sol": "1000 × 10 × 40 = 4.0 × 10⁵ Pa.\nAt 20 m: 2.0 × 10⁵ Pa.\n√(2 × 10 × 40) ≈ 28.3 m/s.", "tools": ["calc"]}, {"kind": "blank", "p": "An aircraft wing of area 30 m² has air (ρ = 1.2 kg/m³) moving at 70 m/s under it and 80 m/s over it.", "tag": "", "marks": "", "flat": [{"t": "Pressure difference = __B1__ Pa", "a": {"B1": "900"}}, {"t": "Lift force = __B1__ N", "a": {"B1": "27000"}}, {"t": "Largest mass it could support = __B1__ kg", "a": {"B1": "2700"}}], "sol": "½ × 1.2 × (6400 − 4900) = 900 Pa.\n900 × 30 = 27 000 N.\n27 000 ÷ 10 = 2700 kg.", "tools": ["calc"]}]}];
/* ================= build slide lists ================= */
var SLIDES = {}; SECTIONS.forEach(function(sec){ SLIDES[sec.id]=sec.slides; });
var TAB_DEFS = SECTIONS.map(function(sec){ return {id:sec.id, label:sec.label, sub:sec.sub}; });

/* ================= state ================= */
function blankItem(slide){
  if(slide.kind==='mcq'||slide.kind==='ar'){
    return {status:'unanswered', attempts:0, choice:undefined};
  }
  return {status:'unanswered', curStep:0, stepStates: slide.flat.map(function(){ return {status:'unanswered', attempts:0, inputs:{}}; })};
}
function defaultState(){
  var s={tabs:{}};
  TAB_DEFS.forEach(function(td){
    s.tabs[td.id] = { idx:0, maxReached:0, items: SLIDES[td.id].map(function(sl){ return blankItem(sl); }) };
  });
  return s;
}
var appState = {mode:null, learning:null, quiz:null};
var state = null;      // alias for appState[appState.mode]
var MODE = null;
var activeTab=TAB_DEFS[0].id;

function setMode(m){
  appState.mode = m;
  if(!appState[m]) appState[m] = defaultState();
  state = appState[m];
  MODE = m;
}
/* ================= student accounts (saved on this device) ================= */
var SHEET_KEY='sopaan-ap1-ch8';
var ACC_KEY='sopaan-students-v1';
var storageOK=true;
var MEM={};
function lsGet(k){ var r=null; try{ r=localStorage.getItem(k); }catch(e){ storageOK=false; }
  if(r===null||r===undefined) r=MEM[k]||null; try{ return r?JSON.parse(r):null; }catch(e){ return null; } }
function lsSet(k,v){ var j=JSON.stringify(v); MEM[k]=j; try{ localStorage.setItem(k,j); return true; }catch(e){ storageOK=false; return false; } }
try{ localStorage.setItem('sopaan-probe','1'); localStorage.removeItem('sopaan-probe'); }catch(e){ storageOK=false; }
function hashPin(pin,salt){ var h=2166136261, str=salt+'|'+pin; for(var i=0;i<str.length;i++){ h^=str.charCodeAt(i); h=Math.imul(h,16777619)>>>0; } return h.toString(36); }
function accKey(name,roll){ return (name.trim().toLowerCase().replace(/\s+/g,' ')+'#'+roll.trim().toLowerCase()); }
function accounts(){ return lsGet(ACC_KEY)||{students:{}}; }
var student=null; // {key,name,roll}
var records=[];   // finished-tab history for this student on this sheet
function progKey(){ return SHEET_KEY+'::'+student.key; }

function loadState(){
  appState = {mode:null, learning:null, quiz:null}; records=[]; activeTab=TAB_DEFS[0].id;
  var saved=lsGet(progKey());
  if(!saved) return;
  try{
    ['learning','quiz'].forEach(function(m){
      if(saved[m] && saved[m].tabs){
        var fresh = defaultState();
        TAB_DEFS.forEach(function(td){
          if(saved[m].tabs[td.id] && saved[m].tabs[td.id].items && saved[m].tabs[td.id].items.length===SLIDES[td.id].length){
            fresh.tabs[td.id] = saved[m].tabs[td.id];
          }
        });
        appState[m] = fresh;
      }
    });
    if(saved.mode==='learning' || saved.mode==='quiz') appState.mode = saved.mode;
    if(saved.activeTab && TAB_DEFS.some(function(t){ return t.id===saved.activeTab; })) activeTab = saved.activeTab;
    if(Array.isArray(saved.records)) records = saved.records;
  }catch(e){}
}
function saveState(){
  if(!student) return;
  lsSet(progKey(), {mode:appState.mode, learning:appState.learning, quiz:appState.quiz, activeTab:activeTab, records:records, updated:Date.now()});
  var acc=accounts(); if(acc.students[student.key]){ acc.students[student.key].last=Date.now(); lsSet(ACC_KEY,acc); }
}
function addRecord(mode, tabId, correct, revealed, skipped, total){
  records.unshift({at:Date.now(), mode:mode, tab:tabId, correct:correct, revealed:revealed, skipped:skipped, total:total});
  if(records.length>60) records.length=60;
  saveState();
}
function fmtDate(ms){ try{ return new Date(ms).toLocaleString(undefined,{day:'numeric',month:'short',hour:'2-digit',minute:'2-digit'}); }catch(e){ return ''; } }

function renderWho(){
  var el=document.getElementById('whoBar');
  if(!student){ el.hidden=true; el.innerHTML=''; return; }
  el.hidden=false;
  el.innerHTML='Signed in as <b>'+esc(student.name)+'</b> · Roll '+esc(student.roll)+
    ' <button id="btnRecord">My record</button> <button id="btnSignOut">Sign out</button>';
  document.getElementById('btnRecord').addEventListener('click', renderRecord);
  document.getElementById('btnSignOut').addEventListener('click', signOut);
}
function signOut(){
  saveState(); student=null; state=null; MODE=null;
  var acc=accounts(); delete acc.current; lsSet(ACC_KEY,acc);
  document.getElementById('modePill').hidden=true;
  renderWho(); renderLogin();
}
function signIn(key){
  var acc=accounts(); var st=acc.students[key]; if(!st) return;
  student={key:key, name:st.name, roll:st.roll};
  acc.current=key; st.last=Date.now(); lsSet(ACC_KEY,acc);
  loadState(); renderWho();
  if(appState.mode==='learning' || appState.mode==='quiz'){
    setMode(appState.mode); document.getElementById('modePill').hidden=false; updateModePill();
    showChrome(true); buildTabbar(); renderSlide();
    showToast('Welcome back, '+st.name.split(' ')[0]+'. Picking up where you left off.');
  } else {
    renderModePicker();
  }
}
function renderLogin(msg){
  showChrome(false);
  var acc=accounts(); var keys=Object.keys(acc.students).sort(function(a,b){ return (acc.students[b].last||0)-(acc.students[a].last||0); });
  var h='<div class="login-card"><h2>Student sign-in</h2>'+
    '<p class="lead">Sign in to save your answers, see your record and continue where you left off next time.</p>';
  if(!storageOK) h+='<div class="login-err">This browser is blocking saved data (for example, a private window). You can still practise, but progress will not be kept after you close the page.</div>';
  if(msg) h+='<div class="login-err">'+esc(msg)+'</div>';
  if(keys.length){
    h+='<div class="known"><span class="known-label">Continue as</span>';
    keys.slice(0,6).forEach(function(k){ var st=acc.students[k];
      h+='<button class="known-btn" data-k="'+esc(k)+'"><span>'+esc(st.name)+' <small>· Roll '+esc(st.roll)+'</small></span><small>'+(st.last?'Last active '+fmtDate(st.last):'')+'</small></button>'; });
    h+='</div>';
  }
  h+='<form id="loginForm" novalidate>'+
    '<div class="fld"><label for="lgName">Full name</label><input id="lgName" autocomplete="name" required></div>'+
    '<div class="fld-row"><div class="fld"><label for="lgRoll">Roll no.</label><input id="lgRoll" required></div>'+
    '<div class="fld"><label for="lgPin">4-digit PIN</label><input id="lgPin" type="password" inputmode="numeric" maxlength="4" autocomplete="off" required></div></div>'+
    '<button class="btn btn-primary" type="submit" style="width:100%;">Sign in</button>'+
    '<p class="login-note">New here? Enter your name, roll no. and a PIN you will remember, and your profile is created. Progress is saved on this device, so use the same device and browser to continue.</p>'+
    '</form></div>';
  var wrap=document.getElementById('wrap'); wrap.innerHTML=h;
  wrap.querySelectorAll('.known-btn').forEach(function(b){
    b.addEventListener('click', function(){
      var st=accounts().students[b.dataset.k];
      document.getElementById('lgName').value=st.name; document.getElementById('lgRoll').value=st.roll;
      document.getElementById('lgPin').focus();
    });
  });
  document.getElementById('loginForm').addEventListener('submit', function(e){
    e.preventDefault();
    var name=document.getElementById('lgName').value.trim(), roll=document.getElementById('lgRoll').value.trim(), pin=document.getElementById('lgPin').value.trim();
    if(!name||!roll){ renderLoginErr('Enter your name and roll no.'); return; }
    if(!/^\d{4}$/.test(pin)){ renderLoginErr('Your PIN must be exactly 4 digits.'); return; }
    var k=accKey(name,roll); var acc=accounts();
    if(acc.students[k]){
      if(acc.students[k].pin!==hashPin(pin,k)){ renderLoginErr('That PIN does not match this name and roll no. Try again.'); return; }
    } else {
      acc.students[k]={name:name.replace(/\s+/g,' '), roll:roll, pin:hashPin(pin,k), created:Date.now()};
      lsSet(ACC_KEY,acc);
    }
    signIn(k);
  });
}
function renderLoginErr(m){
  var n=document.getElementById('lgName').value, r=document.getElementById('lgRoll').value;
  renderLogin(m); document.getElementById('lgName').value=n; document.getElementById('lgRoll').value=r; document.getElementById('lgPin').focus();
}
function tabSummary(m){
  var st=appState[m]; if(!st) return null;
  return TAB_DEFS.map(function(td){
    var items=st.tabs[td.id].items, n=items.length;
    var c=items.filter(function(i){return i.status==='correct';}).length;
    var done=items.filter(function(i){return i.status!=='unanswered';}).length;
    return {label:td.label, n:n, done:done, correct:c};
  });
}
function renderRecord(){
  showChrome(false);
  var tabLabel=function(id){ var t=TAB_DEFS.find(function(x){return x.id===id;}); return t?t.label:id; };
  var h='<div class="rec-card"><h2>'+esc(student.name)+'’s record</h2><p class="rec-empty" style="margin:0 0 12px;">Roll '+esc(student.roll)+' · Fluids</p>';
  ['learning','quiz'].forEach(function(m){
    var sum=tabSummary(m);
    h+='<h3>'+(m==='learning'?'📘 Learning Sheet':'📝 Quiz Mode')+'</h3>';
    if(!sum){ h+='<p class="rec-empty">Not started yet.</p>'; return; }
    h+='<div class="rec-table-wrap"><table class="rec-table"><thead><tr><th>Section</th><th>Progress</th><th>Correct first time</th></tr></thead><tbody>';
    sum.forEach(function(r){ var pct=Math.round(r.done/r.n*100);
      h+='<tr><td>'+r.label+'</td><td><span class="rec-bar"><i style="width:'+pct+'%"></i></span>'+r.done+' / '+r.n+'</td><td>'+(m==='quiz'?'—':r.correct+' / '+r.n)+'</td></tr>'; });
    h+='</tbody></table></div>';
  });
  h+='</div><div class="rec-card"><h3>Finished sections</h3>';
  if(!records.length){ h+='<p class="rec-empty">No sections finished yet. Each time you finish a tab, your score is recorded here.</p>'; }
  else {
    h+='<div class="rec-table-wrap"><table class="rec-table"><thead><tr><th>When</th><th>Mode</th><th>Section</th><th>Score</th></tr></thead><tbody>';
    records.forEach(function(r){ h+='<tr><td>'+fmtDate(r.at)+'</td><td>'+(r.mode==='quiz'?'Quiz':'Learning')+'</td><td>'+tabLabel(r.tab)+'</td><td>'+r.correct+' / '+r.total+(r.mode==='learning'?' <span class="rec-empty">('+r.revealed+' revealed, '+r.skipped+' skipped)</span>':'')+'</td></tr>'; });
    h+='</tbody></table></div>';
  }
  h+='</div><button class="btn btn-primary" id="btnBack">'+(MODE?'Back to practice':'Choose a mode')+'</button>';
  document.getElementById('wrap').innerHTML=h;
  document.getElementById('btnBack').addEventListener('click', function(){
    if(MODE){ showChrome(true); buildTabbar(); renderSlide(); } else renderModePicker();
  });
  window.scrollTo({top:0});
}

/* ================= tab bar ================= */
function buildTabbar(){
  var el=document.getElementById('tabbar');
  el.innerHTML = '<button class="tab-btn'+(activeTab==='theory'?' active':'')+'" data-tab="theory">Theory<span class="tab-count">notes</span></button>' + TAB_DEFS.map(function(t){
    return '<button class="tab-btn'+(t.id===activeTab?' active':'')+'" data-tab="'+t.id+'">'+t.label+'<span class="tab-count">'+SLIDES[t.id].length+'</span></button>';
  }).join('') + '<button class="tab-btn'+(activeTab==='report'?' active':'')+'" data-tab="report">📊 Report<span class="tab-count">pie</span></button>';
  el.querySelectorAll('.tab-btn').forEach(function(btn){
    btn.addEventListener('click', function(){ activeTab=btn.dataset.tab; buildTabbar(); renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); });
  });
}

/* ================= rendering ================= */
function canProceed(item){ return item.status==='correct'||item.status==='revealed'||item.status==='skipped'; }

function renderSlide(){
  if(!state.tabs[activeTab]){ activeTab=TAB_DEFS[0].id; }
  var ts = state.tabs[activeTab];
  var slides = SLIDES[activeTab];
  if(ts.idx>=slides.length||ts.idx<0) ts.idx=0;
  var idx = ts.idx;
  var slide = slides[idx];
  var item = ts.items[idx];

  var tdef=TAB_DEFS.find(function(t){return t.id===activeTab;});
  document.getElementById('spLabel').textContent = tdef.label+' · Question '+(idx+1)+' of '+slides.length;
  document.getElementById('secSub').textContent = tdef.label+' — '+tdef.sub;
  document.getElementById('spFill').style.width = Math.round(((idx)/(Math.max(slides.length-1,1)))*100)+'%';

  var h='<div class="qcard">';
  if(slide.kind==='mcq' || slide.kind==='ar'){
    h += renderChoiceBody(slide, item, idx);
  } else {
    h += renderBlankBody(slide, item, idx);
  }
  h += '<div class="feedback" id="feedbackBox"></div>';
  if(MODE==='learning' && (item.status==='correct'||item.status==='revealed')) h += solutionHTML(slide);
  h += '</div>';

  document.getElementById('wrap').innerHTML = h;
  wireSlideEvents(slide, item, idx);
  restoreFeedback(item);
  renderNavbar(item);
  updateFab();
  saveState();
}

function solutionHTML(slide){
  if(!slide.sol) return '';
  return '<div class="solution"><div class="sol-h">Solution</div>'+slide.sol.split('\n').map(function(l){ return '<div class="sol-line">'+fr(esc(l))+'</div>'; }).join('')+'</div>';
}
var LETTERS=['a','b','c','d','e','f'];
function chosenHTML(slide,item){
  var opts = slide.kind==='mcq' ? slide.opts : AR_OPTIONS;
  if(item.choice===undefined) return '';
  var ok=item.choice===slide.correct;
  var h='<div class="chosen '+(ok?'ok':'bad')+'"><b>Your answer:</b> ('+LETTERS[item.choice]+') '+fr(esc(opts[item.choice]))+(ok?' ✓':' ✗')+'</div>';
  if(!ok) h+='<div class="chosen ok"><b>Correct answer:</b> ('+LETTERS[slide.correct]+') '+fr(esc(opts[slide.correct]))+'</div>';
  return h;
}
function renderChoiceBody(slide, item, idx){
  var h='<div class="qhead"><div class="qnum">'+(idx+1)+'</div>';
  if(slide.kind==='mcq'){
    h += '<div class="qtext">'+fr(esc(slide.text))+(slide.tag?'<span class="qtag">'+esc(slide.tag)+'</span>':'')+'</div>';
  } else {
    h += '<div class="qtext"><span class="qtag" style="margin-left:0;margin-right:6px;">A / R</span>Assertion (A): '+fr(esc(slide.a))+'<br>Reason (R): '+fr(esc(slide.r))+(slide.tag?'<span class="qtag">'+esc(slide.tag)+'</span>':'')+'</div>';
  }
  h += '</div>';
  if(slide.fig) h += '<div class="fig">'+slide.fig+'</div>';
  var opts = slide.kind==='mcq' ? slide.opts : AR_OPTIONS;
  if(MODE==='quiz') h += '<div class="quiz-hint">Quiz mode — pick an option. The correct answer is revealed once you finish this tab.</div>';
  var locked = MODE==='learning' && (item.status==='correct' || item.status==='revealed');
  h += '<div class="options">';
  opts.forEach(function(opt,i){
    var cls='opt';
    if(locked){
      if(i===slide.correct) cls+=' is-correct';
      else if(item.choice===i) cls+=' is-wrong';
      cls+=' locked';
    }
    if(item.choice===i) cls+=' is-chosen';
    h += '<label class="'+cls+'"><input type="radio" name="choice" value="'+i+'" '+(item.choice===i?'checked':'')+' '+(locked?'disabled':'')+'> <span class="opt-l">('+LETTERS[i]+')</span> <span class="opt-t">'+fr(esc(opt))+'</span>'+(item.choice===i?'<span class="opt-tag">'+(locked?(i===slide.correct?'Your answer ✓':'Your answer ✗'):'Selected')+'</span>':'')+'</label>';
  });
  h += '</div>';
  if(locked) h += chosenHTML(slide,item);
  return h;
}

function renderBlankBody(slide, item, idx){
  var h='<div class="qhead"><div class="qnum">'+(idx+1)+'</div><div class="qtext">';
  if(slide.kind==='case'){ h += '<b>'+esc(slide.title)+'.</b> '+esc(slide.body); }
  else { var pp=fr(esc(slide.p)).split('\n'); h += pp[0]+pp.slice(1).map(function(x){return '<span class="datline">'+x+'</span>';}).join(''); }
  h += (slide.tag?'<span class="qtag">'+esc(slide.tag)+'</span>':'')+'</div>';
  if(slide.marks) h += '<div class="marks-pill">'+slide.marks+'</div>';
  h += '</div>';
  if(slide.fig) h += '<div class="fig">'+slide.fig+'</div>';

  var total = slide.flat.length;
  var hasExpr = slide.flat.some(function(s){ return s.expr===true; });
  var hasFrac = slide.flat.some(function(s){ return ['fv','fe','fl','fm','fi','flist'].indexOf(s.expr)>=0; });
  var blankCount=0; slide.flat.forEach(function(s){ blankCount+=Object.keys(s.a).length; });

  if(MODE==='quiz'){
    h += '<div class="step-badge">'+blankCount+' blank'+(blankCount===1?'':'s')+' in this question</div>';
    h += '<div class="quiz-hint">Quiz mode — fill in what you can. Correct answers are revealed once you finish this tab.</div>';
    if(hasFrac) h += '<div class="quiz-hint">Type fractions like <b>3/4</b> and mixed numbers like <b>2 3/4</b> (whole number, space, fraction).</div>';
    if(hasExpr) h += '<div class="quiz-hint">Type answers like <b>2x-5</b>, <b>x^2-4</b> or <b>3+2i</b>. Use ^ for powers, | | for absolute value and pi for π. Any equivalent form is accepted.</div>';
    h += '<div class="steps">';
    for(var qi=0; qi<total; qi++){
      var qstep = slide.flat[qi];
      var qss = item.stepStates[qi];
      if(qstep.partLabel) h += '<div class="subpart-label">'+esc(qstep.partLabel)+'</div>';
      if(qstep.orDivider) h += '<div class="or-divider">OR</div>';
      var qline = fr(qstep.t);
      Object.keys(qstep.a).forEach(function(bkey){
        var val = qss.inputs[bkey]||'';
        var inp='<input class="blank-input'+(['fv','fe','fl','fm','fi','dec'].indexOf(qstep.expr)>=0?' fr':(qstep.expr==='flist'||qstep.expr==='dlist'||qstep.expr==='glist')?' wide':qstep.expr===true?' expr':(qstep.expr==='words'||qstep.expr==='list'||qstep.expr==='expanded'||qstep.expr==='set'||qstep.expr==='primes'||qstep.expr==='trans'||qstep.expr==='rot'?' wide':''))+'" data-step="'+qi+'" data-bkey="'+bkey+'" value="'+esc(val)+'">';
        qline = qline.replace('__'+bkey+'__', inp);
      });
      if(qstep.fig) h += '<div class="fig">'+qstep.fig+'</div>';
      h += '<div class="step-line">'+qline+'</div>';
    }
    h += '</div>';
    return h;
  }

  if(hasFrac) h += '<div class="quiz-hint">Type fractions like <b>3/4</b> and mixed numbers like <b>2 3/4</b> (whole number, space, fraction).</div>';
  if(hasExpr) h += '<div class="quiz-hint">Type answers like <b>2x-5</b>, <b>x^2-4</b> or <b>3+2i</b>. Use ^ for powers, | | for absolute value and pi for π. Any equivalent form is accepted.</div>';
  var locked = item.status==='correct' || item.status==='revealed';
  var upto = locked ? total-1 : item.curStep;
  h += '<div class="step-badge">Step '+(Math.min(item.curStep,total-1)+1)+' of '+total+'</div>';
  h += '<div class="steps">';
  for(var i=0;i<=upto;i++){
    var step = slide.flat[i];
    var ss = item.stepStates[i];
    if(step.partLabel) h += '<div class="subpart-label">'+esc(step.partLabel)+'</div>';
    if(step.orDivider) h += '<div class="or-divider">OR</div>';
    var resolved = ss.status==='correct' || ss.status==='revealed';
    var line = fr(step.t);
    Object.keys(step.a).forEach(function(bkey){
      var fs = ss.inputs['fs_'+bkey];
      var cls = fs==='correct'?'is-correct':(fs==='wrong'?'is-wrong':'');
      var val = ss.inputs[bkey]||'';
      var dis = resolved ? 'disabled':'';
      var inp='<input class="blank-input '+cls+(['fv','fe','fl','fm','fi','dec'].indexOf(step.expr)>=0?' fr':(step.expr==='flist'||step.expr==='dlist'||step.expr==='glist')?' wide':step.expr===true?' expr':(step.expr==='words'||step.expr==='list'||step.expr==='expanded'||step.expr==='set'||step.expr==='primes'||step.expr==='trans'||step.expr==='rot'?' wide':''))+'" data-step="'+i+'" data-bkey="'+bkey+'" value="'+esc(val)+'" '+dis+'>';
      line = line.replace('__'+bkey+'__', inp);
    });
    if(step.fig) h += '<div class="fig">'+step.fig+'</div>';
    h += '<div class="step-line'+(resolved?' resolved':'')+'">'+line+'</div>';
    if(ss.status==='revealed'){
      var reveals=[];
      Object.keys(step.a).forEach(function(bkey){ reveals.push(bkey+' = '+esc(step.a[bkey])); });
      h += '<div class="reveal-note">correct: '+reveals.join(', ')+'</div>';
    }
  }
  h += '</div>';
  return h;
}

var __flash=null;
function restoreFeedback(item){
  var fb=document.getElementById('feedbackBox'); if(!fb) return;
  if(__flash){ fb.className='feedback show '+__flash.c; fb.innerHTML=__flash.h; __flash=null; return; }
  if(MODE==='quiz'){ fb.className='feedback'; fb.innerHTML=''; return; }
  if(item.status==='correct'){ fb.className='feedback show ok'; fb.innerHTML='<b>All done — correct!</b>'; }
  else if(item.status==='revealed'){ fb.className='feedback show reveal'; fb.innerHTML='<b>Answer revealed above.</b> Move on whenever you’re ready.'; }
  else if(item.status==='skipped'){ fb.className='feedback show retry'; fb.innerHTML='Skipped — you can answer it now and press <b>Check</b>, or come back later from the Question Palette.'; }
  else { fb.className='feedback'; fb.innerHTML=''; }
}

function slideIsAnswered(slide,item){
  if(slide.kind==='mcq'||slide.kind==='ar') return item.choice!==undefined;
  return item.stepStates.some(function(ss){ return Object.keys(ss.inputs).some(function(k){ return k.indexOf('fs_')!==0 && ss.inputs[k] && String(ss.inputs[k]).trim()!==''; }); });
}
function renderNavbar(item){
  var ts = state.tabs[activeTab];
  var slides = SLIDES[activeTab];
  var slide = slides[ts.idx];
  var isLast = ts.idx === slides.length-1;
  var h='';
  h += '<button class="btn" id="btnPrev" '+(ts.idx===0?'disabled':'')+'>&larr; Previous</button>';

  if(MODE==='quiz'){
    h += '<button class="btn" id="btnSkip">Skip</button>';
    h += '<span class="spacer"></span>';
    h += '<button class="btn btn-primary" id="btnNext">'+(isLast?'Finish':'Next →')+'</button>';
  } else {
    h += '<button class="btn" id="btnSkip" '+(item.status!=='unanswered'?'disabled':'')+'>Skip</button>';
    h += '<span class="spacer"></span>';
    h += '<button class="btn btn-primary" id="btnCheck" '+((item.status!=='unanswered'&&item.status!=='skipped')?'disabled':'')+'>Check</button>';
    h += '<button class="btn btn-primary" id="btnNext" '+(canProceed(item)?'':'disabled')+'>'+(isLast?'Finish':'Next →')+'</button>';
  }
  document.getElementById('navbarInner').innerHTML = h;

  document.getElementById('btnPrev').addEventListener('click', function(){ if(ts.idx>0){ ts.idx--; renderSlide(); } });

  if(MODE==='quiz'){
    document.getElementById('btnSkip').addEventListener('click', function(){
      item.status='skipped';
      advanceQuiz(ts, slides);
    });
    document.getElementById('btnNext').addEventListener('click', function(){
      item.status = slideIsAnswered(slide,item) ? 'answered' : 'unanswered';
      advanceQuiz(ts, slides);
    });
  } else {
    document.getElementById('btnSkip').addEventListener('click', function(){
      if(item.status==='unanswered'){ item.status='skipped'; renderSlide(); }
    });
    document.getElementById('btnNext').addEventListener('click', function(){
      if(!canProceed(item)) return;
      if(ts.idx < slides.length-1){ ts.idx++; ts.maxReached=Math.max(ts.maxReached, ts.idx); renderSlide(); }
      else { renderFinished(); }
    });
    document.getElementById('btnCheck').addEventListener('click', function(){ handleCheck(); });
  }
}
function advanceQuiz(ts, slides){
  if(ts.idx < slides.length-1){ ts.idx++; ts.maxReached=Math.max(ts.maxReached, ts.idx); renderSlide(); }
  else { renderFinished(); }
}

function wireSlideEvents(slide, item, idx){
  document.querySelectorAll('input[type="radio"][name="choice"]').forEach(function(r){
    r.addEventListener('change', function(){ item.choice=parseInt(r.value,10); saveState();
      document.querySelectorAll('.opt').forEach(function(l){ l.classList.remove('is-chosen'); var t=l.querySelector('.opt-tag'); if(t) t.remove(); });
      var lab=r.closest('.opt'); lab.classList.add('is-chosen'); var tg=document.createElement('span'); tg.className='opt-tag'; tg.textContent='Selected'; lab.appendChild(tg); });
  });
  document.querySelectorAll('.blank-input').forEach(function(inp){
    inp.addEventListener('input', function(){
      var si=parseInt(inp.dataset.step,10), bk=inp.dataset.bkey;
      item.stepStates[si].inputs[bk]=inp.value;
      saveState();
    });
  });
}

function handleCheck(){
  var ts = state.tabs[activeTab];
  var slide = SLIDES[activeTab][ts.idx];
  var item = ts.items[ts.idx];
  if(item.status==='skipped') item.status='unanswered';
  var fb = document.getElementById('feedbackBox');

  if(slide.kind==='mcq' || slide.kind==='ar'){
    if(item.choice===undefined){ fb.className='feedback show err'; fb.innerHTML='Please choose an option first.'; return; }
    var ok = item.choice===slide.correct;
    if(ok){
      item.status='correct'; playSuccess();
      fb.className='feedback show ok'; fb.innerHTML='<b>Correct!</b>';
    } else {
      item.attempts=(item.attempts||0)+1;
      if(item.attempts>=2){ item.status='revealed'; playReveal(); }
      else { playWrong(); fb.className='feedback show retry'; fb.innerHTML='<b>Not quite — try again</b> (attempt 1 of 2) <span class="attempts-dots"><span class="used"></span><span></span></span>'; __flash={c:'retry',h:'<b>Not quite — try again</b> (attempt 1 of 2) <span class="attempts-dots"><span class="used"></span><span></span></span>'}; }
    }
    renderSlide();
    return;
  }

  // blank / case
  var step = slide.flat[item.curStep];
  var ss = item.stepStates[item.curStep];
  var blanks = Object.keys(step.a);
  var missing = blanks.some(function(k){ return !ss.inputs[k] || String(ss.inputs[k]).trim()===''; });
  if(missing){ fb.className='feedback show err'; fb.innerHTML='Fill in every blank in this step before checking.'; return; }

  var allGood=true;
  blanks.forEach(function(k){
    var good=answerMatches(ss.inputs[k], step.a[k], step.accept, step.expr);
    ss.inputs['fs_'+k]=good?'correct':'wrong';
    if(!good) allGood=false;
  });

  if(allGood){
    ss.status='correct'; playSuccess();
    advanceStepOrFinish(item, slide);
  } else {
    ss.attempts=(ss.attempts||0)+1;
    if(ss.attempts>=2){
      ss.status='revealed'; playReveal();
      advanceStepOrFinish(item, slide);
    } else {
      playWrong();
      fb.className='feedback show retry';
      fb.innerHTML='<b>Not quite — try again</b> (attempt 1 of 2) <span class="attempts-dots"><span class="used"></span><span></span></span>'; __flash={c:'retry',h:'<b>Not quite — try again</b> (attempt 1 of 2) <span class="attempts-dots"><span class="used"></span><span></span></span>'};
      renderSlide();
      return;
    }
  }
  renderSlide();
}

function advanceStepOrFinish(item, slide){
  var total = slide.flat.length;
  var hasExpr = slide.flat.some(function(s){ return s.expr===true; });
  var hasFrac = slide.flat.some(function(s){ return ['fv','fe','fl','fm','fi','flist'].indexOf(s.expr)>=0; });
  if(item.curStep < total-1){
    item.curStep++;
  } else {
    var anyRevealed = item.stepStates.some(function(ss){ return ss.status==='revealed'; });
    item.status = anyRevealed ? 'revealed' : 'correct';
  }
}

/* ================= palette ================= */
var overlay=document.getElementById('overlay');
function statusOf(tabId,i){
  var ts=state.tabs[tabId];
  if(i>ts.maxReached) return 'locked';
  if(i===ts.idx) return 'current';
  return ts.items[i].status==='unanswered' ? 'locked' : ts.items[i].status;
}
function buildPalette(){
  var slides=SLIDES[activeTab];
  document.getElementById('paletteTitle').textContent = TAB_DEFS.find(function(t){return t.id===activeTab;}).label+' · Question palette';
  var body=document.getElementById('paletteBody');
  var html='';
  for(var i=0;i<slides.length;i++){
    html += '<div class="chip" data-status="'+statusOf(activeTab,i)+'" data-idx="'+i+'">'+(i+1)+'</div>';
  }
  body.innerHTML = html;
  body.querySelectorAll('.chip').forEach(function(chip){
    chip.addEventListener('click', function(){
      var i=parseInt(chip.dataset.idx,10);
      var ts=state.tabs[activeTab];
      if(i>ts.maxReached){ showToast('Finish the earlier questions to unlock this one.'); return; }
      ts.idx=i; closePalette(); renderSlide();
    });
  });
}
function openPalette(){ buildPalette(); overlay.classList.add('show'); }
function closePalette(){ overlay.classList.remove('show'); }
var toastTimer;
function showToast(msg){
  var t=document.getElementById('toast'); t.textContent=msg; t.classList.add('show');
  clearTimeout(toastTimer); toastTimer=setTimeout(function(){ t.classList.remove('show'); },2200);
}
document.getElementById('paletteFab').addEventListener('click', openPalette);
document.getElementById('paletteClose').addEventListener('click', closePalette);
overlay.addEventListener('click', function(e){ if(e.target===overlay) closePalette(); });

function updateFab(){
  var slides=SLIDES[activeTab];
  var done=state.tabs[activeTab].items.filter(function(it){ return it.status==='correct'||it.status==='revealed'||it.status==='skipped'; }).length;
  document.getElementById('fabBadge').textContent = done+'/'+slides.length;
}

/* ================= overall progress + finish ================= */
function updateChapterProgress(){
  var total=0, done=0;
  TAB_DEFS.forEach(function(td){
    state.tabs[td.id].items.forEach(function(it){
      total++;
      if(it.status==='correct'||it.status==='revealed'||it.status==='skipped') done++;
    });
  });
  var pct = total>0 ? Math.round((done/total)*100) : 0;
  document.getElementById('cpFill').style.width=pct+'%';
  document.getElementById('cpLabel').textContent=pct+'% complete';
}
function isSlideCorrect(tabId,i){
  var slide=SLIDES[tabId][i], item=state.tabs[tabId].items[i];
  if(slide.kind==='mcq'||slide.kind==='ar') return item.choice===slide.correct;
  return slide.flat.every(function(step,si){
    var ss=item.stepStates[si];
    return Object.keys(step.a).every(function(k){ return answerMatches(ss.inputs[k], step.a[k], step.accept, step.expr); });
  });
}
function isSlideAttempted(tabId,i){
  var slide=SLIDES[tabId][i], item=state.tabs[tabId].items[i];
  if(slide.kind==='mcq'||slide.kind==='ar') return item.choice!==undefined;
  return slide.flat.some(function(step,si){
    var ss=item.stepStates[si];
    return Object.keys(step.a).some(function(k){ return ss.inputs[k] && String(ss.inputs[k]).trim()!==''; });
  });
}
function slideLabel(slide){
  var t = slide.kind==='case' ? slide.title : (slide.kind==='ar' ? slide.a : (slide.p||slide.text||''));
  t = String(t);
  return t.length>90 ? t.slice(0,90)+'…' : t;
}
function slideAnswerText(slide, item, correctSide){
  if(slide.kind==='mcq'||slide.kind==='ar'){
    var opts = slide.kind==='mcq' ? slide.opts : AR_OPTIONS;
    if(correctSide) return '('+LETTERS[slide.correct]+') '+opts[slide.correct];
    return item.choice!==undefined ? '('+LETTERS[item.choice]+') '+opts[item.choice] : '— not attempted —';
  }
  return slide.flat.map(function(step,si){
    var ss=item.stepStates[si];
    return Object.keys(step.a).map(function(k){
      return correctSide ? step.a[k] : (ss.inputs[k] || '—');
    }).join(', ');
  }).join('  |  ');
}

function renderFinished(){
  if(MODE==='quiz'){ renderQuizResults(); return; }
  var ts=state.tabs[activeTab];
  var correct=ts.items.filter(function(i){return i.status==='correct';}).length;
  var revealed=ts.items.filter(function(i){return i.status==='revealed';}).length;
  var skipped=ts.items.filter(function(i){return i.status==='skipped';}).length;
  var h='<div class="qcard done-card"><div class="big">✨</div><h2>Tab complete</h2>';
  h+='<p style="color:var(--ink-soft);font-size:14px;">You worked through all '+ts.items.length+' questions in this tab.</p>';
  if(!ts.recorded){ ts.recorded=true; addRecord('learning', activeTab, correct, revealed, skipped, ts.items.length); }
  h+='<div class="score-pills">'+
     '<span class="score-pill" style="background:var(--success-soft);color:var(--success);">'+correct+' correct</span>'+
     '<span class="score-pill" style="background:var(--danger-soft);color:var(--danger);">'+revealed+' revealed</span>'+
     '<span class="score-pill" style="background:var(--gold-soft);color:var(--retry-text);">'+skipped+' skipped</span></div>'+
     '<button class="btn btn-primary" id="btnReview">Review from question 1</button></div>';
  document.getElementById('wrap').innerHTML=h;
  document.getElementById('navbarInner').innerHTML='';
  document.getElementById('btnReview').addEventListener('click', function(){ ts.idx=0; ts.recorded=false; renderSlide(); });
  updateChapterProgress(); saveState();
}

function renderQuizResults(){
  var ts=state.tabs[activeTab];
  var slides=SLIDES[activeTab];
  var correctCount=0, attemptedCount=0;
  var rowsHtml = slides.map(function(slide,i){
    var item=ts.items[i];
    var ok=isSlideCorrect(activeTab,i);
    var att=isSlideAttempted(activeTab,i);
    if(ok) correctCount++;
    if(att) attemptedCount++;
    var tagCls = ok?'ok':(att?'bad':'na');
    var tagText = ok?'Correct':(att?'Incorrect':'Not attempted');
    var row='<div class="review-row">';
    row+='<span class="review-tag '+tagCls+'">Q'+(i+1)+' · '+tagText+'</span>';
    row+='<div class="review-q">'+fr(esc(slideLabel(slide)))+'</div>';
    row+='<div class="review-ans"><b>Your answer:</b> '+fr(esc(slideAnswerText(slide,item,false)))+'</div>';
    if(!ok) row+='<div class="review-ans" style="color:var(--success);"><b>Correct answer:</b> '+fr(esc(slideAnswerText(slide,item,true)))+'</div>';
    if(slide.sol) row+='<details class="rev-sol"><summary>Show solution</summary>'+solutionHTML(slide)+'</details>';
    row+='</div>';
    return row;
  }).join('');

  addRecord('quiz', activeTab, correctCount, 0, 0, slides.length);
  var h='<div class="qcard done-card" style="text-align:left;">';
  h+='<div style="text-align:center;"><div class="big">🏁</div><h2>Quiz complete</h2>';
  h+='<p style="color:var(--ink-soft);font-size:14px;">'+correctCount+' / '+slides.length+' correct · '+attemptedCount+' attempted</p></div>';
  h+='<div style="margin-top:16px;">'+rowsHtml+'</div>';
  h+='<div style="text-align:center;margin-top:6px;"><button class="btn btn-primary" id="btnReview">Review from question 1</button></div>';
  h+='</div>';
  document.getElementById('wrap').innerHTML=h;
  document.getElementById('navbarInner').innerHTML='';
  document.getElementById('btnReview').addEventListener('click', function(){ ts.idx=0; renderSlide(); });
  playSuccess();
  updateChapterProgress(); saveState();
}

/* ================= mode picker ================= */
function updateModePill(){
  var btn=document.getElementById('modePill');
  if(!btn) return;
  btn.textContent = MODE==='quiz' ? '📝 Quiz Mode · switch' : '📘 Learning Sheet · switch';
}
function showChrome(show){
  document.querySelector('.tabbar').style.display = show?'':'none';
  document.querySelector('.slide-progress').style.display = show?'':'none';
  document.querySelector('.navbar').style.display = show?'':'none';
  document.getElementById('paletteFab').style.display = show?'':'none';
}
function renderModePicker(){
  showChrome(false);
  var wrap=document.getElementById('wrap');
  wrap.innerHTML =
    '<div class="mode-pick">'+
      '<div class="mode-card" data-pick="learning"><div class="mode-icon">📘</div><h3>Learning Sheet</h3>'+
      '<p>Work through each question step by step with instant feedback — two tries, then the correct value is revealed right there so you can keep moving.</p></div>'+
      '<div class="mode-card" data-pick="quiz"><div class="mode-icon">📝</div><h3>Quiz Mode</h3>'+
      '<p>Attempt every question with no hints along the way. Your score and the full answer key are shown together once you finish the tab — just like the real exam.</p></div>'+
    '</div>';
  wrap.querySelectorAll('[data-pick]').forEach(function(card){
    card.addEventListener('click', function(){
      setMode(card.dataset.pick); activeTab='theory';
      document.getElementById('modePill').hidden=false;
      updateModePill();
      showChrome(true);
      buildTabbar();
      renderSlide();
    });
  });
}
document.getElementById('modePill').addEventListener('click', function(){
  if(!appState.mode){ return; }
  setMode(appState.mode==='quiz' ? 'learning' : 'quiz');
  updateModePill();
  showChrome(true);
  buildTabbar();
  renderSlide();
});

/* ================= boot ================= */
var _origRenderSlide = renderSlide;
renderSlide = function(){ _origRenderSlide(); updateChapterProgress(); updateModePill(); };


/* ================= theory tab ================= */
function renderTheory(){
  var wrap=document.getElementById('wrap');
  wrap.innerHTML='<div class="theory">'+fr(THEORY)+'</div>';
  document.querySelector('.slide-progress').style.display='none';
  document.querySelector('.navbar').style.display='none';
  document.getElementById('paletteFab').style.display='none';
  document.getElementById('secSub').textContent='Theory — notes, key ideas and worked examples';
  wrap.querySelectorAll('[data-go]').forEach(function(b){ b.addEventListener('click',function(){ activeTab=b.dataset.go; buildTabbar(); renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); }); });
  wrap.querySelectorAll('[data-jump]').forEach(function(b){ b.addEventListener('click',function(){ var t=document.getElementById(b.dataset.jump); if(t) t.scrollIntoView({behavior:'smooth',block:'start'}); }); });
}
var _rsTheory = renderSlide;
renderSlide = function(){
  if(activeTab==='theory'){ renderTheory(); buildTabbar(); updateChapterProgress(); updateModePill(); saveState(); return; }
  document.querySelector('.slide-progress').style.display='';
  document.querySelector('.navbar').style.display='';
  document.getElementById('paletteFab').style.display='';
  _rsTheory();
};


/* ================= MYP criterion report ================= */
var CRIT_COL={A:'var(--accent-text)',B:'var(--gold)',C:'#8A6FC4',D:'#2F9AA0'};
function critStats(){
  return REPORT.map(function(r){
    var tabId=r[0], slides=SLIDES[tabId], ts=state&&state.tabs[tabId];
    var c=0,w=0,n=0;
    slides.forEach(function(sl,i){
      if(!ts||!ts.items[i]){ n++; return; }
      var it=ts.items[i];
      if(MODE==='learning'){
        if(it.status==='correct') c++; else if(it.status==='revealed') w++; else n++;
      } else {
        if(isSlideCorrect(tabId,i)) c++; else if(isSlideAttempted(tabId,i)) w++; else n++;
      }
    });
    var tot=slides.length, pct=tot?Math.round(c/tot*100):0;
    var lvl=Math.round(c/Math.max(tot,1)*8);
    return {tab:tabId,letter:r[1],name:r[2],c:c,w:w,n:n,tot:tot,pct:pct,lvl:lvl};
  });
}
function arcPath(cx,cy,r,a0,a1){
  if(a1-a0>=Math.PI*2-1e-6){ return 'M'+(cx-r)+','+cy+' a'+r+','+r+' 0 1,0 '+(2*r)+',0 a'+r+','+r+' 0 1,0 '+(-2*r)+',0 Z'; }
  var x0=cx+r*Math.sin(a0), y0=cy-r*Math.cos(a0), x1=cx+r*Math.sin(a1), y1=cy-r*Math.cos(a1);
  return 'M'+cx+','+cy+' L'+x0.toFixed(2)+','+y0.toFixed(2)+' A'+r+','+r+' 0 '+((a1-a0)>Math.PI?1:0)+',1 '+x1.toFixed(2)+','+y1.toFixed(2)+' Z';
}
function pieSVG(parts,size,hole,center,sub){
  var tot=parts.reduce(function(s,p){return s+p.v;},0), cx=size/2, cy=size/2, r=size/2-4, a=0, h='';
  if(!tot){ h+='<circle cx="'+cx+'" cy="'+cy+'" r="'+r+'" style="fill:var(--paper-2);stroke:var(--rule)"/>'; }
  parts.forEach(function(p){ if(!p.v) return; var b=a+p.v/tot*Math.PI*2; h+='<path d="'+arcPath(cx,cy,r,a,b)+'" style="fill:'+p.col+';stroke:var(--card);stroke-width:2"><title>'+esc(p.label)+': '+p.v+'</title></path>'; a=b; });
  if(hole) h+='<circle cx="'+cx+'" cy="'+cy+'" r="'+(r*hole)+'" style="fill:var(--card)"/>';
  if(center) h+='<text x="'+cx+'" y="'+(cy-(sub?4:0))+'" text-anchor="middle" dominant-baseline="middle" style="fill:var(--ink);font:700 '+(size>150?22:15)+'px Fraunces,serif">'+center+'</text>';
  if(sub) h+='<text x="'+cx+'" y="'+(cy+16)+'" text-anchor="middle" style="fill:var(--ink-soft);font:600 11px \'Source Sans 3\',sans-serif">'+sub+'</text>';
  return '<svg viewBox="0 0 '+size+' '+size+'" width="'+size+'" height="'+size+'" role="img">'+h+'</svg>';
}
function band(l){ return l===0?'0':(l<=2?'1–2':(l<=4?'3–4':(l<=6?'5–6':'7–8'))); }
function renderReport(){
  var st=critStats(), totC=0, totQ=0;
  st.forEach(function(s){ totC+=s.c; totQ+=s.tot; });
  var h='<div class="theory">';
  h+='<section class="note"><h2>Chapter test report</h2><p class="lt">'+(MODE==='quiz'?'<b>Quiz mode</b> results: answers are marked when you finish each test tab.':'<b>Learning mode</b> results: a question counts as correct only if you got it without the answer being revealed. Switch to Quiz mode for an exam-style score.')+'</p>';
  h+='<div class="rep-top"><div class="rep-pie">'+pieSVG(st.map(function(s){return {v:s.c,col:CRIT_COL[s.letter],label:'Criterion '+s.letter};}),200,0.55,totC+'/'+totQ,'correct')+'</div>';
  h+='<div class="rep-legend"><div class="rep-cap">Marks earned, by criterion</div>'+st.map(function(s){ return '<div class="rep-li"><span class="sw" style="background:'+CRIT_COL[s.letter]+'"></span><b>'+s.letter+'</b>&nbsp;'+esc(s.name)+'<span class="rep-n">'+s.c+' / '+s.tot+'</span></div>'; }).join('')+'</div></div></section>';
  h+='<div class="rep-grid">'+st.map(function(s){
    return '<div class="rep-card"><div class="rep-h"><span class="crit" style="background:'+CRIT_COL[s.letter]+'">'+s.letter+'</span>'+esc(s.name)+'</div>'+
      '<div class="rep-row">'+pieSVG([{v:s.c,col:'var(--success)',label:'Correct'},{v:s.w,col:'var(--danger)',label:'Incorrect'},{v:s.n,col:'var(--locked)',label:'Not attempted'}],120,0.5,s.pct+'%')+
      '<div class="rep-stats"><div><span class="sw" style="background:var(--success)"></span>Correct <b>'+s.c+'</b></div><div><span class="sw" style="background:var(--danger)"></span>Incorrect <b>'+s.w+'</b></div><div><span class="sw" style="background:var(--locked)"></span>Not attempted <b>'+s.n+'</b></div>'+
      '<div class="rep-lvl">Indicative level <b>'+s.lvl+'</b> / 8 <span>(band '+band(s.lvl)+')</span></div></div></div>'+
      '<button class="hub-btn" data-go="'+s.tab+'">Open Test '+s.letter+' →</button></div>';
  }).join('')+'</div>';
  h+='<p class="rep-note">Indicative level = fraction of questions correct × 8, rounded. It is a practice guide only; your teacher awards the real MYP criterion levels.</p></div>';
  var wrap=document.getElementById('wrap'); wrap.innerHTML=h;
  document.querySelector('.slide-progress').style.display='none';
  document.querySelector('.navbar').style.display='none';
  document.getElementById('paletteFab').style.display='none';
  document.getElementById('secSub').textContent='Report — chapter test results by MYP criterion';
  wrap.querySelectorAll('[data-go]').forEach(function(b){ b.addEventListener('click',function(){ activeTab=b.dataset.go; buildTabbar(); renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); }); });
}
var _rsReport = renderSlide;
renderSlide = function(){
  if(activeTab==='report'){ renderReport(); buildTabbar(); updateChapterProgress(); updateModePill(); saveState(); return; }
  _rsReport();
};


/* ================= skipped-question return ================= */
function firstSkippedIdx(ts){
  for(var i=0;i<ts.items.length;i++){
    var it=ts.items[i];
    if(MODE==='quiz'){ if(!isSlideAttempted(activeTab,i)) return i; }
    else if(it.status==='skipped'||it.status==='unanswered') return i;
  }
  return -1;
}
function skippedList(ts){
  var out=[]; for(var i=0;i<ts.items.length;i++){ var it=ts.items[i];
    if(MODE==='quiz' ? !isSlideAttempted(activeTab,i) : (it.status==='skipped'||it.status==='unanswered')) out.push(i); }
  return out;
}
function renderSkipGate(ts){
  var list=skippedList(ts);
  var h='<div class="qcard done-card"><div class="big">⏭️</div><h2>You skipped '+list.length+' question'+(list.length>1?'s':'')+'</h2>'+
    '<p style="color:var(--ink-soft);font-size:14px;">Answer them now, or submit the tab as it is. Answers are marked only when you submit.</p>'+
    '<div class="skip-chips">'+list.map(function(i){ return '<button class="chip skip-go" data-i="'+i+'">Q'+(i+1)+'</button>'; }).join('')+'</div>'+
    '<div class="skip-btns"><button class="btn btn-primary" id="btnGoSkipped">Answer skipped questions</button><button class="btn" id="btnSubmitAnyway">Submit anyway</button></div></div>';
  document.getElementById('wrap').innerHTML=h;
  document.getElementById('navbarInner').innerHTML='';
  var go=function(i){ ts.idx=i; ts.maxReached=Math.max(ts.maxReached,i); renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); };
  document.getElementById('btnGoSkipped').addEventListener('click',function(){ go(list[0]); });
  document.querySelectorAll('.skip-go').forEach(function(b){ b.addEventListener('click',function(){ go(parseInt(b.dataset.i,10)); }); });
  document.getElementById('btnSubmitAnyway').addEventListener('click',function(){ ts.submitOK=true; renderFinished(); ts.submitOK=false; });
  saveState();
}
var _rfSkip = renderFinished;
renderFinished = function(){
  var ts=state.tabs[activeTab];
  if(MODE==='quiz' && !ts.submitOK && skippedList(ts).length){ renderSkipGate(ts); return; }
  _rfSkip();
  if(MODE==='learning'){
    var list=skippedList(ts);
    if(list.length){
      var card=document.querySelector('.done-card');
      if(card){ var d=document.createElement('div'); d.className='skip-btns';
        d.innerHTML='<button class="btn btn-primary" id="btnGoSkipped">Attempt skipped questions ('+list.length+')</button>';
        card.appendChild(d);
        document.getElementById('btnGoSkipped').addEventListener('click',function(){ ts.idx=list[0]; ts.recorded=false; renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); }); }
    }
  }
};


/* ================= approx answers (physics: within 1%) ================= */
var _amTools = answerMatches;
answerMatches = function(input,answer,accept,expr){
  if(expr==='approx'){
    var n1=parseNum(input); if(n1===null) return false;
    return [answer].concat(accept||[]).some(function(a){ var n2=parseNum(a); if(n2===null) return false; return Math.abs(n1-n2) <= Math.max(0.011*Math.abs(n2), 1e-9); });
  }
  return _amTools(input,answer,accept,expr);
};

/* ================= palette: every question already reached can be opened ================= */
statusOf = function(tabId,i){
  var ts=state.tabs[tabId];
  if(i>ts.maxReached) return 'locked';
  if(i===ts.idx) return 'current';
  var s=ts.items[i].status;
  if(s==='unanswered') return 'skipped';
  return s;
};

/* ================= on-screen keyboard ================= */
var KB={on:true, page:'num', target:null};
try{ var kbp=localStorage.getItem('sopaan-kb-pref'); if(kbp==='off') KB.on=false; }catch(e){}
function kbSave(){ try{ localStorage.setItem('sopaan-kb-pref', KB.on?'on':'off'); }catch(e){} }
var KEYS_NUM=[['7','8','9','÷','(',')'],['4','5','6','×','^','²'],['1','2','3','−','x','π'],['0','.','/','+','t','°'],['abc','←','→','⌫','Clear','Done']];
var KEYS_ABC=[['q','w','e','r','t','y','u','i','o','p'],['a','s','d','f','g','h','j','k','l','-'],['z','x','c','v','b','n','m',',',':','/'],['123','space','←','→','⌫','Done']];
function kbBuild(){
  var el=document.getElementById('vkb'); if(!el){ el=document.createElement('div'); el.id='vkb'; el.className='vkb'; document.body.appendChild(el);
    el.addEventListener('pointerdown',function(e){ var b=e.target.closest('button[data-k]'); e.preventDefault(); if(b) kbPress(b.dataset.k); });
    el.addEventListener('mousedown',function(e){ e.preventDefault(); }); }
  var rows=KB.page==='num'?KEYS_NUM:KEYS_ABC;
  el.innerHTML='<div class="vkb-top"><span>⌨️ Keyboard</span><button data-k="device" class="vkb-link">Use device keyboard</button></div>'+
    rows.map(function(r){ return '<div class="vkb-row">'+r.map(function(k){
      var cls='vkb-k'+(/^(abc|123|Done|Clear|⌫|←|→|space)$/.test(k)?' fn':'')+(k==='Done'?' done':'');
      return '<button type="button" class="'+cls+'" data-k="'+k+'">'+(k==='space'?'space':k)+'</button>'; }).join('')+'</div>'; }).join('');
  return el;
}
function kbShow(inp){ KB.target=inp; if(!KB.on) return; var cp=document.getElementById('calcPanel'); if(cp&&cp.classList.contains('show')) return; var el=kbBuild(); var nb=document.querySelector('.navbar'); el.style.bottom=(nb?nb.getBoundingClientRect().height:0)+'px'; el.classList.add('show'); document.body.classList.add('kb-open'); setTimeout(function(){ var r=inp.getBoundingClientRect(), top=el.getBoundingClientRect().top; if(r.bottom>top-12) window.scrollBy({top:r.bottom-top+60,behavior:'smooth'}); else if(r.top<60) window.scrollBy({top:r.top-80,behavior:'smooth'}); },30); }
function kbHide(){ var el=document.getElementById('vkb'); if(el) el.classList.remove('show'); document.body.classList.remove('kb-open'); }
function kbInsert(s){
  var t=KB.target; if(!t||t.disabled) return;
  var a=t.selectionStart==null?t.value.length:t.selectionStart, b=t.selectionEnd==null?a:t.selectionEnd;
  t.value=t.value.slice(0,a)+s+t.value.slice(b); var p=a+s.length; try{ t.setSelectionRange(p,p); }catch(e){}
  t.dispatchEvent(new Event('input',{bubbles:true}));
}
function kbPress(k){
  var t=KB.target; if(k==='device'){ KB.on=false; kbSave(); kbHide(); document.querySelectorAll('.blank-input').forEach(function(i){ i.removeAttribute('inputmode'); }); if(t){ t.blur(); setTimeout(function(){ t.focus(); },50); } showToast('Device keyboard on. Tap ⌨️ on any blank to bring the on-screen keyboard back.'); return; }
  if(k==='Done'){ kbHide(); if(t) t.blur(); return; }
  if(k==='abc'||k==='123'){ KB.page=(k==='abc')?'abc':'num'; kbBuild(); return; }
  if(!t) return;
  if(k==='⌫'){ var a=t.selectionStart, b=t.selectionEnd; if(a===b&&a>0){ t.value=t.value.slice(0,a-1)+t.value.slice(b); try{t.setSelectionRange(a-1,a-1);}catch(e){} } else { t.value=t.value.slice(0,a)+t.value.slice(b); try{t.setSelectionRange(a,a);}catch(e){} } t.dispatchEvent(new Event('input',{bubbles:true})); return; }
  if(k==='Clear'){ t.value=''; t.dispatchEvent(new Event('input',{bubbles:true})); return; }
  if(k==='←'||k==='→'){ var p=(t.selectionStart||0)+(k==='←'?-1:1); p=Math.max(0,Math.min(t.value.length,p)); try{t.setSelectionRange(p,p);}catch(e){} return; }
  var map={'−':'-','space':' '}; kbInsert(map[k]!==undefined?map[k]:k);
}
function kbWire(){
  document.querySelectorAll('.blank-input').forEach(function(inp){
    if(inp.dataset.kb) return; inp.dataset.kb='1';
    if(KB.on) inp.setAttribute('inputmode','none');
    inp.addEventListener('focus',function(){ kbShow(inp); });
    var btn=document.createElement('button'); btn.type='button'; btn.className='kb-toggle'; btn.title='On-screen keyboard'; btn.textContent='⌨️'; btn.tabIndex=-1;
    btn.addEventListener('mousedown',function(e){ e.preventDefault(); });
    btn.addEventListener('click',function(){ KB.on=true; kbSave(); document.querySelectorAll('.blank-input').forEach(function(i){ i.setAttribute('inputmode','none'); }); inp.focus(); kbShow(inp); });
    if(!inp.disabled) inp.insertAdjacentElement('afterend',btn);
  });
}
document.addEventListener('focusout',function(e){ setTimeout(function(){ var a=document.activeElement; if(!a||!a.classList||!a.classList.contains('blank-input')){ if(!document.querySelector('#vkb:hover')) kbHide(); } },120); });

/* ================= calculator ================= */
var CALC={expr:'', ans:0};
function calcEval(src){
  var s=String(src).replace(/×/g,'*').replace(/÷/g,'/').replace(/−/g,'-').replace(/π/g,'(PI)').replace(/Ans/g,'('+CALC.ans+')').replace(/\^/g,'**').replace(/√\(/g,'sqrt(').replace(/²/g,'**2').replace(/E/g,'*10**');
  s=s.replace(/(^|[(*\/+\-,])-/g,'$1(-1)*');
  if(/[^0-9+\-*/().,a-z A-Z]/.test(s)) throw 0;
  var ok=s.replace(/sin|cos|tan|asin|acos|atan|sqrt|log|ln|PI|abs/g,''); if(/[a-zA-Z]/.test(ok)) throw 0;
  var f=new Function('sin','cos','tan','asin','acos','atan','sqrt','log','ln','PI','abs','return ('+s+');');
  var d=Math.PI/180;
  var v=f(function(x){return Math.sin(x*d);},function(x){return Math.cos(x*d);},function(x){return Math.tan(x*d);},
    function(x){return Math.asin(x)/d;},function(x){return Math.acos(x)/d;},function(x){return Math.atan(x)/d;},Math.sqrt,Math.log10,Math.log,Math.PI,Math.abs);
  if(typeof v!=='number'||!isFinite(v)) throw 0; return v;
}
function fmtNum(v){ if(Math.abs(v)>=1e10||(Math.abs(v)<1e-6&&v!==0)) return v.toExponential(6).replace(/\.?0+e/,'e'); return String(parseFloat(v.toPrecision(10))); }
var CKEYS=[['sin(','cos(','tan(','√(','^','²'],['asin(','acos(','atan(','(',')','π'],['7','8','9','÷','⌫','AC'],['4','5','6','×','E','Ans'],['1','2','3','−','(−)','Insert'],['0','.','=','+']];
function openCalc(){
  var p=document.getElementById('calcPanel');
  if(!p){ p=document.createElement('div'); p.id='calcPanel'; p.className='tool-panel calc';
    p.innerHTML='<div class="tp-head"><b>🧮 Calculator</b><span class="tp-note">degrees · tap a blank, then Insert</span><button class="tp-x" data-c="close">✕</button></div>'+
      '<div class="calc-disp"><div class="calc-expr" id="calcExpr"></div><div class="calc-res" id="calcRes">0</div></div>'+
      '<div class="calc-keys">'+CKEYS.map(function(r){ return r.map(function(k){ return '<button type="button" data-c="'+k+'" class="'+(k==='='?'eq':(/^(AC|⌫|Insert)$/.test(k)?'fn':''))+'">'+({'sin(':'sin','cos(':'cos','tan(':'tan','asin(':'sin⁻¹','acos(':'cos⁻¹','atan(':'tan⁻¹','√(':'√'}[k]||k)+'</button>'; }).join(''); }).join('')+'</div>';
    document.body.appendChild(p);
    p.addEventListener('mousedown',function(e){ if(e.target.closest('button')) e.preventDefault(); });
    p.addEventListener('click',function(e){ var b=e.target.closest('button[data-c]'); if(!b) return; calcKey(b.dataset.c); });
  }
  kbHide(); var nb=document.querySelector('.navbar'); p.style.bottom=((nb?nb.getBoundingClientRect().height:0)+8)+'px'; p.classList.add('show'); document.body.classList.add('calc-open'); calcShow();
}
function calcShow(res){ document.getElementById('calcExpr').textContent=CALC.expr||' '; if(res!==undefined) document.getElementById('calcRes').textContent=res; }
function calcKey(k){
  if(k==='close'){ document.getElementById('calcPanel').classList.remove('show'); document.body.classList.remove('calc-open'); return; }
  if(k==='AC'){ CALC.expr=''; calcShow('0'); return; }
  if(k==='⌫'){ CALC.expr=CALC.expr.replace(/(asin\(|acos\(|atan\(|sin\(|cos\(|tan\(|√\(|Ans|.)$/,''); calcShow(); return; }
  if(k==='='){ try{ var v=calcEval(CALC.expr); CALC.ans=v; calcShow(fmtNum(v)); }catch(e){ calcShow('Error'); } return; }
  if(k==='(−)'){ CALC.expr+='−'; calcShow(); return; }
  if(k==='Insert'){ var r=document.getElementById('calcRes').textContent; if(KB.target && !KB.target.disabled && r!=='Error'){ KB.target.value=r; KB.target.dispatchEvent(new Event('input',{bubbles:true})); showToast('Inserted '+r+' into the blank.'); } else showToast('Tap a blank first, then press Insert.'); return; }
  CALC.expr+=k; calcShow();
}

/* ================= Desmos ================= */
var DESMOS_KEY='dcb31709b452b1cf9dc26972add0fda6', desmosCalc=null, desmosLoading=false;
function openDesmos(exprs){
  var p=document.getElementById('desmosPanel');
  if(!p){ p=document.createElement('div'); p.id='desmosPanel'; p.className='tool-panel desmos';
    p.innerHTML='<div class="tp-head"><b>📈 Desmos graphing calculator</b><button class="tp-x" id="desmosReset">Reset graph</button><button class="tp-x" id="desmosClose">✕</button></div><div id="desmosBox"><div class="desmos-msg">Loading Desmos…</div></div>';
    document.body.appendChild(p);
    document.getElementById('desmosClose').addEventListener('click',function(){ p.classList.remove('show'); });
    document.getElementById('desmosReset').addEventListener('click',function(){ if(desmosCalc) desmosSet(p._exprs||[]); });
  }
  p._exprs=exprs||[]; p.classList.add('show');
  if(window.Desmos){ desmosInit(); desmosSet(p._exprs); return; }
  if(desmosLoading) return; desmosLoading=true;
  var sc=document.createElement('script'); sc.src='https://www.desmos.com/api/v1.9/calculator.js?apiKey='+DESMOS_KEY;
  sc.onload=function(){ desmosInit(); desmosSet(p._exprs); };
  sc.onerror=function(){ desmosLoading=false; document.getElementById('desmosBox').innerHTML='<div class="desmos-msg">Desmos needs an internet connection. <a href="https://www.desmos.com/calculator" target="_blank" rel="noopener">Open Desmos in a new tab</a>.</div>'; };
  document.head.appendChild(sc);
}
function desmosInit(){ if(desmosCalc) return; var box=document.getElementById('desmosBox'); box.innerHTML=''; desmosCalc=Desmos.GraphingCalculator(box,{expressionsCollapsed:false,settingsMenu:false,border:false,degreeMode:true}); }
function desmosSet(exprs){ if(!desmosCalc) return; desmosCalc.setBlank(); (exprs||[]).forEach(function(e,i){ if(typeof e==='string') desmosCalc.setExpression({id:'e'+i,latex:e}); else desmosCalc.setExpression(Object.assign({id:'e'+i},e)); }); }

/* ================= toolbar on each question ================= */
var _rsTools = renderSlide;
renderSlide = function(){
  _rsTools();
  kbHide();
  if(activeTab==='theory'||activeTab==='report') return;
  var ts=state.tabs[activeTab]; if(!ts) return;
  var slide=SLIDES[activeTab][ts.idx], card=document.querySelector('#wrap .qcard');
  if(card && slide && slide.tools && slide.tools.length && !card.querySelector('.tool-bar')){
    var bar=document.createElement('div'); bar.className='tool-bar';
    bar.innerHTML=(slide.tools.indexOf('calc')>=0?'<button type="button" class="tool-btn" data-t="calc">🧮 Calculator</button>':'')+
                  (slide.tools.indexOf('desmos')>=0?'<button type="button" class="tool-btn" data-t="desmos">📈 Desmos graph</button>':'');
    card.insertBefore(bar, card.firstChild);
    bar.addEventListener('click',function(e){ var b=e.target.closest('[data-t]'); if(!b) return; if(b.dataset.t==='calc') openCalc(); else openDesmos(slide.desmos||[]); });
  }
  kbWire();
};

renderLogin();
})();
</script>
</body>
</html>
