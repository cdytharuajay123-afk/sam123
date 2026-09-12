<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Field &amp; Frame — Civil Engineering Tools Reference</title>

<!-- Framework: Bootstrap 5 (grid, nav, modal, responsive utilities) -->
<link href="https://cdnjs.cloudflare.com/ajax/libs/bootstrap/5.3.3/css/bootstrap.min.css" rel="stylesheet">

<!-- Type -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=IBM+Plex+Sans:wght@400;500;600&family=IBM+Plex+Mono:wght@400;500;600&display=swap" rel="stylesheet">

<style>
  :root{
    --ink:#0F1E2E;
    --ink-soft:#16283A;
    --paper:#E7E1CF;
    --paper-dim:#DCD4BC;
    --line:#5A8FB8;
    --line-dim:rgba(90,143,184,0.35);
    --accent:#E0602A;
    --steel:#8CA0AC;
    --steel-dark:#3E5061;
    --good:#4E9A6B;
    --bad:#C2483A;
    --radius:2px;
  }

  *{box-sizing:border-box;}
  html{scroll-behavior:smooth;}
  body{
    background:var(--paper);
    color:var(--ink);
    font-family:'IBM Plex Sans', sans-serif;
    margin:0;
    -webkit-font-smoothing:antialiased;
  }
  @media (prefers-reduced-motion: reduce){
    *{animation-duration:0.001ms !important; animation-iteration-count:1 !important; transition-duration:0.001ms !important; scroll-behavior:auto !important;}
  }
  h1,h2,h3,.font-display{ font-family:'Space Grotesk', sans-serif; letter-spacing:-0.01em; margin:0; }
  .mono{ font-family:'IBM Plex Mono', monospace; }
  a{color:inherit;}
  :focus-visible{ outline:2px solid var(--accent); outline-offset:3px; }

  /* ---------- Navbar ---------- */
  .site-nav{ background:var(--ink); border-bottom:1px solid var(--steel-dark); }
  .site-nav .navbar-brand{
    font-family:'Space Grotesk', sans-serif; font-weight:600; font-size:1.05rem;
    color:var(--paper); display:flex; align-items:center; gap:.55rem;
  }
  .site-nav .navbar-brand .mark{
    width:26px;height:26px; border:1.5px solid var(--accent);
    display:flex;align-items:center;justify-content:center; color:var(--accent);
    font-family:'IBM Plex Mono',monospace; font-size:.72rem; transform:rotate(45deg);
  }
  .site-nav .navbar-brand .mark span{transform:rotate(-45deg);}
  .site-nav .nav-link{
    color:var(--steel) !important; font-family:'IBM Plex Mono', monospace;
    font-size:.82rem; letter-spacing:.02em; padding:.5rem .9rem !important;
  }
  .site-nav .nav-link:hover, .site-nav .nav-link.active{ color:var(--paper) !important; }
  .navbar-toggler{ border-color:var(--steel-dark) !important; padding:.3rem .5rem; }
  .navbar-toggler:focus{box-shadow:0 0 0 .15rem var(--line-dim);}
  .navbar-toggler-icon{ background-image:none !important; position:relative; width:20px;height:16px; }
  .navbar-toggler-icon::before, .navbar-toggler-icon::after{
    content:""; position:absolute; left:0; right:0; height:2px; background:var(--paper);
  }
  .navbar-toggler-icon::before{top:1px;}
  .navbar-toggler-icon::after{bottom:1px;}
  .navbar-toggler-icon{border-top:2px solid var(--paper); margin-top:6px;}

  /* ---------- Hero ---------- */
  .hero{ position:relative; background:var(--ink); color:var(--paper); overflow:hidden; padding:5.5rem 0 4.5rem; }
  .hero-grid{ position:absolute; inset:0; opacity:.55; }
  .hero-grid line{ stroke:var(--line); stroke-width:1; opacity:0; animation:draw-line 1.6s ease forwards; }
  @keyframes draw-line{ from{ stroke-dashoffset:1; opacity:0; } to{ stroke-dashoffset:0; opacity:1; } }
  .hero-inner{position:relative; z-index:2;}
  .hero-kicker{
    font-family:'IBM Plex Mono', monospace; font-size:.8rem; color:var(--line);
    margin-bottom:1.1rem; display:flex; align-items:center; gap:.6rem;
  }
  .hero-kicker::before{ content:""; width:26px; height:1px; background:var(--line); display:inline-block; }
  .hero h1{ font-size:clamp(2.1rem, 5vw, 3.6rem); line-height:1.05; font-weight:600; max-width:16ch; }
  .hero h1 em{ font-style:normal; color:var(--accent); }
  .hero p.lede{ max-width:54ch; color:var(--steel); font-size:1.05rem; line-height:1.65; margin-top:1.4rem; }
  .hero-stats{ display:flex; flex-wrap:wrap; gap:2.2rem; margin-top:2.6rem; padding-top:1.8rem; border-top:1px solid var(--steel-dark); }
  .hero-stat b{ display:block; font-family:'Space Grotesk', sans-serif; font-size:1.7rem; color:var(--paper); }
  .hero-stat span{ font-family:'IBM Plex Mono', monospace; font-size:.72rem; color:var(--steel); }

  /* ---------- Filter bar ---------- */
  .filter-bar{ position:sticky; top:0; z-index:40; background:var(--paper); border-bottom:1px solid var(--steel-dark); padding:.9rem 0; }
  .filter-scroll{ display:flex; gap:.5rem; overflow-x:auto; scrollbar-width:none; padding-bottom:2px; }
  .filter-scroll::-webkit-scrollbar{display:none;}
  .filter-btn{
    flex:0 0 auto; background:transparent; border:1px solid var(--steel-dark); color:var(--ink);
    font-family:'IBM Plex Mono', monospace; font-size:.76rem; padding:.45rem .9rem; border-radius:var(--radius);
    cursor:pointer; white-space:nowrap; transition:background .15s ease, color .15s ease, border-color .15s ease;
  }
  .filter-btn:hover{border-color:var(--accent);}
  .filter-btn.active{ background:var(--ink); color:var(--paper); border-color:var(--ink); }
  .filter-btn .count{ color:var(--steel); margin-left:.35rem; }
  .filter-btn.active .count{color:var(--steel);}

  /* ---------- Section headers ---------- */
  .section-pad{padding:3.2rem 0;}
  .section-head{ display:flex; align-items:baseline; justify-content:space-between; gap:1rem; margin-bottom:1.8rem; flex-wrap:wrap; }
  .section-head h2{ font-size:1.5rem; }
  .section-head .idx{ font-family:'IBM Plex Mono', monospace; font-size:.78rem; color:var(--steel-dark); }
  .section-head .hint{ font-family:'IBM Plex Mono', monospace; font-size:.72rem; color:var(--steel-dark); }

  /* ---------- Tool card ---------- */
  .tool-card{
    position:relative; background:var(--ink); color:var(--paper);
    border:1px solid var(--steel-dark); border-radius:var(--radius);
    padding:1.3rem 1.3rem 1.1rem; height:100%; width:100%; text-align:left;
    display:flex; flex-direction:column; cursor:pointer;
    transition:border-color .15s ease, transform .15s ease;
  }
  .tool-card:hover, .tool-card:focus-visible{ border-color:var(--accent); transform:translateY(-2px); }
  .tool-card::before, .tool-card::after{
    content:""; position:absolute; width:9px; height:9px;
    border-top:1.5px solid var(--accent); border-left:1.5px solid var(--accent); top:-1px; left:-1px;
  }
  .tool-card::after{
    top:auto; left:auto; bottom:-1px; right:-1px; border-top:none; border-left:none;
    border-bottom:1.5px solid var(--accent); border-right:1.5px solid var(--accent);
  }
  .tool-card .icon{ width:42px; height:42px; margin-bottom:1rem; color:var(--line); }
  .tool-card .icon svg{width:100%; height:100%;}
  .tool-card .tag{ font-family:'IBM Plex Mono', monospace; font-size:.66rem; color:var(--line); text-transform:lowercase; margin-bottom:.5rem; }
  .tool-card h3{ font-size:1.08rem; font-weight:600; margin-bottom:.5rem; }
  .tool-card p{ font-size:.87rem; color:var(--steel); line-height:1.55; margin-bottom:1rem; flex-grow:1; }
  .tool-card .spec{
    font-family:'IBM Plex Mono', monospace; font-size:.72rem; color:var(--paper);
    border-top:1px dashed var(--steel-dark); padding-top:.65rem; display:flex; justify-content:space-between; gap:.5rem;
  }
  .tool-card .spec b{color:var(--accent); font-weight:500;}
  .tool-card .run-cta{
    margin-top:.7rem; font-family:'IBM Plex Mono', monospace; font-size:.68rem;
    color:var(--accent); display:flex; align-items:center; gap:.35rem;
  }
  .tool-card.hidden{display:none;}

  /* ---------- Process strip ---------- */
  .process-strip{ background:var(--paper-dim); border-top:1px solid var(--steel-dark); border-bottom:1px solid var(--steel-dark); }
  .process-step{ padding:2rem 1.2rem; border-right:1px solid var(--steel-dark); height:100%; }
  .process-step:last-child{border-right:none;}
  .process-step .num{ font-family:'IBM Plex Mono', monospace; font-size:.75rem; color:var(--accent); margin-bottom:.6rem; }
  .process-step h3{font-size:1rem; margin-bottom:.5rem;}
  .process-step p{font-size:.85rem; color:var(--steel-dark); line-height:1.5; margin:0;}
  @media (max-width: 767px){ .process-step{border-right:none; border-bottom:1px solid var(--steel-dark);} }

  /* ---------- Footer ---------- */
  footer{ background:var(--ink); color:var(--steel); padding:2.2rem 0; font-size:.82rem; }
  footer .mono{font-size:.75rem;}
  footer a.foot-link{ color:var(--paper); text-decoration:none; border-bottom:1px solid var(--steel-dark); }
  footer a.foot-link:hover{border-color:var(--accent);}

  /* ---------- Calculator modal ---------- */
  .modal-content.calc-modal{
    background:var(--paper); border-radius:var(--radius); border:1px solid var(--steel-dark);
  }
  .calc-modal .modal-header{
    background:var(--ink); color:var(--paper); border-bottom:1px solid var(--steel-dark); border-radius:0;
    align-items:flex-start;
  }
  .calc-modal .modal-header .tag{ font-family:'IBM Plex Mono', monospace; font-size:.68rem; color:var(--line); margin-bottom:.35rem; display:block; }
  .calc-modal .modal-title{ font-family:'Space Grotesk', sans-serif; font-size:1.2rem; }
  .calc-modal .btn-close{ filter:invert(1) grayscale(1) brightness(2); }
  .calc-desc{ font-size:.88rem; color:var(--steel-dark); line-height:1.55; margin-bottom:1.3rem; }
  .calc-form label{
    font-family:'IBM Plex Mono', monospace; font-size:.72rem; color:var(--ink);
    display:flex; justify-content:space-between; margin-bottom:.3rem;
  }
  .calc-form label .unit{color:var(--steel-dark);}
  .calc-form .form-control, .calc-form .form-select{
    border-radius:var(--radius); border:1px solid var(--steel-dark); font-family:'IBM Plex Mono', monospace;
    font-size:.85rem; background:#fff;
  }
  .calc-form .form-control:focus, .calc-form .form-select:focus{
    border-color:var(--accent); box-shadow:0 0 0 .15rem var(--line-dim);
  }
  .calc-field{margin-bottom:1rem;}
  .calc-results{
    background:var(--ink); color:var(--paper); border-radius:var(--radius);
    padding:1.1rem 1.2rem; margin-top:.5rem;
  }
  .calc-results .row-line{
    display:flex; justify-content:space-between; gap:1rem; padding:.4rem 0;
    border-bottom:1px dashed var(--steel-dark); font-family:'IBM Plex Mono', monospace; font-size:.85rem;
  }
  .calc-results .row-line:last-child{border-bottom:none;}
  .calc-results .row-line b{color:var(--accent); font-weight:500; text-align:right;}
  .calc-flag{
    display:inline-block; margin-top:.7rem; font-family:'IBM Plex Mono', monospace; font-size:.72rem;
    padding:.3rem .6rem; border-radius:var(--radius);
  }
  .calc-flag.pass{background:rgba(78,154,107,.18); color:var(--good); border:1px solid var(--good);}
  .calc-flag.fail{background:rgba(194,72,58,.18); color:var(--bad); border:1px solid var(--bad);}
  .calc-note{ font-size:.74rem; color:var(--steel-dark); margin-top:.9rem; line-height:1.5; }
