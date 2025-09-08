<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1"/>
  <title>Would You Like To Be My Girlfriend? 💖</title>

  <!-- ฟอนต์ -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;600;800&family=Great+Vibes&display=swap" rel="stylesheet">

  <style>
    :root{
      --fg:#f6e9f1;
      --accent:#ff4d6d;
      --accent-2:#ff8fab;
      --card:#101018cc;
    }

    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0; color:var(--fg);
      font-family:"Kanit", system-ui, sans-serif;
      background:#000;
      overflow:hidden;
    }

    #sky{ position:fixed; inset:0; z-index:-2; display:block }

    .moon{ position:fixed; right:32px; top:32px; z-index:-1; filter: drop-shadow(0 0 30px #fff3) }

    .wrap{ position:relative; height:100%; display:grid; place-items:center; padding:24px; }
    .card{
      width:min(780px, 92vw); padding:32px 28px; border-radius:28px;
      background: var(--card);
      backdrop-filter: blur(8px);
      box-shadow: 0 30px 120px rgba(0,0,0,.5), 0 10px 30px rgba(0,0,0,.35);
      text-align:center;
      border:1px solid #ffffff22;
    }

    h1{ margin:4px 0 10px; }
    .name-tag{
      display:inline-block;
      padding:10px 22px;
      border-radius:999px;
      font-weight:700;
      font-size: clamp(28px, 5vw, 40px);
      color:white;
      background:linear-gradient(90deg, var(--accent), var(--accent-2));
      box-shadow: 0 8px 18px rgba(255,77,109,.35);
      letter-spacing: 1px;
    }

    p.sub{opacity:.9; margin:0 8px 18px; font-size: clamp(16px, 2.6vw, 18px)}

    .buttons{ display:flex; gap:14px; justify-content:center; margin-top:18px; flex-wrap:wrap }
    button{
      appearance:none; border:none; cursor:pointer;
      font-family:inherit; font-weight:700;
      padding:14px 20px; border-radius:16px; min-width:150px; font-size:18px;
      transition: transform .15s ease, box-shadow .2s ease;
    }
    .accept{ color:white; background:linear-gradient(135deg,#ff477e,#ff85a1); }
    .deny{ color:#ff88a2; background:#1b0f15; border:1px solid #ff88a233; }
    .accept:hover{ transform: translateY(-2px); }

    .button-zone{ position:relative; display:inline-block; min-width:min(680px, 92vw) }
    @media (max-width:560px){ .button-zone{ min-width:unset; width:100% } button{ min-width:120px } }

    .hearts{ position:fixed; inset:0; pointer-events:none; }

    .modal{ position:fixed; inset:0; display:grid; place-items:center; background:rgba(0,0,0,.45);
            visibility:hidden; opacity:0; transition: opacity .35s ease, visibility 0s .35s }
    .modal.show{ visibility:visible; opacity:1; transition: opacity .35s ease }
    .modal-card{ background:#16161f; color:#fff; border:1px solid #ffffff22;
                border-radius:28px; padding:26px 24px; width:min(620px, 92vw); text-align:center;
                box-shadow: 0 30px 120px rgba(0,0,0,.6); }
    .signature{font-family:"Great Vibes",cursive; font-size: clamp(26px, 5.2vw, 42px); color:#ffd1dc}

    #butterflies{ position:fixed; inset:0; pointer-events:none; z-index:-1; }
    .butterfly{
      position:absolute; font-size:22px; filter: drop-shadow(0 6px 10px #0006);
      animation: flap .8s ease-in-out infinite;
    }
    @keyframes flap{
      0%,100%{ transform: scale(1) rotate(-5deg); }
      50%{ transform: scale(1.08) rotate(5deg); }
    }

    .heart{ position:absolute; width:18px; height:18px; transform:translate(-50%,-50%);
      background: currentColor; color:#ff4d6d;
      clip-path: path('M12 4 C12 2, 10.5 0.5, 8.5 0.5 C7 0.5, 6 1.5, 6 3 C6 1.5, 5 0.5, 3.5 0.5 C1.5 0.5, 0 2, 0 4 C0 7.5, 6 10.5, 6 10.5 C6 10.5, 12 7.5, 12 4 Z');
      opacity:.9; filter: drop-shadow(0 6px 10px rgba(255,77,109,.35));
      animation: floatUp var(--dur) linear forwards;
    }
    @keyframes floatUp{ to{ transform:translate(var(--dx), calc(-100vh - 50px)); opacity:0 } }
  </style>
</head>
<body>
  <canvas id="sky"></canvas>
  <div class="moon" aria-hidden="true">
    <svg viewBox="0 0 200 200" width="200" height="200">
      <defs>
        <radialGradient id="moonGlow" cx="50%" cy="50%">
          <stop offset="0%" stop-color="#fffbe6"/>
          <stop offset="70%" stop-color="#f4f0c8"/>
          <stop offset="100%" stop-color="#f4f0c800"/>
        </radialGradient>
      </defs>
      <circle cx="100" cy="100" r="78" fill="url(#moonGlow)"/>
      <g fill="#2d2d2d" opacity="0.9" transform="translate(72,70) scale(0.9)">
        <ellipse cx="25" cy="55" rx="22" ry="26"/>
        <ellipse cx="16" cy="27" rx="10" ry="20" transform="rotate(-20 16 27)"/>
        <ellipse cx="34" cy="27" rx="10" ry="20" transform="rotate(20 34 27)"/>
        <circle cx="40" cy="52" r="7"/>
        <ellipse cx="46" cy="66" rx="14" ry="8" transform="rotate(-12 46 66)"/>
        <circle cx="18" cy="52" r="5"/>
      </g>
    </svg>
  </div>
  <div class="hearts" id="hearts" aria-hidden="true"></div>
  <div id="butterflies" aria-hidden="true"></div>

  <div class="wrap">
    <div class="card">
      <h1><span class="name-tag">Daring Pimpaka</span></h1>
      <p class="sub">Would You Like To Be My Girlfriend? 💘</p>
      <div class="button-zone">
        <div class="buttons">
          <button class="accept" id="accept">ยอมรับ</button>
          <button class="deny" id="deny">ไม่ยอมรับ</button>
        </div>
      </div>
    </div>
  </div>

  <div class="modal" id="modal">
    <div class="modal-card">
      <h2>แหมม ได้เป็นแฟนกันละเหรอ 💖</h2>
      <p>เค้าจะดูแล <b>เธอ</b> ด้วยความรักและความใส่ใจเสมอ 🌙</p>
      <div class="signature">รักเธอเสมอ</div>
      <div style="margin-top:18px">
        <button class="accept" id="closeModal" style="min-width:200px">ปิดหน้าต่าง</button>
      </div>
    </div>
  </div>

  <script>
    const sky = document.getElementById('sky');
    const ctx = sky.getContext('2d');
    let W = sky.width = innerWidth;
    let H = sky.height = innerHeight;
    addEventListener('resize', () => { W = sky.width = innerWidth; H = sky.height = innerHeight; });

    const stars = [];
    const SHOOTING_INTERVAL_MS = 1800;
    function spawnStar(){
      stars.push({x: Math.random()*W, y: Math.random()*H, r: Math.random()*1.2+0.3, a: Math.random()*0.6+0.2, tw: Math.random()*0.02+0.005});
    }
    for(let i=0;i<350;i++) spawnStar();

    const shooting = [];
    function spawnShooting(){
      const x = Math.random()*W*0.6 + W*0.2;
      const y = -20;
      const ang = (Math.random()*-20 - 25) * Math.PI/180;
      shooting.push({x, y, vx: Math.cos(ang)*12, vy: Math.sin(ang)*12, life:0, max:60});
    }
    setInterval(spawnShooting, SHOOTING_INTERVAL_MS);

    function drawSky(){
      ctx.clearRect(0,0,W,H);
      for(const s of stars){
        s.a += s.tw;
        const o = 0.5 + 0.5*Math.sin(s.a*60);
        ctx.globalAlpha = o; ctx.fillStyle='#fff';
        ctx.beginPath(); ctx.arc(s.x, s.y, s.r, 0, Math.PI*2); ctx.fill();
      }
      ctx.globalAlpha=1;
      for(let i=shooting.length-1;i>=0;i--){
        const m=shooting[i]; m.x+=m.vx; m.y+=m.vy; m.life++;
        const grad=ctx.createLinearGradient(m.x,m.y,m.x-m.vx*4,m.y-m.vy*4);
        grad.addColorStop(0,'rgba(255,255,255,0.95)'); grad.addColorStop(1,'rgba(255,255,255,0)');
        ctx.strokeStyle=grad; ctx.lineWidth=2;
        ctx.beginPath(); ctx.moveTo(m.x-m.vx*6,m.y-m.vy*6); ctx.lineTo(m.x,m.y); ctx.stroke();
        if(m.x<-50||m.x>W+50||m.y>H+50||m.life>m.max) shooting.splice(i,1);
      }
      requestAnimationFrame(drawSky);
    }
    requestAnimationFrame(drawSky);

    const butterflies=document.getElementById('butterflies'); const BCOUNT=8;
    const bList=[];
    function spawnButterfly(){
      const el=document.createElement('div'); el.className='butterfly'; el.textContent='🦋'; butterflies.appendChild(el);
      bList.push({el,x:Math.random()*W,y:H+Math.random()*120,vy:0.6+Math.random()*0.8,amp:40+Math.random()*60,spd:0.002+Math.random()*0.003,t:Math.random()*1000});
    }
    for(let i=0;i<BCOUNT;i++) spawnButterfly();
    function moveB(){for(const b of bList){b.t+=16*b.spd;b.y-=b.vy;const x=b.x+Math.sin(b.t)*b.amp;b.el.style.transform=`translate(${x}px,${b.y}px)`;if(b.y<-40){b.x=Math.random()*W;b.y=H+80;b.t=Math.random()*1000;}} requestAnimationFrame(moveB);}
    requestAnimationFrame(moveB);

    const heartsLayer=document.getElementById('hearts');
    function burstHearts(x,y,n=40){for(let i=0;i<n;i++){const h=document.createElement('div');h.className='heart';const dx=(Math.random()*2-1)*200+'px';h.style.setProperty('--dx',dx);h.style.setProperty('--dur',(2.6+Math.random()*1.4)+'s');h.style.left=(x+(Math.random()*60-30))+'px';h.style.top=(y+(Math.random()*30-15))+'px';h.style.color=Math.random()<.35?'#ff8fab':'#ff4d6d';heartsLayer.appendChild(h);setTimeout(()=>h.remove(),3500);}}

    const acceptBtn=document.getElementById('accept'); const denyBtn=document.getElementById('deny'); const modal=document.getElementById('modal'); const closeModal=document.getElementById('closeModal');
    function moveDeny(){const zone=document.querySelector('.button-zone');const r=zone.getBoundingClientRect();const b=denyBtn.getBoundingClientRect();const pad=10;const nx=Math.min(r.width-b.width-pad,Math.max(pad,(Math.random()*(r.width-b.width-pad*2))));const ny=Math.min(80,Math.max(-10,(Math.random()*60-10)));denyBtn.style.transform=`translate(${nx-(b.left-r.left)}px,${ny}px)`;}
    denyBtn.addEventListener('mouseenter',moveDeny);
    denyBtn.addEventListener('click',()=>{denyBtn.animate([{transform:'translate(0,0) rotate(0)'},{transform:'translate(-6px,0) rotate(-2deg)'},{transform:'translate(6px,0) rotate(2deg)'},{transform:'translate(0,0) rotate(0)'}],{duration:320,iterations:1,easing:'ease-in-out'});moveDeny();});
    acceptBtn.addEventListener('click',()=>{const rect=acceptBtn.getBoundingClientRect();burstHearts(rect.left+rect.width/2,rect.top+window.scrollY);setTimeout(()=>modal.classList.add('show'),350);});
    closeModal.addEventListener('click',()=>modal.classList.remove('show'));
    setInterval(()=>{burstHearts(Math.random()*innerWidth,innerHeight-20,5);},2500);
  </script>
</body>
</html>
