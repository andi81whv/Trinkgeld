<!DOCTYPE html>

<html lang="de">

<head>

  <meta charset="UTF-8" />

  <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover" />

  <meta name="theme-color" content="#0b0c10" />

  <meta name="description" content="TipTracker Pro – Trinkgeld schnell erfassen, auswerten und exportieren." />

  <title>TipTracker Pro</title>


  <!-- Google Fonts (distinct, non-generic) -->

  <link rel="preconnect" href="https://fonts.googleapis.com">

  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

  <link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,500,700&family=Inter:wght@400,500,600,700&display=swap" rel="stylesheet">


  <style>

    :root{

      --bg0:#07080b;

      --bg1:#0b0c10;

      --card: rgba(255,255,255,.06);

      --card2: rgba(255,255,255,.085);

      --stroke: rgba(255,255,255,.12);

      --stroke2: rgba(255,255,255,.20);


      --text: rgba(255,255,255,.92);

      --dim: rgba(255,255,255,.68);

      --muted: rgba(255,255,255,.52);


      --mint:#42ffb7;

      --lime:#c8ff61;

      --danger:#ff4d4d;

      --warn:#ffb020;


      --shadow: 0 18px 50px rgba(0,0,0,.55);

      --shadow2: 0 10px 30px rgba(0,0,0,.45);


      --r12: 14px;

      --r16: 18px;

      --r20: 22px;


      --pad: clamp(16px, 3.3vw, 24px);

      --maxw: 980px;


      --ease: cubic-bezier(.2,.8,.2,1);

    }


    *{box-sizing:border-box}

    html,body{height:100%}

    body{

      margin:0;

      font-family: Inter, system-ui, -apple-system, Segoe UI, Roboto, sans-serif;

      color: var(--text);

      background:

        radial-gradient(1200px 900px at 15% 10%, rgba(66,255,183,.18), transparent 55%),

        radial-gradient(1000px 700px at 85% 20%, rgba(200,255,97,.12), transparent 55%),

        radial-gradient(900px 650px at 55% 92%, rgba(255,77,77,.10), transparent 55%),

        linear-gradient(180deg, var(--bg0), var(--bg1));

      overflow-x:hidden;

    }


    /* Subtle grain without external images */

    body::before{

      content:"";

      position:fixed;

      inset:0;

      pointer-events:none;

      opacity:.08;

      mix-blend-mode: overlay;

      background:

        repeating-linear-gradient(0deg, rgba(255,255,255,.06) 0 1px, transparent 1px 2px),

        repeating-linear-gradient(90deg, rgba(0,0,0,.06) 0 1px, transparent 1px 3px);

      filter: blur(.3px);

    }


    /* App shell */

    .app{

      min-height:100dvh;

      display:grid;

      grid-template-rows: auto 1fr auto;

    }


    header{

      position:sticky;

      top:0;

      z-index: 20;

      backdrop-filter: blur(14px);

      -webkit-backdrop-filter: blur(14px);

      border-bottom: 1px solid rgba(255,255,255,.08);

      background: linear-gradient(180deg, rgba(12,13,18,.78), rgba(12,13,18,.35));

    }


    .topbar{

      max-width: var(--maxw);

      margin: 0 auto;

      padding: 14px var(--pad);

      display:flex;

      align-items:center;

      justify-content:space-between;

      gap: 12px;

    }


    .brand{

      display:flex;

      align-items:center;

      gap: 12px;

      min-width: 0;

    }


    .mark{

      width: 38px;

      height: 38px;

      border-radius: 12px;

      position:relative;

      background:

        radial-gradient(14px 14px at 30% 35%, rgba(255,255,255,.45), transparent 60%),

        radial-gradient(24px 18px at 70% 70%, rgba(255,255,255,.12), transparent 60%),

        linear-gradient(135deg, rgba(66,255,183,.95), rgba(200,255,97,.85));

      box-shadow:

        0 10px 25px rgba(66,255,183,.16),

        0 10px 25px rgba(200,255,97,.10),

        inset 0 0 0 1px rgba(255,255,255,.18);

    }

    .mark::after{

      content:"";

      position:absolute;

      inset: 9px 10px;

      border-radius: 10px;

      background:

        conic-gradient(from 230deg, rgba(0,0,0,.15), rgba(255,255,255,.08), rgba(0,0,0,.12));

      filter: blur(.2px);

      opacity:.75;

    }


    .brand h1{

      margin:0;

      font-family: Fraunces, serif;

      font-weight: 700;

      font-size: clamp(18px, 3.1vw, 22px);

      letter-spacing: -0.02em;

      line-height: 1.15;

      white-space: nowrap;

      overflow:hidden;

      text-overflow: ellipsis;

    }

    .brand .sub{

      display:block;

      margin-top: 2px;

      font-size: 12px;

      color: var(--muted);

      font-weight: 500;

      letter-spacing: .02em;

    }


    .actions{

      display:flex;

      gap: 10px;

      align-items:center;

      flex-wrap: wrap;

      justify-content:flex-end;

    }


    .iconbtn{

      border: 1px solid rgba(255,255,255,.12);

      background: rgba(255,255,255,.05);

      color: var(--text);

      border-radius: 12px;

      padding: 10px 12px;

      cursor:pointer;

      transition: transform .18s var(--ease), border-color .18s var(--ease), background .18s var(--ease);

      box-shadow: 0 10px 25px rgba(0,0,0,.22);

      display:flex;

      align-items:center;

      gap: 8px;

      font-weight: 600;

      font-size: 13px;

      user-select:none;

    }

    .iconbtn:hover{ transform: translateY(-1px); border-color: rgba(255,255,255,.22); background: rgba(255,255,255,.08); }

    .iconbtn:active{ transform: translateY(0px) scale(.98); }

    .iconbtn svg{ width:16px; height:16px; opacity:.9 }


    main{

      max-width: var(--maxw);

      margin: 0 auto;

      width: 100%;

      padding: 18px var(--pad) 26px;

      display:grid;

      gap: 18px;

    }


    /* Hero + input block (asymmetric, app-like) */

    .grid{

      display:grid;

      grid-template-columns: 1.1fr .9fr;

      gap: 16px;

      align-items: start;

    }

    @media (max-width: 880px){

      .grid{ grid-template-columns: 1fr; }

    }


    .panel{

      border-radius: var(--r20);

      background: linear-gradient(180deg, rgba(255,255,255,.07), rgba(255,255,255,.045));

      border: 1px solid rgba(255,255,255,.10);

      box-shadow: var(--shadow);

      overflow:hidden;

      position:relative;

    }

    .panel::before{

      content:"";

      position:absolute;

      inset:-2px;

      pointer-events:none;

      background:

        radial-gradient(500px 220px at 20% 20%, rgba(66,255,183,.12), transparent 55%),

        radial-gradient(500px 220px at 90% 40%, rgba(200,255,97,.10), transparent 55%);

      opacity:.9;

    }


    .panel-inner{

      position:relative;

      padding: 18px;

    }


    .kicker{

      display:flex;

      align-items:center;

      justify-content:space-between;

      gap: 12px;

      margin-bottom: 10px;

    }

    .kicker .title{

      font-family: Fraunces, serif;

      margin: 0;

      font-size: clamp(20px, 3.6vw, 28px);

      letter-spacing: -0.03em;

      line-height: 1.1;

    }

    .kicker .meta{

      color: var(--muted);

      font-size: 12px;

      font-weight: 600;

      letter-spacing: .08em;

      text-transform: uppercase;

      white-space: nowrap;

    }


    .hint{

      margin: 0 0 14px;

      color: var(--dim);

      line-height: 1.5;

      font-size: 14px;

      max-width: 60ch;

    }


    .inputRow{

      display:grid;

      grid-template-columns: 1fr auto;

      gap: 10px;

      align-items: center;

    }

    @media (max-width: 520px){

      .inputRow{ grid-template-columns: 1fr; }

    }


    .field{

      position:relative;

    }

    .field input{

      width:100%;

      padding: 14px 14px 14px 44px;

      border-radius: 14px;

      border: 1px solid rgba(255,255,255,.14);

      background: rgba(0,0,0,.28);

      color: var(--text);

      outline:none;

      font-size: 16px;

      font-weight: 600;

      letter-spacing: .01em;

      transition: border-color .18s var(--ease), box-shadow .18s var(--ease), transform .18s var(--ease);

    }

    .field input:focus{

      border-color: rgba(66,255,183,.55);

      box-shadow: 0 0 0 5px rgba(66,255,183,.12);

    }

    .field .prefix{

      position:absolute;

      top: 50%;

      left: 14px;

      transform: translateY(-50%);

      color: rgba(255,255,255,.62);

      font-weight: 800;

      letter-spacing: .02em;

      font-size: 14px;

      opacity:.95;

      user-select:none;

    }


    .primary{

      border: 1px solid rgba(255,255,255,.15);

      background:

        radial-gradient(18px 18px at 25% 30%, rgba(255,255,255,.45), transparent 55%),

        linear-gradient(135deg, rgba(66,255,183,.95), rgba(200,255,97,.85));

      color: #06110a;

      padding: 13px 16px;

      border-radius: 14px;

      font-weight: 900;

      letter-spacing: .02em;

      cursor:pointer;

      box-shadow:

        0 18px 35px rgba(66,255,183,.16),

        0 18px 35px rgba(200,255,97,.10),

        inset 0 0 0 1px rgba(255,255,255,.22);

      transition: transform .18s var(--ease), filter .18s var(--ease);

      min-height: 48px;

      white-space: nowrap;

    }

    .primary:hover{ transform: translateY(-1px); filter:saturate(1.06); }

    .primary:active{ transform: translateY(0px) scale(.98); }


    .quick{

      display:flex;

      gap: 10px;

      flex-wrap: wrap;

      margin-top: 12px;

    }

    .chip{

      border-radius: 999px;

      padding: 10px 12px;

      border: 1px solid rgba(255,255,255,.12);

      background: rgba(255,255,255,.05);

      color: var(--text);

      cursor:pointer;

      transition: transform .18s var(--ease), background .18s var(--ease), border-color .18s var(--ease);

      font-weight: 700;

      font-size: 13px;

      user-select:none;

    }

    .chip:hover{ transform: translateY(-1px); border-color: rgba(255,255,255,.22); background: rgba(255,255,255,.075); }

    .chip:active{ transform: translateY(0px) scale(.98); }


    /* Stats panel */

    .stats{

      display:grid;

      gap: 12px;

    }


    .statGrid{

      display:grid;

      grid-template-columns: 1fr 1fr;

      gap: 12px;

    }

    .statCard{

      border-radius: var(--r16);

      background: rgba(0,0,0,.20);

      border: 1px solid rgba(255,255,255,.10);

      box-shadow: var(--shadow2);

      padding: 14px;

      position:relative;

      overflow:hidden;

    }

    .statCard::after{

      content:"";

      position:absolute;

      inset:-1px;

      background:

        radial-gradient(250px 120px at 30% 20%, rgba(66,255,183,.10), transparent 58%),

        radial-gradient(240px 120px at 80% 60%, rgba(200,255,97,.08), transparent 62%);

      opacity:.9;

      pointer-events:none;

    }

    .statCard > *{ position:relative; }

    .statCard span{

      display:block;

      color: var(--muted);

      font-size: 12px;

      letter-spacing: .08em;

      text-transform: uppercase;

      font-weight: 700;

      margin-bottom: 10px;

    }

    .statCard strong{

      display:block;

      font-size: clamp(18px, 3.4vw, 26px);

      letter-spacing: -0.02em;

      font-weight: 900;

    }

    .statCard .accent{

      display:inline-block;

      margin-top: 10px;

      font-size: 12px;

      color: rgba(255,255,255,.72);

    }


    .statWide{ grid-column: 1 / -1; }


    /* History */

    .sectionHeader{

      display:flex;

      align-items:flex-end;

      justify-content:space-between;

      gap: 10px;

      margin-top: 4px;

    }

    .sectionHeader h2{

      margin:0;

      font-family: Fraunces, serif;

      font-size: 20px;

      letter-spacing: -0.02em;

    }

    .sectionHeader p{

      margin:0;

      color: var(--muted);

      font-size: 13px;

      font-weight: 600;

    }


    .list{

      border-radius: var(--r20);

      border: 1px solid rgba(255,255,255,.10);

      background: linear-gradient(180deg, rgba(255,255,255,.06), rgba(255,255,255,.04));

      box-shadow: var(--shadow);

      overflow:hidden;

    }


    .item{

      display:grid;

      grid-template-columns: 1fr auto;

      gap: 12px;

      align-items:center;

      padding: 14px 16px;

      border-bottom: 1px solid rgba(255,255,255,.08);

      background: rgba(0,0,0,.14);

      transition: background .18s var(--ease), transform .18s var(--ease);

    }

    .item:hover{ background: rgba(255,255,255,.04); }

    .item:last-child{ border-bottom:none; }


    .itemMain{

      display:flex;

      align-items:baseline;

      justify-content:space-between;

      gap: 12px;

      min-width:0;

    }

    .amount{

      font-weight: 900;

      letter-spacing: -0.02em;

      font-size: 16px;

    }

    .date{

      color: var(--muted);

      font-size: 12px;

      font-weight: 650;

      white-space: nowrap;

    }


    .itemActions{

      display:flex;

      align-items:center;

      gap: 10px;

    }


    .danger{

      border: 1px solid rgba(255,77,77,.35);

      background: rgba(255,77,77,.10);

      color: rgba(255,255,255,.92);

      padding: 10px 12px;

      border-radius: 12px;

      cursor:pointer;

      transition: transform .18s var(--ease), background .18s var(--ease), border-color .18s var(--ease);

      font-weight: 800;

      font-size: 13px;

    }

    .danger:hover{ transform: translateY(-1px); background: rgba(255,77,77,.14); border-color: rgba(255,77,77,.55); }

    .danger:active{ transform: translateY(0px) scale(.98); }


    .empty{

      padding: 18px 16px;

      color: var(--muted);

      font-weight: 600;

      font-size: 14px;

    }


    footer{

      padding: 14px var(--pad) 18px;

      color: rgba(255,255,255,.55);

      font-size: 12px;

      max-width: var(--maxw);

      margin: 0 auto;

      width: 100%;

      display:flex;

      justify-content:space-between;

      gap: 10px;

      flex-wrap: wrap;

    }


    .pill{

      display:inline-flex;

      align-items:center;

      gap: 8px;

      padding: 8px 10px;

      border-radius: 999px;

      border: 1px solid rgba(255,255,255,.10);

      background: rgba(255,255,255,.04);

    }


    /* Staggered reveal */

    .reveal{ opacity:0; transform: translateY(10px); }

    .reveal.in{

      opacity:1;

      transform: translateY(0);

      transition: opacity .55s var(--ease), transform .55s var(--ease);

    }


    /* Install banner */

    .install{

      position: fixed;

      left: 50%;

      transform: translateX(-50%);

      bottom: 14px;

      z-index: 50;

      width: min(720px, calc(100% - 18px));

      border-radius: 18px;

      border: 1px solid rgba(255,255,255,.14);

      background: rgba(10,11,14,.72);

      backdrop-filter: blur(14px);

      -webkit-backdrop-filter: blur(14px);

      box-shadow: var(--shadow);

      padding: 12px 12px;

      display:none;

      gap: 10px;

      align-items:center;

      justify-content:space-between;

    }

    .install .txt{

      min-width:0;

    }

    .install strong{

      display:block;

      font-size: 13px;

      letter-spacing: -0.01em;

    }

    .install span{

      display:block;

      font-size: 12px;

      color: var(--muted);

      margin-top: 2px;

    }

    .install .btns{

      display:flex;

      gap: 8px;

      flex-wrap: nowrap;

    }

    .ghost{

      border: 1px solid rgba(255,255,255,.14);

      background: rgba(255,255,255,.05);

      color: var(--text);

      padding: 10px 12px;

      border-radius: 12px;

      cursor:pointer;

      font-weight: 800;

      font-size: 13px;

      transition: transform .18s var(--ease), background .18s var(--ease);

      white-space: nowrap;

    }

    .ghost:hover{ transform: translateY(-1px); background: rgba(255,255,255,.08); }

    .ghost:active{ transform: translateY(0px) scale(.98); }


    /* Reduce motion */

    @media (prefers-reduced-motion: reduce){

      *{ transition:none !important; animation:none !important; scroll-behavior:auto !important; }

      .reveal{ opacity:1; transform:none; }

    }

  </style>


  <!-- PWA: inline manifest (no extra files) -->

  <link rel="manifest" href="data:application/manifest+json,{

    &quot;name&quot;:&quot;TipTracker Pro&quot;,

    &quot;short_name&quot;:&quot;TipTracker&quot;,

    &quot;start_url&quot;:&quot;.&quot;,

    &quot;display&quot;:&quot;standalone&quot;,

    &quot;background_color&quot;:&quot;#0b0c10&quot;,

    &quot;theme_color&quot;:&quot;#0b0c10&quot;,

    &quot;description&quot;:&quot;Trinkgeld erfassen, Statistiken ansehen, CSV exportieren.&quot;,

    &quot;icons&quot;:[

      {&quot;src&quot;:&quot;data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20512%20512'%3E%3Cdefs%3E%3ClinearGradient%20id='g'%20x1='0'%20y1='0'%20x2='1'%20y2='1'%3E%3Cstop%20offset='0'%20stop-color='%2342ffb7'/%3E%3Cstop%20offset='1'%20stop-color='%23c8ff61'/%3E%3C/linearGradient%3E%3C/defs%3E%3Crect%20width='512'%20height='512'%20rx='120'%20fill='%230b0c10'/%3E%3Crect%20x='58'%20y='58'%20width='396'%20height='396'%20rx='110'%20fill='url(%23g)'%20opacity='0.92'/%3E%3Cpath%20d='M170%20275c0-52%2042-94%2094-94h44c52%200%2094%2042%2094%2094v18c0%2052-42%2094-94%2094h-44c-52%200-94-42-94-94v-18z'%20fill='%23060f0a'%20opacity='0.85'/%3E%3Cpath%20d='M256%20136c-10%200-18-8-18-18s8-18%2018-18%2018%208%2018%2018-8%2018-18%2018z'%20fill='%23ffffff'%20opacity='0.65'/%3E%3C/svg%3E&quot;,

       &quot;sizes&quot;:&quot;512x512&quot;,

       &quot;type&quot;:&quot;image/svg+xml&quot;

      }

    ]

  }">