</style>
</head>
<body>

<!-- ===== NAV ===== -->
<nav class="navbar navbar-expand-lg site-nav sticky-top">
  <div class="container">
    <a class="navbar-brand" href="#top">
      <span class="mark"><span>CE</span></span>
      Field &amp; Frame
    </a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navMenu" aria-controls="navMenu" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navMenu">
      <ul class="navbar-nav ms-auto">
        <li class="nav-item"><a class="nav-link" href="#toolkit">toolkit</a></li>
        <li class="nav-item"><a class="nav-link" href="#process">process</a></li>
        <li class="nav-item"><a class="nav-link" href="#about">about</a></li>
      </ul>
    </div>
  </div>
</nav>

<!-- ===== HERO ===== -->
<header class="hero" id="top">
  <svg class="hero-grid" preserveAspectRatio="none" viewBox="0 0 1000 400" aria-hidden="true">
    <line x1="80" y1="0" x2="80" y2="400" pathLength="1" stroke-dasharray="1" style="animation-delay:.05s"/>
    <line x1="220" y1="0" x2="220" y2="400" pathLength="1" stroke-dasharray="1" style="animation-delay:.15s"/>
    <line x1="360" y1="0" x2="360" y2="400" pathLength="1" stroke-dasharray="1" style="animation-delay:.25s"/>
    <line x1="640" y1="0" x2="640" y2="400" pathLength="1" stroke-dasharray="1" style="animation-delay:.35s"/>
    <line x1="780" y1="0" x2="780" y2="400" pathLength="1" stroke-dasharray="1" style="animation-delay:.45s"/>
    <line x1="920" y1="0" x2="920" y2="400" pathLength="1" stroke-dasharray="1" style="animation-delay:.55s"/>
    <line x1="0" y1="90" x2="1000" y2="90" pathLength="1" stroke-dasharray="1" style="animation-delay:.1s"/>
    <line x1="0" y1="230" x2="1000" y2="230" pathLength="1" stroke-dasharray="1" style="animation-delay:.3s"/>
    <line x1="0" y1="340" x2="1000" y2="340" pathLength="1" stroke-dasharray="1" style="animation-delay:.5s"/>
  </svg>
  <div class="container hero-inner">
    <div class="row">
      <div class="col-lg-9">
        <div class="hero-kicker">SITE REFERENCE — HOUSES · BRIDGES · ROADS</div>
        <h1>The instruments that turn <em>drawings</em> into structures.</h1>
        <p class="lede">A field reference for the equipment civil engineers and crews rely on. Every tool below opens a small working calculator based on how it's actually used on site — not just a description.</p>
        <div class="hero-stats">
          <div class="hero-stat"><b>24</b><span>TOOLS, EACH WITH A LIVE CALCULATOR</span></div>
          <div class="hero-stat"><b>06</b><span>DISCIPLINES</span></div>
          <div class="hero-stat"><b>02</b><span>STRUCTURE TYPES — HOUSES / BRIDGES</span></div>
        </div>
      </div>
    </div>
  </div>
