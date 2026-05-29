<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Dashboard Circuito TVMAX · Mundial 2026</title>
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@900&family=Roboto:wght@400;500;700&display=swap" rel="stylesheet"/>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/tabler-icons.min.css"/>
<style>
*{box-sizing:border-box;margin:0;padding:0;}
body{font-family:'Roboto',sans-serif;background:#0A1A0A;color:#fff;min-height:100vh;padding:24px;}
:root{--green:#6DD400;--green-dim:rgba(109,212,0,0.18);--green-text:rgba(109,212,0,0.75);--card:#0D1E0D;--border:rgba(109,212,0,0.18);--amber:#F5A623;--red:#E53E3E;--blue:#63B3ED;--muted:rgba(255,255,255,0.55);}
.dash{max-width:1200px;margin:0 auto;}
.hero{background:linear-gradient(135deg,#0A2A0A 0%,#0D1F0D 60%,#0A1A0A 100%);border-radius:16px;padding:1.5rem 2rem;display:flex;align-items:center;justify-content:space-between;margin-bottom:1.5rem;border:1px solid var(--border);position:relative;overflow:hidden;}
.hero::before{content:'';position:absolute;right:-40px;top:-40px;width:220px;height:220px;border-radius:50%;background:rgba(109,212,0,0.06);}
.hero-titles h1{font-family:'Poppins',sans-serif;font-weight:900;font-size:24px;color:var(--green);text-transform:uppercase;letter-spacing:1px;}
.hero-titles p{font-size:13px;color:var(--green-text);margin-top:3px;}
.hero-badges{display:flex;gap:10px;z-index:1;}
.hero-badge{background:rgba(109,212,0,0.12);border:1px solid var(--green);border-radius:10px;padding:10px 18px;text-align:center;}
.hero-badge span{display:block;font-family:'Poppins',sans-serif;font-weight:900;font-size:30px;color:var(--green);}
.hero-badge small{font-size:11px;color:var(--green-text);text-transform:uppercase;letter-spacing:0.5px;}
.hero-badge.amber span{color:var(--amber);}
.hero-badge.amber{border-color:var(--amber);background:rgba(245,166,35,0.1);}
.metrics-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-bottom:1.5rem;}
.metric-card{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:14px 16px;}
.metric-card .val{font-family:'Poppins',sans-serif;font-weight:900;font-size:28px;line-height:1;margin-bottom:4px;}
.metric-card .lbl{font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:0.8px;}
.metric-card.green .val{color:var(--green);}
.metric-card.amber .val{color:var(--amber);}
.metric-card.red .val{color:var(--red);}
.metric-card.blue .val{color:var(--blue);}
.tabs{display:flex;gap:4px;margin-bottom:1.25rem;background:#0D1E0D;border-radius:10px;padding:5px;border:1px solid var(--border);}
.tab{flex:1;padding:10px 4px;border-radius:7px;font-size:12px;font-family:'Roboto',sans-serif;font-weight:700;cursor:pointer;border:none;background:transparent;color:rgba(255,255,255,0.65);transition:all 0.2s;letter-spacing:0.3px;}
.tab.active{background:var(--green);color:#0A1A0A;}
.tab:hover:not(.active){color:#fff;background:rgba(109,212,0,0.08);}
.panel{display:none;}.panel.active{display:block;}
.section-title{font-family:'Poppins',sans-serif;font-weight:900;font-size:11px;color:var(--green);text-transform:uppercase;letter-spacing:1.5px;margin-bottom:0.75rem;}
.filter-row{display:flex;gap:6px;margin-bottom:10px;flex-wrap:wrap;}
.filter-btn{padding:5px 14px;border-radius:20px;font-size:11px;font-family:'Roboto',sans-serif;font-weight:700;cursor:pointer;border:1px solid rgba(109,212,0,0.25);background:transparent;color:rgba(255,255,255,0.65);transition:all 0.15s;}
.filter-btn.active{background:var(--green);color:#0A1A0A;border-color:var(--green);}
.filter-btn:hover:not(.active){color:#fff;border-color:rgba(109,212,0,0.5);}
.search-input{width:100%;padding:9px 14px;background:var(--card);border:1px solid var(--border);border-radius:8px;color:#fff;font-size:13px;font-family:'Roboto',sans-serif;margin-bottom:10px;outline:none;}
.search-input::placeholder{color:var(--muted);}
.search-input:focus{border-color:rgba(109,212,0,0.5);}
.prospect-table{width:100%;border-collapse:collapse;}
.prospect-table th{font-size:10px;color:var(--green-text);text-transform:uppercase;letter-spacing:0.8px;padding:9px 10px;text-align:left;border-bottom:1px solid var(--border);font-family:'Roboto',sans-serif;font-weight:700;background:rgba(109,212,0,0.04);}
.prospect-table td{padding:9px 10px;font-size:12px;color:#fff;border-bottom:1px solid rgba(109,212,0,0.06);font-family:'Roboto',sans-serif;vertical-align:top;}
.prospect-table tr:hover td{background:rgba(109,212,0,0.04);}
.obs-text{font-size:10px;color:rgba(255,255,255,0.5);line-height:1.4;max-width:260px;}
.badge{display:inline-flex;align-items:center;gap:4px;padding:3px 9px;border-radius:20px;font-size:10px;font-weight:700;white-space:nowrap;}
.badge.cerrado{background:rgba(109,212,0,0.15);color:#6DD400;border:1px solid rgba(109,212,0,0.3);}
.badge.pendiente{background:rgba(245,166,35,0.15);color:#F5A623;border:1px solid rgba(245,166,35,0.3);}
.badge.sin-resp{background:rgba(229,62,62,0.15);color:#E53E3E;border:1px solid rgba(229,62,62,0.3);}
.badge.otro{background:rgba(160,160,160,0.12);color:#bbb;border:1px solid rgba(160,160,160,0.25);}
.confirm-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px;}
.confirm-card{background:var(--card);border:1px solid var(--border);border-radius:10px;padding:14px 16px;}
.confirm-card h3{font-family:'Poppins',sans-serif;font-weight:900;font-size:13px;color:#fff;margin-bottom:4px;}
.confirm-loc{font-size:10px;color:var(--green-text);margin-bottom:10px;}
.step-row{display:flex;align-items:center;gap:7px;margin-bottom:6px;}
.step-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0;}
.step-dot.done{background:var(--green);}
.step-dot.pend{background:var(--amber);}
.step-dot.na{background:rgba(255,255,255,0.2);}
.step-label{font-size:11px;color:rgba(255,255,255,0.65);flex:1;}
.step-val{font-size:10px;text-align:right;max-width:150px;}
.step-val.done{color:var(--green);}
.step-val.pend{color:var(--amber);}
.step-val.na{color:rgba(255,255,255,0.25);}
.assets-table{width:100%;border-collapse:collapse;}
.assets-table th{font-size:10px;color:var(--green-text);text-transform:uppercase;letter-spacing:0.8px;padding:9px 10px;text-align:left;border-bottom:1px solid var(--border);font-family:'Roboto',sans-serif;font-weight:700;background:rgba(109,212,0,0.04);}
.assets-table td{padding:9px 10px;font-size:12px;color:#fff;border-bottom:1px solid rgba(109,212,0,0.06);vertical-align:middle;}
.assets-table tr:hover td{background:rgba(109,212,0,0.04);}
.pct-bar{height:4px;background:rgba(109,212,0,0.12);border-radius:4px;overflow:hidden;margin-top:4px;}
.pct-fill{height:100%;border-radius:4px;}
.asset-cell-edit{cursor:pointer;border-radius:4px;padding:2px 6px;text-align:center;}
.asset-cell-edit:hover{background:rgba(109,212,0,0.1);}
.overview-2col{display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-bottom:1rem;}
.chart-wrap{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:16px;}
.funnel-item{display:flex;align-items:center;gap:10px;margin-bottom:9px;}
.funnel-bar-bg{flex:1;height:26px;background:rgba(109,212,0,0.07);border-radius:6px;overflow:hidden;}
.funnel-bar-fill{height:100%;border-radius:6px;display:flex;align-items:center;padding-left:10px;font-size:11px;font-weight:700;}
.funnel-label{font-size:11px;color:rgba(255,255,255,0.6);width:120px;text-align:right;}
.scroll-table{overflow-x:auto;}
.modal-overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,0.8);z-index:1000;align-items:center;justify-content:center;}
.modal-overlay.open{display:flex;}
.modal{background:#0D1E0D;border:1px solid var(--border);border-radius:14px;padding:24px;width:620px;max-width:95vw;max-height:85vh;overflow-y:auto;}
.modal h2{font-family:'Poppins',sans-serif;font-weight:900;font-size:16px;color:var(--green);margin-bottom:16px;}
.form-row{margin-bottom:12px;}
.form-label{font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:0.8px;margin-bottom:4px;display:block;font-weight:700;}
.form-input,.form-select,.form-textarea{width:100%;padding:8px 12px;background:#0A1A0A;border:1px solid var(--border);border-radius:7px;color:#fff;font-size:13px;font-family:'Roboto',sans-serif;outline:none;}
.form-input:focus,.form-select:focus,.form-textarea:focus{border-color:var(--green);}
.form-select option{background:#0D1E0D;color:#fff;}
.form-textarea{resize:vertical;min-height:80px;}
.form-2col{display:grid;grid-template-columns:1fr 1fr;gap:10px;}
.btn-row{display:flex;gap:8px;margin-top:16px;justify-content:flex-end;}
.btn{padding:9px 20px;border-radius:7px;font-size:13px;font-family:'Roboto',sans-serif;font-weight:700;cursor:pointer;border:none;}
.btn-primary{background:var(--green);color:#0A1A0A;}
.btn-primary:hover{background:#7EE600;}
.btn-danger{background:rgba(229,62,62,0.15);color:#E53E3E;border:1px solid rgba(229,62,62,0.3);}
.btn-ghost{background:transparent;color:var(--muted);border:1px solid var(--border);}
.btn-ghost:hover{color:#fff;}
.fab{position:fixed;bottom:28px;right:28px;background:var(--green);color:#0A1A0A;border:none;border-radius:50%;width:54px;height:54px;font-size:28px;cursor:pointer;box-shadow:0 4px 20px rgba(109,212,0,0.3);display:flex;align-items:center;justify-content:center;transition:transform 0.2s;font-weight:700;}
.fab:hover{transform:scale(1.08);}
.edit-btn{background:rgba(109,212,0,0.1);border:1px solid rgba(109,212,0,0.2);color:#6DD400;border-radius:6px;padding:4px 10px;font-size:10px;font-weight:700;cursor:pointer;font-family:'Roboto',sans-serif;white-space:nowrap;}
.edit-btn:hover{background:rgba(109,212,0,0.2);}
</style>
</head>
<body>
<div class="dash">

<div class="hero">
  <div class="hero-titles">
    <h1>Dashboard Circuito TVMAX</h1>
    <p>Control de alianzas estratégicas · Mundial FIFA 2026</p>
  </div>
  <div class="hero-badges">
    <div class="hero-badge"><span id="stat-cerrados">0</span><small>Aliados confirmados</small></div>
    <div class="hero-badge amber"><span id="stat-proceso">0</span><small>En negociación</small></div>
  </div>
</div>

<div class="metrics-grid">
  <div class="metric-card green"><div class="val" id="m-cerrados">0</div><div class="lbl">Aliados cerrados</div></div>
  <div class="metric-card blue"><div class="val" id="m-firmas">0</div><div class="lbl">Firmas realizadas</div></div>
  <div class="metric-card amber"><div class="val" id="m-pend">0</div><div class="lbl">Pendientes respuesta</div></div>
  <div class="metric-card red"><div class="val" id="m-perdidos">0</div><div class="lbl">Sin respuesta / perdidos</div></div>
</div>

<div class="tabs">
  <button class="tab active" onclick="showTab('pipeline',this)">Pipeline de Prospectos</button>
  <button class="tab" onclick="showTab('confirmados',this)">Aliados Confirmados</button>
  <button class="tab" onclick="showTab('assets',this)">Tracking de Assets</button>
  <button class="tab" onclick="showTab('overview',this)">Resumen Visual</button>
</div>

<div id="panel-pipeline" class="panel active">
  <div class="filter-row">
    <button class="filter-btn active" onclick="filterP('all',this)">Todos</button>
    <button class="filter-btn" onclick="filterP('cerrado',this)">Cerrados</button>
    <button class="filter-btn" onclick="filterP('pendiente',this)">Pendientes</button>
    <button class="filter-btn" onclick="filterP('sin-resp',this)">Sin respuesta</button>
    <button class="filter-btn" onclick="filterP('otro',this)">Perdidos / Otro</button>
  </div>
  <input class="search-input" type="text" placeholder="Buscar restaurante, contacto, ubicación..." oninput="searchP(this.value)"/>
  <div class="scroll-table">
    <table class="prospect-table">
      <thead><tr><th>#</th><th>Restaurante</th><th>Ubicación</th><th>Contacto</th><th>Teléfono</th><th>Status</th><th>Observaciones</th><th>Acción</th></tr></thead>
      <tbody id="prospect-body"></tbody>
    </table>
  </div>
</div>

<div id="panel-confirmados" class="panel">
  <div class="confirm-grid" id="confirm-grid"></div>
</div>

<div id="panel-assets" class="panel">
  <p style="font-size:12px;color:var(--muted);margin-bottom:10px;">Haz clic en una celda para marcarla como recibida o pendiente.</p>
  <div class="scroll-table">
    <table class="assets-table">
      <thead><tr><th>#</th><th>Restaurante</th><th>Contacto</th><th>Logo</th><th>Mención Producto</th><th>Mención Marca</th><th>Stories IG</th><th>% Completo</th></tr></thead>
      <tbody id="assets-body"></tbody>
    </table>
  </div>
</div>

<div id="panel-overview" class="panel">
  <div class="overview-2col">
    <div class="chart-wrap"><div class="section-title">Funnel de negociación</div><div id="funnel-chart"></div></div>
    <div class="chart-wrap">
      <div class="section-title">Estado de firmas</div><div id="firma-chart"></div>
      <div style="height:14px;"></div>
      <div class="section-title">Cobertura de assets</div><div id="assets-summary"></div>
    </div>
  </div>
  <div class="chart-wrap"><div class="section-title">Distribución por zona</div><div id="zona-chart"></div></div>
</div>

</div>

<button class="fab" onclick="openAddModal()" title="Agregar prospecto">+</button>

<div class="modal-overlay" id="modal">
  <div class="modal">
    <h2 id="modal-title">Agregar Prospecto</h2>
    <div class="form-2col">
      <div class="form-row"><label class="form-label">Restaurante</label><input class="form-input" id="f-rest" type="text" placeholder="Nombre"/></div>
      <div class="form-row"><label class="form-label">Ubicación</label><input class="form-input" id="f-ubi" type="text" placeholder="Zona o dirección"/></div>
    </div>
    <div class="form-2col">
      <div class="form-row"><label class="form-label">Contacto</label><input class="form-input" id="f-cont" type="text" placeholder="Nombre del contacto"/></div>
      <div class="form-row"><label class="form-label">Teléfono</label><input class="form-input" id="f-tel" type="text" placeholder="6000-0000"/></div>
    </div>
    <div class="form-row"><label class="form-label">Status</label>
      <select class="form-select" id="f-status">
        <option value="cerrado">Acuerdo Cerrado</option>
        <option value="pendiente">Pendiente Respuesta</option>
        <option value="sin-resp">Sin Respuesta</option>
        <option value="otro">Perdido / Otro</option>
      </select>
    </div>
    <div class="form-row"><label class="form-label">Observaciones</label><textarea class="form-textarea" id="f-obs" placeholder="Notas clave..."></textarea></div>
    <div class="btn-row">
      <button class="btn btn-ghost" onclick="closeModal()">Cancelar</button>
      <button class="btn btn-danger" id="btn-delete" style="display:none;" onclick="deleteProspect()">Eliminar</button>
      <button class="btn btn-primary" onclick="saveProspect()">Guardar</button>
    </div>
  </div>
</div>

<script>
let editingIdx=-1, currentFilter='all', currentSearch='';

const defaultProspects=[
  {r:'Boho',u:'Río Abajo',c:'Franklyn Robinson',t:'6093-7160',s:'cerrado',obs:'Fanfest exterior con I Star Panamá. Pendiente firma simbólica.'},
  {r:'Minuto7',u:'Calle Uruguay',c:'Juan Alvarado',t:'6204-2886',s:'cerrado',obs:'Firma y pase en vivo realizados el 5 de mayo.'},
  {r:'5 to 5 Hilton',u:'Ave. Balboa',c:'Francesco Magri',t:'6053-3460',s:'cerrado',obs:'Firma el 8 de mayo. Confirmar participación Jonathan Gutiérrez.'},
  {r:'Club Unión Española',u:'Carrasquilla',c:'Luis Arias',t:'6030-0777',s:'cerrado',obs:'Firma 26 mayo. Comunicar como club deportivo, no bar.'},
  {r:'La Manzana',u:'Santa Ana',c:'Edwards Molla',t:'6183-4712',s:'sin-resp',obs:'Evaluando vs Cable Onda Sports y RPC.'},
  {r:'Grill 50',u:'San Francisco',c:'Stefany García',t:'',s:'pendiente',obs:'Seguimiento 25 mayo. Pendiente respuesta.'},
  {r:'La Rana Dorada',u:'Ubicaciones varias',c:'Blanca y Hernán',t:'',s:'otro',obs:'Firmaron con otra plataforma.'},
  {r:'The Yard',u:'San Francisco',c:'Jorge Castro',t:'6611-8931',s:'cerrado',obs:'Firma 12 mayo. Pase en vivo realizado. Cuidar acuerdo con Balboa.'},
  {r:'Central Cervecería',u:'San Francisco',c:'Carlos',t:'6070-8066',s:'cerrado',obs:'Firma pendiente de confirmar fecha.'},
  {r:'Os Segredos Da Carne',u:'Marbella',c:'Rodolfo',t:'6835-7312',s:'pendiente',obs:'Pendiente respuesta.'},
  {r:'Par de Pintas',u:'Calle Uruguay',c:'Ernesto Castillo',t:'6747-6615',s:'pendiente',obs:'Seguimiento 25 mayo.'},
  {r:'Feroz',u:'Ciudad del Saber',c:'Cesar Conto',t:'6090-7564',s:'cerrado',obs:'Firma 18 mayo. Pendiente contenido. Posible ceviche temático.'},
  {r:'Taberna 21',u:'Cangrejo',c:'—',t:'',s:'sin-resp',obs:'Sin contacto registrado.'},
  {r:'Bingo 90',u:'Obarrio',c:'Stephanie',t:'',s:'pendiente',obs:'34 salas en ciudad e interior. Pendiente propuesta formal de TVMAX.'},
  {r:'Pintas Spot',u:'Calle 50',c:'Dainubys Sarmiento',t:'6647-6772',s:'cerrado',obs:'Documento enviado. Pendiente confirmar fecha de firma.'},
  {r:'Charro Mexicano',u:'—',c:'—',t:'',s:'sin-resp',obs:'Sin respuesta.'},
  {r:'Canal House Panama',u:'Amador',c:'Germán',t:'6315-3237',s:'cerrado',obs:'Firma 18 mayo. 4-5 pantallas. Alto tráfico orgánico.'},
  {r:'X3M',u:'Tumba Muerto',c:'Curtis',t:'6264-6589',s:'cerrado',obs:'Firma 18 mayo. Pendiente contenido.'},
  {r:'BlueTap House',u:'Ubicaciones varias',c:'Tomas Santos',t:'6237-5961',s:'otro',obs:'Firmaron con RPC.'},
  {r:'Dorado Mall',u:'El Dorado',c:'Victor',t:'6612-8003',s:'cerrado',obs:'Firma 25 mayo. Pase en vivo realizado.'},
  {r:'PESKITO',u:'Altos/Costa Verde',c:'Abdiel Celis',t:'6618-6973',s:'cerrado',obs:'Firma 14 mayo.'},
  {r:'Austin Mamas',u:'Corozal y Costa Este',c:'Sebastián',t:'6898-6073',s:'cerrado',obs:'Cerrado. Documento pendiente por parte del cliente. 12 pantallas en Corozal.'},
  {r:'Portola',u:'San Francisco',c:'—',t:'',s:'pendiente',obs:'Seguimiento 25 mayo.'},
  {r:'Tacos El Rey',u:'Ubicaciones varias',c:'Yesenia Molina',t:'62958892',s:'sin-resp',obs:'Seguimiento 6 mayo. Sin respuesta.'},
  {r:'Applebees PTY',u:'Ubicaciones varias',c:'—',t:'',s:'sin-resp',obs:'Sin respuesta.'},
  {r:'Wings Famous Grill',u:'Multiplaza',c:'Erika Juarez',t:'62186696',s:'cerrado',obs:'Firma pendiente de confirmar fecha.'},
  {r:'Town Center',u:'Costa del Este',c:'Daiana',t:'',s:'otro',obs:'Entró como venta, no alianza.'},
  {r:'Brewjas',u:'Panamá Oeste',c:'—',t:'',s:'sin-resp',obs:'Esperando respuesta.'},
  {r:'Napoli',u:'Obarrio',c:'Anna Iovanne',t:'66414207',s:'otro',obs:'Decidieron no entrar.'},
  {r:'La Mandolina',u:'Santiago',c:'Ana Laura Virzi',t:'',s:'cerrado',obs:'Firma 16 mayo. Activos con Veracruz United.'},
  {r:'Efímero',u:'—',c:'Fady',t:'6450-5500',s:'sin-resp',obs:'Sin respuesta.'},
  {r:'Autódromo',u:'—',c:'Liz Navarro',t:'6747-8083',s:'sin-resp',obs:'Pendiente nueva fecha de reunión.'},
  {r:'5inco',u:'AltaPlaza Mall',c:'Paula',t:'6857-0873',s:'cerrado',obs:'Firma pendiente de confirmar fecha.'},
  {r:'Orale',u:'—',c:'Armando',t:'6629-1214',s:'sin-resp',obs:'Sin respuesta.'},
  {r:'Huekito Mexicano',u:'Costa del Este',c:'Miguelito',t:'6674-0302',s:'cerrado',obs:'Firma pendiente TVMAX confirme fecha.'},
  {r:'Park & Padel',u:'Obarrio',c:'Yhan Bazan',t:'',s:'cerrado',obs:'Maneja directamente la Brand Manager.'},
  {r:'Donde Arturo',u:'Chitré',c:'Arturo',t:'',s:'cerrado',obs:'Firma pendiente TVMAX confirme fecha.'},
  {r:'Salsa y Carbón',u:'—',c:'—',t:'',s:'sin-resp',obs:'Seguimiento 25 mayo.'},
  {r:'Hotel Guayacanes',u:'—',c:'Walkiria Ramos',t:'',s:'sin-resp',obs:'Seguimiento 25 mayo.'},
  {r:'El Callejón (Grupo Maito)',u:'Casco Viejo',c:'Mary De Luca',t:'6639-5230',s:'cerrado',obs:'Pendiente documento del cliente.'},
  {r:'Tacos La Neta (Grupo Maito)',u:'Brisas y Casco Viejo',c:'Mary De Luca',t:'',s:'cerrado',obs:'Pendiente documento del cliente.'},
  {r:'Asaito (Grupo Maito)',u:'Brisas',c:'Mary De Luca',t:'',s:'cerrado',obs:'Pendiente documento del cliente.'},
  {r:'Cervecería Industrial',u:'Panamá Oeste / La Chorrera',c:'Marcos',t:'6054-7060',s:'pendiente',obs:'Pendiente respuesta.'},
  {r:'La 10',u:'Colón',c:'Jonathan',t:'',s:'cerrado',obs:'Firma pendiente TVMAX confirme fecha.'},
  {r:'The Win',u:'Colón',c:'Jonathan',t:'',s:'cerrado',obs:'Firma pendiente TVMAX confirme fecha.'},
];

const defaultConfirmed=[
  {n:'Boho',l:'Río Abajo',c:'Franklyn Robinson',doc:'enviado',firma:'TBD',pase:'na',contenido:'pend'},
  {n:'Minuto7',l:'Calle Uruguay',c:'Juan Alvarado',doc:'enviado',firma:'5 mayo',pase:'5 mayo',contenido:'done'},
  {n:'5 to 5 Hilton',l:'Ave. Balboa',c:'Francesco Magri',doc:'enviado',firma:'8 mayo',pase:'na',contenido:'done'},
  {n:'The Yard',l:'San Francisco',c:'Jorge Castro',doc:'enviado',firma:'12 mayo',pase:'12 mayo',contenido:'done'},
  {n:'X3M',l:'Tumba Muerto',c:'Curtis',doc:'enviado',firma:'18 mayo',pase:'na',contenido:'pend'},
  {n:'PESKITO',l:'Altos/Costa Verde',c:'Abdiel Celis',doc:'enviado',firma:'14 mayo',pase:'na',contenido:'done'},
  {n:'Canal House',l:'Amador',c:'Germán',doc:'enviado',firma:'18 mayo',pase:'na',contenido:'done'},
  {n:'Feroz',l:'Ciudad del Saber',c:'Cesar Conto',doc:'enviado',firma:'18 mayo',pase:'na',contenido:'pend'},
  {n:'Club Unión Española',l:'Carrasquilla',c:'Luis Arias',doc:'enviado',firma:'26 mayo',pase:'na',contenido:'pend'},
  {n:'Dorado Mall',l:'El Dorado',c:'Victor',doc:'enviado',firma:'25 mayo',pase:'25 mayo',contenido:'done'},
  {n:'La Mandolina',l:'Santiago',c:'Ana Laura Virzi',doc:'enviado',firma:'16 mayo',pase:'na',contenido:'done'},
  {n:'Huekito Mexicano',l:'Costa del Este',c:'Miguelito',doc:'enviado',firma:'pend',pase:'na',contenido:'pend'},
  {n:'Central',l:'SF / Vía Argentina',c:'Carlos',doc:'enviado',firma:'pend',pase:'na',contenido:'pend'},
  {n:'5inco',l:'AltaPlaza Mall',c:'Paula',doc:'enviado',firma:'pend',pase:'na',contenido:'pend'},
  {n:'La 10 Colón',l:'Colón',c:'Jonathan',doc:'enviado',firma:'pend',pase:'na',contenido:'pend'},
  {n:'The Win',l:'Colón',c:'Jonathan',doc:'enviado',firma:'pend',pase:'na',contenido:'pend'},
  {n:'Donde Arturo',l:'Chitré',c:'Arturo',doc:'enviado',firma:'pend',pase:'na',contenido:'pend'},
  {n:'El Callejón',l:'Casco Viejo',c:'Mary de Luca',doc:'pend',firma:'pend',pase:'na',contenido:'pend'},
  {n:'Tacos La Neta',l:'Brisas / Casco',c:'Mary de Luca',doc:'pend',firma:'pend',pase:'na',contenido:'pend'},
  {n:'Asaito',l:'Brisas',c:'Mary de Luca',doc:'pend',firma:'pend',pase:'na',contenido:'pend'},
  {n:'Wings Famous Grill',l:'Multiplaza',c:'Erika Juarez',doc:'enviado',firma:'pend',pase:'na',contenido:'pend'},
  {n:'Brisas Capital',l:'Brisas',c:'Dexis',doc:'pend',firma:'pend',pase:'na',contenido:'pend'},
  {n:'Cervecería Industrial',l:'La Chorrera',c:'Marcos',doc:'pend',firma:'pend',pase:'na',contenido:'pend'},
  {n:'Park & Padel',l:'Obarrio',c:'Yhan Bazan',doc:'pend',firma:'pend',pase:'na',contenido:'pend'},
  {n:'Austin Mamas',l:'Corozal',c:'Sebastián',doc:'pend',firma:'pend',pase:'na',contenido:'pend'},
  {n:'Pintas Spot',l:'Calle 50',c:'Dainubys Sarmiento',doc:'enviado',firma:'pend',pase:'na',contenido:'pend'},
];

const logosDoneNames=['Boho','Minuto7','5 to 5 Hilton','The Yard','X3M','PESKITO','Canal House','Feroz','Club Unión Española','Dorado Mall','Huekito Mexicano','Central','5inco','La 10 Colón','The Win','Donde Arturo','El Callejón','Tacos La Neta','Asaito','Wings Famous Grill','Brisas Capital'];

function buildDefaultAssets(confirmed){
  return confirmed.map(c=>({
    n:c.n, contact:c.c,
    logo: logosDoneNames.some(x=>c.n.includes(x)||x.includes(c.n))?'recibido':'pend',
    mp:'pend', mm:'pend', st:'pend'
  }));
}

let prospects = JSON.parse(localStorage.getItem('tvmax_prospects_v2')||'null') || defaultProspects;
let confirmed = JSON.parse(localStorage.getItem('tvmax_confirmed_v2')||'null') || defaultConfirmed;
let assets = JSON.parse(localStorage.getItem('tvmax_assets_v2')||'null') || buildDefaultAssets(defaultConfirmed);

function save(){
  localStorage.setItem('tvmax_prospects_v2',JSON.stringify(prospects));
  localStorage.setItem('tvmax_confirmed_v2',JSON.stringify(confirmed));
  localStorage.setItem('tvmax_assets_v2',JSON.stringify(assets));
}

function updateMetrics(){
  const cerrados=prospects.filter(p=>p.s==='cerrado').length;
  const pend=prospects.filter(p=>p.s==='pendiente').length;
  const sinResp=prospects.filter(p=>p.s==='sin-resp').length;
  const otro=prospects.filter(p=>p.s==='otro').length;
  const firmasDone=confirmed.filter(c=>c.firma!=='pend'&&c.firma!=='TBD').length;
  document.getElementById('stat-cerrados').textContent=confirmed.length;
  document.getElementById('stat-proceso').textContent=pend;
  document.getElementById('m-cerrados').textContent=cerrados;
  document.getElementById('m-firmas').textContent=firmasDone;
  document.getElementById('m-pend').textContent=pend;
  document.getElementById('m-perdidos').textContent=sinResp+otro;
}

function badgeHTML(s){
  return {
    'cerrado':'<span class="badge cerrado">● Cerrado</span>',
    'pendiente':'<span class="badge pendiente">⏳ Pendiente</span>',
    'sin-resp':'<span class="badge sin-resp">● Sin respuesta</span>',
    'otro':'<span class="badge otro">● Perdido/Otro</span>'
  }[s]||s;
}

function renderProspects(){
  const rows=prospects.map((p,i)=>({...p,_i:i})).filter(p=>{
    const mf=currentFilter==='all'||p.s===currentFilter;
    const q=currentSearch.toLowerCase();
    const ms=!q||(p.r+p.u+p.c).toLowerCase().includes(q);
    return mf&&ms;
  });
  document.getElementById('prospect-body').innerHTML=rows.map((p,idx)=>`<tr>
    <td style="color:rgba(109,212,0,0.5);font-size:10px;">${idx+1}</td>
    <td style="font-weight:700;color:#fff;">${p.r}</td>
    <td style="color:rgba(255,255,255,0.55);font-size:11px;">${p.u||'—'}</td>
    <td style="font-size:11px;color:rgba(255,255,255,0.8);">${p.c||'—'}</td>
    <td style="font-size:11px;color:var(--green-text);">${p.t||'—'}</td>
    <td>${badgeHTML(p.s)}</td>
    <td class="obs-text">${p.obs}</td>
    <td><button class="edit-btn" onclick="openEditModal(${p._i})">Editar</button></td>
  </tr>`).join('');
}

function renderConfirmed(){
  document.getElementById('confirm-grid').innerHTML=confirmed.map((c,i)=>{
    const dd=c.doc==='enviado', fd=c.firma!=='pend'&&c.firma!=='TBD';
    const pd=c.pase!=='na'&&c.pase!=='pend', cd=c.contenido==='done';
    const fl=c.firma==='pend'?'Pendiente TVMAX':c.firma==='TBD'?'TBD - Esperando local':'✓ '+c.firma;
    return `<div class="confirm-card">
      <h3>${c.n}</h3>
      <div class="confirm-loc">📍 ${c.l} &nbsp;|&nbsp; 👤 ${c.c}</div>
      <div class="step-row"><div class="step-dot ${dd?'done':'pend'}"></div><span class="step-label">Documento de alianza</span><span class="step-val ${dd?'done':'pend'}">${dd?'Enviado':'Pendiente cliente'}</span></div>
      <div class="step-row"><div class="step-dot ${fd?'done':'pend'}"></div><span class="step-label">Firma simbólica</span><span class="step-val ${fd?'done':'pend'}" style="font-size:9px;">${fl}</span></div>
      <div class="step-row"><div class="step-dot ${pd?'done':c.pase==='na'?'na':'pend'}"></div><span class="step-label">Pase en vivo</span><span class="step-val ${pd?'done':c.pase==='na'?'na':'pend'}">${pd?'✓ Realizado':c.pase==='na'?'N/A':'Pendiente'}</span></div>
      <div class="step-row"><div class="step-dot ${cd?'done':'pend'}"></div><span class="step-label">Contenido firma</span><span class="step-val ${cd?'done':'pend'}">${cd?'✓ Listo':'Pendiente'}</span></div>
      <div style="margin-top:8px;"><button class="edit-btn" onclick="editConfirmed(${i})" style="width:100%;">Editar estado</button></div>
    </div>`;
  }).join('');
}

function renderAssets(){
  document.getElementById('assets-body').innerHTML=assets.map((a,i)=>{
    const fields=['logo','mp','mm','st'];
    const done=fields.filter(f=>a[f]==='recibido').length;
    const pct=Math.round((done/4)*100);
    const cs=v=>v==='recibido'?'color:#6DD400;':'color:#F5A623;';
    const ct=v=>v==='recibido'?'✅':'⏳';
    return `<tr>
      <td style="color:rgba(109,212,0,0.5);font-size:10px;">${i+1}</td>
      <td style="font-weight:700;color:#fff;font-size:12px;">${a.n}</td>
      <td style="font-size:11px;color:rgba(255,255,255,0.55);">${a.contact}</td>
      <td class="asset-cell-edit" style="${cs(a.logo)}" onclick="toggleAsset(${i},'logo')">${ct(a.logo)}</td>
      <td class="asset-cell-edit" style="${cs(a.mp)}" onclick="toggleAsset(${i},'mp')">${ct(a.mp)}</td>
      <td class="asset-cell-edit" style="${cs(a.mm)}" onclick="toggleAsset(${i},'mm')">${ct(a.mm)}</td>
      <td class="asset-cell-edit" style="${cs(a.st)}" onclick="toggleAsset(${i},'st')">${ct(a.st)}</td>
      <td style="min-width:70px;"><div style="font-size:11px;font-weight:700;color:${pct===100?'#6DD400':pct>50?'#F5A623':'#E53E3E'};">${pct}%</div><div class="pct-bar"><div class="pct-fill" style="width:${pct}%;background:${pct===100?'#6DD400':pct>50?'#F5A623':'#E53E3E'};"></div></div></td>
    </tr>`;
  }).join('');
}

function toggleAsset(i,f){
  assets[i][f]=assets[i][f]==='recibido'?'pend':'recibido';
  save(); renderAssets();
}

function renderOverview(){
  const total=prospects.length;
  const cerrados=prospects.filter(p=>p.s==='cerrado').length;
  const pend=prospects.filter(p=>p.s==='pendiente').length;
  const sinResp=prospects.filter(p=>p.s==='sin-resp').length;
  const otro=prospects.filter(p=>p.s==='otro').length;
  document.getElementById('funnel-chart').innerHTML=[
    {l:'Aliados cerrados',v:cerrados,c:'#6DD400',tc:'#0A1A0A'},
    {l:'En negociación',v:pend,c:'#F5A623',tc:'#0A1A0A'},
    {l:'Sin respuesta',v:sinResp,c:'#E53E3E',tc:'#fff'},
    {l:'Perdidos / otro',v:otro,c:'rgba(160,160,160,0.6)',tc:'#fff'},
  ].map(f=>`<div class="funnel-item"><span class="funnel-label">${f.l}</span><div class="funnel-bar-bg"><div class="funnel-bar-fill" style="width:${Math.round((f.v/total)*100)}%;background:${f.c};color:${f.tc};">&nbsp;${f.v}</div></div></div>`).join('');

  const fd=confirmed.filter(c=>c.firma!=='pend'&&c.firma!=='TBD').length;
  const fp=confirmed.filter(c=>c.firma==='pend'||c.firma==='TBD').length;
  document.getElementById('firma-chart').innerHTML=[
    {l:'Realizadas',v:fd,c:'#6DD400',tc:'#0A1A0A'},
    {l:'Pendientes',v:fp,c:'#F5A623',tc:'#0A1A0A'},
  ].map(f=>`<div class="funnel-item"><span class="funnel-label" style="font-size:10px;">${f.l}</span><div class="funnel-bar-bg" style="height:22px;"><div class="funnel-bar-fill" style="width:${Math.round((f.v/confirmed.length)*100)}%;background:${f.c};color:${f.tc};font-size:11px;">&nbsp;${f.v}</div></div></div>`).join('');

  const ld=assets.filter(a=>a.logo==='recibido').length;
  const pct=Math.round((ld/assets.length)*100);
  document.getElementById('assets-summary').innerHTML=`<div style="font-size:12px;color:rgba(255,255,255,0.75);margin-bottom:5px;">Logos recibidos: <strong style="color:#6DD400;">${ld}/${assets.length}</strong></div><div class="pct-bar" style="height:6px;"><div class="pct-fill" style="width:${pct}%;background:#6DD400;height:6px;"></div></div><div style="font-size:11px;color:rgba(255,255,255,0.35);margin-top:6px;">Menciones y Stories: pendientes de todos los aliados.</div>`;

  const zonas=[
    {l:'Ciudad de Panamá',v:confirmed.filter(c=>!['Santiago','Chitré','Colón','Chorrera'].some(z=>c.l.includes(z))).length,c:'rgba(109,212,0,0.7)'},
    {l:'Colón',v:confirmed.filter(c=>c.l.includes('Colón')).length,c:'rgba(99,179,237,0.7)'},
    {l:'Interior (Santiago / Chitré)',v:confirmed.filter(c=>['Santiago','Chitré'].some(z=>c.l.includes(z))).length,c:'rgba(245,166,35,0.7)'},
    {l:'Panamá Oeste / Chorrera',v:confirmed.filter(c=>c.l.includes('Chorrera')).length,c:'rgba(160,160,160,0.6)'},
  ];
  document.getElementById('zona-chart').innerHTML=zonas.map(z=>`<div class="funnel-item"><span class="funnel-label">${z.l}</span><div class="funnel-bar-bg"><div class="funnel-bar-fill" style="width:${Math.round((z.v/confirmed.length)*100)}%;background:${z.c};color:#0A1A0A;font-size:11px;">&nbsp;${z.v} aliados</div></div></div>`).join('');
}

function showTab(t,btn){
  document.querySelectorAll('.tab').forEach(b=>b.classList.remove('active'));
  document.querySelectorAll('.panel').forEach(p=>p.classList.remove('active'));
  btn.classList.add('active');
  document.getElementById('panel-'+t).classList.add('active');
  if(t==='overview') renderOverview();
}
function filterP(f,btn){
  currentFilter=f;
  document.querySelectorAll('.filter-btn').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
  renderProspects();
}
function searchP(v){currentSearch=v;renderProspects();}

function openAddModal(){
  editingIdx=-1;
  document.getElementById('modal-title').textContent='Agregar Prospecto';
  ['f-rest','f-ubi','f-cont','f-tel','f-obs'].forEach(id=>document.getElementById(id).value='');
  document.getElementById('f-status').value='pendiente';
  document.getElementById('btn-delete').style.display='none';
  document.getElementById('modal').classList.add('open');
}
function openEditModal(i){
  editingIdx=i;
  const p=prospects[i];
  document.getElementById('modal-title').textContent='Editar: '+p.r;
  document.getElementById('f-rest').value=p.r;
  document.getElementById('f-ubi').value=p.u;
  document.getElementById('f-cont').value=p.c;
  document.getElementById('f-tel').value=p.t;
  document.getElementById('f-status').value=p.s;
  document.getElementById('f-obs').value=p.obs;
  document.getElementById('btn-delete').style.display='inline-block';
  document.getElementById('modal').classList.add('open');
}
function closeModal(){document.getElementById('modal').classList.remove('open');}
function saveProspect(){
  const obj={r:document.getElementById('f-rest').value,u:document.getElementById('f-ubi').value,c:document.getElementById('f-cont').value,t:document.getElementById('f-tel').value,s:document.getElementById('f-status').value,obs:document.getElementById('f-obs').value};
  if(!obj.r){alert('Ingresa el nombre del restaurante.');return;}
  if(editingIdx===-1) prospects.push(obj);
  else prospects[editingIdx]=obj;
  save(); updateMetrics(); renderProspects(); closeModal();
}
function deleteProspect(){
  if(!confirm('¿Eliminar este prospecto?')) return;
  prospects.splice(editingIdx,1);
  save(); updateMetrics(); renderProspects(); closeModal();
}
function editConfirmed(i){
  const c=confirmed[i];
  const firma=prompt(`Firma de "${c.n}" (fecha realizada, "pend" o "TBD"):`,c.firma);
  if(firma===null) return;
  const pase=prompt('Pase en vivo (fecha realizada, "na" o "pend"):',c.pase);
  if(pase===null) return;
  const cont=prompt('Contenido firma ("done" o "pend"):',c.contenido);
  if(cont===null) return;
  const doc=prompt('Documento alianza ("enviado" o "pend"):',c.doc);
  if(doc===null) return;
  confirmed[i]={...c,firma:firma.trim(),pase:pase.trim(),contenido:cont.trim(),doc:doc.trim()};
  save(); updateMetrics(); renderConfirmed();
}
document.getElementById('modal').addEventListener('click',function(e){if(e.target===this)closeModal();});

updateMetrics(); renderProspects(); renderConfirmed(); renderAssets();
</script>
</body>
</html>