</head>


<body>

  <div class="app">

    <header>

      <div class="topbar">

        <div class="brand" aria-label="TipTracker Pro">

          <div class="mark" aria-hidden="true"></div>

          <div style="min-width:0">

            <h1>TipTracker Pro <span class="sub">Schnell erfassen · sauber auswerten</span></h1>

          </div>

        </div>


        <div class="actions">

          <button class="iconbtn" id="btnExport" type="button" title="CSV exportieren">

            <svg viewBox="0 0 24 24" fill="none" aria-hidden="true">

              <path d="M12 3v10m0 0 4-4m-4 4-4-4" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>

              <path d="M5 14v4a3 3 0 0 0 3 3h8a3 3 0 0 0 3-3v-4" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>

            </svg>

            Export

          </button>

          <button class="iconbtn" id="btnReset" type="button" title="Alle Daten löschen">

            <svg viewBox="0 0 24 24" fill="none" aria-hidden="true">

              <path d="M3 6h18" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>

              <path d="M8 6V4h8v2" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>

              <path d="M7 6l1 16h8l1-16" stroke="currentColor" stroke-width="2" stroke-linejoin="round"/>

              <path d="M10 11v6M14 11v6" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>

            </svg>

            Reset

          </button>

        </div>

      </div>

    </header>


    <main>

      <section class="grid">

        <article class="panel reveal" aria-label="Trinkgeld eingeben">

          <div class="panel-inner">

            <div class="kicker">

              <h2 class="title">Neuer Eintrag</h2>

              <div class="meta" id="nowLabel">—</div>

            </div>

            <p class="hint">

              Tippe den Betrag ein und speichere. Die App berechnet automatisch <strong>Heute</strong>, <strong>Monat</strong> und <strong>Jahr</strong>.

            </p>


            <div class="inputRow" role="group" aria-label="Betrag eingeben und speichern">

              <div class="field">

                <span class="prefix">€</span>

                <input id="tipInput" type="number" inputmode="decimal" step="0.01" min="0" placeholder="z. B. 7,50" autocomplete="off" />

              </div>

              <button class="primary" id="btnAdd" type="button">Eintragen</button>

            </div>


            <div class="quick" aria-label="Schnellbeträge">

              <button class="chip" data-add="2">+2</button>

              <button class="chip" data-add="5">+5</button>

              <button class="chip" data-add="10">+10</button>

              <button class="chip" data-add="20">+20</button>

              <button class="chip" data-add="50">+50</button>

            </div>

          </div>

        </article>


        <aside class="panel reveal" aria-label="Statistiken">

          <div class="panel-inner">

            <div class="kicker">

              <h2 class="title">Statistiken</h2>

              <div class="meta" id="yearLabel">2026</div>

            </div>


            <div class="statGrid">

              <div class="statCard">

                <span>Heute</span>

                <strong id="statToday">0,00&nbsp;€</strong>

                <div class="accent" id="countToday">0 Einträge</div>

              </div>

              <div class="statCard">

                <span>Dieser Monat</span>

                <strong id="statMonth">0,00&nbsp;€</strong>

                <div class="accent" id="countMonth">0 Einträge</div>

              </div>

              <div class="statCard statWide">

                <span>Gesamt (Jahr)</span>

                <strong id="statYear">0,00&nbsp;€</strong>

                <div class="accent" id="countYear">0 Einträge</div>

              </div>

            </div>

          </div>

        </aside>

      </section>


      <section class="reveal" aria-label="Historie">

        <div class="sectionHeader">

          <h2>Letzte Einträge</h2>

          <p id="historyMeta">—</p>

        </div>


        <div class="list" id="historyList" role="list"></div>

      </section>

    </main>


    <footer>

      <div class="pill" id="storagePill" title="Speicherung erfolgt lokal im Browser">

        Lokal gespeichert · <span id="storageSize">—</span>

      </div>

      <div class="pill">

        PWA-fähig · Offline nutzbar (nach Installation)

      </div>

    </footer>

  </div>


  <!-- Install prompt -->

  <div class="install" id="installBanner" role="region" aria-label="App installieren">

    <div class="txt">

      <strong>Als App installieren</strong>

      <span>Für schnellen Zugriff (Homescreen / Desktop).</span>

    </div>

    <div class="btns">

      <button class="ghost" id="btnDismissInstall" type="button">Später</button>

      <button class="primary" id="btnInstall" type="button" style="min-height:auto;padding:10px 12px;border-radius:12px;">Installieren</button>

    </div>

  </div>


  <script>

    /* ==========================

       Data + formatting helpers

    =========================== */

    const STORAGE_KEY = 'myTips';

    let tips = safeParse(localStorage.getItem(STORAGE_KEY), []);


    function safeParse(v, fallback){

      try { return JSON.parse(v) ?? fallback; } catch { return fallback; }

    }


    const fmtEUR = new Intl.NumberFormat('de-DE', { style:'currency', currency:'EUR' });

    const fmtDateTime = new Intl.DateTimeFormat('de-DE', { dateStyle:'medium', timeStyle:'short' });

    const fmtDate = new Intl.DateTimeFormat('de-DE', { dateStyle:'medium' });


    function startOfDay(d){

      const x = new Date(d);

      x.setHours(0,0,0,0);

      return x;

    }

    function startOfMonth(d){

      return new Date(d.getFullYear(), d.getMonth(), 1, 0,0,0,0);

    }

    function startOfYear(d){

      return new Date(d.getFullYear(), 0, 1, 0,0,0,0);

    }


    function sum(list){ return list.reduce((acc, t) => acc + (Number(t.amount)||0), 0); }


    function normalizeAmount(input){

      if (typeof input !== 'string') input = String(input ?? '');

      input = input.trim().replace(',', '.');

      const v = parseFloat(input);

      if (!isFinite(v) || v <= 0) return null;

      // Round to cents

      return Math.round(v * 100) / 100;

    }


    function save(){

      localStorage.setItem(STORAGE_KEY, JSON.stringify(tips));

      updateStorageSize();

    }


    /* ==========================

       Render

    =========================== */

    const el = {

      tipInput: document.getElementById('tipInput'),

      btnAdd: document.getElementById('btnAdd'),

      btnExport: document.getElementById('btnExport'),

      btnReset: document.getElementById('btnReset'),

      historyList: document.getElementById('historyList'),

      historyMeta: document.getElementById('historyMeta'),

      statToday: document.getElementById('statToday'),

      statMonth: document.getElementById('statMonth'),

      statYear: document.getElementById('statYear'),

      countToday: document.getElementById('countToday'),

      countMonth: document.getElementById('countMonth'),

      countYear: document.getElementById('countYear'),

      nowLabel: document.getElementById('nowLabel'),

      yearLabel: document.getElementById('yearLabel'),

      storageSize: document.getElementById('storageSize'),

    };


    function render(){

      // Ensure newest first

      tips.sort((a,b) => new Date(b.date) - new Date(a.date));


      const now = new Date();

      el.nowLabel.textContent = fmtDateTime.format(now);

      el.yearLabel.textContent = String(now.getFullYear());


      const day0 = startOfDay(now).getTime();

      const month0 = startOfMonth(now).getTime();

      const year0 = startOfYear(now).getTime();


      const todayList = tips.filter(t => new Date(t.date).getTime() >= day0);

      const monthList = tips.filter(t => new Date(t.date).getTime() >= month0);

      const yearList  = tips.filter(t => new Date(t.date).getTime() >= year0);


      el.statToday.textContent = fmtEUR.format(sum(todayList));

      el.statMonth.textContent = fmtEUR.format(sum(monthList));

      el.statYear.textContent  = fmtEUR.format(sum(yearList));


      el.countToday.textContent = plural(todayList.length, 'Eintrag', 'Einträge');

      el.countMonth.textContent = plural(monthList.length, 'Eintrag', 'Einträge');

      el.countYear.textContent  = plural(yearList.length, 'Eintrag', 'Einträge');


      // History meta

      el.historyMeta.textContent = tips.length

        ? `${plural(tips.length,'Eintrag','Einträge')} · zuletzt ${fmtDateTime.format(new Date(tips[0].date))}`

        : 'Noch keine Einträge';


      // History list

      el.historyList.innerHTML = '';


      if (!tips.length){

        const div = document.createElement('div');

        div.className = 'empty';

        div.textContent = 'Noch nichts erfasst. Starte mit deinem ersten Trinkgeld-Eintrag.';

        el.historyList.appendChild(div);

        return;

      }


      tips.slice(0, 50).forEach(t => {

        const row = document.createElement('div');

        row.className = 'item';

        row.setAttribute('role','listitem');


        const left = document.createElement('div');

        left.className = 'itemMain';


        const amount = document.createElement('div');

        amount.className = 'amount';

        amount.textContent = fmtEUR.format(t.amount);


        const date = document.createElement('div');

        date.className = 'date';

        date.textContent = fmtDateTime.format(new Date(t.date));


        left.appendChild(amount);

        left.appendChild(date);


        const actions = document.createElement('div');

        actions.className = 'itemActions';


        const del = document.createElement('button');

        del.className = 'danger';

        del.type = 'button';

        del.textContent = 'Löschen';

        del.addEventListener('click', () => deleteTip(t.id));


        actions.appendChild(del);


        row.appendChild(left);

        row.appendChild(actions);


        el.historyList.appendChild(row);

      });

    }


    function plural(n, s, p){ return `${n} ${n===1?s:p}`; }


    /* ==========================

       Actions

    =========================== */

    function addTip(amountOverride){

      const raw = (amountOverride != null) ? String(amountOverride) : el.tipInput.value;

      const amount = normalizeAmount(raw);

      if (amount == null){

        // Small UX feedback: shake focus ring

        el.tipInput.focus();

        el.tipInput.style.transform = 'translateX(2px)';

        setTimeout(() => el.tipInput.style.transform = 'translateX(-2px)', 70);

        setTimeout(() => el.tipInput.style.transform = 'translateX(0px)', 140);

        return;

      }


      const entry = { id: Date.now(), amount, date: new Date().toISOString() };

      tips.unshift(entry);

      save();

      render();


      el.tipInput.value = '';

      el.tipInput.blur(); // close keyboard on mobile

    }


    function deleteTip(id){

      const ok = confirm('Eintrag wirklich löschen?');

      if (!ok) return;

      tips = tips.filter(t => t.id !== id);

      save();

      render();

    }


    function resetAll(){

      const ok = confirm('Wirklich ALLE Einträge löschen? Das kann nicht rückgängig gemacht werden.');

      if (!ok) return;

      tips = [];

      save();

      render();

    }


    function exportCSV(){

      if (!tips.length){

        alert('Keine Daten zum Exportieren!');

        return;

      }

      // Excel-friendly (semicolon separated, German decimals via de-DE formatting)

      let csv = 'Datum;Uhrzeit;Betrag\n';

      for (const t of [...tips].reverse()){ // oldest -> newest

        const d = new Date(t.date);

        const dateStr = fmtDate.format(d);

        const timeStr = new Intl.DateTimeFormat('de-DE', { timeStyle:'short' }).format(d);

        const amt = (Math.round(t.amount * 100) / 100).toFixed(2).replace('.', ',');

        csv += `${dateStr};${timeStr};${amt}\n`;

      }


      const blob = new Blob([csv], { type: 'text/csv;charset=utf-8' });

      const url = URL.createObjectURL(blob);

      const a = document.createElement('a');

      const stamp = new Date().toISOString().slice(0,10);

      a.href = url;

      a.download = `TipTracker_${stamp}.csv`;

      document.body.appendChild(a);

      a.click();

      a.remove();

      URL.revokeObjectURL(url);

    }


    /* ==========================

       Wire events

    =========================== */

    el.btnAdd.addEventListener('click', () => addTip());

    el.tipInput.addEventListener('keydown', (e) => {

      if (e.key === 'Enter') addTip();

    });

    el.btnExport.addEventListener('click', exportCSV);

    el.btnReset.addEventListener('click', resetAll);


    document.querySelectorAll('.chip').forEach(btn => {

      btn.addEventListener('click', () => {

        const add = normalizeAmount(btn.dataset.add);

        const current = normalizeAmount(el.tipInput.value) ?? 0;

        const next = Math.round((current + add) * 100) / 100;

        el.tipInput.value = String(next).replace('.', ',');

        el.tipInput.focus();

      });

    });


    /* ==========================

       Reveal on scroll

    =========================== */

    const io = new IntersectionObserver((entries) => {

      entries.forEach(en => {

        if (en.isIntersecting) en.target.classList.add('in');

      });

    }, { threshold: 0.08 });

    document.querySelectorAll('.reveal').forEach(n => io.observe(n));


    /* ==========================

       Storage size indicator

    =========================== */

    function updateStorageSize(){

      const raw = localStorage.getItem(STORAGE_KEY) || '[]';

      const bytes = new Blob([raw]).size;

      el.storageSize.textContent = `${Math.max(1, Math.round(bytes/1024))} KB`;

    }


    /* ==========================

       PWA: Service Worker (inline, no extra file)

    =========================== */

    async function registerSW(){

      if (!('serviceWorker' in navigator)) return;


      const swCode = `

        const CACHE = 'tiptracker-pro-v1';

        const CORE = [self.location.href];


        self.addEventListener('install', (e) => {

          e.waitUntil((async () => {

            const cache = await caches.open(CACHE);

            await cache.addAll(CORE);

            self.skipWaiting();

          })());

        });


        self.addEventListener('activate', (e) => {

          e.waitUntil((async () => {

            const keys = await caches.keys();

            await Promise.all(keys.map(k => k === CACHE ? null : caches.delete(k)));

            self.clients.claim();

          })());

        });


        self.addEventListener('fetch', (e) => {

          const req = e.request;

          if (req.method !== 'GET') return;


          e.respondWith((async () => {

            const cache = await caches.open(CACHE);

            const cached = await cache.match(req, { ignoreSearch: true });

            if (cached) return cached;


            try{

              const fresh = await fetch(req);

              // Only cache same-origin documents and static assets

              const url = new URL(req.url);

              if (url.origin === self.location.origin){

                cache.put(req, fresh.clone());

              }

              return fresh;

            }catch(err){

              // Offline fallback: return cached app shell if navigation

              if (req.mode === 'navigate'){

                const shell = await cache.match(self.location.href);

                if (shell) return shell;

              }

              throw err;

            }

          })());

        });

      `;


      const blob = new Blob([swCode], { type: 'text/javascript' });

      const swUrl = URL.createObjectURL(blob);

      try{

        await navigator.serviceWorker.register(swUrl, { scope: './' });

      } finally{

        // keep URL alive a bit for registration; revoke later

        setTimeout(() => URL.revokeObjectURL(swUrl), 10_000);

      }

    }


    /* ==========================

       PWA install prompt UX

    =========================== */

    let deferredPrompt = null;

    const installBanner = document.getElementById('installBanner');

    const btnInstall = document.getElementById('btnInstall');

    const btnDismissInstall = document.getElementById('btnDismissInstall');


    window.addEventListener('beforeinstallprompt', (e) => {

      e.preventDefault();

      deferredPrompt = e;


      // Don't nag too often

      const dismissedAt = Number(localStorage.getItem('installDismissedAt') || 0);

      const week = 7 * 24 * 60 * 60 * 1000;

      if (Date.now() - dismissedAt < week) return;


      installBanner.style.display = 'flex';

    });


    btnDismissInstall.addEventListener('click', () => {

      localStorage.setItem('installDismissedAt', String(Date.now()));

      installBanner.style.display = 'none';

    });


    btnInstall.addEventListener('click', async () => {

      if (!deferredPrompt) return;

      deferredPrompt.prompt();

      await deferredPrompt.userChoice;

      deferredPrompt = null;

      installBanner.style.display = 'none';

    });


    window.addEventListener('appinstalled', () => {

      installBanner.style.display = 'none';

    });


    /* ==========================

       Init

    =========================== */

    updateStorageSize();

    render();

    registerSW();

  </script>

</body>

</html>
