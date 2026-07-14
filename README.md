
[sw.js](https://github.com/user-attachments/files/29998333/sw.js)<img width="150" height="150" alt="icon" src="https://github.com/user-attachments/assets/d018d32a-c590-476e-9f74-6f3c06b40797" />[index.html](https://github.com/user-attachments/files/29998340/index.html)<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Counterleaf — AI Budtender</title>
<meta name="description" content="Counterleaf — an AI budtender that matches you to cannabis products and brands by how you want to feel. Trial demo.">
<meta name="color-scheme" content="light dark">
<meta name="theme-color" content="#2E5A45" media="(prefers-color-scheme: light)">
<meta name="theme-color" content="#101A13" media="(prefers-color-scheme: dark)">
<meta name="mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-title" content="Counterleaf">
<meta property="og:title" content="Counterleaf — AI Budtender">
<meta property="og:description" content="Your vibe, your match. Tell us how you want to feel — we'll handle the rest.">
<meta property="og:type" content="website">
<link rel="icon" href="icon.svg" type="image/svg+xml">
<link rel="apple-touch-icon" href="icon.svg">
<link rel="manifest" href="manifest.webmanifest">
</head>
<body>
<style>
  :root {
    --bg: #ECEDE4;
    --paper: #F5F5EC;
    --surface: #FBFBF4;
    --ink: #1B2A22;
    --muted: #5B6A5E;
    --line: #D7D9CC;
    --line-strong: #C2C6B4;
    --green: #2E5A45;
    --green-deep: #21402F;
    --green-soft: #E0E9DF;
    --sage: #7F9A6F;
    --cream: #E9E4CC;
    --amber: #B27A2A;
    --amber-soft: #F0E4CB;
    --good: #3E8663; --warn: #B27A2A; --crit: #AE4A2C;
    --shadow: 0 1px 2px rgba(20,32,24,.05), 0 8px 24px -12px rgba(20,32,24,.18);
    --shadow-lg: 0 24px 60px -28px rgba(20,32,24,.45);
    --r: 14px; --r-sm: 10px;
    --serif: "Iowan Old Style", "Palatino Linotype", "Palatino", "Georgia", serif;
    --sans: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", sans-serif;
    --mono: "SF Mono", ui-monospace, "SFMono-Regular", Menlo, Consolas, monospace;
  }
  @media (prefers-color-scheme: dark) {
    :root {
      --bg: #101A13; --paper: #16211A; --surface: #1B2820; --ink: #E9E4CC;
      --muted: #97A891; --line: #263127; --line-strong: #33422F;
      --green: #7CA98A; --green-deep: #9AC7A6; --green-soft: #1E2E22;
      --sage: #8FA97C; --cream: #E9E4CC;
      --amber: #D3A054; --amber-soft: #2E2716;
      --good: #6FB894; --warn: #D3A054; --crit: #D97A57;
      --shadow: 0 1px 2px rgba(0,0,0,.3), 0 10px 30px -14px rgba(0,0,0,.6);
      --shadow-lg: 0 30px 70px -30px rgba(0,0,0,.82);
    }
  }
  :root[data-theme="light"] {
    --bg:#ECEDE4;--paper:#F5F5EC;--surface:#FBFBF4;--ink:#1B2A22;--muted:#5B6A5E;--line:#D7D9CC;--line-strong:#C2C6B4;
    --green:#2E5A45;--green-deep:#21402F;--green-soft:#E0E9DF;--sage:#7F9A6F;--cream:#E9E4CC;--amber:#B27A2A;--amber-soft:#F0E4CB;
    --good:#3E8663;--warn:#B27A2A;--crit:#AE4A2C;
    --shadow:0 1px 2px rgba(20,32,24,.05),0 8px 24px -12px rgba(20,32,24,.18);--shadow-lg:0 24px 60px -28px rgba(20,32,24,.45);
  }
  :root[data-theme="dark"] {
    --bg:#101A13;--paper:#16211A;--surface:#1B2820;--ink:#E9E4CC;--muted:#97A891;--line:#263127;--line-strong:#33422F;
    --green:#7CA98A;--green-deep:#9AC7A6;--green-soft:#1E2E22;--sage:#8FA97C;--cream:#E9E4CC;--amber:#D3A054;--amber-soft:#2E2716;
    --good:#6FB894;--warn:#D3A054;--crit:#D97A57;
    --shadow:0 1px 2px rgba(0,0,0,.3),0 10px 30px -14px rgba(0,0,0,.6);--shadow-lg:0 30px 70px -30px rgba(0,0,0,.82);
  }

  * { box-sizing: border-box; }
  body { margin: 0; background: var(--bg); color: var(--ink); font-family: var(--sans);
    font-size: 15px; line-height: 1.55; -webkit-font-smoothing: antialiased; }
  h1,h2,h3,h4 { font-family: var(--serif); font-weight: 600; margin: 0; line-height: 1.14;
    letter-spacing: -.01em; text-wrap: balance; }
  a { color: var(--green); }
  button { font-family: inherit; cursor: pointer; }
  .mono { font-family: var(--mono); font-variant-numeric: tabular-nums; }
  .eyebrow { font-family: var(--mono); font-size: 11px; letter-spacing: .16em; text-transform: uppercase; color: var(--muted); }

  header.top { position: sticky; top: 0; z-index: 40; background: color-mix(in srgb, var(--bg) 88%, transparent);
    backdrop-filter: saturate(1.4) blur(12px); border-bottom: 1px solid var(--line); }
  .top-in { max-width: 1120px; margin: 0 auto; padding: 12px 22px; display: flex; align-items: center; gap: 16px; }
  .brand { display: flex; align-items: center; gap: 11px; }
  .mark { width: 34px; height: 34px; flex: none; }
  .brand b { font-family: var(--sans); font-size: 16px; font-weight: 600; letter-spacing: .2em; text-transform: uppercase; }
  .brand span { display: block; font-family: var(--mono); font-size: 9px; letter-spacing: .22em; text-transform: uppercase; color: var(--muted); margin-top: 2px; }
  nav.tabs { margin-left: auto; display: flex; gap: 2px; background: var(--paper); border: 1px solid var(--line); border-radius: 999px; padding: 4px; }
  nav.tabs button { border: 0; background: transparent; color: var(--muted); font-size: 13px; font-weight: 550; padding: 7px 15px; border-radius: 999px; transition: .18s; white-space: nowrap; }
  nav.tabs button:hover { color: var(--ink); }
  nav.tabs button.on { background: var(--green); color: var(--surface); box-shadow: var(--shadow); }
  .icon-btn { border: 1px solid var(--line); background: var(--paper); color: var(--ink); width: 36px; height: 36px; border-radius: 999px; display: grid; place-items: center; font-size: 15px; }
  .wrap { max-width: 1120px; margin: 0 auto; padding: 28px 22px 90px; }

  .card { background: var(--surface); border: 1px solid var(--line); border-radius: var(--r); box-shadow: var(--shadow); }
  .pill { display: inline-flex; align-items: center; gap: 5px; font-family: var(--mono); font-size: 11px; letter-spacing: .04em; padding: 3px 9px; border-radius: 999px; background: var(--green-soft); color: var(--green-deep); border: 1px solid transparent; white-space: nowrap; }
  .pill.amber { background: var(--amber-soft); color: var(--amber); }
  .pill.line { background: transparent; border-color: var(--line-strong); color: var(--muted); }
  .btn { border: 1px solid var(--green); background: var(--green); color: var(--surface); font-weight: 600; font-size: 14px; padding: 11px 20px; border-radius: 10px; transition: .16s; }
  .btn:hover { background: var(--green-deep); border-color: var(--green-deep); }
  .btn:disabled { opacity: .4; cursor: not-allowed; }
  .btn.ghost { background: transparent; color: var(--ink); border-color: var(--line-strong); }
  .btn.ghost:hover { background: var(--paper); }

  /* hero */
  .hero { display: grid; grid-template-columns: 1.15fr .85fr; gap: 34px; align-items: center; margin-bottom: 30px; }
  .hero h1 { font-size: clamp(30px, 5vw, 46px); line-height: 1.04; }
  .hero h1 em { font-style: italic; color: var(--green); }
  .hero p.lead { color: var(--muted); font-size: 16px; max-width: 46ch; margin: 16px 0 22px; }
  .hero-card { padding: 22px; position: relative; overflow: hidden; }
  .leaffield { position:absolute; inset:0; opacity:.55; }
  .hero-stat { display: flex; gap: 26px; margin-top: 4px; position: relative; }
  .hero-stat div b { font-family: var(--serif); font-size: 26px; display:block; }
  .hero-stat div span { font-family: var(--mono); font-size: 10px; letter-spacing: .1em; text-transform: uppercase; color: var(--muted); }
  @media (max-width: 820px){ .hero { grid-template-columns: 1fr; } }
  .metric-line { display:flex; align-items:center; gap: 10px; font-size: 12.5px; }
  .metric-line .ml-k { width: 88px; color: var(--muted); font-family: var(--mono); font-size: 10.5px; text-transform: uppercase; letter-spacing: .05em; }
  .metric-line .meter { flex: 1; }
  .meter { height: 6px; border-radius: 999px; background: var(--line); overflow: hidden; }
  .meter > i { display: block; height: 100%; background: var(--green); border-radius: 999px; }
  .meter.amber > i { background: var(--amber); }

  /* ---------- one-question survey ---------- */
  .qwrap { max-width: 680px; margin: 0 auto; }
  .qcard { padding: 0; overflow: hidden; }
  .qprog { height: 5px; background: var(--line); }
  .qprog > i { display: block; height: 100%; background: var(--green); border-radius: 0 999px 999px 0; transition: width .45s cubic-bezier(.4,0,.2,1); }
  .qhead { padding: 22px 32px 0; display: flex; justify-content: space-between; align-items: baseline; gap: 12px; }
  .qbody { padding: 14px 32px 6px; animation: fade .32s ease; }
  @keyframes fade { from { opacity: 0; transform: translateY(7px); } to { opacity: 1; transform: none; } }
  @media (prefers-reduced-motion: reduce){ .qbody, .msg, .rec { animation: none !important; } }
  .qbody h2 { font-size: clamp(21px, 3.4vw, 27px); }
  .qbody .qsub { color: var(--muted); margin: 8px 0 4px; max-width: 56ch; }
  .qfoot { display: flex; justify-content: space-between; align-items: center; padding: 22px 32px 28px; }
  .qcount { font-family: var(--mono); font-size: 10.5px; letter-spacing: .14em; text-transform: uppercase; color: var(--muted); }
  .qgroup { color: var(--green); }
  .skip { background: none; border: 0; color: var(--muted); font-size: 13px; cursor: pointer; text-decoration: underline; text-underline-offset: 3px; padding: 8px; }
  .qopts { display: flex; flex-direction: column; gap: 9px; margin-top: 14px; }
  .qopts.chips { flex-direction: row; flex-wrap: wrap; gap: 8px; }
  .q-single { text-align: left; border: 1px solid var(--line-strong); background: var(--paper); color: var(--ink);
    border-radius: 12px; padding: 14px 17px; display: flex; align-items: center; gap: 14px; transition: .15s; width: 100%; }
  .q-single:hover { border-color: var(--green); transform: translateX(3px); }
  .q-single.sel { border-color: var(--green); background: var(--green-soft); box-shadow: var(--shadow); }
  .qs-radio { width: 20px; height: 20px; border-radius: 999px; border: 2px solid var(--line-strong); flex: none; display: grid; place-items: center; transition: .15s; }
  .q-single.sel .qs-radio { border-color: var(--green); }
  .q-single.sel .qs-radio::after { content:''; width: 10px; height: 10px; border-radius: 999px; background: var(--green); }
  .q-single .qs-txt b { display: block; font-size: 15px; }
  .q-single .qs-txt small { color: var(--muted); font-size: 12.5px; }
  .q-single .qs-ic { font-size: 20px; width: 24px; text-align: center; flex: none; }
  .chip { border: 1px solid var(--line-strong); background: var(--paper); color: var(--ink); padding: 9px 15px; border-radius: 999px; font-size: 13.5px; font-weight: 500; transition: .14s; }
  .chip:hover { border-color: var(--green); }
  .chip.sel { background: var(--green); border-color: var(--green); color: var(--surface); }
  .chip.sel.neg { background: var(--crit); border-color: var(--crit); }
  .qtext { width: 100%; border: 1px solid var(--line-strong); background: var(--paper); color: var(--ink); border-radius: 12px; padding: 15px 18px; font-size: 18px; font-family: var(--serif); }
  .qtext:focus { outline: 2px solid var(--green); outline-offset: 1px; border-color: var(--green); }
  .steptype-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(150px,1fr)); gap: 9px; margin-top: 14px; }
  .typecard { border: 1px solid var(--line-strong); background: var(--paper); border-radius: var(--r-sm); padding: 13px; text-align: left; transition: .15s; }
  .typecard:hover { border-color: var(--green); transform: translateY(-2px); }
  .typecard.sel { border-color: var(--green); background: var(--green-soft); box-shadow: var(--shadow); }
  .typecard .ti { font-size: 21px; }
  .typecard b { display: block; font-size: 14px; margin-top: 5px; font-family: var(--serif); }
  .typecard small { color: var(--muted); font-size: 11.5px; }
  .slider-wrap { margin-top: 18px; }
  input[type=range]{ width: 100%; accent-color: var(--green); }
  .scale-labels { display: flex; justify-content: space-between; font-family: var(--mono); font-size: 10.5px; color: var(--muted); text-transform: uppercase; letter-spacing: .08em; margin-top: 4px; }
  .str-read { font-family: var(--serif); font-size: 22px; color: var(--green); text-align: center; margin-top: 8px; }

  /* results */
  .results-head { display: flex; align-items: flex-end; justify-content: space-between; gap: 18px; margin-bottom: 20px; flex-wrap: wrap; }
  .rec-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px; }
  @media (max-width: 900px){ .rec-grid { grid-template-columns: 1fr; } }
  .rec { padding: 0; overflow: hidden; display: flex; flex-direction: column; position: relative; animation: fade .4s ease backwards; }
  .rec:nth-child(2){ animation-delay:.06s; } .rec:nth-child(3){ animation-delay:.12s; }
  .rec.top { border-color: var(--green); box-shadow: var(--shadow-lg); }
  .rank-ribbon { position: absolute; top: 14px; right: 14px; font-family: var(--mono); font-size: 10px; letter-spacing: .1em; text-transform: uppercase; color: var(--muted); }
  .rec-top { padding: 18px 18px 14px; border-bottom: 1px solid var(--line); }
  .match-ring { display:flex; align-items:center; gap: 12px; margin-bottom: 12px; }
  .ring { width: 58px; height: 58px; flex: none; }
  .match-ring .mv b { font-family: var(--serif); font-size: 22px; }
  .match-ring .mv span { display:block; font-family: var(--mono); font-size: 10px; letter-spacing: .08em; text-transform: uppercase; color: var(--muted); }
  .rec h3 { font-size: 19px; }
  .brandline { font-size: 12px; color: var(--muted); margin-top: 3px; }
  .brandline b { color: var(--ink); font-weight: 600; }
  .rec .ptype { font-family: var(--mono); font-size: 11px; letter-spacing: .08em; text-transform: uppercase; color: var(--green); margin-top: 6px; }
  .rec-body { padding: 16px 18px; display: flex; flex-direction: column; gap: 13px; flex: 1; }
  .spec-row { display: grid; grid-template-columns: 1fr 1fr; gap: 8px 14px; }
  .spec .k { font-family: var(--mono); font-size: 10px; letter-spacing: .06em; text-transform: uppercase; color: var(--muted); }
  .spec .v { font-size: 13.5px; font-weight: 600; }
  .terps { display: flex; flex-wrap: wrap; gap: 5px; }
  .kmini { font-family: var(--mono); font-size: 10px; letter-spacing: .06em; text-transform: uppercase; color: var(--muted); margin-bottom: 6px; }
  .why { font-size: 13px; background: var(--paper); border-left: 3px solid var(--green); padding: 10px 12px; border-radius: 0 8px 8px 0; }
  .why b { color: var(--green); }
  .rec-foot { padding: 12px 18px 16px; border-top: 1px dashed var(--line-strong); }
  .flags { display: flex; flex-wrap: wrap; gap: 6px; }
  .alt { font-size: 12px; color: var(--muted); }
  .alt a { cursor: pointer; }
  .empty { text-align: center; padding: 60px 20px; color: var(--muted); }

  /* brands panel */
  .brands-wrap { margin-top: 22px; }
  .brand-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(220px,1fr)); gap: 12px; margin-top: 14px; }
  .brand-card { border: 1px solid var(--line); background: var(--surface); border-radius: var(--r-sm); padding: 16px; box-shadow: var(--shadow); }
  .brand-card .bc-top { display:flex; align-items:center; justify-content:space-between; gap:8px; margin-bottom: 8px; }
  .brand-card h4 { font-size: 16px; }
  .brand-card p { font-size: 12.5px; color: var(--muted); margin: 0; }
  .brand-badge { font-family: var(--mono); font-size: 9.5px; letter-spacing: .08em; text-transform: uppercase; padding: 3px 8px; border-radius: 999px; background: var(--green-soft); color: var(--green-deep); }
  .brand-badge.craft { background: var(--amber-soft); color: var(--amber); }
  .brand-badge.value { background: var(--green-soft); color: var(--green-deep); }
  .brand-badge.wellness { background: color-mix(in srgb, var(--sage) 24%, transparent); color: var(--green-deep); }

  /* compare */
  .cmp-picker { display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 18px; }
  .cmp-table-wrap { overflow-x: auto; border: 1px solid var(--line); border-radius: var(--r); }
  table.cmp { border-collapse: collapse; width: 100%; min-width: 640px; background: var(--surface); }
  table.cmp th, table.cmp td { text-align: left; padding: 12px 14px; border-bottom: 1px solid var(--line); font-size: 13.5px; vertical-align: top; }
  table.cmp thead th { position: sticky; top: 0; background: var(--paper); z-index: 1; }
  table.cmp thead th h4 { font-size: 15px; }
  table.cmp thead th small { color: var(--muted); font-weight: 400; font-family: var(--sans); }
  table.cmp tbody tr:last-child td { border-bottom: 0; }
  table.cmp .rowkey { font-family: var(--mono); font-size: 10.5px; letter-spacing: .06em; text-transform: uppercase; color: var(--muted); background: var(--paper); white-space: nowrap; }

  /* chat */
  .chat-layout { display: grid; grid-template-columns: 1fr 280px; gap: 22px; align-items: start; }
  @media (max-width: 860px){ .chat-layout { grid-template-columns: 1fr; } }
  .chat-box { display: flex; flex-direction: column; height: 66vh; min-height: 460px; overflow: hidden; }
  .chat-scroll { flex: 1; overflow-y: auto; padding: 20px; display: flex; flex-direction: column; gap: 16px; }
  .msg { max-width: 84%; animation: fade .3s ease; }
  .msg.user { align-self: flex-end; }
  .msg .bubble { padding: 12px 15px; border-radius: 14px; font-size: 14px; line-height: 1.55; }
  .msg.user .bubble { background: var(--green); color: var(--surface); border-bottom-right-radius: 4px; }
  .msg.bot .bubble { background: var(--paper); border: 1px solid var(--line); border-bottom-left-radius: 4px; }
  .msg.bot .who { font-family: var(--mono); font-size: 10px; letter-spacing: .1em; text-transform: uppercase; color: var(--green); margin-bottom: 5px; display: flex; align-items: center; gap: 6px; }
  .evidence { margin-top: 10px; border-top: 1px dashed var(--line-strong); padding-top: 9px; font-size: 12px; }
  .ev-conf { display: inline-flex; align-items: center; gap: 6px; font-family: var(--mono); font-size: 10.5px; text-transform: uppercase; letter-spacing: .06em; margin-bottom: 6px; }
  .conf-dot { width: 8px; height: 8px; border-radius: 999px; }
  .cites { display: flex; flex-direction: column; gap: 3px; }
  .cites a { font-size: 11.5px; color: var(--muted); text-decoration: none; }
  .cites a:hover { color: var(--green); text-decoration: underline; }
  .cites a::before { content: "↗ "; color: var(--green); }
  .chat-input { display: flex; gap: 9px; padding: 13px; border-top: 1px solid var(--line); background: var(--surface); }
  .chat-input input { flex: 1; border: 1px solid var(--line-strong); background: var(--paper); color: var(--ink); border-radius: 10px; padding: 11px 14px; font-size: 14px; font-family: inherit; }
  .chat-input input:focus { outline: 2px solid var(--green); outline-offset: 1px; border-color: var(--green); }
  .suggests { display: flex; flex-direction: column; gap: 7px; }
  .suggests button { text-align: left; border: 1px solid var(--line); background: var(--surface); color: var(--ink); border-radius: 10px; padding: 10px 12px; font-size: 12.5px; transition: .14s; }
  .suggests button:hover { border-color: var(--green); background: var(--paper); transform: translateX(2px); }
  .typing span { display: inline-block; width: 6px; height: 6px; border-radius: 50%; background: var(--muted); margin: 0 1px; animation: blink 1.2s infinite; }
  .typing span:nth-child(2){ animation-delay: .2s; } .typing span:nth-child(3){ animation-delay: .4s; }
  @keyframes blink { 0%,60%,100%{ opacity:.25; } 30%{ opacity:1; } }

  /* profile */
  .prof-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
  @media (max-width: 720px){ .prof-grid { grid-template-columns: 1fr; } }
  .taglist { display:flex; flex-wrap: wrap; gap:6px; margin-top: 8px; }
  .kv { display:flex; justify-content: space-between; padding: 8px 0; border-bottom: 1px dashed var(--line); font-size: 13.5px; }
  .kv:last-child { border-bottom: 0; }
  .kv b { font-family: var(--mono); font-variant-numeric: tabular-nums; }
  .fb-item { padding: 14px; border: 1px solid var(--line); border-radius: var(--r-sm); margin-bottom: 10px; background: var(--surface); }

  /* age gate */
  .gate { position: fixed; inset: 0; z-index: 100; background: color-mix(in srgb, var(--bg) 55%, #000 45%); backdrop-filter: blur(8px); display: grid; place-items: center; padding: 20px; }
  .gate-card { max-width: 420px; width: 100%; padding: 34px 30px; text-align: center; background: var(--surface); border: 1px solid var(--line); border-radius: 18px; box-shadow: var(--shadow-lg); }
  .gate-card h2 { font-size: 26px; margin-bottom: 8px; }
  .gate-card p { color: var(--muted); font-size: 13.5px; }
  .gate-actions { display: flex; gap: 10px; margin-top: 22px; }
  .gate-actions .btn { flex: 1; }

  .disclaimer { margin-top: 40px; padding: 16px 18px; border: 1px solid var(--line); border-radius: var(--r); background: var(--paper); color: var(--muted); font-size: 12px; line-height: 1.6; display:flex; gap:12px; }
  .disclaimer svg { flex: none; margin-top: 2px; }
  .hidden { display: none !important; }
  .toast { position: fixed; bottom: 22px; left: 50%; transform: translateX(-50%) translateY(20px); background: var(--ink); color: var(--bg); padding: 11px 18px; border-radius: 999px; font-size: 13px; font-weight: 500; box-shadow: var(--shadow-lg); opacity: 0; transition: .3s; z-index: 90; pointer-events: none; }
  .toast.show { opacity: 1; transform: translateX(-50%) translateY(0); }
  ::-webkit-scrollbar { width: 10px; height: 10px; }
  ::-webkit-scrollbar-thumb { background: var(--line-strong); border-radius: 999px; border: 3px solid var(--bg); }
</style>

<!-- ================= AGE GATE ================= -->
<div class="gate" id="gate">
  <div class="gate-card">
    <svg width="52" height="52" viewBox="0 0 64 64" style="margin-bottom:12px">
      <path d="M44 17 A19 19 0 1 0 44 47" fill="none" stroke="var(--green)" stroke-width="5" stroke-linecap="round"/>
      <g stroke="var(--sage)" stroke-width="3" fill="none" stroke-linecap="round" stroke-linejoin="round">
        <path d="M33 46 C33 32 42 25 52 23 C51 34 44 44 33 46 Z"/><path d="M33 47 L49 27"/>
      </g>
    </svg>
    <h2>Welcome to Counterleaf</h2>
    <p>An educational cannabis guide. You must be <b>21 or older</b> (or of legal age in your region) to enter.</p>
    <div class="gate-actions">
      <button class="btn ghost" onclick="location.href='https://www.samhsa.gov/find-help/national-helpline'">I'm under 21</button>
      <button class="btn" onclick="enterApp()">I'm 21 or older</button>
    </div>
    <p style="margin-top:16px;font-size:11.5px">Counterleaf provides general education, not medical advice.</p>
  </div>
</div>

<!-- ================= HEADER ================= -->
<header class="top">
  <div class="top-in">
    <div class="brand">
      <svg class="mark" viewBox="0 0 64 64">
        <path d="M44 17 A19 19 0 1 0 44 47" fill="none" stroke="var(--ink)" stroke-width="5" stroke-linecap="round"/>
        <g stroke="var(--sage)" stroke-width="3.4" fill="none" stroke-linecap="round" stroke-linejoin="round">
          <path d="M33 46 C33 32 42 25 52 23 C51 34 44 44 33 46 Z"/><path d="M33 47 L49 27"/>
        </g>
      </svg>
      <div><b>Counterleaf</b><span>AI Budtender</span></div>
    </div>
    <nav class="tabs">
      <button data-tab="find" class="on">Find</button>
      <button data-tab="compare">Compare</button>
      <button data-tab="ask">Ask</button>
      <button data-tab="profile">Profile</button>
    </nav>
    <button class="icon-btn" id="themeBtn" title="Toggle theme">◑</button>
  </div>
</header>

<div class="wrap">
  <!-- ================= FIND ================= -->
  <section data-view="find">
    <div id="heroView">
      <div class="hero">
        <div>
          <div class="eyebrow" style="margin-bottom:14px">Personalized · Unbiased · Educational</div>
          <h1>Your vibe, your <em>match</em>.</h1>
          <p class="lead" style="color:var(--ink);font-size:18px;font-family:var(--serif);font-style:italic;max-width:40ch;margin:16px 0 10px">Tell us how you want to feel — I'll handle the rest.</p>
          <p class="lead" style="margin-top:0">Counterleaf returns products and brands scored on how well they match — with a plain-English reason for every one, and nothing pushed because it's expensive.</p>
          <button class="btn" onclick="startSurvey()">Start the conversation →</button>
          <div class="hero-stat">
            <div><b id="catCount">—</b><span>Products</span></div>
            <div><b id="brandCount">—</b><span>Brands</span></div>
            <div><b>Low&nbsp;&amp;&nbsp;slow</b><span>Beginner-first</span></div>
          </div>
        </div>
        <div class="card hero-card">
          <canvas class="leaffield" id="leafCanvas"></canvas>
          <div class="eyebrow" style="position:relative">How matching works</div>
          <div style="position:relative;margin-top:14px;display:flex;flex-direction:column;gap:12px">
            <div class="metric-line"><span class="ml-k">Effects</span><div class="meter"><i style="width:92%"></i></div></div>
            <div class="metric-line"><span class="ml-k">Your goals</span><div class="meter"><i style="width:80%"></i></div></div>
            <div class="metric-line"><span class="ml-k">Tolerance</span><div class="meter"><i style="width:85%"></i></div></div>
            <div class="metric-line"><span class="ml-k">Avoid-list</span><div class="meter amber"><i style="width:64%"></i></div></div>
            <div class="metric-line"><span class="ml-k">Brand fit</span><div class="meter"><i style="width:72%"></i></div></div>
          </div>
          <p style="position:relative;color:var(--muted);font-size:12px;margin:16px 0 0">Every factor is weighted, then combined into one match score. Nothing is hidden — you always see why.</p>
        </div>
      </div>
    </div>

    <div id="surveyView" class="hidden">
      <div class="qwrap"><div class="card qcard" id="qcard"></div></div>
    </div>

    <div id="resultsView" class="hidden">
      <div class="results-head">
        <div>
          <div class="eyebrow">Your matches</div>
          <h2 style="font-size:28px;margin-top:6px" id="resultTitle">Top 3 recommendations</h2>
          <p style="color:var(--muted);margin:6px 0 0" id="resultSummary"></p>
        </div>
        <div style="display:flex;gap:10px">
          <button class="btn ghost" onclick="startSurvey()">Edit answers</button>
          <button class="btn ghost" onclick="resetAll()">Start over</button>
        </div>
      </div>
      <div class="rec-grid" id="recGrid"></div>
      <div id="matchExplain"></div>
      <div class="brands-wrap" id="brandsPanel"></div>
    </div>
  </section>

  <!-- ================= COMPARE ================= -->
  <section data-view="compare" class="hidden">
    <div class="eyebrow">Side by side</div>
    <h2 style="font-size:28px;margin:6px 0 4px">Compare products</h2>
    <p style="color:var(--muted);margin:0 0 18px">Pick 2–4 products to weigh brand, THC, terpenes, price, effects and beginner-friendliness against each other.</p>
    <div class="cmp-picker" id="cmpPicker"></div>
    <div id="cmpOut"></div>
  </section>

  <!-- ================= ASK ================= -->
  <section data-view="ask" class="hidden">
    <div class="eyebrow">AI Budtender</div>
    <h2 style="font-size:28px;margin:6px 0 4px">Ask anything</h2>
    <p style="color:var(--muted);margin:0 0 18px">Evidence-based answers with confidence ratings and citations. When the science is thin, Counterleaf says so.</p>
    <div class="chat-layout">
      <div class="card chat-box">
        <div class="chat-scroll" id="chatScroll"></div>
        <div class="chat-input">
          <input id="chatInput" placeholder="e.g. What terpene helps with focus?" autocomplete="off">
          <button class="btn" onclick="sendChat()">Ask</button>
        </div>
      </div>
      <div>
        <div class="eyebrow" style="margin-bottom:10px">Popular questions</div>
        <div class="suggests" id="suggests"></div>
      </div>
    </div>
  </section>

  <!-- ================= PROFILE ================= -->
  <section data-view="profile" class="hidden">
    <div class="eyebrow">Personalization</div>
    <h2 style="font-size:28px;margin:6px 0 4px">My profile</h2>
    <p style="color:var(--muted);margin:0 0 18px">Counterleaf remembers your preferences on this device to sharpen future matches. Nothing leaves your browser.</p>
    <div class="prof-grid" id="profGrid"></div>
    <div style="margin-top:18px"><button class="btn ghost" onclick="clearProfile()">Reset saved profile</button></div>
  </section>

  <div class="disclaimer">
    <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="M12 9v4M12 17h.01M10.3 3.9 1.8 18a2 2 0 0 0 1.7 3h17a2 2 0 0 0 1.7-3L13.7 3.9a2 2 0 0 0-3.4 0Z"/></svg>
    <div><b style="color:var(--ink)">Educational use only.</b> Counterleaf does not make medical claims, diagnose, or treat any condition. THC affects everyone differently — start low and go slow. Cannabis is illegal in some jurisdictions and restricted to adults 21+ in most legal markets. Product and brand data shown is illustrative for demonstration. If you're pregnant, nursing, taking medication, or have a health condition, consult a licensed clinician. In crisis? Call or text <b style="color:var(--ink)">988</b> (US).</div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
/* ========================= DATA ========================= */
const EFFECTS = ["relax","sleep","stress relief","anxiety relief","happiness","creativity","focus","energy","socializing","pain management","appetite","body high","head high","balanced","euphoric"];
const FLAVORS = ["citrus","sweet","berry","earthy","pine","diesel","candy","fruity","gassy","herbal"];
const AVOIDS  = ["anxiety","couch lock","dry mouth","dry eyes","high thc","strong smell","sleepiness"];
const TIMES   = ["morning","afternoon","evening","night","anytime"];
const STRENGTHS = ["Very Mild","Mild","Medium","Strong","Extremely Strong"];

const TYPES = [
  {id:"flower",name:"Flower",icon:"🌿",sub:"Classic bud"},
  {id:"preroll",name:"Pre-rolls",icon:"🚬",sub:"Ready to spark"},
  {id:"vape",name:"Vape Carts",icon:"💨",sub:"510 & disposables"},
  {id:"concentrate",name:"Concentrates",icon:"💎",sub:"Wax, resin, rosin"},
  {id:"edible",name:"Edibles",icon:"🍬",sub:"Gummies & more"},
  {id:"drink",name:"Drinks",icon:"🥤",sub:"Fast-acting sips"},
  {id:"tincture",name:"Tinctures",icon:"💧",sub:"Sublingual drops"},
  {id:"capsule",name:"Capsules",icon:"💊",sub:"Precise doses"},
  {id:"topical",name:"Topicals",icon:"🧴",sub:"Balms & creams"},
];

const BRAND_INFO = {
  "Foothold Farms": {style:"craft", blurb:"Small-batch indoor flower with a terpene-first philosophy."},
  "Common Ground":  {style:"value", blurb:"Dependable everyday flower and pre-rolls at a fair price."},
  "Halcyon":        {style:"wellness", blurb:"CBD-forward, low-intoxication products for calm and relief."},
  "Cinder":         {style:"classic", blurb:"Bright, energetic sativas built for daytime and creativity."},
  "Nightshade":     {style:"classic", blurb:"Indica specialists focused on rest and deep relaxation."},
  "Marrow Extracts":{style:"craft", blurb:"Solventless rosin and badder, prized for purity and flavor."},
  "Emberline Extracts":{style:"craft", blurb:"Full-spectrum live resin carts and diamonds."},
  "Volt":           {style:"value", blurb:"High-potency distillate and wax at budget-friendly prices."},
  "Baker's Dozen":  {style:"classic", blurb:"Classic, reliable edibles in familiar, well-labeled doses."},
  "Micro":          {style:"wellness", blurb:"Precise micro-doses for a gentle, controllable buzz."},
  "Lift":           {style:"classic", blurb:"Fast-acting cannabis drinks made for social moments."},
  "Even":           {style:"wellness", blurb:"Consistent capsules and tinctures for measured dosing."},
  "Salve & Co":     {style:"wellness", blurb:"Non-intoxicating topicals for targeted, localized relief."},
};

const CATALOG = [
  {id:"f1",brand:"Foothold Farms",name:"Blue Dream",type:"flower",thc:18,cbd:0.5,terps:["Myrcene","Pinene","Caryophyllene"],flavors:["berry","sweet","herbal"],effects:["happiness","creativity","stress relief","balanced","head high"],strength:3,beginner:4,price:38,time:["afternoon","anytime"],avoids:[],note:"A gentle sativa-leaning hybrid; famously balanced and approachable."},
  {id:"f2",brand:"Nightshade",name:"Granddaddy Purple",type:"flower",thc:20,cbd:0.3,terps:["Myrcene","Linalool","Caryophyllene"],flavors:["berry","sweet","earthy"],effects:["relax","sleep","pain management","body high"],strength:4,beginner:3,price:42,time:["evening","night"],avoids:["couch lock","sleepiness"],note:"Heavy indica for winding down; strong body sedation."},
  {id:"f3",brand:"Halcyon",name:"Harlequin CBD",type:"flower",thc:7,cbd:10,terps:["Myrcene","Pinene"],flavors:["earthy","citrus","herbal"],effects:["relax","anxiety relief","stress relief","pain management","balanced"],strength:2,beginner:5,price:36,time:["morning","afternoon","anytime"],avoids:[],note:"High-CBD, low-THC — clear-headed relief with minimal intoxication."},
  {id:"f4",brand:"Cinder",name:"Sour Diesel",type:"flower",thc:22,cbd:0.2,terps:["Caryophyllene","Limonene","Myrcene"],flavors:["diesel","citrus","gassy"],effects:["energy","focus","creativity","euphoric","head high"],strength:4,beginner:2,price:44,time:["morning","afternoon"],avoids:["anxiety","strong smell","dry mouth"],note:"Pungent, fast-hitting daytime sativa; can be racy for the sensitive."},
  {id:"f5",brand:"Common Ground",name:"Northern Lights",type:"flower",thc:16,cbd:0.4,terps:["Myrcene","Caryophyllene","Pinene"],flavors:["earthy","pine","sweet"],effects:["relax","sleep","happiness","body high"],strength:3,beginner:4,price:40,time:["evening","night"],avoids:["sleepiness"],note:"A classic mellow indica, forgiving for newer users seeking calm."},

  {id:"p1",brand:"Foothold Farms",name:"Wedding Cake Pre-Roll",type:"preroll",thc:21,cbd:0.3,terps:["Limonene","Caryophyllene","Myrcene"],flavors:["sweet","earthy","fruity"],effects:["relax","happiness","stress relief","euphoric","body high"],strength:4,beginner:3,price:14,time:["evening","anytime"],avoids:["dry mouth"],note:"Single-gram hybrid roll; relaxing without full couch lock."},
  {id:"p2",brand:"Cinder",name:"Jack Herer Infused Roll",type:"preroll",thc:28,cbd:0.2,terps:["Terpinolene","Pinene","Caryophyllene"],flavors:["pine","citrus","herbal"],effects:["energy","focus","creativity","euphoric","head high"],strength:5,beginner:1,price:18,time:["morning","afternoon"],avoids:["anxiety","high thc"],note:"Kief-infused and potent — for experienced daytime users."},
  {id:"p3",brand:"Halcyon",name:"CBD Calm 5-Pack",type:"preroll",thc:6,cbd:12,terps:["Myrcene","Linalool"],flavors:["herbal","earthy"],effects:["relax","anxiety relief","stress relief","balanced"],strength:2,beginner:5,price:22,time:["anytime"],avoids:[],note:"High-CBD minis for microdosing calm; very gentle."},

  {id:"v1",brand:"Emberline Extracts",name:"Live Resin Cart — Gelato",type:"vape",thc:78,cbd:0.5,terps:["Caryophyllene","Limonene","Linalool"],flavors:["sweet","fruity","berry"],effects:["relax","happiness","stress relief","euphoric","balanced"],strength:4,beginner:3,price:45,subtype:"510 · Live Resin",time:["evening","anytime"],avoids:["dry mouth"],note:"Full-spectrum live resin — rich terpenes, smoother and more balanced than distillate."},
  {id:"v2",brand:"Volt",name:"Distillate Cart — Blue Razz",type:"vape",thc:88,cbd:0,terps:["Added terpenes"],flavors:["candy","berry","sweet"],effects:["euphoric","happiness","head high"],strength:5,beginner:2,price:30,subtype:"510 · Distillate",time:["anytime"],avoids:["high thc","dry mouth"],note:"Very high THC, flavor from added terpenes; potent and inexpensive."},
  {id:"v3",brand:"Nightshade",name:"Disposable — Sleepytime Indica",type:"vape",thc:74,cbd:2,terps:["Myrcene","Linalool","Caryophyllene"],flavors:["earthy","berry","herbal"],effects:["relax","sleep","body high","pain management"],strength:4,beginner:3,price:35,subtype:"Disposable · Live Resin",time:["night","evening"],avoids:["sleepiness","couch lock"],note:"All-in-one disposable tuned for nighttime rest."},
  {id:"v4",brand:"Marrow Extracts",name:"Rosin Cart — Papaya",type:"vape",thc:72,cbd:1,terps:["Myrcene","Caryophyllene","Limonene"],flavors:["fruity","sweet","earthy"],effects:["relax","happiness","stress relief","balanced","body high"],strength:4,beginner:3,price:55,subtype:"510 · Solventless Rosin",time:["evening","anytime"],avoids:[],note:"Solventless rosin — no solvents used, prized for purity and flavor."},
  {id:"v5",brand:"Even",name:"Balanced Cart — 1:1 CBD:THC",type:"vape",thc:38,cbd:38,terps:["Myrcene","Pinene","Limonene"],flavors:["herbal","citrus"],effects:["relax","anxiety relief","stress relief","pain management","balanced"],strength:2,beginner:5,price:42,subtype:"510 · 1:1",time:["anytime"],avoids:[],note:"Even CBD:THC ratio takes the edge off THC — a great starter cart."},

  {id:"c1",brand:"Marrow Extracts",name:"Live Rosin Badder — Sherb",type:"concentrate",thc:76,cbd:1,terps:["Caryophyllene","Limonene","Myrcene"],flavors:["sweet","gassy","fruity"],effects:["relax","euphoric","happiness","body high"],strength:5,beginner:1,price:60,subtype:"Live Rosin Badder",time:["evening"],avoids:["high thc"],note:"Solventless badder — full-flavored and very potent; dab-experienced only."},
  {id:"c2",brand:"Emberline Extracts",name:"Live Resin Diamonds",type:"concentrate",thc:90,cbd:0,terps:["Limonene","Caryophyllene"],flavors:["gassy","citrus","diesel"],effects:["euphoric","head high","energy"],strength:5,beginner:1,price:50,subtype:"Diamonds + Sauce",time:["afternoon","evening"],avoids:["high thc","anxiety"],note:"THCA diamonds — among the strongest concentrates available."},
  {id:"c3",brand:"Volt",name:"Cured Wax — GSC",type:"concentrate",thc:72,cbd:1,terps:["Caryophyllene","Humulene","Limonene"],flavors:["earthy","sweet"],effects:["relax","happiness","body high","euphoric"],strength:5,beginner:2,price:32,subtype:"Wax / Budder",time:["evening"],avoids:["high thc"],note:"Budget cured wax; potent, best for seasoned dabbers."},

  {id:"e1",brand:"Micro",name:"Micro Gummies — 2.5mg",type:"edible",thc:2.5,cbd:0,dose:2.5,terps:[],flavors:["fruity","berry","sweet"],effects:["relax","happiness","stress relief"],strength:1,beginner:5,price:18,subtype:"2.5mg / piece",time:["anytime","evening"],avoids:[],note:"True microdose — ideal first edible. Wait 2 hours before more."},
  {id:"e2",brand:"Micro",name:"Balanced Gummies — 5mg 1:1",type:"edible",thc:5,cbd:5,dose:5,terps:[],flavors:["citrus","sweet"],effects:["relax","anxiety relief","stress relief","balanced"],strength:2,beginner:5,price:22,subtype:"5mg THC : 5mg CBD",time:["anytime"],avoids:[],note:"CBD softens the THC; gentle and forgiving."},
  {id:"e3",brand:"Baker's Dozen",name:"Classic Gummies — 10mg",type:"edible",thc:10,cbd:0,dose:10,terps:[],flavors:["fruity","candy","berry"],effects:["euphoric","happiness","body high","relax"],strength:3,beginner:3,price:25,subtype:"10mg / piece",time:["evening","night"],avoids:[],note:"Standard single dose; more than many beginners need — consider halving."},
  {id:"e4",brand:"Nightshade",name:"Sleep Gummies — 10mg + CBN",type:"edible",thc:10,cbd:2,dose:10,terps:[],flavors:["berry","herbal"],effects:["sleep","relax","body high"],strength:3,beginner:3,price:28,subtype:"10mg THC + 5mg CBN",time:["night"],avoids:["sleepiness"],note:"CBN blend aimed at sleep; anecdotally sedating, evidence still emerging."},
  {id:"e5",brand:"Baker's Dozen",name:"High-Dose Chocolate — 25mg",type:"edible",thc:25,cbd:0,dose:25,terps:[],flavors:["sweet"],effects:["euphoric","body high","sleep","pain management"],strength:5,beginner:1,price:24,subtype:"100mg bar · 25mg squares",time:["night"],avoids:["high thc","couch lock"],note:"For high-tolerance users only; 25mg overwhelms most beginners."},

  {id:"d1",brand:"Lift",name:"Sparkling Sipper — 5mg",type:"drink",thc:5,cbd:0,dose:5,terps:[],flavors:["citrus","fruity"],effects:["socializing","happiness","relax","euphoric"],strength:2,beginner:5,price:8,subtype:"Fast-acting · 5mg",time:["afternoon","evening","anytime"],avoids:[],note:"Nano-emulsified for quicker, shorter onset — social-friendly."},
  {id:"d2",brand:"Micro",name:"Microdose Seltzer — 2mg",type:"drink",thc:2,cbd:2,dose:2,terps:[],flavors:["berry","citrus"],effects:["relax","socializing","stress relief","balanced"],strength:1,beginner:5,price:6,subtype:"2mg THC : 2mg CBD",time:["anytime"],avoids:[],note:"Barely-there buzz; a mellow alcohol alternative."},

  {id:"t1",brand:"Even",name:"1:1 Balance Tincture",type:"tincture",thc:10,cbd:10,dose:10,terps:[],flavors:["herbal","earthy"],effects:["relax","anxiety relief","pain management","balanced"],strength:2,beginner:4,price:40,subtype:"per 1mL dropper · adjustable",time:["anytime"],avoids:[],note:"Precise, adjustable dosing; sublingual onset ~15–45 min."},
  {id:"t2",brand:"Halcyon",name:"CBD-Forward Tincture 20:1",type:"tincture",thc:1,cbd:20,dose:20,terps:[],flavors:["herbal"],effects:["relax","anxiety relief","stress relief"],strength:1,beginner:5,price:45,subtype:"20mg CBD : 1mg THC",time:["anytime","morning"],avoids:[],note:"Minimal intoxication; calm without a noticeable high."},

  {id:"cap1",brand:"Even",name:"Even 5mg Softgels",type:"capsule",thc:5,cbd:0,dose:5,terps:[],flavors:[],effects:["relax","stress relief","pain management"],strength:2,beginner:5,price:30,subtype:"5mg / capsule",time:["anytime"],avoids:[],note:"No flavor, no smoke; consistent, discreet dosing."},
  {id:"cap2",brand:"Nightshade",name:"Nightcap 10mg + CBN Caps",type:"capsule",thc:10,cbd:0,dose:10,terps:[],flavors:[],effects:["sleep","relax","body high"],strength:3,beginner:3,price:34,subtype:"10mg THC + CBN",time:["night"],avoids:["sleepiness"],note:"Sleep-targeted capsule; take an hour before bed."},

  {id:"top1",brand:"Salve & Co",name:"1:1 Relief Balm",type:"topical",thc:0,cbd:0,dose:0,terps:["Caryophyllene","Linalool"],flavors:["herbal","pine"],effects:["pain management","relax"],strength:1,beginner:5,price:35,subtype:"Non-intoxicating · localized",time:["anytime"],avoids:[],note:"Applied to skin — localized relief, does not cause a high."},
  {id:"top2",brand:"Salve & Co",name:"Cooling Muscle Roll-On",type:"topical",thc:2,cbd:20,dose:0,terps:["Menthol","Caryophyllene"],flavors:["herbal"],effects:["pain management","relax","body high"],strength:1,beginner:5,price:28,subtype:"CBD-forward · localized",time:["anytime"],avoids:[],note:"Menthol + CBD for sore muscles; no intoxication."},
];
document.getElementById('catCount').textContent = CATALOG.length;
document.getElementById('brandCount').textContent = Object.keys(BRAND_INFO).length;

/* ========================= STATE ========================= */
const LS = "counterleaf_v1";
const defaultProfile = { name:"", flavors:{}, terps:{}, types:{}, effects:{}, brands:{}, brandPref:null, disliked:[], tolerance:[], budget:null, feedback:[], surveys:0 };
let profile = load();
function load(){ try { return Object.assign({}, defaultProfile, JSON.parse(localStorage.getItem(LS)||"{}")); } catch(e){ return {...defaultProfile}; } }
function save(){ try { localStorage.setItem(LS, JSON.stringify(profile)); } catch(e){} }

function freshSurvey(){ return { name:profile.name||"", experience:null, frequency:null, goals:[], effects:[], avoid:[], times:[], setting:null, type:null, prodq:{}, strength:3, tolerance:null, doseTol:null, flavors:[], brandPref:profile.brandPref||null, budget:null }; }
let survey = freshSurvey();

/* ========================= GATE + THEME + TABS ========================= */
function enterApp(){ document.getElementById('gate').classList.add('hidden'); localStorage.setItem('counterleaf_age','1'); }
if(localStorage.getItem('counterleaf_age')==='1') document.getElementById('gate').classList.add('hidden');
const themeBtn = document.getElementById('themeBtn');
themeBtn.onclick = ()=>{
  const cur = document.documentElement.getAttribute('data-theme');
  const next = cur==='dark'?'light':cur==='light'?'dark':(matchMedia('(prefers-color-scheme: dark)').matches?'light':'dark');
  document.documentElement.setAttribute('data-theme', next); localStorage.setItem('counterleaf_theme', next);
};
if(localStorage.getItem('counterleaf_theme')) document.documentElement.setAttribute('data-theme', localStorage.getItem('counterleaf_theme'));

document.querySelectorAll('nav.tabs button').forEach(b=> b.onclick=()=>switchTab(b.dataset.tab));
function switchTab(t){
  document.querySelectorAll('nav.tabs button').forEach(b=> b.classList.toggle('on', b.dataset.tab===t));
  document.querySelectorAll('section[data-view]').forEach(s=> s.classList.toggle('hidden', s.dataset.view!==t));
  if(t==='compare') renderComparePicker();
  if(t==='profile') renderProfile();
  window.scrollTo({top:0,behavior:'smooth'});
}
let toastT; function toast(m){ const el=document.getElementById('toast'); el.textContent=m; el.classList.add('show'); clearTimeout(toastT); toastT=setTimeout(()=>el.classList.remove('show'),2200); }
function nice(s){ return (s||'').toString().replace(/\b\w/g,c=>c.toUpperCase()).replace(/Thc/g,'THC').replace(/Cbd/g,'CBD').replace(/Cbn/g,'CBN'); }

/* ========================= SURVEY OPTIONS ========================= */
const EXPERIENCE = [
  {v:"first",label:"First time",sub:"Never tried it",ic:"🌱"},
  {v:"beginner",label:"Beginner",sub:"A few times",ic:"🌿"},
  {v:"occasional",label:"Occasional",sub:"Now and then",ic:"🍃"},
  {v:"regular",label:"Regular",sub:"Weekly-ish",ic:"🪴"},
  {v:"heavy",label:"Heavy user",sub:"High tolerance",ic:"🌳"},
];
const FREQUENCY = [
  {v:"never",label:"Not currently",sub:"Just starting or coming back"},
  {v:"rare",label:"Once in a while",sub:"Special occasions"},
  {v:"monthly",label:"A few times a month"},
  {v:"weekly",label:"About weekly"},
  {v:"daily",label:"Most days",sub:"Seasoned & steady"},
];
const GOALS = [
  {v:"unwind",label:"Wind down & relax",eff:["relax","stress relief"]},
  {v:"sleep",label:"Sleep better",eff:["sleep","relax"]},
  {v:"calm",label:"Ease stress or anxiety",eff:["anxiety relief","stress relief"]},
  {v:"pain",label:"Manage pain",eff:["pain management"]},
  {v:"create",label:"Get creative or focused",eff:["creativity","focus"]},
  {v:"energy",label:"Boost energy",eff:["energy"]},
  {v:"social",label:"Be more social",eff:["socializing","happiness"]},
  {v:"fun",label:"Just have fun",eff:["euphoric","happiness"]},
  {v:"explore",label:"Explore & learn",eff:[]},
];
const SETTINGS = [
  {v:"solo",label:"Solo downtime",sub:"Just me, unwinding",ic:"🛋️"},
  {v:"partner",label:"With a partner",sub:"A quiet evening in",ic:"🫶"},
  {v:"social",label:"A social gathering",sub:"Friends & good vibes",ic:"🎉"},
  {v:"active",label:"Out & about",sub:"A hike, music, activity",ic:"🥾"},
  {v:"bed",label:"Right before bed",sub:"Winding down for sleep",ic:"🌙"},
];
const BRAND_PREFS = [
  {v:"craft",label:"Craft & premium",sub:"Small-batch, top-shelf quality",ic:"✨"},
  {v:"value",label:"Best value",sub:"Most for my money",ic:"🏷️"},
  {v:"trusted",label:"Trusted & consistent",sub:"Reliable names I can count on",ic:"🤝"},
  {v:"any",label:"No preference",sub:"Just show me the best fit",ic:"🎯"},
];
const THC_TOL = [{v:"u10",label:"Under 10%"},{v:"10-18",label:"10–18%"},{v:"18-25",label:"18–25%"},{v:"25+",label:"25%+"}];
const DOSE_TOL = [{v:"2.5",label:"2.5mg"},{v:"5",label:"5mg"},{v:"10",label:"10mg"},{v:"20+",label:"20mg+"}];
const BUDGET = [{v:"u20",label:"Under $20"},{v:"20-40",label:"$20–40"},{v:"40-60",label:"$40–60"},{v:"60+",label:"$60+"}];
const PRODQ = {
  flower:[{k:"tier",q:"What tier of flower do you want?",hint:"Optional.",opts:["Budget","Premium","Indoor"]},{k:"profile",q:"THC-forward, or balanced with CBD?",hint:"Optional.",opts:["High THC","Balanced THC/CBD"]}],
  preroll:[{k:"style",q:"How do you like your pre-rolls?",hint:"Optional.",opts:["Single","Multi-pack","Infused"]}],
  vape:[{k:"format",q:"510 cart or all-in-one disposable?",hint:"Optional.",opts:["510 cart","Disposable"]},{k:"extract",q:"Any extract type you prefer?",hint:"Live resin & rosin keep more flavor; distillate is cheaper and stronger.",opts:["Live Resin","Distillate","Rosin"]}],
  concentrate:[{k:"kind",q:"Which consistency are you after?",hint:"Optional.",opts:["Wax","Live Resin","Rosin","Badder","Diamonds"]},{k:"method",q:"Solvent or solventless?",hint:"Solventless (rosin) is prized for purity.",opts:["Solvent","Solventless"]}],
  edible:[{k:"form",q:"What kind of edible sounds good?",hint:"Optional.",opts:["Gummies","Chocolate","Other"]},{k:"ratio",q:"THC only, or balanced with CBD?",hint:"CBD makes edibles gentler.",opts:["THC only","1:1 CBD:THC"]}],
  drink:[{k:"onset",q:"Fast-acting or standard onset?",hint:"Fast-acting drinks kick in quicker.",opts:["Fast-acting","Standard"]}],
  tincture:[{k:"ratio",q:"Which ratio suits you?",hint:"Optional.",opts:["THC-forward","1:1","CBD-forward"]}],
  capsule:[{k:"aim",q:"Daytime relief or sleep?",hint:"Optional.",opts:["Daytime","Sleep"]}],
  topical:[{k:"aim",q:"What are you treating?",hint:"Optional.",opts:["Pain relief","Recovery"]}],
};

/* ========================= SURVEY FLOW ENGINE ========================= */
let qIndex = 0, advLock = false, FLOW = [];
function edibleType(){ return ['edible','drink','tincture','capsule'].includes(survey.type); }

function buildFlow(){
  const f = [];
  const nm = survey.name ? survey.name.trim().split(/\s+/)[0] : "";
  f.push({id:"name",group:"Hello",kind:"text",title:"First — what should I call you?",hint:"Optional, and it stays on your device. It just makes this feel less like a form.",placeholder:"Your name",key:"name",optional:true});
  f.push({id:"experience",group:"Getting to know you",kind:"single",title:nm?`Nice to meet you, ${nice(nm)}. How much experience do you have with cannabis?`:"How much experience do you have with cannabis?",hint:"No wrong answer — this calibrates everything, and we always lean gentle.",options:EXPERIENCE,key:"experience"});
  f.push({id:"frequency",group:"Getting to know you",kind:"single",title:"How often are you using it these days?",hint:"Helps me read your tolerance beyond just experience.",options:FREQUENCY,key:"frequency",optional:true});
  f.push({id:"goals",group:"Getting to know you",kind:"multi",title:"What's bringing you in today?",hint:"Pick whatever fits — this seeds your matches. You can choose more than one.",options:GOALS.map(g=>({v:g.v,label:g.label})),key:"goals",optional:true});
  f.push({id:"effects",group:"What you want",kind:"multi",title:"Which effects are you hoping for?",hint:"This is the biggest driver of your matches. Choose as many as feel right.",options:EFFECTS.map(e=>({v:e,label:nice(e)})),key:"effects",required:true});
  f.push({id:"avoid",group:"What you want",kind:"multi",title:"Anything you'd rather avoid?",hint:"Deal-breakers get weighted heavily, so we steer around them. Skip if nothing applies.",options:AVOIDS.map(a=>({v:a,label:nice(a)})),key:"avoid",neg:true,optional:true});
  f.push({id:"times",group:"What you want",kind:"multi",title:"When will you mostly use it?",hint:"Daytime picks stay clear-headed; nighttime picks lean calming.",options:TIMES.map(t=>({v:t,label:nice(t)})),key:"times",optional:true});
  f.push({id:"setting",group:"What you want",kind:"single",title:"Where do you picture using it?",hint:"Sets the vibe — solo calm feels different from a night out.",options:SETTINGS,key:"setting",optional:true});
  f.push({id:"type",group:"The product",kind:"type",title:"Any product format in mind?",hint:"Totally optional. Leave it open and I'll weigh every category for you.",key:"type"});
  if(survey.type && PRODQ[survey.type]) PRODQ[survey.type].forEach(row=> f.push({id:"pq_"+row.k,group:"The product",kind:"single",title:row.q,hint:row.hint,options:row.opts.map(o=>({v:o,label:o})),key:"prodq."+row.k,optional:true}));
  f.push({id:"strength",group:"Strength",kind:"slider",title:"How strong do you want it to feel?",hint:"We'll never push you past a comfortable ceiling.",key:"strength"});
  f.push({id:"tolerance",group:"Strength",kind:"single",key:edibleType()?"doseTol":"tolerance",
    title:edibleType()?"How many milligrams do you usually take?":"How much THC do you usually tolerate?",
    hint:edibleType()?"Edibles are dosed in mg and hit harder than they read.":"Flower & concentrate potency shows as % THC.",
    options:(edibleType()?DOSE_TOL:THC_TOL),optional:true});
  f.push({id:"flavor",group:"Taste",kind:"multi",title:"Any flavors you gravitate toward?",hint:"Optional — terpenes shape both taste and effect.",options:FLAVORS.map(x=>({v:x,label:nice(x)})),key:"flavors",optional:true});
  f.push({id:"brandPref",group:"Brands",kind:"single",title:"How do you like to choose a brand?",hint:"I'll factor this in and suggest brands worth exploring.",options:BRAND_PREFS,key:"brandPref",optional:true});
  f.push({id:"budget",group:"Budget",kind:"single",title:"What's your budget per item?",hint:"Keeps your picks realistic.",options:BUDGET,key:"budget",optional:true});
  return f;
}

function setAns(key,val){ if(key.indexOf('prodq.')===0){ survey.prodq[key.split('.')[1]]=val; } else survey[key]=val; }
function getAns(key){ if(key.indexOf('prodq.')===0) return survey.prodq[key.split('.')[1]]; return survey[key]; }

function startSurvey(){
  survey.name = profile.name||survey.name;
  document.getElementById('heroView').classList.add('hidden');
  document.getElementById('resultsView').classList.add('hidden');
  document.getElementById('surveyView').classList.remove('hidden');
  switchTab('find'); qIndex=0; renderQ();
}
function resetAll(){
  survey = freshSurvey(); qIndex=0;
  document.getElementById('surveyView').classList.add('hidden');
  document.getElementById('resultsView').classList.add('hidden');
  document.getElementById('heroView').classList.remove('hidden');
  switchTab('find');
}
function nextQ(){ FLOW=buildFlow(); if(qIndex>=FLOW.length-1){ runRecommend(); return; } qIndex++; renderQ(); }
function prevQ(){ if(qIndex>0){ qIndex--; renderQ(); } }

function renderQ(){
  FLOW = buildFlow();
  if(qIndex>=FLOW.length){ runRecommend(); return; }
  const q = FLOW[qIndex];
  const isLast = qIndex===FLOW.length-1;
  const pct = Math.round((qIndex+1)/FLOW.length*100);
  const host = document.getElementById('qcard');

  let optHTML = "";
  if(q.kind==="text"){
    optHTML = `<div class="qopts"><input class="qtext" id="qtextInput" placeholder="${q.placeholder||''}" value="${(getAns(q.key)||'').replace(/"/g,'&quot;')}"></div>`;
  } else if(q.kind==="single"){
    optHTML = `<div class="qopts">` + q.options.map(o=>{
      const sel = getAns(q.key)===o.v;
      return `<button class="q-single ${sel?'sel':''}" onclick="pickSingle('${q.key}','${o.v}',${isLast})">
        ${o.ic?`<span class="qs-ic">${o.ic}</span>`:`<span class="qs-radio"></span>`}
        <span class="qs-txt"><b>${o.label}</b>${o.sub?`<small>${o.sub}</small>`:''}</span>
        ${o.ic?`<span class="qs-radio" style="margin-left:auto"></span>`:''}</button>`;
    }).join('') + `</div>`;
  } else if(q.kind==="multi"){
    const arr = getAns(q.key)||[];
    optHTML = `<div class="qopts chips">` + q.options.map(o=>{
      const sel = arr.includes(o.v);
      return `<button class="chip ${sel?'sel':''} ${q.neg&&sel?'neg':''}" onclick="toggleMulti('${q.key}','${o.v}')">${o.label}</button>`;
    }).join('') + `</div>`;
  } else if(q.kind==="type"){
    optHTML = `<div class="steptype-grid">
      <button class="typecard ${survey.type===null?'sel':''}" onclick="pickType(null,${isLast})"><div class="ti">✳️</div><b>Open to anything</b><small>Weigh all categories</small></button>` +
      TYPES.map(t=>`<button class="typecard ${survey.type===t.id?'sel':''}" onclick="pickType('${t.id}',${isLast})"><div class="ti">${t.icon}</div><b>${t.name}</b><small>${t.sub}</small></button>`).join('') + `</div>`;
  } else if(q.kind==="slider"){
    optHTML = `<div class="slider-wrap">
      <div class="str-read" id="strRead">${STRENGTHS[survey.strength-1]}</div>
      <input type="range" min="1" max="5" step="1" value="${survey.strength}" id="strRange" oninput="survey.strength=+this.value;document.getElementById('strRead').textContent=STRENGTHS[survey.strength-1]">
      <div class="scale-labels"><span>Very mild</span><span>Medium</span><span>Extreme</span></div></div>`;
  }

  // footer
  const arr = getAns(q.key);
  const multiCount = Array.isArray(arr)?arr.length:0;
  const canContinue = !(q.required && q.kind==='multi' && multiCount===0);
  let primary = "";
  if(q.kind==="single" || q.kind==="type"){
    primary = isLast ? `<button class="btn" onclick="runRecommend()">See my matches →</button>` :
      (q.optional?`<button class="skip" onclick="nextQ()">Skip</button>`:``);
  } else {
    const label = isLast ? "See my matches →" : "Continue";
    const action = isLast ? "runRecommend()" : "commitAndNext()";
    primary = `<div style="display:flex;align-items:center;gap:6px">
      ${q.optional&&multiCount===0&&q.kind==='multi'?`<button class="skip" onclick="${isLast?'runRecommend()':'nextQ()'}">Skip</button>`:''}
      <button class="btn" ${canContinue?'':'disabled'} onclick="${action}">${label}</button></div>`;
  }

  host.innerHTML = `
    <div class="qprog"><i style="width:${pct}%"></i></div>
    <div class="qhead"><span class="qcount"><span class="qgroup">${q.group}</span> · ${qIndex+1} of ${FLOW.length}</span>
      <span class="qcount">${pct}%</span></div>
    <div class="qbody"><h2>${q.title}</h2><p class="qsub">${q.hint||''}</p>${optHTML}</div>
    <div class="qfoot">
      <button class="btn ghost" ${qIndex===0?'style="visibility:hidden"':''} onclick="prevQ()">← Back</button>
      ${primary}
    </div>`;

  const ti = document.getElementById('qtextInput');
  if(ti){ ti.focus(); ti.addEventListener('keydown',e=>{ if(e.key==='Enter') commitAndNext(); }); }
  document.getElementById('surveyView').scrollIntoView({block:'nearest'});
}

function pickSingle(key,val,isLast){
  setAns(key, getAns(key)===val && FLOW[qIndex].optional ? null : val);
  if(isLast){ renderQ(); return; }
  if(advLock) return; advLock=true; renderQ();
  setTimeout(()=>{ advLock=false; nextQ(); }, 230);
}
function pickType(id,isLast){
  survey.type = id; survey.prodq = {};
  if(isLast){ renderQ(); return; }
  if(advLock) return; advLock=true; renderQ();
  setTimeout(()=>{ advLock=false; nextQ(); }, 230);
}
function toggleMulti(key,val){
  const arr = getAns(key)||[]; const i=arr.indexOf(val);
  if(i>=0) arr.splice(i,1); else arr.push(val);
  setAns(key,arr); renderQ();
}
function commitAndNext(){
  const q=FLOW[qIndex];
  if(q.kind==='text'){ const ti=document.getElementById('qtextInput'); if(ti){ survey.name=ti.value.trim(); profile.name=survey.name; save(); } }
  nextQ();
}

/* ========================= RECOMMENDATION ENGINE ========================= */
const TOL_MAX={"u10":10,"10-18":18,"18-25":25,"25+":100};
const DOSE_MAX={"2.5":2.5,"5":5,"10":10,"20+":100};
const BUDGET_MAX={"u20":20,"20-40":40,"40-60":60,"60+":9999};
const AVOID_MAP={
  "anxiety":p=> p.avoids.includes("anxiety")||(p.thc>=22&&(p.effects.includes("energy")||p.effects.includes("head high"))),
  "couch lock":p=> p.avoids.includes("couch lock")||(p.strength>=4&&p.effects.includes("body high")&&p.effects.includes("sleep")),
  "dry mouth":p=> p.avoids.includes("dry mouth"),
  "dry eyes":p=> p.avoids.includes("dry eyes"),
  "high thc":p=> p.avoids.includes("high thc")||(['edible','drink','capsule','tincture'].includes(p.type)?p.dose>=20:((p.type==='vape'||p.type==='concentrate')&&p.thc>=75))||(['flower','preroll'].includes(p.type)&&p.thc>=25),
  "strong smell":p=> p.avoids.includes("strong smell")||p.flavors.includes("diesel")||p.flavors.includes("gassy"),
  "sleepiness":p=> p.avoids.includes("sleepiness")||p.effects.includes("sleep"),
};
function brandPrefScore(pref,style){
  const m={craft:{craft:1,wellness:.6,classic:.6,value:.35},value:{value:1,classic:.6,wellness:.55,craft:.35},trusted:{classic:1,wellness:.75,craft:.7,value:.6}};
  return (m[pref]&&m[pref][style])!=null?m[pref][style]:.5;
}
function expRank(){
  let r={first:1,beginner:2,occasional:3,regular:4,heavy:5}[survey.experience];
  if(!r) r={never:1,rare:2,monthly:3,weekly:4,daily:5}[survey.frequency]||3;
  return r;
}
function scoreProduct(p){
  const parts=[]; let score=0,weightSum=0;
  const add=(label,val,weight,detail)=>{ parts.push({label,val:Math.round(val*100),weight,detail}); score+=val*weight; weightSum+=weight; };

  if(survey.effects.length){
    const hit=survey.effects.filter(e=>p.effects.includes(e)).length;
    add("Desired effects", hit/survey.effects.length, 32, `${hit}/${survey.effects.length} present`);
  }
  const goalEff=new Set(); survey.goals.forEach(g=>{ const G=GOALS.find(x=>x.v===g); if(G) G.eff.forEach(e=>goalEff.add(e)); });
  if(goalEff.size){ const arr=[...goalEff]; const hit=arr.filter(e=>p.effects.includes(e)).length; add("Your goals", hit/arr.length, 10, `${hit}/${arr.length} goal effects`); }

  const sdiff=Math.abs(p.strength-survey.strength);
  add("Strength fit", Math.max(0,1-sdiff/3), 15, `Want ${STRENGTHS[survey.strength-1]}, this is ${STRENGTHS[p.strength-1]}`);

  const edibleish=['edible','drink','tincture','capsule'].includes(p.type);
  if(edibleish && survey.doseTol){ const ceil=DOSE_MAX[survey.doseTol]; const v=p.dose<=ceil?1:Math.max(0,1-(p.dose-ceil)/ceil); add("Dose tolerance",v,15,p.dose<=ceil?`${p.dose}mg within comfort`:`${p.dose}mg above your usual`); }
  else if(!edibleish && survey.tolerance){ const ceil=TOL_MAX[survey.tolerance]; const val=(p.type==='flower'||p.type==='preroll')?p.thc:(p.type==='vape'||p.type==='concentrate'?(p.strength>=5?30:p.strength>=4?24:16):p.thc); const v=val<=ceil?1:Math.max(0,1-(val-ceil)/ceil); add("THC tolerance",v,15,val<=ceil?`Within your ${survey.tolerance} range`:`Above your ${survey.tolerance} range`); }

  const er=expRank(); let bv;
  if(er<=2) bv=p.beginner/5; else if(er===3) bv=0.4+0.6*(p.beginner/5); else bv=0.7+0.3*(1-Math.abs(p.strength-4)/4);
  add("Suits experience", bv, 11, er<=2?`Beginner-friendliness ${p.beginner}/5`:`Matched to ${survey.experience||'your'} level`);

  if(survey.times.length){ const m=survey.times.includes("anytime")||p.time.includes("anytime")||survey.times.some(t=>p.time.includes(t)); add("Time of day", m?1:0.3, 8, m?"Fits when you'll use it":"Suited to another time"); }
  if(survey.brandPref && survey.brandPref!=='any'){ const st=(BRAND_INFO[p.brand]||{}).style; add("Brand fit", brandPrefScore(survey.brandPref,st), 8, `${p.brand} · ${nice(st||'')}`); }
  if(survey.flavors.length && p.flavors.length){ const hit=survey.flavors.filter(f=>p.flavors.includes(f)).length; add("Flavor", hit>0?Math.min(1,hit/Math.min(survey.flavors.length,2)):0.3, 6, hit>0?`${hit} flavor match`:"Different profile"); }
  if(survey.budget){ const within=p.price<=BUDGET_MAX[survey.budget]; add("Budget", within?1:0.2, 8, within?`$${p.price} within budget`:`$${p.price} over budget`); }

  let avoidPenalty=0; const avoidHits=[];
  survey.avoid.forEach(a=>{ if(AVOID_MAP[a]&&AVOID_MAP[a](p)){ avoidPenalty++; avoidHits.push(a); } });

  let base = weightSum? score/weightSum : 0.5;
  base = base*Math.pow(0.72, avoidPenalty);
  let pboost=0;
  p.flavors.forEach(f=>{ if(profile.flavors[f]) pboost+=0.01*profile.flavors[f]; });
  p.terps.forEach(t=>{ if(profile.terps[t]) pboost+=0.01*profile.terps[t]; });
  if(profile.brands[p.brand]) pboost+=0.015*profile.brands[p.brand];
  if(profile.types[p.type]) pboost+=0.01*profile.types[p.type];
  if(profile.disliked.includes(p.id)) base*=0.5;
  base=Math.min(1, base+Math.min(0.07,pboost));
  return { p, score:Math.round(base*100), parts, avoidHits, avoidPenalty };
}

let lastResults=[];
function runRecommend(){
  // learn from survey
  survey.flavors.forEach(f=> profile.flavors[f]=(profile.flavors[f]||0)+1);
  if(survey.type) profile.types[survey.type]=(profile.types[survey.type]||0)+1;
  survey.effects.forEach(e=> profile.effects[e]=(profile.effects[e]||0)+1);
  if(survey.tolerance) profile.tolerance.push(survey.tolerance);
  if(survey.brandPref) profile.brandPref=survey.brandPref;
  if(survey.name) profile.name=survey.name;
  profile.budget=survey.budget; profile.surveys=(profile.surveys||0)+1; save();

  let pool=CATALOG.slice();
  if(survey.type) pool=pool.filter(p=>p.type===survey.type);
  const pq=survey.prodq||{};
  if(survey.type==='vape'&&pq.extract) pool=pool.filter(p=>(p.subtype||'').toLowerCase().includes(pq.extract.toLowerCase()));
  if(survey.type==='vape'&&pq.format) pool=pool.filter(p=> pq.format==='Disposable'?/disposable/i.test(p.subtype||''):/510/i.test(p.subtype||''));
  if(pool.length<3&&survey.type) pool=CATALOG.filter(p=>p.type===survey.type);
  if(pool.length===0) pool=CATALOG.slice();

  const scored=pool.map(scoreProduct).sort((a,b)=>b.score-a.score);
  lastResults=scored;
  const top3=scored.slice(0,3);

  const answered=[survey.experience,survey.effects.length,survey.times.length,survey.goals.length,survey.tolerance||survey.doseTol,survey.flavors.length,survey.budget,survey.brandPref].filter(Boolean).length;
  const infoConf=answered/8;

  document.getElementById('surveyView').classList.add('hidden');
  document.getElementById('heroView').classList.add('hidden');
  document.getElementById('resultsView').classList.remove('hidden');

  const nm = survey.name? nice(survey.name.split(/\s+/)[0]) : "";
  document.getElementById('resultTitle').textContent = nm? `${nm}, here are your top 3` : "Top 3 recommendations";
  const wants = survey.effects.slice(0,3).map(nice).join(", ")||"a balanced experience";
  document.getElementById('resultSummary').innerHTML =
    `Based on your <b>${nice(survey.experience||'—')}</b> experience, wanting <b>${wants}</b>${survey.times.length?` for the <b>${survey.times.map(nice).join('/')}</b>`:''}${survey.avoid.length?`, avoiding <b>${survey.avoid.map(nice).join(', ')}</b>`:''}.`;

  renderRecs(top3,scored,infoConf);
  renderBrands(top3,scored);
  window.scrollTo({top:0,behavior:'smooth'});
}

function ringSVG(pct,size=58){
  const r=size/2-5,c=2*Math.PI*r,off=c*(1-pct/100);
  const col=pct>=75?'var(--green)':pct>=55?'var(--amber)':'var(--muted)';
  return `<svg class="ring" viewBox="0 0 ${size} ${size}"><circle cx="${size/2}" cy="${size/2}" r="${r}" fill="none" stroke="var(--line)" stroke-width="5"/>
    <circle cx="${size/2}" cy="${size/2}" r="${r}" fill="none" stroke="${col}" stroke-width="5" stroke-linecap="round" stroke-dasharray="${c}" stroke-dashoffset="${off}" transform="rotate(-90 ${size/2} ${size/2})"/>
    <text x="50%" y="52%" text-anchor="middle" dominant-baseline="middle" font-family="var(--serif)" font-size="15" font-weight="600" fill="var(--ink)">${pct}</text></svg>`;
}
function renderRecs(top3,scored,infoConf){
  const grid=document.getElementById('recGrid'); grid.innerHTML='';
  top3.forEach((r,i)=>{
    const p=r.p;
    const alt=scored.find(s=>s.p.type===p.type&&s.p.id!==p.id&&!top3.slice(0,i+1).some(t=>t.p.id===s.p.id))||scored.find(s=>!top3.some(t=>t.p.id===s.p.id));
    const conf=Math.min(99,Math.round(r.score*0.6+infoConf*100*0.4));
    const beginnerLabel=["—","Experts only","Cautious","Moderate","Friendly","Very friendly"][p.beginner];
    const typeName=TYPES.find(t=>t.id===p.type).name;
    const bstyle=(BRAND_INFO[p.brand]||{}).style;
    const card=document.createElement('div'); card.className='card rec'+(i===0?' top':'');
    card.innerHTML=`
      <div class="rank-ribbon">${i===0?'★ Best match':'Pick '+(i+1)}</div>
      <div class="rec-top">
        <div class="match-ring">${ringSVG(r.score)}<div class="mv"><b>${r.score}%</b><span>Match</span></div></div>
        <h3>${p.name}</h3>
        <div class="brandline">by <b>${p.brand}</b> <span class="brand-badge ${bstyle}" style="margin-left:4px">${nice(bstyle||'')}</span></div>
        <div class="ptype">${typeName}${p.subtype?' · '+p.subtype:''}</div>
      </div>
      <div class="rec-body">
        <div class="spec-row">
          <div class="spec"><div class="k">THC</div><div class="v mono">${p.thc}%${p.dose?` · ${p.dose}mg`:''}</div></div>
          <div class="spec"><div class="k">CBD</div><div class="v mono">${p.cbd}%</div></div>
          <div class="spec" style="grid-column:1/3"><div class="k">Dominant terpenes</div><div class="v">${p.terps.length?p.terps.join(' · '):'—'}</div></div>
          <div class="spec" style="grid-column:1/3"><div class="k">Flavor</div><div class="terps">${(p.flavors.length?p.flavors:['neutral']).map(f=>`<span class="pill line">${nice(f)}</span>`).join('')}</div></div>
        </div>
        <div><div class="kmini">Expected effects</div><div class="terps">${p.effects.map(e=>`<span class="pill ${survey.effects.includes(e)?'':'line'}">${nice(e)}</span>`).join('')}</div></div>
        <div class="metric-line"><span class="ml-k">Strength</span><div class="meter ${p.strength>=4?'amber':''}"><i style="width:${p.strength*20}%"></i></div><span class="mono" style="font-size:11px;width:74px">${STRENGTHS[p.strength-1]}</span></div>
        <div class="metric-line"><span class="ml-k">Beginner</span><div class="meter"><i style="width:${p.beginner*20}%"></i></div><span class="mono" style="font-size:11px;width:74px">${beginnerLabel}</span></div>
        <div class="why"><b>Why this fits:</b> ${whyText(r)}</div>
        ${r.avoidHits.length?`<div class="flags"><span class="pill amber">⚠ note: ${r.avoidHits.map(nice).join(', ')}</span></div>`:''}
        <div class="flags"><span class="pill">${conf}% confidence</span>${p.cbd>=p.thc*0.4?'<span class="pill line">CBD balanced</span>':''}${p.beginner>=4?'<span class="pill">Starter-safe</span>':''}</div>
      </div>
      <div class="rec-foot"><div class="alt">Similar: <a onclick="switchTab('compare');setCompare(['${p.id}','${alt?alt.p.id:''}'])">${alt?alt.p.name:'—'}</a> ·
        <a onclick="switchTab('compare');setCompare(['${p.id}'])">Compare</a> ·
        <a onclick="openFeedback('${p.id}')">I tried this</a></div></div>`;
    grid.appendChild(card);
  });

  const top=top3[0], ex=document.getElementById('matchExplain');
  ex.innerHTML=`<div class="card" style="padding:22px;margin-top:22px">
    <div class="eyebrow">Explain the match · ${top.p.name}</div>
    <h3 style="font-size:20px;margin:8px 0 12px">Why ${top.p.name} by ${top.p.brand} scored ${top.score}%</h3>
    <p style="max-width:70ch;margin:0 0 18px">${matchNarrative(top)}</p>
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px 26px;max-width:760px">
      ${top.parts.map(pt=>`<div class="metric-line"><span class="ml-k" style="width:120px">${pt.label}</span><div class="meter ${pt.val<55?'amber':''}"><i style="width:${pt.val}%"></i></div><span class="mono" style="font-size:11px;width:38px;text-align:right">${pt.val}%</span></div>`).join('')}
    </div>
    <p style="color:var(--muted);font-size:12px;margin:16px 0 0">Bars show how well each factor scored; wider = stronger fit. Effects and strength carry the most weight.
    ${(survey.experience==='first'||survey.experience==='beginner')?'<b style="color:var(--green)"> Beginner tip:</b> start with the lowest amount, wait, and take more only if needed.':''}</p></div>`;
}
function whyText(r){
  const p=r.p,bits=[];
  const hitE=survey.effects.filter(e=>p.effects.includes(e)).map(nice);
  if(hitE.length) bits.push(`delivers the ${hitE.slice(0,3).join(', ')} you asked for`);
  const sdiff=Math.abs(p.strength-survey.strength);
  if(sdiff===0) bits.push(`lands right at your target strength`); else if(sdiff===1) bits.push(`sits close to your desired strength`);
  if(p.cbd>=p.thc*0.4&&p.thc>0) bits.push(`its CBD content softens the THC`);
  if((survey.experience==='first'||survey.experience==='beginner')&&p.beginner>=4) bits.push(`it's forgiving for newer users`);
  if(survey.avoid.length&&!r.avoidHits.length) bits.push(`it steers clear of your avoid-list`);
  const hitF=survey.flavors.filter(f=>p.flavors.includes(f)).map(nice);
  if(hitF.length) bits.push(`with the ${hitF.join('/')} flavor you like`);
  if(survey.brandPref==='craft'&&(BRAND_INFO[p.brand]||{}).style==='craft') bits.push(`from a craft brand, which you prefer`);
  if(survey.brandPref==='value'&&(BRAND_INFO[p.brand]||{}).style==='value') bits.push(`at a value-focused price`);
  if(!bits.length) bits.push(`it's a solid all-round fit for your answers`);
  return bits.join('; ')+'.';
}
function matchNarrative(r){
  const p=r.p, exp=survey.experience||'your';
  const wants=survey.effects.length?survey.effects.map(nice).join(', '):'a balanced experience';
  let s=`Based on your ${nice(exp)} experience level and your interest in ${wants}`;
  if(survey.times.length) s+=` for the ${survey.times.map(nice).join(' and ')}`;
  s+=`, ${p.name} from ${p.brand} stands out`;
  if(p.cbd>=p.thc*0.4&&p.thc>0) s+=` because its more balanced ${p.terps[0]?p.terps[0]+'-led ':''}profile delivers what you want without leaning as intense as a high-THC ${nice(p.type)}`;
  else s+=` because its ${p.terps[0]?p.terps[0]+'-forward ':''}profile aligns with the effects you're after`;
  if(survey.brandPref&&survey.brandPref!=='any') s+=`, and ${p.brand} fits your taste for ${survey.brandPref==='craft'?'craft, premium':survey.brandPref==='value'?'good value':'trusted, consistent'} brands`;
  if(survey.avoid.length&&!r.avoidHits.length) s+=`. It also avoids ${survey.avoid.map(nice).join(', ')}`;
  s+='.';
  if(survey.avoid.length&&r.avoidHits.length) s+=` One caveat: it may still involve ${r.avoidHits.map(nice).join(', ')} — worth keeping in mind.`;
  return s;
}
function styleMatch(pref,style){ return (pref==='craft'&&style==='craft')||(pref==='value'&&style==='value')||(pref==='trusted'&&style==='classic'); }
function renderBrands(top3,scored){
  const inMatches=[...new Set(top3.map(r=>r.p.brand))];
  const brandBest={};
  scored.forEach(r=>{ const b=r.p.brand; const ov=survey.effects.filter(e=>r.p.effects.includes(e)).length;
    if(!(b in brandBest)||ov>brandBest[b].ov||(ov===brandBest[b].ov&&r.score>brandBest[b].score)) brandBest[b]={ov,score:r.score,p:r.p}; });
  let others=Object.keys(brandBest).filter(b=>!inMatches.includes(b));
  others.sort((a,b)=>{
    const wa=(survey.brandPref&&survey.brandPref!=='any'&&styleMatch(survey.brandPref,(BRAND_INFO[a]||{}).style))?1:0;
    const wb=(survey.brandPref&&survey.brandPref!=='any'&&styleMatch(survey.brandPref,(BRAND_INFO[b]||{}).style))?1:0;
    if(wa!==wb) return wb-wa;
    return (brandBest[b].ov-brandBest[a].ov)||(brandBest[b].score-brandBest[a].score);
  });
  const explore=others.slice(0,3);
  const card=(b,tag)=>{ const info=BRAND_INFO[b]||{style:'classic',blurb:''}; const p=brandBest[b].p;
    return `<div class="brand-card"><div class="bc-top"><h4>${b}</h4><span class="brand-badge ${info.style}">${nice(info.style)}</span></div>
      <p>${info.blurb}</p>
      <div style="margin-top:10px;font-size:11.5px;color:var(--muted)">${tag} · e.g. <a onclick="switchTab('compare');setCompare(['${p.id}'])" style="cursor:pointer">${p.name}</a></div></div>`; };
  document.getElementById('brandsPanel').innerHTML=`
    <div class="card" style="padding:22px">
      <div class="eyebrow">Brands for you</div>
      <h3 style="font-size:20px;margin:8px 0 4px">${survey.brandPref&&survey.brandPref!=='any'?`Matched to your taste for ${survey.brandPref==='craft'?'craft':survey.brandPref==='value'?'value':'trusted'} brands`:'Brands worth knowing'}</h3>
      <p style="color:var(--muted);margin:0 0 6px;font-size:13px">The houses behind your matches, plus a few others strong in the effects you want.</p>
      <div class="kmini" style="margin-top:16px">In your picks</div>
      <div class="brand-grid">${inMatches.map(b=>card(b,'In your matches')).join('')}</div>
      ${explore.length?`<div class="kmini" style="margin-top:18px">Worth exploring</div><div class="brand-grid">${explore.map(b=>card(b,'Strong for your effects')).join('')}</div>`:''}
    </div>`;
}

/* ========================= FEEDBACK ========================= */
function openFeedback(pid){
  const p=CATALOG.find(x=>x.id===pid);
  const worked=confirm(`Feedback on ${p.name} (${p.brand})\n\nDid it work for you?  (OK = yes · Cancel = no)`);
  const strong=confirm(`Was it too strong?  (OK = yes, too strong · Cancel = strength was fine)`);
  const again=confirm(`Would you buy ${p.name} again?  (OK = yes · Cancel = no)`);
  const acc=Math.max(1,Math.min(5,parseInt(prompt("How accurate was this recommendation? 1–5","4"))||3));
  profile.feedback.unshift({pid,name:p.name,brand:p.brand,worked,tooStrong:strong,again,accuracy:acc,ts:Date.now()});
  if(!worked||!again){ if(!profile.disliked.includes(pid)) profile.disliked.push(pid); }
  if(worked&&again){ p.flavors.forEach(f=>profile.flavors[f]=(profile.flavors[f]||0)+2); p.terps.forEach(t=>profile.terps[t]=(profile.terps[t]||0)+2); profile.types[p.type]=(profile.types[p.type]||0)+1; profile.brands[p.brand]=(profile.brands[p.brand]||0)+2; }
  save();
  toast(worked&&again?"Thanks — I'll recommend more like this.":"Got it — I'll adjust away from this.");
}

/* ========================= COMPARE ========================= */
let cmpSel=[];
function renderComparePicker(){
  document.getElementById('cmpPicker').innerHTML=CATALOG.map(p=>`<button class="chip ${cmpSel.includes(p.id)?'sel':''}" onclick="toggleCmp('${p.id}')">${p.name} <span style="opacity:.6">· ${p.brand}</span></button>`).join('');
  renderCmpTable();
}
function toggleCmp(id){ const i=cmpSel.indexOf(id); if(i>=0) cmpSel.splice(i,1); else { if(cmpSel.length>=4){ toast("Compare up to 4 at once."); return; } cmpSel.push(id); } renderComparePicker(); }
function setCompare(ids){ cmpSel=ids.filter(Boolean).slice(0,4); renderComparePicker(); }
function renderCmpTable(){
  const out=document.getElementById('cmpOut');
  if(cmpSel.length<1){ out.innerHTML=`<div class="empty">Select products above to compare them side by side.</div>`; return; }
  const ps=cmpSel.map(id=>CATALOG.find(p=>p.id===id));
  const rows=[
    ["Brand",p=>`${p.brand}<br><small style="color:var(--muted)">${nice((BRAND_INFO[p.brand]||{}).style||'')}</small>`],
    ["Type",p=>nice(p.type)+(p.subtype?`<br><small style="color:var(--muted)">${p.subtype}</small>`:'')],
    ["THC",p=>`<span class="mono">${p.thc}%${p.dose?` · ${p.dose}mg`:''}</span>`],
    ["CBD",p=>`<span class="mono">${p.cbd}%</span>`],
    ["Terpenes",p=>p.terps.length?p.terps.join(', '):'—'],
    ["Flavor",p=>(p.flavors.length?p.flavors:['neutral']).map(f=>`<span class="pill line">${nice(f)}</span>`).join(' ')],
    ["Effects",p=>p.effects.map(e=>`<span class="pill">${nice(e)}</span>`).join(' ')],
    ["Strength",p=>`${STRENGTHS[p.strength-1]}<div class="meter ${p.strength>=4?'amber':''}" style="margin-top:5px"><i style="width:${p.strength*20}%"></i></div>`],
    ["Duration",p=>durationOf(p)],
    ["Best for",p=>bestFor(p)],
    ["Beginner rating",p=>`${p.beginner}/5<div class="meter" style="margin-top:5px"><i style="width:${p.beginner*20}%"></i></div>`],
    ["Price",p=>`<span class="mono">$${p.price}</span>`],
  ];
  out.innerHTML=`<div class="cmp-table-wrap"><table class="cmp">
    <thead><tr><th class="rowkey"></th>${ps.map(p=>`<th><h4>${p.name}</h4><small>${p.brand}</small></th>`).join('')}</tr></thead>
    <tbody>${rows.map(([k,fn])=>`<tr><td class="rowkey">${k}</td>${ps.map(p=>`<td>${fn(p)}</td>`).join('')}</tr>`).join('')}</tbody></table></div>`;
}
function durationOf(p){
  if(['edible','capsule'].includes(p.type)) return "4–8 hrs (slow onset 30–90 min)";
  if(p.type==='drink') return "2–4 hrs (faster onset)";
  if(p.type==='tincture') return "3–6 hrs (onset 15–45 min)";
  if(p.type==='topical') return "2–4 hrs (localized)";
  return "1–3 hrs (near-instant onset)";
}
function bestFor(p){ const e=p.effects;
  if(e.includes('sleep')) return "Nighttime & rest";
  if(e.includes('energy')||e.includes('focus')) return "Daytime & activity";
  if(e.includes('socializing')) return "Social settings";
  if(e.includes('pain management')) return "Relief & recovery";
  if(e.includes('creativity')) return "Creative sessions";
  return "Relaxed unwinding";
}

/* ========================= ASK ========================= */
const KB=[
  {q:["difference between live resin and distillate","live resin vs distillate","resin distillate"],conf:"high",
   a:`<b>Live resin</b> is extracted from fresh, flash-frozen cannabis, so it keeps the plant's original terpenes — richer flavor and a fuller "entourage" effect. <b>Distillate</b> is stripped to nearly pure THC (often 85–95%), then flavored with terpenes added back in. Distillate is more potent by THC alone and usually cheaper; live resin tends to taste better and feel more nuanced or balanced. In our catalog, <b>Emberline's Gelato live resin</b> vs. <b>Volt's Blue Razz distillate</b> is exactly this contrast.`,
   cites:[["Leafly: Live resin vs. distillate","https://www.leafly.com/news/cannabis-101/live-resin"],["NIH — Cannabis terpenes review","https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7324885/"]]},
  {q:["best cart for sleep","cart for sleep","vape for sleep","best product for sleep"],conf:"moderate",
   a:`For sleep, look for an <b>indica-leaning cart rich in myrcene and linalool</b>, ideally with some <b>CBN</b>. In our catalog, <b>Nightshade's Sleepytime Indica</b> disposable and <b>Sleep Gummies (10mg + CBN)</b> are tuned for rest. Edibles last longer (staying asleep) while a vape acts fast (falling asleep). Evidence for cannabis and sleep is mixed and mostly short-term.`,
   cites:[["Sleep Medicine Reviews — cannabis & sleep","https://pubmed.ncbi.nlm.nih.gov/28349316/"],["NIH — CBN research (limited)","https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8383237/"]]},
  {q:["why did this strain make me anxious","strain made me anxious","cannabis anxiety","weed anxiety"],conf:"high",
   a:`High-THC products can trigger anxiety, especially at higher doses or for less experienced users — THC over-activates CB1 receptors in fear-related brain regions. What helps: <b>lower THC</b>, choosing products with <b>CBD</b> (which can blunt THC's anxiety), and terpenes like <b>linalool</b> and <b>limonene</b>. Start low, go slow. A rough experience is usually a dose issue, not a permanent reaction.`,
   cites:[["JAMA/NIH — THC dose & anxiety","https://pubmed.ncbi.nlm.nih.gov/28150151/"],["Neuropsychopharmacology — CBD & anxiety","https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4604171/"]]},
  {q:["what terpene helps with focus","terpene for focus","focus terpene"],conf:"moderate",
   a:`<b>Pinene</b> is the terpene most linked to alertness and focus — the piney aroma in rosemary and conifers, with small studies tying it to memory and clear-headedness. <b>Limonene</b> (citrus) is uplifting and may help mood/energy. Most terpene-and-focus evidence is preclinical, so treat it as promising rather than proven.`,
   cites:[["NIH — Pinene pharmacology review","https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3111147/"],["Frontiers — terpenes & the entourage effect","https://www.frontiersin.org/articles/10.3389/fnins.2018.01487/full"]]},
  {q:["how much should a beginner smoke","how much should a beginner","beginner dose","start dose"],conf:"high",
   a:`<b>Start with one small inhale and wait 10–15 minutes</b> before more — smoking/vaping peaks fast. For edibles, start at <b>2.5mg THC (never more than 5mg)</b> and wait a full <b>2 hours</b>. Lower-THC or 1:1 CBD:THC products are the gentlest entry. You can always take more; you can't take less.`,
   cites:[["Colorado gov — 'Start Low, Go Slow'","https://cdphe.colorado.gov/marijuana"],["Canada — Lower-Risk Use Guidelines","https://www.canada.ca/en/health-canada/services/drugs-medication/cannabis/health-effects.html"]]},
  {q:["difference between indica and sativa","indica vs sativa","indica sativa"],conf:"moderate",
   a:`The rule of thumb: <b>indica = relaxing/body</b>, <b>sativa = energizing/heady</b>, hybrids in between. Useful shorthand, but scientists increasingly say the <b>indica/sativa label doesn't reliably predict effects</b> — the experience comes from the mix of <b>THC, CBD, and terpenes</b>. Read the cannabinoid and terpene profile over the label when you can.`,
   cites:[["Nature — cannabis taxonomy & effects","https://www.nature.com/articles/s41598-021-84755-z"],["NIH — chemotype vs. indica/sativa","https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4189631/"]]},
  {q:["how do edibles compare to smoking","edibles vs smoking","edibles compared to smoking"],conf:"high",
   a:`<b>Onset:</b> smoking/vaping hits in minutes, fades in 1–3 hrs; edibles take <b>30–90 min</b> and last <b>4–8 hrs</b>. <b>Intensity:</b> the liver converts edible THC into a stronger, more sedating compound (11-hydroxy-THC), so edibles feel more potent per mg and are easier to overdo. <b>Lungs:</b> edibles avoid inhalation. Golden rule with edibles: dose low and be patient.`,
   cites:[["NIH — oral vs inhaled THC pharmacokinetics","https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3820295/"],["11-hydroxy-THC metabolism","https://pubmed.ncbi.nlm.nih.gov/6273315/"]]},
  {q:["what product is similar to this","similar product","something similar"],conf:"moderate",
   a:`Tell me a product name and I'll find the closest match by type, potency, and terpene profile — or use the <b>Compare</b> tab to line options up side by side. "Similar" usually means the same category, a comparable THC level, and overlapping dominant terpenes (often from the same brand's house style).`,
   cites:[["Leafly — reading terpene profiles","https://www.leafly.com/news/cannabis-101/terpenes-the-flavors-of-cannabis-aromatherapy"]]},
  {q:["why is this product expensive","why expensive","product expensive","cost so much"],conf:"moderate",
   a:`Price mostly tracks <b>how it's made and who makes it</b>. <b>Solventless</b> extracts (live rosin, badder) are labor-intensive and command a premium; <b>indoor</b> and craft flower cost more to grow; small-batch brands (like our Marrow Extracts or Foothold Farms) price higher than value houses (Volt, Common Ground). Taxes are steep too. Higher price doesn't always mean better <em>for you</em> — a mid-priced match to your needs often beats a pricier mismatch.`,
   cites:[["MJBizDaily — cannabis pricing factors","https://mjbizdaily.com/"],["Leafly — solventless vs solvent extracts","https://www.leafly.com/news/cannabis-101/what-is-solventless-cannabis-concentrate"]]},
  {q:["which products taste fruity","fruity products","fruity flavor","taste fruity"],conf:"high",
   a:`Fruity flavor comes mostly from terpenes and genetics. Fruity-leaning picks here include <b>Marrow's Rosin Cart — Papaya</b>, <b>Emberline's Gelato live resin</b>, <b>Baker's Dozen Classic Gummies</b>, and <b>Foothold's Wedding Cake pre-roll</b>. Driving terpenes: <b>limonene</b> (citrus), <b>myrcene</b> (mango/berry), and <b>caryophyllene</b> blends. Use the Flavor step in the survey to prioritize it.`,
   cites:[["Frontiers — terpene aroma profiles","https://www.frontiersin.org/articles/10.3389/fpls.2019.01487/full"]]},
  {q:["strongest concentrate","what is the strongest concentrate","most potent concentrate"],conf:"high",
   a:`By raw THC, <b>THCA diamonds</b> are strongest — often <b>90%+</b> (our <b>Emberline Live Resin Diamonds</b>). Distillate is similarly high. Solventless <b>live rosin</b> is a bit lower in pure THC but prized for full-spectrum flavor. These are for <b>experienced users only</b> — one dab can exceed a beginner's whole session. Start rice-grain-sized if you're new to dabbing.`,
   cites:[["Leafly — cannabis concentrates guide","https://www.leafly.com/news/cannabis-101/what-are-cannabis-concentrates"],["NIH — high-potency cannabis & risk","https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7092635/"]]},
  {q:["what should i avoid as a beginner","beginner should avoid","avoid as a beginner","beginner avoid"],conf:"high",
   a:`As a beginner, avoid: <b>high-THC concentrates and dabs</b> (diamonds, wax), <b>large edible doses</b> (over 5mg to start), <b>heavily infused pre-rolls</b>, and mixing with alcohol. Better starts: <b>low-dose edibles/drinks (2.5–5mg)</b>, <b>1:1 CBD:THC</b> products, or <b>lower-THC flower</b>. Always start low, wait, and go slow.`,
   cites:[["CAMH — Lower-Risk Cannabis Use Guidelines","https://www.camh.ca/en/health-info/lower-risk-cannabis-use-guidelines"],["Colorado — Start Low Go Slow","https://cdphe.colorado.gov/marijuana"]]},
  {q:["what is cbd","cbd","cannabidiol"],conf:"high",
   a:`<b>CBD (cannabidiol)</b> is a non-intoxicating cannabinoid — it won't get you "high." People use it for calm and everyday relief, and it can <b>counteract some of THC's anxiety and intensity</b>, which is why 1:1 products feel gentler. Strongest evidence is for a prescription form treating rare epilepsy; for anxiety, sleep, and pain the research is promising but still developing.`,
   cites:[["FDA — CBD (Epidiolex) approval","https://www.fda.gov/news-events/press-announcements/fda-approves-first-drug-comprised-active-ingredient-derived-marijuana-treat-rare-severe-forms"],["WHO — CBD critical review","https://www.who.int/publications/i/item/WHO-PSM-QSP-2018.1"]]},
  {q:["what are terpenes","terpenes","terpene"],conf:"moderate",
   a:`<b>Terpenes</b> are the aromatic oils that give cannabis (and lavender, citrus, pine) its smell and flavor. Beyond aroma, many researchers think they subtly shape effects via the <b>"entourage effect"</b> — e.g. myrcene (calming), limonene (uplifting), pinene (alert), linalool (relaxing), caryophyllene (soothing). A compelling theory with growing but not yet conclusive evidence.`,
   cites:[["Frontiers — terpenes & entourage effect","https://www.frontiersin.org/articles/10.3389/fnins.2018.01487/full"],["British J. Pharmacology — Taming THC","https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3165946/"]]},
];
const KB_FALLBACK={conf:"limited",a:`I don't have a sourced answer for that exact question yet, so I'd rather not guess. Try me on <b>live resin vs. distillate, terpenes, dosing, indica vs. sativa, edibles vs. smoking, beginner tips, or pricing</b> — or run the <b>survey</b> for a personalized pick. For anything medical, please talk to a licensed clinician.`,cites:[["NIH — cannabis research portal","https://www.nih.gov/news-events/nih-research-matters"]]};
const SUGGESTS=["What's the difference between live resin and distillate?","What's the best cart for sleep?","Why did this strain make me anxious?","What terpene helps with focus?","How much should a beginner smoke?","What's the difference between indica and sativa?","How do edibles compare to smoking?","Why is this product expensive?","Which products taste fruity?","What's the strongest concentrate?","What should I avoid as a beginner?"];
function renderSuggests(){ document.getElementById('suggests').innerHTML=SUGGESTS.map(s=>`<button onclick="askSuggest(this)">${s}</button>`).join(''); }
function askSuggest(btn){ document.getElementById('chatInput').value=btn.textContent; sendChat(); }
function matchKB(text){
  const t=text.toLowerCase(); let best=null,bestScore=0;
  KB.forEach(item=> item.q.forEach(key=>{ const kw=key.split(/\s+/); let hit=0; kw.forEach(w=>{ if(w.length>2&&t.includes(w)) hit++; }); let sc=hit/kw.length; if(t.includes(key)) sc+=1; if(sc>bestScore){ bestScore=sc; best=item; } }));
  return bestScore>=0.34?best:KB_FALLBACK;
}
const CONF_META={high:["High-quality evidence","var(--good)"],moderate:["Moderate evidence","var(--warn)"],limited:["Limited / anecdotal","var(--crit)"]};
function confBadge(l){ const [lab,col]=CONF_META[l]||CONF_META.limited; return `<span class="ev-conf"><span class="conf-dot" style="background:${col}"></span>Evidence: ${lab}</span>`; }
function pushMsg(role,html){ const s=document.getElementById('chatScroll'); const d=document.createElement('div'); d.className='msg '+role;
  d.innerHTML=role==='bot'?`<div class="bubble"><div class="who"><span>🌿</span> Counterleaf</div>${html}</div>`:`<div class="bubble">${html}</div>`; s.appendChild(d); s.scrollTop=s.scrollHeight; return d; }
function sendChat(){
  const inp=document.getElementById('chatInput'); const q=inp.value.trim(); if(!q) return;
  pushMsg('user',escapeHtml(q)); inp.value='';
  const typing=pushMsg('bot',`<div class="typing"><span></span><span></span><span></span></div>`);
  setTimeout(()=>{ const item=matchKB(q);
    const html=`${item.a}<div class="evidence">${confBadge(item.conf)}${item.conf!=='high'?`<div style="color:var(--muted);font-size:11.5px;margin:4px 0 6px">${item.conf==='limited'?'Based largely on user reports — evidence is thin.':'Some scientific support, but not conclusive.'}</div>`:''}<div class="cites">${item.cites.map(([t,u])=>`<a href="${u}" target="_blank" rel="noopener">${t}</a>`).join('')}</div></div>`;
    typing.querySelector('.bubble').innerHTML=`<div class="who"><span>🌿</span> Counterleaf</div>${html}`;
    document.getElementById('chatScroll').scrollTop=1e9;
  },550);
}
function escapeHtml(s){ return s.replace(/[&<>"]/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;'}[c])); }
document.getElementById('chatInput').addEventListener('keydown',e=>{ if(e.key==='Enter') sendChat(); });
function initChat(){ const s=document.getElementById('chatScroll'); if(s.children.length) return;
  pushMsg('bot',`Hi — I'm your AI budtender. Ask me anything about products, brands, effects, terpenes, or dosing, and I'll answer with evidence and citations. I'll always tell you when the science is thin. <b>What can I help you find?</b><div class="evidence">${confBadge('high')}<div class="cites"><a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7324885/" target="_blank" rel="noopener">NIH — Cannabis & terpene research</a></div></div>`);
  renderSuggests(); }

/* ========================= PROFILE ========================= */
function topKeys(obj,n=6){ return Object.entries(obj||{}).sort((a,b)=>b[1]-a[1]).slice(0,n); }
function renderProfile(){
  const g=document.getElementById('profGrid');
  const favF=topKeys(profile.flavors),favT=topKeys(profile.terps),favTy=topKeys(profile.types),favB=topKeys(profile.brands);
  const tolMode=profile.tolerance.length?profile.tolerance.slice(-1)[0]:null;
  const disliked=profile.disliked.map(id=>{const p=CATALOG.find(x=>x.id===id);return p?p.name:null;}).filter(Boolean);
  const bp=profile.brandPref;
  g.innerHTML=`
    <div class="card" style="padding:20px">
      <div class="eyebrow">Learned preferences</div>
      <h3 style="font-size:18px;margin:8px 0 12px">${profile.name?nice(profile.name)+"'s profile":'What Counterleaf knows'}</h3>
      <div class="kv"><span>Surveys completed</span><b>${profile.surveys||0}</b></div>
      <div class="kv"><span>Typical THC tolerance</span><b>${tolMode?nice(tolMode):'—'}</b></div>
      <div class="kv"><span>Brand preference</span><b>${bp?(bp==='craft'?'Craft & premium':bp==='value'?'Best value':bp==='trusted'?'Trusted':'No preference'):'—'}</b></div>
      <div class="kv"><span>Budget</span><b>${profile.budget?nice(profile.budget.replace('u','under ')):'—'}</b></div>
      <div class="kv"><span>Feedback logged</span><b>${profile.feedback.length}</b></div>
      <div style="margin-top:14px"><div class="kmini">Favorite brands</div><div class="taglist">${favB.length?favB.map(([k,v])=>`<span class="pill">${k} ·${v}</span>`).join(''):'<span style="color:var(--muted);font-size:12px">Log a product you loved to build this.</span>'}</div></div>
      <div style="margin-top:12px"><div class="kmini">Favorite flavors</div><div class="taglist">${favF.length?favF.map(([k,v])=>`<span class="pill line">${nice(k)} ·${v}</span>`).join(''):'<span style="color:var(--muted);font-size:12px">Complete a survey to build this.</span>'}</div></div>
      <div style="margin-top:12px"><div class="kmini">Favorite terpenes</div><div class="taglist">${favT.length?favT.map(([k,v])=>`<span class="pill amber">${k} ·${v}</span>`).join(''):'<span style="color:var(--muted);font-size:12px">—</span>'}</div></div>
      ${disliked.length?`<div style="margin-top:12px"><div class="kmini">Steering away from</div><div class="taglist">${disliked.map(n=>`<span class="pill line" style="color:var(--crit)">${n}</span>`).join('')}</div></div>`:''}
    </div>
    <div class="card" style="padding:20px">
      <div class="eyebrow">Feedback loop</div>
      <h3 style="font-size:18px;margin:8px 0 12px">Your product reviews</h3>
      ${profile.feedback.length?profile.feedback.slice(0,8).map(f=>`
        <div class="fb-item">
          <div style="display:flex;justify-content:space-between;align-items:center;gap:8px"><b>${f.name} <span style="color:var(--muted);font-weight:400">· ${f.brand||''}</span></b><span class="pill ${f.worked&&f.again?'':'line'}">${f.accuracy}/5 accurate</span></div>
          <div class="taglist" style="margin-top:8px">
            <span class="pill line" style="color:${f.worked?'var(--good)':'var(--crit)'}">${f.worked?'✓ Worked':'✗ Didn\'t work'}</span>
            <span class="pill line">${f.tooStrong?'Too strong':'Strength OK'}</span>
            <span class="pill line" style="color:${f.again?'var(--good)':'var(--crit)'}">${f.again?'Would rebuy':'Won\'t rebuy'}</span>
          </div></div>`).join(''):`<div style="color:var(--muted);font-size:13px">No reviews yet. After a recommendation, tap <b>"I tried this"</b> to log how it went — Counterleaf uses it to refine future picks and learn which brands you love.</div>`}
    </div>`;
}
function clearProfile(){ if(!confirm("Reset all saved preferences and feedback on this device?")) return; profile={...defaultProfile,flavors:{},terps:{},types:{},effects:{},brands:{},disliked:[],tolerance:[],feedback:[]}; save(); survey=freshSurvey(); renderProfile(); toast("Profile reset."); }

/* ========================= HERO CANVAS ========================= */
function initLeaves(){
  const cv=document.getElementById('leafCanvas'); if(!cv) return; const ctx=cv.getContext('2d'); let W,H,dots;
  function size(){ const r=cv.getBoundingClientRect(); W=cv.width=r.width*devicePixelRatio; H=cv.height=r.height*devicePixelRatio;
    dots=Array.from({length:26},()=>({x:Math.random()*W,y:Math.random()*H,r:(6+Math.random()*16)*devicePixelRatio,vy:(0.05+Math.random()*0.12)*devicePixelRatio,vx:(Math.random()-0.5)*0.05*devicePixelRatio,a:0.04+Math.random()*0.06})); }
  size(); const reduce=matchMedia('(prefers-reduced-motion: reduce)').matches;
  const col=()=>getComputedStyle(document.documentElement).getPropertyValue('--sage').trim();
  function draw(){ ctx.clearRect(0,0,W,H); const c=col();
    dots.forEach(d=>{ ctx.beginPath(); ctx.fillStyle=c; ctx.globalAlpha=d.a; ctx.arc(d.x,d.y,d.r,0,7); ctx.fill(); if(!reduce){ d.y-=d.vy; d.x+=d.vx; if(d.y<-20){ d.y=H+20; d.x=Math.random()*W; } } });
    ctx.globalAlpha=1; if(!reduce) requestAnimationFrame(draw); }
  draw(); addEventListener('resize',size);
}

/* ========================= INIT ========================= */
initChat(); initLeaves();
</script>
<style>
  .demo-badge{position:fixed;left:14px;bottom:14px;z-index:80;font-family:var(--sans,system-ui,sans-serif);
    font-size:10.5px;font-weight:700;letter-spacing:.16em;text-transform:uppercase;color:#fff;
    background:var(--green,#2E5A45);border:1px solid rgba(255,255,255,.14);border-radius:999px;
    padding:7px 13px;box-shadow:0 10px 26px -14px rgba(0,0,0,.6);opacity:.94;pointer-events:none;}
  @media (max-width:640px){ .demo-badge{ left:10px; bottom:10px; font-size:9.5px; padding:6px 11px; } }
</style>
<div class="demo-badge">Trial Demo</div>
<script>
  if ('serviceWorker' in navigator) {
    window.addEventListener('load', () => navigator.serviceWorker.register('sw.js').catch(() => {}));
  }
</script>
</body>
</html>
