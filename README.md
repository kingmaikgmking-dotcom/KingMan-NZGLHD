<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Dashboard Hybride</title>
<style>
  body { font-family: Arial, sans-serif; margin:0; display:flex; background:#f4f4f4; }
  .sidebar { width:220px; background:#222; color:#fff; padding:10px; }
  .sidebar h3 { margin-top:10px; }
  .sidebar ul { list-style:none; padding:0; }
  .sidebar ul li { margin:5px 0; cursor:pointer; }
  .main { flex:1; padding:15px; overflow-y:scroll; height:100vh; }
  .panel { background:#fff; margin-bottom:10px; padding:10px; border:1px solid #ccc; border-radius:5px; }
  .panel h4 { margin:0 0 5px 0; }
  button { margin:2px; }
  .notif-badge { background:red;color:#fff;border-radius:50%;padding:2px 6px;font-size:12px;margin-left:5px; }
  .dark { background:#121212; color:#eee; }
  .compact .panel { padding:5px; font-size:12px; }
  .fullscreen .panel { width:100%; height:400px; }
  .minimal .panel { border:none; box-shadow:none; padding:5px; }
  .fast-read p { line-height:1.2; font-size:14px; }
  .read { opacity:0.5; }
  #popup { position:fixed; top:20px; right:20px; background:#fff; padding:10px; border:1px solid #ccc; }
  .hidden { display:none; }
</style>
</head>
<body>

<!-- Sidebar gauche -->
<div class="sidebar">
  <h3>Menu Principal</h3>
  <ul>
    <li onclick="showPanel('messages')">Messagerie</li>
    <li onclick="showPanel('feed')">Fil</li>
    <li onclick="showPanel('marketplace')">Marketplace</li>
    <li onclick="showPanel('stats')">Statistiques</li>
  </ul>

  <h3>Filtres & Options</h3>
  <label><input type="checkbox" id="show-friends-only"> Amis seulement</label><br>
  <label><input type="checkbox" id="show-ai-recommendations"> Recommandé IA</label><br>
  <button id="toggle-compact">Mode Compact</button>
  <button id="toggle-fullscreen">Plein écran</button>
  <button id="dark-mode-btn">Mode Sombre</button>
  <button id="minimal-btn">Mode Minimal</button>
  <label>Couleur thème: <input type="color" id="theme-color" value="#3498db"></label>
  <button id="refresh-btn">🔄 Actualiser</button>
</div>

<!-- Zone principale -->
<div class="main" id="panel-content">
  <!-- Panneaux dynamiques -->
</div>

<!-- Pop-up exemple -->
<div id="popup" class="hidden">Nouveautés disponibles ! <button id="close-popup">X</button></div>

<!-- Audio notification -->
<audio id="notif-sound" src="notif.mp3"></audio>

<script>
//=== Variables de base ===//
let currentUser = { name:'Oacai', role:'vendeur', favorites:['Post1','ProduitX'] };

//=== Fonctions principales ===//
function showPanel(panel){
  const content = document.getElementById('panel-content');
  content.style.opacity = 0;
  setTimeout(() => {
    content.innerHTML = '';
    if(panel==='messages'){ renderRecentMessages(); renderInteractions(); }
    if(panel==='feed'){ renderTrendingPosts(); renderMustSee(); renderRSSNews(); }
    if(panel==='marketplace'){ renderDailyDeals(); renderTopSelling(); renderFeaturedStores(); renderPopularProducts(); renderWishlist(); renderSuggestions(); }
    if(panel==='stats'){ renderStats(); renderSummary(); }
    content.style.opacity = 1;
  },300);
}

//=== Fonctions pour chaque panel / widget ===//

// Messages récents
const recentMessages = ['Alice : Salut !', 'Bob : Nouvelle photo !'];
function renderRecentMessages(){
  const div = document.createElement('div'); div.className='panel';
  div.innerHTML=`<h4>Messages récents</h4><ul>${recentMessages.map(m=>`<li>${m}</li>`).join('')}</ul>`;
  document.getElementById('panel-content').appendChild(div);
}

// Interactions
const interactions = ['Alice a liké votre post', 'Bob a commenté Story'];
function renderInteractions(){
  const div = document.createElement('div'); div.className='panel';
  div.innerHTML=`<h4>Interactions récentes</h4>${interactions.map(i=>`<p>${i}</p>`).join('')}`;
  document.getElementById('panel-content').appendChild(div);
}

// Fil tendances
const trendingPosts = ['Post1 : 100 likes', 'Post2 : 85 likes'];
function renderTrendingPosts(){
  const div = document.createElement('div'); div.className='panel';
  div.innerHTML=`<h4>Posts tendances</h4><ul>${trendingPosts.map(p=>`<li>${p}</li>`).join('')}</ul>`;
  document.getElementById('panel-content').appendChild(div);
}

// À ne pas manquer
const mustSee = ['Live Lena 18h','Promo Produit X','Story Bob'];
function renderMustSee(){
  const div = document.createElement('div'); div.className='panel';
  div.innerHTML=`<h4>À ne pas manquer</h4><ul>${mustSee.map(i=>`<li>${i}</li>`).join('')}</ul>`;
  document.getElementById('panel-content').appendChild(div);
}

// RSS
const rssNews = ['Titre 1','Titre 2','Titre 3'];
function renderRSSNews(){
  const div = document.createElement('div'); div.className='panel';
  div.innerHTML=`<h4>Actualités RSS</h4><ul>${rssNews.map(r=>`<li>${r}</li>`).join('')}</ul>`;
  document.getElementById('panel-content').appendChild(div);
}

// Marketplace widgets
const dailyDeals = ['Produit A -20%','Produit B -15%','Produit C -10%'];
function renderDailyDeals(){
  const div = document.createElement('div'); div.className='panel';
  div.innerHTML=`<h4>Offres du jour</h4><ul>${dailyDeals.map(d=>`<li>${d}</li>`).join('')}</ul>`;
  document.getElementById('panel-content').appendChild(div);
}
const topSelling = ['Produit X','Produit Y','Produit Z'];
function renderTopSelling(){
  const div = document.createElement('div'); div.className='panel';
  div.innerHTML=`<h4>Produits les plus vendus</h4><ul>${topSelling.map(p=>`<li>${p}</li>`).join('')}</ul>`;
  document.getElementById('panel-content').appendChild(div);
}
const featuredStores = ['Boutique 1','Boutique 2','Boutique 3'];
function renderFeaturedStores(){
  const div = document.createElement('div'); div.className='panel';
  div.innerHTML=`<h4>Boutiques en vedette</h4><ul>${featuredStores.map(s=>`<li>${s}</li>`).join('')}</ul>`;
  document.getElementById('panel-content').appendChild(div);
}
const popularProducts = ['Produit X','Produit Y','Produit Z'];
function renderPopularProducts(){
  const div = document.createElement('div'); div.className='panel';
  div.innerHTML=`<h4>Produits populaires</h4><ul>${popularProducts.map(p=>`<li>${p}</li>`).join('')}</ul>`;
  document.getElementById('panel-content').appendChild(div);
}
const wishlist = ['Produit X','Produit Y'];
function renderWishlist(){
  const div = document.createElement('div'); div.className='panel';
  div.innerHTML=`<h4>Favoris</h4><ul>${wishlist.map(p=>`<li>${p}</li>`).join('')}</ul>`;
  document.getElementById('panel-content').appendChild(div);
}
const suggestions = ['Produit A','Post de Lena','Boutique B'];
function renderSuggestions(){
  const div = document.createElement('div'); div.className='panel';
  div.innerHTML=`<h4>Suggestions personnalisées</h4><ul>${suggestions.map(s=>`<li>${s}</li>`).join('')}</ul>`;
  document.getElementById('panel-content').appendChild(div);
}

// Stats
const stats = { ventes:5, likes:120, commentaires:30 };
function renderStats(){
  const div = document.createElement('div'); div.className='panel';
  div.innerHTML=`<h4>Statistiques</h4><p>Ventes : ${stats.ventes}, Likes : ${stats.likes}, Commentaires : ${stats.commentaires}</p>`;
  document.getElementById('panel-content').appendChild(div);
}

// Résumé du jour
const dailySummary = { messages:10, posts:5, ventes:3 };
function renderSummary(){
  const div = document.createElement('div'); div.className='panel';
  div.innerHTML=`<h4>Résumé du jour</h4><p>Messages : ${dailySummary.messages}, Posts : ${dailySummary.posts}, Ventes : ${dailySummary.ventes}</p>`;
  document.getElementById('panel-content').appendChild(div);
}

//=== Options globales ===//
document.getElementById('dark-mode-btn').addEventListener('click',()=>document.body.classList.toggle('dark'));
document.getElementById('toggle-compact').addEventListener('click',()=>document.body.classList.toggle('compact'));
document.getElementById('toggle-fullscreen').addEventListener('click',()=>document.body.classList.toggle('fullscreen'));
document.getElementById('minimal-btn').addEventListener('click',()=>document.body.classList.toggle('minimal'));
document.getElementById('theme-color').addEventListener('input',e=>{
  document.documentElement.style.setProperty('--theme-color', e.target.value);
});
document.getElementById('refresh-btn').addEventListener('click',()=>{
  showPanel('feed');
  alert('Contenu actualisé !');
});
document.getElementById('close-popup').addEventListener('click',()=>document.getElementById('popup').classList.add('hidden'));

//=== Initialisation ===//
showPanel('feed');

</script>

</body>
</html>
