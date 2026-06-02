<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Circuito TVMAX · Dashboard</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@900&family=Roboto:wght@400;500;700&display=swap" rel="stylesheet"/>
<style>
*{box-sizing:border-box;margin:0;padding:0;}
body{font-family:'Roboto',sans-serif;background:#0A1A0A;color:#fff;padding:20px;min-height:100vh;}
:root{
  --g:#6DD400;--gt:rgba(109,212,0,0.65);
  --card:#0E1E0E;--b:rgba(109,212,0,0.15);
  --am:#F5A623;--re:#E53E3E;--bl:#63B3ED;
  --mu:rgba(255,255,255,0.45);
}
.wrap{max-width:1280px;margin:0 auto;}

/* ── HERO ── */
.hero{background:linear-gradient(135deg,#0B2B0B,#0D1F0D 60%,#0A1A0A);border-radius:14px;padding:18px 24px;display:flex;align-items:center;justify-content:space-between;margin-bottom:14px;border:1px solid var(--b);}
.hero h1{font-family:'Poppins',sans-serif;font-weight:900;font-size:20px;color:var(--g);text-transform:uppercase;letter-spacing:1px;}
.hero p{font-size:11px;color:var(--gt);margin-top:2px;}
.kpis{display:flex;gap:8px;}
.kpi{border-radius:10px;padding:8px 16px;text-align:center;min-width:85px;border:1px solid;}
.kpi span{display:block;font-family:'Poppins',sans-serif;font-weight:900;font-size:26px;}
.kpi small{font-size:9px;text-transform:uppercase;letter-spacing:.5px;}
.kpi.g{border-color:var(--g);background:rgba(109,212,0,0.09);}  .kpi.g span,.kpi.g small{color:var(--g);}
.kpi.a{border-color:var(--am);background:rgba(245,166,35,0.09);} .kpi.a span,.kpi.a small{color:var(--am);}
.kpi.r{border-color:var(--re);background:rgba(229,62,62,0.07);}  .kpi.r span,.kpi.r small{color:var(--re);}
.kpi.b{border-color:var(--bl);background:rgba(99,179,237,0.07);} .kpi.b span,.kpi.b small{color:var(--bl);}

/* ── TABS ── */
.tabs{display:flex;gap:3px;margin-bottom:14px;background:var(--card);border-radius:10px;padding:4px;border:1px solid var(--b);}
.tab{flex:1;padding:10px 6px;border-radius:7px;font-size:12px;font-family:'Roboto',sans-serif;font-weight:700;cursor:pointer;border:none;background:transparent;color:rgba(255,255,255,0.5);transition:all .15s;}
.tab.active{background:var(--g);color:#0A1A0A;}
.tab:hover:not(.active){color:#fff;background:rgba(109,212,0,0.07);}
.panel{display:none;}.panel.active{display:block;}

/* ── TOOLBAR ── */
.toolbar{display:flex;gap:6px;margin-bottom:10px;flex-wrap:wrap;align-items:center;}
.srch{flex:1;min-width:200px;padding:8px 12px;background:var(--card);border:1px solid var(--b);border-radius:8px;color:#fff;font-size:12px;font-family:'Roboto',sans-serif;outline:none;}
.srch::placeholder{color:var(--mu);}
.srch:focus{border-color:rgba(109,212,0,.4);}
.chip{padding:5px 13px;border-radius:20px;font-size:11px;font-weight:700;cursor:pointer;border:1px solid rgba(109,212,0,.2);background:transparent;color:rgba(255,255,255,.5);transition:all .13s;font-family:'Roboto',sans-serif;}
.chip.on{background:var(--g);color:#0A1A0A;border-color:var(--g);}
.chip:hover:not(.on){color:#fff;border-color:rgba(109,212,0,.4);}

/* ── TABLE BASE ── */
.sx{overflow-x:auto;}
.tbl{width:100%;border-collapse:collapse;}
.tbl th{font-size:10px;color:var(--gt);text-transform:uppercase;letter-spacing:.7px;padding:9px 10px;text-align:left;border-bottom:1px solid var(--b);font-weight:700;background:rgba(109,212,0,0.03);white-space:nowrap;}
.tbl td{padding:8px 10px;font-size:12px;color:#fff;border-bottom:1px solid rgba(109,212,0,0.05);vertical-align:middle;}
.tbl tr:hover td{background:rgba(109,212,0,0.025);}
.tbl th.c,.tbl td.c{text-align:center;}
.note{font-size:11px;color:var(--mu);}

/* ── STATUS BADGES ── */
.s-ce{display:inline-block;padding:3px 9px;border-radius:12px;font-size:10px;font-weight:700;background:rgba(109,212,0,.13);color:#6DD400;border:1px solid rgba(109,212,0,.28);}
.s-pe{display:inline-block;padding:3px 9px;border-radius:12px;font-size:10px;font-weight:700;background:rgba(245,166,35,.13);color:#F5A623;border:1px solid rgba(245,166,35,.28);}
.s-sr{display:inline-block;padding:3px 9px;border-radius:12px;font-size:10px;font-weight:700;background:rgba(229,62,62,.13);color:#E53E3E;border:1px solid rgba(229,62,62,.28);}
.s-ot{display:inline-block;padding:3px 9px;border-radius:12px;font-size:10px;font-weight:700;background:rgba(150,150,150,.11);color:#999;border:1px solid rgba(150,150,150,.22);}
.obs{font-size:10px;color:rgba(255,255,255,.38);line-height:1.35;max-width:220px;}

/* ── FIRMAS: células de estado ── */
.ic-ok{color:#6DD400;font-size:15px;}
.ic-pe{color:#F5A623;font-size:13px;}
.ic-na{color:rgba(255,255,255,.2);font-size:13px;}
.ic-url{color:#63B3ED;font-size:13px;text-decoration:none;}
td.clk{cursor:pointer;}
td.clk:hover{background:rgba(109,212,0,.07)!important;}
.fecha{font-size:9px;color:rgba(255,255,255,.35);display:block;margin-top:2px;}

/* ── EDIT BUTTON ── */
.eb{background:rgba(109,212,0,.08);border:1px solid rgba(109,212,0,.16);color:#6DD400;border-radius:5px;padding:3px 9px;font-size:10px;font-weight:700;cursor:pointer;font-family:'Roboto',sans-serif;}
.eb:hover{background:rgba(109,212,0,.18);}

/* ── MODAL ── */
.mo{display:none;position:fixed;inset:0;background:rgba(0,0,0,.85);z-index:1000;align-items:center;justify-content:center;}
.mo.open{display:flex;}
.mbox{background:#0E1E0E;border:1px solid var(--b);border-radius:13px;padding:22px;width:560px;max-width:95vw;max-height:88vh;overflow-y:auto;}
.mbox h2{font-family:'Poppins',sans-serif;font-weight:900;font-size:14px;color:var(--g);margin-bottom:14px;}
.ml{font-size:10px;color:var(--mu);text-transform:uppercase;letter-spacing:.7px;margin-bottom:3px;display:block;font-weight:700;}
.mi,.ms,.mta{width:100%;padding:7px 10px;background:#0A1A0A;border:1px solid var(--b);border-radius:6px;color:#fff;font-size:12px;font-family:'Roboto',sans-serif;outline:none;margin-bottom:9px;}
.ms option{background:#0E1E0E;}
.mta{resize:vertical;min-height:60px;}
.f2{display:grid;grid-template-columns:1fr 1fr;gap:8px;}
.mbr{display:flex;gap:6px;justify-content:flex-end;margin-top:8px;}
.btn{padding:8px 17px;border-radius:6px;font-size:12px;font-family:'Roboto',sans-serif;font-weight:700;cursor:pointer;border:none;}
.btn-p{background:var(--g);color:#0A1A0A;}.btn-p:hover{background:#7EE600;}
.btn-d{background:rgba(229,62,62,.13);color:#E53E3E;border:1px solid rgba(229,62,62,.26);}
.btn-g{background:transparent;color:var(--mu);border:1px solid var(--b);}.btn-g:hover{color:#fff;}
.fab{position:fixed;bottom:22px;right:22px;background:var(--g);color:#0A1A0A;border:none;border-radius:50%;width:48px;height:48px;font-size:22px;font-weight:900;cursor:pointer;box-shadow:0 4px 16px rgba(109,212,0,.28);display:flex;align-items:center;justify-content:center;}
.fab:hover{transform:scale(1.07);}

/* ── FIRMAS RESUMEN CARDS ── */
.f-cards{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-bottom:16px;}
.f-card{background:var(--card);border:1px solid var(--b);border-radius:10px;padding:14px 16px;}
.f-card .num{font-family:'Poppins',sans-serif;font-weight:900;font-size:28px;line-height:1;}
.f-card .lbl{font-size:10px;color:var(--mu);text-transform:uppercase;letter-spacing:.7px;margin-top:3px;}
.f-card.g .num{color:var(--g);} .f-card.a .num{color:var(--am);} .f-card.b .num{color:var(--bl);} .f-card.r .num{color:var(--re);}
</style>
</head>
<body>
<div class="wrap">

<!-- HERO -->
<div class="hero">
  <div>
    <h1>Circuito TVMAX · Mundial 2026</h1>
    <p>Dashboard de control · 2 de junio de 2026</p>
  </div>
  <div class="kpis">
    <div class="kpi g"><span id="k-ce">0</span><small>Cerrados</small></div>
    <div class="kpi a"><span id="k-pe">0</span><small>Negociación</small></div>
    <div class="kpi r"><span id="k-sr">0</span><small>Sin respuesta</small></div>
    <div class="kpi b"><span id="k-to">0</span><small>Total</small></div>
  </div>
</div>

<!-- TABS -->
<div class="tabs">
  <button class="tab active" onclick="showTab('prospectos',this)">📋 Prospectos</button>
  <button class="tab" onclick="showTab('firmas',this)">🤝 Fase de Firmas</button>
</div>

<!-- ════════════════════════════════════════ -->
<!-- TAB 1 · PROSPECTOS                      -->
<!-- ════════════════════════════════════════ -->
<div id="panel-prospectos" class="panel active">
  <div class="toolbar">
    <input class="srch" type="text" placeholder="Buscar restaurante, contacto, ubicación..." oninput="buscar(this.value)"/>
    <button class="chip on"  onclick="filtrar('all',this)">Todos</button>
    <button class="chip" onclick="filtrar('ce',this)">✅ Cerrados</button>
    <button class="chip" onclick="filtrar('pe',this)">⏳ Negociación</button>
    <button class="chip" onclick="filtrar('sr',this)">🔴 Sin respuesta</button>
    <button class="chip" onclick="filtrar('ot',this)">⚫ Perdidos</button>
  </div>
  <div class="sx">
    <table class="tbl">
      <thead><tr>
        <th>#</th><th>Restaurante</th><th>Ubicación</th>
        <th>Contacto</th><th>Teléfono</th><th>Correo</th>
        <th>Status</th><th>Observaciones</th><th></th>
      </tr></thead>
      <tbody id="tb-p"></tbody>
    </table>
  </div>
</div>

<!-- ════════════════════════════════════════ -->
<!-- TAB 2 · FASE DE FIRMAS                  -->
<!-- ════════════════════════════════════════ -->
<div id="panel-firmas" class="panel">

  <!-- Mini KPIs firmas -->
  <div class="f-cards">
    <div class="f-card g"><div class="num" id="fk-firma-ok">0</div><div class="lbl">Firmas realizadas</div></div>
    <div class="f-card a"><div class="num" id="fk-firma-pe">0</div><div class="lbl">Firmas pendientes</div></div>
    <div class="f-card g"><div class="num" id="fk-cont-ok">0</div><div class="lbl">Contenido publicado</div></div>
    <div class="f-card b"><div class="num" id="fk-pase-ok">0</div><div class="lbl">Pases en vivo firma</div></div>
  </div>

  <div class="toolbar">
    <button class="chip on"  onclick="filtrarF('all',this)">Todos</button>
    <button class="chip" onclick="filtrarF('firma-ok',this)">✅ Firma realizada</button>
    <button class="chip" onclick="filtrarF('firma-pe',this)">⏳ Firma pendiente</button>
    <button class="chip" onclick="filtrarF('cont-ok',this)">📸 Con contenido</button>
    <button class="chip" onclick="filtrarF('pase-ok',this)">📺 Con pase en vivo</button>
  </div>

  <div class="sx">
    <table class="tbl">
      <thead><tr>
        <th>#</th>
        <th>Aliado</th>
        <th>Ubicación</th>
        <th>Contacto</th>
        <th class="c">Documento<br>alianza</th>
        <th class="c">Firma<br>simbólica</th>
        <th class="c">Contenido<br>de firma</th>
        <th class="c">Pase en<br>vivo firma</th>
        <th></th>
      </tr></thead>
      <tbody id="tb-f"></tbody>
    </table>
  </div>
</div>

</div><!-- /wrap -->

<button class="fab" onclick="abrirAdd()" title="Agregar">+</button>

<!-- MODAL PROSPECTO -->
<div class="mo" id="modal">
  <div class="mbox">
    <h2 id="m-tit">Prospecto</h2>
    <div class="f2">
      <div><label class="ml">Restaurante</label><input class="mi" id="m-r"/></div>
      <div><label class="ml">Ubicación</label><input class="mi" id="m-u"/></div>
    </div>
    <div class="f2">
      <div><label class="ml">Contacto</label><input class="mi" id="m-c"/></div>
      <div><label class="ml">Teléfono</label><input class="mi" id="m-t"/></div>
    </div>
    <label class="ml">Correo</label><input class="mi" id="m-e"/>
    <label class="ml">Status</label>
    <select class="ms" id="m-s">
      <option value="ce">✅ Acuerdo Cerrado</option>
      <option value="pe">⏳ En Negociación</option>
      <option value="sr">🔴 Sin Respuesta</option>
      <option value="ot">⚫ Perdido / Otro</option>
    </select>
    <label class="ml">Observaciones</label>
    <textarea class="mta" id="m-o"></textarea>
    <div class="mbr">
      <button class="btn btn-g" onclick="cerrarM()">Cancelar</button>
      <button class="btn btn-d" id="m-del" style="display:none" onclick="eliminarP()">Eliminar</button>
      <button class="btn btn-p" onclick="guardarP()">Guardar</button>
    </div>
  </div>
</div>

<script>
// ══════════════════════════════════════════════════════
// DATOS — Prospectos (del Excel hoja 1)
// ══════════════════════════════════════════════════════
const DEF_P = [
  {r:'Boho',u:'Río Abajo',c:'Franklyn Robinson',t:'6093-7160',e:'robinson.franklyn@gmail.com',s:'ce',o:'Fanfest exterior con I Star Panamá. Pendiente fecha firma simbólica.'},
  {r:'Minuto7',u:'Calle Uruguay',c:'Juan Alvarado',t:'6204-2886',e:'',s:'ce',o:'Firma y pase en vivo realizados el 5 de mayo.'},
  {r:'5 to 5 Hilton (Star Bay Casino)',u:'Hilton, Ave. Balboa',c:'Francesco Magri',t:'6053-3460',e:'francesco.magri@starbaycasino.com',s:'ce',o:'Firma 8 mayo. Pendiente confirmar participación de Jonathan Gutiérrez.'},
  {r:'Club Deportivo Unión Española',u:'Carrasquilla',c:'Luis Arias',t:'6030-0777',e:'',s:'ce',o:'Firma 26 mayo. Comunicar como club deportivo, no bar.'},
  {r:'La Manzana',u:'Santa Ana',c:'Edwards Molla',t:'6183-4712',e:'edwards@lamanzanapanama.com',s:'sr',o:'Evaluando vs Cable Onda Sports y RPC. Pendiente decisión final.'},
  {r:'Grill 50',u:'San Francisco, Calle 77',c:'Stefany García',t:'',e:'grillholdings@gmail.com',s:'ce',o:'Firma programada 4 de junio.'},
  {r:'La Rana Dorada',u:'Ubicaciones varias',c:'Blanca y Hernán',t:'',e:'',s:'ot',o:'Firmaron con otra plataforma.'},
  {r:'The Yard',u:'San Francisco',c:'Jorge Castro',t:'6611-8931',e:'',s:'ce',o:'Firma 12 mayo. Cuidar acuerdo con Balboa.'},
  {r:'Central Cervecería',u:'San Francisco',c:'Carlos',t:'6070-8066',e:'',s:'ce',o:'Firma realizada 1 de junio.'},
  {r:'Os Segredos Da Carne',u:'Marbella',c:'Rodolfo',t:'6835-7312',e:'',s:'pe',o:'Pendiente respuesta. Reunión agendada.'},
  {r:'Par de Pintas',u:'Calle Uruguay',c:'Ernesto Castillo',t:'6747-6615',e:'',s:'ce',o:'Firma programada 4 de junio.'},
  {r:'Feroz',u:'Ciudad del Saber',c:'Cesar Conto',t:'6090-7564',e:'',s:'ce',o:'Firma 18 mayo. Posible ceviche temático "La Marea Roja".'},
  {r:'Taberna 21',u:'Cangrejo',c:'—',t:'',e:'',s:'sr',o:'Sin respuesta.'},
  {r:'Bingo 90',u:'Obarrio',c:'Stephanie',t:'',e:'',s:'pe',o:'Propuesta enviada 29 mayo. 34 salas nacional. Pendiente respuesta interna.'},
  {r:'Entre Espumas (era Pintas Spot)',u:'Calle 50',c:'Dainubys Sarmiento',t:'6647-6772',e:'',s:'ce',o:'Firma realizada 1 de junio.'},
  {r:'Charro Mexicano',u:'—',c:'—',t:'',e:'',s:'sr',o:'Sin respuesta.'},
  {r:'Canal House Panama',u:'Amador',c:'Germán',t:'6315-3237',e:'',s:'ce',o:'Firma 18 mayo. 4-5 pantallas. Alto tráfico orgánico.'},
  {r:'X3M',u:'Tumba Muerto',c:'Curtis',t:'6264-6589',e:'',s:'ce',o:'Firma 18 mayo. Pendiente confirmar fecha.'},
  {r:'BlueTap House',u:'Ubicaciones varias',c:'Tomas Santos',t:'6237-5961',e:'',s:'ot',o:'Firmaron con RPC.'},
  {r:'Dorado Mall',u:'El Dorado',c:'Victor',t:'6612-8003',e:'',s:'ce',o:'Firma 25 mayo. Pase en vivo realizado.'},
  {r:'PESKITO',u:'Altos / Costa Verde',c:'Abdiel Celis',t:'6618-6973',e:'',s:'ce',o:'Firma 14 mayo.'},
  {r:'Austin Mamas',u:'Corozal y Costa Este',c:'Sebastián',t:'6898-6073',e:'',s:'ce',o:'Documento pendiente por cliente. 12 pantallas en Corozal.'},
  {r:'Portola',u:'San Francisco',c:'—',t:'',e:'',s:'pe',o:'Contactado 29 mayo. Pendiente respuesta.'},
  {r:'Tacos El Rey',u:'Ubicaciones varias',c:'Yesenia Molina',t:'62958892',e:'',s:'sr',o:'Sin respuesta desde 6 mayo.'},
  {r:'Applebees PTY',u:'Ubicaciones varias',c:'—',t:'',e:'',s:'sr',o:'Sin respuesta.'},
  {r:'Wings Famous Grill',u:'Multiplaza Mall',c:'Erika Juarez',t:'62186696',e:'erika.juarez@corporacionpiramide.com',s:'ce',o:'Firma programada 4 de junio.'},
  {r:'Town Center',u:'Costa del Este',c:'Daiana',t:'',e:'',s:'ot',o:'Entró como venta/patrocinio, no alianza.'},
  {r:'Brewjas',u:'Panamá Oeste',c:'—',t:'',e:'',s:'sr',o:'Sin respuesta.'},
  {r:'Napoli',u:'Obarrio',c:'Anna Iovanne',t:'66414207',e:'',s:'ot',o:'Decidieron no entrar.'},
  {r:'La Mandolina (Hotel Gran David)',u:'Santiago',c:'Ana Laura Virzi',t:'',e:'avirzi@supercarnes.com',s:'ce',o:'Firma 16 mayo. Alianza con Veracruz United.'},
  {r:'Efímero',u:'—',c:'Fady',t:'6450-5500',e:'',s:'sr',o:'Sin respuesta.'},
  {r:'Autódromo',u:'—',c:'Liz Navarro',t:'6747-8083',e:'',s:'sr',o:'Pendiente nueva fecha de reunión.'},
  {r:'5inco',u:'AltaPlaza Mall',c:'Agustín',t:'6629-1214',e:'',s:'ce',o:'Firma realizada 1 de junio.'},
  {r:'Orale',u:'—',c:'Armando',t:'6629-1214',e:'',s:'sr',o:'Sin respuesta.'},
  {r:'Huekito Mexicano',u:'Costa del Este',c:'Miguelito',t:'6674-0302',e:'',s:'ce',o:'Firma programada 2 de junio.'},
  {r:'Park & Padel',u:'Obarrio',c:'Yhan Bazan',t:'',e:'',s:'ce',o:'Pendiente propuesta TVMAX.'},
  {r:'Donde Arturo Bar y Parrillada',u:'Chitré',c:'Arturo',t:'',e:'',s:'ce',o:'Pendiente TVMAX confirme fecha firma.'},
  {r:'Salsa y Carbón',u:'Chitré',c:'John',t:'',e:'',s:'ce',o:'Pendiente TVMAX confirme fecha firma.'},
  {r:'Hotel Guayacanes',u:'—',c:'Walkiria Ramos',t:'',e:'',s:'sr',o:'Sin respuesta. Seguimiento 25 mayo.'},
  {r:'El Callejón (Grupo Maito)',u:'Casco Viejo',c:'Mary De Luca',t:'6639-5230',e:'',s:'ce',o:'Pendiente documento por cliente.'},
  {r:'Tacos La Neta (Grupo Maito)',u:'Brisas y Casco Viejo',c:'Mary De Luca',t:'',e:'',s:'ce',o:'Pendiente documento por cliente.'},
  {r:'Asaito (Grupo Maito)',u:'Brisas',c:'Mary De Luca',t:'',e:'',s:'ce',o:'Pendiente documento por cliente.'},
  {r:'Cervecería Industrial',u:'La Chorrera',c:'Marcos',t:'6054-7060',e:'',s:'ce',o:'Pendiente TVMAX confirme fecha firma.'},
  {r:'La 10',u:'Colón',c:'Jonathan',t:'',e:'',s:'ce',o:'Pendiente TVMAX confirme fecha firma.'},
  {r:'The Win',u:'Colón',c:'Jonathan',t:'',e:'',s:'ce',o:'Pendiente TVMAX confirme fecha firma.'},
  {r:'Taberna de Max by Habibis',u:'San Francisco',c:'Camila',t:'',e:'',s:'ce',o:'Firma programada 4 de junio.'},
  {r:'Brisas Capital',u:'Brisas',c:'Dexis',t:'',e:'',s:'ce',o:'Pendiente TVMAX confirme fecha firma.'},
];

// ══════════════════════════════════════════════════════
// DATOS — Fase de Firmas (del Excel hoja 2)
// doc: 'ok'|'pe-cli'|'pe-tvmax'
// firma: texto con fecha | 'pe-tvmax' | 'pe-prox' (próxima programada)
// cont: url | 'pe-subir' | 'pe-real' | 'na'
// pase: 'ok' | 'pe' | 'na'
// ══════════════════════════════════════════════════════
const DEF_F = [
  {n:'Boho',l:'Río Abajo',c:'Franklyn Robinson',doc:'ok',firma:'pe-tvmax',firmaTxt:'TBD — depende local',cont:'pe-real',pase:'pe'},
  {n:'Minuto7',l:'Calle Uruguay',c:'Juan Alvarado',doc:'ok',firma:'ok',firmaTxt:'✅ 5 de mayo',cont:'https://www.instagram.com/reel/DYIv5VaRcmq/',pase:'ok'},
  {n:'5 to 5 Hilton (Star Bay Casino)',l:'Ave. Balboa',c:'Francesco Magri',doc:'ok',firma:'ok',firmaTxt:'✅ 8 de mayo',cont:'https://www.instagram.com/p/DYFiwb_EZ5b/',pase:'na'},
  {n:'The Yard',l:'San Francisco',c:'Jorge Castro',doc:'ok',firma:'ok',firmaTxt:'✅ 12 de mayo',cont:'https://www.instagram.com/p/DYS6aX5xmi1/',pase:'ok'},
  {n:'X3M',l:'Tumba Muerto',c:'Curtis',doc:'ok',firma:'ok',firmaTxt:'✅ 18 de mayo',cont:'https://www.instagram.com/p/DY-lVrroWLG/',pase:'na'},
  {n:'PESKITO',l:'Altos / Costa Verde',c:'Abdiel Celis',doc:'ok',firma:'ok',firmaTxt:'✅ 14 de mayo',cont:'https://www.instagram.com/p/DYffF4ER2Xz/',pase:'na'},
  {n:'Canal House',l:'Amador',c:'Germán',doc:'ok',firma:'ok',firmaTxt:'✅ 18 de mayo',cont:'https://www.instagram.com/reels/DY5ANTJxHrc/',pase:'na'},
  {n:'Feroz',l:'Ciudad del Saber',c:'Cesar Conto',doc:'ok',firma:'ok',firmaTxt:'✅ 18 de mayo',cont:'https://www.instagram.com/p/DY9rYyPhq-p/',pase:'na'},
  {n:'Club Deportivo Unión Española',l:'Carrasquilla',c:'Luis Arias',doc:'ok',firma:'ok',firmaTxt:'✅ 26 de mayo',cont:'pe-subir',pase:'na'},
  {n:'Dorado Mall',l:'El Dorado',c:'Victor',doc:'ok',firma:'ok',firmaTxt:'✅ 25 de mayo',cont:'https://www.instagram.com/p/DYxymZ0EXId/',pase:'ok'},
  {n:'La Mandolina (Hotel Gran David)',l:'Santiago',c:'Ana Laura Virzi',doc:'ok',firma:'ok',firmaTxt:'✅ 16 de mayo',cont:'https://www.instagram.com/reels/DYxcFclRr2Z/',pase:'na'},
  {n:'Huekito Mexicano',l:'Costa del Este',c:'Miguelito',doc:'ok',firma:'pe-prox',firmaTxt:'⏳ 2 de junio',cont:'pe-real',pase:'na'},
  {n:'Central',l:'San Francisco / Vía Argentina / Costa Verde',c:'Carlos',doc:'ok',firma:'ok',firmaTxt:'✅ 1 de junio',cont:'pe-subir',pase:'na'},
  {n:'5inco',l:'AltaPlaza Mall',c:'Paula',doc:'ok',firma:'ok',firmaTxt:'✅ 1 de junio',cont:'pe-subir',pase:'na'},
  {n:'La 10 Colón',l:'Colón',c:'Jonathan',doc:'ok',firma:'pe-tvmax',firmaTxt:'⏳ Pendiente TVMAX',cont:'pe-real',pase:'na'},
  {n:'The Win (Colón)',l:'Colón',c:'—',doc:'ok',firma:'pe-tvmax',firmaTxt:'⏳ Pendiente TVMAX',cont:'pe-real',pase:'na'},
  {n:'Donde Arturo',l:'Chitré',c:'Arturo',doc:'ok',firma:'pe-tvmax',firmaTxt:'⏳ Pendiente TVMAX',cont:'pe-real',pase:'na'},
  {n:'El Callejón',l:'Casco Viejo',c:'Mary de Luca',doc:'pe-cli',firma:'pe-tvmax',firmaTxt:'⏳ Pendiente TVMAX',cont:'pe-real',pase:'na'},
  {n:'Tacos La Neta',l:'Brisas y Casco Viejo',c:'—',doc:'pe-cli',firma:'pe-cli',firmaTxt:'⏳ Pendiente cliente',cont:'pe-real',pase:'na'},
  {n:'Asaito',l:'Brisas',c:'—',doc:'pe-cli',firma:'pe-cli',firmaTxt:'⏳ Pendiente cliente',cont:'pe-real',pase:'na'},
  {n:'Wings Famous Grill',l:'Multiplaza Mall',c:'Erika Juarez',doc:'ok',firma:'pe-prox',firmaTxt:'⏳ 4 de junio',cont:'pe-real',pase:'na'},
  {n:'Brisas Capital',l:'Brisas',c:'Dexis',doc:'ok',firma:'pe-tvmax',firmaTxt:'⏳ Pendiente TVMAX',cont:'pe-real',pase:'pe'},
  {n:'Cervecería Industrial',l:'La Chorrera',c:'Marcos',doc:'ok',firma:'pe-tvmax',firmaTxt:'⏳ Pendiente TVMAX',cont:'pe-real',pase:'na'},
  {n:'Park & Padel',l:'Obarrio',c:'Yhan Bazan',doc:'pe-tvmax',firma:'pe-tvmax',firmaTxt:'⏳ Pendiente TVMAX',cont:'pe-real',pase:'pe'},
  {n:'Austin Mamas',l:'Corozal',c:'Sebastián',doc:'pe-cli',firma:'pe-tvmax',firmaTxt:'⏳ Pendiente TVMAX',cont:'pe-real',pase:'pe'},
  {n:'Entre Espumas',l:'Calle 50',c:'Dainubys Sarmiento',doc:'ok',firma:'ok',firmaTxt:'✅ 1 de junio',cont:'pe-subir',pase:'na'},
  {n:'Taberna de Max by Habibis',l:'San Francisco',c:'Camila',doc:'ok',firma:'pe-prox',firmaTxt:'⏳ 4 de junio',cont:'pe-real',pase:'na'},
  {n:'Salsa y Carbón',l:'Chitré',c:'John',doc:'ok',firma:'pe-tvmax',firmaTxt:'⏳ Pendiente TVMAX',cont:'pe-real',pase:'na'},
  {n:'Grill 50',l:'San Francisco',c:'Stefany',doc:'ok',firma:'pe-prox',firmaTxt:'⏳ 4 de junio',cont:'pe-real',pase:'na'},
  {n:'Par de Pintas',l:'Calle Uruguay',c:'Ernesto',doc:'pe-cli',firma:'pe-prox',firmaTxt:'⏳ 4 de junio',cont:'pe-real',pase:'na'},
];

// ══════════════════════════════════════════════════════
// STATE
// ══════════════════════════════════════════════════════
let P = JSON.parse(localStorage.getItem('tvx5_p')||'null') || DEF_P;
let F = JSON.parse(localStorage.getItem('tvx5_f')||'null') || DEF_F;

let editIdx=-1, curFP='all', curBP='', curFF='all';

function save(){
  localStorage.setItem('tvx5_p',JSON.stringify(P));
  localStorage.setItem('tvx5_f',JSON.stringify(F));
}

// ══════════════════════════════════════════════════════
// HELPERS
// ══════════════════════════════════════════════════════
function bdg(s){
  return {
    ce:'<span class="s-ce">✅ Cerrado</span>',
    pe:'<span class="s-pe">⏳ Negociación</span>',
    sr:'<span class="s-sr">🔴 Sin respuesta</span>',
    ot:'<span class="s-ot">⚫ Perdido</span>'
  }[s]||s;
}

function docIcon(v){
  if(v==='ok') return '<span class="ic-ok">✅</span>';
  if(v==='pe-cli') return '<span class="ic-pe" title="Pendiente cliente">⏳ cliente</span>';
  if(v==='pe-tvmax') return '<span class="ic-pe" title="Pendiente TVMAX">⏳ TVMAX</span>';
  return '<span class="ic-pe">⏳</span>';
}

function firmaIcon(f, txt){
  if(f==='ok') return `<span class="ic-ok">✅</span><span class="fecha">${txt.replace('✅ ','')}</span>`;
  if(f==='pe-prox') return `<span class="ic-pe">⏳</span><span class="fecha">${txt.replace('⏳ ','')}</span>`;
  if(f==='pe-tvmax') return `<span class="ic-pe">⏳</span><span class="fecha">Pend. TVMAX</span>`;
  if(f==='pe-cli') return `<span class="ic-pe">⏳</span><span class="fecha">Pend. cliente</span>`;
  return '<span class="ic-pe">⏳</span>';
}

function contIcon(v){
  if(v && v.startsWith('http'))
    return `<a class="ic-url" href="${v}" target="_blank" title="Ver contenido">📸 Ver</a>`;
  if(v==='pe-subir') return '<span class="ic-pe" title="Realizado, pendiente subir">📤 Subir</span>';
  if(v==='pe-real') return '<span class="ic-pe">⏳ Pendiente</span>';
  if(v==='na') return '<span class="ic-na">—</span>';
  return '<span class="ic-pe">⏳</span>';
}

function paseIcon(v){
  if(v==='ok') return '<span class="ic-ok">✅</span>';
  if(v==='pe') return '<span class="ic-pe">⏳</span>';
  if(v==='na') return '<span class="ic-na">—</span>';
  return '<span class="ic-pe">⏳</span>';
}

// ══════════════════════════════════════════════════════
// RENDER PROSPECTOS
// ══════════════════════════════════════════════════════
function rP(){
  const rows = P.map((p,i)=>({...p,_i:i})).filter(p=>{
    const mf = curFP==='all' || p.s===curFP;
    const ms = !curBP || (p.r+p.u+p.c+p.e).toLowerCase().includes(curBP);
    return mf && ms;
  });
  document.getElementById('tb-p').innerHTML = rows.map((p,i)=>`<tr>
    <td style="color:rgba(109,212,0,.4);font-size:10px;">${i+1}</td>
    <td style="font-weight:700;">${p.r}</td>
    <td style="font-size:11px;color:var(--mu);">${p.u||'—'}</td>
    <td style="font-size:11px;">${p.c||'—'}</td>
    <td style="font-size:11px;color:var(--gt);">${p.t||'—'}</td>
    <td style="font-size:10px;color:rgba(99,179,237,.65);">${p.e||'—'}</td>
    <td>${bdg(p.s)}</td>
    <td class="obs">${p.o}</td>
    <td><button class="eb" onclick="abrirEdit(${p._i})">Editar</button></td>
  </tr>`).join('');

  // KPIs
  const ce = P.filter(x=>x.s==='ce').length;
  const pe = P.filter(x=>x.s==='pe').length;
  const sr = P.filter(x=>x.s==='sr').length;
  document.getElementById('k-ce').textContent = ce;
  document.getElementById('k-pe').textContent = pe;
  document.getElementById('k-sr').textContent = sr;
  document.getElementById('k-to').textContent = P.length;
}

// ══════════════════════════════════════════════════════
// RENDER FIRMAS
// ══════════════════════════════════════════════════════
function rF(){
  // KPIs firmas
  const firmaOk = F.filter(f=>f.firma==='ok').length;
  const firmaPe = F.filter(f=>f.firma!=='ok').length;
  const contOk  = F.filter(f=>f.cont && f.cont.startsWith('http')).length;
  const paseOk  = F.filter(f=>f.pase==='ok').length;
  document.getElementById('fk-firma-ok').textContent = firmaOk;
  document.getElementById('fk-firma-pe').textContent = firmaPe;
  document.getElementById('fk-cont-ok').textContent  = contOk;
  document.getElementById('fk-pase-ok').textContent  = paseOk;

  const rows = F.filter(f=>{
    if(curFF==='all') return true;
    if(curFF==='firma-ok') return f.firma==='ok';
    if(curFF==='firma-pe') return f.firma!=='ok';
    if(curFF==='cont-ok')  return f.cont && f.cont.startsWith('http');
    if(curFF==='pase-ok')  return f.pase==='ok';
    return true;
  });

  document.getElementById('tb-f').innerHTML = rows.map((f,i)=>{
    const realIdx = F.indexOf(f);
    return `<tr>
      <td style="color:rgba(109,212,0,.4);font-size:10px;">${i+1}</td>
      <td style="font-weight:700;">${f.n}</td>
      <td style="font-size:10px;color:var(--mu);">${f.l}</td>
      <td style="font-size:11px;">${f.c}</td>
      <td class="c clk" onclick="togDoc(${realIdx})" title="Clic para cambiar">${docIcon(f.doc)}</td>
      <td class="c clk" onclick="editFirma(${realIdx})" title="Clic para editar">${firmaIcon(f.firma, f.firmaTxt)}</td>
      <td class="c clk" onclick="editCont(${realIdx})" title="Clic para editar">${contIcon(f.cont)}</td>
      <td class="c clk" onclick="togPase(${realIdx})" title="Clic para cambiar">${paseIcon(f.pase)}</td>
      <td></td>
    </tr>`;
  }).join('');
}

// ── TOGGLES FIRMAS ──
function togDoc(i){
  const ciclo = ['ok','pe-cli','pe-tvmax'];
  const cur = F[i].doc;
  F[i].doc = ciclo[(ciclo.indexOf(cur)+1)%ciclo.length];
  save(); rF();
}

function editFirma(i){
  const v = prompt('Fecha de firma (ej: "12 de mayo"), o escribe "pe-tvmax" / "pe-cli" / "pe-prox fecha":',
    F[i].firmaTxt.replace('✅ ','').replace('⏳ ',''));
  if(v===null) return;
  const val = v.trim();
  if(val==='pe-tvmax'||val==='pe-cli'||val==='pe-prox') {
    F[i].firma = val; F[i].firmaTxt = '⏳ '+val.replace('pe-','');
  } else if(val.startsWith('pe-')) {
    F[i].firma='pe-prox'; F[i].firmaTxt='⏳ '+val.replace('pe-','');
  } else {
    F[i].firma='ok'; F[i].firmaTxt='✅ '+val;
  }
  save(); rF();
}

function editCont(i){
  const v = prompt('URL del contenido, "pe-subir" (listo, sin subir), "pe-real" (pendiente) o "na":',
    F[i].cont);
  if(v===null) return;
  F[i].cont = v.trim();
  save(); rF();
}

function togPase(i){
  const ciclo = ['ok','pe','na'];
  const cur = F[i].pase;
  F[i].pase = ciclo[(ciclo.indexOf(cur)+1)%ciclo.length];
  save(); rF();
}

// ══════════════════════════════════════════════════════
// TABS / FILTERS
// ══════════════════════════════════════════════════════
function showTab(t,btn){
  document.querySelectorAll('.tab').forEach(b=>b.classList.remove('active'));
  document.querySelectorAll('.panel').forEach(p=>p.classList.remove('active'));
  btn.classList.add('active');
  document.getElementById('panel-'+t).classList.add('active');
}

function filtrar(f,btn){
  curFP=f;
  document.querySelectorAll('#panel-prospectos .chip').forEach(b=>b.classList.remove('on'));
  btn.classList.add('on'); rP();
}
function buscar(v){ curBP=v.toLowerCase(); rP(); }

function filtrarF(f,btn){
  curFF=f;
  document.querySelectorAll('#panel-firmas .chip').forEach(b=>b.classList.remove('on'));
  btn.classList.add('on'); rF();
}

// ══════════════════════════════════════════════════════
// MODAL PROSPECTO
// ══════════════════════════════════════════════════════
function abrirAdd(){
  editIdx=-1;
  document.getElementById('m-tit').textContent='Agregar Prospecto';
  ['m-r','m-u','m-c','m-t','m-e','m-o'].forEach(id=>document.getElementById(id).value='');
  document.getElementById('m-s').value='pe';
  document.getElementById('m-del').style.display='none';
  document.getElementById('modal').classList.add('open');
}
function abrirEdit(i){
  editIdx=i;
  const p=P[i];
  document.getElementById('m-tit').textContent='Editar: '+p.r;
  document.getElementById('m-r').value=p.r;
  document.getElementById('m-u').value=p.u;
  document.getElementById('m-c').value=p.c;
  document.getElementById('m-t').value=p.t;
  document.getElementById('m-e').value=p.e;
  document.getElementById('m-s').value=p.s;
  document.getElementById('m-o').value=p.o;
  document.getElementById('m-del').style.display='inline-block';
  document.getElementById('modal').classList.add('open');
}
function cerrarM(){ document.getElementById('modal').classList.remove('open'); }
function guardarP(){
  const o={r:document.getElementById('m-r').value,u:document.getElementById('m-u').value,
    c:document.getElementById('m-c').value,t:document.getElementById('m-t').value,
    e:document.getElementById('m-e').value,s:document.getElementById('m-s').value,
    o:document.getElementById('m-o').value};
  if(!o.r){alert('Ingresa el nombre del restaurante.');return;}
  if(editIdx===-1) P.push(o); else P[editIdx]=o;
  save(); rP(); cerrarM();
}
function eliminarP(){
  if(!confirm('¿Eliminar este prospecto?')) return;
  P.splice(editIdx,1); save(); rP(); cerrarM();
}
document.getElementById('modal').addEventListener('click',function(e){if(e.target===this)cerrarM();});

// ══════════════════════════════════════════════════════
// INIT
// ══════════════════════════════════════════════════════
rP(); rF();
</script>
</body>
</html>