</header>

<!-- ===== FILTER BAR ===== -->
<div class="filter-bar" id="toolkit">
  <div class="container">
    <div class="filter-scroll" id="filterBar" role="tablist" aria-label="Filter tools by discipline"></div>
  </div>
</div>

<!-- ===== TOOL GRID ===== -->
<div class="container section-pad">
  <div class="section-head">
    <h2>The toolkit</h2>
    <span class="hint">click a card to run its calculator</span>
    <span class="idx mono" id="resultCount">24 / 24 shown</span>
  </div>
  <div class="row g-3" id="toolGrid"></div>
</div>

<!-- ===== PROCESS STRIP ===== -->
<section class="process-strip" id="process">
  <div class="container">
    <div class="row g-0">
      <div class="col-md-3"><div class="process-step"><div class="num mono">01</div><h3>Survey the site</h3><p>Establish control points, elevations, and boundaries before anything is dug or poured.</p></div></div>
      <div class="col-md-3"><div class="process-step"><div class="num mono">02</div><h3>Move &amp; prepare earth</h3><p>Excavate, grade, and compact the ground so foundations and footings sit on stable soil.</p></div></div>
      <div class="col-md-3"><div class="process-step"><div class="num mono">03</div><h3>Build the structure</h3><p>Pour concrete, place reinforcement, and erect steel or timber framing to plan.</p></div></div>
      <div class="col-md-3"><div class="process-step"><div class="num mono">04</div><h3>Lift, join &amp; verify</h3><p>Hoist heavy members into place, join them, then test that the finished work meets spec.</p></div></div>
    </div>
  </div>
</section>

<!-- ===== ABOUT / FOOTER ===== -->
<footer id="about">
  <div class="container">
    <div class="row">
      <div class="col-md-7">
        <p class="mono" style="color:var(--paper); margin-bottom:.6rem;">FIELD &amp; FRAME</p>
        <p>A reference page for civil engineering tools and equipment used across residential, bridge, and general infrastructure work. Built with HTML, CSS, vanilla JavaScript, and Bootstrap. Each tool's calculator uses standard, simplified rules of thumb for illustration — verify against project specifications and a licensed engineer before using any figure for real design or construction decisions.</p>
      </div>
      <div class="col-md-5">
        <p class="mono">Sections</p>
        <p><a class="foot-link" href="#top">Top</a> &nbsp;·&nbsp; <a class="foot-link" href="#toolkit">Toolkit</a> &nbsp;·&nbsp; <a class="foot-link" href="#process">Build process</a></p>
      </div>
    </div>
  </div>
</footer>

