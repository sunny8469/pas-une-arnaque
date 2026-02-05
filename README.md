<!doctype html>
<html lang="fr">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>💘 Valentine</title>
  <style>
    :root{
      --bg1:#ff5f8f;
      --bg2:#ffd1dd;
      --card:#ffffffee;
      --text:#242424;
      --yes:#27c46a;
      --no:#ff5a5a;
      --shadow: 0 18px 45px rgba(0,0,0,.18);
    }
    *{ box-sizing:border-box; }
    body{
      margin:0;
      min-height:100vh;
      display:grid;
      place-items:center;
      font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Arial, "Apple Color Emoji","Segoe UI Emoji";
      color:var(--text);
      background:
        radial-gradient(1000px 700px at 15% 20%, rgba(255,255,255,.35), transparent 60%),
        radial-gradient(900px 600px at 85% 30%, rgba(255,255,255,.25), transparent 60%),
        linear-gradient(135deg, var(--bg1), var(--bg2));
      overflow:hidden;
    }

    /* Petits coeurs flottants (fond) */
    .heart{
      position:absolute;
      width:16px; height:16px;
      transform: rotate(45deg);
      opacity:.22;
      animation: float 10s linear infinite;
      filter: drop-shadow(0 6px 10px rgba(0,0,0,.12));
      z-index:0;
      pointer-events:none;
    }
    .heart:before, .heart:after{
      content:"";
      position:absolute;
      width:16px; height:16px;
      border-radius:50%;
      background: rgba(255,255,255,.95);
    }
    .heart{ background: rgba(255,255,255,.95); }
    .heart:before{ left:-8px; top:0; }
    .heart:after{ left:0; top:-8px; }

    @keyframes float{
      from{ transform: translateY(110vh) rotate(45deg); }
      to{ transform: translateY(-20vh) rotate(45deg); }
    }

    .card{
      width:min(820px, 92vw);
      background:var(--card);
      backdrop-filter: blur(8px);
      border-radius:26px;
      padding:30px 22px;
      box-shadow:var(--shadow);
      text-align:center;
      position:relative;
      z-index:2;
      border: 1px solid rgba(255,255,255,.6);
    }

    h1{
      margin:0 0 8px;
      font-size: clamp(26px, 4.2vw, 40px);
      font-weight: 900;
      letter-spacing: -0.3px;
    }
    .sub{
      margin:0 0 18px;
      opacity:.75;
      font-size: 14px;
    }

    /* Barre message (comme ton exemple) */
    .msg{
      min-height: 52px;
      display:flex;
      align-items:center;
      justify-content:center;
      font-weight:800;
      padding:12px 14px;
      border-radius:16px;
      background: rgba(255,255,255,.55);
      border: 1px solid rgba(255,105,135,.28);
      margin: 0 auto 18px;
      width: min(640px, 100%);
      box-shadow: 0 10px 25px rgba(0,0,0,.06);
    }

    /* Boutons en BARRES verticales */
    .buttons{
      display:flex;
      flex-direction: column;
      gap:14px;
      align-items:stretch;
      width: min(680px, 100%);
      margin: 6px auto 0;
    }

    .btn{
      width: 100%;
      border:0;
      cursor:pointer;
      border-radius:18px;
      font-weight:900;
      color:white;
      box-shadow: 0 14px 25px rgba(0,0,0,.12);
      transition: transform .12s ease, filter .2s ease, height .22s ease, font-size .22s ease, opacity .22s ease, box-shadow .22s ease;
      user-select:none;

      height: 66px;
      font-size: 16px;
      letter-spacing: .2px;
    }
    .btn:hover{ filter: brightness(1.04); }
    .btn:active{ transform: translateY(1px) scale(.99); }

    #yesBtn{ background: var(--yes); }
    #noBtn { background: var(--no);  }

    .footer{
      margin-top:14px;
      opacity:.55;
      font-size:12px;
    }

    /* Écran final “OUI énorme” */
    .final{
      position: fixed;
      inset: 0;
      display: grid;
      place-items: center;
      background: rgba(0,0,0,.22);
      backdrop-filter: blur(6px);
      z-index: 9999;
      padding: 18px;
    }
    .hidden{ display:none; }

    .finalBox{
      width: min(94vw, 980px);
      height: min(70vh, 560px);
      border-radius: 26px;
      display: grid;
      place-items: center;
      gap: 10px;
      background: #ffffff;
      box-shadow: 0 22px 70px rgba(0,0,0,.28);
      padding: 22px;
      border: 1px solid rgba(0,0,0,.05);
      transform: translateY(8px) scale(.98);
      animation: pop .25s ease-out forwards;
    }
    @keyframes pop{
      to{ transform: translateY(0) scale(1); }
    }

    .finalText{
      font-weight: 1000;
      font-size: clamp(90px, 22vw, 230px);
      line-height: 1;
      letter-spacing: -3px;
      text-transform: uppercase;
    }
    .finalSub{
      font-weight: 850;
      opacity: .75;
      font-size: clamp(14px, 2.6vw, 22px);
      text-align:center;
    }
    .finalHint{
      margin-top: 8px;
      font-weight: 700;
      opacity: .45;
      font-size: 12px;
      text-align:center;
    }

    /* Confettis */
    .confetti{
      position:absolute;
      top:-20px;
      width:10px; height:14px;
      border-radius:3px;
      opacity:.95;
      animation: drop 1.7s ease-in forwards;
      z-index: 10000;
      pointer-events:none;
    }
    @keyframes drop{
      to{ transform: translateY(115vh) rotate(720deg); opacity:1; }
    }
  </style>
