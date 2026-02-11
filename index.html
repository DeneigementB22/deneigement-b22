<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Calculateur Pieds Carrés Toiture – Déneigement</title>
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
<link rel="stylesheet" href="https://unpkg.com/leaflet-draw@1.0.4/dist/leaflet.draw.css" />
<style>
:root{--primary:#0ea5e9;--secondary:#020617;--accent:#22c55e;--bg:#f1f5f9}
body{font-family:-apple-system,BlinkMacSystemFont,Segoe UI,Roboto;background:#020617;padding:20px;color:#e5e7eb}
.card{max-width:900px;margin:auto;background:var(--bg);color:#020617;padding:24px;border-radius:20px;box-shadow:0 20px 40px rgba(0,0,0,.35)}
h1{text-align:center;margin-bottom:6px}
.subtitle{text-align:center;font-size:14px;color:#475569;margin-bottom:20px}
label{display:block;margin-top:14px;font-weight:600}
input,select{width:100%;padding:12px;margin-top:6px;border-radius:10px;border:1px solid #cbd5f5;font-size:15px}
button{margin-top:12px;padding:10px 14px;font-size:14px;background:linear-gradient(135deg,var(--primary),#38bdf8);color:white;border:none;border-radius:10px;font-weight:bold;cursor:pointer}
.secondary{background:#020617}
.success{background:#16a34a}
.danger{background:#dc2626}
.dark{background:#334155}
.row{display:flex;gap:10px;flex-wrap:wrap}
.result{margin-top:24px;padding:18px;background:#ecfeff;border-radius:14px;font-size:17px;border:2px solid var(--primary)}
.total{font-size:22px;font-weight:800;color:var(--accent);margin-top:10px;text-align:center}
.sub{padding:10px;margin-bottom:8px;border-radius:10px}
</style>
<link rel="manifest" href="manifest.json" />
<meta name="apple-mobile-web-app-capable" content="yes" />
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
<meta name="apple-mobile-web-app-title" content="Déneigement Pro" />
<link rel="apple-touch-icon" href="icon-192.png" />
</head>
<body>
<nav style="max-width:900px;margin:0 auto 16px;display:flex;gap:10px">
<button id="menuCalc" class="secondary" style="flex:1">🧮 Soumission</button>
<button id="menuRegister" class="dark" style="flex:1">📋 Registre</button>
</nav>

<div class="card" id="pageCalc">
<h1>Soumission toiture</h1>
<div class="subtitle">Déneigement professionnel – estimation précise</div>
<label>Nom du client</label><input id="clientName" />
<label>Téléphone</label><input id="phone" />
<label>Adresse complète</label><input id="address" />
<label>📍 Dessiner la toiture (vue satellite)</label>
<div id="drawMap" style="height:300px;border-radius:12px"></div>
<label>✏️ Ou entrer les mesures manuellement</label>
<div class="row"><input type="number" id="length" placeholder="Longueur (pi)" /><input type="number" id="width" placeholder="Largeur (pi)" /></div>
<button id="manualBtn" class="secondary">Calculer surface manuelle</button>
<label>Pente</label><select id="pitch"><option value="1">0–4:12</option><option value="1.06">5–7:12</option><option value="1.12">8–9:12</option><option value="1.18">10–11:12</option><option value="1.25">12:12</option></select>
<label>Versants</label><select id="faces"><option value="1">2 versants</option><option value="1.15">4 versants</option><option value="1.3">5–8 versants</option><option value="1.45">9+ versants</option></select>
<label>Hauteur</label><select id="height"><option value="1">1 étage</option><option value="1.15">2 étages</option><option value="1.3">3 étages+</option></select>
<label>Condition</label><select id="surfaceType"><option value="1">Neige standard</option><option value="1.15">Neige abondante</option><option value="1.35">Neige + glace</option></select>
<label>Nombre de noues</label><input type="number" id="valleysQty" min="0" value="0" />
<button id="calcBtn">Calculer</button>
<div class="result" id="result">Dessinez la toiture ou entrez les données.</div>
<button id="saveBtn" class="success">💾 Enregistrer</button>
</div>

<div class="card" id="pageRegister" style="display:none">
<h1>Registre</h1>
<input id="search" placeholder="🔍 Nom, adresse ou téléphone" />
<h3>🟢 Actives</h3><div id="active"></div>
<h3>🟡 En attente paiement</h3><div id="pending"></div>
<h3>💰 Payées</h3><div id="paid"></div>
<h3>❌ Expirées / Annulées</h3><div id="expired"></div>
<div id="map" style="height:320px;margin-top:20px;border-radius:12px"></div>
</div>

<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
<script src="https://unpkg.com/leaflet-draw@1.0.4/dist/leaflet.draw.js"></script>
<script src="https://unpkg.com/leaflet-geometryutil@0.10.0/src/leaflet.geometryutil.js"></script>
<script>
let map, drawMap, drawnLayer, roofArea = 0;
const statusColor={active:'#22c55e',pending:'#f59e0b',paid:'#15803d',expired:'#dc2626'};

const sounds={
  save:new Audio('data:audio/wav;base64,UklGRiQAAABXQVZFZm10IBAAAAABAAEAESsAACJWAAACABAAZGF0YQAAAAA='),
  delete:new Audio('data:audio/wav;base64,UklGRiQAAABXQVZFZm10IBAAAAABAAEAESsAACJWAAACABAAZGF0YQAAAAA=')
};
function playSound(t){try{sounds[t].currentTime=0;sounds[t].play();}catch(e){}}

document.addEventListener('DOMContentLoaded',()=>{
  menuCalc.onclick=()=>show('calc');
  menuRegister.onclick=()=>show('register');
  calcBtn.onclick=calculate;
  manualBtn.onclick=manualArea;
  saveBtn.onclick=save;
  search.oninput=load;

  drawMap=L.map('drawMap').setView([45.8,-73.9],18);
  L.tileLayer('https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}').addTo(drawMap);
  L.tileLayer('https://services.arcgisonline.com/ArcGIS/rest/services/Reference/World_Boundaries_and_Places/MapServer/tile/{z}/{y}/{x}').addTo(drawMap);
  const drawnItems=new L.FeatureGroup().addTo(drawMap);
  new L.Control.Draw({draw:{polygon:{showArea:true,metric:false},polyline:false,rectangle:false,circle:false,marker:false,circlemarker:false},edit:{featureGroup:drawnItems}}).addTo(drawMap);

  drawMap.on(L.Draw.Event.CREATED,e=>{
    drawnItems.clearLayers();
    drawnLayer=e.layer;
    drawnItems.addLayer(drawnLayer);
    const area=L.GeometryUtil.geodesicArea(drawnLayer.getLatLngs()[0]);
    roofArea=Math.round(area*10.7639);
    result.innerHTML=`Surface dessinée: <b>${roofArea} pi²</b>`;
  });
});

function show(p){
  pageCalc.style.display=p==='calc'?'block':'none';
  pageRegister.style.display=p==='register'?'block':'none';
  if(p==='register') load();
}

function calculate(){
  if(roofArea<=0) return alert('Surface requise');
  const area=Math.round(roofArea*pitch.value*faces.value*height.value*surfaceType.value*(1+valleysQty.value*0.1));
  const price=Math.max(400,Math.round(area*0.35));
  result.innerHTML=`Surface calculée: <b>${area} pi²</b><div class='total'>TOTAL: ${price}$</div>`;
}

function manualArea(){
  if(length.value<=0||width.value<=0) return alert('Mesures invalides');
  roofArea=Math.round(length.value*width.value);
  result.innerHTML=`Surface manuelle: <b>${roofArea} pi²</b>`;
}

function genNumber(){
  return 'S-'+new Date().getFullYear()+'-'+Math.floor(Math.random()*9000+1000);
}

function save(){
  if(!result.innerText.includes('TOTAL')) return alert('Calcul requis');
  const subs=JSON.parse(localStorage.getItem('subs')||'[]');
  subs.push({
    id:Date.now(),
    num:genNumber(),
    name:clientName.value||'Client',
    phone:phone.value||'',
    address:address.value||'',
    price:result.innerText,
    area:roofArea,
    latlng:drawnLayer?drawnLayer.getBounds().getCenter():null,
    date:new Date().toISOString(),
    status:'active'
  });
  localStorage.setItem('subs',JSON.stringify(subs));
  playSound('save');
  load();
}

function load(){
  const containers={active, pending, paid, expired};
  Object.values(containers).forEach(c=>c.innerHTML='');

  if(!map){
    map=L.map('map').setView([45.8,-73.9],9);
    L.tileLayer('https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}').addTo(map);
    L.tileLayer('https://services.arcgisonline.com/ArcGIS/rest/services/Reference/World_Boundaries_and_Places/MapServer/tile/{z}/{y}/{x}').addTo(map);
  }

  map.eachLayer(l=>{if(l instanceof L.Marker) map.removeLayer(l)});

  const q=search.value.toLowerCase();
  let subs=JSON.parse(localStorage.getItem('subs')||'[]');

  subs.forEach(s=>{
    if((Date.now()-new Date(s.date))/86400000>15 && s.status==='active') s.status='expired';
    if(![s.name,s.phone,s.address].join(' ').toLowerCase().includes(q)) return;

    const box=containers[s.status];
    if(!box) return;

    const d=document.createElement('div');
    d.className='sub';
    d.style.background=s.status==='active'?'#dcfce7':s.status==='pending'?'#fef9c3':s.status==='paid'?'#bbf7d0':'#fecaca';

    const actions=document.createElement('div');

    if(s.status==='active'){
      const p=document.createElement('button');p.textContent='Paiement';p.onclick=()=>setStatus(s.id,'pending');actions.appendChild(p);
      const a=document.createElement('button');a.textContent='Annuler';a.className='danger';a.onclick=()=>setStatus(s.id,'expired');actions.appendChild(a);
    }
    if(s.status==='pending'){
      const p=document.createElement('button');p.textContent='Payé';p.onclick=()=>setStatus(s.id,'paid');actions.appendChild(p);
      const a=document.createElement('button');a.textContent='Annuler';a.className='danger';a.onclick=()=>setStatus(s.id,'expired');actions.appendChild(a);
    }
    if(s.status==='expired'){
      const del=document.createElement('button');del.textContent='Supprimer';del.className='danger';del.onclick=()=>deleteSub(s.id);actions.appendChild(del);
    }

    d.innerHTML=`<b>${s.num}</b> – ${s.name}<br>${s.address}<br>${s.phone}<br>${s.price}<br>`;
    d.appendChild(actions);
    box.appendChild(d);

    if(s.latlng){
      const icon=L.divIcon({html:`<div style=\"background:${statusColor[s.status]};width:26px;height:26px;border-radius:50%;border:3px solid white;box-shadow:0 0 8px rgba(0,0,0,.7)\"></div>`});
      L.marker(s.latlng,{icon}).addTo(map);
    }
  });
  localStorage.setItem('subs',JSON.stringify(subs));
}

window.setStatus=function(id,st){
  const s=JSON.parse(localStorage.getItem('subs')||'[]');
  const f=s.find(x=>x.id===id);
  if(f) f.status=st;
  localStorage.setItem('subs',JSON.stringify(s));
  load();
}

window.deleteSub=function(id){
  if(!confirm('Supprimer définitivement cette soumission ?')) return;
  const subs=JSON.parse(localStorage.getItem('subs')||'[]').filter(s=>s.id!==id);
  localStorage.setItem('subs',JSON.stringify(subs));
  playSound('delete');
  load();
}
</script>
</body>
</html>