<!-- ===== SHARED CALCULATOR MODAL ===== -->
<div class="modal fade" id="toolModal" tabindex="-1" aria-labelledby="toolModalLabel" aria-hidden="true">
  <div class="modal-dialog modal-dialog-centered modal-dialog-scrollable">
    <div class="modal-content calc-modal">
      <div class="modal-header">
        <div>
          <span class="tag mono" id="modalTag"></span>
          <h2 class="modal-title" id="toolModalLabel"></h2>
        </div>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        <p class="calc-desc" id="modalDesc"></p>
        <form class="calc-form" id="calcForm"></form>
        <div class="calc-results" id="calcResults"></div>
        <p class="calc-note" id="modalNote"></p>
      </div>
    </div>
  </div>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/bootstrap/5.3.3/js/bootstrap.bundle.min.js"></script>
<script>
/* ---------------------------------------------------
   ICONS
--------------------------------------------------- */
const ICONS = {
  survey: `<svg viewBox="0 0 48 48" fill="none" stroke="currentColor" stroke-width="1.6"><path d="M24 6l14 24H10L24 6z"/><circle cx="24" cy="30" r="2.4" fill="currentColor" stroke="none"/><path d="M6 42h36"/></svg>`,
  earth: `<svg viewBox="0 0 48 48" fill="none" stroke="currentColor" stroke-width="1.6"><path d="M6 34h36"/><path d="M10 34l4-14h8l3 6h6l4-8h5"/><circle cx="14" cy="38" r="3"/><circle cx="34" cy="38" r="3"/></svg>`,
  concrete: `<svg viewBox="0 0 48 48" fill="none" stroke="currentColor" stroke-width="1.6"><rect x="8" y="8" width="32" height="32"/><path d="M8 20h32M8 30h32M18 8v32M30 8v32"/></svg>`,
  steel: `<svg viewBox="0 0 48 48" fill="none" stroke="currentColor" stroke-width="1.6"><path d="M8 40V16l16-8 16 8v24"/><path d="M8 24h32M8 32h32"/></svg>`,
  lift: `<svg viewBox="0 0 48 48" fill="none" stroke="currentColor" stroke-width="1.6"><path d="M10 40V10h4l14 10V10h4"/><path d="M10 10l-4-4M32 20l6-6"/><path d="M32 20v20"/><path d="M24 40h16"/></svg>`,
  test: `<svg viewBox="0 0 48 48" fill="none" stroke="currentColor" stroke-width="1.6"><circle cx="21" cy="21" r="12"/><path d="M30 30l10 10"/><path d="M21 15v6l4 4"/></svg>`
};

