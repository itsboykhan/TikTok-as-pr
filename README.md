<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>for my love</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,500;0,700;1,600&family=Cormorant+Garamond:ital,wght@0,400;0,600;1,400&family=Dancing+Script:wght@500;700&display=swap" rel="stylesheet">
<style>
  :root{
    --cream:#FBF3E9;
    --paper:#FFFBF6;
    --blush:#F1C7D0;
    --rose:#E28FA0;
    --wine:#7A2E3D;
    --wine-dark:#5A1F2B;
    --gold:#C9A24B;
    --ink:#3B1620;
    --shadow: 0 25px 70px rgba(90,31,43,0.28);
  }

  *{box-sizing:border-box;}

  html,body{
    margin:0;
    padding:0;
    width:100%;
    height:100%;
    overflow:hidden;
    font-family:'Cormorant Garamond', serif;
    color:var(--ink);
  }

  body{
    background: linear-gradient(120deg, #FCE4E9, #FBF3E9, #F6DCE2, #FCE9EF);
    background-size: 300% 300%;
    animation: driftBg 18s ease infinite;
  }
  @keyframes driftBg{
    0%{background-position:0% 50%;}
    50%{background-position:100% 50%;}
    100%{background-position:0% 50%;}
  }

  /* soft radial glow that follows the cursor, purely ambient */
  .glow{
    position:fixed;
    width:420px;
    height:420px;
    border-radius:50%;
    background: radial-gradient(circle, rgba(226,143,160,0.22), transparent 70%);
    pointer-events:none;
    z-index:0;
    transform:translate(-50%,-50%);
    transition: left 0.15s ease-out, top 0.15s ease-out;
  }

  /* ambient floating hearts */
  .ambient{
    position:fixed;
    inset:0;
    pointer-events:none;
    z-index:0;
    overflow:hidden;
  }
  .ambient span{
    position:absolute;
    bottom:-10%;
    color:var(--rose);
    opacity:0.35;
    animation: floatUp linear infinite;
    filter: drop-shadow(0 0 3px rgba(226,143,160,0.4));
  }
  @keyframes floatUp{
    0%{ transform: translateY(0) translateX(0) rotate(0deg) scale(1); opacity:0;}
    10%{opacity:0.45;}
    90%{opacity:0.3;}
    100%{ transform: translateY(-115vh) translateX(30px) rotate(30deg) scale(1.1); opacity:0;}
  }

  .stage{
    position:relative;
    width:100%;
    height:100%;
    display:flex;
    align-items:center;
    justify-content:center;
    z-index:1;
  }

  .hint{
    position:absolute;
    bottom:30px;
    left:50%;
    transform:translateX(-50%);
    font-family:'Dancing Script', cursive;
    font-size:1.4rem;
    color:var(--wine);
    opacity:0.55;
    letter-spacing:0.5px;
  }

  /* progress dots */
  .progress{
    position:fixed;
    top:26px;
    left:50%;
    transform:translateX(-50%);
    display:flex;
    gap:10px;
    z-index:30;
  }
  .progress span{
    width:8px;
    height:8px;
    border-radius:50%;
    background: rgba(122,46,61,0.25);
    transition: background 0.4s ease, transform 0.4s ease;
  }
  .progress span.active{
    background: var(--wine);
    transform: scale(1.3);
  }

  /* ---------- overlay base ---------- */
  .overlay{
    position:fixed;
    inset:0;
    display:flex;
    align-items:center;
    justify-content:center;
    background: rgba(58,20,29,0.30);
    backdrop-filter: blur(7px);
    -webkit-backdrop-filter: blur(7px);
    z-index:10;
    opacity:0;
    pointer-events:none;
    transition: opacity 0.5s ease;
  }
  .overlay.visible{
    opacity:1;
    pointer-events:auto;
  }

  .card{
    position:relative;
    background: var(--paper);
    border-radius:20px;
    box-shadow: var(--shadow);
    padding:50px 46px;
    max-width:440px;
    width:88%;
    text-align:center;
    border:1px solid rgba(201,162,75,0.35);
    transform: scale(0.85) translateY(14px);
    transition: transform 0.55s cubic-bezier(.2,.9,.3,1.3);
  }
  .overlay.visible .card{
    transform: scale(1) translateY(0);
  }

  .card::before, .card::after{
    content:"";
    position:absolute;
    width:60px;
    height:60px;
    border:1.5px solid var(--gold);
    opacity:0.5;
  }
  .card::before{ top:12px; left:12px; border-right:none; border-bottom:none; }
  .card::after{ bottom:12px; right:12px; border-left:none; border-top:none; }

  /* ---------- envelope (popup 1) ---------- */
  .envelope-wrap{
    cursor:pointer;
    user-select:none;
  }
  .envelope{
    position:relative;
    width:190px;
    height:126px;
    margin:0 auto 26px;
    animation: heartbeat 2.6s ease-in-out infinite;
  }
  @keyframes heartbeat{
    0%,100%{ transform: scale(1); }
    10%{ transform: scale(1.035); }
    20%{ transform: scale(1); }
  }
  .envelope.open{ animation:none; }
  .env-body{
    position:absolute;
    inset:0;
    background: linear-gradient(135deg, var(--blush), var(--rose));
    border-radius:6px;
    box-shadow: 0 12px 26px rgba(122,46,61,0.28);
  }
  .env-flap{
    position:absolute;
    top:0; left:0; right:0;
    height:0;
    border-left:95px solid transparent;
    border-right:95px solid transparent;
    border-top:63px solid var(--wine);
    transform-origin: top center;
    transition: transform 0.65s ease;
    filter: drop-shadow(0 4px 6px rgba(90,31,43,0.3));
  }
  .envelope.open .env-flap{
    transform: rotateX(180deg);
  }
  .seal{
    position:absolute;
    top:46px; left:50%;
    transform:translate(-50%,0);
    width:36px; height:36px;
    background: radial-gradient(circle at 35% 30%, #d9b25f, var(--gold));
    border-radius:50%;
    display:flex;align-items:center;justify-content:center;
    font-family:'Playfair Display', serif;
    font-weight:700;
    font-size:15px;
    color:#fff8ec;
    box-shadow: 0 3px 6px rgba(0,0,0,0.25);
    z-index:2;
    transition: opacity 0.3s ease;
  }
  .envelope.open .seal{ opacity:0; }

  .eyebrow{
    font-family:'Dancing Script', cursive;
    color:var(--gold);
    font-size:1.15rem;
    letter-spacing:0.5px;
    margin-bottom:2px;
    opacity:0.9;
  }
  .letter-title{
    font-family:'Playfair Display', serif;
    font-style:italic;
    font-weight:700;
    font-size:2.2rem;
    color:var(--wine);
    margin:4px 0 6px;
    letter-spacing:0.3px;
  }
  .letter-sub{
    font-size:1.15rem;
    color:var(--ink);
    opacity:0.75;
    margin:0 0 22px;
    line-height:1.5;
  }
  .tap-note{
    font-family:'Dancing Script', cursive;
    color:var(--rose);
    font-size:1.2rem;
  }

  /* ---------- letter reveal (popup 1.5) ---------- */
  .letter-body{
    text-align:left;
    font-size:1.15rem;
    line-height:1.75;
    color:var(--ink);
    min-height:150px;
    margin-bottom:18px;
  }
  .letter-body .cursor{
    display:inline-block;
    width:2px;
    height:1.1em;
    background:var(--rose);
    vertical-align:middle;
    margin-left:2px;
    animation: blink 0.9s steps(1) infinite;
  }
  @keyframes blink{ 50%{opacity:0;} }
  .continue-btn{
    display:inline-block;
    margin-top:6px;
    font-family:'Cormorant Garamond', serif;
    font-weight:600;
    font-size:1.15rem;
    padding:12px 28px;
    border-radius:999px;
    border:none;
    cursor:pointer;
    background: linear-gradient(135deg, var(--wine), var(--wine-dark));
    color:#FBF3E9;
    box-shadow: 0 10px 22px rgba(122,46,61,0.35);
    opacity:0;
    transform: translateY(8px);
    transition: opacity 0.5s ease, transform 0.5s ease, box-shadow 0.25s ease, transform 0.25s ease;
    pointer-events:none;
  }
  .continue-btn.ready{
    opacity:1;
    transform: translateY(0);
    pointer-events:auto;
  }
  .continue-btn:hover{
    transform: scale(1.05);
    box-shadow: 0 14px 26px rgba(122,46,61,0.45);
  }

  /* ---------- question card (popup 2) ---------- */
  .question-title{
    font-family:'Playfair Display', serif;
    font-weight:600;
    font-size:1.95rem;
    color:var(--wine-dark);
    margin:0 0 8px;
    line-height:1.3;
  }
  .question-sub{
    font-size:1.1rem;
    color:var(--ink);
    opacity:0.7;
    margin:0 0 30px;
  }

  .btn-row{
    position:relative;
    display:flex;
    gap:22px;
    justify-content:center;
    align-items:center;
    min-height:70px;
  }

  .btn{
    font-family:'Cormorant Garamond', serif;
    font-weight:600;
    font-size:1.25rem;
    padding:14px 32px;
    border-radius:999px;
    border:none;
    cursor:pointer;
    letter-spacing:0.5px;
    transition: transform 0.22s cubic-bezier(.3,1.5,.5,1), box-shadow 0.25s ease, font-size 0.25s ease;
  }
  .btn-yes{
    background: linear-gradient(135deg, var(--wine), var(--wine-dark));
    color:#FBF3E9;
    box-shadow: 0 10px 22px rgba(122,46,61,0.35);
  }
  .btn-yes:hover{
    transform: scale(1.08);
    box-shadow: 0 14px 28px rgba(122,46,61,0.45);
  }
  .btn-no{
    background: var(--paper);
    color:var(--wine);
    border:1.5px solid var(--rose);
    position:fixed;
    z-index:20;
  }

  .plea{
    margin-top:18px;
    min-height:24px;
    font-family:'Dancing Script', cursive;
    font-size:1.3rem;
    color:var(--rose);
    transition: opacity 0.3s ease;
  }

  .attempt-counter{
    margin-top:6px;
    font-size:0.95rem;
    color:var(--ink);
    opacity:0.45;
    letter-spacing:0.3px;
  }

  /* ---------- celebration (popup 3) ---------- */
  .celebrate-title{
    font-family:'Playfair Display', serif;
    font-style:italic;
    font-weight:700;
    font-size:2.4rem;
    color:var(--wine-dark);
    margin:10px 0;
  }
  .celebrate-sub{
    font-size:1.2rem;
    color:var(--ink);
    opacity:0.8;
    margin-bottom:6px;
    line-height:1.6;
  }
  .hearts-burst{
    font-size:2.5rem;
    margin-bottom:6px;
  }
  .signature{
    margin-top:18px;
    font-family:'Dancing Script', cursive;
    font-size:1.5rem;
    color:var(--gold);
  }

  canvas#confetti{
    position:fixed;
    inset:0;
    pointer-events:none;
    z-index:40;
  }

  @media (max-width:480px){
    .card{ padding:38px 26px; }
    .letter-title{ font-size:1.8rem; }
    .question-title{ font-size:1.55rem; }
    .btn{ font-size:1.05rem; padding:12px 24px; }
    .letter-body{ font-size:1.05rem; }
  }
</style>
</head>
<body>

  <div class="glow" id="glow"></div>
  <div class="ambient" id="ambient"></div>

  <div class="progress" id="progress">
    <span class="active" data-step="1"></span>
    <span data-step="2"></span>
    <span data-step="3"></span>
  </div>

  <div class="stage">
    <div class="hint">a little something for you&hellip;</div>
  </div>

  <canvas id="confetti"></canvas>

  <!-- Popup 1: Envelope -->
  <div class="overlay visible" id="overlay1">
    <div class="card envelope-wrap" id="envelopeWrap">
      <div class="envelope" id="envelope">
        <div class="env-flap"></div>
        <div class="env-body"></div>
        <div class="seal">M</div>
      </div>
      <div class="eyebrow">for my love</div>
      <div class="letter-title">I love you</div>
      <div class="letter-sub">There's a letter waiting inside for you.</div>
      <div class="tap-note">tap the envelope to open it</div>
    </div>
  </div>

  <!-- Popup 1.5: Letter -->
  <div class="overlay" id="overlayLetter">
    <div class="card">
      <div class="eyebrow">a letter to my love</div>
      <div class="letter-body" id="letterBody"><span class="cursor"></span></div>
      <button class="continue-btn" id="continueBtn">Turn the page</button>
    </div>
  </div>

  <!-- Popup 2: Question -->
  <div class="overlay" id="overlay2">
    <div class="card">
      <div class="question-title">will you accept my love?</div>
      <div class="question-sub">Choose wisely &mdash; your heart already knows.</div>
      <div class="btn-row" id="btnRow">
        <button class="btn btn-yes" id="yesBtn">Yes</button>
        <button class="btn btn-no" id="noBtn">No</button>
      </div>
      <div class="plea" id="plea"></div>
      <div class="attempt-counter" id="attemptCounter"></div>
    </div>
  </div>

  <!-- Popup 3: Celebration -->
  <div class="overlay" id="overlay3">
    <div class="card">
      <div class="hearts-burst">&hearts;&nbsp;&hearts;&nbsp;&hearts;</div>
      <div class="celebrate-title">I knew it, my love.</div>
      <div class="celebrate-sub">You've just made me the happiest person alive. Thank you for choosing my heart.</div>
      <div class="signature">forever yours</div>
    </div>
  </div>

<script>
  /* ---------------- ambient hearts + cursor glow ---------------- */
  const ambient = document.getElementById('ambient');
  for(let i=0;i<20;i++){
    const s = document.createElement('span');
    s.textContent = '♥';
    s.style.left = Math.random()*100 + '%';
    s.style.fontSize = (14 + Math.random()*22) + 'px';
    s.style.animationDuration = (10 + Math.random()*12) + 's';
    s.style.animationDelay = (Math.random()*12) + 's';
    ambient.appendChild(s);
  }

  const glow = document.getElementById('glow');
  window.addEventListener('mousemove', (e) => {
    glow.style.left = e.clientX + 'px';
    glow.style.top = e.clientY + 'px';
  });

  /* ---------------- progress dots ---------------- */
  const progressDots = document.querySelectorAll('.progress span');
  function setStep(step){
    progressDots.forEach(d => d.classList.toggle('active', Number(d.dataset.step) <= step));
  }

  /* ---------------- elements ---------------- */
  const overlay1 = document.getElementById('overlay1');
  const overlayLetter = document.getElementById('overlayLetter');
  const overlay2 = document.getElementById('overlay2');
  const overlay3 = document.getElementById('overlay3');
  const envelope = document.getElementById('envelope');
  const envelopeWrap = document.getElementById('envelopeWrap');
  const letterBody = document.getElementById('letterBody');
  const continueBtn = document.getElementById('continueBtn');
  const noBtn = document.getElementById('noBtn');
  const yesBtn = document.getElementById('yesBtn');
  const plea = document.getElementById('plea');
  const attemptCounter = document.getElementById('attemptCounter');

  /* ---------------- letter typewriter ---------------- */
  const letterLines = [
    "My dearest love,",
    "",
    "From the moment you walked into my life, everything felt a little more like poetry.",
    "Your smile has a way of rewriting my worst days into my best ones.",
    "I don't say this lightly, and I don't say it because it's easy \u2014 I say it because it's true:",
    "I love you so much. Completely, quietly, and without asking for anything in return.",
    "So here I am, laying my heart open on this little page, waiting for your answer."
  ];

  let lineIdx = 0, charIdx = 0;
  function typeLetter(){
    if(lineIdx >= letterLines.length){
      continueBtn.classList.add('ready');
      return;
    }
    const line = letterLines[lineIdx];
    if(charIdx === 0){
      const p = document.createElement('div');
      p.className = 'type-line';
      p.style.minHeight = '1.2em';
      letterBody.insertBefore(p, letterBody.querySelector('.cursor'));
    }
    const lines = letterBody.querySelectorAll('.type-line');
    const current = lines[lines.length - 1];
    if(charIdx < line.length){
      current.textContent = line.slice(0, charIdx + 1);
      charIdx++;
      setTimeout(typeLetter, 18 + Math.random()*18);
    } else {
      lineIdx++;
      charIdx = 0;
      setTimeout(typeLetter, line === "" ? 80 : 260);
    }
  }

  /* ---------------- flow: envelope -> letter -> question -> celebration ---------------- */
  envelopeWrap.addEventListener('click', () => {
    envelope.classList.add('open');
    setTimeout(() => {
      overlay1.classList.remove('visible');
      overlayLetter.classList.add('visible');
      setStep(2);
      setTimeout(typeLetter, 300);
    }, 600);
  });

  continueBtn.addEventListener('click', () => {
    overlayLetter.classList.remove('visible');
    overlay2.classList.add('visible');
    setStep(3);
    placeNoInitial();
  });

  /* ---------------- dodging No button ---------------- */
  const pleas = [
    "wait, come back...",
    "are you sure, my love?",
    "pretty please?",
    "think about it...",
    "give it a chance!",
    "my heart says yes...",
    "just try to catch it \uD83D\uDE09",
    "it's shy, that's all",
    "yes is right there though \u2192"
  ];
  let pleaIndex = 0;
  let yesScale = 1;
  let dodgeCount = 0;

  function placeNoInitial(){
    const rect = noBtn.getBoundingClientRect();
    noBtn.style.left = rect.left + 'px';
    noBtn.style.top = rect.top + 'px';
  }

  function clampAndMoveNo(avoidX, avoidY){
    const btnW = noBtn.offsetWidth;
    const btnH = noBtn.offsetHeight;
    const margin = 20;
    const maxX = window.innerWidth - btnW - margin;
    const maxY = window.innerHeight - btnH - margin;

    let newX, newY, dist;
    let attempts = 0;
    do{
      newX = margin + Math.random() * (maxX - margin);
      newY = margin + Math.random() * (maxY - margin);
      const cx = newX + btnW/2;
      const cy = newY + btnH/2;
      dist = Math.hypot(cx - avoidX, cy - avoidY);
      attempts++;
    } while(dist < 260 && attempts < 24);

    noBtn.style.left = newX + 'px';
    noBtn.style.top = newY + 'px';
    noBtn.style.transform = `rotate(${(Math.random()*16 - 8).toFixed(1)}deg)`;

    yesScale = Math.min(yesScale + 0.05, 1.55);
    yesBtn.style.transform = `scale(${yesScale})`;
    yesBtn.style.fontSize = (1.25 + (yesScale-1)*0.55) + 'rem';

    plea.textContent = pleas[pleaIndex % pleas.length];
    pleaIndex++;
    plea.style.opacity = '1';

    dodgeCount++;
    attemptCounter.textContent = dodgeCount === 1
      ? "1 attempt to click No"
      : dodgeCount + " attempts to click No";
  }

  function dodge(e){
    if(!overlay2.classList.contains('visible')) return;
    const rect = noBtn.getBoundingClientRect();
    const btnCx = rect.left + rect.width/2;
    const btnCy = rect.top + rect.height/2;

    const clientX = e.touches ? e.touches[0].clientX : e.clientX;
    const clientY = e.touches ? e.touches[0].clientY : e.clientY;

    const dist = Math.hypot(clientX - btnCx, clientY - btnCy);
    const threshold = 115;

    if(dist < threshold){
      clampAndMoveNo(clientX, clientY);
    }
  }

  document.addEventListener('mousemove', dodge);
  document.addEventListener('touchmove', dodge, {passive:true});
  noBtn.addEventListener('mouseenter', () => {
    const rect = noBtn.getBoundingClientRect();
    clampAndMoveNo(rect.left + rect.width/2, rect.top + rect.height/2);
  });
  noBtn.addEventListener('click', (e) => {
    e.preventDefault();
    clampAndMoveNo(e.clientX, e.clientY);
  });

  window.addEventListener('resize', () => {
    if(overlay2.classList.contains('visible')){
      const rect = noBtn.getBoundingClientRect();
      const maxX = window.innerWidth - rect.width - 20;
      const maxY = window.innerHeight - rect.height - 20;
      noBtn.style.left = Math.min(rect.left, maxX) + 'px';
      noBtn.style.top = Math.min(rect.top, maxY) + 'px';
    }
  });

  /* ---------------- Yes -> celebration + confetti hearts ---------------- */
  yesBtn.addEventListener('click', () => {
    overlay2.classList.remove('visible');
    overlay3.classList.add('visible');
    setStep(3);
    burstHearts();
  });

  /* ---------------- canvas heart confetti ---------------- */
  const canvas = document.getElementById('confetti');
  const ctx = canvas.getContext('2d');
  function resizeCanvas(){
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
  }
  resizeCanvas();
  window.addEventListener('resize', resizeCanvas);

  function drawHeart(x, y, size, rotation, color, opacity){
    ctx.save();
    ctx.translate(x, y);
    ctx.rotate(rotation);
    ctx.globalAlpha = opacity;
    ctx.fillStyle = color;
    ctx.beginPath();
    const topCurveHeight = size * 0.3;
    ctx.moveTo(0, topCurveHeight);
    ctx.bezierCurveTo(0, 0, -size/2, 0, -size/2, topCurveHeight);
    ctx.bezierCurveTo(-size/2, size*0.7, 0, size*0.9, 0, size*1.2);
    ctx.bezierCurveTo(0, size*0.9, size/2, size*0.7, size/2, topCurveHeight);
    ctx.bezierCurveTo(size/2, 0, 0, 0, 0, topCurveHeight);
    ctx.fill();
    ctx.restore();
  }

  let particles = [];
  function burstHearts(){
    const colors = ['#7A2E3D', '#E28FA0', '#C9A24B', '#F1C7D0'];
    const cx = canvas.width / 2;
    const cy = canvas.height * 0.35;
    for(let i=0;i<70;i++){
      const angle = Math.random() * Math.PI * 2;
      const speed = 3 + Math.random()*7;
      particles.push({
        x: cx, y: cy,
        vx: Math.cos(angle)*speed,
        vy: Math.sin(angle)*speed - 3,
        size: 8 + Math.random()*14,
        rot: Math.random()*Math.PI*2,
        vrot: (Math.random()-0.5)*0.2,
        color: colors[Math.floor(Math.random()*colors.length)],
        life: 1
      });
    }
    if(!animating){ animating = true; animateParticles(); }
  }

  let animating = false;
  function animateParticles(){
    ctx.clearRect(0,0,canvas.width, canvas.height);
    particles.forEach(p => {
      p.vy += 0.12;
      p.x += p.vx;
      p.y += p.vy;
      p.rot += p.vrot;
      p.life -= 0.008;
      drawHeart(p.x, p.y, p.size, p.rot, p.color, Math.max(p.life,0));
    });
    particles = particles.filter(p => p.life > 0 && p.y < canvas.height + 50);
    if(particles.length > 0){
      requestAnimationFrame(animateParticles);
    } else {
      animating = false;
      ctx.clearRect(0,0,canvas.width, canvas.height);
    }
  }
</script>
</body>
</html>
