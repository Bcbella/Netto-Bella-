# Netto-Bella-<!DOCTYPE html>

<html lang="da">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Netto Bella — Driftssystem</title>
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Sora:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;500&display=swap');
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --g0:#0d2b14;--g1:#1a5c2a;--g2:#2d7a40;--g3:#4caf6e;--g4:#a8e6bb;--g5:#e8f5eb;
  --ink:#0f1f12;--ink2:#3a5a3f;--muted:#8aaa8f;--line:#d4ead8;--bg:#f2f8f3;--white:#fff;
  --r1:#1a5c2a;--r2:#4caf50;--r3:#ff9800;--r4:#f44336;--r5:#b71c1c;
  --radius:14px;--shadow:0 2px 20px rgba(26,92,42,0.10);
}
body{font-family:'Sora',sans-serif;background:var(--bg);color:var(--ink);min-height:100vh}

/* ── LOGIN ── */
#login-screen{display:flex;align-items:center;justify-content:center;min-height:100vh;background:linear-gradient(135deg,var(–g0),var(–g1))}
.login-box{background:white;border-radius:24px;padding:40px 36px;width:360px;box-shadow:0 20px 60px rgba(0,0,0,0.3)}
.login-logo{font-size:26px;font-weight:800;color:var(–g1);margin-bottom:4px}
.login-logo span{color:var(–g3)}
.login-sub{font-size:13px;color:var(–muted);margin-bottom:28px}
.field{margin-bottom:16px}
.field label{display:block;font-size:12px;font-weight:700;text-transform:uppercase;letter-spacing:0.6px;color:var(–muted);margin-bottom:6px}
.field input{width:100%;padding:12px 14px;border:1.5px solid var(–line);border-radius:10px;font-family:‘Sora’,sans-serif;font-size:14px;color:var(–ink);outline:none;transition:border-color 0.15s}
.field input:focus{border-color:var(–g1)}
.login-btn{width:100%;padding:14px;background:var(–g1);color:white;border:none;border-radius:10px;font-family:‘Sora’,sans-serif;font-size:15px;font-weight:700;cursor:pointer;margin-top:8px;transition:background 0.15s}
.login-btn:hover{background:var(–g2)}
.login-error{font-size:13px;color:var(–r4);margin-top:10px;text-align:center;min-height:20px}

/* ── APP SHELL ── */
#app-screen{display:none;min-height:100vh;flex-direction:column}
nav{background:var(–g1);height:56px;display:flex;align-items:center;justify-content:space-between;padding:0 24px;position:sticky;top:0;z-index:100;box-shadow:0 2px 12px rgba(0,0,0,0.15)}
.nav-brand{font-size:15px;font-weight:800;color:white}
.nav-brand span{color:var(–g4)}
.nav-tabs{display:flex;gap:4px}
.nav-tab{padding:6px 13px;border-radius:6px;font-size:12px;font-weight:600;color:rgba(255,255,255,0.6);cursor:pointer;border:none;background:none;font-family:‘Sora’,sans-serif;transition:all 0.15s}
.nav-tab:hover{color:white;background:rgba(255,255,255,0.1)}
.nav-tab.active{color:white;background:rgba(255,255,255,0.18)}
.nav-right{display:flex;align-items:center;gap:12px}
.nav-user{font-size:12px;color:rgba(255,255,255,0.6);font-family:‘JetBrains Mono’,monospace}
.logout-btn{font-size:12px;color:rgba(255,255,255,0.5);cursor:pointer;border:1px solid rgba(255,255,255,0.2);background:none;padding:4px 10px;border-radius:6px;font-family:‘Sora’,sans-serif;transition:all 0.15s}
.logout-btn:hover{color:white;border-color:rgba(255,255,255,0.5)}

/* ── PAGES ── */
.page{display:none;padding:24px;max-width:960px;margin:0 auto}
.page.active{display:block}
h2{font-size:20px;font-weight:800;color:var(–g1);margin-bottom:18px;letter-spacing:-0.3px}
h3{font-size:11px;font-weight:700;text-transform:uppercase;letter-spacing:0.8px;color:var(–muted);margin-bottom:10px}

/* ── CARDS ── */
.card{background:white;border-radius:var(–radius);box-shadow:var(–shadow);border:1px solid var(–line);overflow:hidden;margin-bottom:16px}
.card-header{background:var(–g1);color:white;padding:12px 18px;font-size:13px;font-weight:700;display:flex;align-items:center;justify-content:space-between}
.card-subheader{background:var(–g5);color:var(–g1);padding:8px 18px;font-size:11px;font-weight:700;text-transform:uppercase;letter-spacing:0.6px;border-bottom:1px solid var(–line)}