/* ---------------------------------------------------
   TOOL DATA + CALCULATORS
   Each tool has a `calc` object:
     inputs: [{id,label,unit,type:'number'|'select',default,step,options}]
     run(v): returns {rows:[{label,value}], flag:'pass'|'fail'|null, note}
--------------------------------------------------- */
const TOOLS = [

  // ---------------- SURVEYING ----------------
  {cat:'survey', label:'Surveying', name:'Total Station', spec:'Accuracy', val:'±2 mm + 2ppm',
    desc:'Combines an electronic theodolite with distance measurement to fix angles and coordinates for site layout.',
    calc:{
      inputs:[
        {id:'n0', label:'Occupied point — Northing', unit:'m', default:1000},
        {id:'e0', label:'Occupied point — Easting', unit:'m', default:1000},
        {id:'brg', label:'Horizontal bearing (0°=N, clockwise)', unit:'deg', default:45},
        {id:'sd', label:'Slope distance measured', unit:'m', default:30},
        {id:'va', label:'Vertical angle (+ up / − down)', unit:'deg', default:5}
      ],
      run(v){
        const rad = d => d*Math.PI/180;
        const hd = v.sd*Math.cos(rad(v.va));
        const dN = hd*Math.cos(rad(v.brg));
        const dE = hd*Math.sin(rad(v.brg));
        const dz = v.sd*Math.sin(rad(v.va));
        return {rows:[
          {label:'Horizontal distance', value:hd.toFixed(3)+' m'},
          {label:'New Northing', value:(v.n0+dN).toFixed(3)+' m'},
          {label:'New Easting', value:(v.e0+dE).toFixed(3)+' m'},
          {label:'Elevation change', value:(dz>=0?'+':'')+dz.toFixed(3)+' m'}
        ]};
      }
    }},
  {cat:'survey', label:'Surveying', name:'GNSS Receiver', spec:'Fix time', val:'< 10 sec',
    desc:'Reads satellite signals to pin down site coordinates and elevation across large or remote sites.',
    calc:{
      inputs:[
        {id:'lat', label:'Latitude', unit:'decimal deg', default:27.7172},
        {id:'lon', label:'Longitude', unit:'decimal deg', default:85.3240}
      ],
      run(v){
        const zone = Math.floor((v.lon+180)/6)+1;
        const hemi = v.lat>=0 ? 'Northern' : 'Southern';
        return {rows:[
          {label:'UTM zone', value:zone},
          {label:'Hemisphere', value:hemi},
          {label:'Approx. band', value:v.lat>=0?'N':'S'}
        ], note:'UTM zone = floor((longitude + 180) ÷ 6) + 1 — a quick way field crews translate GNSS fixes into a projected grid.'};
      }
    }},
  {cat:'survey', label:'Surveying', name:'Rotary Laser Level', spec:'Range', val:'300 m diam.',
    desc:'Projects a level plane around a site so crews can set consistent height references for foundations and slabs.',
    calc:{
      inputs:[
        {id:'be', label:'Known benchmark elevation', unit:'m', default:100.000},
        {id:'bs', label:'Backsight reading (on benchmark)', unit:'m', default:1.250},
        {id:'fs', label:'Foresight reading (on target point)', unit:'m', default:0.870}
      ],
      run(v){
        const hi = v.be + v.bs;
        const target = hi - v.fs;
        return {rows:[
          {label:'Height of instrument (HI)', value:hi.toFixed(3)+' m'},
          {label:'Target point elevation', value:target.toFixed(3)+' m'},
          {label:'Rise from benchmark', value:(target-v.be).toFixed(3)+' m'}
        ]};
      }
    }},
  {cat:'survey', label:'Surveying', name:"Builder's Level & Staff", spec:'Read to', val:'1 mm',
    desc:'A simple optical level and graduated staff used to check relative heights between two points.',
    calc:{
      inputs:[
        {id:'ra', label:'Staff reading at point A', unit:'m', default:1.680},
        {id:'rb', label:'Staff reading at point B', unit:'m', default:1.220}
      ],
      run(v){
        const diff = v.ra - v.rb;
        const type = diff>0 ? 'Rise (B is higher than A)' : diff<0 ? 'Fall (B is lower than A)' : 'Level (A and B match)';
        return {rows:[
          {label:'Reading difference', value:Math.abs(diff).toFixed(3)+' m'},
          {label:'Result', value:type}
        ]};
      }
    }},

  // ---------------- EARTHMOVING ----------------
  {cat:'earth', label:'Earthmoving', name:'Hydraulic Excavator', spec:'Dig depth', val:'up to 6 m',
    desc:'Digs foundations, trenches, and basements, and loads spoil onto trucks.',
    calc:{
      inputs:[
        {id:'bucket', label:'Bucket capacity', unit:'m³', default:1.0},
        {id:'fill', label:'Bucket fill factor', unit:'0–1', default:0.85, step:0.05},
        {id:'cycle', label:'Cycle time', unit:'sec', default:22},
        {id:'vol', label:'Total volume to excavate', unit:'m³', default:250}
      ],
      run(v){
        const cyclesPerHr = 3600/v.cycle;
        const m3PerHr = v.bucket*v.fill*cyclesPerHr;
        const hours = v.vol/m3PerHr;
        return {rows:[
          {label:'Output rate', value:m3PerHr.toFixed(1)+' m³/hr'},
          {label:'Estimated time', value:hours.toFixed(1)+' hours'}
        ], note:'Output rate = bucket capacity × fill factor × (3600 ÷ cycle time). Excludes swing angle, soil class, and operator efficiency losses.'};
      }
    }},
  {cat:'earth', label:'Earthmoving', name:'Bulldozer', spec:'Blade width', val:'3–4.5 m',
    desc:'Pushes and grades large volumes of soil to shape a site before construction begins.',
    calc:{
      inputs:[
        {id:'w', label:'Blade width', unit:'m', default:3.5},
        {id:'h', label:'Blade height', unit:'m', default:1.1},
        {id:'vol', label:'Total volume to move', unit:'m³', default:400}
      ],
      run(v){
        const capacity = 0.5*v.w*v.h*v.h;
        const passes = Math.ceil(v.vol/capacity);
        return {rows:[
          {label:'Estimated capacity per pass', value:capacity.toFixed(2)+' m³'},
          {label:'Passes needed', value:passes}
        ], note:'Rule-of-thumb heaped blade capacity ≈ 0.5 × width × height². Real output also depends on push distance and material.'};
      }
    }},
  {cat:'earth', label:'Earthmoving', name:'Backhoe Loader', spec:'Reach', val:'~5.5 m',
    desc:'A dual-purpose machine that digs with its rear arm and loads or clears with its front bucket.',
    calc:{
      inputs:[
        {id:'bucket', label:'Loader bucket capacity', unit:'m³', default:1.0},
        {id:'cycle', label:'Loading cycle time', unit:'sec', default:25},
        {id:'truck', label:'Truck bed capacity', unit:'m³', default:10}
      ],
      run(v){
        const buckets = Math.ceil(v.truck/v.bucket);
        const time = (buckets*v.cycle)/60;
        return {rows:[
          {label:'Bucket loads needed', value:buckets},
          {label:'Time to fill one truck', value:time.toFixed(1)+' min'}
        ]};
      }
    }},
  {cat:'earth', label:'Earthmoving', name:'Vibratory Roller', spec:'Compaction force', val:'~13 t',
    desc:'Compacts soil, sub-base, or asphalt layers so they can bear structural loads.',
    calc:{
      inputs:[
        {id:'width', label:'Drum width', unit:'m', default:1.7},
        {id:'speed', label:'Operating speed', unit:'km/h', default:4},
        {id:'passes', label:'Passes required', unit:'count', default:6},
        {id:'area', label:'Area to compact', unit:'m²', default:1000}
      ],
      run(v){
        const coverageRate = v.width*(v.speed*1000/60)*0.9; // m²/min, 10% overlap
        const totalMin = (v.area*v.passes)/coverageRate;
        return {rows:[
          {label:'Coverage rate (1 pass)', value:coverageRate.toFixed(0)+' m²/min'},
          {label:'Total time for all passes', value:(totalMin/60).toFixed(1)+' hours'}
        ], note:'Assumes 10% overlap between adjacent passes; real compaction passes required depend on soil type and lift thickness.'};
      }
    }},

  // ---------------- CONCRETE ----------------
  {cat:'concrete', label:'Concrete', name:'Concrete Mixer Truck', spec:'Drum capacity', val:'6–9 m³',
    desc:'Mixes and transports ready-mix concrete to the pour site while keeping it workable.',
    calc:{
      inputs:[
        {id:'vol', label:'Wet concrete volume needed', unit:'m³', default:5},
        {id:'c', label:'Mix ratio — cement parts', unit:'part', default:1},
        {id:'s', label:'Mix ratio — sand parts', unit:'part', default:2},
        {id:'a', label:'Mix ratio — aggregate parts', unit:'part', default:4}
      ],
      run(v){
        const dryVol = v.vol*1.54; // bulking + voids allowance
        const totalParts = v.c+v.s+v.a;
        const cementVol = dryVol*(v.c/totalParts);
        const sandVol = dryVol*(v.s/totalParts);
        const aggVol = dryVol*(v.a/totalParts);
        const bags = cementVol/0.0347; // ~0.0347 m³ per 50kg bag
        return {rows:[
          {label:'Dry volume (× 1.54)', value:dryVol.toFixed(2)+' m³'},
          {label:'Cement volume', value:cementVol.toFixed(2)+' m³ ('+bags.toFixed(0)+' bags)'},
          {label:'Sand volume', value:sandVol.toFixed(2)+' m³'},
          {label:'Aggregate volume', value:aggVol.toFixed(2)+' m³'}
        ], note:'Standard field estimate: dry volume = wet volume × 1.54 to account for voids and bulking, split by mix ratio. 1 bag cement ≈ 0.0347 m³.'};
      }
    }},
  {cat:'concrete', label:'Concrete', name:'Poker Vibrator', spec:'Frequency', val:'~12,000 vpm',
    desc:'Vibrates freshly poured concrete to release trapped air and settle it fully around reinforcement.',
    calc:{
      inputs:[
        {id:'radius', label:'Radius of action', unit:'mm', default:300},
        {id:'area', label:'Slab area to vibrate', unit:'m²', default:40},
        {id:'time', label:'Vibration time per insertion', unit:'sec', default:12}
      ],
      run(v){
        const rM = v.radius/1000;
        const perPoint = Math.PI*rM*rM;
        const points = Math.ceil(v.area/perPoint);
        const totalMin = (points*v.time)/60;
        return {rows:[
          {label:'Coverage per insertion', value:perPoint.toFixed(2)+' m²'},
          {label:'Insertion points needed', value:points},
          {label:'Total vibration time', value:totalMin.toFixed(1)+' min'}
        ]};
      }
    }},
  {cat:'concrete', label:'Concrete', name:'Rebar Cutter & Bender', spec:'Bar capacity', val:'up to 40 mm',
    desc:'Cuts and bends steel reinforcement bars to the shapes called for in structural drawings.',
    calc:{
      inputs:[
        {id:'a', label:'Leg A length', unit:'mm', default:600},
        {id:'b', label:'Leg B length', unit:'mm', default:400},
        {id:'d', label:'Bar diameter', unit:'mm', default:12}
      ],
      run(v){
        const cutLength = v.a + v.b - 2*v.d;
        return {rows:[
          {label:'Cutting length (one 90° bend)', value:cutLength.toFixed(0)+' mm'}
        ], note:'Common field rule for a single 90° bend: cutting length = leg A + leg B − 2 × bar diameter. Check against your rebar detailing standard for exact deductions.'};
      }
    }},
  {cat:'concrete', label:'Concrete', name:'Screed & Float', spec:'Pass width', val:'2–4 m',
    desc:'Levels and finishes a concrete surface to a smooth, uniform plane before it cures.',
    calc:{
      inputs:[
        {id:'l', label:'Slab length', unit:'m', default:10},
        {id:'w', label:'Slab width', unit:'m', default:6},
        {id:'rate', label:'Screeding rate', unit:'m²/hr', default:25}
      ],
      run(v){
        const area = v.l*v.w;
        const time = area/v.rate;
        return {rows:[
          {label:'Slab area', value:area.toFixed(1)+' m²'},
          {label:'Estimated finishing time', value:time.toFixed(1)+' hours'}
        ]};
      }
    }},

  // ---------------- STRUCTURAL ----------------
  {cat:'steel', label:'Structural', name:'Tower Crane', spec:'Max load', val:'up to 20 t',
    desc:'Lifts steel, precast panels, and formwork to height on tall buildings and bridge piers.',
    calc:{
      inputs:[
        {id:'moment', label:'Rated moment capacity', unit:'kN·m', default:1200},
        {id:'radius', label:'Working radius', unit:'m', default:30}
      ],
      run(v){
        const loadKN = v.moment/v.radius;
        const loadKg = (loadKN*1000)/9.81;
        return {rows:[
          {label:'Max load at this radius', value:loadKN.toFixed(1)+' kN'},
          {label:'Equivalent mass', value:loadKg.toFixed(0)+' kg'}
        ], note:'Tower cranes work to a roughly constant rated moment: max load = rated moment ÷ radius. Always read the manufacturer\'s load chart for the actual machine.'};
      }
    }},
  {cat:'steel', label:'Structural', name:'Arc Welding Set', spec:'Output current', val:'50–300 A',
    desc:'Fuses steel beams, plates, and connections together for structural framing.',
    calc:{
      inputs:[
        {id:'dia', label:'Electrode diameter', unit:'mm', default:3.2}
      ],
      run(v){
        const low = v.dia*30, high = v.dia*40;
        return {rows:[
          {label:'Recommended current range', value:low.toFixed(0)+' – '+high.toFixed(0)+' A'}
        ], note:'Rule of thumb for mild-steel electrodes: current ≈ 30–40 × electrode diameter (mm). Confirm with the electrode manufacturer\'s data sheet.'};
      }
    }},
  {cat:'steel', label:'Structural', name:'Pile Driving Rig', spec:'Hammer energy', val:'up to 150 kJ',
    desc:'Drives steel, timber, or concrete piles deep into the ground to carry a structure\'s load.',
    calc:{
      inputs:[
        {id:'mass', label:'Hammer ram mass', unit:'kg', default:3000},
        {id:'drop', label:'Drop height', unit:'m', default:1.2},
        {id:'eff', label:'Hammer efficiency', unit:'0–1', default:0.75, step:0.05}
      ],
      run(v){
        const energy = v.mass*9.81*v.drop/1000; // kJ
        const useful = energy*v.eff;
        return {rows:[
          {label:'Theoretical energy per blow', value:energy.toFixed(1)+' kJ'},
          {label:'Efficiency-adjusted energy', value:useful.toFixed(1)+' kJ'}
        ], note:'Energy per blow = mass × 9.81 × drop height (potential energy). Actual pile capacity requires a proper dynamic or static formula and soil data.'};
      }
    }},
  {cat:'steel', label:'Structural', name:'Hydraulic Jack', spec:'Lift capacity', val:'up to 500 t',
    desc:'Lifts and aligns heavy structural sections, bridge decks, or bearings during placement.',
    calc:{
      inputs:[
        {id:'ain', label:'Input piston area', unit:'cm²', default:2},
        {id:'aout', label:'Output piston area', unit:'cm²', default:40},
        {id:'fin', label:'Applied input force', unit:'N', default:150}
      ],
      run(v){
        const ratio = v.aout/v.ain;
        const fout = v.fin*ratio;
        return {rows:[
          {label:'Mechanical advantage', value:ratio.toFixed(1)+'×'},
          {label:'Output force', value:fout.toFixed(0)+' N'},
          {label:'Equivalent lifting mass', value:(fout/9.81).toFixed(0)+' kg'}
        ], note:"Pascal's law: pressure is equal throughout the fluid, so output force = input force × (output area ÷ input area)."};
      }
    }},

  // ---------------- LIFTING ----------------
  {cat:'lift', label:'Lifting', name:'Mobile Crane', spec:'Boom length', val:'up to 60 m',
    desc:'A road-mobile crane used to lift materials on sites without a fixed tower crane.',
    calc:{
      inputs:[
        {id:'refCap', label:'Rated capacity at reference radius', unit:'t', default:10},
        {id:'refRad', label:'Reference radius', unit:'m', default:6},
        {id:'newRad', label:'Desired working radius', unit:'m', default:15}
      ],
      run(v){
        const moment = v.refCap*v.refRad;
        const newCap = moment/v.newRad;
        return {rows:[
          {label:'Estimated capacity at new radius', value:newCap.toFixed(2)+' t'}
        ], note:'Simplified constant-moment approximation (capacity × radius ≈ constant). Always use the crane\'s certified load chart for an actual lift.'};
      }
    }},
  {cat:'lift', label:'Lifting', name:'Launching Gantry', spec:'Span capacity', val:'up to 60 m',
    desc:'Lifts and places precast bridge girders or deck segments span by span.',
    calc:{
      inputs:[
        {id:'volume', label:'Segment volume', unit:'m³', default:12},
        {id:'density', label:'Concrete density', unit:'kg/m³', default:2400},
        {id:'rated', label:'Gantry rated capacity', unit:'t', default:35}
      ],
      run(v){
        const weightT = (v.volume*v.density)/1000;
        const pass = weightT <= v.rated;
        return {rows:[
          {label:'Segment weight', value:weightT.toFixed(2)+' t'},
          {label:'Rated capacity', value:v.rated+' t'}
        ], flag: pass?'pass':'fail', note: pass?'Segment weight is within the gantry\'s rated capacity.':'Segment weight exceeds the gantry\'s rated capacity — do not lift.'};
      }
    }},
  {cat:'lift', label:'Lifting', name:'Electric Winch', spec:'Line pull', val:'1–20 t',
    desc:'Pulls or hoists loads using a motor-driven drum and cable, often paired with cranes or rigging.',
    calc:{
      inputs:[
        {id:'load', label:'Load weight', unit:'kg', default:2000},
        {id:'lines', label:'Supporting rope lines (pulleys)', unit:'count', default:4},
        {id:'eff', label:'Efficiency per sheave', unit:'0–1', default:0.95, step:0.01}
      ],
      run(v){
        const idealForce = (v.load*9.81)/v.lines;
        const realForce = idealForce/Math.pow(v.eff, v.lines-1 || 1);
        return {rows:[
          {label:'Ideal pull force needed', value:(idealForce/1000).toFixed(2)+' kN'},
          {label:'Friction-adjusted pull force', value:(realForce/1000).toFixed(2)+' kN'}
        ], note:'Block-and-tackle estimate: more supporting lines reduce required pull force, but each sheave adds friction loss.'};
      }
    }},
  {cat:'lift', label:'Lifting', name:'Modular Scaffolding', spec:'Load class', val:'up to 6 kN/m²',
    desc:'A temporary access structure that supports workers and materials at height around a building.',
    calc:{
      inputs:[
        {id:'class', label:'Duty load class', unit:'kN/m²', default:2.0, step:0.5},
        {id:'area', label:'Platform area', unit:'m²', default:8}
      ],
      run(v){
        const totalKN = v.class*v.area;
        const totalKg = (totalKN*1000)/9.81;
        return {rows:[
          {label:'Safe total platform load', value:totalKN.toFixed(1)+' kN'},
          {label:'Equivalent mass', value:totalKg.toFixed(0)+' kg'}
        ], note:'Typical duty classes: light ~1.5, general ~2.0, heavy ~4.5–6 kN/m². Confirm against the scaffold design and standard in use.'};
      }
    }},

  // ---------------- TESTING ----------------
  {cat:'test', label:'Testing', name:'Slump Cone', spec:'Cone height', val:'300 mm',
    desc:'Checks the consistency of fresh concrete before it is placed, to confirm it matches the mix design.',
    calc:{
      inputs:[
        {id:'slump', label:'Measured slump', unit:'mm', default:75}
      ],
      run(v){
        let cls;
        if(v.slump<=25) cls='Very low — stiff, low workability';
        else if(v.slump<=50) cls='Low — used for mass concrete, roads';
        else if(v.slump<=100) cls='Medium — typical for slabs, beams';
        else if(v.slump<=175) cls='High — used where placement is congested';
        else cls='Very high / flowing — self-compacting range';
        return {rows:[{label:'Workability class', value:cls}]};
      }
    }},
  {cat:'test', label:'Testing', name:'Rebar Cover Meter', spec:'Detection depth', val:'up to 180 mm',
    desc:'Locates embedded reinforcement and measures the concrete cover protecting it from corrosion.',
    calc:{
      inputs:[
        {id:'measured', label:'Measured cover', unit:'mm', default:38},
        {id:'required', label:'Required cover (exposure class)', unit:'mm', default:40}
      ],
      run(v){
        const pass = v.measured >= v.required;
        return {rows:[
          {label:'Measured cover', value:v.measured+' mm'},
          {label:'Required cover', value:v.required+' mm'},
          {label:'Difference', value:(v.measured-v.required).toFixed(0)+' mm'}
        ], flag: pass?'pass':'fail'};
      }
    }},
  {cat:'test', label:'Testing', name:'Soil Compaction Tester', spec:'Test method', val:'Nuclear / drive-cone',
    desc:'Measures in-place soil density to confirm ground has been compacted enough to build on.',
    calc:{
      inputs:[
        {id:'field', label:'Field dry density', unit:'kg/m³', default:1880},
        {id:'max', label:'Max (Proctor) dry density', unit:'kg/m³', default:1950},
        {id:'req', label:'Required compaction', unit:'%', default:95}
      ],
      run(v){
        const pct = (v.field/v.max)*100;
        const pass = pct >= v.req;
        return {rows:[
          {label:'Relative compaction', value:pct.toFixed(1)+'%'},
          {label:'Required', value:v.req+'%'}
        ], flag: pass?'pass':'fail'};
      }
    }},
  {cat:'test', label:'Testing', name:'Strain Gauge & Load Cell', spec:'Sensitivity', val:'± 1 µε',
    desc:'Monitors stress and load on structural members during construction and load testing.',
    calc:{
      inputs:[
        {id:'force', label:'Applied force', unit:'N', default:5000},
        {id:'area', label:'Cross-section area', unit:'mm²', default:500},
        {id:'strain', label:'Measured strain', unit:'µε', default:250},
        {id:'e', label:'Elastic modulus (E)', unit:'GPa', default:200}
      ],
      run(v){
        const stressFromForce = v.force/v.area; // MPa
        const stressFromStrain = v.e*1000*(v.strain/1e6); // MPa
        return {rows:[
          {label:'Stress from force ÷ area', value:stressFromForce.toFixed(2)+' MPa'},
          {label:'Stress from E × strain (Hooke\'s law)', value:stressFromStrain.toFixed(2)+' MPa'}
        ]};
      }
    }}
];

