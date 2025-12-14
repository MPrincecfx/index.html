<!-- =========================
UNION PRESTIGE – V2 CATALOGUE
Files included below:
1) index.html
2) catalogue.html
3) produit.html
4) data.js
========================= -->

<!-- ===== index.html ===== -->
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Union Prestige – Invitations de Luxe</title>
  <style>
    body{margin:0;font-family:Poppins,Arial,sans-serif;background:#0b0b0b;color:#fff}
    header{text-align:center;padding:60px 20px}
    h1{color:#d4af37;font-size:2.8rem}
    p{opacity:.85}
    a.btn{display:inline-block;margin-top:30px;padding:14px 30px;border-radius:30px;background:#d4af37;color:#000;text-decoration:none;font-weight:bold}
  </style>
</head>
<body>
<header>
  <h1>Union Prestige</h1>
  <p>L’élégance commence par une invitation</p>
  <a class="btn" href="catalogue.html">Accéder au catalogue</a>
</header>
</body>
</html>

<!-- ===== catalogue.html ===== -->
<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<title>Catalogue – Union Prestige</title>
<style>
body{margin:0;font-family:Poppins,Arial,sans-serif;background:#0b0b0b;color:#fff}
h2{text-align:center;color:#d4af37;margin:40px 0}
.filters{text-align:center;margin-bottom:30px}
.filters button{margin:5px;padding:10px 20px;border-radius:20px;border:none;background:#222;color:#d4af37;cursor:pointer}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(250px,1fr));gap:20px;padding:20px}
.card{background:#141414;border-radius:15px;padding:15px;text-align:center}
.card img,.card video{width:100%;border-radius:10px}
.card h3{color:#d4af37}
.card a{display:inline-block;margin-top:10px;padding:10px 20px;background:#d4af37;color:#000;border-radius:20px;text-decoration:none}
</style>
<script src="data.js"></script>
</head>
<body>
<h2>Choisissez la carte qui sublimera votre événement</h2>
<div class="filters">
<button onclick="filterPack('Tous')">Tous</button>
<button onclick="filterPack('Essentiel')">Essentiel</button>
<button onclick="filterPack('Élégance')">Élégance</button>
<button onclick="filterPack('Golden')">Golden</button>
</div>
<div class="grid" id="catalogue"></div>
<script>
function render(pack){
 const c=document.getElementById('catalogue');c.innerHTML='';
 cards.filter(x=>pack==='Tous'||x.pack===pack).forEach(card=>{
  c.innerHTML+=`
  <div class='card'>
   ${card.type==='video'?`<video src='images/${card.media}' controls></video>`:`<img src='images/${card.media}'>`}
   <h3>${card.id}</h3>
   <p>Pack ${card.pack}</p>
   <a href='produit.html?id=${card.id}'>Voir détail</a>
  </div>`;
 });
}
function filterPack(p){render(p)}
render('Tous');
</script>
</body>
</html>

<!-- ===== produit.html ===== -->
<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<title>Détail Carte</title>
<style>
body{margin:0;font-family:Poppins,Arial,sans-serif;background:#0b0b0b;color:#fff;text-align:center;padding:40px}
h2{color:#d4af37}
a.btn{display:inline-block;margin-top:20px;padding:12px 25px;background:#d4af37;color:#000;border-radius:25px;text-decoration:none}
</style>
<script src="data.js"></script>
</head>
<body>
<div id="content"></div>
<script>
const id=new URLSearchParams(window.location.search).get('id');
const card=cards.find(c=>c.id===id);
if(card){
 document.getElementById('content').innerHTML=`
 <h2>${card.id}</h2>
 ${card.type==='video'?`<video src='images/${card.media}' controls style='width:80%'></video>`:`<img src='images/${card.media}' style='width:80%'>`}
 <p>Pack ${card.pack}</p>
 <a class='btn' href='https://wa.me/0000000000?text=Bonjour%20Union%20Prestige,%20je%20suis%20intéressé%20par%20la%20carte%20${card.id}%20(Pack%20${card.pack})'>Commander via WhatsApp</a>`;
}
</script>
</body>
</html>

<!-- ===== data.js ===== -->
const cards=[
 {id:'UP-001',pack:'Essentiel',type:'image',media:'carte1.jpg'},
 {id:'UP-002',pack:'Élégance',type:'image',media:'carte2.jpg'},
 {id:'UP-003',pack:'Golden',type:'video',media:'carte3.mp4'}
];