</head>

<body>
  <div class="card" id="card" role="dialog" aria-label="Question Saint-Valentin">
    <h1>💘 Veux-tu être ma Valentine ?</h1>
    <p class="sub">Choisis… mais attention 😄</p>

    <div class="msg" id="msg">Clique sur un bouton 👀</div>

    <div class="buttons">
      <button class="btn" id="yesBtn">OUI 💞</button>
      <button class="btn" id="noBtn">NON 🙃</button>
    </div>

    <div class="footer">Tu peux envoyer ce fichier ou le mettre en lien (Netlify/GitHub Pages).</div>
  </div>

  <!-- Écran final -->
  <div id="finalScreen" class="final hidden" aria-hidden="true">
    <div class="finalBox">
      <div class="finalText">OUI</div>
      <div class="finalSub">💘 Trop bien 💘</div>
      <div class="finalHint">(Clique n’importe où pour fermer)</div>
    </div>
  </div>

  <script>
    // Messages "Non" random
    const noMessages = [
      "Tu veux vraiment cliquer NON encore ? 👀",
      "T’es sûre ? 🥺",
      "Réfléchis encore 2 secondes… 😭",
      "Mais… ça me brise le cœur là 💔",
      "Dernière chance avant que je boude 😤",
      "Ok mais imagine… nous deux + chocolat 🍫",
      "C’était un faux bouton non, hein ? 😅",
      "Je vais faire grandir le OUI, c’est plus simple 😌",
      "C’est une erreur de doigt, j’en suis sûr 😭",
      "Allez… dis oui… pour voir 😏"
    ];

    const msgEl = document.getElementById("msg");
    const yesBtn = document.getElementById("yesBtn");
    const noBtn  = document.getElementById("noBtn");
    const finalScreen = document.getElementById("finalScreen");
    const card = document.getElementById("card");

    function pick(arr){
      return arr[Math.floor(Math.random() * arr.length)];
    }

    // Progression : progresser dans les étapes à chaque NON, avec des changements de style
    let step = 0;
    const STEP_MAX = 10;

    function applySizes(){
      // OUI grossit (hauteur + glow)
      const yesH = Math.min(66 + step*18, 180);
      const yesFont = Math.min(16 + step*1.2, 22);

      // NON rapetisse (hauteur + texte)
      const noH = Math.max(66 - step*6, 34);
      const noFont = Math.max(16 - step*1.1, 12);

      yesBtn.style.height = yesH + "px";
      yesBtn.style.fontSize = yesFont + "px";

      noBtn.style.height = noH + "px";
      noBtn.style.fontSize = noFont + "px";

      // Glow progressif sur OUI
      const glow = Math.min(12 + step*7, 80);
      yesBtn.style.boxShadow = `0 16px 30px rgba(0,0,0,.14), 0 0 ${glow}px rgba(39,196,106,.55)`;

      // Non devient fade
      noBtn.style.opacity = Math.max(1 - step*0.07, 0.55);

      // Texte du NON
      if(step >= 8) noBtn.textContent = "…";
      else if(step >= 6) noBtn.textContent = "NON..? 😶";
      else noBtn.textContent = "NON 🙃";
    }

    applySizes();

    noBtn.addEventListener("click", () => {
      msgEl.textContent = pick(noMessages);
      step = Math.min(step + 1, STEP_MAX);
      applySizes();
    });

    yesBtn.addEventListener("click", () => {
      msgEl.textContent = "Bonne réponse 😌💘";

      // Affiche l’écran final “OUI énorme”
      finalScreen.classList.remove("hidden");
      finalScreen.setAttribute("aria-hidden", "false");

      // Cache la carte
      card.style.display = "none";

      confettiBurst();
    });

    // Clique pour fermer l’écran final et revenir
    finalScreen.addEventListener("click", () => {
      finalScreen.classList.add("hidden");
      finalScreen.setAttribute("aria-hidden", "true");
      card.style.display = "";
    });

    function confettiBurst(){
      const count = 90;
      for(let i=0;i<count;i++){
        const c = document.createElement("div");
        c.className = "confetti";
        c.style.left = Math.random()*100 + "vw";
        c.style.background = `hsl(${Math.floor(Math.random()*360)}, 90%, 60%)`;
        c.style.animationDelay = (Math.random()*0.25) + "s";
        c.style.transform = `translateY(0) rotate(${Math.random()*180}deg)`;
        document.body.appendChild(c);
        setTimeout(() => c.remove(), 2300);
      }
    }

    // Coeurs en fond
    (function makeHearts(){
      const n = 18;
      for(let i=0;i<n;i++){
        const h = document.createElement("div");
        h.className = "heart";
        h.style.left = Math.random()*100 + "vw";
        h.style.animationDelay = (-Math.random()*10) + "s";
        h.style.animationDuration = (8 + Math.random()*8) + "s";
        h.style.transform = `rotate(45deg) scale(${0.6 + Math.random()*1.2})`;
        document.body.appendChild(h);
      }
    })();
  </script>
</body>
</html>