const CATEGORIES = [
  {key:'all', label:'All disciplines'},
  {key:'survey', label:'Surveying'},
  {key:'earth', label:'Earthmoving'},
  {key:'concrete', label:'Concrete'},
  {key:'steel', label:'Structural'},
  {key:'lift', label:'Lifting'},
  {key:'test', label:'Testing'}
];

/* ---------------------------------------------------
   RENDER: filter bar + cards
--------------------------------------------------- */
const grid = document.getElementById('toolGrid');
const filterBar = document.getElementById('filterBar');
const resultCount = document.getElementById('resultCount');

function countFor(key){ return key === 'all' ? TOOLS.length : TOOLS.filter(t => t.cat === key).length; }

function renderFilters(){
  filterBar.innerHTML = CATEGORIES.map(c => `
    <button class="filter-btn${c.key==='all' ? ' active' : ''}" data-cat="${c.key}" role="tab" aria-selected="${c.key==='all'}">
      ${c.label}<span class="count mono">${countFor(c.key)}</span>
    </button>
  `).join('');
}

function renderCards(){
  grid.innerHTML = TOOLS.map((t, i) => `
    <div class="col-sm-6 col-lg-4 col-xl-3 tool-item" data-cat="${t.cat}">
      <button type="button" class="tool-card" data-index="${i}" aria-haspopup="dialog">
        <div class="icon">${ICONS[t.cat]}</div>
        <div class="tag mono">${t.label}</div>
        <h3>${t.name}</h3>
        <p>${t.desc}</p>
        <div class="spec"><span>${t.spec}</span><b>${t.val}</b></div>
        <div class="run-cta">▸ run calculator</div>
      </button>
    </div>
  `).join('');
}

