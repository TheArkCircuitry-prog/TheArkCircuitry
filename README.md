<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>TheArkCircuitryLLC</title>

  <!-- Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;800&display=swap" rel="stylesheet">

  <!-- Leaflet -->
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />

  <style>
    :root {
      --bg:#05070f;
      --panel:#0f1428;
      --accent:#ffffff;
      --muted:#9aa0b8;
      --green:#3cff8f;
      --red:#ff4d4d;
    }

    *{box-sizing:border-box}

    body{
      margin:0;
      font-family:'Orbitron',sans-serif;
      background:radial-gradient(circle at top,#141a35,#05070f);
      color:var(--accent);
    }

    header{
      display:flex;
      justify-content:space-between;
      align-items:center;
      padding:18px 40px;
      background:linear-gradient(180deg,#0f1428,#070a14);
      border-bottom:1px solid #222;
    }

    header img{height:52px}

    nav a{
      margin-left:28px;
      color:var(--accent);
      text-decoration:none;
      opacity:.8;
    }
    nav a:hover{opacity:1}

    .hero{
      text-align:center;
      padding:80px 20px 40px;
    }

    .hero h1{
      font-size:3rem;
      margin-bottom:12px;
      letter-spacing:2px;
    }

    .hero p{
      max-width:720px;
      margin:auto;
      color:var(--muted);
      line-height:1.6;
    }

    #map{height:60vh;margin-top:30px}

    /* TICKER BAR */
    .ticker{
      display:flex;
      justify-content:center;
      gap:40px;
      padding:18px;
      background:#070a14;
      border-top:1px solid #222;
      border-bottom:1px solid #222;
      font-size:.9rem;
    }

    .tick{display:flex;gap:10px;align-items:center}
    .up{color:var(--green)}
    .down{color:var(--red)}

    .section{
      padding:70px 40px;
      max-width:1300px;
      margin:auto;
    }

    .grid{
      display:grid;
      grid-template-columns:repeat(auto-fit,minmax(280px,1fr));
      gap:30px;
    }

    .card{
      background:linear-gradient(180deg,#141a35,#0b1022);
      padding:25px;
      border-radius:16px;
      box-shadow:0 0 40px rgba(0,0,0,.6);
      transition:transform .3s ease;
    }
    .card:hover{transform:translateY(-6px)}

    footer{
      text-align:center;
      padding:25px;
      background:#060812;
      color:#777;
      font-size:.85rem;
    }

    /* LOGIN MODAL */
    .modal{
      position:fixed;
      inset:0;
      background:rgba(0,0,0,.7);
      display:none;
      justify-content:center;
      align-items:center;
    }

    .modal-content{
      background:#0f1428;
      padding:30px;
      border-radius:14px;
      width:320px;
    }

    .modal-content input{
      width:100%;
      margin-bottom:15px;
      padding:10px;
      border:none;
      border-radius:8px;
    }

    .modal-content button{
      width:100%;
      padding:10px;
      border:none;
      border-radius:8px;
      background:var(--green);
      font-weight:600;
      cursor:pointer;
    }

    /* PULSING MAP CIRCLES */
    .pulse{
      animation:pulse 2.5s infinite;
    }

    @keyframes pulse{
      0%{opacity:.6}
      50%{opacity:1}
      100%{opacity:.6}
    }
  </style>
</head>
<body>

<header>
  <img src="logo.png" alt="TheArkCircuitryLLC">
  <nav>
    <a href="#">Home</a>
    <a href="#markets">Markets</a>
    <a href="#research">Research</a>
    <a href="#" onclick="openLogin()">Login</a>
  </nav>
</header>

<section class="hero">
  <h1>THE ARK CIRCUITRY LLC</h1>
  <p>Global market intelligence, execution models, and circuit-based trading infrastructure.</p>
</section>

<div id="map"></div>

<div class="ticker">
  <div class="tick">ES <span class="up">+12.50</span></div>
  <div class="tick">NQ <span class="up">+40.25</span></div>
  <div class="tick">BTC <span class="down">-250.80</span></div>
</div>

<section class="section" id="research">
  <h2>Research & Analysis</h2>
  <div class="grid">
    <div class="card">Market Structure – USD/JPY</div>
    <div class="card">Weekly Outlook</div>
    <div class="card">Execution Models</div>
  </div>
</section>

<footer>© 2025 TheArkCircuitryLLC • All Rights Reserved</footer>

<div class="modal" id="loginModal">
  <div class="modal-content">
    <h3>Client Login</h3>
    <input type="email" placeholder="Email">
    <input type="password" placeholder="Password">
    <button>Login</button>
  </div>
</div>

<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
<script>
  const map=L.map('map').setView([20,0],2);
  L.tileLayer('https://{s}.basemaps.cartocdn.com/dark_all/{z}/{x}/{y}{r}.png').addTo(map);

  const locations=[
    {name:'New York',coords:[40.71,-74.01]},
    {name:'London',coords:[51.50,-0.12]},
    {name:'Tokyo',coords:[35.67,139.65]},
    {name:'Singapore',coords:[1.35,103.82]}
  ];

  locations.forEach(loc=>{
    const c=L.circle(loc.coords,{radius:450000,color:'#ffffff',fillOpacity:.25,className:'pulse'}).addTo(map);
    c.bindTooltip(loc.name);
  });

  function openLogin(){document.getElementById('loginModal').style.display='flex'}
  window.onclick=e=>{if(e.target.id==='loginModal')loginModal.style.display='none'}
</script>

</body>
</html>
