<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Keitel.com Character Explorer (Single)</title>
  <style>@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800&display=swap');

:root{
  --bg1:#0f172a; --bg2:#111827;
  --text:#e5e7eb; --muted:#9ca3af;
  --card:rgba(255,255,255,0.06); --card-hover:rgba(255,255,255,0.09);
  --border:rgba(255,255,255,0.14);
  --primary:#7dd3fc; --primary-2:#22d3ee; --danger:#fb7185;
  --shadow:0 18px 50px rgba(0,0,0,.35); --radius:16px;
}
*{box-sizing:border-box}
html,body{height:100%}
body{
  margin:0; font-family:Inter,system-ui,-apple-system,Segoe UI,Roboto,Arial,Helvetica,sans-serif; color:var(--text);
  background:
    radial-gradient(1200px 600px at 10% -10%, rgba(56,189,248,.18), transparent 60%),
    radial-gradient(1000px 500px at 110% 10%, rgba(34,211,238,.16), transparent 60%),
    linear-gradient(135deg,var(--bg1),var(--bg2));
}
.container{max-width:1180px;margin:0 auto;padding:0 18px}
.app-header{position:sticky; top:0; z-index:20; background: rgba(15,23,42,.6);
  backdrop-filter: blur(10px); -webkit-backdrop-filter: blur(10px);
  border-bottom:1px solid rgba(255,255,255,.08);
}
.header-inner{display:flex;align-items:center;justify-content:space-between;padding:18px 0}
.app-header h1{margin:0;font-size:34px;font-weight:800;letter-spacing:.5px}
.subtitle{margin:2px 0 0 0;color:var(--muted)}
.icon-btn{border:1px solid var(--border); color:var(--text);
  background:rgba(255,255,255,.05); backdrop-filter: blur(12px);
  border-radius:12px;padding:10px 12px;cursor:pointer;
}
.controls{display:flex;flex-wrap:wrap;gap:12px; align-items:center;justify-content:flex-start;
  padding:18px; margin:18px 0 8px;
  background: rgba(255,255,255,.06); border:1px solid var(--border);
  backdrop-filter: blur(10px); -webkit-backdrop-filter: blur(10px);
  border-radius:20px; box-shadow: var(--shadow);
}
.search-group{display:flex;align-items:center;gap:10px;flex:1 1 320px}
.search-group input{flex:1; padding:12px 14px;border:1px solid var(--border);
  border-radius:12px; background:rgba(255,255,255,.07); outline:none; font-size:14px; color:var(--text);
}
.search-group input::placeholder{color:var(--muted)}
.primary-btn,.danger-btn{border:none;border-radius:12px;padding:12px 16px;cursor:pointer;
  font-weight:700; color:#0b1220; background: linear-gradient(90deg,var(--primary), var(--primary-2));
  box-shadow: var(--shadow);
}
.primary-btn:hover{filter:brightness(1.03)}
.danger-btn{background: linear-gradient(90deg, #fb7185, #f472b6); color:white;}
select{padding:12px;border-radius:12px;border:1px solid var(--border);
  background:rgba(255,255,255,.07); color:var(--text); min-width:170px;}
.chk{display:flex;align-items:center;gap:8px;color:var(--muted)}
.muted{color:var(--muted);margin:6px 0 12px 0}
.grid{display:grid; grid-template-columns: repeat( auto-fill, minmax(260px, 1fr) ); gap:20px; padding:6px 0 42px}
.card{background:var(--card); border:1px solid var(--border); border-radius:var(--radius);
  box-shadow: var(--shadow); overflow:hidden; display:flex;flex-direction:column;
  transition: transform .2s ease, background .2s ease, border-color .2s ease;
}
.card:hover{transform: translateY(-3px); background:var(--card-hover); border-color: rgba(255,255,255,.22);}
.thumb{width:100%;height:200px;object-fit:cover;background:#0b1220}
.card-content{padding:16px 16px 18px}
.card h3{margin:8px 0 8px 0;font-size:18px}
.meta{font-size:14px;color:var(--muted);line-height:1.45}
.badge-dot{display:inline-flex;align-items:center;gap:8px}
.dot{ width:9px;height:9px;border-radius:50%;display:inline-block }
.dot.alive{background:#22c55e}.dot.dead{background:#ef4444}.dot.unknown{background:#94a3b8}
.buttons{display:flex;gap:10px;margin-top:14px}
.btn{padding:10px 12px;border-radius:12px;border:1px solid var(--border);
  background:rgba(255,255,255,.07); color:var(--text); cursor:pointer}
.btn.primary{background: linear-gradient(90deg,var(--primary), var(--primary-2));
  border-color: transparent; color:#0b1220; font-weight:700}
.btn.primary:hover{filter:brightness(1.03)}
.fav-btn{margin-left:auto; background:rgba(255,255,255,.07);border:1px solid var(--border);
  border-radius:12px;padding:9px 12px;cursor:pointer;min-width:44px;color:#fcd34d}
.fav-btn.faved{background:rgba(250,204,21,.14); border-color: rgba(250,204,21,.5)}
.fav-star{font-size:18px;line-height:1}
.sentinel{height:40px}
.app-footer{text-align:center;font-size:14px;color:var(--muted);
  padding:22px 10px;margin-top:20px; border-top:1px solid rgba(255,255,255,.08);
  background: rgba(255,255,255,.04); backdrop-filter: blur(10px);}
.app-footer a{color:var(--primary);text-decoration:none}
.app-footer a:hover{text-decoration:underline}

/* Episode info banner */
.ep-info{display:none; margin:10px 0 6px; padding:12px 14px;
  background: rgba(125, 211, 252, .08); border:1px solid rgba(125, 211, 252, .35);
  border-radius: 12px; color: var(--text);}
.ep-info strong{color:#7dd3fc}
.ep-info .ep-meta{color:var(--muted); font-size: 13px}

/* Modal */
.modal{position:fixed; inset:0; display:flex; align-items:center; justify-content:center; z-index:50}
.modal.hidden{display:none}
.modal-backdrop{position:absolute; inset:0; background:rgba(0,0,0,.55); backdrop-filter: blur(2px);}
.modal-dialog{position:relative; z-index:1; max-width:780px; width:92%;
  background: rgba(255,255,255,0.06); border:1px solid rgba(255,255,255,0.18);
  backdrop-filter: blur(14px); -webkit-backdrop-filter: blur(14px);
  border-radius:16px; box-shadow: 0 30px 80px rgba(0,0,0,.45); padding:18px 18px 22px;}
.modal-close{position:absolute; top:10px; right:10px; border:1px solid rgba(255,255,255,.2);
  background:rgba(255,255,255,.08); color:#e5e7eb; border-radius:10px; padding:6px 9px; cursor:pointer}
.modal-content h2{margin:6px 0 10px 0; font-size:22px}
.modal-content .row{display:flex; flex-wrap:wrap; gap:10px; color:#cbd5e1; font-size:14px; margin-bottom:8px}
.modal-content .badge{display:inline-flex; align-items:center; gap:6px; padding:6px 10px; border-radius:999px;
  background:rgba(255,255,255,.08); border:1px solid rgba(255,255,255,.14)}
.modal-content .episodes{margin-top:12px}
.modal-content .episodes h3{font-size:16px; margin:0 0 8px 0; color:#7dd3fc}
.modal-content ul{margin:0; padding-left:18px}
.modal-content li{margin:4px 0; color:#9ca3af}
.modal-content .hero{display:flex; gap:16px; align-items:center}
.modal-content .hero img{width:132px; height:132px; object-fit:cover; border-radius:14px; border:1px solid rgba(255,255,255,.18)}
</style>
</head>
<body>
  <header class="app-header">
    <div class="container header-inner">
      <div>
        <h1>Rick & Morty</h1>
        <p class="subtitle">Character Explorer</p>
      </div>
      <button id="themeToggle" class="icon-btn" title="Tema">
        <span>🌙</span>
      </button>
    </div>
  </header>

  <main class="container">
    <section class="controls">
      <div class="search-group">
        <input id="searchInput" type="search" placeholder="Buscar personajes por nombre..." />
        <button id="searchBtn" class="primary-btn" title="Buscar">🔎</button>
      </div>
      <select id="statusSelect">
        <option value="">Todos los estados</option>
        <option value="alive">Vivo</option>
        <option value="dead">Muerto</option>
        <option value="unknown">Desconocido</option>
      </select>
      <select id="speciesSelect">
        <option value="">Todas las especies</option>
      </select>
      <select id="episodeSelect">
        <option value="">Todos los episodios</option>
      </select>
      <label class="chk">
        <input type="checkbox" id="onlyFavs" />
        Solo favoritos
      </label>
      <button id="clearBtn" class="danger-btn">Limpiar filtros</button>
    </section>

    <div id="episodeInfo" class="ep-info" aria-live="polite"></div>
    <p id="resultInfo" class="muted"></p>
    <section id="cards" class="grid"></section>
    <div id="sentinel" class="sentinel"></div>
  </main>

  <div id="modal" class="modal hidden" aria-hidden="true" role="dialog" aria-modal="true">
    <div class="modal-backdrop" data-close="modal"></div>
    <div class="modal-dialog" role="document">
      <button class="modal-close" data-close="modal" aria-label="Cerrar">✕</button>
      <div id="modalContent" class="modal-content"></div>
    </div>
  </div>

  <footer class="app-footer">
    © 2025 keitel.com Character Explorer <br />
    Desarrollado con ❤️ para los chicos del Diplomado de Front End <br />
    API proporcionada por
    <a href="https://rickandmortyapi.com" target="_blank">rickandmortyapi.com</a>
  </footer>

  <script>(function(){
  const API_BASE = "https://rickandmortyapi.com/api";
  const $ = s => document.querySelector(s);

  // --- Elements
  const searchInput=$("#searchInput"), searchBtn=$("#searchBtn"),
        statusSelect=$("#statusSelect"), speciesSelect=$("#speciesSelect"),
        episodeSelect=$("#episodeSelect"), onlyFavs=$("#onlyFavs"),
        clearBtn=$("#clearBtn"), resultInfo=$("#resultInfo"),
        cards=$("#cards"), sentinel=$("#sentinel"), episodeInfo=$("#episodeInfo"),
        modal=$("#modal"), modalContent=$("#modalContent");

  // --- State
  const state = {
    name:"", status:"", species:"", episodeId:"",
    onlyFavs:false, page:1, total:0, loading:false,
    buffer:[], mode:"api", speciesSet:new Set(),
    favorites:new Set(loadFavorites()),
    episodeMeta:null,
  };

  function loadFavorites(){ try{ return JSON.parse(localStorage.getItem("rm_favorites")||"[]"); }catch{ return []; } }
  function saveFavorites(){ localStorage.setItem("rm_favorites", JSON.stringify([...state.favorites])); }

  function showMessage(msg){ resultInfo.textContent = msg || ""; }
  function el(html){ const t=document.createElement('template'); t.innerHTML=html.trim(); return t.content.firstElementChild; }
  function statusClass(s){ s=(s||'unknown').toLowerCase(); if(s==='alive')return 'alive'; if(s==='dead')return 'dead'; return 'unknown'; }

  function renderCard(ch, isFav){
    return el(`<article class="card" data-id="${ch.id}">
      <img class="thumb" src="${ch.image}" alt="${ch.name}" loading="lazy">
      <div class="card-content">
        <h3>${ch.name}</h3>
        <div class="meta">
          <span class="badge-dot"><span class="dot ${statusClass(ch.status)}"></span>${ch.status||"Unknown"}</span>
          &nbsp;·&nbsp; ${ch.species||"Unknown"}
          <div>Origen: ${ch.origin?.name||"Unknown"}</div>
        </div>
        <div class="buttons">
          <button class="btn primary" data-action="details">Ver Detalles</button>
          <button class="fav-btn ${isFav ? "faved": ""}" data-action="fav" aria-label="Favorito">
            <span class="fav-star">${isFav ? "★" : "☆"}</span>
          </button>
        </div>
      </div>
    </article>`);
  }

  // --- API helpers
  async function fetchCharacters({ page=1, name="", status="", species="" } = {}){
    const params = new URLSearchParams();
    params.set("page", page);
    if (name) params.set("name", name);
    if (status) params.set("status", status);
    if (species) params.set("species", species);
    const res = await fetch(`${API_BASE}/character/?${params.toString()}`);
    if (!res.ok) throw new Error("Error al cargar personajes");
    return res.json();
  }

  async function fetchCharactersByIds(ids){
    if (!ids || !ids.length) return [];
    const batches = [];
    for (let i=0;i<ids.length;i+=20) batches.push(ids.slice(i,i+20));
    const out = [];
    for (const b of batches){
      const res = await fetch(`${API_BASE}/character/${b.join(",")}`);
      if (!res.ok) continue;
      const data = await res.json();
      Array.isArray(data) ? out.push(...data) : out.push(data);
    }
    return out;
  }

  async function fetchAllEpisodes(){
    let page=1, all=[];
    while (true){
      const res = await fetch(`${API_BASE}/episode?page=${page}`);
      if (!res.ok) break;
      const data = await res.json();
      all.push(...data.results);
      if (!data.info?.next) break;
      page++;
    }
    return all;
  }

  async function fetchEpisode(id){
    const res = await fetch(`${API_BASE}/episode/${id}`);
    if (!res.ok) throw new Error("Episodio no encontrado");
    return res.json();
  }

  async function fetchCharacter(id){
    const res = await fetch(`${API_BASE}/character/${id}`);
    if (!res.ok) throw new Error("Personaje no encontrado");
    return res.json();
  }

  async function fetchEpisodesByIds(ids){
    if (!ids || !ids.length) return [];
    const res = await fetch(`${API_BASE}/episode/${ids.join(",")}`);
    if (!res.ok) return [];
    const data = await res.json();
    return Array.isArray(data) ? data : [data];
  }

  // --- Modal helpers
  function openModal(html){
    modalContent.innerHTML = html;
    modal.classList.remove('hidden');
    modal.setAttribute('aria-hidden','false');
  }
  function closeModal(){
    modal.classList.add('hidden');
    modal.setAttribute('aria-hidden','true');
  }
  document.addEventListener('keydown', e=>{ if(e.key==='Escape') closeModal(); });
  modal?.addEventListener('click', e=>{ if (e.target?.dataset?.close==='modal') closeModal(); });

  // --- Init
  document.addEventListener("DOMContentLoaded", async () => {
    try{
      attachEvents();
      await hydrateEpisodes();
      await resetAndLoad();
    }catch(err){
      console.error(err);
      showMessage("Error inicializando la app.");
    }
  });

  function attachEvents(){
    let t;
    const doSearch = async () => {
      clearTimeout(t); t=setTimeout(async ()=>{ state.name = searchInput.value.trim(); await resetAndLoad(); }, 350);
    };
    searchInput.addEventListener('input', doSearch);
    searchBtn.addEventListener('click', () => { state.name = searchInput.value.trim(); resetAndLoad(); });
    statusSelect.addEventListener('change', () => { state.status = statusSelect.value; resetAndLoad(); });
    speciesSelect.addEventListener('change', () => { state.species = speciesSelect.value; resetAndLoad(); });
    episodeSelect.addEventListener('change', async () => {
      state.episodeId = episodeSelect.value;
      await updateEpisodeInfo();
      await resetAndLoad();
      window.scrollTo({top:0,behavior:'smooth'});
    });
    onlyFavs.addEventListener('change', async () => { state.onlyFavs = onlyFavs.checked; await resetAndLoad(); });
    clearBtn.addEventListener('click', async () => {
      searchInput.value=""; statusSelect.value=""; speciesSelect.value="";
      episodeSelect.value=""; onlyFavs.checked=false;
      Object.assign(state,{name:"",status:"",species:"",episodeId:"",onlyFavs:false,episodeMeta:null});
      await updateEpisodeInfo();
      await resetAndLoad();
    });

    cards.addEventListener('click', async (e) => {
      const detailsBtn = e.target.closest('[data-action="details"]');
      if (detailsBtn){
        const card = e.target.closest('.card'); const id = Number(card?.dataset?.id);
        if (id) openDetails(id);
        return;
      }
      const favBtn = e.target.closest('[data-action="fav"]');
      if (favBtn){
        const card = e.target.closest('.card'); const id = Number(card?.dataset?.id);
        toggleFavorite(id, favBtn);
      }
    });

    const observer = new IntersectionObserver(async (entries)=>{
      for (const entry of entries){ if (entry.isIntersecting) await loadMore(); }
    },{rootMargin:'120px'});
    observer.observe(sentinel);
  }

  function toggleFavorite(id, btn){
    if (!id) return;
    if (state.favorites.has(id)) state.favorites.delete(id); else state.favorites.add(id);
    saveFavorites();
    btn.classList.toggle('faved');
    const star = btn.querySelector('.fav-star'); if (star) star.textContent = btn.classList.contains('faved') ? "★" : "☆";
    if (state.onlyFavs && !state.favorites.has(id)){ const card = btn.closest('.card'); if (card) card.remove(); }
  }

  async function hydrateEpisodes(){
    const episodes = await fetchAllEpisodes();
    for (const ep of episodes){
      const opt = document.createElement("option");
      opt.value = String(ep.id); opt.textContent = `${ep.episode} – ${ep.name}`;
      episodeSelect.appendChild(opt);
    }
  }

  async function updateEpisodeInfo(){
    if (!state.episodeId){
      episodeInfo.style.display="none"; episodeInfo.innerHTML=""; return;
    }
    const ep = await fetchEpisode(state.episodeId);
    state.episodeMeta = ep;
    episodeInfo.style.display="block";
    episodeInfo.innerHTML = `<div><strong>${ep.episode}</strong> — ${ep.name}</div>
      <div class="ep-meta">Fecha de emisión: ${ep.air_date} · Personajes en este episodio: ${ep.characters?.length || 0}</div>`;
  }

  async function resetAndLoad(){
    state.page=1; state.total=0; state.buffer=[]; cards.innerHTML=""; showMessage("Cargando...");
    state.mode = (state.episodeId || state.onlyFavs) ? "local" : "api";
    await loadMore(true);
  }

  async function loadMore(isFirst=false){
    if (state.loading) return; state.loading = true;
    try{
      if (state.mode === "api"){
        const data = await fetchCharacters({ page: state.page, name: state.name, status: state.status, species: state.species });
        const items = data.results || []; state.total = data.info?.count || items.length;
        appendCards(items); state.page++; updateInfo(items.length, isFirst);
        updateSpeciesSet(items);
      }else{
        if (!state.buffer.length && isFirst){ state.buffer = await buildLocalBuffer(); state.total = state.buffer.length; }
        const start = (state.page-1)*20; const slice = state.buffer.slice(start, start+20);
        appendCards(slice); if (isFirst && !slice.length){ showMessage('Este episodio no tiene resultados con los filtros actuales (revisa "Solo favoritos" o borra filtros).'); }
        state.page++; updateInfo(slice.length, isFirst);
        updateSpeciesSet(slice);
      }
    }catch(err){
      if (isFirst){ cards.innerHTML=""; showMessage("No se encontraron resultados con los filtros actuales."); }
      console.error(err);
    }finally{ state.loading = false; }
  }

  function appendCards(list){
    const frag = document.createDocumentFragment();
    for (const ch of list){ const isFav = state.favorites.has(ch.id); frag.appendChild(renderCard(ch, isFav)); }
    cards.appendChild(frag);
  }

  function updateSpeciesSet(list){
    let updated=false;
    for (const ch of list){
      if (ch.species && !state.speciesSet.has(ch.species)){ state.speciesSet.add(ch.species); updated=true; }
    }
    if (updated){
      const current = state.species;
      while (speciesSelect.options.length > 1) speciesSelect.remove(1);
      [...state.speciesSet].sort().forEach(sp => {
        const opt = document.createElement("option");
        opt.value = sp; opt.textContent = sp;
        speciesSelect.appendChild(opt);
      });
      speciesSelect.value = current;
    }
  }

  function updateInfo(loadedCount, isFirst){
    const currently = cards.children.length;
    if (state.total){
      const start = Math.max(1, currently - loadedCount + 1);
      const end = currently;
      showMessage(`Mostrando ${start}-${end} de ${state.total} personajes`);
    }else if(isFirst){ showMessage(""); }
  }

  async function buildLocalBuffer(){
    let ids = [];
    if (state.episodeId){
      const ep = state.episodeMeta || await fetchEpisode(state.episodeId);
      ids = ep.characters.map(u => Number(u.split('/').pop())).filter(Boolean);
    } else {
      ids = [...state.favorites];
    }
    if (state.episodeId && state.onlyFavs){ const fav = new Set(state.favorites); ids = ids.filter(id => fav.has(id)); }
    const chars = await fetchCharactersByIds(ids);
    const name = state.name.toLowerCase(), status = state.status.toLowerCase(), species = state.species;
    const filtered = chars.filter(ch => {
      if (name && !String(ch.name).toLowerCase().includes(name)) return false;
      if (status && String(ch.status).toLowerCase() !== status) return false;
      if (species && String(ch.species) !== species) return false;
      return true;
    });
    filtered.sort((a,b)=>a.id-b.id);
    return filtered;
  }

  async function openDetails(id){
    try{
      const ch = await fetchCharacter(id);
      const epIds = ch.episode.map(u => Number(u.split('/').pop())).filter(Boolean);
      const eps = await fetchEpisodesByIds(epIds.slice(0,12));
      const items = eps.map(e => `<li><strong>${e.episode}</strong> — ${e.name}</li>`).join("") || "<li>Sin episodios</li>";
      const html = `
        <div class="hero">
          <img src="${ch.image}" alt="${ch.name}"/>
          <div class="meta">
            <h2>${ch.name}</h2>
            <div class="row">
              <span class="badge">Estado: ${ch.status}</span>
              <span class="badge">Especie: ${ch.species}</span>
              <span class="badge">Género: ${ch.gender}</span>
            </div>
            <div class="row">
              <span class="badge">Origen: ${ch.origin?.name || "Unknown"}</span>
              <span class="badge">Ubicación: ${ch.location?.name || "Unknown"}</span>
            </div>
          </div>
        </div>
        <div class="episodes">
          <h3>Episodios (${epIds.length})</h3>
          <ul>${items}</ul>
        </div>`;
      openModal(html);
    }catch(err){
      openModal("<p>No se pudo cargar el personaje.</p>");
      console.error(err);
    }
  }

})();</script>
</body>
</html>
