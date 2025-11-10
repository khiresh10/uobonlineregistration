<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>ATM → Online Banking Registration — Step-by-Step Guide</title>
  <style>
    /* ===== THEME (UOB palette) ===== */
    :root{
      --uob-blue:#0050A0; /* primary */
      --uob-red:#ED1C24;  /* accent */
      --bg:#0b1020; --panel:#11162a; --ink:#e7ebff; --muted:#9aa5d1; --border:rgba(255,255,255,.08);
      --shadow:0 10px 30px rgba(0,0,0,.35); --radius:16px;
      /* background image controls */
      --bgimg:url('make-tmrw-yours-mob.jpg');
      --bgimg-opacity: .12;
    }
    *{box-sizing:border-box}
    html,body{ $1 }
    /* full-viewport background image overlay */
    body::before{ content:""; position:fixed; inset:0; background-image:var(--bgimg); background-size:cover; background-position:center; background-repeat:no-repeat; opacity:var(--bgimg-opacity); pointer-events:none; z-index:0 }
    html{ scroll-behavior:smooth }
    body{ margin:0; font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Ubuntu, Cantarell, Noto Sans, Arial; color:var(--ink);
      background: radial-gradient(1200px 600px at 80% -50%, color-mix(in oklab, var(--uob-blue) 30%, transparent), transparent 60%),
                  radial-gradient(800px 500px at -20% -40%, color-mix(in oklab, var(--uob-red) 24%, transparent), transparent 60%), var(--bg) }
    .app{ max-width:1080px; margin:24px auto; padding:16px }

    /* ===== APP BAR ===== */
    header.appbar{ position:sticky; top:0; z-index:100; backdrop-filter:blur(10px); background:color-mix(in oklab, var(--bg) 75%, transparent); border-bottom:1px solid var(--border) }
    .appbar-inner{ display:flex; gap:16px; align-items:center; padding:12px 8px }
    .logo-sq{ width:36px; height:36px; border-radius:10px; background:linear-gradient(135deg, var(--uob-blue), var(--uob-red)); box-shadow:var(--shadow) }
    .title{ font-weight:700; letter-spacing:.2px }
    .spacer{ flex:1 }
    .bar-actions{ display:flex; gap:8px; align-items:center }
    .quicknav{ display:flex; gap:8px; margin-left:12px }
    .qbtn{ background:transparent; border:1px solid var(--border); color:var(--ink); padding:6px 10px; border-radius:10px; cursor:pointer; font-size:13px }
    .qbtn:hover{ outline:2px solid var(--uob-blue) }
    button.icon{ display:inline-grid; place-items:center; width:36px; height:36px; border-radius:12px; border:1px solid var(--border); background:rgba(255,255,255,.03); color:var(--ink); cursor:pointer }
    button.icon:hover{ background:rgba(255,255,255,.08) }
    .bank-logo{ height:28px; width:auto; display:inline-block; margin-left:6px; filter: drop-shadow(0 2px 6px rgba(0,0,0,.35)); }
    @media (max-width:600px){ .bank-logo{ height:22px } }

    /* ===== LAYOUT ===== */
    main{ display:grid; grid-template-columns:300px 1fr; gap:16px; margin-top:16px }
    @media (max-width:980px){ main{ grid-template-columns:1fr } .sidebar{ order:2 } }
    .panel{ background:color-mix(in oklab, var(--panel) 92%, transparent); border:1px solid var(--border); border-radius:var(--radius); box-shadow:var(--shadow) }

    .sidebar{ padding:14px; position:sticky; top:68px; height:calc(100vh - 88px); overflow:auto }

    /* Progress */
    .progress{ margin:12px 0 16px; height:10px; background:#0e1430; border-radius:999px; overflow:hidden; border:1px solid var(--border) }
    .progress > span{ display:block; height:100%; width:0%; background:var(--uob-red, #ED1C24); transition: width .35s ease }

    /* Tabs */
    .tabs{ display:flex; gap:6px; margin:8px 0 10px }
    .tab{ flex:1; background:transparent; border:1px solid var(--border); color:var(--ink); padding:8px 10px; border-radius:10px; cursor:pointer; font-size:13px }
    .tab[aria-selected="true"]{ outline:2px solid var(--uob-blue) }

    /* TOC + Checklist */
    .toc{ list-style:none; padding:0; margin:10px 0; display:flex; flex-direction:column; gap:6px }
    .toc button{ width:100%; text-align:left; background:transparent; border:1px solid var(--border); color:var(--ink); padding:10px 12px; border-radius:12px; cursor:pointer }
    .toc button[aria-current="step"]{ outline:2px solid var(--uob-blue) }

    .checklist{ list-style:none; padding:0; margin:10px 0; display:flex; flex-direction:column; gap:6px }
    .check-item{ display:flex; align-items:center; gap:10px; border:1px solid var(--border); border-radius:12px; padding:10px 12px; background:rgba(255,255,255,.02) }
    .check-item input{ width:18px; height:18px }

    /* Content */
    .content{ padding:16px }
    .step{ $1 scroll-margin-top:76px }
    .step h2{ margin:0 0 8px; font-size:20px; display:flex; align-items:center; gap:8px }
    .meta{ display:flex; gap:12px; align-items:center; color:var(--muted); font-size:13px; margin-bottom:10px }
    .pill{ padding:4px 8px; border-radius:999px; background:rgba(0,80,160,.16); color:var(--ink); border:1px solid var(--border) }
    .stepdone{ margin-left:auto; display:inline-flex; align-items:center; gap:6px; font-size:13px; color:var(--muted) }

    /* i-term */
    .term{ display:inline-flex; align-items:center; gap:6px; border:none; background:none; color:#0050A0 !important; padding:0; cursor:pointer; font-weight:700 }
    .term .i{ display:inline-grid; place-items:center; width:16px; height:16px; font-size:12px; border-radius:999px; border:1px solid #0050A0 !important; color:#0050A0 !important }
    .term:hover{ text-decoration:underline }
    .term .i{ display:inline-grid; place-items:center; width:16px; height:16px; font-size:12px; border-radius:999px; border:1px solid currentColor }

    /* Corner glossary panel */
    .gpanel{ position:fixed; right:16px; bottom:16px; width:360px; max-width:94vw; background:var(--panel); color:var(--ink); border:1px solid var(--border); border-radius:14px; box-shadow:var(--shadow); padding:12px; z-index:200; /* animated bubble */ opacity:0; transform:translateY(8px) scale(.98); pointer-events:none; transition: opacity .28s ease, transform .28s ease }
    .gpanel[data-open="true"]{ opacity:1; transform:translateY(0) scale(1); pointer-events:auto }
    .gpanel h3{ margin:0 0 6px; font-size:14px; color:var(--ink) }
    .gpanel p{ margin:0; font-size:13px; color:inherit }
    .gpanel .row{ display:flex; gap:8px; align-items:center; margin-bottom:6px }
    .gpanel .close{ margin-left:auto; background:transparent; border:1px solid var(--border); color:var(--ink); border-radius:8px; padding:4px 8px; cursor:pointer }

    .toast{ position:fixed; bottom:16px; left:50%; transform:translateX(-50%); background:#0c132e; color:var(--ink); padding:10px 14px; border-radius:10px; border:1px solid var(--border); box-shadow:var(--shadow); display:none; z-index:120 }

    @media print{ header, .sidebar, .toast, .gpanel{ display:none !important } body{ background:white; color:black } .content{ padding:0 } .step{ page-break-inside:avoid } }
  </style>
</head>
<body>
  <header class="appbar">
    <div class="app appbar-inner">
      <div class="logo-sq" aria-hidden="true"></div>
      <div class="title">ATM → Online Banking Registration</div>
      <nav class="quicknav" aria-label="Quick actions">
        <button class="qbtn" id="qReg" aria-label="Go to Online Banking Registration">Online Banking Registration</button>
        <button class="qbtn" id="qReset" aria-label="Go to Password Reset">Password Reset</button>
        <button class="qbtn" id="qUnusual" aria-label="Go to Unusual Activity Detected">Unusual Activity Detected</button>
      </nav>
      <div class="spacer"></div>
      <div class="bar-actions">
        <button class="icon" id="toggleDark" aria-pressed="false" title="Toggle dark mode" aria-label="Toggle dark mode">🌙</button>
        <button class="icon" id="printBtn" title="Print / Save PDF" aria-label="Print or Save PDF">🖨️</button>
        <button class="icon" id="resetBtn" title="Reset progress" aria-label="Reset progress">♻️</button>
        <!-- UOB logo image: keep file name the same directory as HTML -->
        <img src="uob logo.png" alt="UOB" class="bank-logo" onerror="this.style.display='none'"/>
      </div>
    </div>
  </header>

  <div class="app">
    <main>
      <aside class="panel sidebar" aria-label="Sidebar navigation">
        <div style="font-size:13px;opacity:.9">Follow each step. Tick off completed steps; your progress is saved locally.</div>
        <div class="progress" role="progressbar" aria-valuemin="0" aria-valuemax="100" aria-valuenow="0" aria-label="Progress">
          <span id="bar"></span>
        </div>

        <div class="tabs" role="tablist">
          <button id="tabGuide" class="tab" role="tab" aria-selected="true" aria-controls="panelGuide">Guide</button>
          <button id="tabChecklist" class="tab" role="tab" aria-selected="false" aria-controls="panelChecklist">Checklist</button>
        </div>

        <div id="panelGuide" role="tabpanel" aria-labelledby="tabGuide">
          <ul class="toc" id="toc" aria-label="Steps navigation"></ul>
        </div>
        <div id="panelChecklist" role="tabpanel" aria-labelledby="tabChecklist" hidden>
          <ul class="checklist" id="checklist"></ul>
        </div>
      </aside>

      <section class="panel content">
        <article id="steps"></article>
      </section>
    </main>
  </div>

  <!-- Corner glossary panel -->
  <div id="gPanel" class="gpanel" role="dialog" aria-modal="false" aria-live="polite" aria-hidden="true">
    <div class="row">
      <strong id="gTerm">Glossary</strong>
      <button class="close" id="gClose" aria-label="Close glossary">✕</button>
    </div>
    <div id="gBody"><em>Click any i icon to see the explanation here.</em></div>
  </div>

  <div id="toast" class="toast" role="status" aria-live="polite"></div>

  <script>
    /* ===== Content Data ===== */
    const hotline = "03-2612 8101";

    const steps = [
      { id:"atm-reg", title:"Get Temporary Username & Password at the ATM", tag:"ATM", items:[
        "Insert your debit/credit card at the ATM and select language.",
        "Choose <b><span class=term data-key=atm_services role=button tabindex=0>ATM Services<span class=i>i</span></span></b> (only for <span class=term data-key=credit_card role=button tabindex=0>Credit Card<span class=i>i</span></span> flows).",
        "Enter your 6-digit <span class=term data-key=atm_pin role=button tabindex=0>ATM PIN<span class=i>i</span></span>.",
        "For <span class=term data-key=credit_card role=button tabindex=0>Credit Card<span class=i>i</span></span>: 1) Others → 2) Internet Banking → 3) Online Registration.",
        "For <span class=term data-key=debit_card role=button tabindex=0>Debit Card<span class=i>i</span></span>: 1) Others → 2) Others → 3) Online Banking/TPin Reset → 4) Online Banking Registration.",
        "Create a <span class=term data-key=temp_password role=button tabindex=0>Temporary Password<span class=i>i</span></span> of 8 digits and re-enter to confirm.",
        "Enter mobile phone no. to receive <span class=term data-key=sms_otp role=button tabindex=0>SMS-OTP<span class=i>i</span></span> (Malaysia & Singapore numbers only).",
        "Your <span class=term data-key=temp_username role=button tabindex=0>Temporary Username<span class=i>i</span></span> prints on the ATM receipt and you’ll also get an SMS once successful."
      ]},
      { id:"download", title:"Download & Log In to <span class=term data-key=uob_tmrw role=button tabindex=0>UOB TMRW<span class=i>i</span></span>", tag:"App", items:[
        "Allow notifications when prompted, then tap <b>Login</b>.",
        "Log in with the temporary username & <span class=term data-key=temp_password role=button tabindex=0>Temporary Password<span class=i>i</span></span> from the ATM.",
        "Set <b>Current Password</b> to the temporary one, then create a new <span class=term data-key=username role=button tabindex=0>Username<span class=i>i</span></span> and new <span class=term data-key=password role=button tabindex=0>Password<span class=i>i</span></span>.",
        "Log out and log back in using your new <span class=term data-key=username role=button tabindex=0>Username<span class=i>i</span></span> and <span class=term data-key=password role=button tabindex=0>Password<span class=i>i</span></span>."
      ]},
      { id:"secure-pin", title:"Create <span class=term data-key=secure_pin role=button tabindex=0>Secure PIN<span class=i>i</span></span>", tag:"Security", items:[
        "Enter your new <span class=term data-key=username role=button tabindex=0>Username<span class=i>i</span></span> & <span class=term data-key=password role=button tabindex=0>Password<span class=i>i</span></span> to begin <span class=term data-key=uob_access role=button tabindex=0>UOB Access<span class=i>i</span></span> registration.",
        "Enter the <span class=term data-key=sms_otp role=button tabindex=0>SMS-OTP<span class=i>i</span></span> sent to your phone.",
        "Tap <b>Set up <span class=term data-key=secure_pin role=button tabindex=0>Secure PIN<span class=i>i</span></span></b> and choose verification: <span class=term data-key=card_pin role=button tabindex=0>Card & PIN<span class=i>i</span></span> or <span class=term data-key=email_sms_otp role=button tabindex=0>Email and SMS OTP<span class=i>i</span></span>.",
        "Tap <b>Create <span class=term data-key=secure_pin role=button tabindex=0>Secure PIN<span class=i>i</span></span></b>, enter a 6-digit code, then re-enter to confirm."
      ]},
      { id:"activate", title:"<span class=term data-key=secure_pin_activation role=button tabindex=0>Activate Secure PIN<span class=i>i</span></span> (Call Centre)", tag:"Call", items:[
        `Dial <b>${hotline}</b> on your <span class=term data-key=phone_keypad role=button tabindex=0>Phone Keypad<span class=i>i</span></span>`,
        "Select language and request <b>Secure PIN Activation</b> to the CS Agent.",
        "Answer <span class=term data-key=reverification role=button tabindex=0>Reverification<span class=i>i</span></span> questions if prompted.",
        "Agent may advise that full transaction access starts after 12 hours; <span class=\"term\" data-key=\"cooldown_options\" role=\"button\" tabindex=\"0\">other app options<span class=\"i\">i</span></span> remain available meanwhile."
      ]},
      { id:"secret-word", title:"Create <span class=term data-key=secret_word role=button tabindex=0>Secret Word<span class=i>i</span></span> (optional – Personal Internet Banking)", tag:"Optional", items:[
        "Tap <b>Create now</b>.",
        "Enter Secret Word and confirm.",
        "Key in your <span class=term data-key=secret_word role=button tabindex=0>SECURE WORD<span class=i>i</span></span> to confirm."
      ]},
      { id:"reset", title:"Password Reset via ATM (if you forgot your password)", tag:"Reset", items:[
        "Insert your debit/credit card at the ATM and select language.",
        "Choose <b><span class=term data-key=atm_services role=button tabindex=0>ATM Services<span class=i>i</span></span></b> (only for <span class=term data-key=credit_card role=button tabindex=0>Credit Card<span class=i>i</span></span> flows).",
        "Enter your 6-digit <span class=term data-key=atm_pin role=button tabindex=0>ATM PIN<span class=i>i</span></span>.",
        "For <span class=term data-key=credit_card role=button tabindex=0>Credit Card<span class=i>i</span></span>: 1) Others → 2) Internet Banking → 3) Password Reset.",
        "For <span class=term data-key=debit_card role=button tabindex=0>Debit Card<span class=i>i</span></span>: 1) Others → 2) Others → 3) Online Banking/TPin Reset → 4) Password Reset.",
        "Create a new 8‑digit <span class=term data-key=temp_password role=button tabindex=0>Temporary Password<span class=i>i</span></span>. The <span class=term data-key=temp_username role=button tabindex=0>Temporary Username<span class=i>i</span></span> prints on the receipt and an SMS confirms the reset.",
        "In the app, log in with <span class=term data-key=username role=button tabindex=0>Username<span class=i>i</span></span> + <span class=term data-key=temp_password role=button tabindex=0>Temporary Password<span class=i>i</span></span>, set Current Password to the temporary one, then set a new <span class=term data-key=username role=button tabindex=0>Username<span class=i>i</span></span> and <span class=term data-key=password role=button tabindex=0>Password<span class=i>i</span></span>.",
        "If needed, repeat the <b>Create <span class=term data-key=secure_pin role=button tabindex=0>Secure PIN<span class=i>i</span></span></b> and <b>Activate Secure PIN</b> steps above."
      ]},
      { id:"unusual", title:"If an ‘<span class=term data-key=unusual_activity_notification role=button tabindex=0>Unusual Activity Notification<span class=i>i</span></span>’ appears", tag:"Help", items:[
        `Call <b>${hotline}</b> and say you received an <span class=term data-key=unusual_activity_notification role=button tabindex=0>Unusual Activity Notification<span class=i>i</span></span>.`,
        "After successful verification, access to the app will resume in about 12 hours with full banking transaction functionality.",
        "You can continue to browse limited app options while waiting."
      ]}
    ];

    // Glossary (clicking an i opens this panel)
    const glossary = {
      cooldown_options: { term:"Other app options (cooldown)", def:"Viewing Statement, Balance and Past Transactions available during cooldown period" },
      atm_services: { term:"ATM Services", def:"ATM menu section used during registration/reset flows (location may differ for debit vs credit)." },
      atm_pin: { term:"ATM PIN", def:"6 Digit ATM Card Pincode" },
      temp_password: { term:"Temporary Password", def:"A simple password (e.g. 12345678) as can be changed into a new one immediately after logging into the App" },
      username: { term:"Username", def:"(minimum 5 characters 1 digit 1 alphabet, no special characters e.g.!@#$%^&*()?/)" },
      password: { term:"Password", def:"(minimum 8 characters 1 digit 1 alphabet, no special characters e.g.!@#$%^&*()?/)" },
      sms_otp: { term:"SMS-OTP", def:"One-time password sent by SMS to your registered mobile number to confirm sensitive actions." },
      temp_username: { term:"Temporary Username", def:"Short-term username printed on ATM receipt during registration/reset. Also sent by SMS." },
      uob_tmrw: { term:"UOB TMRW", def:"UOB mobile banking app used to log in and manage accounts after ATM registration." },
      uob_access: { term:"UOB Access", def:"In-app verification layer for logins/transactions (Secure PIN or OTP)." },
      secure_pin: { term:"Secure PIN", def:"A 6 digit password required to perform any transfer (DuitNow) instead of using OTP" },
      card_pin: { term:"Card & PIN", def:"Verification option that uses your physical card’s 6-digit ATM PIN during Secure PIN setup." },
      email_sms_otp: { term:"Email and SMS OTP", def:"Verification option using codes sent to your email and mobile during Secure PIN setup." },
      secure_pin_activation: { term:"Secure PIN Activation", def:"Final step done via call centre to enable full use of your Secure PIN after creation." },
      reverification: { term:"Reverification", def:"Call-centre identity check required for activation or when access is limited." },
      supplementary_card: { term:"Supplementary Card", def:"Secondary credit card under a principal account, issued to another person." },
      joint_account: { term:"Joint Account", def:"Account held by more than one person; some features depend on the signing mandate." },
      credit_card: { term:"Credit Card", def:"Card billed monthly; separate from your deposit balance." },
      debit_card: { term:"Debit Card", def:"Card that draws directly from your account balance (often labelled ‘DEBIT’)." },
      secret_word: { term:"Secret Word", def:"Optional phrase for Personal Internet Banking (web) to add recognition/security when you sign in." },
      phone_keypad: { term:"Phone Keypad", def:"Phone used to register for user’s Internet Banking" },
      unusual_activity: { term:"Unusual Activity", def:"DO NOT WORRY THIS DOES NOT MEAN FRAUDULANT ACTIVITY, ONLY A SIMPLE VERIFICATION OF YOUR IDENTITY IS REQUIRED TO ACCESS MOBILE BANKING" },
      unusual_activity_notification: { term:"Unusual Activity Notification", def:"DO NOT WORRY THIS DOES NOT MEAN FRAUDULANT ACTIVITY, ONLY A SIMPLE VERIFICATION OF YOUR IDENTITY IS REQUIRED TO ACCESS MOBILE BANKING" }
    };

    /* ===== State (localStorage) ===== */
    function loadDone(){ return new Set(JSON.parse(localStorage.getItem('done-steps')||'[]')) }
    function saveDone(set){ localStorage.setItem('done-steps', JSON.stringify([...set])) }
    function pctDone(){ return Math.round((loadDone().size / steps.length) * 100) }

    /* ===== DOM refs ===== */
    const stepsRoot = document.getElementById('steps');
    const toc = document.getElementById('toc');
    const checklist = document.getElementById('checklist');
    const bar = document.getElementById('bar');
    const tabGuide = document.getElementById('tabGuide');
    const tabChecklist = document.getElementById('tabChecklist');
    const panelGuide = document.getElementById('panelGuide');
    const panelChecklist = document.getElementById('panelChecklist');
    const gPanel = document.getElementById('gPanel');
    const gTerm = document.getElementById('gTerm');
    const gBody = document.getElementById('gBody');

    /* ===== Render ===== */
    function render(){
      stepsRoot.innerHTML = '';
      toc.innerHTML = '';
      checklist.innerHTML = '';

      const done = loadDone();
      steps.forEach((s,idx)=>{
        // Content card
        const card = document.createElement('section'); card.className='step'; card.id=s.id;
        const h = document.createElement('h2'); h.innerHTML = s.title;
        const mark = document.createElement('label'); mark.className='stepdone'; mark.innerHTML = `<input type="checkbox" data-step="${s.id}"> Mark done`;
        const meta = document.createElement('div'); meta.className='meta'; meta.innerHTML = `<span class="pill">Step ${idx+1} of ${steps.length}</span> <span>${s.tag}</span>`;
        const ul = document.createElement('ol');
        s.items.forEach((it)=>{ const li=document.createElement('li'); li.innerHTML = it; ul.appendChild(li) });
        h.appendChild(mark); card.append(h, meta, ul); stepsRoot.appendChild(card);

        // TOC
        const btn = document.createElement('button'); btn.textContent = `Step ${idx+1}: ${s.title.replace(/<[^>]*>/g,'')}`;
        btn.addEventListener('click',()=>{ document.getElementById(s.id).scrollIntoView({behavior:'smooth',block:'start'}); setCurrent(idx) });
        toc.appendChild(btn);

        // Checklist entry
        const citem = document.createElement('li'); citem.className='check-item';
        citem.innerHTML = `<input type="checkbox" data-step="${s.id}"><span>Step ${idx+1}: ${s.title.replace(/<[^>]*>/g,'')}</span>`;
        checklist.appendChild(citem);
      });

      // Sync checkbox states & bind events
      document.querySelectorAll('[data-step]').forEach(cb=>{ cb.checked = done.has(cb.getAttribute('data-step')) });
      document.querySelectorAll('[data-step]').forEach(cb=>{
        cb.addEventListener('change', (e)=>{
          const id = e.currentTarget.getAttribute('data-step');
          const set = loadDone();
          if(e.currentTarget.checked) set.add(id); else set.delete(id);
          saveDone(set);
          updateProgress();
          // mirror
          document.querySelectorAll(`[data-step="${id}"]`).forEach(x=>{ if(x!==e.currentTarget) x.checked = e.currentTarget.checked });
        });
      });

      updateProgress();
      setCurrent(0);
    }

    function setCurrent(i){ Array.from(toc.children).forEach((b,idx)=> b.setAttribute('aria-current', idx===i? 'step': 'false')) }
    function updateProgress(){ const p = pctDone(); bar.style.width = p + '%'; bar.parentElement.setAttribute('aria-valuenow', p) }

    /* ===== Tabs ===== */
    function selectTab(which){ const isGuide = which==='guide'; tabGuide.setAttribute('aria-selected', isGuide); tabChecklist.setAttribute('aria-selected', !isGuide); panelGuide.hidden = !isGuide; panelChecklist.hidden = isGuide }
    tabGuide.addEventListener('click', ()=> selectTab('guide'));
    tabChecklist.addEventListener('click', ()=> selectTab('checklist'));

    /* ===== Glossary behaviour ===== */
    function openGlossary(key){ const g = glossary[key]; if(!g) return; gTerm.textContent = g.term; gBody.textContent = g.def; gPanel.dataset.open = 'true'; gPanel.setAttribute('aria-hidden','false') }
    function closeGlossary(){ gPanel.dataset.open = 'false'; gPanel.setAttribute('aria-hidden','true') }
    document.getElementById('gClose').addEventListener('click', closeGlossary);
    document.addEventListener('click',(e)=>{ const t = e.target.closest('.term'); if(t){ e.preventDefault(); e.stopPropagation(); openGlossary(t.getAttribute('data-key')); } });
    document.addEventListener('keydown',(e)=>{ if(e.key==='Escape') closeGlossary() });

    /* ===== Utilities ===== */
    function toast(msg){ const t=document.getElementById('toast'); t.textContent=msg; t.style.display='block'; setTimeout(()=>t.style.display='none', 2000) }
    document.getElementById('printBtn').addEventListener('click', ()=> window.print());
    document.getElementById('resetBtn').addEventListener('click', ()=>{ localStorage.removeItem('done-steps'); updateProgress(); toast('Checklist cleared') });
    document.getElementById('toggleDark').addEventListener('click', (e)=>{
      const d = document.documentElement; const isDark = d.dataset.theme !== 'light'; d.dataset.theme = isDark? 'light':'dark'; e.currentTarget.setAttribute('aria-pressed', (!isDark).toString());
      if(!isDark){ d.style.setProperty('--bg','#f6f7fb'); d.style.setProperty('--panel','#ffffff'); d.style.setProperty('--ink','#0b1020'); d.style.setProperty('--muted','#4a557a'); d.style.setProperty('--border','rgba(0,0,0,.1)') }
      else{ d.style.setProperty('--bg','#0b1020'); d.style.setProperty('--panel','#11162a'); d.style.setProperty('--ink','#e7ebff'); d.style.setProperty('--muted','#9aa5d1'); d.style.setProperty('--border','rgba(255,255,255,.08)') }
    });

    // Quicknav scroll handlers
    document.getElementById('qReg').addEventListener('click', ()=>{
      document.getElementById('atm-reg')?.scrollIntoView({behavior:'smooth', block:'start'});
      setCurrent(0);
    });
    document.getElementById('qReset').addEventListener('click', ()=>{
      // Per your instruction, both Password Reset and Unusual Activity go to Step 6
      document.getElementById('reset')?.scrollIntoView({behavior:'smooth', block:'start'});
      setCurrent(5);
    });
    document.getElementById('qUnusual').addEventListener('click', ()=>{
      document.getElementById('reset')?.scrollIntoView({behavior:'smooth', block:'start'});
      setCurrent(5);
    });

    // Kick-off
    render();
  </script>
</body>
</html>
