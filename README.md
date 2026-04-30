<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Verset du Jour</title>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,600;1,400;1,600&family=Cinzel:wght@400;600&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --gold: #C9A96E;
    --gold-light: #E8D5A3;
    --dark: #0D0B08;
    --dark2: #1A1612;
    --dark3: #2A2319;
    --text: #F0E8D8;
    --text-muted: #9C8F78;
    --border: rgba(201, 169, 110, 0.25);
    --bg: #0D0B08;
    --card-bg: rgba(255,255,255,0.02);
    --cross-color: white;
  }

  body.light {
    --dark: #FAF6EF;
    --bg: #FAF6EF;
    --dark2: #F0E8D8;
    --text: #2A1F0E;
    --text-muted: #7A6A50;
    --border: rgba(150, 110, 50, 0.25);
    --card-bg: rgba(0,0,0,0.02);
    --cross-color: #2A1F0E;
  }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Cormorant Garamond', serif;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    position: relative;
    overflow-x: hidden;
    transition: background 0.4s ease, color 0.4s ease;
  }

  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background:
      radial-gradient(ellipse 60% 50% at 50% 0%, rgba(201,169,110,0.07) 0%, transparent 70%),
      radial-gradient(ellipse 40% 40% at 80% 80%, rgba(201,169,110,0.04) 0%, transparent 60%);
    pointer-events: none;
  }

  .cross-bg {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    opacity: 0.025;
    pointer-events: none;
  }

  .cross-bg svg { width: 600px; height: 600px; }
  .cross-bg rect { fill: var(--cross-color); transition: fill 0.4s; }

  .container {
    max-width: 720px;
    width: 100%;
    padding: 3rem 2rem;
    position: relative;
    z-index: 1;
    text-align: center;
  }

  .site-title {
    font-family: 'Cinzel', serif;
    font-size: clamp(0.75rem, 2vw, 0.9rem);
    letter-spacing: 0.35em;
    color: var(--gold);
    text-transform: uppercase;
    margin-bottom: 3rem;
    opacity: 0.8;
  }

  .ornament {
    color: var(--gold);
    opacity: 0.5;
    font-size: 1.4rem;
    letter-spacing: 0.5em;
    display: block;
    margin-bottom: 0.5rem;
  }

  .date-display {
    font-size: 0.85rem;
    color: var(--text-muted);
    letter-spacing: 0.15em;
    margin-bottom: 3rem;
    font-style: italic;
  }

  .verse-card {
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 3rem 3rem 2.5rem;
    background: var(--card-bg);
    position: relative;
    margin-bottom: 2rem;
    animation: fadeIn 1s ease;
    transition: background 0.4s ease, border-color 0.4s ease;
  }

  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(16px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .verse-card::before, .verse-card::after {
    content: '';
    position: absolute;
    width: 40px;
    height: 40px;
    border-color: var(--gold);
    border-style: solid;
    opacity: 0.4;
  }
  .verse-card::before { top: -1px; left: -1px; border-width: 2px 0 0 2px; }
  .verse-card::after  { bottom: -1px; right: -1px; border-width: 0 2px 2px 0; }

  .quote-mark {
    font-size: 5rem;
    line-height: 0.5;
    color: var(--gold);
    opacity: 0.3;
    font-family: 'Cormorant Garamond', serif;
    display: block;
    margin-bottom: 1.2rem;
  }

  .verse-text {
    font-size: clamp(1.4rem, 3.5vw, 1.85rem);
    line-height: 1.65;
    font-style: italic;
    color: var(--text);
    margin-bottom: 2rem;
    font-weight: 400;
  }

  .verse-ref {
    font-family: 'Cinzel', serif;
    font-size: 0.9rem;
    color: var(--gold);
    letter-spacing: 0.2em;
    display: inline-block;
    padding: 0.4rem 1.5rem;
    border: 1px solid var(--border);
    border-radius: 2px;
  }

  .nav-row {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 1.5rem;
    margin-top: 2.5rem;
  }

  .nav-btn {
    background: none;
    border: 1px solid var(--border);
    color: var(--text-muted);
    font-family: 'Cormorant Garamond', serif;
    font-size: 0.95rem;
    padding: 0.55rem 1.5rem;
    border-radius: 2px;
    cursor: pointer;
    transition: all 0.25s;
    letter-spacing: 0.08em;
  }
  .nav-btn:hover {
    border-color: var(--gold);
    color: var(--gold);
    background: rgba(201,169,110,0.05);
  }

  .verse-counter {
    font-size: 0.8rem;
    color: var(--text-muted);
    opacity: 0.6;
    font-style: italic;
  }

  footer {
    margin-top: 4rem;
    font-size: 0.78rem;
    color: var(--text-muted);
    opacity: 0.45;
    letter-spacing: 0.1em;
  }

  @media (max-width: 520px) {
    .verse-card { padding: 2rem 1.5rem; }
    .container { padding: 2rem 1.25rem; }
  }

  /* Top bar */
  .top-bar {
    position: fixed;
    top: 1.2rem;
    right: 1.5rem;
    display: flex;
    gap: 0.6rem;
    z-index: 100;
  }

  .icon-btn {
    background: var(--card-bg);
    border: 1px solid var(--border);
    color: var(--text-muted);
    width: 38px;
    height: 38px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    font-size: 1rem;
    transition: all 0.2s;
    backdrop-filter: blur(4px);
  }
  .icon-btn:hover { border-color: var(--gold); color: var(--gold); }
  .icon-btn.active { color: var(--gold); border-color: var(--gold); }

  /* Action row below card */
  .action-row {
    display: flex;
    justify-content: center;
    gap: 0.75rem;
    margin-bottom: 1.5rem;
    flex-wrap: wrap;
  }

  .action-btn {
    background: none;
    border: 1px solid var(--border);
    color: var(--text-muted);
    font-family: 'Cormorant Garamond', serif;
    font-size: 0.88rem;
    padding: 0.45rem 1.1rem;
    border-radius: 2px;
    cursor: pointer;
    transition: all 0.2s;
    display: flex;
    align-items: center;
    gap: 0.4rem;
    letter-spacing: 0.05em;
  }
  .action-btn:hover { border-color: var(--gold); color: var(--gold); background: rgba(201,169,110,0.05); }
  .action-btn.fav-active { color: #e8734a; border-color: #e8734a; }
  .action-btn .icon { font-size: 1rem; }

  /* Toast notification */
  .toast {
    position: fixed;
    bottom: 2rem;
    left: 50%;
    transform: translateX(-50%) translateY(80px);
    background: var(--gold);
    color: #1a1208;
    font-family: 'Cormorant Garamond', serif;
    font-size: 0.9rem;
    padding: 0.6rem 1.5rem;
    border-radius: 3px;
    letter-spacing: 0.05em;
    transition: transform 0.35s ease;
    z-index: 200;
    white-space: nowrap;
    font-weight: 600;
  }
  .toast.show { transform: translateX(-50%) translateY(0); }

  /* Favorites panel */
  .fav-panel {
    position: fixed;
    top: 0; right: 0;
    width: min(380px, 100vw);
    height: 100vh;
    background: var(--bg);
    border-left: 1px solid var(--border);
    z-index: 300;
    display: flex;
    flex-direction: column;
    transform: translateX(100%);
    transition: transform 0.35s ease, background 0.4s ease;
    overflow: hidden;
  }
  .fav-panel.open { transform: translateX(0); }

  .fav-header {
    padding: 1.5rem 1.5rem 1rem;
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .fav-header h2 {
    font-family: 'Cinzel', serif;
    font-size: 0.85rem;
    letter-spacing: 0.25em;
    color: var(--gold);
    text-transform: uppercase;
  }
  .fav-close {
    background: none;
    border: none;
    color: var(--text-muted);
    font-size: 1.3rem;
    cursor: pointer;
    line-height: 1;
    transition: color 0.2s;
  }
  .fav-close:hover { color: var(--text); }

  .fav-list {
    flex: 1;
    overflow-y: auto;
    padding: 1rem;
  }
  .fav-list::-webkit-scrollbar { width: 4px; }
  .fav-list::-webkit-scrollbar-thumb { background: var(--border); border-radius: 2px; }

  .fav-empty {
    text-align: center;
    color: var(--text-muted);
    font-style: italic;
    font-size: 1rem;
    margin-top: 3rem;
    line-height: 1.7;
  }

  .fav-item {
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 1rem 1rem 0.8rem;
    margin-bottom: 0.75rem;
    cursor: pointer;
    transition: border-color 0.2s, background 0.2s;
  }
  .fav-item:hover { border-color: var(--gold); background: rgba(201,169,110,0.04); }
  .fav-item-ref {
    font-family: 'Cinzel', serif;
    font-size: 0.72rem;
    color: var(--gold);
    letter-spacing: 0.15em;
    margin-bottom: 0.4rem;
  }
  .fav-item-text {
    font-size: 0.92rem;
    line-height: 1.55;
    color: var(--text-muted);
    font-style: italic;
    display: -webkit-box;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }
  .fav-item-remove {
    font-size: 0.75rem;
    color: var(--text-muted);
    opacity: 0.5;
    float: right;
    margin-left: 0.5rem;
    line-height: 1;
  }

  /* Share modal */
  .share-modal-bg {
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.5);
    z-index: 400;
    display: none;
    align-items: center;
    justify-content: center;
    backdrop-filter: blur(3px);
  }
  .share-modal-bg.open { display: flex; }
  .share-modal {
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 2rem;
    width: min(360px, 90vw);
    text-align: center;
    animation: fadeIn 0.3s ease;
  }
  .share-modal h3 {
    font-family: 'Cinzel', serif;
    font-size: 0.8rem;
    letter-spacing: 0.25em;
    color: var(--gold);
    text-transform: uppercase;
    margin-bottom: 1.5rem;
  }
  .share-btns {
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
  }
  .share-link-btn {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    padding: 0.75rem 1.25rem;
    border: 1px solid var(--border);
    border-radius: 4px;
    background: none;
    color: var(--text);
    font-family: 'Cormorant Garamond', serif;
    font-size: 1rem;
    cursor: pointer;
    transition: all 0.2s;
    text-decoration: none;
    letter-spacing: 0.05em;
  }
  .share-link-btn:hover { border-color: var(--gold); color: var(--gold); background: rgba(201,169,110,0.05); }
  .share-link-btn .s-icon { font-size: 1.2rem; width: 1.5rem; text-align: center; }
  .share-cancel {
    margin-top: 1rem;
    background: none;
    border: none;
    color: var(--text-muted);
    font-family: 'Cormorant Garamond', serif;
    font-size: 0.9rem;
    cursor: pointer;
    letter-spacing: 0.08em;
  }
  .share-cancel:hover { color: var(--text); }

  /* Overlay for fav panel */
  .overlay {
    position: fixed;
    inset: 0;
    z-index: 299;
    display: none;
  }
  .overlay.open { display: block; }
</style>
</head>
<body>

<div class="top-bar">
  <button class="icon-btn" id="theme-btn" title="Mode jour/nuit">🌙</button>
  <button class="icon-btn" id="fav-open-btn" title="Mes favoris">🔖</button>
</div>

<div class="overlay" id="overlay"></div>

<div class="fav-panel" id="fav-panel">
  <div class="fav-header">
    <h2>✦ Mes Favoris</h2>
    <button class="fav-close" id="fav-close">✕</button>
  </div>
  <div class="fav-list" id="fav-list">
    <p class="fav-empty">Tu n'as pas encore de favoris.<br>Clique sur ♡ pour en ajouter.</p>
  </div>
</div>

<div class="share-modal-bg" id="share-modal-bg">
  <div class="share-modal">
    <h3>Partager ce verset</h3>
    <div class="share-btns">
      <button class="share-link-btn" id="copy-btn">
        <span class="s-icon">📋</span> Copier le texte
      </button>
      <a class="share-link-btn" id="whatsapp-btn" target="_blank" rel="noopener">
        <span class="s-icon">💬</span> WhatsApp
      </a>
      <a class="share-link-btn" id="facebook-btn" target="_blank" rel="noopener">
        <span class="s-icon">📘</span> Facebook
      </a>
    </div>
    <button class="share-cancel" id="share-cancel">Annuler</button>
  </div>
</div>

<div class="toast" id="toast"></div>

<div class="cross-bg">
  <svg viewBox="0 0 200 200" fill="none" xmlns="http://www.w3.org/2000/svg">
    <rect x="85" y="20" width="30" height="160" fill="white"/>
    <rect x="30" y="65" width="140" height="30" fill="white"/>
  </svg>
</div>

<div class="container">
  <div class="site-title">
    <span class="ornament">✦ ✦ ✦</span>
    Verset du Jour
  </div>

  <div class="date-display" id="date-display"></div>

  <div class="verse-card" id="verse-card">
    <span class="quote-mark">"</span>
    <p class="verse-text" id="verse-text"></p>
    <span class="verse-ref" id="verse-ref"></span>
  </div>

  <div class="action-row">
    <button class="action-btn" id="fav-btn"><span class="icon">♡</span> Favori</button>
    <button class="action-btn" id="share-btn"><span class="icon">↗</span> Partager</button>
  </div>

  <div class="nav-row">
    <button class="nav-btn" id="prev-btn">← Précédent</button>
    <span class="verse-counter" id="verse-counter"></span>
    <button class="nav-btn" id="next-btn">Suivant →</button>
  </div>

  <footer>« Ta parole est une lampe à mes pieds et une lumière sur mon sentier. » — Psaume 119:105</footer>
</div>

<script>
const VERSETS = [
  { ref: "Jean 3:16", texte: "Car Dieu a tant aimé le monde qu'il a donné son Fils unique, afin que quiconque croit en lui ne périsse pas, mais qu'il ait la vie éternelle." },
  { ref: "Romains 8:28", texte: "Nous savons, du reste, que toutes choses concourent au bien de ceux qui aiment Dieu, de ceux qui sont appelés selon son dessein." },
  { ref: "Jérémie 29:11", texte: "Car je connais les projets que j'ai formés sur vous, dit l'Éternel, projets de paix et non de malheur, afin de vous donner un avenir et de l'espérance." },
  { ref: "Philippiens 4:13", texte: "Je puis tout par celui qui me fortifie." },
  { ref: "Psaume 23:1", texte: "L'Éternel est mon berger : je ne manquerai de rien." },
  { ref: "Ésaïe 40:31", texte: "Mais ceux qui se confient en l'Éternel renouvellent leur force. Ils prennent leur essor comme des aigles ; ils courent sans se fatiguer, et marchent sans se lasser." },
  { ref: "Matthieu 11:28", texte: "Venez à moi, vous tous qui êtes fatigués et chargés, et je vous donnerai du repos." },
  { ref: "Proverbes 3:5-6", texte: "Confie-toi en l'Éternel de tout ton cœur, et ne t'appuie pas sur ta sagesse. Reconnais-le dans toutes tes voies, et il aplanira tes sentiers." },
  { ref: "Psaume 46:1", texte: "Dieu est pour nous un refuge et un appui, un secours qui ne manque jamais dans la détresse." },
  { ref: "Romains 8:37", texte: "Mais dans toutes ces choses nous sommes plus que vainqueurs par celui qui nous a aimés." },
  { ref: "Josué 1:9", texte: "Ne t'ai-je pas donné cet ordre : Sois fort et courageux ? Ne t'inquiète pas et ne t'effraie pas, car l'Éternel, ton Dieu, est avec toi dans tout ce que tu entreprendras." },
  { ref: "2 Corinthiens 5:17", texte: "Si quelqu'un est en Christ, il est une nouvelle créature. Les choses anciennes sont passées ; voici, toutes choses sont devenues nouvelles." },
  { ref: "Psaume 27:1", texte: "L'Éternel est ma lumière et mon salut : de qui aurais-je crainte ? L'Éternel est le soutien de ma vie : de qui aurais-je peur ?" },
  { ref: "Ésaïe 41:10", texte: "Ne crains pas, car je suis avec toi ; ne regarde pas avec inquiétude, car je suis ton Dieu. Je te fortifie, je viens à ton secours, je te soutiens de ma droite triomphante." },
  { ref: "Matthieu 6:33", texte: "Cherchez premièrement le royaume et la justice de Dieu ; et toutes ces choses vous seront données par-dessus." },
  { ref: "Galates 5:22-23", texte: "Mais le fruit de l'Esprit, c'est l'amour, la joie, la paix, la patience, la bonté, la bienveillance, la foi, la douceur, la tempérance." },
  { ref: "Romains 12:2", texte: "Ne vous conformez pas au siècle présent, mais soyez transformés par le renouvellement de l'intelligence, afin que vous discerniez quelle est la volonté de Dieu, ce qui est bon, agréable et parfait." },
  { ref: "Psaume 37:4", texte: "Fais de l'Éternel tes délices, et il te donnera ce que ton cœur désire." },
  { ref: "Philippiens 4:6-7", texte: "Ne vous inquiétez de rien ; mais en toute chose faites connaître vos besoins à Dieu par des prières et des supplications, avec des actions de grâces. Et la paix de Dieu, qui surpasse toute intelligence, gardera vos cœurs et vos pensées en Jésus-Christ." },
  { ref: "Lamentations 3:22-23", texte: "Les bontés de l'Éternel ne sont pas épuisées, ses compassions ne sont pas à leur terme. Elles se renouvellent chaque matin. Ta fidélité est grande !" },
  { ref: "Hébreux 11:1", texte: "Or, la foi est une ferme assurance des choses qu'on espère, une démonstration de celles qu'on ne voit pas." },
  { ref: "Jacques 1:17", texte: "Toute grâce excellente et tout don parfait descendent d'en haut, du Père des lumières, en qui il n'y a ni changement ni ombre de variation." },
  { ref: "1 Jean 4:19", texte: "Nous l'aimons, parce qu'il nous a aimés le premier." },
  { ref: "Psaume 119:105", texte: "Ta parole est une lampe à mes pieds et une lumière sur mon sentier." },
  { ref: "Colossiens 3:17", texte: "Et quoi que vous fassiez, en parole ou en œuvre, faites tout au nom du Seigneur Jésus, en rendant par lui des actions de grâces à Dieu le Père." },
  { ref: "Hébreux 13:8", texte: "Jésus-Christ est le même hier, aujourd'hui, et éternellement." },
  { ref: "Matthieu 5:8", texte: "Heureux ceux qui ont le cœur pur, car ils verront Dieu !" },
  { ref: "1 Pierre 5:7", texte: "Déchargez-vous sur lui de tous vos soucis, car lui-même prend soin de vous." },
  { ref: "Romains 5:8", texte: "Mais Dieu prouve son amour envers nous, en ce que, lorsque nous étions encore des pécheurs, Christ est mort pour nous." },
  { ref: "Ésaïe 43:2", texte: "Quand tu traverseras les eaux, je serai avec toi ; quand tu traverseras les fleuves, ils ne te submergeront pas ; quand tu marcheras dans le feu, tu ne te brûleras pas, et la flamme ne t'embrasera pas." },
  { ref: "Psaume 34:18", texte: "L'Éternel est près de ceux qui ont le cœur brisé, et il sauve ceux dont l'esprit est dans l'abattement." },
  { ref: "Jean 14:6", texte: "Jésus lui dit : Je suis le chemin, la vérité, et la vie. Nul ne vient au Père que par moi." },
  { ref: "Ésaïe 55:8-9", texte: "Car mes pensées ne sont pas vos pensées, et vos voies ne sont pas mes voies, dit l'Éternel. Autant les cieux sont élevés au-dessus de la terre, autant mes voies sont élevées au-dessus de vos voies, et mes pensées au-dessus de vos pensées." },
  { ref: "Psaume 91:1", texte: "Celui qui demeure sous l'abri du Très-Haut repose à l'ombre du Tout-Puissant." },
  { ref: "Matthieu 7:7", texte: "Demandez, et l'on vous donnera ; cherchez, et vous trouverez ; frappez, et l'on vous ouvrira." },
  { ref: "1 Corinthiens 13:4-5", texte: "La charité est patiente, elle est pleine de bonté ; la charité n'est point envieuse ; la charité ne se vante point, elle ne s'enfle point d'orgueil, elle ne fait rien de malhonnête, elle ne cherche point son intérêt." },
  { ref: "Psaume 145:18", texte: "L'Éternel est près de tous ceux qui l'invoquent, de tous ceux qui l'invoquent avec sincérité." },
  { ref: "Jean 10:10", texte: "Le voleur ne vient que pour dérober, égorger et détruire ; moi, je suis venu afin que les brebis aient la vie, et qu'elles soient dans l'abondance." },
  { ref: "Romains 8:1", texte: "Il n'y a donc maintenant aucune condamnation pour ceux qui sont en Jésus-Christ." },
  { ref: "Ésaïe 26:3", texte: "À celui qui est ferme dans ses dispositions tu assures la paix, la paix, parce qu'il se confie en toi." },
  { ref: "Psaume 51:10", texte: "O Dieu, crée en moi un cœur pur, renouvelle en moi un esprit bien disposé." },
  { ref: "1 Thessaloniciens 5:16-18", texte: "Soyez toujours dans la joie. Priez sans cesse. Rendez grâces en toutes choses, car c'est à votre égard la volonté de Dieu en Jésus-Christ." },
  { ref: "Marc 11:24", texte: "C'est pourquoi je vous dis : Tout ce que vous demanderez en priant, croyez que vous l'avez reçu, et vous le verrez s'accomplir." },
  { ref: "Psaume 103:2-3", texte: "Mon âme, bénis l'Éternel, et n'oublie aucun de ses bienfaits ! C'est lui qui pardonne toutes tes iniquités, qui guérit toutes tes maladies." },
  { ref: "Romains 8:38-39", texte: "Car j'ai l'assurance que ni la mort ni la vie, ni les anges ni les dominations, ni les choses présentes ni les choses à venir, ni les puissances, ni la hauteur, ni la profondeur, ni aucune autre créature ne pourra nous séparer de l'amour de Dieu manifesté en Jésus-Christ notre Seigneur." },
  { ref: "Ésaïe 40:28-29", texte: "Ne le sais-tu pas ? Ne l'as-tu pas appris ? L'Éternel est un Dieu d'éternité, il a créé les extrémités de la terre. Il ne se fatigue point, il ne se lasse point ; sa sagesse est insondable. Il donne de la force à celui qui est fatigué, et il augmente la vigueur de celui qui est à bout de forces." },
  { ref: "Jean 8:36", texte: "Si donc le Fils vous affranchit, vous serez réellement libres." },
  { ref: "Matthieu 28:20", texte: "Et voici, je suis avec vous tous les jours, jusqu'à la fin du monde." },
  { ref: "1 Jean 1:9", texte: "Si nous confessons nos péchés, il est fidèle et juste pour nous les pardonner, et pour nous purifier de toute iniquité." },
  { ref: "Psaume 121:1-2", texte: "Je lève les yeux vers les montagnes… D'où me viendra le secours ? Le secours me vient de l'Éternel, qui a fait les cieux et la terre." },
  { ref: "Habacuc 3:17-18", texte: "Car, même si le figuier ne fleurit pas, si la vigne ne donne plus de fruit, si le produit de l'olivier est décevant, si les champs ne produisent pas de nourriture, si le bétail disparaît des enclos et s'il n'y a plus de troupeaux dans les étables, moi je veux me réjouir en l'Éternel et exulter dans le Dieu de mon salut." },
  { ref: "Deutéronome 31:6", texte: "Soyez forts et courageux, ne craignez pas et ne tremblez pas devant eux, car l'Éternel, ton Dieu, lui-même marche avec toi. Il ne te laissera pas, il ne t'abandonnera pas." },
  { ref: "Psaume 62:5-6", texte: "Mon âme, repose-toi en Dieu seul, car mon espoir vient de lui. Lui seul est mon rocher et mon salut, ma haute retraite ; je ne serai pas ébranlé." },
  { ref: "1 Corinthiens 10:13", texte: "Aucune tentation ne vous est survenue qui n'ait été humaine, et Dieu, qui est fidèle, ne permettra pas que vous soyez tentés au-delà de vos forces ; mais avec la tentation il préparera aussi le moyen d'en sortir, afin que vous puissiez la supporter." },
  { ref: "Proverbes 16:3", texte: "Recommande à l'Éternel tes œuvres, et tes projets s'accompliront." },
  { ref: "Ésaïe 64:4", texte: "On n'a jamais entendu, on n'a point perçu par l'oreille, l'œil n'a point vu de Dieu hormis toi, ce que tu feras pour celui qui espère en toi." },
  { ref: "Matthieu 5:6", texte: "Heureux ceux qui ont faim et soif de la justice, car ils seront rassasiés !" },
  { ref: "1 Pierre 2:9", texte: "Vous êtes une race élue, un sacerdoce royal, une nation sainte, un peuple acquis, afin que vous annonciez les vertus de celui qui vous a appelés des ténèbres à son admirable lumière." },
  { ref: "Psaume 16:11", texte: "Tu me feras connaître le sentier de la vie ; il y a une abondance de joies devant ta face, des délices éternelles à ta droite." },
  { ref: "Jean 15:5", texte: "Je suis le cep, vous êtes les sarments. Celui qui demeure en moi et en qui je demeure porte beaucoup de fruit, car sans moi vous ne pouvez rien faire." },
  { ref: "Éphésiens 3:20", texte: "Or, à celui qui peut faire, par la puissance qui agit en nous, infiniment au-delà de tout ce que nous demandons ou pensons, à lui soit la gloire dans l'Église et en Jésus-Christ, dans toutes les générations, aux siècles des siècles ! Amen !" },
  { ref: "Psaume 32:8", texte: "Je t'instruirai et te montrerai la voie que tu dois suivre ; je te conseillerai, j'aurai les yeux sur toi." },
  { ref: "Romains 15:13", texte: "Que le Dieu de l'espérance vous remplisse de toute joie et de toute paix dans la foi, pour que vous abondiez en espérance, par la puissance du Saint-Esprit !" },
  { ref: "Ésaïe 53:5", texte: "Mais il était blessé pour nos péchés, brisé pour nos iniquités ; le châtiment qui nous donne la paix est tombé sur lui, et c'est par ses meurtrissures que nous sommes guéris." },
  { ref: "2 Timothée 1:7", texte: "Car ce n'est pas un esprit de timidité que Dieu nous a donné, mais un esprit de force, d'amour et de sagesse." },
  { ref: "Jean 16:33", texte: "Je vous ai dit ces choses, afin que vous ayez la paix en moi. Vous aurez des tribulations dans le monde ; mais prenez courage, j'ai vaincu le monde." },
  { ref: "Psaume 73:26", texte: "Ma chair et mon cœur peuvent défaillir : Dieu sera toujours le rocher de mon cœur et mon partage." },
  { ref: "Hébreux 4:16", texte: "Approchons-nous donc avec assurance du trône de la grâce, afin d'obtenir miséricorde et de trouver grâce, pour être secourus dans nos besoins." },
  { ref: "Romains 12:12", texte: "Réjouissez-vous en espérance. Soyez patients dans la tribulation. Persévérez dans la prière." },
  { ref: "Actes 1:8", texte: "Mais vous recevrez une puissance, le Saint-Esprit survenant sur vous, et vous serez mes témoins à Jérusalem, dans toute la Judée, dans la Samarie, et jusqu'aux extrémités de la terre." },
  { ref: "Ésaïe 43:18-19", texte: "Ne vous souvenez plus des choses passées, et ne songez plus aux choses anciennes ! Car voici, je vais faire une chose nouvelle, et déjà elle pointe : ne la voyez-vous pas ?" },
  { ref: "Colossiens 3:2", texte: "Affectionnez-vous aux choses d'en haut, et non à celles qui sont sur la terre." },
  { ref: "Psaume 55:22", texte: "Décharge sur l'Éternel ton fardeau, et il te soutiendra ; il ne laissera jamais chanceler le juste." },
  { ref: "Jean 14:27", texte: "Je vous laisse la paix, je vous donne ma paix. Je ne vous donne pas comme le monde donne. Que votre cœur ne se trouble point, et ne s'alarme point." },
  { ref: "Apocalypse 21:4", texte: "Il essuiera toute larme de leurs yeux, et la mort ne sera plus, et il n'y aura plus ni deuil, ni cri, ni douleur, car les premières choses ont disparu." },
  { ref: "Proverbes 18:10", texte: "Le nom de l'Éternel est une tour forte ; le juste s'y réfugie et se trouve en sécurité." },
  { ref: "1 Rois 8:56", texte: "Béni soit l'Éternel, qui a donné du repos à son peuple Israël, selon tout ce qu'il avait dit ! Pas une seule de toutes les bonnes paroles qu'il avait faites par Moïse, son serviteur, n'est restée sans effet." },
  { ref: "Jean 11:25", texte: "Jésus lui dit : Je suis la résurrection et la vie. Celui qui croit en moi vivra, quand même il serait mort." },
  { ref: "Romains 1:16", texte: "Car je n'ai pas honte de l'Évangile : c'est une puissance de Dieu pour le salut de quiconque croit." },
  { ref: "1 Jean 5:4", texte: "Parce que tout ce qui est né de Dieu triomphe du monde ; et la victoire qui triomphe du monde, c'est notre foi." },
  { ref: "Psaume 100:4-5", texte: "Entrez dans ses portes avec des actions de grâces, dans ses parvis avec des louanges. Célébrez-le, bénissez son nom ! Car l'Éternel est bon, sa bonté dure toujours, et sa fidélité de génération en génération." },
  { ref: "Matthieu 5:16", texte: "Que votre lumière luise ainsi devant les hommes, afin qu'ils voient vos bonnes œuvres, et qu'ils glorifient votre Père qui est dans les cieux." },
  { ref: "Éphésiens 6:10", texte: "Du reste, fortifiez-vous dans le Seigneur, et par sa force toute-puissante." },
  { ref: "Psaume 3:3", texte: "Mais toi, Éternel ! tu es un bouclier autour de moi, tu es ma gloire, et tu relèves ma tête." },
  { ref: "Genèse 1:1", texte: "Au commencement, Dieu créa les cieux et la terre." },
  { ref: "Jean 1:1", texte: "Au commencement était la Parole, et la Parole était avec Dieu, et la Parole était Dieu." },
  { ref: "Apocalypse 3:20", texte: "Voici, je me tiens à la porte, et je frappe. Si quelqu'un entend ma voix et ouvre la porte, j'entrerai chez lui, je souperai avec lui, et lui avec moi." },
  { ref: "Romains 8:14", texte: "Car tous ceux qui sont conduits par l'Esprit de Dieu sont fils de Dieu." },
  { ref: "Hébreux 12:2", texte: "Ayant les regards sur Jésus, le chef et le consommateur de la foi, qui, en vue de la joie qui lui était réservée, a souffert la croix, méprisé l'ignominie, et s'est assis à la droite du trône de Dieu." },
  { ref: "Matthieu 6:9-10", texte: "Notre Père qui es aux cieux ! Que ton nom soit sanctifié ; que ton règne vienne ; que ta volonté soit faite sur la terre comme au ciel." },
  { ref: "1 Samuel 16:7", texte: "L'homme regarde à ce qui frappe les yeux, mais l'Éternel regarde au cœur." },
  { ref: "Psaume 139:14", texte: "Je te loue de ce que je suis une créature si merveilleuse. Tes œuvres sont admirables, et mon âme le reconnaît bien." },
  { ref: "Ésaïe 1:18", texte: "Venez et plaidons, dit l'Éternel. Si vos péchés sont comme le cramoisi, ils deviendront blancs comme la neige." },
  { ref: "Ézéchiel 36:26", texte: "Je vous donnerai un cœur nouveau, et je mettrai en vous un esprit nouveau ; j'ôterai de votre corps le cœur de pierre, et je vous donnerai un cœur de chair." },
  { ref: "Apocalypse 1:8", texte: "Je suis l'Alpha et l'Oméga, dit le Seigneur Dieu, celui qui est, qui était, et qui vient, le Tout-Puissant." },
  { ref: "Jean 3:3", texte: "Jésus lui répondit : En vérité, en vérité, je te le dis, si un homme ne naît de nouveau, il ne peut voir le royaume de Dieu." },
  { ref: "Ésaïe 9:5", texte: "Car un enfant nous est né, un fils nous a été donné, et la domination reposera sur son épaule ; on l'appellera Admirable, Conseiller, Dieu puissant, Père éternel, Prince de la paix." },
  { ref: "1 Corinthiens 15:57", texte: "Mais grâces soient rendues à Dieu, qui nous donne la victoire par notre Seigneur Jésus-Christ !" },
  { ref: "Psaume 28:7", texte: "L'Éternel est ma force et mon bouclier ; en lui mon cœur se confie, et je suis secouru ; aussi mon cœur est dans l'allégresse, et je le loue par mes cantiques." },
  { ref: "Ésaïe 57:15", texte: "Car ainsi parle le Très-Haut, dont la demeure est éternelle et dont le nom est saint : J'habite dans les lieux élevés et dans la sainteté ; mais je suis avec l'homme brisé et humilié, afin de ranimer les esprits humiliés, afin de ranimer les cœurs brisés." },
  { ref: "Jean 6:35", texte: "Jésus leur dit : Je suis le pain de vie. Celui qui vient à moi n'aura jamais faim, et celui qui croit en moi n'aura jamais soif." },
  { ref: "Psaume 145:3", texte: "L'Éternel est grand et très digne de louange, et sa grandeur est insondable." },
  { ref: "Proverbes 4:23", texte: "Garde ton cœur plus que toute autre chose, car de lui viennent les sources de la vie." },
  { ref: "Galates 2:20", texte: "J'ai été crucifié avec Christ ; et si je vis, ce n'est plus moi qui vis, c'est Christ qui vit en moi ; si je vis maintenant dans la chair, je vis dans la foi au Fils de Dieu, qui m'a aimé et qui s'est livré lui-même pour moi." },
  { ref: "Psaume 34:8", texte: "Goûtez et voyez combien l'Éternel est bon ! Heureux l'homme qui cherche en lui son refuge !" },
  { ref: "Matthieu 5:3", texte: "Heureux les pauvres en esprit, car le royaume des cieux est à eux !" },
  { ref: "Romains 6:23", texte: "Car le salaire du péché, c'est la mort ; mais le don gratuit de Dieu, c'est la vie éternelle en Jésus-Christ notre Seigneur." },
  { ref: "2 Pierre 3:9", texte: "Le Seigneur ne tarde pas dans l'accomplissement de sa promesse, comme quelques-uns le croient ; mais il use de patience envers vous, ne voulant pas qu'aucun périsse, mais voulant que tous arrivent à la repentance." },
  { ref: "Psaume 18:2", texte: "L'Éternel est mon rocher, ma forteresse, mon libérateur ; mon Dieu est le rocher où je trouve un abri, mon bouclier et la force qui me sauve, ma haute retraite." },
  { ref: "Jean 15:13", texte: "Il n'y a pas de plus grand amour que de donner sa vie pour ses amis." },
  { ref: "Colossiens 1:16-17", texte: "Car en lui ont été créées toutes les choses qui sont dans les cieux et sur la terre, les visibles et les invisibles… tout a été créé par lui et pour lui. Il est avant toutes choses, et toutes choses subsistent en lui." },
  { ref: "2 Corinthiens 12:9", texte: "Ma grâce te suffit, car ma puissance s'accomplit dans la faiblesse. C'est pourquoi je me glorifierai bien plutôt de mes faiblesses, afin que la puissance de Christ repose sur moi." },
  { ref: "Psaume 86:5", texte: "Car tu es bon, Seigneur, tu pardonnes, et tu es plein de bonté pour tous ceux qui t'invoquent." },
  { ref: "Ésaïe 61:1", texte: "L'Esprit du Seigneur, l'Éternel, est sur moi, car l'Éternel m'a oint pour apporter de bonnes nouvelles aux malheureux, il m'a envoyé pour panser ceux qui ont le cœur brisé." },
  { ref: "Matthieu 18:20", texte: "Car là où deux ou trois sont assemblés en mon nom, je suis au milieu d'eux." },
  { ref: "1 Corinthiens 6:19-20", texte: "Ne savez-vous pas que votre corps est le temple du Saint-Esprit qui est en vous, que vous avez reçu de Dieu, et que vous ne vous appartenez pas à vous-mêmes ? Car vous avez été rachetés à un grand prix." },
  { ref: "Ésaïe 48:17", texte: "Ainsi parle l'Éternel, ton Rédempteur, le Saint d'Israël : C'est moi, l'Éternel, ton Dieu, qui t'enseigne pour ton profit, qui te conduis par le chemin que tu dois suivre." },
  { ref: "Psaume 147:3", texte: "Il guérit ceux qui ont le cœur brisé, et il panse leurs blessures." },
  { ref: "Romains 10:9", texte: "Si tu confesses de ta bouche le Seigneur Jésus, et si tu crois dans ton cœur que Dieu l'a ressuscité des morts, tu seras sauvé." },
  { ref: "Jean 4:24", texte: "Dieu est Esprit, et il faut que ceux qui l'adorent l'adorent en esprit et en vérité." },
  { ref: "Psaume 139:23-24", texte: "Sonde-moi, ô Dieu, et connais mon cœur ! Éprouve-moi, et connais mes pensées ! Regarde si je suis sur une mauvaise voie, et conduis-moi sur la voie éternelle !" },
  { ref: "Ésaïe 40:11", texte: "Il paît son troupeau comme un berger, il réunit les agneaux dans ses bras ; il les porte sur son sein, il mène doucement les brebis qui allaitent." },
  { ref: "Actes 2:17", texte: "Dans les derniers jours, dit Dieu, je répandrai de mon Esprit sur toute chair ; vos fils et vos filles prophétiseront, vos jeunes gens auront des visions, et vos vieillards auront des songes." },
  { ref: "Nombres 6:24-26", texte: "Que l'Éternel te bénisse et te garde ! Que l'Éternel fasse luire sa face sur toi, et qu'il t'accorde sa grâce ! Que l'Éternel tourne sa face vers toi, et qu'il te donne la paix !" },
  { ref: "Jean 13:34", texte: "Je vous donne un commandement nouveau : Aimez-vous les uns les autres ; comme je vous ai aimés, vous aussi, aimez-vous les uns les autres." },
  { ref: "Psaume 91:11", texte: "Car il donnera des ordres à ses anges à ton sujet, pour te garder dans toutes tes voies." },
  { ref: "Matthieu 5:9", texte: "Heureux les artisans de paix, car ils seront appelés fils de Dieu !" },
  { ref: "2 Corinthiens 3:17", texte: "Or, le Seigneur c'est l'Esprit ; et là où est l'Esprit du Seigneur, là est la liberté." },
  { ref: "Proverbes 31:25", texte: "Elle est revêtue de force et de magnificence, et elle se rit de l'avenir." },
  { ref: "Psaume 29:11", texte: "L'Éternel donne la force à son peuple, l'Éternel bénit son peuple et lui donne la paix." },
  { ref: "1 Rois 19:12", texte: "Après le feu, une voix douce et légère." },
  { ref: "Éphésiens 2:8-9", texte: "Car c'est par la grâce que vous êtes sauvés, par le moyen de la foi. Et cela ne vient pas de vous, c'est le don de Dieu. Ce n'est point par les œuvres, afin que personne ne se glorifie." },
  { ref: "Psaume 56:3", texte: "Le jour où je crains, moi, en toi je me confie." },
  { ref: "Jean 17:17", texte: "Sanctifie-les par ta vérité : ta parole est la vérité." },
  { ref: "Romans 3:23-24", texte: "Car tous ont péché et sont privés de la gloire de Dieu ; et ils sont gratuitement justifiés par sa grâce, par le moyen de la rédemption qui est en Jésus-Christ." },
  { ref: "Psaume 84:10", texte: "Un seul jour dans tes parvis vaut mieux que mille. J'aimerais mieux être à la porte de la maison de mon Dieu que d'habiter dans les tentes de la méchanceté." },
  { ref: "Luc 1:37", texte: "Car rien n'est impossible à Dieu." },
  { ref: "Actes 4:12", texte: "Il n'y a de salut en aucun autre ; car il n'y a sous le ciel aucun autre nom qui ait été donné parmi les hommes, par lequel nous devions être sauvés." },
  { ref: "Psaume 19:1", texte: "Les cieux racontent la gloire de Dieu, et l'étendue manifeste l'œuvre de ses mains." },
  { ref: "Deutéronome 6:5", texte: "Tu aimeras l'Éternel, ton Dieu, de tout ton cœur, de toute ton âme et de toute ta force." },
  { ref: "Matthieu 22:37-39", texte: "Tu aimeras le Seigneur, ton Dieu, de tout ton cœur, de toute ton âme, et de toute ta pensée. C'est le premier et le plus grand commandement. Et voici le second, qui lui est semblable : Tu aimeras ton prochain comme toi-même." },
  { ref: "Psaume 150:6", texte: "Que tout ce qui respire loue l'Éternel ! Louez l'Éternel !" },
  { ref: "Romains 8:11", texte: "Et si l'Esprit de celui qui a ressuscité Jésus d'entre les morts habite en vous, celui qui a ressuscité Christ d'entre les morts rendra aussi la vie à vos corps mortels par son Esprit qui habite en vous." },
  { ref: "Ésaïe 30:18", texte: "C'est pourquoi l'Éternel attend le moment d'être propice ; c'est pourquoi il s'élève pour vous faire grâce. Car l'Éternel est un Dieu d'équité. Heureux tous ceux qui espèrent en lui !" },
  { ref: "Jean 5:24", texte: "En vérité, en vérité, je vous le dis, celui qui entend ma parole et qui croit à celui qui m'a envoyé, a la vie éternelle et ne vient pas en jugement, mais il est passé de la mort à la vie." },
  { ref: "Psaume 37:23-24", texte: "L'Éternel affermit les pas de l'homme et prend plaisir en sa voie. Quand il tombe, il ne reste pas à terre, car l'Éternel soutient sa main." },
  { ref: "Hébreux 6:18", texte: "Afin que, par deux choses immuables dans lesquelles il est impossible que Dieu mente, nous trouvions un puissant encouragement, nous dont le refuge a été de saisir l'espérance proposée." },
  { ref: "1 Timothée 6:6", texte: "Or, la piété avec le contentement est un grand gain." },
  { ref: "Psaume 9:9", texte: "L'Éternel est aussi un refuge pour l'opprimé, un refuge aux temps de détresse." },
  { ref: "Jacques 4:8", texte: "Approchez-vous de Dieu, et il s'approchera de vous." },
  { ref: "Proverbes 17:22", texte: "Un cœur joyeux est un bon remède, mais un esprit abattu dessèche les os." },
  { ref: "Psaume 130:3-4", texte: "Si tu gardais le souvenir des iniquités, Éternel, Seigneur, qui pourrait subsister ? Mais le pardon se trouve auprès de toi, afin qu'on te craigne." },
  { ref: "2 Corinthiens 4:17", texte: "Car nos légères afflictions du moment présent produisent pour nous, au-delà de toute mesure, un poids éternel de gloire." },
  { ref: "Jean 20:29", texte: "Jésus lui dit : Parce que tu m'as vu, tu as cru. Heureux ceux qui n'ont pas vu, et qui ont cru !" },
  { ref: "Psaume 42:1-2", texte: "Comme une biche soupire après des courants d'eau, ainsi mon âme soupire après toi, ô Dieu ! Mon âme a soif de Dieu, du Dieu vivant." },
  { ref: "Ésaïe 43:1", texte: "Et maintenant, ainsi parle l'Éternel qui t'a créé, ô Jacob, qui t'a formé, ô Israël ! Ne crains pas, car je te rachète, je t'appelle par ton nom : tu es à moi !" },
  { ref: "Romains 8:26", texte: "De même aussi l'Esprit nous aide dans notre faiblesse, car nous ne savons pas ce qu'il nous convient de demander dans nos prières. Mais l'Esprit lui-même intercède par des soupirs inexprimables." },
  { ref: "Psaume 34:1", texte: "Je bénirai l'Éternel en tout temps ; sa louange sera toujours dans ma bouche." },
  { ref: "Colossiens 4:2", texte: "Persévérez dans la prière, veillez-y avec actions de grâces." },
  { ref: "Jean 7:38", texte: "Celui qui croit en moi, des fleuves d'eau vive couleront de son sein, comme dit l'Écriture." },
  { ref: "Psaume 5:3", texte: "Éternel, tu entends ma voix le matin ; dès le matin je me présente à toi, et j'attends." },
  { ref: "Matthieu 5:14", texte: "Vous êtes la lumière du monde. Une ville située sur une montagne ne peut être cachée." },
  { ref: "Éphésiens 4:32", texte: "Soyez bons les uns envers les autres, compatissants, vous pardonnant réciproquement, comme Dieu vous a pardonné en Christ." },
  { ref: "Psaume 126:5-6", texte: "Ceux qui sèment avec larmes moissonneront avec chants de joie. Celui qui marche en pleurant, quand il porte la semence, reviendra avec allégresse, quand il portera ses gerbes." },
  { ref: "2 Chroniques 7:14", texte: "Si mon peuple sur qui est invoqué mon nom s'humilie, prie, et cherche ma face, et s'il se détourne de ses mauvaises voies, je l'exaucerai des cieux, je lui pardonnerai son péché, et je guérirai son pays." },
  { ref: "Psaume 37:7", texte: "Reste en repos devant l'Éternel et espère en lui ; ne t'irrite pas contre celui qui réussit dans ses voies, contre l'homme qui vient à bout de ses mauvais desseins." },
  { ref: "1 Jean 3:1", texte: "Voyez quel amour le Père nous a témoigné, pour que nous soyons appelés enfants de Dieu ! Et nous le sommes." },
  { ref: "Psaume 63:3", texte: "Car ta bonté vaut mieux que la vie ; mes lèvres te glorifieront." },
  { ref: "Jean 10:27-28", texte: "Mes brebis entendent ma voix ; je les connais, et elles me suivent. Je leur donne la vie éternelle ; elles ne périront jamais, et personne ne les ravira de ma main." },
  { ref: "Ésaïe 58:11", texte: "Et l'Éternel te conduira continuellement, il rassasiera ton âme dans les lieux desséchés, il donnera de la vigueur à tes os ; et tu seras comme un jardin arrosé, comme une source dont les eaux ne tarissent point." },
  { ref: "Psaume 138:8", texte: "L'Éternel accomplira tout ce qui me concerne ! Éternel, ta bonté est éternelle ; n'abandonne pas les œuvres de tes mains !" },
  { ref: "Ésaïe 44:22", texte: "J'efface tes transgressions comme un nuage, et tes péchés comme une nuée. Reviens à moi, car je te rachète." },
  { ref: "Psaume 91:4", texte: "Il te couvrira de ses plumes, et tu trouveras un refuge sous ses ailes ; sa fidélité est un bouclier et une armure." },
  { ref: "Matthieu 9:22", texte: "Jésus se retourna, et en la voyant, il dit : Aie bon courage, ma fille ; ta foi t'a guérie." },
  { ref: "1 Corinthiens 16:14", texte: "Que tout ce que vous faites se fasse avec charité." },
  { ref: "Psaume 23:4", texte: "Quand je marche dans la vallée de l'ombre de la mort, je ne crains aucun mal, car tu es avec moi." },
  { ref: "Luc 11:9", texte: "Moi, je vous dis : Demandez, et l'on vous donnera ; cherchez, et vous trouverez ; frappez, et l'on vous ouvrira." },
  { ref: "Ésaïe 7:14", texte: "C'est pourquoi le Seigneur lui-même vous donnera un signe, voici, la vierge sera enceinte et enfantera un fils, et elle lui donnera le nom d'Emmanuel." },
  { ref: "Psaume 50:15", texte: "Invoque-moi au jour de la détresse ; je te délivrerai, et tu me glorifieras." },
  { ref: "Romains 8:15", texte: "Vous n'avez pas reçu un esprit de servitude pour être encore dans la crainte ; mais vous avez reçu un Esprit d'adoption, par lequel nous crions : Abba ! Père !" },
  { ref: "Jean 8:12", texte: "Jésus leur parla de nouveau, et dit : Je suis la lumière du monde ; celui qui me suit ne marchera pas dans les ténèbres, mais il aura la lumière de la vie." },
  { ref: "Psaume 31:14-15", texte: "Mais moi, j'ai confiance en toi, Éternel ! Je dis : Tu es mon Dieu ! Mon sort est entre tes mains." },
  { ref: "Proverbes 3:9-10", texte: "Honore l'Éternel avec tes biens, et avec les prémices de tout ton revenu ; et tes greniers seront remplis d'abondance, et tes cuves regorgèrent de vin nouveau." },
  { ref: "2 Rois 6:16", texte: "Élisée dit : Ne crains pas, car ceux qui sont avec nous sont en plus grand nombre que ceux qui sont avec eux." },
  { ref: "Psaume 108:4", texte: "Car ta grâce s'élève jusqu'aux cieux, et ta fidélité jusqu'aux nues." },
  { ref: "Ésaïe 40:1", texte: "Consolez, consolez mon peuple, dit votre Dieu." },
  { ref: "Matthieu 26:41", texte: "Veillez et priez, afin que vous ne tombiez pas dans la tentation ; l'esprit est bien disposé, mais la chair est faible." },
  { ref: "1 Jean 4:4", texte: "Vous, petits enfants, vous êtes de Dieu, et vous les avez vaincus, parce que celui qui est en vous est plus grand que celui qui est dans le monde." },
  { ref: "Psaume 116:1-2", texte: "J'aime l'Éternel, car il a entendu ma voix, mes supplications ; car il a incliné vers moi son oreille, et je l'invoquerai toute ma vie." },
  { ref: "Colossiens 3:15", texte: "Et que la paix de Christ, à laquelle vous avez été appelés pour former un seul corps, règne dans vos cœurs. Et soyez reconnaissants." },
  { ref: "Psaume 48:14", texte: "Car c'est ici notre Dieu, notre Dieu pour toujours et à jamais ; il nous conduira jusqu'à la mort." },
  { ref: "Jean 15:7", texte: "Si vous demeurez en moi, et que mes paroles demeurent en vous, demandez ce que vous voudrez, et cela vous sera accordé." },
  { ref: "Néhémie 8:10", texte: "Ne vous attristez pas, car la joie de l'Éternel sera votre force." },
  { ref: "Psaume 136:1", texte: "Célébrez l'Éternel, car il est bon, car sa miséricorde dure à toujours !" },
  { ref: "Actes 16:31", texte: "Crois au Seigneur Jésus, et tu seras sauvé, toi et ta famille." },
  { ref: "Psaume 68:5", texte: "Père des orphelins et juge des veuves : tel est Dieu dans la demeure de sa sainteté." },
  { ref: "2 Rois 20:5", texte: "Voici, je te guéris ; dans trois jours tu monteras au temple de l'Éternel." },
  { ref: "Éphésiens 1:3", texte: "Béni soit Dieu, le Père de notre Seigneur Jésus-Christ, qui nous a bénis de toutes sortes de bénédictions spirituelles dans les lieux célestes en Christ !" },
  { ref: "Psaume 30:5", texte: "Car sa colère dure un moment, mais sa grâce dure toute la vie ; les pleurs durent pendant la nuit, mais au matin éclate la joie." },
  { ref: "Ésaïe 54:17", texte: "Aucune arme forgée contre toi ne réussira, et tu condamneras toute langue qui s'élèvera en jugement contre toi. Tel est l'héritage des serviteurs de l'Éternel." },
  { ref: "Jean 15:16", texte: "Ce n'est pas vous qui m'avez choisi ; mais moi, je vous ai choisis, et je vous ai établis, afin que vous alliez, et que vous portiez du fruit, et que votre fruit demeure." },
  { ref: "Psaume 71:5", texte: "Car tu es mon espérance, Seigneur Éternel, tu es ma confiance dès ma jeunesse." },
  { ref: "Romains 4:20-21", texte: "Il ne chancela pas dans sa foi en considérant son corps comme déjà mort ; mais il fut fortifié dans sa foi, donnant gloire à Dieu, pleinement convaincu que ce que Dieu a promis, il est aussi puissant pour l'exécuter." },
  { ref: "Lamentations 3:25", texte: "L'Éternel est bon pour qui espère en lui, pour l'âme qui le cherche." },
  { ref: "Psaume 112:4", texte: "Une lumière se lève dans les ténèbres pour les hommes droits ; il est miséricordieux, compatissant et juste." },
  { ref: "Jean 14:2-3", texte: "Il y a plusieurs demeures dans la maison de mon Père. Si cela n'était pas, je vous l'aurais dit. Je vais vous préparer une place. Et lorsque je m'en serai allé, et que je vous aurai préparé une place, je reviendrai, et je vous prendrai avec moi." },
  { ref: "Psaume 7:17", texte: "Je louerai l'Éternel selon sa justice, je célébrerai le nom de l'Éternel, le Très-Haut." },
  { ref: "Actes 2:21", texte: "Et quiconque invoquera le nom du Seigneur sera sauvé." },
  { ref: "Proverbes 10:22", texte: "La bénédiction de l'Éternel enrichit, et il n'y ajoute point de tristesse." },
  { ref: "Psaume 25:4-5", texte: "Éternel, fais-moi connaître tes voies, enseigne-moi tes sentiers. Conduis-moi dans ta vérité, et instruis-moi ; car tu es le Dieu de mon salut." },
  { ref: "Hébreux 10:23", texte: "Retenons fermement la profession de notre espérance sans vaciller, car celui qui a fait la promesse est fidèle." },
  { ref: "Psaume 119:11", texte: "Je serre ta parole dans mon cœur, afin de ne pas pécher contre toi." },
  { ref: "Matthieu 6:34", texte: "Ne vous inquiétez donc pas du lendemain ; car le lendemain aura soin de lui-même. À chaque jour suffit sa peine." },
  { ref: "1 Chroniques 29:11", texte: "À toi, Éternel, la grandeur, la force et la magnificence, la durée et la gloire ! Car tout ce qui est dans le ciel et sur la terre t'appartient. À toi, Éternel, le règne, et la souveraineté suprême." },
  { ref: "Psaume 93:1", texte: "L'Éternel règne, il est revêtu de majesté ; l'Éternel est revêtu, il est ceint de force." },
  { ref: "Sophonie 3:17", texte: "L'Éternel, ton Dieu, est au milieu de toi, comme un héros qui sauve ; il fera de toi sa plus grande joie, il te renouvellera par son amour, il se réjouira sur toi avec des cris de joie." },
  { ref: "Psaume 119:89", texte: "À toujours, Éternel ! ta parole est établie dans les cieux." },
  { ref: "Jean 3:36", texte: "Celui qui croit au Fils a la vie éternelle ; celui qui ne croit pas au Fils ne verra pas la vie." },
  { ref: "Éphésiens 5:20", texte: "Rendez continuellement grâces pour toutes choses à Dieu le Père, au nom de notre Seigneur Jésus-Christ." },
  { ref: "Psaume 17:8", texte: "Garde-moi comme la prunelle de l'œil, cache-moi à l'ombre de tes ailes." },
  { ref: "Ésaïe 43:25", texte: "Moi, moi, j'efface tes transgressions pour l'amour de moi, et je ne me souviendrai plus de tes péchés." },
  { ref: "Jean 6:51", texte: "Je suis le pain vivant qui est descendu du ciel. Si quelqu'un mange de ce pain, il vivra éternellement." },
  { ref: "Psaume 23:6", texte: "Oui, le bonheur et la grâce m'accompagneront tous les jours de ma vie, et j'habiterai dans la maison de l'Éternel pour la durée des jours." },
  { ref: "Hébreux 11:6", texte: "Or sans la foi il est impossible de lui être agréable ; car il faut que celui qui s'approche de Dieu croie que Dieu existe, et qu'il est le rémunérateur de ceux qui le cherchent." },
  { ref: "Psaume 40:1-2", texte: "J'ai espéré, j'ai espéré en l'Éternel, et il s'est penché vers moi, il a écouté mes cris. Il m'a retiré de la fosse de destruction, du bourbier fangeux ; il a dressé mes pieds sur le roc, affermi mes pas." },
  { ref: "Genèse 28:15", texte: "Je suis avec toi, je te garderai partout où tu iras, et je te ramènerai dans ce pays ; car je ne t'abandonnerai pas." },
  { ref: "Psaume 103:12-13", texte: "Autant l'orient est éloigné de l'occident, autant il éloigne de nous nos transgressions. Comme un père est miséricordieux pour ses enfants, l'Éternel est miséricordieux pour ceux qui le craignent." },
  { ref: "1 Pierre 3:15", texte: "Mais sanctifiez dans vos cœurs Christ le Seigneur, étant toujours prêts à vous défendre, avec douceur et respect, devant quiconque vous demande raison de l'espérance qui est en vous." },
  { ref: "Psaume 31:24", texte: "Soyez forts et que votre cœur ait de la vigueur, vous tous qui espérez en l'Éternel !" },
  { ref: "Ésaïe 55:11", texte: "Ainsi en est-il de ma parole, qui sort de ma bouche : elle ne retourne pas à moi sans effet, sans avoir exécuté ma volonté et accompli ce que j'ai résolu." },
  { ref: "Matthieu 5:5", texte: "Heureux les débonnaires, car ils hériteront la terre !" },
  { ref: "Psaume 19:14", texte: "Que les paroles de ma bouche et les méditations de mon cœur soient agréables devant toi, Éternel, mon rocher et mon rédempteur !" },
  { ref: "Jean 12:46", texte: "Moi, je suis venu dans le monde comme une lumière, afin que quiconque croit en moi ne demeure pas dans les ténèbres." },
  { ref: "Romains 12:1", texte: "Je vous exhorte donc, frères, par les compassions de Dieu, à offrir vos corps comme un sacrifice vivant, saint, agréable à Dieu, ce qui sera de votre part un culte raisonnable." },
  { ref: "Psaume 145:9", texte: "L'Éternel est bon envers tous, et ses compassions s'étendent sur toutes ses œuvres." },
  { ref: "Romains 5:3-4", texte: "Nous nous glorifions même des afflictions, sachant que l'affliction produit la patience, la patience l'expérience, l'expérience l'espérance." },
  { ref: "Psaume 57:10", texte: "Car ta grâce est grande jusqu'aux cieux, ta fidélité jusqu'aux nues." },
  { ref: "Michée 6:8", texte: "On t'a fait connaître, ô homme, ce qui est bien ; et ce que l'Éternel demande de toi, c'est que tu pratiques la justice, que tu aimes la miséricorde, et que tu marches humblement avec ton Dieu." },
  { ref: "Psaume 8:3-4", texte: "Quand je contemple les cieux, ouvrage de tes mains, la lune et les étoiles que tu as créées : Qu'est-ce que l'homme, pour que tu te souviennes de lui ? Et le fils de l'homme, pour que tu prennes garde à lui ?" },
  { ref: "Jean 17:3", texte: "Or, la vie éternelle, c'est qu'ils te connaissent, toi, le seul vrai Dieu, et celui que tu as envoyé, Jésus-Christ." },
  { ref: "2 Corinthiens 9:8", texte: "Et Dieu peut vous combler de toutes grâces, afin que, possédant toujours en toutes choses de quoi satisfaire à tous vos besoins, vous abondiez pour toute bonne œuvre." },
  { ref: "Psaume 36:5", texte: "Ta bonté, Éternel, s'étend jusqu'aux cieux, ta fidélité jusqu'aux nuées." },
  { ref: "Ésaïe 12:2", texte: "Voici, Dieu est ma délivrance, je m'assurerai et je ne craindrai pas, car ma force et ma chanson, c'est l'Éternel, l'Éternel : il a été ma délivrance." },
  { ref: "Galates 6:9", texte: "Ne nous lassons pas de faire le bien ; car nous moissonnerons au temps convenable, si nous ne nous relâchons pas." },
  { ref: "Psaume 72:18-19", texte: "Béni soit l'Éternel Dieu, le Dieu d'Israël, qui seul fait des prodiges ! Béni soit à jamais son nom glorieux ! Que toute la terre soit remplie de sa gloire !" },
  { ref: "Actes 17:28", texte: "Car en lui nous avons la vie, le mouvement, et l'être." },
  { ref: "Psaume 118:24", texte: "C'est ici la journée que l'Éternel a faite : qu'elle soit pour nous un sujet d'allégresse et de joie !" },
  { ref: "Ésaïe 46:4", texte: "Jusqu'à votre vieillesse je serai le même, et jusqu'à votre vieux âge je vous porterai ; je l'ai fait, et je vous porterai, je vous soutiendrai et je vous délivrerai." },
  { ref: "Jean 15:9", texte: "Comme le Père m'a aimé, je vous ai aussi aimés. Demeurez dans mon amour." },
  { ref: "Psaume 86:12", texte: "Je te louerai, Seigneur, mon Dieu, de tout mon cœur, et je glorifierai ton nom pour toujours." },
  { ref: "Matthieu 5:7", texte: "Heureux les miséricordieux, car ils obtiendront miséricorde !" },
  { ref: "Colossiens 2:9-10", texte: "Car en lui habite corporellement toute la plénitude de la divinité. Vous avez tout pleinement en lui, qui est le chef de toute domination et de toute autorité." },
  { ref: "Psaume 37:39", texte: "Le salut des justes vient de l'Éternel ; il est leur refuge au temps de la détresse." },
  { ref: "Ésaïe 43:4", texte: "Parce que tu as du prix à mes yeux, parce que tu es précieux et que je t'aime, je donne des hommes à ta place, et des peuples pour ta vie." },
  { ref: "Romains 11:33", texte: "Ô profondeur de la richesse, de la sagesse et de la science de Dieu ! Que ses jugements sont insondables, et ses voies incompréhensibles !" },
  { ref: "Psaume 68:19-20", texte: "Béni soit le Seigneur ! Chaque jour il nous comble de bienfaits, le Dieu qui est notre délivrance. Ce Dieu est pour nous un Dieu qui sauve ; c'est de l'Éternel, le Seigneur, que vient la délivrance de la mort." },
  { ref: "Tite 3:5", texte: "Il nous a sauvés, non à cause des œuvres de justice que nous aurions faites, mais selon sa miséricorde, par le bain de la régénération et le renouvellement du Saint-Esprit." },
  { ref: "Psaume 13:5-6", texte: "Moi, je me confie en ta grâce, mon cœur est dans la joie de ton salut ; je chante à l'Éternel, car il m'a accordé ses bienfaits." },
  { ref: "Deutéronome 33:27", texte: "Dieu est un refuge, depuis toujours, sous ses bras éternels." },
  { ref: "Psaume 33:18", texte: "Voici, l'œil de l'Éternel est sur ceux qui le craignent, sur ceux qui espèrent en sa grâce." },
  { ref: "Jean 14:13", texte: "Et tout ce que vous demanderez en mon nom, je le ferai, afin que le Père soit glorifié dans le Fils." },
  { ref: "Psaume 89:1", texte: "Je chanterai éternellement les grâces de l'Éternel ; j'annoncerai ta fidélité de bouche en bouche, de génération en génération." },
  { ref: "Ésaïe 40:4", texte: "Que toute vallée soit relevée, toute montagne et toute colline abaissée, que les endroits escarpés deviennent des plaines, et les lieux montagneux des plaines." },
  { ref: "Psaume 100:1-2", texte: "Poussez vers l'Éternel des cris de joie, vous, toute la terre ! Servez l'Éternel avec joie, venez en sa présence avec des chants d'allégresse !" },
  { ref: "1 Rois 3:14", texte: "Si tu marches dans mes voies, si tu observes mes lois et mes commandements, comme a marché David, ton père, je prolongerai tes jours." },
  { ref: "Psaume 111:10", texte: "La crainte de l'Éternel est le commencement de la sagesse ; tous ceux qui l'observent ont une raison saine. Sa louange subsiste à toujours." },
  { ref: "Jean 21:25", texte: "Il y a encore beaucoup d'autres choses que Jésus a faites, et qui, si on les écrivait en détail, je pense que le monde entier ne pourrait pas contenir les livres qu'on écrirait." },
  { ref: "Psaume 145:13", texte: "Ton règne est un règne de tous les siècles, et ta domination subsiste dans tous les âges." },
  { ref: "Romains 8:31", texte: "Que dirons-nous donc de plus ? Si Dieu est pour nous, qui sera contre nous ?" },
  { ref: "Psaume 22:3", texte: "Toi qui es saint, qui habites au milieu des louanges d'Israël." },
  { ref: "Ézéchiel 37:14", texte: "Je mettrai mon esprit en vous, et vous vivrez ; je vous établirai dans votre pays, et vous saurez que c'est moi, l'Éternel, qui ai parlé et qui ai agi, dit l'Éternel." },
  { ref: "Psaume 149:4", texte: "Car l'Éternel prend plaisir en son peuple, il glorifie les humbles par la délivrance." },
  { ref: "2 Samuel 22:3", texte: "Mon Dieu est mon rocher où je cherche un abri, mon bouclier et la force qui me sauve, ma haute retraite et mon refuge. Mon sauveur, tu me délivres de la violence." },
  { ref: "Matthieu 19:26", texte: "Jésus les regarda et dit : Aux hommes cela est impossible, mais à Dieu tout est possible." },
  { ref: "Psaume 28:8", texte: "L'Éternel est la force de son peuple, le refuge et le salut de son oint." },
  { ref: "Actes 10:38", texte: "Comment Dieu a oint du Saint-Esprit et de force Jésus de Nazareth, qui allait de lieu en lieu faisant du bien et guérissant tous ceux qui étaient sous l'empire du diable, car Dieu était avec lui." },
  { ref: "Psaume 16:8", texte: "J'ai constamment l'Éternel sous mes yeux ; lorsqu'il est à ma droite, je ne chancelle pas." },
  { ref: "Genèse 17:1", texte: "Je suis le Dieu tout-puissant. Marche en ma présence, et sois intègre." },
  { ref: "Psaume 119:130", texte: "La révélation de tes paroles éclaire, elle donne de l'intelligence aux simples." },
  { ref: "Ésaïe 60:1", texte: "Lève-toi, sois illuminée ; car ta lumière est venue, et la gloire de l'Éternel s'est levée sur toi." },
  { ref: "Luc 19:10", texte: "Car le Fils de l'homme est venu chercher et sauver ce qui était perdu." },
  { ref: "Psaume 92:2-3", texte: "Il est bon de louer l'Éternel, et de chanter en l'honneur de ton nom, ô Toi qui es le Très-Haut ! De publier le matin ta grâce, et ta fidélité durant les nuits." },
  { ref: "Romains 14:8", texte: "Car si nous vivons, nous vivons pour le Seigneur, et si nous mourons, nous mourons pour le Seigneur. Soit donc que nous vivions, soit que nous mourions, nous sommes au Seigneur." },
  { ref: "Psaume 90:2", texte: "Avant que les montagnes fussent nées, et que tu eusses créé la terre et le monde, d'éternité en éternité tu es Dieu." },
  { ref: "Ésaïe 43:7", texte: "Celui qui est appelé de mon nom, que j'ai créé pour ma gloire, que j'ai formé et que j'ai fait." },
  { ref: "Matthieu 5:10", texte: "Heureux ceux qui sont persécutés pour la justice, car le royaume des cieux est à eux !" },
  { ref: "Psaume 103:17", texte: "Mais la grâce de l'Éternel dure de toute éternité et à toujours pour ceux qui le craignent, et sa justice pour les enfants de leurs enfants." },
  { ref: "Jean 6:37", texte: "Tout ce que le Père me donne viendra à moi, et je ne mettrai pas dehors celui qui vient à moi." },
  { ref: "Ésaïe 54:10", texte: "Les montagnes se déplaceront et les collines chancelleront, mais ma grâce ne s'éloignera pas de toi, et mon alliance de paix ne chancellera pas, dit l'Éternel, qui a pitié de toi." },
  { ref: "Psaume 84:5", texte: "Heureux l'homme dont tu es la force ! Dans son cœur sont les chemins de Sion." },
  { ref: "Hébreux 13:20-21", texte: "Que le Dieu de paix, qui a ramené d'entre les morts notre Seigneur Jésus, le grand pasteur des brebis, par le sang d'une alliance éternelle, vous rende capables de toute bonne œuvre pour l'accomplissement de sa volonté." },
  { ref: "Psaume 62:2", texte: "Oui, c'est en Dieu que réside mon salut et ma gloire, mon rocher fort, mon refuge." },
  { ref: "1 Corinthiens 1:30", texte: "Or, c'est par lui que vous êtes en Jésus-Christ, lui qui, de par Dieu, a été fait pour nous sagesse, justice, sanctification et rédemption." },
  { ref: "Psaume 118:14", texte: "L'Éternel est ma force et mon cantique, et il a été mon salut." },
  { ref: "Jean 3:30", texte: "Il faut qu'il croisse, et que je diminue." },
  { ref: "Philippiens 4:11", texte: "Ce n'est pas que je cherche les dons, mais je cherche ce qui abonde pour votre compte. J'ai appris à être content dans toutes les circonstances où je me trouve." },
  { ref: "Psaume 115:1", texte: "Non pas à nous, Éternel, non pas à nous, mais à ton nom donne la gloire, à cause de ta grâce, à cause de ta fidélité !" },
  { ref: "Ésaïe 41:13", texte: "Car moi, l'Éternel, ton Dieu, je tiens ta main droite, et je te dis : Ne crains pas, je viens à ton secours." },
  { ref: "Psaume 31:3", texte: "Car tu es mon rocher et ma forteresse ; et à cause de ton nom tu me dirigeras et me conduiras." },
  { ref: "2 Corinthiens 5:7", texte: "Car nous marchons par la foi et non par la vue." },
  { ref: "Psaume 76:4", texte: "Tu es éclatant, majestueux, plus que les montagnes éternelles." },
  { ref: "Matthieu 6:8", texte: "Ne leur ressemblez pas, car votre Père sait ce dont vous avez besoin avant que vous le lui demandiez." },
  { ref: "Psaume 46:10", texte: "Arrêtez, et sachez que je suis Dieu : je domine sur les nations, je domine sur la terre." },
  { ref: "Éphésiens 2:4-5", texte: "Mais Dieu, qui est riche en miséricorde, à cause du grand amour dont il nous a aimés, nous a rendus vivants avec Christ, alors que nous étions morts par nos offenses." },
  { ref: "Psaume 145:7", texte: "Ils publieront le souvenir de ta grande bonté, et ils feront retentir les louanges de ta justice." },
  { ref: "1 Jean 5:14-15", texte: "Nous avons auprès de lui cette assurance que si nous demandons quelque chose selon sa volonté, il nous écoute. Et si nous savons qu'il nous écoute, quoi que ce soit que nous demandions, nous savons que nous avons ce que nous lui avons demandé." },
  { ref: "Psaume 33:22", texte: "Que ta grâce, Éternel, soit sur nous, comme notre espoir est en toi !" },
  { ref: "Ésaïe 43:11", texte: "Moi, moi, je suis l'Éternel, et hors moi il n'y a point de sauveur." },
  { ref: "Luc 21:33", texte: "Le ciel et la terre passeront, mais mes paroles ne passeront point." },
  { ref: "Psaume 57:2", texte: "Je crie à Dieu le Très-Haut, à Dieu qui accomplit les choses pour moi." },
  { ref: "Zacharie 4:6", texte: "Ce n'est pas par la puissance ni par la force, mais c'est par mon Esprit, dit l'Éternel des armées." },
  { ref: "Psaume 69:30", texte: "Je louerai le nom de Dieu par un cantique, et je le magnifierai par des actions de grâces." },
  { ref: "Jean 11:40", texte: "Jésus lui dit : Ne t'ai-je pas dit que, si tu crois, tu verras la gloire de Dieu ?" },
  { ref: "Psaume 119:105", texte: "Ta parole est une lampe à mes pieds et une lumière sur mon sentier." },
  { ref: "Matthieu 5:4", texte: "Heureux ceux qui pleurent, car ils seront consolés !" },
  { ref: "1 Corinthiens 2:9", texte: "C'est ce qui est écrit : Ce que l'œil n'a pas vu, ce que l'oreille n'a pas entendu, et ce qui n'est pas monté au cœur de l'homme, Dieu l'a préparé pour ceux qui l'aiment." },
  { ref: "Psaume 40:4", texte: "Heureux l'homme qui a mis sa confiance en l'Éternel, et qui ne regarde pas du côté des orgueilleux." },
  { ref: "Ésaïe 44:3", texte: "Car je répandrai des eaux sur le pays qui a soif, et des ruisseaux sur le terrain desséché ; je répandrai mon Esprit sur ta postérité, et ma bénédiction sur tes rejetons." },
  { ref: "Psaume 34:4", texte: "J'ai cherché l'Éternel, et il m'a répondu ; il m'a délivré de toutes mes frayeurs." },
  { ref: "Jean 6:47", texte: "En vérité, en vérité, je vous le dis, celui qui croit en moi a la vie éternelle." },
  { ref: "Philippiens 1:6", texte: "Étant persuadé que celui qui a commencé en vous cette bonne œuvre la rendra parfaite pour le jour de Jésus-Christ." },
  { ref: "Psaume 20:7", texte: "Les uns mettent leur confiance dans les chars, les autres dans les chevaux ; nous, nous invoquons le nom de l'Éternel, notre Dieu." },
  { ref: "Jérémie 17:7-8", texte: "Béni soit l'homme qui se confie en l'Éternel, et dont l'Éternel est l'espérance ! Il est comme un arbre planté au bord des eaux, qui étend ses racines vers le courant ; il ne craint pas la chaleur quand elle vient." },
  { ref: "Psaume 32:10", texte: "Les douleurs seront nombreuses pour le méchant ; mais celui qui se confie en l'Éternel sera entouré de sa grâce." },
  { ref: "Actes 1:11", texte: "Ce Jésus, qui a été enlevé au ciel du milieu de vous, reviendra de la même manière que vous l'avez vu allant au ciel." },
  { ref: "Psaume 145:14", texte: "L'Éternel soutient tous ceux qui tombent, et il redresse tous ceux qui sont courbés." },
  { ref: "Proverbes 28:26", texte: "Celui qui se confie en son propre cœur est un insensé ; mais celui qui marche dans la sagesse sera délivré." },
  { ref: "Psaume 119:165", texte: "Ceux qui aiment ta loi jouissent d'une grande paix, et il ne leur arrive aucun faux pas." },
  { ref: "Ésaïe 49:15-16", texte: "Une femme oublie-t-elle l'enfant qu'elle allaite ? N'a-t-elle pas compassion du fils de ses entrailles ? Quand elle l'oublierait, moi, je ne t'oublierai pas. Voici, je t'ai gravé sur mes mains." },
  { ref: "Psaume 18:32", texte: "Il est le Dieu qui me ceint de force, et qui rend ma voie sans défaut." },
  { ref: "2 Corinthiens 1:3-4", texte: "Béni soit Dieu, le Père de notre Seigneur Jésus-Christ, le Père des miséricordes, et le Dieu de toute consolation, qui nous console dans toutes nos afflictions, afin que, par la consolation dont nous sommes l'objet de la part de Dieu, nous puissions aussi consoler ceux qui se trouvent dans quelque affliction !" },
  { ref: "Psaume 86:10", texte: "Car tu es grand et tu fais des prodiges ; toi seul tu es Dieu." },
  { ref: "Colossiens 3:23", texte: "Quoi que vous fassiez, faites-le de tout votre cœur, comme pour le Seigneur et non pour des hommes." },
  { ref: "Psaume 56:4", texte: "En Dieu je me confie, je ne crains rien. Que me ferait un homme ?" },
  { ref: "Hébreux 12:28", texte: "C'est pourquoi, puisque nous recevons un royaume inébranlable, pratiquons la reconnaissance, et, au moyen d'elle, rendons à Dieu un culte qui lui soit agréable, avec respect et avec crainte." },
  { ref: "Psaume 99:9", texte: "Exaltez l'Éternel, notre Dieu, et prosternez-vous vers sa montagne sainte ! Car il est saint, l'Éternel, notre Dieu !" },
  { ref: "Jean 1:14", texte: "Et la Parole a été faite chair, et elle a habité parmi nous, pleine de grâce et de vérité ; et nous avons contemplé sa gloire, une gloire comme la gloire du Fils unique venu du Père." },
  { ref: "Psaume 34:17-18", texte: "Les justes crient, et l'Éternel les entend ; il les délivre de toutes leurs détresses. L'Éternel est près de ceux qui ont le cœur brisé, et il sauve ceux dont l'esprit est abattu." },
  { ref: "Ésaïe 40:3", texte: "Une voix crie : Dans le désert, frayez le chemin de l'Éternel, aplanissez dans des lieux déserts une route pour notre Dieu." },
  { ref: "Psaume 23:3", texte: "Il restaure mon âme, il me conduit dans les sentiers de la justice, à cause de son nom." },
  { ref: "Luc 4:18", texte: "L'Esprit du Seigneur est sur moi, parce qu'il m'a oint pour annoncer une bonne nouvelle aux pauvres." },
  { ref: "Psaume 66:18-19", texte: "Si j'avais regardé l'iniquité dans mon cœur, le Seigneur ne m'aurait pas exaucé. Mais certainement Dieu m'a exaucé, il a été attentif à la voix de ma prière." },
  { ref: "Ésaïe 32:17", texte: "Le fruit de la justice sera la paix, et la justice produira un repos perpétuel et une sécurité parfaite." },
  { ref: "Psaume 34:9", texte: "Craignez l'Éternel, vous ses saints ! car rien ne manque à ceux qui le craignent." },
  { ref: "1 Pierre 1:6-7", texte: "En cela vous vous réjouissez, quoique maintenant, puisqu'il le faut, vous soyez attristés pour un peu de temps par diverses épreuves, afin que l'épreuve de votre foi, plus précieuse que l'or périssable (qui cependant est éprouvé par le feu) ait pour résultat la louange, la gloire et l'honneur, lors de la révélation de Jésus-Christ." },
  { ref: "Psaume 43:3", texte: "Envoie ta lumière et ta vérité : qu'elles me guident, qu'elles me conduisent à ta montagne sainte et à ta demeure !" },
  { ref: "Esther 4:14", texte: "Et qui sait si ce n'est pas pour une circonstance comme celle-ci que tu es parvenue à ta position royale ?" },
  { ref: "Psaume 104:33-34", texte: "Je veux chanter à l'Éternel tant que je vivrai, je veux célébrer mon Dieu tant que j'existerai. Que ma méditation lui soit agréable !" },
  { ref: "Apocalypse 22:13", texte: "Je suis l'Alpha et l'Oméga, le premier et le dernier, le commencement et la fin." },
  { ref: "Psaume 9:1", texte: "Je louerai l'Éternel de tout mon cœur, je raconterai toutes tes merveilles." },
  { ref: "Matthieu 14:27", texte: "Aussitôt Jésus leur parla, et dit : Rassurez-vous, c'est moi ; n'ayez pas peur !" },
  { ref: "Psaume 63:1", texte: "O Dieu ! tu es mon Dieu, je te cherche ; mon âme a soif de toi, ma chair soupire après toi, dans une terre aride et desséchée, sans eau." },
  { ref: "Actes 20:24", texte: "Mais je ne fais pour moi-même aucun cas de ma vie, comme si elle m'était précieuse, pourvu que j'accomplisse ma course avec joie, et le ministère que j'ai reçu du Seigneur Jésus, d'annoncer la bonne nouvelle de la grâce de Dieu." },
  { ref: "Psaume 37:25", texte: "J'ai été jeune, et j'ai vieilli ; et je n'ai pas vu le juste abandonné, ni sa postérité mendiant son pain." },
  { ref: "Jean 6:63", texte: "C'est l'esprit qui vivifie ; la chair ne sert de rien. Les paroles que je vous ai dites sont esprit et vie." },
  { ref: "Psaume 11:7", texte: "Car l'Éternel est juste, il aime la justice ; les hommes droits verront sa face." },
  { ref: "Ésaïe 45:22", texte: "Tournez-vous vers moi pour être sauvés, vous toutes les extrémités de la terre ! Car je suis Dieu, et il n'y en a point d'autre." },
  { ref: "Psaume 96:3", texte: "Racontez sa gloire parmi les nations, ses merveilles parmi tous les peuples !" }
];

function getDayOfYear(d) {
  const start = new Date(d.getFullYear(), 0, 0);
  const diff = d - start + ((start.getTimezoneOffset() - d.getTimezoneOffset()) * 60 * 1000);
  return Math.floor(diff / 86400000);
}

const today = new Date();
const totalVersets = VERSETS.length;
const todayIndex = getDayOfYear(today) % totalVersets;
let currentIndex = todayIndex;

// ── FAVORITES ──────────────────────────────────────────
function getFavs() {
  try { return JSON.parse(localStorage.getItem('kam_favs') || '[]'); } catch(e) { return []; }
}
function saveFavs(favs) {
  try { localStorage.setItem('kam_favs', JSON.stringify(favs)); } catch(e) {}
}
function isFav(index) { return getFavs().includes(index); }
function toggleFav(index) {
  let favs = getFavs();
  if (favs.includes(index)) {
    favs = favs.filter(i => i !== index);
    showToast('Retiré des favoris');
  } else {
    favs.push(index);
    showToast('Ajouté aux favoris ♡');
  }
  saveFavs(favs);
  updateFavBtn();
  renderFavList();
}

function updateFavBtn() {
  const btn = document.getElementById('fav-btn');
  if (isFav(currentIndex)) {
    btn.innerHTML = '<span class="icon">♥</span> Favori';
    btn.classList.add('fav-active');
  } else {
    btn.innerHTML = '<span class="icon">♡</span> Favori';
    btn.classList.remove('fav-active');
  }
}

function renderFavList() {
  const favs = getFavs();
  const list = document.getElementById('fav-list');
  if (favs.length === 0) {
    list.innerHTML = '<p class="fav-empty">Tu n\'as pas encore de favoris.<br>Clique sur ♡ pour en ajouter.</p>';
    return;
  }
  list.innerHTML = favs.map(i => {
    const v = VERSETS[i];
    return `<div class="fav-item" data-index="${i}">
      <div class="fav-item-ref">
        <span class="fav-item-remove" data-remove="${i}">✕</span>
        ${v.ref}
      </div>
      <div class="fav-item-text">${v.texte}</div>
    </div>`;
  }).join('');

  list.querySelectorAll('.fav-item').forEach(el => {
    el.addEventListener('click', (e) => {
      if (e.target.dataset.remove !== undefined) return;
      currentIndex = parseInt(el.dataset.index);
      render(currentIndex, true);
      closeFavPanel();
    });
  });
  list.querySelectorAll('[data-remove]').forEach(el => {
    el.addEventListener('click', (e) => {
      e.stopPropagation();
      const idx = parseInt(el.dataset.remove);
      let favs = getFavs().filter(i => i !== idx);
      saveFavs(favs);
      updateFavBtn();
      renderFavList();
    });
  });
}

document.getElementById('fav-btn').addEventListener('click', () => toggleFav(currentIndex));
document.getElementById('fav-open-btn').addEventListener('click', openFavPanel);
document.getElementById('fav-close').addEventListener('click', closeFavPanel);
document.getElementById('overlay').addEventListener('click', closeFavPanel);

function openFavPanel() {
  renderFavList();
  document.getElementById('fav-panel').classList.add('open');
  document.getElementById('overlay').classList.add('open');
}
function closeFavPanel() {
  document.getElementById('fav-panel').classList.remove('open');
  document.getElementById('overlay').classList.remove('open');
}

// ── THEME ──────────────────────────────────────────────
let isLight = localStorage.getItem('kam_theme') === 'light';
function applyTheme() {
  document.body.classList.toggle('light', isLight);
  document.getElementById('theme-btn').textContent = isLight ? '🌙' : '☀️';
}
applyTheme();
document.getElementById('theme-btn').addEventListener('click', () => {
  isLight = !isLight;
  localStorage.setItem('kam_theme', isLight ? 'light' : 'dark');
  applyTheme();
});

// ── SHARE ──────────────────────────────────────────────
function getShareText() {
  const v = VERSETS[currentIndex];
  return `« ${v.texte} » — ${v.ref}`;
}

document.getElementById('share-btn').addEventListener('click', () => {
  const v = VERSETS[currentIndex];
  const text = getShareText();
  const url = encodeURIComponent(window.location.href);
  const encoded = encodeURIComponent(text);
  document.getElementById('whatsapp-btn').href = `https://wa.me/?text=${encoded}`;
  document.getElementById('facebook-btn').href = `https://www.facebook.com/sharer/sharer.php?u=${url}&quote=${encoded}`;
  document.getElementById('share-modal-bg').classList.add('open');
});

document.getElementById('share-cancel').addEventListener('click', () => {
  document.getElementById('share-modal-bg').classList.remove('open');
});
document.getElementById('share-modal-bg').addEventListener('click', (e) => {
  if (e.target === document.getElementById('share-modal-bg'))
    document.getElementById('share-modal-bg').classList.remove('open');
});

document.getElementById('copy-btn').addEventListener('click', () => {
  const text = getShareText();
  navigator.clipboard.writeText(text).then(() => {
    document.getElementById('share-modal-bg').classList.remove('open');
    showToast('Verset copié !');
  }).catch(() => {
    const ta = document.createElement('textarea');
    ta.value = text; document.body.appendChild(ta); ta.select();
    document.execCommand('copy'); document.body.removeChild(ta);
    document.getElementById('share-modal-bg').classList.remove('open');
    showToast('Verset copié !');
  });
});

// ── TOAST ──────────────────────────────────────────────
let toastTimer;
function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  clearTimeout(toastTimer);
  toastTimer = setTimeout(() => t.classList.remove('show'), 2500);
}

// ── RENDER ─────────────────────────────────────────────
function render(index, animate) {
  const v = VERSETS[index];
  const card = document.getElementById('verse-card');
  if (animate) {
    card.style.animation = 'none';
    card.offsetHeight;
    card.style.animation = 'fadeIn 0.6s ease';
  }
  document.getElementById('verse-text').textContent = v.texte;
  document.getElementById('verse-ref').textContent = v.ref;
  document.getElementById('verse-counter').textContent =
    (index === todayIndex ? '★ Aujourd\'hui · ' : '') +
    'N° ' + (index + 1) + ' / ' + totalVersets;
  updateFavBtn();
}

const months = ['janvier','février','mars','avril','mai','juin','juillet','août','septembre','octobre','novembre','décembre'];
const days = ['Dimanche','Lundi','Mardi','Mercredi','Jeudi','Vendredi','Samedi'];
document.getElementById('date-display').textContent =
  days[today.getDay()] + ' ' + today.getDate() + ' ' + months[today.getMonth()] + ' ' + today.getFullYear();

render(currentIndex, false);

document.getElementById('prev-btn').addEventListener('click', () => {
  currentIndex = (currentIndex - 1 + totalVersets) % totalVersets;
  render(currentIndex, true);
});
document.getElementById('next-btn').addEventListener('click', () => {
  currentIndex = (currentIndex + 1) % totalVersets;
  render(currentIndex, true);
});
</script>
</body>
</html>