function applyFilter(cat){
  const items = grid.querySelectorAll('.tool-item');
  let shown = 0;
  items.forEach(item => {
    const match = cat === 'all' || item.dataset.cat === cat;
    item.classList.toggle('hidden', !match);
    if(match) shown++;
  });
  resultCount.textContent = `${shown} / ${TOOLS.length} shown`;
  filterBar.querySelectorAll('.filter-btn').forEach(btn => {
    const active = btn.dataset.cat === cat;
    btn.classList.toggle('active', active);
    btn.setAttribute('aria-selected', active);
  });
}

renderFilters();
renderCards();
applyFilter('all');

filterBar.addEventListener('click', e => {
  const btn = e.target.closest('.filter-btn');
  if(!btn) return;
  applyFilter(btn.dataset.cat);
});

/* ---------------------------------------------------
   CALCULATOR MODAL
--------------------------------------------------- */
const toolModalEl = document.getElementById('toolModal');
const toolModal = new bootstrap.Modal(toolModalEl);
const modalTag = document.getElementById('modalTag');
const modalTitle = document.getElementById('toolModalLabel');
const modalDesc = document.getElementById('modalDesc');
const calcForm = document.getElementById('calcForm');
const calcResults = document.getElementById('calcResults');
const modalNote = document.getElementById('modalNote');