/* ── CHECKLIST ── */
.check-row{display:flex;align-items:center;padding:11px 18px;border-bottom:1px solid var(–line);gap:12px;cursor:pointer;transition:background 0.1s}
.check-row:last-child{border-bottom:none}
.check-row:hover{background:var(–g5)}
.check-row.checked{background:var(–g5)}
.circle-btn{width:24px;height:24px;border-radius:50%;border:2px solid var(–g2);background:white;cursor:pointer;flex-shrink:0;display:flex;align-items:center;justify-content:center;font-size:12px;color:transparent;transition:all 0.15s}
.circle-btn.done{background:var(–g1);border-color:var(–g1);color:white}
.check-label{font-size:14px;color:var(–ink2);flex:1}
.check-row.checked .check-label{color:var(–muted);text-decoration:line-through}

/* ── RATING ── */
.rating-row{display:flex;align-items:center;padding:10px 18px;border-bottom:1px solid var(–line);gap:10px}
.rating-row:last-child{border-bottom:none}
.rating-name{font-size:12px;font-weight:600;color:var(–ink);min-width:150px}
.rating-pills{display:flex;gap:5px;flex:1}
.rpill{flex:1;padding:5px 4px;border-radius:6px;border:1.5px solid;font-size:9px;font-weight:700;text-align:center;cursor:pointer;opacity:0.3;transition:opacity 0.15s;line-height:1.3}
.rpill.sel{opacity:1}
.rp1{border-color:#1a5c2a;color:#1a5c2a;background:#e8f5eb}
.rp2{border-color:#4caf50;color:#388e3c;background:#f1f9f1}
.rp3{border-color:#ff9800;color:#e65100;background:#fff8f0}
.rp4{border-color:#f44336;color:#c62828;background:#fff0f0}
.rp5{border-color:#b71c1c;color:#7f0000;background:#fdf0f0}

/* ── STATS ── */
.stats-row{display:flex;gap:12px;margin-bottom:20px;flex-wrap:wrap}
.stat-card{flex:1;min-width:120px;background:white;border-radius:var(–radius);border:1px solid var(–line);padding:16px;text-align:center;box-shadow:var(–shadow)}
.stat-num{font-size:26px;font-weight:800;color:var(–g1);font-family:‘JetBrains Mono’,monospace}
.stat-label{font-size:10px;color:var(–muted);margin-top:3px;text-transform:uppercase;letter-spacing:0.5px}
.grid-2{display:grid;grid-template-columns:1fr 1fr;gap:16px}
@media(max-width:600px){.grid-2{grid-template-columns:1fr}}

/* ── TIME SELECTOR ── */
.time-selector{display:flex;gap:10px;margin-bottom:16px}
.time-btn{flex:1;padding:12px;border-radius:10px;border:2px solid var(–line);background:white;font-family:‘JetBrains Mono’,monospace;font-size:15px;font-weight:600;color:var(–muted);cursor:pointer;transition:all 0.15s;text-align:center}
.time-btn.active{background:var(–g1);border-color:var(–g1);color:white}

/* ── HERO ── */
.hero{background:linear-gradient(135deg,var(–g0),var(–g1));border-radius:var(–radius);padding:22px;color:white;margin-bottom:20px;position:relative;overflow:hidden}
.hero::after{content:’’;position:absolute;right:-20px;top:-20px;width:130px;height:130px;border-radius:50%;background:rgba(255,255,255,0.05)}
.hero-label{font-size:11px;font-weight:700;text-transform:uppercase;letter-spacing:1px;color:var(–g4);margin-bottom:6px}
.hero-day{font-size:26px;font-weight:800;letter-spacing:-0.5px}
.hero-date{font-size:13px;color:rgba(255,255,255,0.5);margin-bottom:14px}
.hero-pills{display:flex;gap:8px;flex-wrap:wrap}
.hero-pill{background:rgba(255,255,255,0.12);border:1px solid rgba(255,255,255,0.15);border-radius:20px;padding:5px 12px;font-size:12px;font-weight:600}

/* ── TABLE ── */
.tbl{width:100%;border-collapse:collapse;font-size:13px}
.tbl th{background:var(–g5);color:var(–g1);padding:10px 14px;text-align:left;font-weight:700;font-size:11px;text-transform:uppercase;letter-spacing:0.4px;border-bottom:2px solid var(–line)}
.tbl td{padding:10px 14px;border-bottom:1px solid var(–line);color:var(–ink2)}
.tbl tr:last-child td{border-bottom:none}
.tbl tr:hover td{background:var(–g5)}
.badge{display:inline-block;padding:3px 8px;border-radius:12px;font-size:11px;font-weight:700}
.bg{background:var(–g5);color:var(–g1)}.bo{background:#fff3e0;color:#e65100}.br{background:#fdecea;color:#c62828}

/* ── FEEDBACK ── */
.fb-header-row{display:flex;align-items:center;padding:8px 18px;background:var(–g5);border-bottom:2px solid var(–line)}
.fb-num-col{width:30px;font-size:10px;font-weight:700;text-transform:uppercase;color:var(–muted)}
.fb-dots-header{display:flex;flex:1;gap:4px}
.fb-dot-hdr{flex:1;text-align:center;font-size:8.5px;font-weight:700;line-height:1.3;padding:0 2px}
.fb-row{display:flex;align-items:center;padding:9px 18px;border-bottom:1px solid var(–line)}
.fb-row:last-child{border-bottom:none}
.fb-num{width:30px;font-family:‘JetBrains Mono’,monospace;font-size:13px;font-weight:700;color:var(–g1)}
.fb-dots{display:flex;flex:1;gap:4px}
.fb-dot{flex:1;height:26px;border-radius:6px;border:2px solid;cursor:pointer;opacity:0.25;transition:opacity 0.15s}
.fb-dot.sel{opacity:1}
.fb-legend{padding:10px 18px;background:var(–g5);display:flex;flex-wrap:wrap;gap:4px 14px;border-top:1px solid var(–line)}
.fb-legend-item{font-size:11px;color:var(–ink2)}
.fb-legend-item strong{color:var(–g1)}

/* ── TEXTAREA ── */
textarea{width:100%;border:1.5px solid var(–line);border-radius:8px;padding:10px 12px;font-family:‘Sora’,sans-serif;font-size:14px;color:var(–ink);resize:vertical;min-height:80px;outline:none;transition:border-color 0.15s;background:var(–g5)}
textarea:focus{border-color:var(–g1)}

/* ── BTN ── */
.btn{background:var(–g1);color:white;border:none;padding:13px 28px;border-radius:10px;font-family:‘Sora’,sans-serif;font-size:14px;font-weight:700;cursor:pointer;transition:background 0.15s;margin-top:12px;display:inline-flex;align-items:center;gap:8px}
.btn:hover{background:var(–g2)}
.btn:active{transform:scale(0.98)}
.btn.saving{background:var(–g3);pointer-events:none}

/* ── TOAST ── */
.toast{position:fixed;bottom:24px;left:50%;transform:translateX(-50%) translateY(80px);background:var(–g0);color:white;padding:12px 24px;border-radius:12px;font-size:14px;font-weight:600;z-index:999;transition:transform 0.3s;box-shadow:0 4px 20px rgba(0,0,0,0.3)}
.toast.show{transform:translateX(-50%) translateY(0)}

/* ── ROLE BADGE ── */
.role-leder{background:linear-gradient(135deg,#1a1a2e,var(–g1));color:white;font-size:11px;font-weight:700;padding:3px 10px;border-radius:20px}

.weekly-banner{background:linear-gradient(135deg,var(–g0),#1a3d20);border-radius:var(–radius);padding:18px 20px;color:white;display:flex;align-items:center;justify-content:space-between;margin-bottom:16px}
.weekly-uge{font-family:‘JetBrains Mono’,monospace;font-size:36px;font-weight:800;color:var(–g3)}
.weekly-info{display:flex;flex-direction:column;gap:6px}
.weekly-item{font-size:12px;font-weight:500;display:flex;align-items:center;gap:8px}
.wdot{width:8px;height:8px;border-radius:50%;flex-shrink:0}
.gap{margin-bottom:20px}
</style>

</head>
<body>

<!-- ── LOGIN ── -->

<div id="login-screen">
  <div class="login-box">
    <div class="login-logo">Netto <span>Bella</span></div>
    <div class="login-sub">Log ind for at fortsætte</div>
    <div class="field">
      <label>Email</label>
      <input type="email" id="login-email" placeholder="din@email.dk" autocomplete="email">
    </div>
    <div class="field">
      <label>Adgangskode</label>
      <input type="password" id="login-password" placeholder="••••••••" autocomplete="current-password">
    </div>
    <button class="login-btn" onclick="doLogin()">Log ind</button>
    <div class="login-error" id="login-error"></div>
  </div>
</div>

<!-- ── APP ── -->

<div id="app-screen" style="display:none;flex-direction:column">
  <nav>
    <div class="nav-brand">Netto <span>Bella</span></div>
    <div class="nav-tabs">
      <button class="nav-tab active" onclick="showPage('dashboard',this)">Dashboard</button>
      <button class="nav-tab" onclick="showPage('butiksrunde',this)">Butiksrunde</button>
      <button class="nav-tab" onclick="showPage('fokus',this)">Fokusområder</button>
      <button class="nav-tab leder-only" onclick="showPage('leder',this)" style="display:none">Leder</button>
    </div>
    <div class="nav-right">
      <span class="nav-user" id="nav-username"></span>
      <button class="logout-btn" onclick="doLogout()">Log ud</button>
    </div>
  </nav>

  <!-- DASHBOARD -->

  <div class="page active" id="page-dashboard">
    <div class="hero">
      <div class="hero-label">I dag</div>
      <div class="hero-day" id="hero-day"></div>
      <div class="hero-date" id="hero-date"></div>
      <div class="hero-pills">
        <div class="hero-pill" id="hp-runde">0/3 runder</div>
        <div class="hero-pill" id="hp-fokus">0/14 fokus</div>
      </div>
    </div>

```
<h3>Daglig status</h3>
<div class="stats-row">
  <div class="stat-card">
    <div class="stat-num" id="stat-runde">0/3</div>
    <div class="stat-label">Butiksrunder i dag</div>
  </div>
  <div class="stat-card">
    <div class="stat-num" id="stat-fokus">—</div>
    <div class="stat-label">Fokusopgaver</div>
  </div>
</div>

<h3 style="margin-top:8px">Ugentlig</h3>
<div class="weekly-banner">
  <div>
    <div style="font-size:11px;color:rgba(255,255,255,0.5);text-transform:uppercase;letter-spacing:0.6px;margin-bottom:4px">Aktuel uge</div>
    <div class="weekly-uge" id="uge-num">—</div>
  </div>
  <div class="weekly-info">
    <div class="weekly-item"><div class="wdot" style="background:var(--g3)"></div>Ugerapport — afventer</div>
    <div class="weekly-item"><div class="wdot" style="background:var(--g3)"></div>Priskontrol — afventer</div>
  </div>
</div>

<h3>Seneste aktivitet</h3>
<div class="card">
  <div class="card-body">
    <table class="tbl">
      <thead><tr><th>Skema</th><th>Bruger</th><th>Tid</th><th>Status</th></tr></thead>
      <tbody id="activity-tbody">
        <tr><td colspan="4" style="text-align:center;color:var(--muted);padding:20px">Indlæser aktivitet...</td></tr>
      </tbody>
    </table>
  </div>
</div>
```

  </div>

  <!-- BUTIKSRUNDE -->

  <div class="page" id="page-butiksrunde">
    <h2>Butiksrunde</h2>
    <div class="time-selector">
      <div class="time-btn active" onclick="selectTime(this,'06:30')">🕖 06:30</div>
      <div class="time-btn" onclick="selectTime(this,'12:00')">🕛 12:00</div>
      <div class="time-btn" onclick="selectTime(this,'17:00')">🕔 17:00</div>
    </div>
    <div id="runde-zones"></div>
    <div class="card">
      <div class="card-header">Overordnede noter</div>
      <div style="padding:14px"><textarea id="runde-noter" placeholder="Skriv noter, afvigelser eller opfølgningspunkter..."></textarea></div>
    </div>
    <button class="btn" onclick="gemRundeForm()">✓ Gem butiksrunde</button>
  </div>

  <!-- FOKUS -->

  <div class="page" id="page-fokus">
    <h2>Fokusområder</h2>
    <div class="grid-2">
      <div class="card">
        <div class="card-header">Løst af MA</div>
        <div id="fokus-ma"></div>
      </div>
      <div class="card">
        <div class="card-header">Kasselinje</div>
        <div id="fokus-kasse"></div>
      </div>
    </div>

```
<div class="card gap">
  <div class="card-header">Feedback fra morgenholdet</div>
  <div class="fb-header-row">
    <div class="fb-num-col">#</div>
    <div class="fb-dots-header" id="fb-header"></div>
  </div>
  <div id="fb-rows"></div>
  <div class="fb-legend" id="fb-legend"></div>
</div>

<div class="card">
  <div class="card-header">Overordnede noter til næste hold</div>
  <div style="padding:14px"><textarea id="fokus-noter" placeholder="Skriv noter til næste hold..."></textarea></div>
</div>
<button class="btn" onclick="gemFokusForm()">✓ Gem fokusområder</button>
```

  </div>

  <!-- LEDER -->

  <div class="page" id="page-leder">
    <h2>Leder — Ugerapport & Priskontrol <span style="font-size:13px;font-weight:400;color:var(--muted)">Udfyldes hver fredag</span></h2>

```
<div class="card">
  <div class="card-header">Afdelingsvurderinger</div>
  <div class="card-subheader">
    <span style="margin-right:16px">VK = Verdensklasse</span>
    <span style="margin-right:16px">B = Bedre end tilfredsst.</span>
    <span style="margin-right:16px">T = Tilfredsstillende</span>
    <span style="margin-right:16px">I = Ikke tilfredsst.</span>
    <span>L = Langt fra tilfredsst.</span>
  </div>
  <div id="leder-ratings"></div>
</div>

<div class="grid-2">
  <div class="card">
    <div class="card-header">Opfølgning fra forrige uge</div>
    <div style="padding:14px"><textarea id="leder-opf" placeholder="Hvad lå der fra forrige uge?"></textarea></div>
  </div>
  <div class="card">
    <div class="card-header">Afvigelser & handlinger</div>
    <div style="padding:14px"><textarea id="leder-afv" placeholder="Hvad gik galt og hvad blev gjort?"></textarea></div>
  </div>
</div>

<div class="card">
  <div class="card-header">Priskontrol — Spot Områder <span style="font-weight:400;opacity:0.7;font-size:11px;margin-left:8px">Ugentlig fredag</span></div>
  <div id="pris-rows"></div>
</div>

<button class="btn" onclick="gemLederForm()">✓ Gem ugerapport & priskontrol</button>
```

  </div>

</div>

<div class="toast" id="toast"></div>

<script>
// ── SUPABASE ───────────────────────────────────────────────
const { createClient } = supabase;
const sb = createClient(
  'https://isnrslwqvtgjrhhhrhme.supabase.co',
  'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImlzbnJzbHdxdnRnanJoaGhyaG1lIiwicm9sZSI6ImFub24iLCJpYXQiOjE3Nzc0NjU3MDYsImV4cCI6MjA5MzA0MTcwNn0.eo2HCuxondJ26fwVXvyFOMKfkrNmcvEfT0ku9-46JNE'
);

let currentUser = null;
let currentProfile = null;
let selectedTime = '06:30';
const rundeState = {};
const fokusState = { ma: {}, kasse: {} };
const lederState = {};
const fbState = {};
const prisState = {};

// ── DATA ───────────────────────────────────────────────────
const rundeZones = [
  {name:'Udenfor & Indgang', tasks:['Rent og ryddeligt ved indgang','Aktuel og offensiv','Kurve/vogne ryddet og tilgængelige','Automatiske døre fungerer']},
  {name:'Frugt & Grønt', tasks:['Rent og ryddeligt område','Opfyldt og præsentabelt','Kvalitet og friskhed','Udstilling salgsklar']},
  {name:'Køl & Frost', tasks:['Rent og ryddeligt','Opfyldt og ingen huller','Korrekte og synlige priser','Frost bokse opfyldte']},
  {name:'Kød & Convenience', tasks:['Rent og ryddeligt','Opfyldt og præsentabelt','Korrekte og synlige priser','Spot boks salgsklar']},
  {name:'Spot Områder', tasks:['Rent og ryddeligt','Spots opfyldte og salgsklar','Ingen tomme udstillinger','Korrekte priser']},
  {name:'Tørvarer & Hylder', tasks:['Rent og ryddeligt','Trimning — ingen tomme fronter','Korrekte og synlige priser','Hyldeforkanter på plads']},
  {name:'Brød & Bake-off', tasks:['Rent og ryddeligt','Opfyldt og præsentabelt','Udstilling indbydende','Korrekte og synlige priser']},
  {name:'Drikkevarer, Vin & Øl', tasks:['Rent og ryddeligt','Opfyldt — ingen huller','Køleskab opfyldt og lukket','Udstilling salgsklar']},
  {name:'Kasselinje', tasks:['Rent og ryddeligt','Impulsvarer opfyldt','Kasser fungerer','Returvarer samles']},
  {name:'Lager & Bagrum', tasks:['Rent og ryddeligt','Skrald og pap fjernet','Varer placeret korrekt','Generel orden og overblik']},
];
const fokusMA = ['Modtagelse af butikken','Dødsrunde','Lager oprydning','Opfyld Fresh-områder','Turbo trim kolo','Kvalitetsrunder','Trim ¼ område','Lukkerutiner'];
const fokusKasse = ['Samle returvarer','Ryd op i kasse 1 og 2','Rengør kasselinjeområde','Turbo trim','Køleskabsliste','Opfyld køleskab'];
const spotOmraader = ['Food Spot','Nonfood Spot','Sæson Spot','Slik Spot','Pers. Pleje Spot','Nearfood Spot','Chips Spot','Drikke Spot','Køl og Ost Spot','Brød Spot','Knækbrød Spot'];
const depts = rundeZones.map(z => z.name);
const rLabels = ['VK','B.e.T','Tilf.','Ikke','Langt'];
const rClasses = ['rp1','rp2','rp3','rp4','rp5'];
const rColors = ['#1a5c2a','#4caf50','#ff9800','#f44336','#b71c1c'];
const fbFullLabels = ['Verdensklasse','Bedre end tilfredsst.','Tilfredsstillende','Ikke tilfredsst.','Langt fra tilfredsst.'];

// ── AUTH ───────────────────────────────────────────────────
async function doLogin() {
  const email = document.getElementById('login-email').value.trim();
  const pass  = document.getElementById('login-password').value;
  document.getElementById('login-error').textContent = '';
  if (!email || !pass) { document.getElementById('login-error').textContent = 'Udfyld email og adgangskode.'; return; }
  const { data, error } = await sb.auth.signInWithPassword({ email, password: pass });
  if (error) { document.getElementById('login-error').textContent = 'Forkert email eller adgangskode.'; return; }
  await loadProfile(data.user);
}

async function loadProfile(user) {
  currentUser = user;
  const { data } = await sb.from('profiles').select('*').eq('id', user.id).single();
  currentProfile = data;
  startApp();
}

async function doLogout() {
  await sb.auth.signOut();
  document.getElementById('app-screen').style.display = 'none';
  document.getElementById('login-screen').style.display = 'flex';
  currentUser = null; currentProfile = null;
}

function startApp() {
  document.getElementById('login-screen').style.display = 'none';
  document.getElementById('app-screen').style.display = 'flex';
  const name = currentProfile?.navn || currentUser.email.split('@')[0];
  document.getElementById('nav-username').textContent = name;
  // Show leder tab if role is leder
  if (currentProfile?.rolle === 'leder') {
    document.querySelectorAll('.leder-only').forEach(el => el.style.display = '');
  }
  buildAll();
  loadDashboard();
  setDateInfo();
}

// ── DATE ───────────────────────────────────────────────────
function setDateInfo() {
  const days = ['Søndag','Mandag','Tirsdag','Onsdag','Torsdag','Fredag','Lørdag'];
  const months = ['jan','feb','mar','apr','maj','jun','jul','aug','sep','okt','nov','dec'];
  const d = new Date();
  document.getElementById('hero-day').textContent = days[d.getDay()];
  document.getElementById('hero-date').textContent = `${d.getDate()}. ${months[d.getMonth()]} ${d.getFullYear()}`;
  document.getElementById('uge-num').textContent = getWeek(d);
}
function getWeek(d) {
  const date = new Date(Date.UTC(d.getFullYear(), d.getMonth(), d.getDate()));
  const day = date.getUTCDay() || 7;
  date.setUTCDate(date.getUTCDate() + 4 - day);
  const yearStart = new Date(Date.UTC(date.getUTCFullYear(), 0, 1));
  return Math.ceil((((date - yearStart) / 86400000) + 1) / 7);
}

// ── DASHBOARD ──────────────────────────────────────────────
async function loadDashboard() {
  const today = new Date().toISOString().split('T')[0];
  // Butiksrunder today
  const { data: runder } = await sb.from('butiksrunder').select('tidspunkt,oprettet_at').gte('oprettet_at', today);
  const rundeCount = runder ? runder.length : 0;
  document.getElementById('stat-runde').textContent = `${rundeCount}/3`;
  document.getElementById('hp-runde').textContent = `${rundeCount}/3 runder`;

  // Fokus today
  const { data: fokus } = await sb.from('fokusomraader').select('oprettet_at').gte('oprettet_at', today);
  const fokusOk = fokus && fokus.length > 0 ? '✓' : '—';
  document.getElementById('stat-fokus').textContent = fokusOk;
  document.getElementById('hp-fokus').textContent = fokus && fokus.length > 0 ? 'Fokus udfyldt' : 'Fokus mangler';

  // Activity feed
  const { data: activity } = await sb.from('aktivitet').select('*').order('oprettet_at', { ascending: false }).limit(6);
  const tbody = document.getElementById('activity-tbody');
  if (activity && activity.length > 0) {
    tbody.innerHTML = activity.map(a => {
      const tid = new Date(a.oprettet_at).toLocaleTimeString('da-DK', { hour: '2-digit', minute: '2-digit' });
      const badge = a.status === 'fuldfort' ? '<span class="badge bg">Fuldført</span>' : '<span class="badge bo">Delvist</span>';
      return `<tr><td>${a.skema}</td><td>${a.bruger_navn||'—'}</td><td>${tid}</td><td>${badge}</td></tr>`;
    }).join('');
  } else {
    tbody.innerHTML = '<tr><td colspan="4" style="text-align:center;color:var(--muted);padding:20px">Ingen aktivitet registreret i dag endnu</td></tr>';
  }
}

// ── BUILD UI ───────────────────────────────────────────────
function buildAll() {
  buildRunde();
  buildFokus();
  buildFeedback();
  buildLeder();
  buildPris();
}

function buildRunde() {
  const container = document.getElementById('runde-zones');
  container.innerHTML = '';
  rundeZones.forEach((zone, zi) => {
    rundeState[zi] = {};
    const card = document.createElement('div');
    card.className = 'card';
    let rows = zone.tasks.map((t, ti) => `
      <div class="check-row" onclick="toggleCheck(this,'runde',${zi},${ti})">
        <div class="circle-btn">✓</div>
        <div class="check-label">${t}</div>
      </div>`).join('');
    card.innerHTML = `<div class="card-header">${zone.name}</div>${rows}`;
    container.appendChild(card);
  });
}

function buildFokus() {
  buildChecklist(fokusMA, 'fokus-ma', 'ma');
  buildChecklist(fokusKasse, 'fokus-kasse', 'kasse');
}

function buildChecklist(items, containerId, key) {
  const el = document.getElementById(containerId);
  el.innerHTML = items.map((t, i) => `
    <div class="check-row" onclick="toggleCheck(this,'fokus_${key}',0,${i})">
      <div class="circle-btn">✓</div>
      <div class="check-label">${t}</div>
    </div>`).join('');
}

function buildFeedback() {
  // Header
  const hdr = document.getElementById('fb-header');
  hdr.innerHTML = fbFullLabels.map((l, i) =>
    `<div class="fb-dot-hdr" style="color:${rColors[i]}">${l}</div>`
  ).join('');

  // Rows
  const rows = document.getElementById('fb-rows');
  rows.innerHTML = '';
  depts.forEach((dept, di) => {
    fbState[di] = null;
    const row = document.createElement('div');
    row.className = 'fb-row';
    row.style.background = di % 2 === 0 ? 'white' : 'var(--g5)';
    let dots = rColors.map((col, ri) =>
      `<div class="fb-dot sel-${di}" style="border-color:${col};background:${col}" data-di="${di}" data-ri="${ri}" onclick="pickFb(this)"></div>`
    ).join('');
    row.innerHTML = `<div class="fb-num">${di+1}</div><div class="fb-dots">${dots}</div>`;
    rows.appendChild(row);
  });

  // Legend
  const legend = document.getElementById('fb-legend');
  legend.innerHTML = depts.map((d, i) =>
    `<span class="fb-legend-item"><strong>${i+1}.</strong> ${d}</span>`
  ).join('');
}

function buildLeder() {
  const container = document.getElementById('leder-ratings');
  container.innerHTML = '';
  depts.forEach((dept, di) => {
    lederState[di] = null;
    const row = document.createElement('div');
    row.className = 'rating-row';
    row.style.background = di % 2 === 0 ? 'white' : 'var(--g5)';
    let pills = rLabels.map((l, ri) =>
      `<div class="rpill ${rClasses[ri]} lp-${di}" data-di="${di}" data-ri="${ri}" onclick="pickLeder(this)">${l}</div>`
    ).join('');
    row.innerHTML = `<div class="rating-name">${dept}</div><div class="rating-pills">${pills}</div>`;
    container.appendChild(row);
  });
}

function buildPris() {
  const container = document.getElementById('pris-rows');
  container.innerHTML = spotOmraader.map((spot, i) => {
    const bg = i % 2 === 0 ? '' : 'background:var(--g5)';
    return `<div style="display:flex;align-items:center;padding:10px 18px;border-bottom:1px solid var(--line);gap:16px;${bg}">
      <div style="flex:1;font-size:14px;font-weight:600;color:var(--ink)">${spot}</div>
      <div style="display:flex;gap:10px;align-items:center;font-size:13px;color:var(--muted)">
        <span>Manglende:</span>
        <input type="number" min="0" id="pris-m-${i}" style="width:52px;padding:5px 8px;border:1.5px solid var(--line);border-radius:6px;font-family:'Sora',sans-serif;text-align:center">
        <span>Forkerte:</span>
        <input type="number" min="0" id="pris-f-${i}" style="width:52px;padding:5px 8px;border:1.5px solid var(--line);border-radius:6px;font-family:'Sora',sans-serif;text-align:center">
      </div>
    </div>`;
  }).join('') + '<div style="border-bottom:none"></div>';
}

// ── INTERACTIONS ───────────────────────────────────────────
function toggleCheck(el, key, zi, ti) {
  el.classList.toggle('checked');
  const btn = el.querySelector('.circle-btn');
  btn.classList.toggle('done');
  if (key === 'runde') rundeState[zi][ti] = el.classList.contains('checked');
  else if (key === 'fokus_ma') fokusState.ma[ti] = el.classList.contains('checked');
  else if (key === 'fokus_kasse') fokusState.kasse[ti] = el.classList.contains('checked');
}

function pickFb(el) {
  const di = el.dataset.di;
  document.querySelectorAll(`.sel-${di}`).forEach(d => d.classList.remove('sel'));
  el.classList.add('sel');
  fbState[di] = parseInt(el.dataset.ri);
}

function pickLeder(el) {
  const di = el.dataset.di;
  document.querySelectorAll(`.lp-${di}`).forEach(p => p.classList.remove('sel'));
  el.classList.add('sel');
  lederState[di] = parseInt(el.dataset.ri);
}

function selectTime(btn, time) {
  document.querySelectorAll('.time-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  selectedTime = time;
}

// ── SAVE TO SUPABASE ───────────────────────────────────────
async function gemRundeForm() {
  const btn = event.target;
  btn.textContent = 'Gemmer...';
  btn.classList.add('saving');
  const { error } = await sb.from('butiksrunder').insert({
    bruger_id: currentUser.id,
    tidspunkt: selectedTime,
    data: rundeState,
    noter: document.getElementById('runde-noter').value,
  });
  btn.classList.remove('saving');
  btn.textContent = '✓ Gem butiksrunde';
  if (error) { showToast('Fejl — prøv igen'); return; }
  showToast('✓ Butiksrunde gemt!');
  loadDashboard();
}

async function gemFokusForm() {
  const btn = event.target;
  btn.textContent = 'Gemmer...'; btn.classList.add('saving');
  const { error } = await sb.from('fokusomraader').insert({
    bruger_id: currentUser.id,
    ma_opgaver: fokusState.ma,
    kasse_opgaver: fokusState.kasse,
    feedback: fbState,
    noter: document.getElementById('fokus-noter').value,
  });
  btn.classList.remove('saving'); btn.textContent = '✓ Gem fokusområder';
  if (error) { showToast('Fejl — prøv igen'); return; }
  showToast('✓ Fokusområder gemt!');
  loadDashboard();
}

async function gemLederForm() {
  const btn = event.target;
  btn.textContent = 'Gemmer...'; btn.classList.add('saving');
  const prisData = spotOmraader.map((_, i) => ({
    manglende: parseInt(document.getElementById(`pris-m-${i}`).value)||0,
    forkerte:  parseInt(document.getElementById(`pris-f-${i}`).value)||0,
  }));
  const { error } = await sb.from('ugerapporter').insert({
    bruger_id: currentUser.id,
    uge: getWeek(new Date()),
    aar: new Date().getFullYear(),
    afdelinger: lederState,
    opfoelgning: document.getElementById('leder-opf').value,
    afvigelser: document.getElementById('leder-afv').value,
    priskontrol: prisData,
  });
  btn.classList.remove('saving'); btn.textContent = '✓ Gem ugerapport & priskontrol';
  if (error) { showToast('Fejl — prøv igen'); return; }
  showToast('✓ Ugerapport gemt!');
}

// ── NAVIGATION ─────────────────────────────────────────────
function showPage(id, btn) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nav-tab').forEach(t => t.classList.remove('active'));
  document.getElementById('page-' + id).classList.add('active');
  if (btn) btn.classList.add('active');
  if (id === 'dashboard') loadDashboard();
}

// ── TOAST ───────────────────────────────────────────────────
function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 3000);
}

// ── INIT ────────────────────────────────────────────────────
sb.auth.onAuthStateChange(async (event, session) => {
  if (session?.user) {
    await loadProfile(session.user);
  }
});
</script>

</body>
</html>
