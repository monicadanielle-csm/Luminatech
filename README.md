# Presentation for Luminatech Analysis of Churn Rate
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Customer Churn Analysis — Luminatech 2023–2024</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&family=DM+Serif+Display&display=swap" rel="stylesheet">
<style>
  :root {
    --teal-bright: #3ecfcf;
    --teal-mid: #2aafb8;
    --teal-dark: #1a7a85;
    --bg-dark: #0d1f26;
    --bg-mid: #112830;
    --bg-card: rgba(255,255,255,0.04);
    --bg-card-hover: rgba(255,255,255,0.07);
    --white: #ffffff;
    --white-70: rgba(255,255,255,0.7);
    --white-40: rgba(255,255,255,0.4);
    --white-15: rgba(255,255,255,0.12);
    --orange: #e8622a;
    --green: #3ecf8e;
    --red: #e85a5a;
    --navy: #1a2a4a;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'Inter', sans-serif;
    background: var(--bg-dark);
    color: var(--white);
    overflow-x: hidden;
  }

  /* ── NAV ── */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    display: flex; align-items: center; justify-content: space-between;
    padding: 18px 48px;
    background: rgba(13,31,38,0.85);
    backdrop-filter: blur(16px);
    border-bottom: 1px solid var(--white-15);
  }
  .nav-brand { display: flex; align-items: center; gap: 10px; }
  .nav-logo {
    width: 32px; height: 32px; border-radius: 50%;
    background: linear-gradient(135deg, var(--teal-bright), var(--teal-dark));
    display: flex; align-items: center; justify-content: center;
    font-size: 14px; font-weight: 800; color: var(--bg-dark);
  }
  .nav-title { font-size: 14px; font-weight: 600; letter-spacing: 0.04em; color: var(--white-70); }
  .nav-links { display: flex; gap: 32px; }
  .nav-links a {
    font-size: 12px; font-weight: 500; letter-spacing: 0.06em;
    text-transform: uppercase; color: var(--white-40);
    text-decoration: none; transition: color 0.2s;
  }
  .nav-links a:hover { color: var(--teal-bright); }

  /* ── SECTIONS ── */
  section { min-height: 100vh; padding: 120px 48px 80px; position: relative; overflow: hidden; }
  section + section { border-top: 1px solid var(--white-15); }

  /* ── GRADIENT BARS (CoreDeck signature element) ── */
  .gradient-bars {
    position: absolute; top: 0; right: 0;
    width: 420px; height: 100%;
    pointer-events: none; overflow: hidden;
  }
  .gradient-bars span {
    position: absolute; top: 0; bottom: 0;
    width: 28px; border-radius: 0 0 14px 14px;
    opacity: 0;
    animation: barRise 1.2s ease forwards;
  }
  .gradient-bars span:nth-child(1) { right: 340px; background: linear-gradient(180deg, var(--teal-bright) 0%, transparent 80%); animation-delay: 0.1s; }
  .gradient-bars span:nth-child(2) { right: 300px; background: linear-gradient(180deg, var(--teal-mid) 0%, transparent 70%); animation-delay: 0.2s; height: 65%; }
  .gradient-bars span:nth-child(3) { right: 260px; background: linear-gradient(180deg, var(--teal-bright) 0%, transparent 90%); animation-delay: 0.3s; height: 80%; }
  .gradient-bars span:nth-child(4) { right: 220px; background: linear-gradient(180deg, #3ecfcf88 0%, transparent 60%); animation-delay: 0.4s; height: 50%; }
  .gradient-bars span:nth-child(5) { right: 180px; background: linear-gradient(180deg, var(--teal-dark) 0%, transparent 85%); animation-delay: 0.5s; height: 90%; }
  .gradient-bars span:nth-child(6) { right: 140px; background: linear-gradient(180deg, var(--teal-bright) 0%, transparent 70%); animation-delay: 0.6s; height: 40%; }
  .gradient-bars span:nth-child(7) { right: 100px; background: linear-gradient(180deg, var(--teal-mid) 0%, transparent 95%); animation-delay: 0.7s; height: 75%; }
  .gradient-bars span:nth-child(8) { right: 60px; background: linear-gradient(180deg, var(--teal-bright) 0%, transparent 65%); animation-delay: 0.8s; height: 55%; }
  .gradient-bars span:nth-child(9) { right: 20px; background: linear-gradient(180deg, #3ecfcfaa 0%, transparent 80%); animation-delay: 0.9s; height: 70%; }

  @keyframes barRise {
    from { opacity: 0; transform: translateY(-30px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* ── HERO ── */
  #hero {
    background: radial-gradient(ellipse 80% 60% at 60% 0%, rgba(62,207,207,0.18) 0%, transparent 70%),
                linear-gradient(160deg, var(--bg-dark) 0%, #0e2530 100%);
    display: flex; flex-direction: column; justify-content: center;
    gap: 0;
  }
  .eyebrow {
    font-size: 11px; font-weight: 600; letter-spacing: 0.14em;
    text-transform: uppercase; color: var(--teal-bright);
    margin-bottom: 20px;
  }
  .hero-title {
    font-family: 'DM Serif Display', serif;
    font-size: clamp(48px, 6vw, 84px);
    line-height: 1.05; font-weight: 400;
    max-width: 700px;
  }
  .hero-title em { font-style: normal; color: var(--teal-bright); }
  .hero-sub {
    font-size: 16px; font-weight: 400; color: var(--white-70);
    max-width: 480px; line-height: 1.7; margin-top: 24px;
  }
  .hero-stats {
    display: flex; gap: 48px; margin-top: 64px;
    flex-wrap: wrap;
  }
  .hero-stat .num {
    font-size: 48px; font-weight: 800; line-height: 1;
    color: var(--teal-bright);
  }
  .hero-stat .lbl {
    font-size: 12px; font-weight: 500; letter-spacing: 0.08em;
    text-transform: uppercase; color: var(--white-40); margin-top: 6px;
  }
  .hero-toc {
    margin-top: 72px;
    display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
    gap: 1px; background: var(--white-15);
    border-radius: 12px; overflow: hidden; max-width: 860px;
  }
  .toc-item {
    background: var(--bg-card); padding: 20px 24px;
    transition: background 0.2s;
  }
  .toc-item:hover { background: var(--bg-card-hover); }
  .toc-num { font-size: 11px; font-weight: 700; color: var(--teal-mid); letter-spacing: 0.1em; }
  .toc-name { font-size: 13px; font-weight: 500; color: var(--white-70); margin-top: 4px; }

  /* ── SECTION LABEL ── */
  .sec-label {
    display: inline-block;
    font-size: 10px; font-weight: 700; letter-spacing: 0.14em;
    text-transform: uppercase; color: var(--bg-dark);
    background: var(--teal-bright);
    padding: 4px 12px; border-radius: 3px;
    margin-bottom: 32px;
  }
  .sec-heading {
    font-family: 'DM Serif Display', serif;
    font-size: clamp(28px, 3.5vw, 46px);
    line-height: 1.1; font-weight: 400;
    max-width: 780px; margin-bottom: 48px;
  }

  /* ── STAT CARDS ── */
  .stat-row {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1px; background: var(--white-15);
    border-radius: 14px; overflow: hidden;
    margin-bottom: 48px;
  }
  .stat-card {
    background: var(--bg-card);
    padding: 28px 24px;
    position: relative;
  }
  .stat-card::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0;
    height: 2px;
  }
  .stat-card.teal::before { background: var(--teal-bright); }
  .stat-card.orange::before { background: var(--orange); }
  .stat-card.green::before { background: var(--green); }
  .stat-card.red::before { background: var(--red); }
  .stat-card.navy::before { background: #4a6fa5; }

  .stat-card .big {
    font-size: 40px; font-weight: 800; line-height: 1; margin-bottom: 8px;
  }
  .stat-card.teal .big { color: var(--teal-bright); }
  .stat-card.orange .big { color: var(--orange); }
  .stat-card.green .big { color: var(--green); }
  .stat-card.red .big { color: var(--red); }
  .stat-card.navy .big { color: #7ba7d4; }

  .stat-card .label { font-size: 12px; font-weight: 600; color: var(--white-70); letter-spacing: 0.05em; }
  .stat-card .sub { font-size: 11px; color: var(--white-40); margin-top: 4px; }
  .star-badge {
    display: inline-block; font-size: 10px; font-weight: 600;
    color: var(--teal-bright); border: 1px solid var(--teal-bright);
    padding: 2px 8px; border-radius: 20px; margin-top: 6px;
  }

  /* ── BULLET CARDS ── */
  .content-grid {
    display: grid; grid-template-columns: 1fr 1fr; gap: 24px;
    align-items: start;
  }
  .bullet-card {
    background: var(--bg-card);
    border: 1px solid var(--white-15);
    border-radius: 12px; padding: 28px;
  }
  .bullet-card h4 {
    font-size: 13px; font-weight: 600; color: var(--teal-bright);
    letter-spacing: 0.06em; text-transform: uppercase;
    margin-bottom: 16px;
  }
  .bullet-card ul { list-style: none; display: flex; flex-direction: column; gap: 12px; }
  .bullet-card li {
    font-size: 14px; line-height: 1.6; color: var(--white-70);
    padding-left: 16px; position: relative;
  }
  .bullet-card li::before {
    content: ''; position: absolute; left: 0; top: 9px;
    width: 5px; height: 5px; border-radius: 50%;
    background: var(--teal-bright);
  }
  strong.highlight { color: var(--white); font-weight: 600; }
  strong.red { color: var(--red); }
  strong.green { color: var(--green); }
  strong.teal { color: var(--teal-bright); }

  /* ── BIG COMPARISON ── */
  .compare-pair {
    display: grid; grid-template-columns: 1fr 1fr; gap: 1px;
    background: var(--white-15); border-radius: 14px; overflow: hidden;
    margin-bottom: 32px;
  }
  .compare-half { background: var(--bg-card); padding: 32px 28px; }
  .compare-half .big2 {
    font-size: 52px; font-weight: 800; line-height: 1;
    color: var(--teal-bright); margin-bottom: 6px;
  }
  .compare-half.churned .big2 { color: var(--red); }
  .compare-half .lbl2 { font-size: 12px; color: var(--white-40); font-weight: 500; letter-spacing: 0.06em; }

  /* ── HYPOTHESIS BLOCKS ── */
  .hyp-table {
    width: 100%; border-collapse: collapse; margin-bottom: 28px;
  }
  .hyp-table td {
    padding: 14px 20px; border-bottom: 1px solid var(--white-15);
    font-size: 13px; color: var(--white-70);
  }
  .hyp-table td:first-child {
    font-size: 11px; font-weight: 600; letter-spacing: 0.08em;
    text-transform: uppercase; color: var(--white-40); width: 140px;
  }
  .verdict {
    display: flex; gap: 24px; margin-bottom: 32px;
  }
  .verdict-box {
    flex: 1; background: var(--bg-card); border: 1px solid var(--white-15);
    border-radius: 10px; padding: 20px 24px;
  }
  .verdict-box .p-val {
    font-size: 36px; font-weight: 800; color: var(--red); margin-bottom: 4px;
  }
  .verdict-box .p-lbl { font-size: 11px; color: var(--white-40); letter-spacing: 0.06em; }
  .verdict-box .reject {
    font-size: 20px; font-weight: 700; color: var(--green);
  }
  .verdict-box .reject-sub { font-size: 11px; color: var(--white-40); margin-top: 2px; }

  /* ── MODEL COMPARISON TABLE ── */
  .model-table { width: 100%; border-collapse: collapse; margin-top: 32px; }
  .model-table th {
    padding: 16px 20px; font-size: 13px; font-weight: 700;
    text-transform: uppercase; letter-spacing: 0.06em;
  }
  .model-table th:first-child { text-align: left; color: var(--white-40); }
  .model-table th.lr-h { background: var(--navy); color: var(--white); border-radius: 8px 8px 0 0; }
  .model-table th.rf-h { background: var(--orange); color: var(--white); border-radius: 8px 8px 0 0; }
  .model-table td {
    padding: 14px 20px; border-bottom: 1px solid var(--white-15);
    font-size: 14px; text-align: center;
  }
  .model-table td:first-child { text-align: left; color: var(--white-70); font-weight: 500; }
  .model-table tr:last-child td { border-bottom: none; }
  .winner-pill {
    display: inline-block; font-size: 10px; font-weight: 700;
    padding: 2px 8px; border-radius: 20px;
    letter-spacing: 0.06em; margin-left: 6px;
  }
  .win-lr { background: rgba(30,50,100,0.5); color: #7ba7d4; border: 1px solid #4a6fa5; }
  .win-rf { background: rgba(232,98,42,0.2); color: var(--orange); border: 1px solid var(--orange); }
  .star-row td:first-child { color: var(--green) !important; font-weight: 700 !important; }

  /* ── FEATURE BAR ── */
  .feat-bar-row { display: flex; flex-direction: column; gap: 20px; margin-top: 32px; }
  .feat-bar {
    display: grid; grid-template-columns: 160px 1fr 50px;
    align-items: center; gap: 16px;
  }
  .feat-bar .name { font-size: 13px; font-weight: 600; color: var(--white-70); text-align: right; }
  .feat-bar .track { background: var(--white-15); border-radius: 4px; height: 8px; overflow: hidden; }
  .feat-bar .fill {
    height: 100%; border-radius: 4px;
    background: linear-gradient(90deg, var(--teal-dark), var(--teal-bright));
    transform-origin: left;
    animation: barGrow 1s ease forwards;
    transform: scaleX(0);
  }
  @keyframes barGrow { to { transform: scaleX(1); } }
  .feat-bar .val { font-size: 13px; font-weight: 700; color: var(--teal-bright); }
  .feat-desc { font-size: 11px; color: var(--white-40); margin-top: 4px; grid-column: 2; }

  /* ── GEOGRAPHY BARS ── */
  .geo-row { display: flex; flex-direction: column; gap: 10px; margin-top: 28px; }
  .geo-bar {
    display: grid; grid-template-columns: 140px 1fr 50px;
    align-items: center; gap: 12px;
  }
  .geo-bar .n { font-size: 12px; font-weight: 500; color: var(--white-70); text-align: right; }
  .geo-bar .track { background: var(--white-15); border-radius: 3px; height: 6px; overflow: hidden; }
  .geo-bar .fill-g {
    height: 100%; border-radius: 3px;
    animation: barGrow 1s ease forwards;
    transform-origin: left; transform: scaleX(0);
  }
  .geo-bar.above .fill-g { background: var(--red); }
  .geo-bar.below .fill-g { background: var(--green); }
  .geo-bar .pct { font-size: 12px; font-weight: 700; }
  .geo-bar.above .pct { color: var(--red); }
  .geo-bar.below .pct { color: var(--green); }

  /* ── RECS ── */
  #recs {
    background: radial-gradient(ellipse 70% 50% at 50% 100%, rgba(62,207,207,0.12) 0%, transparent 70%);
  }
  .rec-list { display: flex; flex-direction: column; gap: 16px; max-width: 860px; }
  .rec-item {
    display: grid; grid-template-columns: 48px 1fr;
    gap: 20px; align-items: start;
    background: var(--bg-card); border: 1px solid var(--white-15);
    border-radius: 12px; padding: 24px 28px;
    transition: background 0.2s, border-color 0.2s;
  }
  .rec-item:hover {
    background: var(--bg-card-hover);
    border-color: rgba(62,207,207,0.3);
  }
  .rec-num {
    width: 40px; height: 40px; border-radius: 50%;
    background: linear-gradient(135deg, var(--teal-bright), var(--teal-dark));
    display: flex; align-items: center; justify-content: center;
    font-size: 16px; font-weight: 800; color: var(--bg-dark);
    flex-shrink: 0;
  }
  .rec-text { font-size: 15px; line-height: 1.6; color: var(--white-70); padding-top: 8px; }
  .rec-text strong { color: var(--white); font-weight: 600; }

  /* ── CONVERGENCE BOXES ── */
  .converge-grid {
    display: grid; grid-template-columns: repeat(3, 1fr); gap: 1px;
    background: var(--white-15); border-radius: 14px; overflow: hidden;
    margin-bottom: 40px;
  }
  .converge-box {
    background: var(--bg-card); padding: 28px;
  }
  .converge-box .src {
    font-size: 10px; font-weight: 700; letter-spacing: 0.1em;
    text-transform: uppercase; margin-bottom: 8px;
  }
  .converge-box:nth-child(1) .src { color: var(--teal-bright); }
  .converge-box:nth-child(2) .src { color: var(--orange); }
  .converge-box:nth-child(3) .src { color: #aaa; }
  .converge-box h4 { font-size: 16px; font-weight: 700; margin-bottom: 16px; }
  .converge-box p { font-size: 13px; color: var(--white-70); line-height: 1.8; }

  /* ── FOOTER ── */
  footer {
    padding: 40px 48px;
    border-top: 1px solid var(--white-15);
    display: flex; justify-content: space-between; align-items: center;
  }
  footer p { font-size: 12px; color: var(--white-40); }

  /* ── SECTION BG VARIANTS ── */
  #data-prep { background: linear-gradient(160deg, var(--bg-dark) 0%, #0e2830 100%); }
  #insights { background: linear-gradient(180deg, #0e2830 0%, var(--bg-dark) 100%); }
  #hypothesis { background: linear-gradient(160deg, var(--bg-dark) 0%, #0f1e2a 100%); }
  #model { background: linear-gradient(180deg, #0f1e2a 0%, var(--bg-dark) 100%); }

  /* ── SCROLL FADE IN ── */
  .reveal { opacity: 0; transform: translateY(24px); transition: opacity 0.6s ease, transform 0.6s ease; }
  .reveal.visible { opacity: 1; transform: translateY(0); }

  @media (max-width: 768px) {
    nav { padding: 16px 20px; }
    .nav-links { display: none; }
    section { padding: 100px 20px 60px; }
    .content-grid, .compare-pair, .converge-grid { grid-template-columns: 1fr; }
    .hero-stats { gap: 28px; }
    .gradient-bars { width: 200px; }
  }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <div class="nav-brand">
    <div class="nav-logo">L</div>
    <span class="nav-title">Luminatech · Churn Analysis</span>
  </div>
  <div class="nav-links">
    <a href="#data-prep">Data</a>
    <a href="#insights">Insights</a>
    <a href="#hypothesis">Tests</a>
    <a href="#model">Model</a>
    <a href="#recs">Recs</a>
  </div>
</nav>

<!-- ══════════ HERO ══════════ -->
<section id="hero">
  <div class="gradient-bars">
    <span></span><span></span><span></span><span></span><span></span>
    <span></span><span></span><span></span><span></span>
  </div>

  <div class="eyebrow">Dataset 2023 – 2024</div>
  <h1 class="hero-title">Customer <em>Churn</em><br>Analysis</h1>
  <p class="hero-sub">A full analytical pipeline — from data preparation through predictive modelling — applied to Luminatech's customer base to understand, predict, and prevent churn.</p>

  <div class="hero-stats">
    <div class="hero-stat"><div class="num">3,070</div><div class="lbl">Customers Analysed</div></div>
    <div class="hero-stat"><div class="num">12.3%</div><div class="lbl">Churn Rate</div></div>
    <div class="hero-stat"><div class="num">−9.2%</div><div class="lbl">Revenue YoY</div></div>
    <div class="hero-stat"><div class="num">0.908</div><div class="lbl">Model ROC-AUC (LR)</div></div>
  </div>

  <div class="hero-toc">
    <div class="toc-item"><div class="toc-num">01</div><div class="toc-name">Data Preparation</div></div>
    <div class="toc-item"><div class="toc-num">02</div><div class="toc-name">Exploratory Insights</div></div>
    <div class="toc-item"><div class="toc-num">03</div><div class="toc-name">Hypothesis Testing</div></div>
    <div class="toc-item"><div class="toc-num">04</div><div class="toc-name">Churn Prediction</div></div>
    <div class="toc-item"><div class="toc-num">05</div><div class="toc-name">Recommendations</div></div>
  </div>
</section>

<!-- ══════════ DATA PREP ══════════ -->
<section id="data-prep">
  <div class="gradient-bars" style="opacity:0.5;">
    <span></span><span></span><span></span><span></span><span></span>
    <span></span><span></span><span></span><span></span>
  </div>

  <div class="reveal">
    <div class="sec-label">Section 01 · Data Preparation</div>
    <h2 class="sec-heading">Building <em style="font-style:normal;color:var(--teal-bright)">churn_df</em></h2>
  </div>

  <div class="stat-row reveal">
    <div class="stat-card teal">
      <div class="big">3,070</div>
      <div class="label">Total Customers</div>
      <div class="sub">2023 cohort analysed</div>
    </div>
    <div class="stat-card red">
      <div class="big">12.3%</div>
      <div class="label">Churn Rate</div>
      <div class="sub"><span class="star-badge">★ Key Stat</span></div>
      <div class="sub" style="margin-top:6px">379 of 3,070 churned</div>
    </div>
    <div class="stat-card orange">
      <div class="big">50</div>
      <div class="label">Avg Recency</div>
      <div class="sub">Ranging 0–361 days</div>
    </div>
    <div class="stat-card green">
      <div class="big">269</div>
      <div class="label">Avg Tenure</div>
      <div class="sub">Engage consistently year-round</div>
    </div>
    <div class="stat-card navy">
      <div class="big">16</div>
      <div class="label">Columns</div>
      <div class="sub">12 numeric · 1 categorical · target</div>
    </div>
  </div>

  <div class="content-grid reveal">
    <div class="bullet-card">
      <h4>How churn_df Is Built</h4>
      <ul>
        <li><strong class="teal">Step 1</strong> — Identify customer cohorts: separate 2023 vs 2024 customers, exclude new 2024-only customers.</li>
        <li><strong class="teal">Step 2</strong> — Aggregate per customer via <code style="font-size:12px;color:var(--teal-bright)">groupby(customer_code).agg()</code> → spend, frequency & engagement features.</li>
        <li><strong class="teal">Step 3</strong> — Derive recency, tenure & margin. Recency = days from last 2023 purchase to year-end.</li>
        <li><strong class="teal">Step 4</strong> — Assign primary district. Most frequent district code per customer mapped to city name.</li>
        <li><strong class="teal">Step 5</strong> — Label the target. <code style="font-size:12px;color:var(--teal-bright)">churned = 1</code> if absent from 2024, else 0. Missing values imputed via median/mode.</li>
      </ul>
    </div>
    <div class="bullet-card">
      <h4>The 16 Columns</h4>
      <ul>
        <li><strong class="highlight">Spend & Volume</strong> — total_spend · total_profit · avg_txn_value · avg_margin · total_quantity</li>
        <li><strong class="highlight">Engagement & Frequency</strong> — n_transactions · n_months_active · n_business_areas · n_distinct_items · n_distinct_salesppl</li>
        <li><strong class="highlight">Recency & Tenure</strong> — recency_days · tenure_days</li>
        <li><strong class="highlight">Geography</strong> — district_name (customer's primary sales district)</li>
        <li><strong class="highlight">Target Variable</strong> — churned (1 = did not return in 2024, 0 = returned)</li>
      </ul>
    </div>
  </div>
</section>

<!-- ══════════ INSIGHTS ══════════ -->
<section id="insights">
  <div class="reveal">
    <div class="sec-label">Section 02 · Exploratory Insights</div>
    <h2 class="sec-heading">5 Data-Driven Findings</h2>
  </div>

  <!-- Insight 1 -->
  <div class="reveal" style="margin-bottom:64px">
    <div style="font-size:11px;font-weight:700;letter-spacing:0.1em;text-transform:uppercase;color:var(--white-40);margin-bottom:16px;">Insight 1 of 5</div>
    <h3 style="font-size:22px;font-weight:700;margin-bottom:28px;">Revenue Declined 9.2% — Customer Loss Is the Driver</h3>
    <div class="compare-pair">
      <div class="compare-half">
        <div class="big2">$84.9M</div>
        <div class="lbl2">2023 Revenue</div>
      </div>
      <div class="compare-half churned">
        <div class="big2">$77.1M</div>
        <div class="lbl2">2024 Revenue (−9.2%)</div>
      </div>
    </div>
    <div class="bullet-card">
      <h4>Key Findings</h4>
      <ul>
        <li>Monthly revenue tracked customer count <strong class="highlight">almost perfectly</strong> across both years — a near-perfect correlation.</li>
        <li>Decline is driven by <strong class="red">losing customers</strong>, not by existing customers spending less.</li>
        <li>A May revenue peak is visible in both years, confirming a <strong class="highlight">seasonal demand cycle</strong>.</li>
        <li>Pre-season promotions could maximise the natural high-demand window before the peak.</li>
      </ul>
    </div>
  </div>

  <!-- Insight 2 -->
  <div class="reveal" style="margin-bottom:64px">
    <div style="font-size:11px;font-weight:700;letter-spacing:0.1em;text-transform:uppercase;color:var(--white-40);margin-bottom:16px;">Insight 2 of 5</div>
    <h3 style="font-size:22px;font-weight:700;margin-bottom:28px;">Recency & Frequency Reveal Two Distinct Customer Clusters</h3>
    <div class="stat-row" style="max-width:700px">
      <div class="stat-card red"><div class="big">47</div><div class="label">Recency Threshold</div><div class="sub">75th percentile (days)</div></div>
      <div class="stat-card orange"><div class="big">86.3%</div><div class="label">Churned Beyond Threshold</div><div class="sub">vs 16.4% of retained</div></div>
      <div class="stat-card teal"><div class="big">332 vs 28</div><div class="label">Avg Transactions</div><div class="sub">Retained vs Churned</div></div>
    </div>
    <div class="bullet-card">
      <h4>Key Findings</h4>
      <ul>
        <li>Retained customers form a <strong class="green">dense cluster</strong> — low recency, high frequency.</li>
        <li>Churned customers spread beyond the <strong class="red">47-day mark</strong> with far fewer transactions.</li>
        <li>Customer inactivity beyond 47 days is an <strong class="teal">actionable churn-risk signal</strong>, enabling earlier intervention and more targeted retention strategies.</li>
      </ul>
    </div>
  </div>

  <!-- Insight 3 -->
  <div class="reveal" style="margin-bottom:64px">
    <div style="font-size:11px;font-weight:700;letter-spacing:0.1em;text-transform:uppercase;color:var(--white-40);margin-bottom:16px;">Insight 3 of 5</div>
    <h3 style="font-size:22px;font-weight:700;margin-bottom:28px;">Churn Is a Behavioural Pattern — Not a Spending Pattern</h3>
    <div style="display:grid;grid-template-columns:1fr 1fr 1fr 1fr;gap:1px;background:var(--white-15);border-radius:14px;overflow:hidden;max-width:900px;margin-bottom:28px;">
      <div class="stat-card green"><div class="big" style="font-size:32px">13 days</div><div class="label">Retained Median Recency</div></div>
      <div class="stat-card red"><div class="big" style="font-size:32px">166 days</div><div class="label">Churned Median Recency</div></div>
      <div class="stat-card green"><div class="big" style="font-size:32px">12 mo</div><div class="label">Retained Median Active</div></div>
      <div class="stat-card red"><div class="big" style="font-size:32px">2 mo</div><div class="label">Churned Median Active</div></div>
    </div>
    <div class="bullet-card">
      <h4>Key Findings</h4>
      <ul>
        <li><strong class="red">Burst-and-exit pattern</strong>: churned customers buy in short windows then disappear entirely.</li>
        <li>Retained customers maintained purchasing over <strong class="green">340 days</strong> vs only 35 days for churned.</li>
        <li>Average transaction value gap is modest ($96 vs $77) — <strong class="highlight">spending is NOT the signal</strong>.</li>
        <li>Monitoring recency and months active is far more valuable than monitoring spend.</li>
      </ul>
    </div>
  </div>

  <!-- Insight 4 -->
  <div class="reveal" style="margin-bottom:64px">
    <div style="font-size:11px;font-weight:700;letter-spacing:0.1em;text-transform:uppercase;color:var(--white-40);margin-bottom:16px;">Insight 4 of 5</div>
    <h3 style="font-size:22px;font-weight:700;margin-bottom:28px;">Churn Risk Is Geographically Concentrated</h3>
    <div class="content-grid">
      <div class="bullet-card">
        <h4>District Findings</h4>
        <ul>
          <li><strong class="red">Adelaide (14.5%)</strong> and <strong class="red">Melbourne (13.1%)</strong> are above the 12.3% national average.</li>
          <li><strong class="green">ACT/Riverina retains 97.5%</strong> of customers — best in the country.</li>
          <li>Sydney & Melbourne represent the largest volume, meaning the most absolute churners.</li>
          <li>Despite Adelaide's highest rate, <strong class="red">Sydney loses ~103 customers</strong> — making it the highest-priority intervention target.</li>
          <li>Investigate ACT/Riverina & Townsville for replicable best practices.</li>
        </ul>
      </div>
      <div>
        <div class="geo-row">
          <div class="geo-bar above"><div class="n">Adelaide (n=283)</div><div class="track"><div class="fill-g" style="width:100%;animation-delay:0.1s"></div></div><div class="pct">14.5%</div></div>
          <div class="geo-bar above"><div class="n">Melbourne (n=662)</div><div class="track"><div class="fill-g" style="width:90%;animation-delay:0.2s"></div></div><div class="pct">13.1%</div></div>
          <div class="geo-bar below"><div class="n">Sydney (n=841)</div><div class="track"><div class="fill-g" style="width:84%;animation-delay:0.3s"></div></div><div class="pct">12.2%</div></div>
          <div class="geo-bar below"><div class="n">Perth (n=319)</div><div class="track"><div class="fill-g" style="width:80%;animation-delay:0.4s"></div></div><div class="pct">11.6%</div></div>
          <div class="geo-bar below"><div class="n">Brisbane (n=553)</div><div class="track"><div class="fill-g" style="width:77%;animation-delay:0.5s"></div></div><div class="pct">11.2%</div></div>
          <div class="geo-bar below"><div class="n">Darwin (n=89)</div><div class="track"><div class="fill-g" style="width:71%;animation-delay:0.6s"></div></div><div class="pct">10.3%</div></div>
          <div class="geo-bar below"><div class="n">Tasmania (n=62)</div><div class="track"><div class="fill-g" style="width:56%;animation-delay:0.7s"></div></div><div class="pct">8.1%</div></div>
          <div class="geo-bar below"><div class="n">Townsville (n=95)</div><div class="track"><div class="fill-g" style="width:36%;animation-delay:0.8s"></div></div><div class="pct">5.3%</div></div>
          <div class="geo-bar below"><div class="n">ACT/Riverina (n=79)</div><div class="track"><div class="fill-g" style="width:17%;animation-delay:0.9s"></div></div><div class="pct">2.5%</div></div>
        </div>
        <div style="margin-top:12px;font-size:11px;color:var(--white-40);">Red = above 12.3% average · Green = below average</div>
      </div>
    </div>
  </div>

  <!-- Insight 5 -->
  <div class="reveal">
    <div style="font-size:11px;font-weight:700;letter-spacing:0.1em;text-transform:uppercase;color:var(--white-40);margin-bottom:16px;">Insight 5 of 5</div>
    <h3 style="font-size:22px;font-weight:700;margin-bottom:28px;">Feature Correlation: What Actually Predicts Churn?</h3>
    <div class="stat-row" style="max-width:600px;margin-bottom:32px">
      <div class="stat-card red"><div class="big">+0.60</div><div class="label">recency_days ↔ churn</div><div class="sub">Strongest positive predictor</div></div>
      <div class="stat-card green"><div class="big">−0.56</div><div class="label">tenure_days ↔ churn</div></div>
      <div class="stat-card green"><div class="big">−0.53</div><div class="label">n_months_active ↔ churn</div></div>
    </div>
    <div class="bullet-card">
      <h4>Correlation Insights</h4>
      <ul>
        <li>Recency is the <strong class="red">strongest positive predictor</strong> of churn (+0.60).</li>
        <li>Tenure and months active are the strongest negative protective factors (−0.56, −0.53).</li>
        <li>Several volume features are nearly perfectly intercorrelated (r = 0.89–1.00) — adding them all adds no predictive value.</li>
        <li><strong class="teal">Monitor engagement frequency and recency</strong>, not revenue, as primary loyalty indicators.</li>
      </ul>
    </div>
  </div>
</section>

<!-- ══════════ HYPOTHESIS ══════════ -->
<section id="hypothesis">
  <div class="gradient-bars" style="opacity:0.4;">
    <span></span><span></span><span></span><span></span><span></span>
    <span></span><span></span><span></span><span></span>
  </div>

  <div class="reveal">
    <div class="sec-label">Section 03 · Hypothesis Testing</div>
    <h2 class="sec-heading">3 Welch's Two-Sample t-Tests · α = 0.05</h2>
  </div>

  <!-- T-Test 1 -->
  <div class="reveal" style="margin-bottom:56px">
    <h3 style="font-size:20px;font-weight:700;margin-bottom:8px;color:var(--white)">3.1 · Did Churned Customers Stop Purchasing Earlier?</h3>
    <p style="font-size:13px;color:var(--white-40);margin-bottom:24px;font-style:italic">Upper-tailed t-test — testing whether churned customers have significantly higher recency days.</p>
    <table class="hyp-table">
      <tr><td>Null H₀</td><td>Recency days are equal or lower for churned customers (μ_churned ≤ μ_retained)</td></tr>
      <tr><td>Alt H₁</td><td>Churned customers have significantly higher recency days (μ_churned > μ_retained)</td></tr>
    </table>
    <div class="verdict">
      <div class="verdict-box"><div class="p-val">p &lt; 0.001</div><div class="p-lbl">p-value (one-tailed)</div></div>
      <div class="verdict-box"><div class="reject">✓ Reject H₀</div><div class="reject-sub">p &lt;&lt; 0.05</div></div>
    </div>
    <div class="bullet-card">
      <h4>Insights</h4>
      <ul>
        <li>Churned customers: <strong class="red">169 days</strong> vs Retained customers: <strong class="green">34 days</strong> — a mean gap of 135 days.</li>
        <li>Customers inactive for <strong class="teal">47+ days have an 86.3% probability of not returning</strong> (P75 recency), a data-derived early warning threshold.</li>
        <li>Implementing a <strong class="highlight">47-day automated inactivity alert</strong> would allow the sales team to proactively intervene before full disengagement.</li>
      </ul>
    </div>
  </div>

  <!-- T-Test 2 -->
  <div class="reveal" style="margin-bottom:56px">
    <h3 style="font-size:20px;font-weight:700;margin-bottom:8px;color:var(--white)">3.2 · Did Churned Customers Purchase Across Fewer Months?</h3>
    <p style="font-size:13px;color:var(--white-40);margin-bottom:24px;font-style:italic">Lower-tailed t-test — testing whether churned customers were active across fewer months.</p>
    <table class="hyp-table">
      <tr><td>Null H₀</td><td>Churned customers have equal or more active months (μ_churned ≥ μ_retained)</td></tr>
      <tr><td>Alt H₁</td><td>Churned customers have significantly fewer active months (μ_churned &lt; μ_retained)</td></tr>
    </table>
    <div class="verdict">
      <div class="verdict-box"><div class="p-val">p &lt;&lt; 0.05</div><div class="p-lbl">p-value (one-tailed)</div></div>
      <div class="verdict-box"><div class="reject">✓ Reject H₀</div><div class="reject-sub">p &lt;&lt; 0.05</div></div>
    </div>
    <div class="bullet-card">
      <h4>Insights</h4>
      <ul>
        <li><strong class="green">Retained: 9.57 months</strong> vs <strong class="red">Churned: 2.86 months</strong> active — a gap of nearly 7 months, confirming burst-and-exit pattern.</li>
        <li>Customers who place a second or third order <strong class="teal">within the first 2 months</strong> are significantly more likely to develop a recurring buying habit.</li>
        <li>Follow-up outreach after the first order with tailored product recommendations or loyalty incentives can encourage early repeat purchases.</li>
      </ul>
    </div>
  </div>

  <!-- T-Test 3 -->
  <div class="reveal">
    <h3 style="font-size:20px;font-weight:700;margin-bottom:8px;color:var(--white)">3.3 · Is Avg Transaction Value Different Between Groups?</h3>
    <p style="font-size:13px;color:var(--white-40);margin-bottom:24px;font-style:italic">Two-tailed t-test — testing whether average transaction value differs between churned and retained.</p>
    <table class="hyp-table">
      <tr><td>Null H₀</td><td>No significant difference in average transaction value (μ_churned = μ_retained)</td></tr>
      <tr><td>Alt H₁</td><td>Significant difference in average transaction value exists (μ_churned ≠ μ_retained)</td></tr>
    </table>
    <div class="verdict">
      <div class="verdict-box"><div class="p-val">p &lt; 0.05</div><div class="p-lbl">p-value (two-tailed)</div></div>
      <div class="verdict-box" style="border-color:var(--orange)"><div class="reject" style="color:var(--orange)">✓ Reject H₀</div><div class="reject-sub">Counterintuitive result</div></div>
    </div>
    <div class="bullet-card">
      <h4>Insights</h4>
      <ul>
        <li>Churned customers had a <strong class="red">higher</strong> average transaction value (<strong class="red">$106</strong> vs <strong class="green">$95</strong>) — proving that high spenders are not necessarily loyal customers.</li>
        <li>Churned customers are <strong class="orange" style="color:var(--orange)">project-driven buyers</strong> who place large orders in a short burst before disappearing entirely.</li>
        <li>Sales teams should proactively engage large infrequent accounts <strong class="teal">during active projects</strong> to secure the next opportunity before the project ends.</li>
      </ul>
    </div>
  </div>
</section>

<!-- ══════════ MODEL ══════════ -->
<section id="model">
  <div class="reveal">
    <div class="sec-label">Section 04 · Churn Prediction</div>
    <h2 class="sec-heading">Logistic Regression vs Random Forest</h2>
    <p style="font-size:14px;color:var(--white-40);margin-bottom:48px;max-width:600px">Binary classification · 3,070 customers · Test set: 921 samples (30% stratified holdout)</p>
  </div>

  <!-- LR Performance -->
  <div class="reveal" style="margin-bottom:48px">
    <h3 style="font-size:18px;font-weight:600;color:var(--white-70);margin-bottom:20px;letter-spacing:0.04em;">4.1 · Logistic Regression</h3>
    <div style="background:var(--navy);border-radius:12px;padding:24px 28px;margin-bottom:1px;display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:16px;">
      <div><span style="font-size:28px;font-weight:800;color:var(--white)">ROC-AUC = 0.908</span></div>
      <div style="font-size:13px;color:var(--white-70);max-width:400px">The model correctly ranks churned customers above retained 90.8% of the time across all decision thresholds.</div>
    </div>
    <div class="stat-row" style="border-radius:0 0 12px 12px;">
      <div class="stat-card teal">
        <div class="big">77.2%</div>
        <div class="label">Recall</div>
        <div class="sub"><span class="star-badge">★ Primary Metric</span></div>
        <div class="sub" style="margin-top:6px">Catches 3 in 4 churners</div>
      </div>
      <div class="stat-card navy">
        <div class="big">43.3%</div>
        <div class="label">Precision</div>
        <div class="sub">43% of flagged are true churners</div>
      </div>
      <div class="stat-card orange">
        <div class="big">55.5%</div>
        <div class="label">F1 Score</div>
        <div class="sub">Balance of Precision & Recall</div>
      </div>
      <div class="stat-card green">
        <div class="big">84.7%</div>
        <div class="label">Accuracy</div>
        <div class="sub">Overall correct predictions</div>
      </div>
    </div>
  </div>

  <!-- RF Performance -->
  <div class="reveal" style="margin-bottom:48px">
    <h3 style="font-size:18px;font-weight:600;color:var(--white-70);margin-bottom:20px;letter-spacing:0.04em;">4.3 · Random Forest</h3>
    <div style="background:rgba(232,98,42,0.2);border-radius:12px;padding:24px 28px;margin-bottom:1px;display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:16px;">
      <div><span style="font-size:28px;font-weight:800;color:var(--white)">ROC-AUC = 0.935</span></div>
      <div style="font-size:13px;color:var(--white-70);max-width:400px">Higher AUC but significantly lower recall — misses 62% of at-risk customers.</div>
    </div>
    <div class="stat-row" style="border-radius:0 0 12px 12px;">
      <div class="stat-card red">
        <div class="big">37.7%</div>
        <div class="label">Recall</div>
        <div class="sub">Lower Recall vs LR · catches only 2 in 5</div>
      </div>
      <div class="stat-card green">
        <div class="big">66.2%</div>
        <div class="label">Precision</div>
        <div class="sub">66% of flagged are true churners</div>
      </div>
      <div class="stat-card orange">
        <div class="big">48.0%</div>
        <div class="label">F1 Score</div>
        <div class="sub">Below LR</div>
      </div>
      <div class="stat-card green">
        <div class="big">89.9%</div>
        <div class="label">Accuracy</div>
        <div class="sub">Misleading due to class imbalance</div>
      </div>
    </div>
  </div>

  <!-- Comparison Table -->
  <div class="reveal" style="margin-bottom:56px">
    <h3 style="font-size:18px;font-weight:600;color:var(--white-70);margin-bottom:20px;">4.4 · Model Comparison — Which to Deploy?</h3>
    <div style="overflow-x:auto;">
      <table class="model-table">
        <thead>
          <tr>
            <th></th>
            <th class="lr-h">Logistic Regression</th>
            <th class="rf-h">Random Forest</th>
            <th style="font-size:11px;color:var(--white-40);font-weight:600;text-transform:uppercase;letter-spacing:0.06em;">Winner</th>
          </tr>
        </thead>
        <tbody>
          <tr><td>Accuracy</td><td>0.847</td><td style="color:var(--green);font-weight:700;">0.899 ←</td><td><span class="winner-pill win-rf">RF wins</span></td></tr>
          <tr><td>Precision</td><td>0.433</td><td style="color:var(--green);font-weight:700;">0.662 ←</td><td><span class="winner-pill win-rf">RF wins</span></td></tr>
          <tr class="star-row"><td>★ Recall</td><td style="color:var(--green);font-weight:700;">0.772 ←</td><td>0.377</td><td><span class="winner-pill win-lr">LR wins</span></td></tr>
          <tr><td>F1 Score</td><td style="color:var(--green);font-weight:700;">0.555 ←</td><td>0.480</td><td><span class="winner-pill win-lr">LR wins</span></td></tr>
          <tr><td>ROC-AUC</td><td>0.908</td><td style="color:var(--green);font-weight:700;">0.935 ←</td><td><span class="winner-pill win-rf">RF wins</span></td></tr>
        </tbody>
      </table>
    </div>
    <div style="margin-top:16px;padding:16px 20px;background:rgba(62,207,207,0.08);border-left:3px solid var(--teal-bright);border-radius:0 8px 8px 0;">
      <span style="font-size:13px;font-weight:600;color:var(--teal-bright)">Priority Metric: </span>
      <span style="font-size:13px;color:var(--white-70)">Recall is the business priority — a missed churner costs more than a false alarm.</span>
    </div>
  </div>

  <!-- Key Predictors -->
  <div class="reveal">
    <h3 style="font-size:18px;font-weight:600;color:var(--white-70);margin-bottom:20px;">4.6 · Key Predictors — Three Independent Sources Converge</h3>
    <div class="converge-grid">
      <div class="converge-box">
        <div class="src">Section 2.5 · Correlation Heatmap</div>
        <h4>Feature Correlations</h4>
        <p>+0.60 recency<br>−0.56 tenure<br>−0.53 months active</p>
      </div>
      <div class="converge-box">
        <div class="src">Section 3 · Hypothesis Tests</div>
        <h4>Statistical Tests</h4>
        <p>p ≈ 0 for recency<br>p ≈ 0 for months active<br>All three H₀ rejected</p>
      </div>
      <div class="converge-box">
        <div class="src">Section 4.3 · RF Feature Importance</div>
        <h4>Feature Importance</h4>
        <p>recency 0.220<br>tenure 0.152<br>months 0.120</p>
      </div>
    </div>
    <div class="feat-bar-row">
      <div style="font-size:12px;font-weight:600;color:var(--teal-bright);letter-spacing:0.08em;text-transform:uppercase;margin-bottom:8px;">All three approaches converge on the same three behavioural signals</div>
      <div>
        <div class="feat-bar">
          <div class="name">recency_days</div>
          <div class="track"><div class="fill" style="width:100%"></div></div>
          <div class="val">0.220</div>
        </div>
        <div style="grid-column:2;font-size:11px;color:var(--white-40);margin-top:4px;margin-left:176px;margin-bottom:16px">Higher value = customer hasn't bought in a long time → higher churn risk</div>
      </div>
      <div>
        <div class="feat-bar">
          <div class="name">tenure_days</div>
          <div class="track"><div class="fill" style="width:69%;animation-delay:0.2s"></div></div>
          <div class="val">0.152</div>
        </div>
        <div style="font-size:11px;color:var(--white-40);margin-top:4px;margin-left:176px;margin-bottom:16px">Higher value = customer has been buying over a longer span → lower churn risk</div>
      </div>
      <div>
        <div class="feat-bar">
          <div class="name">n_months_active</div>
          <div class="track"><div class="fill" style="width:55%;animation-delay:0.4s"></div></div>
          <div class="val">0.120</div>
        </div>
        <div style="font-size:11px;color:var(--white-40);margin-top:4px;margin-left:176px">Higher value = customer purchases across more months → lower churn risk</div>
      </div>
    </div>
  </div>
</section>

<!-- ══════════ RECOMMENDATIONS ══════════ -->
<section id="recs">
  <div class="reveal">
    <div class="sec-label">Section 05 · Summary & Recommendations</div>
    <h2 class="sec-heading">Key Findings & Management Recommendations</h2>
  </div>

  <div class="rec-list reveal">
    <div class="rec-item">
      <div class="rec-num">1</div>
      <div class="rec-text"><strong>Automate a 47-day inactivity alert</strong> → trigger immediate sales team outreach. 86.3% of customers inactive beyond this threshold do not return.</div>
    </div>
    <div class="rec-item">
      <div class="rec-num">2</div>
      <div class="rec-text"><strong>Focus on habit formation</strong> — target a repeat purchase within the first 60 days. Customers active within the first 2 months are significantly more likely to become long-term buyers.</div>
    </div>
    <div class="rec-item">
      <div class="rec-num">3</div>
      <div class="rec-text"><strong>Do not prioritise by spend</strong> — high-value accounts ($106 avg txn) still churn. Monitor recency and engagement frequency as primary loyalty indicators, not revenue.</div>
    </div>
    <div class="rec-item">
      <div class="rec-num">4</div>
      <div class="rec-text"><strong>Geo-targeted retention</strong> — Adelaide, Melbourne, and Sydney need dedicated retention programmes. Investigate ACT/Riverina (2.5% churn) and Townsville (5.3%) for replicable best practices.</div>
    </div>
    <div class="rec-item">
      <div class="rec-num">5</div>
      <div class="rec-text"><strong>Deploy Logistic Regression monthly</strong> with a quarterly retraining cycle. The LR model catches 77.2% of churners vs Random Forest's 37.7% — operationally far more valuable for intervention.</div>
    </div>
  </div>

  <div style="margin-top:64px;padding:32px;background:var(--bg-card);border:1px solid var(--white-15);border-radius:14px;max-width:860px;" class="reveal">
    <div style="font-size:11px;font-weight:700;letter-spacing:0.1em;text-transform:uppercase;color:var(--teal-bright);margin-bottom:12px;">Model Deployment Plan</div>
    <div style="display:flex;gap:8px;flex-wrap:wrap;align-items:center;">
      <span style="font-size:13px;color:var(--white-70)">Monthly scoring pipeline</span>
      <span style="color:var(--white-40)">→</span>
      <span style="font-size:13px;color:var(--white-70)">Flag accounts above risk threshold</span>
      <span style="color:var(--white-40)">→</span>
      <span style="font-size:13px;color:var(--white-70)">Sales team alert</span>
      <span style="color:var(--white-40)">→</span>
      <span style="font-size:13px;color:var(--white-70)">Proactive outreach</span>
      <span style="color:var(--white-40)">→</span>
      <span style="font-size:13px;color:var(--teal-bright);font-weight:600;">Retrain quarterly</span>
    </div>
  </div>
</section>

<footer>
  <p>Luminatech · Customer Churn Analysis 2023–2024</p>
  <p>379 churned · 2,691 retained · 12.3% churn rate</p>
</footer>

<script>
  // Scroll reveal
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.classList.add('visible');
      }
    });
  }, { threshold: 0.1 });

  document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

  // Re-trigger bar animations on scroll into view
  const barObserver = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.querySelectorAll('.fill, .fill-g').forEach(bar => {
          bar.style.animation = 'none';
          bar.offsetHeight; // reflow
          bar.style.animation = '';
        });
      }
    });
  }, { threshold: 0.2 });

  document.querySelectorAll('.feat-bar-row, .geo-row').forEach(el => barObserver.observe(el));
</script>
</body>
</html>