let currentTool = null;

function openTool(index){
  currentTool = TOOLS[index];
  modalTag.textContent = currentTool.label;
  modalTitle.textContent = currentTool.name;
  modalDesc.textContent = currentTool.desc;

  calcForm.innerHTML = currentTool.calc.inputs.map(inp => `
    <div class="calc-field">
      <label for="f_${inp.id}">${inp.label} <span class="unit">${inp.unit || ''}</span></label>
      <input type="number" class="form-control" id="f_${inp.id}" data-id="${inp.id}"
        value="${inp.default}" step="${inp.step || 'any'}">
    </div>
  `).join('');

  calcForm.querySelectorAll('input').forEach(inputEl => {
    inputEl.addEventListener('input', runCurrentCalc);
  });

  runCurrentCalc();
  toolModal.show();
}

function runCurrentCalc(){
  if(!currentTool) return;
  const values = {};
  calcForm.querySelectorAll('input').forEach(el => {
    values[el.dataset.id] = parseFloat(el.value) || 0;
  });

  let result;
  try{
    result = currentTool.calc.run(values);
  }catch(err){
    calcResults.innerHTML = `<div class="row-line"><span>Error</span><b>check inputs</b></div>`;
    return;
  }

  let html = result.rows.map(r => `<div class="row-line"><span>${r.label}</span><b>${r.value}</b></div>`).join('');
  if(result.flag){
    html += `<div class="calc-flag ${result.flag}">${result.flag === 'pass' ? '✓ WITHIN LIMIT' : '✕ OUT OF LIMIT'}</div>`;
  }
  calcResults.innerHTML = html;
  modalNote.textContent = result.note || '';
}

grid.addEventListener('click', e => {
  const card = e.target.closest('.tool-card');
  if(!card) return;
  openTool(parseInt(card.dataset.index, 10));
});
</script>
</body>
</html>
