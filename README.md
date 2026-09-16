<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>EFiS — Gestión de Estructura</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500;600&display=swap');
:root {
  --bg: #f0f2f5;
  --surface: #ffffff;
  --surface2: #f8f9fb;
  --border: #e2e6ed;
  --border2: #cdd3dc;
  --accent: #0f7b6c;
  --accent-light: #e6f4f2;
  --accent2: #2563eb;
  --accent2-light: #eff6ff;
  --warn: #d97706;
  --warn-light: #fffbeb;
  --danger: #dc2626;
  --danger-light: #fef2f2;
  --success: #16a34a;
  --success-light: #f0fdf4;
  --purple: #7c3aed;
  --purple-light: #f5f3ff;
  --text: #1e293b;
  --text2: #475569;
  --muted: #94a3b8;
  --mono: 'JetBrains Mono', monospace;
  --sans: 'Inter', sans-serif;
  --radius: 8px;
  --shadow: 0 1px 3px rgba(0,0,0,.08), 0 1px 2px rgba(0,0,0,.04);
  --shadow-md: 0 4px 12px rgba(0,0,0,.1), 0 2px 4px rgba(0,0,0,.06);
  --dup-pos: rgba(220,38,38,.08);
  --dup-dni: rgba(217,119,6,.08);
  --dup-both: rgba(124,58,237,.1);
}
* { box-sizing: border-box; margin: 0; padding: 0; }
body { background: var(--bg); color: var(--text); font-family: var(--sans); font-size: 13px; min-height: 100vh; }

/* HEADER */
header {
  background: var(--surface);
  border-bottom: 1px solid var(--border);
  padding: 0 24px;
  display: flex;
  align-items: center;
  gap: 20px;
  height: 54px;
  position: sticky;
  top: 0;
  z-index: 100;
  box-shadow: var(--shadow);
}
.logo { font-family: var(--mono); font-size: 14px; font-weight: 600; color: var(--accent); letter-spacing: .02em; white-space: nowrap; }
.logo span { color: var(--muted); font-weight: 400; }
.tabs { display: flex; gap: 4px; margin-left: auto; }
.tab { padding: 6px 16px; border-radius: 6px; cursor: pointer; font-family: var(--sans); font-size: 12px; font-weight: 500; color: var(--text2); border: none; background: transparent; transition: all .15s; }
.tab:hover { color: var(--text); background: var(--surface2); }
.tab.active { color: var(--accent); background: var(--accent-light); font-weight: 600; }

/* STATS BAR */
.stats-bar { display: flex; gap: 1px; background: var(--border); border-bottom: 1px solid var(--border); }
.stat-card { flex: 1; background: var(--surface); padding: 12px 18px; display: flex; flex-direction: column; gap: 3px; }
.stat-label { font-size: 10px; font-weight: 600; color: var(--muted); letter-spacing: .06em; text-transform: uppercase; }
.stat-value { font-family: var(--mono); font-size: 22px; font-weight: 700; color: var(--text); }
.sv-green { color: var(--success); }
.sv-yellow { color: var(--warn); }
.sv-red { color: var(--danger); }
.sv-blue { color: var(--accent2); }
.sv-teal { color: var(--accent); }
.sv-pur { color: var(--purple); }

/* MAIN */
.main { padding: 16px 24px; }
.section-header { display: flex; align-items: center; gap: 8px; margin-bottom: 14px; flex-wrap: wrap; }
.panel-title { font-size: 11px; font-weight: 700; color: var(--text2); letter-spacing: .08em; text-transform: uppercase; }

/* FILTERS */
.filters { display: flex; gap: 6px; margin-bottom: 12px; flex-wrap: wrap; align-items: center; }
.fi { background: var(--surface); border: 1px solid var(--border2); color: var(--text); padding: 6px 10px; border-radius: 6px; font-family: var(--sans); font-size: 12px; outline: none; transition: border .15s, box-shadow .15s; }
.fi:focus { border-color: var(--accent); box-shadow: 0 0 0 3px rgba(15,123,108,.12); }
.fi::placeholder { color: var(--muted); }
.fi-search { flex: 1; min-width: 200px; }
.fi-sel { min-width: 150px; cursor: pointer; }
.fi-sm { min-width: 120px; }

/* BUTTONS */
.btn { padding: 6px 14px; border-radius: 6px; border: none; cursor: pointer; font-family: var(--sans); font-size: 12px; font-weight: 500; transition: all .15s; white-space: nowrap; display: inline-flex; align-items: center; gap: 5px; }
.btn-p { background: var(--accent); color: #fff; }
.btn-p:hover { background: #0a6459; box-shadow: var(--shadow); }
.btn-s { background: var(--surface); color: var(--text2); border: 1px solid var(--border2); }
.btn-s:hover { border-color: var(--accent); color: var(--accent); background: var(--accent-light); }
.btn-d { background: var(--danger-light); color: var(--danger); border: 1px solid rgba(220,38,38,.25); }
.btn-d:hover { background: #fee2e2; }
.btn-w { background: var(--warn-light); color: var(--warn); border: 1px solid rgba(217,119,6,.25); }
.btn-w:hover { background: #fef3c7; }
.btn-pur { background: var(--purple-light); color: var(--purple); border: 1px solid rgba(124,58,237,.25); }
.btn-pur:hover { background: #ede9fe; }

/* BADGE FILTERS */
.fbadge { display: inline-flex; align-items: center; gap: 5px; padding: 6px 10px; border-radius: 6px; font-size: 11px; font-weight: 500; cursor: pointer; border: 1px solid var(--border2); background: var(--surface); color: var(--text2); transition: all .15s; white-space: nowrap; }
.fbadge:hover { border-color: var(--border2); background: var(--surface2); }
.fbadge.on { border-color: var(--warn); color: var(--warn); background: var(--warn-light); }
.fbadge.on-r { border-color: var(--danger); color: var(--danger); background: var(--danger-light); }

/* TABLE */
.tw { background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius); overflow: auto; box-shadow: var(--shadow); }
table { width: 100%; border-collapse: collapse; font-size: 12px; }
thead { background: var(--surface2); }
th { text-align: left; padding: 10px 12px; font-size: 10px; font-weight: 700; color: var(--text2); letter-spacing: .07em; text-transform: uppercase; white-space: nowrap; border-bottom: 1px solid var(--border); cursor: pointer; user-select: none; }
th:hover { color: var(--accent); }
td { padding: 8px 12px; border-bottom: 1px solid var(--border); vertical-align: middle; max-width: 180px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; color: var(--text); }
tr:last-child td { border-bottom: none; }
tr:hover td { background: var(--surface2); }
tr.vac td { background: #fffbeb; }
tr.vac:hover td { background: #fef3c7; }
tr.dup-pos td { background: var(--dup-pos); }
tr.dup-dni td { background: var(--dup-dni); }
tr.dup-both td { background: var(--dup-both); }

/* TAGS */
.tag { display: inline-block; padding: 2px 7px; border-radius: 4px; font-size: 10px; font-weight: 600; white-space: nowrap; }
.tg { background: var(--success-light); color: var(--success); border: 1px solid rgba(22,163,74,.2); }
.ty { background: var(--warn-light); color: var(--warn); border: 1px solid rgba(217,119,6,.2); }
.tr { background: var(--danger-light); color: var(--danger); border: 1px solid rgba(220,38,38,.2); }
.tb { background: var(--accent2-light); color: var(--accent2); border: 1px solid rgba(37,99,235,.2); }
.tgr { background: #f1f5f9; color: var(--text2); border: 1px solid var(--border); }
.tp { background: var(--purple-light); color: var(--purple); border: 1px solid rgba(124,58,237,.2); }
.tteal { background: var(--accent-light); color: var(--accent); border: 1px solid rgba(15,123,108,.2); }

.ceco { font-family: var(--mono); font-size: 11px; color: var(--accent); font-weight: 500; }
.pos { font-family: var(--mono); font-size: 11px; color: var(--text2); }
.pname { font-weight: 500; color: var(--text); }
.vacl { color: var(--warn); font-weight: 600; font-style: italic; }
.dup-icon { font-size: 10px; margin-left: 3px; cursor: help; color: var(--danger); }

/* ROW ACTIONS */
.ract { display: flex; gap: 3px; opacity: 0; transition: opacity .15s; }
tr:hover .ract { opacity: 1; }
.ab { padding: 3px 8px; border-radius: 4px; font-size: 10px; font-weight: 600; border: none; cursor: pointer; transition: all .15s; }
.ab-e { background: var(--accent2-light); color: var(--accent2); }
.ab-e:hover { background: #dbeafe; }
.ab-m { background: var(--accent-light); color: var(--accent); }
.ab-m:hover { background: #ccede9; }
.ab-d { background: var(--danger-light); color: var(--danger); }
.ab-d:hover { background: #fee2e2; }
.ab-u { background: var(--warn-light); color: var(--warn); }
.ab-u:hover { background: #fef3c7; }

/* DUP LEGEND */
.dup-legend { display: flex; gap: 14px; align-items: center; padding: 8px 12px; background: var(--surface); border: 1px solid var(--border); border-radius: 6px; margin-bottom: 10px; flex-wrap: wrap; }
.dl-item { display: flex; align-items: center; gap: 6px; font-size: 11px; color: var(--text2); font-weight: 500; }
.dl-dot { width: 12px; height: 12px; border-radius: 3px; flex-shrink: 0; }

/* MODAL */
.modal-bd { display: none; position: fixed; inset: 0; background: rgba(15,23,42,.45); z-index: 200; align-items: center; justify-content: center; backdrop-filter: blur(2px); }
.modal-bd.open { display: flex; }
.modal { background: var(--surface); border: 1px solid var(--border); border-radius: 12px; width: 620px; max-width: 96vw; max-height: 92vh; overflow-y: auto; box-shadow: var(--shadow-md); }
.modal-lg { width: 760px; }
.mh { padding: 16px 20px; border-bottom: 1px solid var(--border); display: flex; align-items: center; justify-content: space-between; position: sticky; top: 0; background: var(--surface); z-index: 1; border-radius: 12px 12px 0 0; }
.mt { font-size: 14px; font-weight: 700; color: var(--text); }
.mt-sub { font-size: 12px; color: var(--text2); font-weight: 400; margin-top: 2px; }
.mc { background: var(--surface2); border: 1px solid var(--border); color: var(--text2); cursor: pointer; font-size: 14px; line-height: 1; width: 28px; height: 28px; border-radius: 6px; display: flex; align-items: center; justify-content: center; }
.mc:hover { background: var(--border); color: var(--text); }
.mb { padding: 20px; display: flex; flex-direction: column; gap: 14px; }
.mf { padding: 14px 20px; border-top: 1px solid var(--border); display: flex; gap: 8px; justify-content: flex-end; position: sticky; bottom: 0; background: var(--surface); border-radius: 0 0 12px 12px; }
.fg { display: flex; flex-direction: column; gap: 5px; }
.fl { font-size: 11px; font-weight: 600; color: var(--text2); letter-spacing: .04em; }
.finp { background: var(--surface); border: 1px solid var(--border2); color: var(--text); padding: 8px 12px; border-radius: 6px; font-family: var(--sans); font-size: 13px; outline: none; transition: border .15s, box-shadow .15s; width: 100%; }
.finp:focus { border-color: var(--accent); box-shadow: 0 0 0 3px rgba(15,123,108,.12); }
.finp[readonly] { background: var(--surface2); color: var(--text2); }
.fr { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
.fr3 { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 12px; }
.section-divider { font-size: 11px; font-weight: 700; color: var(--text2); padding: 8px 0 4px; border-top: 1px solid var(--border); margin-top: 4px; letter-spacing: .05em; text-transform: uppercase; }

/* ALERTS */
.alert { padding: 10px 14px; border-radius: 6px; font-size: 12px; border-left: 3px solid; }
.al-w { background: var(--warn-light); border-color: var(--warn); color: #92400e; }
.al-i { background: var(--accent2-light); border-color: var(--accent2); color: #1e40af; }
.al-s { background: var(--success-light); border-color: var(--success); color: #14532d; }
.al-r { background: var(--danger-light); border-color: var(--danger); color: #7f1d1d; }

/* PAGES */
.page { display: none; } .page.active { display: block; }

/* PAGINATION */
.pg { display: flex; align-items: center; gap: 8px; margin-top: 10px; justify-content: flex-end; }
.pi { font-size: 12px; color: var(--text2); }

/* SERVICE CARDS */
.sg { display: grid; grid-template-columns: repeat(auto-fill, minmax(290px, 1fr)); gap: 10px; }
.sc { background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius); padding: 14px 16px; display: flex; flex-direction: column; gap: 8px; transition: box-shadow .15s, border-color .15s; box-shadow: var(--shadow); }
.sc:hover { border-color: var(--accent); box-shadow: var(--shadow-md); }
.sch { display: flex; justify-content: space-between; align-items: flex-start; }
.sct { font-size: 12px; font-weight: 600; color: var(--text); line-height: 1.3; }
.sb { height: 5px; background: var(--border); border-radius: 3px; overflow: hidden; }
.sbf { height: 100%; border-radius: 3px; background: linear-gradient(90deg, var(--accent), var(--accent2)); transition: width .4s; }
.sn { display: flex; gap: 16px; }
.snv { font-family: var(--mono); font-size: 17px; font-weight: 700; }
.snl { font-size: 10px; color: var(--muted); font-weight: 500; margin-top: 1px; }

/* CHANGELOG */
.cli { border-left: 3px solid var(--border); padding: 10px 14px; display: flex; flex-direction: column; gap: 3px; border-radius: 0 6px 6px 0; background: var(--surface); margin-bottom: 4px; transition: border-color .15s; }
.cli:hover { border-color: var(--accent); }
.cld { font-size: 11px; color: var(--muted); font-family: var(--mono); }
.clt { font-size: 10px; font-weight: 700; letter-spacing: .06em; }
.cldesc { font-size: 13px; color: var(--text); font-weight: 500; }
.cldet { font-size: 11px; color: var(--text2); }
.cl-A .clt { color: var(--success); } .cl-A { border-color: var(--success) !important; }
.cl-B .clt { color: var(--danger); } .cl-B { border-color: var(--danger) !important; }
.cl-R .clt { color: var(--warn); } .cl-R { border-color: var(--warn) !important; }
.cl-E .clt { color: var(--accent2); }
.cl-M .clt { color: var(--purple); } .cl-M { border-color: var(--purple) !important; }
.cl-U .clt { color: var(--accent); } .cl-U { border-color: var(--accent) !important; }

.empty { padding: 32px; text-align: center; color: var(--muted); font-size: 13px; }

/* MASIVA */
.masiva-step { background: var(--surface2); border: 1px solid var(--border); border-radius: 8px; padding: 14px; display: flex; flex-direction: column; gap: 10px; }
.masiva-step-title { font-size: 11px; font-weight: 700; color: var(--accent); letter-spacing: .06em; text-transform: uppercase; }
.match-count { font-size: 13px; font-weight: 600; color: var(--accent); padding: 4px 0; }
.preview-wrap { overflow: auto; max-height: 220px; border: 1px solid var(--border); border-radius: 6px; }
.preview-table { width: 100%; border-collapse: collapse; font-size: 11px; }
.preview-table th { background: var(--surface2); padding: 6px 10px; font-size: 10px; font-weight: 700; color: var(--text2); text-align: left; border-bottom: 1px solid var(--border); white-space: nowrap; position: sticky; top: 0; }
.preview-table td { padding: 5px 10px; border-bottom: 1px solid var(--border); white-space: nowrap; }
.preview-table tr.ch td { background: #f0fdf4; }
.new-val { color: var(--accent); font-weight: 700; font-family: var(--mono); font-size: 11px; }

/* UPLOAD */
.dropzone { border: 2px dashed var(--border2); border-radius: 8px; padding: 32px; text-align: center; cursor: pointer; transition: all .2s; color: var(--text2); }
.dropzone:hover, .dropzone.drag { border-color: var(--accent); color: var(--accent); background: var(--accent-light); }
.dz-icon { font-size: 28px; margin-bottom: 8px; }
.dz-title { font-size: 14px; font-weight: 600; margin-bottom: 4px; }
.dz-sub { font-size: 11px; color: var(--muted); }
.upload-result { background: var(--surface2); border: 1px solid var(--border); border-radius: 8px; padding: 12px 14px; margin-top: 10px; }
.ur-row { display: flex; justify-content: space-between; align-items: center; padding: 5px 0; border-bottom: 1px solid var(--border); }
.ur-row:last-child { border-bottom: none; }
.ur-label { font-size: 12px; color: var(--text2); }
.ur-val { font-family: var(--mono); font-size: 13px; font-weight: 700; color: var(--text); }

::-webkit-scrollbar { width: 5px; height: 5px; }
::-webkit-scrollbar-track { background: var(--surface2); }
::-webkit-scrollbar-thumb { background: var(--border2); border-radius: 3px; }
</style>
</head>
<body>

<header>
  <div class="logo">EFiS <span>/ Gestión de Estructura</span></div>
  <div class="tabs">
    <button class="tab active" onclick="showPage('personal',this)">Personal</button>
    <button class="tab" onclick="showPage('vacantes',this)">Vacantes</button>
    <button class="tab" onclick="showPage('servicios',this)">Por Servicio</button>
    <button class="tab" onclick="showPage('changelog',this)">Movimientos</button>
  </div>
</header>

<div class="stats-bar">
  <div class="stat-card"><div class="stat-label">Total Posiciones</div><div class="stat-value sv-blue" id="stTotal">—</div></div>
  <div class="stat-card"><div class="stat-label">Ocupadas</div><div class="stat-value sv-teal" id="stOcup">—</div></div>
  <div class="stat-card"><div class="stat-label">Vacantes</div><div class="stat-value sv-yellow" id="stVac">—</div></div>
  <div class="stat-card"><div class="stat-label">WC – Jerárquico</div><div class="stat-value sv-blue" id="stWC">—</div></div>
  <div class="stat-card"><div class="stat-label">BC – Petrolero</div><div class="stat-value sv-pur" id="stBC">—</div></div>
  <div class="stat-card"><div class="stat-label">Duplicados</div><div class="stat-value sv-red" id="stDup">0</div></div>
  <div class="stat-card"><div class="stat-label">Movimientos</div><div class="stat-value" id="stMov">0</div></div>
</div>

<!-- ===== PERSONAL ===== -->
<div class="page active" id="page-personal"><div class="main">
  <div class="section-header">
    <span class="panel-title">Estructura completa</span>
    <button class="btn btn-p" onclick="openModal('alta')">+ Alta</button>
    <button class="btn btn-pur" onclick="openModal('masiva')">⚡ Edición Masiva</button>
    <button class="btn btn-s" onclick="openModal('upload')">↑ Cargar Excel</button>
    <button class="btn btn-s" onclick="exportCSV()">↓ Exportar CSV</button>
  </div>
  <div class="filters">
    <input class="fi fi-search" id="srch" placeholder="Buscar nombre, DNI, posición, jefe..." oninput="renderPersonal()">
    <select class="fi fi-sel" id="fServ" onchange="renderPersonal()"><option value="">— Servicio —</option></select>
    <select class="fi fi-sel" id="fCeco" onchange="renderPersonal()"><option value="">— CECO —</option></select>
    <select class="fi fi-sm" id="fWCBC" onchange="renderPersonal()">
      <option value="">— WC/BC —</option>
      <option value="WC">WC – Jerárquico</option>
      <option value="BC">BC – Petrolero</option>
    </select>
    <select class="fi fi-sm" id="fSoc" onchange="renderPersonal()">
      <option value="">— Sociedad —</option>
      <option value="Energy Field Services">EFS</option>
      <option value="TECPETROL S.A.">TECPETROL</option>
    </select>
    <select class="fi fi-sel" id="fFlag" onchange="renderPersonal()"><option value="">— Cuadrilla —</option></select>
    <button class="fbadge" id="btnVac" onclick="toggleFilter('vac')">⚠ Vacantes</button>
    <button class="fbadge" id="btnDup" onclick="toggleFilter('dup')">⬥ Duplicados</button>
  </div>
  <div class="dup-legend" id="dupLegend" style="display:none">
    <span style="font-size:11px;font-weight:700;color:var(--text2)">Leyenda:</span>
    <div class="dl-item"><div class="dl-dot" style="background:var(--dup-pos);border:1px solid rgba(220,38,38,.3)"></div>Posición SAP repetida</div>
    <div class="dl-item"><div class="dl-dot" style="background:var(--dup-dni);border:1px solid rgba(217,119,6,.3)"></div>DNI repetido</div>
    <div class="dl-item"><div class="dl-dot" style="background:var(--dup-both);border:1px solid rgba(124,58,237,.3)"></div>Ambos duplicados</div>
  </div>
  <div class="tw"><table>
    <thead><tr>
      <th onclick="sortBy('POSICION')">Posición SAP ↕</th>
      <th onclick="sortBy('DESCRIPCION_PERSONA')">Persona ↕</th>
      <th onclick="sortBy('ID_META_4')">DNI ↕</th>
      <th onclick="sortBy('OBJETO_DE_IMPUTACION')">CECO ↕</th>
      <th onclick="sortBy('DESCRIPCION_POSICION')">Cargo ↕</th>
      <th onclick="sortBy('GERENCIA_JEFATURA')">Servicio ↕</th>
      <th onclick="sortBy('NOMBRE_JEFE')">Jefe ↕</th>
      <th onclick="sortBy('FLAG_LICENCIA')">Cuadrilla ↕</th>
      <th onclick="sortBy('WC_BC')">WC/BC ↕</th>
      <th onclick="sortBy('SOCIEDAD')">Soc. ↕</th>
      <th>Estado</th>
      <th>Acciones</th>
    </tr></thead>
    <tbody id="tbPersonal"></tbody>
  </table></div>
  <div class="pg">
    <span class="pi" id="pgInfo"></span>
    <button class="btn btn-s" id="btnPrev" onclick="changePage(-1)">← Anterior</button>
    <button class="btn btn-s" id="btnNext" onclick="changePage(1)">Siguiente →</button>
  </div>
</div></div>

<!-- ===== VACANTES ===== -->
<div class="page" id="page-vacantes"><div class="main">
  <div class="section-header">
    <span class="panel-title">Puestos Vacantes</span>
    <button class="btn btn-p" onclick="openModal('alta')">+ Cubrir puesto</button>
  </div>
  <div class="alert al-w" style="margin-bottom:12px">Posiciones sin persona asignada. Cubrí una con el botón "Cubrir" o registrando un Alta.</div>
  <div class="tw"><table>
    <thead><tr><th>Posición SAP</th><th>Descripción Posición (vacante)</th><th>CECO</th><th>Cuadrilla</th><th>WC/BC</th><th>Sociedad</th><th>Jefe</th><th>Acción</th></tr></thead>
    <tbody id="tbVacantes"></tbody>
  </table></div>
</div></div>

<!-- ===== SERVICIOS ===== -->
<div class="page" id="page-servicios"><div class="main">
  <div class="section-header">
    <span class="panel-title">Cuadrillas por FLAG_LICENCIA</span>
    <input class="fi" id="fFlag" placeholder="Buscar cuadrilla..." oninput="renderServicios()" style="min-width:220px;margin-left:auto">
    <select class="fi fi-sm" id="fFlagServ" onchange="renderServicios()"><option value="">— Servicio —</option></select>
  </div>
  <div id="flagSummary" style="display:flex;gap:10px;margin-bottom:12px;flex-wrap:wrap"></div>
  <div class="sg" id="sGrid"></div>
</div></div>

<!-- ===== CHANGELOG ===== -->
<div class="page" id="page-changelog"><div class="main">
  <div class="section-header">
    <span class="panel-title">Registro de Movimientos</span>
    <div style="display:flex;gap:6px;margin-left:auto">
      <select class="fi fi-sm" id="fTipoMov" onchange="renderChangelog()">
        <option value="">— Todos —</option>
        <option value="A">Alta</option><option value="B">Baja</option>
        <option value="R">Rotación</option><option value="E">Edición</option>
        <option value="M">Masiva</option><option value="U">Reversión</option>
      </select>
      <button class="btn btn-s" onclick="exportChangelogCSV()">↓ Exportar</button>
    </div>
  </div>
  <div class="alert al-i" style="margin-bottom:12px">Cada movimiento registrado debe impactarse en SAP para asegurar liquidaciones correctas.</div>
  <div id="clList"><div class="empty">No hay movimientos registrados aún.</div></div>
</div></div>

<!-- ===== MODAL: ALTA ===== -->
<div class="modal-bd" id="modal-alta"><div class="modal">
  <div class="mh">
    <div><div class="mt">Alta de persona</div><div class="mt-sub">Completá los datos de la nueva incorporación</div></div>
    <button class="mc" onclick="closeModal('alta')">✕</button>
  </div>
  <div class="mb">
    <div class="fr">
      <div class="fg"><label class="fl">Posición SAP</label><input class="finp" id="a_pos" placeholder="ej. 3360828"></div>
      <div class="fg"><label class="fl">DNI (ID_META_4)</label><input class="finp" id="a_dni" placeholder="ej. DU28636995"></div>
    </div>
    <div class="fg"><label class="fl">Nombre y Apellido</label><input class="finp" id="a_nom" placeholder="ej. García Juan Carlos"></div>
    <div class="fr">
      <div class="fg"><label class="fl">CECO</label><input class="finp" id="a_ceco" list="dlCeco" placeholder="ej. EFR-FN0920"></div>
      <div class="fg"><label class="fl">Servicio</label><input class="finp" id="a_serv" list="dlServ" placeholder="ej. O&M Services"></div>
    </div>
    <div class="fg"><label class="fl">Cargo / Descripción Posición</label><input class="finp" id="a_cargo" placeholder="ej. Maintenance Sr. Supervisor"></div>
    <div class="fr">
      <div class="fg"><label class="fl">Sociedad</label><select class="finp" id="a_soc"><option>Energy Field Services</option><option>TECPETROL S.A.</option></select></div>
      <div class="fg"><label class="fl">WC / BC</label><select class="finp" id="a_wcbc"><option value="WC">WC – Jerárquico</option><option value="BC">BC – Petrolero</option></select></div>
    </div>
    <div class="fr">
      <div class="fg"><label class="fl">Jefe directo</label><input class="finp" id="a_jefe" list="dlJefe" placeholder="Nombre del jefe"></div>
      <div class="fg"><label class="fl">FLAG / Categoría</label><input class="finp" id="a_flag" placeholder="ej. PRR Supervisores Mtto"></div>
    </div>
    <div class="fg"><label class="fl">Observaciones</label><input class="finp" id="a_obs" placeholder="Motivo del alta, contexto..."></div>
  </div>
  <div class="mf"><button class="btn btn-s" onclick="closeModal('alta')">Cancelar</button><button class="btn btn-p" onclick="saveAlta()">Guardar Alta</button></div>
</div></div>

<!-- ===== MODAL: EDICIÓN ===== -->
<div class="modal-bd" id="modal-edit"><div class="modal">
  <div class="mh"><div class="mt">Editar posición</div><button class="mc" onclick="closeModal('edit')">✕</button></div>
  <div class="mb" id="editBody"></div>
  <div class="mf"><button class="btn btn-s" onclick="closeModal('edit')">Cancelar</button><button class="btn btn-p" onclick="saveEdit()">Guardar cambios</button></div>
</div></div>

<!-- ===== MODAL: BAJA ===== -->
<div class="modal-bd" id="modal-baja"><div class="modal">
  <div class="mh">
    <div><div class="mt" style="color:var(--danger)">Registrar Baja</div><div class="mt-sub">La posición quedará vacante. Recordá impactarlo en SAP.</div></div>
    <button class="mc" onclick="closeModal('baja')">✕</button>
  </div>
  <div class="mb">
    <div class="fg"><label class="fl">Persona</label><input class="finp" id="b_per" readonly></div>
    <div class="fr">
      <div class="fg"><label class="fl">Posición SAP</label><input class="finp" id="b_pos" readonly></div>
      <div class="fg"><label class="fl">CECO al momento de la baja</label><input class="finp" id="b_ceco" readonly></div>
    </div>
    <div class="fg"><label class="fl">Motivo de la baja</label>
      <select class="finp" id="b_motivo">
        <option>Renuncia voluntaria</option><option>Despido / Desvinculación</option>
        <option>Jubilación</option><option>Vencimiento contrato</option>
        <option>Fallecimiento</option><option>Otro</option>
      </select>
    </div>
    <div class="fg"><label class="fl">Observaciones</label><input class="finp" id="b_obs" placeholder="Detalle adicional..."></div>
  </div>
  <div class="mf"><button class="btn btn-s" onclick="closeModal('baja')">Cancelar</button><button class="btn btn-d" onclick="confirmarBaja()">Confirmar Baja</button></div>
</div></div>

<!-- ===== MODAL: ROTACIÓN ===== -->
<div class="modal-bd" id="modal-rot"><div class="modal">
  <div class="mh">
    <div><div class="mt">Movimiento / Traslado</div><div class="mt-sub">Completá solo los campos que cambian</div></div>
    <button class="mc" onclick="closeModal('rot')">✕</button>
  </div>
  <div class="mb">
    <div class="fg"><label class="fl">Persona</label><input class="finp" id="r_per" readonly></div>
    <div class="section-divider">Posición SAP</div>
    <div class="fr">
      <div class="fg"><label class="fl">Actual</label><input class="finp" id="r_pos_from" readonly></div>
      <div class="fg"><label class="fl">Nueva</label><input class="finp" id="r_pos_to" placeholder="Dejar vacío si no cambia"></div>
    </div>
    <div class="section-divider">CECO</div>
    <div class="fr">
      <div class="fg"><label class="fl">Actual</label><input class="finp" id="r_ceco_from" readonly></div>
      <div class="fg"><label class="fl">Nuevo</label><input class="finp" id="r_ceco_to" list="dlCeco" placeholder="Dejar vacío si no cambia"></div>
    </div>
    <div class="section-divider">Servicio</div>
    <div class="fr">
      <div class="fg"><label class="fl">Actual</label><input class="finp" id="r_serv_from" readonly></div>
      <div class="fg"><label class="fl">Nuevo</label><input class="finp" id="r_serv_to" list="dlServ" placeholder="Dejar vacío si no cambia"></div>
    </div>
    <div class="section-divider">Jefe</div>
    <div class="fr">
      <div class="fg"><label class="fl">Actual</label><input class="finp" id="r_jefe_from" readonly></div>
      <div class="fg"><label class="fl">Nuevo</label><input class="finp" id="r_jefe_to" list="dlJefe" placeholder="Dejar vacío si no cambia"></div>
    </div>
    <div class="fg" style="margin-top:4px"><label class="fl">Motivo / Observaciones</label><input class="finp" id="r_obs" placeholder="Motivo del traslado o cambio..."></div>
  </div>
  <div class="mf"><button class="btn btn-s" onclick="closeModal('rot')">Cancelar</button><button class="btn btn-p" onclick="saveRot()">Confirmar Movimiento</button></div>
</div></div>

<!-- ===== MODAL: EDICIÓN MASIVA ===== -->
<div class="modal-bd" id="modal-masiva"><div class="modal modal-lg">
  <div class="mh">
    <div><div class="mt">Edición Masiva</div><div class="mt-sub">Aplicá un cambio a múltiples filas en un paso</div></div>
    <button class="mc" onclick="closeModal('masiva')">✕</button>
  </div>
  <div class="mb">
    <div class="masiva-step">
      <div class="masiva-step-title">① Filtro — ¿A qué filas aplicar?</div>
      <div class="fr">
        <div class="fg"><label class="fl">Filtrar por campo</label>
          <select class="finp" id="m_ff" onchange="onMasivaFilterFieldChange()">
            <option value="">— Todas las filas —</option>
            <option value="NOMBRE_JEFE">Jefe</option>
            <option value="GERENCIA_JEFATURA">Servicio</option>
            <option value="OBJETO_DE_IMPUTACION">CECO</option>
            <option value="WC_BC">WC/BC</option>
            <option value="SOCIEDAD">Sociedad</option>
            <option value="FLAG_LICENCIA">FLAG</option>
            <option value="DESCRIPCION_POSICION">Cargo</option>
          </select>
        </div>
        <div class="fg"><label class="fl">Valor a buscar</label>
          <input class="finp" id="m_fv" list="dlMF" placeholder="Valor del campo filtro" oninput="previewMasiva()">
          <datalist id="dlMF"></datalist>
        </div>
      </div>
    </div>
    <div class="masiva-step">
      <div class="masiva-step-title">② Cambio — ¿Qué campo reemplazar?</div>
      <div class="fr">
        <div class="fg"><label class="fl">Campo a modificar</label>
          <select class="finp" id="m_tf" onchange="onMasivaTargetFieldChange()">
            <option value="">— Elegir campo —</option>
            <option value="NOMBRE_JEFE">Jefe</option>
            <option value="GERENCIA_JEFATURA">Servicio</option>
            <option value="OBJETO_DE_IMPUTACION">CECO</option>
            <option value="WC_BC">WC/BC</option>
            <option value="SOCIEDAD">Sociedad</option>
            <option value="FLAG_LICENCIA">FLAG</option>
          </select>
        </div>
        <div class="fg"><label class="fl">Valor nuevo</label>
          <input class="finp" id="m_nv" list="dlMT" placeholder="Valor a aplicar" oninput="previewMasiva()">
          <datalist id="dlMT"></datalist>
        </div>
      </div>
    </div>
    <div id="m_info" class="match-count"></div>
    <div class="preview-wrap" id="m_preview"><div class="empty">Configurá el filtro y el campo destino para ver la previsualización.</div></div>
  </div>
  <div class="mf">
    <button class="btn btn-s" onclick="closeModal('masiva')">Cancelar</button>
    <button class="btn btn-pur" id="btnMasiva" onclick="aplicarMasiva()" disabled>⚡ Aplicar cambios</button>
  </div>
</div></div>

<!-- ===== MODAL: UPLOAD ===== -->
<div class="modal-bd" id="modal-upload"><div class="modal modal-lg">
  <div class="mh">
    <div><div class="mt">Cargar Excel de Estructura</div><div class="mt-sub">El sistema detectará filas nuevas y cambios en campos clave</div></div>
    <button class="mc" onclick="closeModal('upload')">✕</button>
  </div>
  <div class="mb">
    <div class="alert al-i">Las columnas requeridas son: POSICION, ID_META_4, DESCRIPCION_PERSONA, OBJETO_DE_IMPUTACION. El resto es opcional.</div>
    <div class="dropzone" id="dropzone"
      onclick="document.getElementById('fileInput').click()"
      ondragover="event.preventDefault();this.classList.add('drag')"
      ondragleave="this.classList.remove('drag')"
      ondrop="handleDrop(event)">
      <div class="dz-icon">📂</div>
      <div class="dz-title">Hacé clic o arrastrá el archivo XLSX aquí</div>
      <div class="dz-sub">Formatos soportados: .xlsx, .xls, .csv</div>
    </div>
    <input type="file" id="fileInput" accept=".xlsx,.xls,.csv" style="display:none" onchange="handleFileUpload(this.files[0])">
    <div id="uploadResult"></div>
    <div class="preview-wrap" id="uploadPreview" style="display:none;margin-top:8px"></div>
  </div>
  <div class="mf">
    <button class="btn btn-s" onclick="closeModal('upload')">Cancelar</button>
    <button class="btn btn-p" id="btnApplyUpload" onclick="applyUpload()" style="display:none">✓ Aplicar cambios</button>
  </div>
</div></div>

<datalist id="dlCeco"></datalist>
<datalist id="dlServ"></datalist>
<datalist id="dlJefe"></datalist>

<script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
<script>
// ===== DATA =====
const BASE = [{"POSICION":"3360828","DESCRIPCION_POSICION":"O&M Services Director","ID_META_4":"DU20916565","OBJETO_DE_IMPUTACION":"FPF-FN0940","DESCRIPCION_PERSONA":"Lusso Mauricio Ricardo","GERENCIA_JEFATURA":"O&M Services","NOMBRE_JEFE":"Mamani Carlos Walter","SOCIEDAD":"TECPETROL S.A.","FLAG_LICENCIA":"Sueldos TECPE","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3417016","DESCRIPCION_POSICION":"O&M Services Sr. Manager","ID_META_4":"DU29109359","OBJETO_DE_IMPUTACION":"FPF-FN0940","DESCRIPCION_PERSONA":"Fabro Facundo","GERENCIA_JEFATURA":"O&M Services","NOMBRE_JEFE":"Lusso Mauricio Ricardo","SOCIEDAD":"TECPETROL S.A.","FLAG_LICENCIA":"Sueldos TECPE","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3197992","DESCRIPCION_POSICION":"Maintenance Services Manager","ID_META_4":"DU28636995","OBJETO_DE_IMPUTACION":"FPF-FN0940","DESCRIPCION_PERSONA":"Batallan Pablo Alejandro","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Fabro Facundo","SOCIEDAD":"TECPETROL S.A.","FLAG_LICENCIA":"Sueldos TECPE","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3294913","DESCRIPCION_POSICION":"Operations Services Manager","ID_META_4":"DU28044115","OBJETO_DE_IMPUTACION":"FPF-FN0940","DESCRIPCION_PERSONA":"Lopez Rodrigo Gaston","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Fabro Facundo","SOCIEDAD":"TECPETROL S.A.","FLAG_LICENCIA":"Sueldos TECPE","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3364085","DESCRIPCION_POSICION":"O&M Optimization Process Analyst","ID_META_4":"DU40927304","OBJETO_DE_IMPUTACION":"FPF-FN0940","DESCRIPCION_PERSONA":"Gili Arianna","GERENCIA_JEFATURA":"O&M Services - Optimization Process","NOMBRE_JEFE":"Lusso Mauricio Ricardo","SOCIEDAD":"TECPETROL S.A.","FLAG_LICENCIA":"Sueldos TECPE","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392801","DESCRIPCION_POSICION":"Maintenance Services Coordinator","ID_META_4":"DU28063207","OBJETO_DE_IMPUTACION":"EFR-FN0920","DESCRIPCION_PERSONA":"Huarte Esteban","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Batallan Pablo Alejandro","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"PRR Facilitadores Pta/Prod","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392802","DESCRIPCION_POSICION":"Operations Services Coordinator","ID_META_4":"DU32090502","OBJETO_DE_IMPUTACION":"EFR-FN0920","DESCRIPCION_PERSONA":"Cordova Daniela Emiliana","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Batallan Pablo Alejandro","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"PRR Facilitadores Pta/Prod","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392803","DESCRIPCION_POSICION":"Maintenance Services Coordinator","ID_META_4":"DU34666188","OBJETO_DE_IMPUTACION":"EFR-FN0920","DESCRIPCION_PERSONA":"Altamiranda Leandro Damian","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Batallan Pablo Alejandro","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"PRR Facilitadores Pta/Prod","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392804","DESCRIPCION_POSICION":"Production Services Coordinator","ID_META_4":"DU24131475","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Macias Ceferino Oscar","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Lopez Rodrigo Gaston","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392805","DESCRIPCION_POSICION":"Plants Services Coordinator","ID_META_4":"DU32195174","OBJETO_DE_IMPUTACION":"EFR-FN0900","DESCRIPCION_PERSONA":"Bechara Lucas Antonio","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Lopez Rodrigo Gaston","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"PRR Facilitadores Mtto","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392806","DESCRIPCION_POSICION":"Operations Services Coordinator","ID_META_4":"DU30191811","OBJETO_DE_IMPUTACION":"EFR-FN0920","DESCRIPCION_PERSONA":"Casal Gustavo Daniel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Lopez Rodrigo Gaston","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"PRR Facilitadores Pta/Prod","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392807","DESCRIPCION_POSICION":"O&M Services Analyst","ID_META_4":"","OBJETO_DE_IMPUTACION":"EFR-FN0900","DESCRIPCION_PERSONA":"Baja posición facilitador ASAL","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Batallan Pablo Alejandro","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"PRR Facilitadores Mtto","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392808","DESCRIPCION_POSICION":"Technical Training Specialist","ID_META_4":"DU22168868","OBJETO_DE_IMPUTACION":"EFR-FN0920","DESCRIPCION_PERSONA":"Mondaca Ruben Jose","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Lopez Rodrigo Gaston","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"PRR Facilitadores Pta/Prod","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3406970","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU47368614","OBJETO_DE_IMPUTACION":"EFF-FP0921","DESCRIPCION_PERSONA":"Gonzalez Mendez Simon","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Mecánico FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3414076","DESCRIPCION_POSICION":"Maintenance Supervisor","ID_META_4":"DU36718136","OBJETO_DE_IMPUTACION":"EFR-FN0910","DESCRIPCION_PERSONA":"Montefinale Federico Miguel","GERENCIA_JEFATURA":"Maintenance TLM","NOMBRE_JEFE":"Segura Alejandro","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"PRR Supervisores Mtto","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392809","DESCRIPCION_POSICION":"O&M Planning Analyst","ID_META_4":"DU41254675","OBJETO_DE_IMPUTACION":"FPF-FN0940","DESCRIPCION_PERSONA":"Baza Coseani Luisina","GERENCIA_JEFATURA":"O&M Services - Optimization Process","NOMBRE_JEFE":"Gili Arianna","SOCIEDAD":"TECPETROL S.A.","FLAG_LICENCIA":"Sueldos TECPE","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392810","DESCRIPCION_POSICION":"Accounts Payable Analyst","ID_META_4":"DU38493274","OBJETO_DE_IMPUTACION":"FPF-FN0940","DESCRIPCION_PERSONA":"Apestegui Juan Pablo","GERENCIA_JEFATURA":"Adm. & Finance Neuquén","NOMBRE_JEFE":"Romano Mariano Bruno","SOCIEDAD":"TECPETROL S.A.","FLAG_LICENCIA":"Sueldos TECPE","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392811","DESCRIPCION_POSICION":"HRBP Analyst","ID_META_4":"DU39076574","OBJETO_DE_IMPUTACION":"EFR-FN0941","DESCRIPCION_PERSONA":"Barrera Anahi Malen","GERENCIA_JEFATURA":"Neuquén","NOMBRE_JEFE":"Corbalan Federico Martin","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Indirectos PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392812","DESCRIPCION_POSICION":"HRBP Sr. Analyst","ID_META_4":"DU36801186","OBJETO_DE_IMPUTACION":"EFR-FN0941","DESCRIPCION_PERSONA":"Tarifeño Ernesto Eduardo","GERENCIA_JEFATURA":"Neuquén","NOMBRE_JEFE":"Corbalan Federico Martin","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Indirectos PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"","DESCRIPCION_POSICION":"HRBP Sr. Analyst","ID_META_4":"DU38493136","OBJETO_DE_IMPUTACION":"EFR-FN0941","DESCRIPCION_PERSONA":"Jara Micaela","GERENCIA_JEFATURA":"Neuquén","NOMBRE_JEFE":"Corbalan Federico Martin","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Indirectos PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392813","DESCRIPCION_POSICION":"Labor Relations Expert","ID_META_4":"DU30264777","OBJETO_DE_IMPUTACION":"EFR-FN0941","DESCRIPCION_PERSONA":"Seguel Maria Fernanda","GERENCIA_JEFATURA":"Labor Relations & CORE","NOMBRE_JEFE":"Gaisch Alejandro Hector","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Indirectos PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392814","DESCRIPCION_POSICION":"Quality Analyst","ID_META_4":"DU36010010","OBJETO_DE_IMPUTACION":"EFR-FN0941","DESCRIPCION_PERSONA":"Campora Camila María","GERENCIA_JEFATURA":"Quality","NOMBRE_JEFE":"Seri Walter Omar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Indirectos PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392815","DESCRIPCION_POSICION":"General Services Supervisor","ID_META_4":"DU33067280","OBJETO_DE_IMPUTACION":"EFR-FN0941","DESCRIPCION_PERSONA":"Rizzo Sebastian","GERENCIA_JEFATURA":"Neuquén","NOMBRE_JEFE":"Zuluaga Gabriel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Indirectos PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392816","DESCRIPCION_POSICION":"HSE Sr. Supervisor","ID_META_4":"DU36669185","OBJETO_DE_IMPUTACION":"EFR-FN0945","DESCRIPCION_PERSONA":"Figueroa Franco Martin","GERENCIA_JEFATURA":"Health & Safety","NOMBRE_JEFE":"Chazarreta Jose Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"SAS PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392817","DESCRIPCION_POSICION":"HSE Sr. Supervisor","ID_META_4":"DU33926407","OBJETO_DE_IMPUTACION":"EFR-FN0945","DESCRIPCION_PERSONA":"Mora Federico","GERENCIA_JEFATURA":"Health & Safety","NOMBRE_JEFE":"Chazarreta Jose Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"SAS PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392818","DESCRIPCION_POSICION":"HSE Sr. Supervisor","ID_META_4":"DU28387841","OBJETO_DE_IMPUTACION":"EFR-FN0945","DESCRIPCION_PERSONA":"Sea Oscar Ariel","GERENCIA_JEFATURA":"Health & Safety","NOMBRE_JEFE":"Chazarreta Jose Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"SAS PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392819","DESCRIPCION_POSICION":"HSE Sr. Supervisor","ID_META_4":"DU33885206","OBJETO_DE_IMPUTACION":"EFR-FN0945","DESCRIPCION_PERSONA":"Palma Belen del Milagro","GERENCIA_JEFATURA":"Health & Safety","NOMBRE_JEFE":"Chazarreta Jose Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"SAS PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392820","DESCRIPCION_POSICION":"HSE Sr. Supervisor","ID_META_4":"DU23918152","OBJETO_DE_IMPUTACION":"EFR-FN0945","DESCRIPCION_PERSONA":"Huaiquiñir Juan Jose","GERENCIA_JEFATURA":"Health & Safety","NOMBRE_JEFE":"Lemes Mariana De Los Angeles","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"SAS PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392821","DESCRIPCION_POSICION":"HSE Sr. Supervisor","ID_META_4":"DU28254170","OBJETO_DE_IMPUTACION":"EFR-FN0945","DESCRIPCION_PERSONA":"Galdame Carlos David","GERENCIA_JEFATURA":"Health & Safety","NOMBRE_JEFE":"Lemes Mariana De Los Angeles","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"SAS PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3424838","DESCRIPCION_POSICION":"Operations Services Coordinator","ID_META_4":"DU24260286","OBJETO_DE_IMPUTACION":"EFR-2E0950","DESCRIPCION_PERSONA":"Mercado Mauricio Edgardo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Lopez Rodrigo Gaston","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"PRR Facilitadores LT2E","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3424839","DESCRIPCION_POSICION":"Operations Services Coordinator","ID_META_4":"DU27841592","OBJETO_DE_IMPUTACION":"EFR-2E0950","DESCRIPCION_PERSONA":"Fredes Ruben Oscar","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Lopez Rodrigo Gaston","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"PRR Facilitadores LT2E","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3395761","DESCRIPCION_POSICION":"Medical Assistant","ID_META_4":"DU33135662","OBJETO_DE_IMPUTACION":"EFR-FN0945","DESCRIPCION_PERSONA":"Feruglio Adrian Federico","GERENCIA_JEFATURA":"Health & Safety","NOMBRE_JEFE":"Martel Maximiliano Jose Tomas","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"SAS PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3395760","DESCRIPCION_POSICION":"Medical Assistant","ID_META_4":"DU26638146","OBJETO_DE_IMPUTACION":"EFR-FN0945","DESCRIPCION_PERSONA":"Schlosser Adolfo Julio","GERENCIA_JEFATURA":"Health & Safety","NOMBRE_JEFE":"Martel Maximiliano Jose Tomas","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"SAS PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392823","DESCRIPCION_POSICION":"Environmental Supervisor","ID_META_4":"DU33316128","OBJETO_DE_IMPUTACION":"EFR-FN0945","DESCRIPCION_PERSONA":"Leiva Ricardo Alejandro","GERENCIA_JEFATURA":"Environmental","NOMBRE_JEFE":"Carreño Venegas Cecilia","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"SAS PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3414072","DESCRIPCION_POSICION":"Environmental Sr. Supervisor","ID_META_4":"DU36344221","OBJETO_DE_IMPUTACION":"EFR-FN0945","DESCRIPCION_PERSONA":"Acuña Fernanda Natali","GERENCIA_JEFATURA":"Environmental","NOMBRE_JEFE":"Carreño Venegas Cecilia","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"SAS PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392824","DESCRIPCION_POSICION":"Health Auxiliar","ID_META_4":"DU29463906","OBJETO_DE_IMPUTACION":"EFR-FN0945","DESCRIPCION_PERSONA":"Prieto Beatriz Alejandra","GERENCIA_JEFATURA":"Health & Safety","NOMBRE_JEFE":"Martel Maximiliano Jose Tomas","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"SAS PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392825","DESCRIPCION_POSICION":"Operations Technology Maint. Engineer","ID_META_4":"DU33993061","OBJETO_DE_IMPUTACION":"EFR-FN0930","DESCRIPCION_PERSONA":"Crespillo Faur Adrian Alejandro","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Contreras Fernando Andres","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"OT PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392826","DESCRIPCION_POSICION":"Operations Technology Maint. Engineer","ID_META_4":"DU31806630","OBJETO_DE_IMPUTACION":"EFR-FN0930","DESCRIPCION_PERSONA":"Gonzalez Rodrigo Jeremias","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Contreras Fernando Andres","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"OT PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392827","DESCRIPCION_POSICION":"Operations Technology Maint. Engineer","ID_META_4":"DU37518969","OBJETO_DE_IMPUTACION":"EFR-FN0930","DESCRIPCION_PERSONA":"Forconi Enzo Ramiro","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Contreras Fernando Andres","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"OT PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392828","DESCRIPCION_POSICION":"Operations Technology Maint. Engineer","ID_META_4":"DU95871315","OBJETO_DE_IMPUTACION":"EFR-FN0930","DESCRIPCION_PERSONA":"Rodriguez Bordones Marcel Josue","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Contreras Fernando Andres","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"OT PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392829","DESCRIPCION_POSICION":"Operations Technology Maint. Engineer","ID_META_4":"DU37943788","OBJETO_DE_IMPUTACION":"EFR-FN0930","DESCRIPCION_PERSONA":"Lillo Mauricio","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Contreras Fernando Andres","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"OT PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392830","DESCRIPCION_POSICION":"Operations Technology Maint. Engineer","ID_META_4":"DU34127114","OBJETO_DE_IMPUTACION":"EFR-FN0930","DESCRIPCION_PERSONA":"Saenz Emiliano Jesus","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Contreras Fernando Andres","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"OT PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392831","DESCRIPCION_POSICION":"Operations Technology Maint. Engineer","ID_META_4":"DU96032842","OBJETO_DE_IMPUTACION":"EFR-FN0930","DESCRIPCION_PERSONA":"Suarez Jhoana Mariela","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Contreras Fernando Andres","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"OT PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392832","DESCRIPCION_POSICION":"Operations Technology Eng. Engineer","ID_META_4":"DU31316545","OBJETO_DE_IMPUTACION":"EFR-FN0930","DESCRIPCION_PERSONA":"Marasco Nestor Damian","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Schmidt Brian Eric","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"OT PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392833","DESCRIPCION_POSICION":"Operations Technology Eng. Engineer","ID_META_4":"DU39881413","OBJETO_DE_IMPUTACION":"EFR-FN0930","DESCRIPCION_PERSONA":"Viluron Santiago Ezequiel","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Schmidt Brian Eric","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"OT PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392846","DESCRIPCION_POSICION":"Integrity Supervisor","ID_META_4":"DU27872461","OBJETO_DE_IMPUTACION":"EFR-FN0931","DESCRIPCION_PERSONA":"Urrutia Segundo Manuel","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Diaz Luis Alberto","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Integridad PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392868","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU44103409","OBJETO_DE_IMPUTACION":"EFF-LB0901","DESCRIPCION_PERSONA":"Cheuquel Agustin Gabriel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392834","DESCRIPCION_POSICION":"Maintenance Sr. Supervisor","ID_META_4":"DU21381134","OBJETO_DE_IMPUTACION":"EFR-FN0910","DESCRIPCION_PERSONA":"Olave Omar Luis","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Sheffield Naiara Eileen","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"PRR Supervisores Mtto","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392835","DESCRIPCION_POSICION":"Maintenance Sr. Supervisor","ID_META_4":"DU39954968","OBJETO_DE_IMPUTACION":"EFR-FN0910","DESCRIPCION_PERSONA":"Poblete Torres Juan Esteban","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Sheffield Naiara Eileen","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"PRR Supervisores Mtto","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3401242","DESCRIPCION_POSICION":"Maintenance Sr. Supervisor","ID_META_4":"DU33476887","OBJETO_DE_IMPUTACION":"EFR-FN0910","DESCRIPCION_PERSONA":"Bohl Damian Alfredo","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Mazoue Juan Manuel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"PRR Supervisores Mtto","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3418339","DESCRIPCION_POSICION":"Operations Technology Eng. Engineer","ID_META_4":"","OBJETO_DE_IMPUTACION":"EFR-FN0930","DESCRIPCION_PERSONA":"Vacante OT LT2E","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Forte Federico","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"OT PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392836","DESCRIPCION_POSICION":"Plant Lead Supervisor","ID_META_4":"DU25173304","OBJETO_DE_IMPUTACION":"EFF-FP0911","DESCRIPCION_PERSONA":"Inostroza Juan Marcelo","GERENCIA_JEFATURA":"Operations - Plant","NOMBRE_JEFE":"Doria Pablo Cesar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Operadores SALA EPF","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392837","DESCRIPCION_POSICION":"Plant Lead Supervisor","ID_META_4":"DU24825640","OBJETO_DE_IMPUTACION":"EFF-FP0911","DESCRIPCION_PERSONA":"Pedrero Jorge Esteban","GERENCIA_JEFATURA":"Operations - Plant","NOMBRE_JEFE":"Doria Pablo Cesar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Operadores SALA EPF","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392838","DESCRIPCION_POSICION":"Plant Lead Supervisor","ID_META_4":"DU31341714","OBJETO_DE_IMPUTACION":"EFF-FP0911","DESCRIPCION_PERSONA":"Aguilera Martin Fabian","GERENCIA_JEFATURA":"Operations - Plant","NOMBRE_JEFE":"Doria Pablo Cesar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Operadores SALA EPF","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392839","DESCRIPCION_POSICION":"Plant Lead Supervisor","ID_META_4":"DU24817522","OBJETO_DE_IMPUTACION":"EFF-FP0911","DESCRIPCION_PERSONA":"Aquin Jorge Alfredo","GERENCIA_JEFATURA":"Operations - Plant","NOMBRE_JEFE":"Doria Pablo Cesar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Operadores SALA EPF","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3395767","DESCRIPCION_POSICION":"Plant Sr. Supervisor","ID_META_4":"DU27994695","OBJETO_DE_IMPUTACION":"EFR-FN0960","DESCRIPCION_PERSONA":"Acuña Israel Maximiliano","GERENCIA_JEFATURA":"Operations - Plant","NOMBRE_JEFE":"Alcantu Bargna Marcelo Luis","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"PRR Supervisores Producción","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3395519","DESCRIPCION_POSICION":"Production Supervisor","ID_META_4":"DU20334479","OBJETO_DE_IMPUTACION":"EFR-FN0960","DESCRIPCION_PERSONA":"Orrego Omar Nelson","GERENCIA_JEFATURA":"Operations - Field - Production LT2E","NOMBRE_JEFE":"Baissac Roberto Enrique","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"PRR Supervisores Producción","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3395768","DESCRIPCION_POSICION":"Production Supervisor","ID_META_4":"DU25113792","OBJETO_DE_IMPUTACION":"EFR-FN0960","DESCRIPCION_PERSONA":"Rivera Jorge David","GERENCIA_JEFATURA":"Operations - Field - Production LT2E","NOMBRE_JEFE":"Baissac Roberto Enrique","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"PRR Supervisores Producción","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392840","DESCRIPCION_POSICION":"Integrity Lead Engineer","ID_META_4":"DU95753737","OBJETO_DE_IMPUTACION":"EFR-FN0931","DESCRIPCION_PERSONA":"Pedraza Romero Ingrith Cristina","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Diaz Luis Alberto","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Integridad PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392841","DESCRIPCION_POSICION":"Maintenance Planning Analyst","ID_META_4":"DU32951591","OBJETO_DE_IMPUTACION":"EFR-FN0932","DESCRIPCION_PERSONA":"Zapata Gustavo Ceferino","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Gulayin Mariana Laura","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Programador PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392842","DESCRIPCION_POSICION":"Maintenance Planning Analyst","ID_META_4":"DU30519172","OBJETO_DE_IMPUTACION":"EFR-FN0932","DESCRIPCION_PERSONA":"Orozco Luciano Nicolas","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Cañaveras Adrian Marcelo","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Programador PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3418340","DESCRIPCION_POSICION":"Operations Technology Eng. Engineer","ID_META_4":"","OBJETO_DE_IMPUTACION":"EFR-FN0930","DESCRIPCION_PERSONA":"Vacante OT LT2E","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Forte Federico","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"OT PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3408113","DESCRIPCION_POSICION":"Maintenance Planning Analyst","ID_META_4":"DU32246164","OBJETO_DE_IMPUTACION":"EFR-FN0932","DESCRIPCION_PERSONA":"Corti Ortola Cristian Dario","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Cañaveras Adrian Marcelo","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Programador PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392844","DESCRIPCION_POSICION":"Integrity Lead Supervisor","ID_META_4":"DU22104238","OBJETO_DE_IMPUTACION":"EFR-FN0931","DESCRIPCION_PERSONA":"Garcia Oscar Ariel","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Diaz Luis Alberto","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Integridad PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392845","DESCRIPCION_POSICION":"Maintenance Sr. Supervisor","ID_META_4":"DU35834385","OBJETO_DE_IMPUTACION":"EFR-FN0910","DESCRIPCION_PERSONA":"Sieben Nicolas","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Kraemer Nicolás","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"PRR Supervisores Mtto","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392960","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU39129973","OBJETO_DE_IMPUTACION":"EFF-FP0907","DESCRIPCION_PERSONA":"Canales Vanina Daniela","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. Planta Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3414070","DESCRIPCION_POSICION":"HSE Lead Supervisor","ID_META_4":"DU36998204","OBJETO_DE_IMPUTACION":"EFF-FN1000","DESCRIPCION_PERSONA":"Ocaranza Jonathan","GERENCIA_JEFATURA":"Health & Safety TLM","NOMBRE_JEFE":"Martel Maximiliano Jose Tomas","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"PJ TLM","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3414075","DESCRIPCION_POSICION":"Integrity Engineering Engineer","ID_META_4":"DU38092352","OBJETO_DE_IMPUTACION":"EFF-FN1000","DESCRIPCION_PERSONA":"Chalop Marcos","GERENCIA_JEFATURA":"Maintenance TLM","NOMBRE_JEFE":"Segura Alejandro","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"PJ TLM","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392843","DESCRIPCION_POSICION":"O&M Control lead analyst","ID_META_4":"DU26783746","OBJETO_DE_IMPUTACION":"EFR-FN0932","DESCRIPCION_PERSONA":"Muccela Jose Daniel","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Cañaveras Adrian Marcelo","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Programador PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3418975","DESCRIPCION_POSICION":"Ingresante sin experiencia","ID_META_4":"","OBJETO_DE_IMPUTACION":"EFF-FP0944","DESCRIPCION_PERSONA":"VACANTE RELEVO VACAS MECÁNICOS","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mecánicos FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392822","DESCRIPCION_POSICION":"HSE Sr. Supervisor","ID_META_4":"DU35899723","OBJETO_DE_IMPUTACION":"EFR-FN0945","DESCRIPCION_PERSONA":"Wilton Smith","GERENCIA_JEFATURA":"Health & Safety","NOMBRE_JEFE":"Vicencio Cecilia Stefania","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"SAS PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3414077","DESCRIPCION_POSICION":"TLM Services Coordinator","ID_META_4":"DU41437832","OBJETO_DE_IMPUTACION":"EFF-FN1000","DESCRIPCION_PERSONA":"Saffe Julian Agustín","GERENCIA_JEFATURA":"O&M Services - TLM","NOMBRE_JEFE":"Batallan Pablo Alejandro","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"PJ TLM","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3424476","DESCRIPCION_POSICION":"Facilities Operations Lead Supervisor","ID_META_4":"DU30824024","OBJETO_DE_IMPUTACION":"EFF-FN2000","DESCRIPCION_PERSONA":"Orellana Omar Ismael","GERENCIA_JEFATURA":"Otras especialidades","NOMBRE_JEFE":"Carabajal Marcelo","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Otras especialidades","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3424477","DESCRIPCION_POSICION":"Chemical Treatment Lead Supervisor","ID_META_4":"DU29554367","OBJETO_DE_IMPUTACION":"EFF-FN2000","DESCRIPCION_PERSONA":"Rodriguez Lucas Matias","GERENCIA_JEFATURA":"Otras especialidades","NOMBRE_JEFE":"Carreras Natania","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Otras especialidades","WC_BC":"WC","ENCUADRE":""},{"POSICION":"34192161","DESCRIPCION_POSICION":"General Services Supervisor","ID_META_4":"DU21389528","OBJETO_DE_IMPUTACION":"EFF-FN2000","DESCRIPCION_PERSONA":"Bartusch Fabian","GERENCIA_JEFATURA":"Otras especialidades","NOMBRE_JEFE":"Zuluaga Gabriel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Otras especialidades","WC_BC":"WC","ENCUADRE":""},{"POSICION":"34192159","DESCRIPCION_POSICION":"General Services Supervisor","ID_META_4":"","OBJETO_DE_IMPUTACION":"EFF-FN2000","DESCRIPCION_PERSONA":"Vacante Sup SERGE","GERENCIA_JEFATURA":"Otras especialidades","NOMBRE_JEFE":"Zuluaga Gabriel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Otras especialidades","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3429151","DESCRIPCION_POSICION":"Well Services Supervisor","ID_META_4":"DU32352316","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Fiore Marco Cesar","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Buzaglo Sebastian","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3429150","DESCRIPCION_POSICION":"Well Services Supervisor","ID_META_4":"DU21750188","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Lozano Jorge Alberto","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Buzaglo Sebastian","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392847","DESCRIPCION_POSICION":"Operador Especializado Semi Jr. Plantas","ID_META_4":"DU31020868","OBJETO_DE_IMPUTACION":"EFF-LB0908","DESCRIPCION_PERSONA":"Alcaraz Gonzalo Ruben","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392848","DESCRIPCION_POSICION":"Operador Principal","ID_META_4":"DU27046756","OBJETO_DE_IMPUTACION":"EFF-LB0908","DESCRIPCION_PERSONA":"Nimbro Andres Alejandro","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392849","DESCRIPCION_POSICION":"Operador Principal","ID_META_4":"DU26149215","OBJETO_DE_IMPUTACION":"EFF-LB0908","DESCRIPCION_PERSONA":"Ijurco Jose Luis","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392850","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU31314191","OBJETO_DE_IMPUTACION":"EFF-LB0908","DESCRIPCION_PERSONA":"Fuentes Osvaldo Nazareno","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392851","DESCRIPCION_POSICION":"Ingresante de Plantas","ID_META_4":"DU42910545","OBJETO_DE_IMPUTACION":"EFF-LB0908","DESCRIPCION_PERSONA":"Sepulveda Miño Matias Ariel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392852","DESCRIPCION_POSICION":"Ingresante de Plantas","ID_META_4":"DU42518590","OBJETO_DE_IMPUTACION":"EFF-LB0908","DESCRIPCION_PERSONA":"Abarzua Ruiu Jose Ignacio","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392853","DESCRIPCION_POSICION":"Operador Especializado Semi Jr. Plantas","ID_META_4":"DU26132258","OBJETO_DE_IMPUTACION":"EFF-LB0908","DESCRIPCION_PERSONA":"Tapia Dario Andres","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392854","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU24659935","OBJETO_DE_IMPUTACION":"EFF-LB0908","DESCRIPCION_PERSONA":"Insulza Sergio Ramon","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392855","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU33285275","OBJETO_DE_IMPUTACION":"EFF-LB0908","DESCRIPCION_PERSONA":"Sepulveda Gustavo Andres","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392856","DESCRIPCION_POSICION":"Operador Especializado Semi Jr. Plantas","ID_META_4":"DU31173446","OBJETO_DE_IMPUTACION":"EFF-LB0908","DESCRIPCION_PERSONA":"Navarrete Miguel Andres","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392857","DESCRIPCION_POSICION":"Ingresante de Plantas","ID_META_4":"DU35492858","OBJETO_DE_IMPUTACION":"EFF-LB0908","DESCRIPCION_PERSONA":"Fuentes Guillermo Ivan","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392858","DESCRIPCION_POSICION":"Ingresante de Plantas","ID_META_4":"DU95988960","OBJETO_DE_IMPUTACION":"EFF-LB0908","DESCRIPCION_PERSONA":"Medina Chourio Luis Guillermo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392859","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU16197017","OBJETO_DE_IMPUTACION":"EFF-LB0908","DESCRIPCION_PERSONA":"Valdez Mario Sergio","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392860","DESCRIPCION_POSICION":"Ingresante de Plantas","ID_META_4":"DU43530857","OBJETO_DE_IMPUTACION":"EFF-LB0904","DESCRIPCION_PERSONA":"Espinoza Jose Luis","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Tareas Generales Prod LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392861","DESCRIPCION_POSICION":"Ingresante de Plantas","ID_META_4":"DU36840081","OBJETO_DE_IMPUTACION":"EFF-LB0904","DESCRIPCION_PERSONA":"Rebolledo Brian Nahuel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Tareas Generales Prod LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392862","DESCRIPCION_POSICION":"Ayudante de Plantas","ID_META_4":"DU24659848","OBJETO_DE_IMPUTACION":"EFR-FN0929","DESCRIPCION_PERSONA":"Gomez Carlos Oscar","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"T. Grales Serge PRR","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392863","DESCRIPCION_POSICION":"Administrativo de Almacén","ID_META_4":"DU30584916","OBJETO_DE_IMPUTACION":"EFF-FP0942","DESCRIPCION_PERSONA":"Bilbao Raul Alberto","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"NUEVO FACILITADOR","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Aux. Almacén FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392864","DESCRIPCION_POSICION":"Ayudante de Almacén","ID_META_4":"DU36514053","OBJETO_DE_IMPUTACION":"EFF-FP0942","DESCRIPCION_PERSONA":"Galera Carla Debora","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"NUEVO FACILITADOR","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Aux. Almacén FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392865","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU27238140","OBJETO_DE_IMPUTACION":"EFF-LB0901","DESCRIPCION_PERSONA":"Solorza Cristian Alejandro","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392866","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU29027641","OBJETO_DE_IMPUTACION":"EFF-LB0901","DESCRIPCION_PERSONA":"Jara Jonathan Jose Ariel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392867","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU34220747","OBJETO_DE_IMPUTACION":"EFF-LB0901","DESCRIPCION_PERSONA":"Hernandez Denis Alfredo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3427236","DESCRIPCION_POSICION":"HSE Sr. Supervisor","ID_META_4":"DU31923558","OBJETO_DE_IMPUTACION":"EFR-FN0945","DESCRIPCION_PERSONA":"Kissner Nelson  Daniel","GERENCIA_JEFATURA":"Health & Safety","NOMBRE_JEFE":"Vicencio Cecilia Stefania","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"SAS PRR","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392869","DESCRIPCION_POSICION":"Recorredor","ID_META_4":"DU32570313","OBJETO_DE_IMPUTACION":"EFF-LB0901","DESCRIPCION_PERSONA":"Benegas Silvio Sebastian","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392870","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU38495228","OBJETO_DE_IMPUTACION":"EFF-LB0901","DESCRIPCION_PERSONA":"Godoy Juan Manuel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392871","DESCRIPCION_POSICION":"Recorredor Semi Jr.","ID_META_4":"DU41010522","OBJETO_DE_IMPUTACION":"EFF-LB0901","DESCRIPCION_PERSONA":"Marin Juan Agustin","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392872","DESCRIPCION_POSICION":"Recorredor Semi Jr.","ID_META_4":"DU37176013","OBJETO_DE_IMPUTACION":"EFF-LB0901","DESCRIPCION_PERSONA":"Moreno Maira Ayelen","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392873","DESCRIPCION_POSICION":"Recorredor","ID_META_4":"DU37946313","OBJETO_DE_IMPUTACION":"EFF-LB0901","DESCRIPCION_PERSONA":"Cayhueque Claudio Alejandro","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392874","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU32746948","OBJETO_DE_IMPUTACION":"EFF-LB0901","DESCRIPCION_PERSONA":"Reyes Jose Angel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392875","DESCRIPCION_POSICION":"Recorredor Semi Jr.","ID_META_4":"DU92945733","OBJETO_DE_IMPUTACION":"EFF-LB0901","DESCRIPCION_PERSONA":"Castro Cifuentes Roberto Andres","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392876","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU36712459","OBJETO_DE_IMPUTACION":"EFF-LB0923","DESCRIPCION_PERSONA":"Olmos Matias Emanuel","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Instrumentos LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392877","DESCRIPCION_POSICION":"Operador Principal de Cuadrilla","ID_META_4":"DU32292825","OBJETO_DE_IMPUTACION":"EFF-LB0923","DESCRIPCION_PERSONA":"Meza Daniel Alejandro","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Instrumentos LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392878","DESCRIPCION_POSICION":"Operador Principal de Cuadrilla","ID_META_4":"DU28413149","OBJETO_DE_IMPUTACION":"EFF-LB0922","DESCRIPCION_PERSONA":"Vazquez Diego Augusto","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Eléctrico LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392879","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU31099482","OBJETO_DE_IMPUTACION":"EFF-LB0922","DESCRIPCION_PERSONA":"Lavarini San Roman Cristhian Andres","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Eléctrico LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392880","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU41590041","OBJETO_DE_IMPUTACION":"EFF-LB0921","DESCRIPCION_PERSONA":"Diaz Nicolas Nahuel","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Mecánico LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392881","DESCRIPCION_POSICION":"Operador Principal de Cuadrilla","ID_META_4":"DU23346669","OBJETO_DE_IMPUTACION":"EFF-LB0921","DESCRIPCION_PERSONA":"Mulbayer Nestor Omar","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Mecánico LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392882","DESCRIPCION_POSICION":"Ayudante de Oficios","ID_META_4":"DU46330132","OBJETO_DE_IMPUTACION":"EFF-LB0921","DESCRIPCION_PERSONA":"Muñoz Luciano Franco Sebastian","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Mecánico LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392883","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU37101594","OBJETO_DE_IMPUTACION":"EFF-LB0925","DESCRIPCION_PERSONA":"Arancena Leandro Alfredo","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Soldadura LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392884","DESCRIPCION_POSICION":"Oficial Sr. de Oficios","ID_META_4":"DU21626829","OBJETO_DE_IMPUTACION":"EFF-LB0925","DESCRIPCION_PERSONA":"Cancino Carlos Ruben","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Soldadura LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392885","DESCRIPCION_POSICION":"Operador Principal de Cuadrilla","ID_META_4":"DU25042689","OBJETO_DE_IMPUTACION":"EFF-LB0925","DESCRIPCION_PERSONA":"Leguizamon Eusebio","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Soldadura LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393252","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU24392753","OBJETO_DE_IMPUTACION":"EFF-FP0925","DESCRIPCION_PERSONA":"De la Fuente Daniel Antonio","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Soldadura FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392886","DESCRIPCION_POSICION":"Operador Principal","ID_META_4":"DU27739939","OBJETO_DE_IMPUTACION":"EFF-AS0908","DESCRIPCION_PERSONA":"Garayalde Victor Ariel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392887","DESCRIPCION_POSICION":"Operador Principal","ID_META_4":"DU37758896","OBJETO_DE_IMPUTACION":"EFF-AS0908","DESCRIPCION_PERSONA":"Petretto Angel Guillermo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392888","DESCRIPCION_POSICION":"Operador Principal","ID_META_4":"DU33941810","OBJETO_DE_IMPUTACION":"EFF-AS0908","DESCRIPCION_PERSONA":"Pichel Javier Alejandro","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392889","DESCRIPCION_POSICION":"Operador Principal","ID_META_4":"DU29428368","OBJETO_DE_IMPUTACION":"EFF-AS0908","DESCRIPCION_PERSONA":"Sanchez Raul Dario","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392890","DESCRIPCION_POSICION":"Operador Especializado Semi Jr. Plantas","ID_META_4":"DU33302240","OBJETO_DE_IMPUTACION":"EFF-AS0908","DESCRIPCION_PERSONA":"Caceres Hernan Rodrigo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392891","DESCRIPCION_POSICION":"Operador Especializado Semi Jr. Plantas","ID_META_4":"DU17434162","OBJETO_DE_IMPUTACION":"EFF-AS0908","DESCRIPCION_PERSONA":"Hechenleitner Carlos Walter","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392892","DESCRIPCION_POSICION":"Operador Especializado Semi Jr. Plantas","ID_META_4":"DU37758974","OBJETO_DE_IMPUTACION":"EFF-AS0908","DESCRIPCION_PERSONA":"Pichel Daniela Andrea","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392893","DESCRIPCION_POSICION":"Operador Especializado Semi Jr. Plantas","ID_META_4":"DU39866462","OBJETO_DE_IMPUTACION":"EFF-AS0908","DESCRIPCION_PERSONA":"Velez Leandro Gabriel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392894","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU40111059","OBJETO_DE_IMPUTACION":"EFF-AS0901","DESCRIPCION_PERSONA":"Romero Rodrigo Ariel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392895","DESCRIPCION_POSICION":"Oficial Sr. de Oficios","ID_META_4":"DU20502072","OBJETO_DE_IMPUTACION":"EFF-AS0904","DESCRIPCION_PERSONA":"Cardozo Marcos Dante","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Tareas Generales Prod SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392896","DESCRIPCION_POSICION":"Ayudante Jr. de Plantas","ID_META_4":"","OBJETO_DE_IMPUTACION":"EFF-AS0904","DESCRIPCION_PERSONA":"Vacante Tgrales ASAL (baja posición)","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Tareas Generales Prod SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392897","DESCRIPCION_POSICION":"Ayudante de Plantas","ID_META_4":"DU39869621","OBJETO_DE_IMPUTACION":"EFF-AS0904","DESCRIPCION_PERSONA":"Paris Ruiz Braian","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Tareas Generales Prod SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392899","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU30496337","OBJETO_DE_IMPUTACION":"EFF-AS0901","DESCRIPCION_PERSONA":"Campo Mauricio Gonzalo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392900","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU30384995","OBJETO_DE_IMPUTACION":"EFF-AS0901","DESCRIPCION_PERSONA":"Giner Jose Luis","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392901","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU28254164","OBJETO_DE_IMPUTACION":"EFF-AS0901","DESCRIPCION_PERSONA":"Mardones Santiago Oscar","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392902","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU24026927","OBJETO_DE_IMPUTACION":"EFF-AS0901","DESCRIPCION_PERSONA":"Olate Nestor Fabian","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392903","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU33485558","OBJETO_DE_IMPUTACION":"EFF-AS0901","DESCRIPCION_PERSONA":"Pereyra Jonatan Denis","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392904","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU30724331","OBJETO_DE_IMPUTACION":"EFF-AS0901","DESCRIPCION_PERSONA":"Riveira Jose Alfredo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392905","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU27647925","OBJETO_DE_IMPUTACION":"EFF-AS0901","DESCRIPCION_PERSONA":"Vazquez Diego Gonzalo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392906","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU27773643","OBJETO_DE_IMPUTACION":"EFF-AS0901","DESCRIPCION_PERSONA":"Sepulveda Cristian Enzo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392907","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU21985000","OBJETO_DE_IMPUTACION":"EFF-AS0901","DESCRIPCION_PERSONA":"Acevedo Jose Luis","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392908","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU30496418","OBJETO_DE_IMPUTACION":"EFF-AS0901","DESCRIPCION_PERSONA":"Garavaglia German Gabriel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392909","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU30496473","OBJETO_DE_IMPUTACION":"EFF-AS0901","DESCRIPCION_PERSONA":"Jara Pablo Andres","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392910","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU22855885","OBJETO_DE_IMPUTACION":"EFF-AS0901","DESCRIPCION_PERSONA":"Romero Walter Dario","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392911","DESCRIPCION_POSICION":"Medio Oficial Recorredor","ID_META_4":"DU27614355","OBJETO_DE_IMPUTACION":"EFF-AS0901","DESCRIPCION_PERSONA":"Pograniczny Mauricio Fabian","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392912","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU25259053","OBJETO_DE_IMPUTACION":"EFF-AS0901","DESCRIPCION_PERSONA":"Marianetti Mauricio Daniel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392913","DESCRIPCION_POSICION":"Recorredor Semi Jr.","ID_META_4":"DU37598999","OBJETO_DE_IMPUTACION":"EFF-AS0901","DESCRIPCION_PERSONA":"Rebolledo Maximiliano Carlos","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392914","DESCRIPCION_POSICION":"Recorredor Semi Jr.","ID_META_4":"","OBJETO_DE_IMPUTACION":"EFF-AS0901","DESCRIPCION_PERSONA":"VACANTE (baja posición)","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3428279","DESCRIPCION_POSICION":"Recorredor Semi Jr.","ID_META_4":"DU39869649","OBJETO_DE_IMPUTACION":"EFF-AS0901","DESCRIPCION_PERSONA":"Pograniczny Omar Denis","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392915","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU43892263","OBJETO_DE_IMPUTACION":"EFF-AS0923","DESCRIPCION_PERSONA":"Avalo Enzo Gustavo Martin","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Instrumentos SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392916","DESCRIPCION_POSICION":"Operador Principal de Cuadrilla","ID_META_4":"DU22012489","OBJETO_DE_IMPUTACION":"EFF-AS0923","DESCRIPCION_PERSONA":"Zuñiga Anibal","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Instrumentos SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392917","DESCRIPCION_POSICION":"Operador Principal de Cuadrilla","ID_META_4":"DU33485529","OBJETO_DE_IMPUTACION":"EFF-AS0922","DESCRIPCION_PERSONA":"Balastegui Jorge Luis","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Eléctrico SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392918","DESCRIPCION_POSICION":"Operador Principal de Cuadrilla","ID_META_4":"DU23883553","OBJETO_DE_IMPUTACION":"EFF-AS0922","DESCRIPCION_PERSONA":"Velez Jose Esteban","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Eléctrico SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392919","DESCRIPCION_POSICION":"Operador Principal de Cuadrilla","ID_META_4":"DU33331242","OBJETO_DE_IMPUTACION":"EFF-AS0921","DESCRIPCION_PERSONA":"Meza Dante Luciano","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Mecánico SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392920","DESCRIPCION_POSICION":"Operador Principal de Cuadrilla","ID_META_4":"DU21638891","OBJETO_DE_IMPUTACION":"EFF-AS0921","DESCRIPCION_PERSONA":"Rios Victor Armando","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Mecánico SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392921","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU21916259","OBJETO_DE_IMPUTACION":"EFF-AS0922","DESCRIPCION_PERSONA":"Arriagada Walter David","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Eléctrico SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392922","DESCRIPCION_POSICION":"Operador Principal de Cuadrilla","ID_META_4":"DU26082374","OBJETO_DE_IMPUTACION":"EFF-AS0925","DESCRIPCION_PERSONA":"Jahan Enrique Gonzalo","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Soldadura SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392923","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU26881097","OBJETO_DE_IMPUTACION":"EFF-AS0925","DESCRIPCION_PERSONA":"Olguin Nelson Antonio","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Soldadura SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392924","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU31600510","OBJETO_DE_IMPUTACION":"EFF-AS0925","DESCRIPCION_PERSONA":"Diaz Antonio","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Soldadura SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392925","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU38147510","OBJETO_DE_IMPUTACION":"EFF-FP0906","DESCRIPCION_PERSONA":"Montecino Miguel Angel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. EPF FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392926","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU35178521","OBJETO_DE_IMPUTACION":"EFF-FP0906","DESCRIPCION_PERSONA":"Lara Oscar Alexis","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. EPF FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392927","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU44604989","OBJETO_DE_IMPUTACION":"EFF-FP0906","DESCRIPCION_PERSONA":"Castillo Marion Itati","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. EPF FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392941","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU22236756","OBJETO_DE_IMPUTACION":"EFF-FP0905","DESCRIPCION_PERSONA":"Huenchullan Jose Enrique","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. LTS FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392929","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU44122295","OBJETO_DE_IMPUTACION":"EFF-FP0906","DESCRIPCION_PERSONA":"Pereyra Gianluca","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. EPF FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392930","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU35313504","OBJETO_DE_IMPUTACION":"EFF-FP0906","DESCRIPCION_PERSONA":"Perea Maximiliano Exequiel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. EPF FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392935","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU28624132","OBJETO_DE_IMPUTACION":"EFF-FP0905","DESCRIPCION_PERSONA":"Cordoba Diego Gerardo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. LTS FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392932","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU96013867","OBJETO_DE_IMPUTACION":"EFF-FP0906","DESCRIPCION_PERSONA":"Ventura Montoya Fernando Jose","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. EPF FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392933","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU37856483","OBJETO_DE_IMPUTACION":"EFF-FP0906","DESCRIPCION_PERSONA":"Contreras Nahir Kalis","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. EPF FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392934","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU46068665","OBJETO_DE_IMPUTACION":"EFF-FP0905","DESCRIPCION_PERSONA":"Puel Luciano Nazaret","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. LTS FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392958","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU45258911","OBJETO_DE_IMPUTACION":"EFF-FP0908","DESCRIPCION_PERSONA":"Almonacid Santiago Rodrigo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392936","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU40067099","OBJETO_DE_IMPUTACION":"EFF-FP0905","DESCRIPCION_PERSONA":"Querci Lucas Hernan","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. LTS FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392937","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU40293570","OBJETO_DE_IMPUTACION":"EFF-FP0905","DESCRIPCION_PERSONA":"Paz Heredia Martin Nicolas","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. LTS FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392938","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU20436984","OBJETO_DE_IMPUTACION":"EFF-FP0905","DESCRIPCION_PERSONA":"Estelrrig Miguel Horacio","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. LTS FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392939","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU25308875","OBJETO_DE_IMPUTACION":"EFF-FP0905","DESCRIPCION_PERSONA":"Querci Norman Gabriel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. LTS FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392940","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU31760927","OBJETO_DE_IMPUTACION":"EFF-FP0905","DESCRIPCION_PERSONA":"Velasquez Rodrigo Martin","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. LTS FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392928","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"","OBJETO_DE_IMPUTACION":"EFF-FP0906","DESCRIPCION_PERSONA":"VACANTE  relevo LTS","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. EPF FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392942","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU31939885","OBJETO_DE_IMPUTACION":"EFF-FP0905","DESCRIPCION_PERSONA":"Filippi Victor Adrian","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. LTS FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392943","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU32119820","OBJETO_DE_IMPUTACION":"EFF-FP0905","DESCRIPCION_PERSONA":"Figueroa Pablo Emanuel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. LTS FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392944","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU46257883","OBJETO_DE_IMPUTACION":"EFF-FP0905","DESCRIPCION_PERSONA":"Romero Tobias Juan Cruz","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. LTS FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392945","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU43703442","OBJETO_DE_IMPUTACION":"EFF-FP0908","DESCRIPCION_PERSONA":"Sanchez Millarin Claudio","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392946","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU39544442","OBJETO_DE_IMPUTACION":"EFF-FP0908","DESCRIPCION_PERSONA":"Rivolta Magali Soledad","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392947","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU18501761","OBJETO_DE_IMPUTACION":"EFF-FP0908","DESCRIPCION_PERSONA":"Cofre Miguel Angel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392948","DESCRIPCION_POSICION":"Operador de Plantas","ID_META_4":"DU41706620","OBJETO_DE_IMPUTACION":"EFF-FP0908","DESCRIPCION_PERSONA":"Nicloux Grecia Macarena","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392950","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU33610908","OBJETO_DE_IMPUTACION":"EFF-FP0908","DESCRIPCION_PERSONA":"Tortosa Garcia Luis Aricelio","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392951","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU29418337","OBJETO_DE_IMPUTACION":"EFF-FP0908","DESCRIPCION_PERSONA":"Mendez Daniela Tamara","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392952","DESCRIPCION_POSICION":"Ingresante de Plantas","ID_META_4":"DU33618500","OBJETO_DE_IMPUTACION":"EFF-FP0908","DESCRIPCION_PERSONA":"Lemos Gustavo Damian","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392953","DESCRIPCION_POSICION":"Operador de Plantas","ID_META_4":"DU35865028","OBJETO_DE_IMPUTACION":"EFF-FP0908","DESCRIPCION_PERSONA":"Carrasco Yohana Yanina Belen","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392955","DESCRIPCION_POSICION":"Operador de Plantas","ID_META_4":"DU16011236","OBJETO_DE_IMPUTACION":"EFF-FP0908","DESCRIPCION_PERSONA":"Zapata Elias","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392956","DESCRIPCION_POSICION":"Operador de Plantas","ID_META_4":"DU92975913","OBJETO_DE_IMPUTACION":"EFF-FP0908","DESCRIPCION_PERSONA":"Sandoval Chandia Ramon Rodrigo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392957","DESCRIPCION_POSICION":"Ingresante de Plantas","ID_META_4":"DU46482269","OBJETO_DE_IMPUTACION":"EFF-FP0908","DESCRIPCION_PERSONA":"Sanhueza Ramiro Exequiel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392931","DESCRIPCION_POSICION":"Operador Sr. de Plantas","ID_META_4":"DU33673463","OBJETO_DE_IMPUTACION":"EFF-FP0906","DESCRIPCION_PERSONA":"Oehmcke Dante Guillermo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. EPF FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392959","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU21381155","OBJETO_DE_IMPUTACION":"EFF-FP0908","DESCRIPCION_PERSONA":"Otarola Alfredo Gustavo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3406968","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU31157058","OBJETO_DE_IMPUTACION":"EFF-FP0907","DESCRIPCION_PERSONA":"Centeno Victor Emilio","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. Planta Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3401243","DESCRIPCION_POSICION":"Maintenance Sr. Supervisor","ID_META_4":"DU27682204","OBJETO_DE_IMPUTACION":"EFF-FN2000","DESCRIPCION_PERSONA":"Ferrari Fernando Gonzalo","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Mazoue Juan Manuel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Otras especialidades","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3392967","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU35753424","OBJETO_DE_IMPUTACION":"EFF-FP0907","DESCRIPCION_PERSONA":"Della Paolera Sebastian","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. Planta Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3406966","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU37697664","OBJETO_DE_IMPUTACION":"EFF-FP0907","DESCRIPCION_PERSONA":"Floridio Alana David","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. Planta Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392966","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU33291680","OBJETO_DE_IMPUTACION":"EFF-FP0907","DESCRIPCION_PERSONA":"Garcia Pacek German Daniel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. Planta Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3406965","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU40067274","OBJETO_DE_IMPUTACION":"EFF-FP0907","DESCRIPCION_PERSONA":"Gutierrez Tomas Agustin","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. Planta Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3406967","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU32710339","OBJETO_DE_IMPUTACION":"EFF-FP0907","DESCRIPCION_PERSONA":"Magliotto Pablo Andres","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. Planta Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392968","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU30264711","OBJETO_DE_IMPUTACION":"EFF-FP0907","DESCRIPCION_PERSONA":"Montenegro Cesar Francisco","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. Planta Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392963","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU42518458","OBJETO_DE_IMPUTACION":"EFF-FP0907","DESCRIPCION_PERSONA":"Querci Damian Agustin","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. Planta Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392964","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU22619156","OBJETO_DE_IMPUTACION":"EFF-FP0907","DESCRIPCION_PERSONA":"Sepulveda Victor Francisco","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. Planta Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393046","DESCRIPCION_POSICION":"Chofer","ID_META_4":"DU25711715","OBJETO_DE_IMPUTACION":"EFF-FP0926","DESCRIPCION_PERSONA":"Espinosa Nestor Victalo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Tareas Generales Mtto FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392971","DESCRIPCION_POSICION":"Operador Especializado Semi Jr. Plantas","ID_META_4":"DU39381423","OBJETO_DE_IMPUTACION":"EFF-FP0909","DESCRIPCION_PERSONA":"Encina Lucas Maximiliano","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Tareas Generales Planta FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392972","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU38493607","OBJETO_DE_IMPUTACION":"EFF-FP0909","DESCRIPCION_PERSONA":"Montesino Matias Eleazar","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Tareas Generales Planta FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392973","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU30588270","OBJETO_DE_IMPUTACION":"EFF-FP0909","DESCRIPCION_PERSONA":"Valenzuela Juan Carlos David","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Tareas Generales Planta FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392974","DESCRIPCION_POSICION":"Chofer Transporte Personal (14+1)","ID_META_4":"DU22379296","OBJETO_DE_IMPUTACION":"EFF-FP0943","DESCRIPCION_PERSONA":"Roga Hector Leandro","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"NUEVO FACILITADOR","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Chofer FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392975","DESCRIPCION_POSICION":"Chofer Especializado Transporte Personal","ID_META_4":"DU31788379","OBJETO_DE_IMPUTACION":"EFF-FP0943","DESCRIPCION_PERSONA":"Zapata Cecilia Liliana","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"NUEVO FACILITADOR","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Chofer FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392976","DESCRIPCION_POSICION":"Ingresante de Oficios","ID_META_4":"DU40067838","OBJETO_DE_IMPUTACION":"EFF-FN1003","DESCRIPCION_PERSONA":"Tapia Facundo Emmanuel","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Rizzo Sebastian","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mecánicos de flota TLM","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392977","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU28075950","OBJETO_DE_IMPUTACION":"EFF-FP0944","DESCRIPCION_PERSONA":"Lopez Jonatan Martin","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Rizzo Sebastian","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mecánicos FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392978","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU40443478","OBJETO_DE_IMPUTACION":"EFF-FP0944","DESCRIPCION_PERSONA":"Garcia Hector Francisco","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Rizzo Sebastian","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mecánicos FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392979","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU40707368","OBJETO_DE_IMPUTACION":"EFF-FP0944","DESCRIPCION_PERSONA":"Quesada Facundo Ezequiel","GERENCIA_JEFATURA":"Maintenance","NOMBRE_JEFE":"Rizzo Sebastian","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mecánicos FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392980","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU35834918","OBJETO_DE_IMPUTACION":"EFF-FP0901","DESCRIPCION_PERSONA":"Salazar Denis Alejandro","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392981","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU25089979","OBJETO_DE_IMPUTACION":"EFF-FP0901","DESCRIPCION_PERSONA":"Castro Marcos Aurelio","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392983","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU29682585","OBJETO_DE_IMPUTACION":"EFF-FP0901","DESCRIPCION_PERSONA":"Fonseca Lucas Ivan","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392984","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU37856716","OBJETO_DE_IMPUTACION":"EFF-FP0901","DESCRIPCION_PERSONA":"Quiñiñiri Sebastian Alejandro","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392985","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU29861604","OBJETO_DE_IMPUTACION":"EFF-FP0901","DESCRIPCION_PERSONA":"Mendoza Segundo Rodolfo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392986","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU29429989","OBJETO_DE_IMPUTACION":"EFF-FP0901","DESCRIPCION_PERSONA":"Garce Mauro Xavier","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392987","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU23718238","OBJETO_DE_IMPUTACION":"EFF-FP0901","DESCRIPCION_PERSONA":"Astorga Sergio Edgardo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392988","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU40960566","OBJETO_DE_IMPUTACION":"EFF-FP0901","DESCRIPCION_PERSONA":"Parada Ariel Gaspar","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392989","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU35834683","OBJETO_DE_IMPUTACION":"EFF-FP0901","DESCRIPCION_PERSONA":"Mendez Milton Gabriel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392990","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU31530001","OBJETO_DE_IMPUTACION":"EFF-FP0901","DESCRIPCION_PERSONA":"Herrera Sergio Mauricio","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392991","DESCRIPCION_POSICION":"Recorredor","ID_META_4":"DU44311211","OBJETO_DE_IMPUTACION":"EFF-FP0901","DESCRIPCION_PERSONA":"Bunajul Emiliano Miguel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392992","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU32909263","OBJETO_DE_IMPUTACION":"EFF-FP0901","DESCRIPCION_PERSONA":"Gutierrez Oscar Javier","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392993","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU23214468","OBJETO_DE_IMPUTACION":"EFF-FP0901","DESCRIPCION_PERSONA":"Abarzua Mario Hernan","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392994","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU24131600","OBJETO_DE_IMPUTACION":"EFF-FP0901","DESCRIPCION_PERSONA":"Ortega Ignacio Jose","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392995","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU36192389","OBJETO_DE_IMPUTACION":"EFF-FP0901","DESCRIPCION_PERSONA":"Donnini Julio Samuel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392996","DESCRIPCION_POSICION":"Recorredor","ID_META_4":"DU33302253","OBJETO_DE_IMPUTACION":"EFF-FP0901","DESCRIPCION_PERSONA":"Rivero Daniel Alexis","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392997","DESCRIPCION_POSICION":"Ayudante de Recorredor","ID_META_4":"DU93793325","OBJETO_DE_IMPUTACION":"EFF-FP0901","DESCRIPCION_PERSONA":"Gonzalez Perez Andy Paolo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392998","DESCRIPCION_POSICION":"Operador Especializado Semi Jr. Plantas","ID_META_4":"DU34734137","OBJETO_DE_IMPUTACION":"EFF-FP0903","DESCRIPCION_PERSONA":"Gallas Fernando Ezequiel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Almacenamiento de Agua FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392999","DESCRIPCION_POSICION":"Operador Especializado Semi Jr. Plantas","ID_META_4":"DU33478674","OBJETO_DE_IMPUTACION":"EFF-FP0903","DESCRIPCION_PERSONA":"Pineda Jorge Oscar","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Almacenamiento de Agua FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393000","DESCRIPCION_POSICION":"Operador Especializado Semi Jr. Plantas","ID_META_4":"DU28621033","OBJETO_DE_IMPUTACION":"EFF-FP0903","DESCRIPCION_PERSONA":"Gonzalez Jorge Omar","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Almacenamiento de Agua FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393001","DESCRIPCION_POSICION":"Operador Especializado Semi Jr. Plantas","ID_META_4":"DU35037940","OBJETO_DE_IMPUTACION":"EFF-FP0903","DESCRIPCION_PERSONA":"Sandoval Marcos Alexis Aryon","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Almacenamiento de Agua FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393002","DESCRIPCION_POSICION":"Operador Especializado Semi Jr. Plantas","ID_META_4":"DU38149619","OBJETO_DE_IMPUTACION":"EFF-FP0903","DESCRIPCION_PERSONA":"Candia Matias Emanuel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Almacenamiento de Agua FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393003","DESCRIPCION_POSICION":"Operador Especializado de Well Testing","ID_META_4":"DU31000303","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Rosales Nelson David","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393004","DESCRIPCION_POSICION":"Operador Especializado de Well Testing","ID_META_4":"DU31086174","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Losso Andres Francisco","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393005","DESCRIPCION_POSICION":"Operador Especializado de Well Testing","ID_META_4":"DU33615416","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Mora Jonatan Daniel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393006","DESCRIPCION_POSICION":"Operador Especializado de Well Testing","ID_META_4":"DU18861854","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Correa Cardenas Gustavo Rodolfo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393007","DESCRIPCION_POSICION":"Chofer Operador","ID_META_4":"DU22440673","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Berra Juan Alberto","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393008","DESCRIPCION_POSICION":"Chofer Operador","ID_META_4":"DU28445476","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Vasquez Roberto Ariel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393009","DESCRIPCION_POSICION":"Recorredor","ID_META_4":"DU33792814","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Fuentes Lopez Gaston Emiliano","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393010","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU33754698","OBJETO_DE_IMPUTACION":"EFF-FP0923","DESCRIPCION_PERSONA":"Quiroga Pedro Pablo","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Instrumentos FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393011","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU43094131","OBJETO_DE_IMPUTACION":"EFF-FP0923","DESCRIPCION_PERSONA":"Fariña Sol Agustina","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Instrumentos FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392982","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU32020422","OBJETO_DE_IMPUTACION":"EFF-FP0901","DESCRIPCION_PERSONA":"Fuentes Roberto Alejandro","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393012","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU41858833","OBJETO_DE_IMPUTACION":"EFF-FP0923","DESCRIPCION_PERSONA":"Montecinos Guzman Elias Daniel","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Instrumentos FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393014","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU41438366","OBJETO_DE_IMPUTACION":"EFF-FP0923","DESCRIPCION_PERSONA":"Valenzuela Joaquin Thomas","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Instrumentos FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393015","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU43215690","OBJETO_DE_IMPUTACION":"EFF-FP0923","DESCRIPCION_PERSONA":"Van Laten Facundo Nicolas","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Instrumentos FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393016","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU37857880","OBJETO_DE_IMPUTACION":"EFF-FP0923","DESCRIPCION_PERSONA":"Aniñir Juan Emanuel","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Instrumentos FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393017","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU45375842","OBJETO_DE_IMPUTACION":"EFF-FP0923","DESCRIPCION_PERSONA":"Gonzalez Guerrero Franco Nicolas","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Instrumentos FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393018","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"","OBJETO_DE_IMPUTACION":"EFF-FP0923","DESCRIPCION_PERSONA":"Vacante relevo instrument FP","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Instrumentos FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393019","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU28180483","OBJETO_DE_IMPUTACION":"EFF-FP0922","DESCRIPCION_PERSONA":"Arin Raul Alberto","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Eléctrico FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393020","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU39950326","OBJETO_DE_IMPUTACION":"EFF-FP0922","DESCRIPCION_PERSONA":"Rodriguez Matias Walter","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Eléctrico FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393021","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU41977742","OBJETO_DE_IMPUTACION":"EFF-FP0922","DESCRIPCION_PERSONA":"Pena Daira Yamel","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Eléctrico FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393022","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU33660770","OBJETO_DE_IMPUTACION":"EFF-FP0922","DESCRIPCION_PERSONA":"Meza Edgardo Joaquin","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Eléctrico FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393024","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU35312911","OBJETO_DE_IMPUTACION":"EFF-FP0921","DESCRIPCION_PERSONA":"Olmedo Nahuel Fernando","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Mecánico FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393025","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU39868058","OBJETO_DE_IMPUTACION":"EFF-FP0921","DESCRIPCION_PERSONA":"Marin Carlos Martin","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Mecánico FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393026","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU35312703","OBJETO_DE_IMPUTACION":"EFF-FP0921","DESCRIPCION_PERSONA":"Lopez Ezequiel Sebastian","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Mecánico FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393027","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU41404711","OBJETO_DE_IMPUTACION":"EFF-FP0921","DESCRIPCION_PERSONA":"Sanchez Ignacio Emanuel","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Mecánico FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393028","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU39266237","OBJETO_DE_IMPUTACION":"EFF-FP0921","DESCRIPCION_PERSONA":"Chanqueo Guillermo Lautaro","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Mecánico FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393029","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU41619361","OBJETO_DE_IMPUTACION":"EFF-FP0921","DESCRIPCION_PERSONA":"Bustamante Agustin","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Mecánico FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393030","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU39354578","OBJETO_DE_IMPUTACION":"EFF-FP0921","DESCRIPCION_PERSONA":"Muñoz Gustavo Alberto","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Mecánico FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393031","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU38536083","OBJETO_DE_IMPUTACION":"EFF-FP0921","DESCRIPCION_PERSONA":"Sanchez Alcaraz Rodrigo Ezequiel","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Mecánico FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393033","DESCRIPCION_POSICION":"Operador Principal de Cuadrilla","ID_META_4":"DU26909367","OBJETO_DE_IMPUTACION":"EFF-FP0921","DESCRIPCION_PERSONA":"Nava Eduardo David","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Mecánico FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393034","DESCRIPCION_POSICION":"Operador Principal de Cuadrilla","ID_META_4":"DU24131430","OBJETO_DE_IMPUTACION":"EFF-FP0925","DESCRIPCION_PERSONA":"Cariñe Juan Marcelo","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Soldadura FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393035","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU29682509","OBJETO_DE_IMPUTACION":"EFF-FP0925","DESCRIPCION_PERSONA":"Zapata Damian Gilberto","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Soldadura FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393036","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU34780573","OBJETO_DE_IMPUTACION":"EFF-FP0925","DESCRIPCION_PERSONA":"Heredia Rogelio Walter Jesus","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Soldadura FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393037","DESCRIPCION_POSICION":"Operador Principal de Cuadrilla","ID_META_4":"DU23346642","OBJETO_DE_IMPUTACION":"EFF-FP0925","DESCRIPCION_PERSONA":"Almonacid Saul Rodrigo","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Soldadura FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393038","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU37603343","OBJETO_DE_IMPUTACION":"EFF-FP0925","DESCRIPCION_PERSONA":"Almonacid Edgar Eliel","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Soldadura FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393039","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU27367750","OBJETO_DE_IMPUTACION":"EFF-FP0925","DESCRIPCION_PERSONA":"Huenupi Cristian Fabian","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Soldadura FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393040","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU39584586","OBJETO_DE_IMPUTACION":"EFF-FP0924","DESCRIPCION_PERSONA":"Inostroza Enzo Alex","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393041","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU43359136","OBJETO_DE_IMPUTACION":"EFF-FP0924","DESCRIPCION_PERSONA":"Dip Emir Abdul","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393042","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU35571160","OBJETO_DE_IMPUTACION":"EFF-FP0924","DESCRIPCION_PERSONA":"Zeni Matias Jesus","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393043","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU50866767","OBJETO_DE_IMPUTACION":"EFF-FP0924","DESCRIPCION_PERSONA":"Soleto Julio Cesar","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393044","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU41420521","OBJETO_DE_IMPUTACION":"EFF-FP0924","DESCRIPCION_PERSONA":"Rojas Kevin Alexis","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393045","DESCRIPCION_POSICION":"Medio Oficial Sr. de Oficios","ID_META_4":"DU26105637","OBJETO_DE_IMPUTACION":"EFF-FP0926","DESCRIPCION_PERSONA":"Flores Jose Luis","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Tareas Generales Mtto FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393054","DESCRIPCION_POSICION":"Ayudante Jr. de Oficios","ID_META_4":"DU30072541","OBJETO_DE_IMPUTACION":"EFF-FP0928","DESCRIPCION_PERSONA":"Perez Juan Hector","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Engrase FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393047","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU20211425","OBJETO_DE_IMPUTACION":"EFF-FP0926","DESCRIPCION_PERSONA":"Rosales Jose Luis","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Tareas Generales Mtto FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393048","DESCRIPCION_POSICION":"Oficial Sr. de Oficios","ID_META_4":"DU33823386","OBJETO_DE_IMPUTACION":"EFF-FP0926","DESCRIPCION_PERSONA":"Quintero Jonathan Carlos","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Tareas Generales Mtto FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393049","DESCRIPCION_POSICION":"Ingresante de Oficios","ID_META_4":"DU45259450","OBJETO_DE_IMPUTACION":"EFF-FP0926","DESCRIPCION_PERSONA":"Fonseca Juance Luca","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Tareas Generales Mtto FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393050","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU24377040","OBJETO_DE_IMPUTACION":"EFF-FP0927","DESCRIPCION_PERSONA":"Marcial Gomez Domingo Alfredo","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Asistencia a Planta FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393051","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU26441378","OBJETO_DE_IMPUTACION":"EFF-FP0927","DESCRIPCION_PERSONA":"Medel Alfredo Ignacio","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Asistencia a Planta FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393052","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU38813625","OBJETO_DE_IMPUTACION":"EFF-FP0927","DESCRIPCION_PERSONA":"Barahona Alexis Emanuel","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Asistencia a Planta FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393053","DESCRIPCION_POSICION":"Operador Especializado Semi Jr. Plantas","ID_META_4":"DU30500550","OBJETO_DE_IMPUTACION":"EFF-FP0927","DESCRIPCION_PERSONA":"Paynemil Jorge Raul","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Asistencia a Planta FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393058","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU44090723","OBJETO_DE_IMPUTACION":"EFF-FP0927","DESCRIPCION_PERSONA":"Vizcarra Walter Adrian","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Asistencia a Planta FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393055","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU31755425","OBJETO_DE_IMPUTACION":"EFF-FP0928","DESCRIPCION_PERSONA":"Hernandez Ramon Horacio","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Engrase FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393056","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU33721679","OBJETO_DE_IMPUTACION":"EFF-FP0928","DESCRIPCION_PERSONA":"Garrido Hector Ruben","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Engrase FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393057","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU27368559","OBJETO_DE_IMPUTACION":"EFF-FP0928","DESCRIPCION_PERSONA":"Urbina Omar Dario","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Engrase FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3409930","DESCRIPCION_POSICION":"Medio Oficial Sr. de Oficios","ID_META_4":"DU31086065","OBJETO_DE_IMPUTACION":"EFF-FP0943","DESCRIPCION_PERSONA":"Sierpina Cristian Luis","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"NUEVO FACILITADOR","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Chofer FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393059","DESCRIPCION_POSICION":"Oficial Especializado de Almacén","ID_META_4":"DU29755100","OBJETO_DE_IMPUTACION":"EFF-LB0942","DESCRIPCION_PERSONA":"Konaschuk Marcelo Nicolas","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Aux. Almacén LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393060","DESCRIPCION_POSICION":"Ayudante de Almacén","ID_META_4":"DU30751007","OBJETO_DE_IMPUTACION":"EFF-FP0942","DESCRIPCION_PERSONA":"Corvalan Romina Del Carmen","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"NUEVO FACILITADOR","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Aux. Almacén FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393061","DESCRIPCION_POSICION":"Administrativo de Almacén","ID_META_4":"DU43703262","OBJETO_DE_IMPUTACION":"EFF-FP0942","DESCRIPCION_PERSONA":"Gutierrez Franco Matias","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"NUEVO FACILITADOR","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Aux. Almacén FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393062","DESCRIPCION_POSICION":"Ayudante de Almacén","ID_META_4":"DU42317710","OBJETO_DE_IMPUTACION":"EFF-FP0942","DESCRIPCION_PERSONA":"Rivera Rosa Camila","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"NUEVO FACILITADOR","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Aux. Almacén FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393063","DESCRIPCION_POSICION":"Administrativo de Almacén","ID_META_4":"DU39682526","OBJETO_DE_IMPUTACION":"EFF-AS0942","DESCRIPCION_PERSONA":"Navarro Jonathan Adrian","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Aux. Almacén SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393064","DESCRIPCION_POSICION":"Administrativo de Almacén","ID_META_4":"DU40334680","OBJETO_DE_IMPUTACION":"EFF-FP0942","DESCRIPCION_PERSONA":"Gonzalez Daiana Ayelen","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"NUEVO FACILITADOR","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Aux. Almacén FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393065","DESCRIPCION_POSICION":"Oficial de Almacén","ID_META_4":"DU22783932","OBJETO_DE_IMPUTACION":"EFF-FP0942","DESCRIPCION_PERSONA":"Aqueveque Mariana","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"NUEVO FACILITADOR","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Aux. Almacén FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393066","DESCRIPCION_POSICION":"Oficial de Almacén","ID_META_4":"DU36257759","OBJETO_DE_IMPUTACION":"EFF-FP0942","DESCRIPCION_PERSONA":"Guerrero Hector Martin","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"NUEVO FACILITADOR","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Aux. Almacén FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393067","DESCRIPCION_POSICION":"Ingresante de Almacén","ID_META_4":"DU37213684","OBJETO_DE_IMPUTACION":"EFF-FP0942","DESCRIPCION_PERSONA":"Contreras Romina Abigail","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"NUEVO FACILITADOR","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Aux. Almacén FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393068","DESCRIPCION_POSICION":"Medio Oficial Sr. de Almacén","ID_META_4":"DU37946173","OBJETO_DE_IMPUTACION":"EFF-FP0942","DESCRIPCION_PERSONA":"San Martin Antonella Claudia Graciela","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"NUEVO FACILITADOR","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Aux. Almacén FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393069","DESCRIPCION_POSICION":"Oficial Sr. de Oficios","ID_META_4":"DU36963012","OBJETO_DE_IMPUTACION":"EFF-FP0929","DESCRIPCION_PERSONA":"Delgado Luciano Miguel","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"NUEVO FACILITADOR","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"T. Grales Serge Fp","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393070","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU42605388","OBJETO_DE_IMPUTACION":"EFF-FP0929","DESCRIPCION_PERSONA":"Mora Matias","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"NUEVO FACILITADOR","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"T. Grales Serge Fp","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393071","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU30500730","OBJETO_DE_IMPUTACION":"EFF-FP0929","DESCRIPCION_PERSONA":"Lizaso Federico Gaston","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"NUEVO FACILITADOR","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"T. Grales Serge Fp","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393072","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU35310859","OBJETO_DE_IMPUTACION":"EFF-FP0929","DESCRIPCION_PERSONA":"Perez Mauro Nicolas","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"NUEVO FACILITADOR","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"T. Grales Serge Fp","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393073","DESCRIPCION_POSICION":"Oficial Sr. de Oficios","ID_META_4":"DU39130831","OBJETO_DE_IMPUTACION":"EFF-FP0929","DESCRIPCION_PERSONA":"Villar Lucas","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"NUEVO FACILITADOR","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"T. Grales Serge Fp","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393074","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU34002040","OBJETO_DE_IMPUTACION":"EFF-FP0929","DESCRIPCION_PERSONA":"Vazquez Jorge Andres","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"NUEVO FACILITADOR","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"T. Grales Serge Fp","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393253","DESCRIPCION_POSICION":"Oficial de Oficios","ID_META_4":"DU37101683","OBJETO_DE_IMPUTACION":"EFF-2E0929","DESCRIPCION_PERSONA":"Sanchez Luz Dalila","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"T. Grales Serge LT2E","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393075","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU22959268","OBJETO_DE_IMPUTACION":"EFF-2E0901","DESCRIPCION_PERSONA":"Botella Sergio David","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"NUEVO FACILITADOR LOTO","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LT2E","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393076","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU29856948","OBJETO_DE_IMPUTACION":"EFF-2E0901","DESCRIPCION_PERSONA":"Zabala Lopez Claudio Luis Alberto","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"NUEVO FACILITADOR LOTO","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LT2E","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393077","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU41609046","OBJETO_DE_IMPUTACION":"EFF-2E0901","DESCRIPCION_PERSONA":"Gonzalez Franco Emanuel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"NUEVO FACILITADOR LOTO","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LT2E","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393078","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU31346496","OBJETO_DE_IMPUTACION":"EFF-2E0901","DESCRIPCION_PERSONA":"Salva Juan Alberto","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"NUEVO FACILITADOR LOTO","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LT2E","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393079","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU14783528","OBJETO_DE_IMPUTACION":"EFF-2E0901","DESCRIPCION_PERSONA":"Bustos Jesus Mario","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"NUEVO FACILITADOR LOTO","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LT2E","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393080","DESCRIPCION_POSICION":"Recorredor","ID_META_4":"DU35835313","OBJETO_DE_IMPUTACION":"EFF-2E0901","DESCRIPCION_PERSONA":"Campos Lucas Jose","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"NUEVO FACILITADOR LOTO","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LT2E","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393081","DESCRIPCION_POSICION":"Recorredor","ID_META_4":"DU37468345","OBJETO_DE_IMPUTACION":"EFF-2E0901","DESCRIPCION_PERSONA":"Melgarejo Gaspar Emmanuel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"NUEVO FACILITADOR LOTO","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LT2E","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393082","DESCRIPCION_POSICION":"Chofer Transporte Personal (9+1)","ID_META_4":"DU29027371","OBJETO_DE_IMPUTACION":"EFF-2E0943","DESCRIPCION_PERSONA":"San Martin Norberto Antonio","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"NUEVO FACILITADOR LOTO","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Chofer LT2E","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393083","DESCRIPCION_POSICION":"Chofer Transporte Personal (9+1)","ID_META_4":"DU30896746","OBJETO_DE_IMPUTACION":"EFF-2E0943","DESCRIPCION_PERSONA":"Santander Marcos Roman","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"NUEVO FACILITADOR LOTO","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Chofer LT2E","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392970","DESCRIPCION_POSICION":"","ID_META_4":"DU38811359","OBJETO_DE_IMPUTACION":"EFF-FP0909","DESCRIPCION_PERSONA":"Parada Matias Gonzalo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Tareas Generales Planta FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3410843","DESCRIPCION_POSICION":"Oficial de Almacén","ID_META_4":"DU37624033","OBJETO_DE_IMPUTACION":"EFF-2E0942","DESCRIPCION_PERSONA":"Castro Micaela Aldana","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"NUEVO FACILITADOR LOTO","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Aux. Almacén LT2E","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3410842","DESCRIPCION_POSICION":"Oficial de Almacén","ID_META_4":"DU35595724","OBJETO_DE_IMPUTACION":"EFF-2E0942","DESCRIPCION_PERSONA":"Sierra Sergio","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"NUEVO FACILITADOR LOTO","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Aux. Almacén LT2E","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392965","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"","OBJETO_DE_IMPUTACION":"EFF-FP0907","DESCRIPCION_PERSONA":"VACANTE PLANTA COMPRESIÓN","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. Planta Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392961","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"","OBJETO_DE_IMPUTACION":"EFF-FP0907","DESCRIPCION_PERSONA":"Vacante planta compresión fpd","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. Planta Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393094","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU44605225","OBJETO_DE_IMPUTACION":"EFF-FP0907","DESCRIPCION_PERSONA":"Vega Obreque Yoel Ezequiel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. Planta Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3406969","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU42849197","OBJETO_DE_IMPUTACION":"EFF-FP0907","DESCRIPCION_PERSONA":"Videla Lucas Patricio","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. Planta Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3392962","DESCRIPCION_POSICION":"Operador Especializado de Plantas","ID_META_4":"DU26530596","OBJETO_DE_IMPUTACION":"EFF-FP0907","DESCRIPCION_PERSONA":"Villagra Eduardo Rogelio","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. Planta Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3426982","DESCRIPCION_POSICION":"Well Services Supervisor","ID_META_4":"DU33178833","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Angelletta Walter Dario","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Buzaglo Sebastian","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3406971","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU26217477","OBJETO_DE_IMPUTACION":"EFF-FP0924","DESCRIPCION_PERSONA":"Irigoyen Mauro Adrian","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3406972","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU30234385","OBJETO_DE_IMPUTACION":"EFF-FP0924","DESCRIPCION_PERSONA":"Gonzalez Nicolas Hipolito","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3406973","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU38810885","OBJETO_DE_IMPUTACION":"EFF-FP0924","DESCRIPCION_PERSONA":"Meier Tomas Agustin","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3406974","DESCRIPCION_POSICION":"Operador Principal de Cuadrilla","ID_META_4":"DU39521568","OBJETO_DE_IMPUTACION":"EFF-FP0924","DESCRIPCION_PERSONA":"Garcia Jorge Andres","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Compresión FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3414078","DESCRIPCION_POSICION":"Mtto TLM","ID_META_4":"DU36841295","OBJETO_DE_IMPUTACION":"EFF-FN1002","DESCRIPCION_PERSONA":"Contreras Hector Hilario","GERENCIA_JEFATURA":"O&M Services - TLM","NOMBRE_JEFE":"Saffe Julian Agustín","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mantenimiento TLM","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3414079","DESCRIPCION_POSICION":"Mtto TLM","ID_META_4":"DU32293205","OBJETO_DE_IMPUTACION":"EFF-FN1002","DESCRIPCION_PERSONA":"Flores Nicolas","GERENCIA_JEFATURA":"O&M Services - TLM","NOMBRE_JEFE":"Saffe Julian Agustín","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mantenimiento TLM","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3414080","DESCRIPCION_POSICION":"Mtto TLM","ID_META_4":"DU32368748","OBJETO_DE_IMPUTACION":"EFF-FN1002","DESCRIPCION_PERSONA":"Barrientos Juan Emilio","GERENCIA_JEFATURA":"O&M Services - TLM","NOMBRE_JEFE":"Saffe Julian Agustín","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mantenimiento TLM","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3414082","DESCRIPCION_POSICION":"Mec Flota TLM","ID_META_4":"DU31358735","OBJETO_DE_IMPUTACION":"EFF-FN1003","DESCRIPCION_PERSONA":"Telechea Gonzalo Gabriel","GERENCIA_JEFATURA":"O&M Services - TLM","NOMBRE_JEFE":"Rizzo Sebastian","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mecánicos de flota TLM","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3414081","DESCRIPCION_POSICION":"Mec Flota TLM","ID_META_4":"DU33475851","OBJETO_DE_IMPUTACION":"EFF-FN1003","DESCRIPCION_PERSONA":"Ochoa Diego Fernando","GERENCIA_JEFATURA":"O&M Services - TLM","NOMBRE_JEFE":"Rizzo Sebastian","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mecánicos de flota TLM","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3414084","DESCRIPCION_POSICION":"4to hombre","ID_META_4":"DU28617096","OBJETO_DE_IMPUTACION":"EFF-FN1001","DESCRIPCION_PERSONA":"Chandia Daniel Arcadio","GERENCIA_JEFATURA":"O&M Services - TLM","NOMBRE_JEFE":"Saffe Julian Agustín","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Operadores TLM","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3414083","DESCRIPCION_POSICION":"4to hombre","ID_META_4":"DU36775845","OBJETO_DE_IMPUTACION":"EFF-FN1001","DESCRIPCION_PERSONA":"Baigorria Rodrigo Emanuel","GERENCIA_JEFATURA":"O&M Services - TLM","NOMBRE_JEFE":"Saffe Julian Agustín","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Operadores TLM","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3414085","DESCRIPCION_POSICION":"4to hombre","ID_META_4":"DU43759638","OBJETO_DE_IMPUTACION":"EFF-FN1001","DESCRIPCION_PERSONA":"Reyes Castillo Lihuen","GERENCIA_JEFATURA":"O&M Services - TLM","NOMBRE_JEFE":"Saffe Julian Agustín","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Operadores TLM","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3414087","DESCRIPCION_POSICION":"Coord Camiones","ID_META_4":"DU40458028","OBJETO_DE_IMPUTACION":"EFF-FN1001","DESCRIPCION_PERSONA":"Logarzo Julian Alejandro","GERENCIA_JEFATURA":"O&M Services - TLM","NOMBRE_JEFE":"Saffe Julian Agustín","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Operadores TLM","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3414086","DESCRIPCION_POSICION":"Coord Camiones","ID_META_4":"DU36800803","OBJETO_DE_IMPUTACION":"EFF-FN1001","DESCRIPCION_PERSONA":"Poblete Matias Ezequiel","GERENCIA_JEFATURA":"O&M Services - TLM","NOMBRE_JEFE":"Saffe Julian Agustín","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Operadores TLM","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3414088","DESCRIPCION_POSICION":"Coord Camiones","ID_META_4":"DU31978173","OBJETO_DE_IMPUTACION":"EFF-FN1001","DESCRIPCION_PERSONA":"Peña Dardo Levis","GERENCIA_JEFATURA":"O&M Services - TLM","NOMBRE_JEFE":"Saffe Julian Agustín","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Operadores TLM","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3414090","DESCRIPCION_POSICION":"Op. Autoelevador","ID_META_4":"DU39130922","OBJETO_DE_IMPUTACION":"EFF-FN1001","DESCRIPCION_PERSONA":"Manzano Peña Rodrigo Arnaldo","GERENCIA_JEFATURA":"O&M Services - TLM","NOMBRE_JEFE":"Saffe Julian Agustín","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Operadores TLM","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3414089","DESCRIPCION_POSICION":"Op. Autoelevador","ID_META_4":"DU38492506","OBJETO_DE_IMPUTACION":"EFF-FN1001","DESCRIPCION_PERSONA":"Martinez Mauricio Alejandro","GERENCIA_JEFATURA":"O&M Services - TLM","NOMBRE_JEFE":"Saffe Julian Agustín","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Operadores TLM","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3414091","DESCRIPCION_POSICION":"Op. Autoelevador","ID_META_4":"DU41241632","OBJETO_DE_IMPUTACION":"EFF-FN1001","DESCRIPCION_PERSONA":"Barrera Poblete Pablo Alejandro","GERENCIA_JEFATURA":"O&M Services - TLM","NOMBRE_JEFE":"Saffe Julian Agustín","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Operadores TLM","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3414092","DESCRIPCION_POSICION":"Op. Blender","ID_META_4":"DU25329470","OBJETO_DE_IMPUTACION":"EFF-FN1001","DESCRIPCION_PERSONA":"Hidalgo Sergio Antonio","GERENCIA_JEFATURA":"O&M Services - TLM","NOMBRE_JEFE":"Saffe Julian Agustín","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Operadores TLM","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3414093","DESCRIPCION_POSICION":"Op. Blender","ID_META_4":"DU40443299","OBJETO_DE_IMPUTACION":"EFF-FN1001","DESCRIPCION_PERSONA":"Vazquez Juan Carlos","GERENCIA_JEFATURA":"O&M Services - TLM","NOMBRE_JEFE":"Saffe Julian Agustín","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Operadores TLM","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3414094","DESCRIPCION_POSICION":"Op. Blender","ID_META_4":"","OBJETO_DE_IMPUTACION":"EFF-FN1001","DESCRIPCION_PERSONA":"Vacante Oper TLM","GERENCIA_JEFATURA":"O&M Services - TLM","NOMBRE_JEFE":"Saffe Julian Agustín","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Operadores TLM","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3414095","DESCRIPCION_POSICION":"Relevo","ID_META_4":"DU40217645","OBJETO_DE_IMPUTACION":"EFF-FN1004","DESCRIPCION_PERSONA":"Jarpa Matias Leonardo","GERENCIA_JEFATURA":"O&M Services - TLM","NOMBRE_JEFE":"Saffe Julian Agustín","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Relevos TLM","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3414096","DESCRIPCION_POSICION":"Relevo","ID_META_4":"DU28443459","OBJETO_DE_IMPUTACION":"EFF-FN1004","DESCRIPCION_PERSONA":"Torres Lorena","GERENCIA_JEFATURA":"O&M Services - TLM","NOMBRE_JEFE":"Saffe Julian Agustín","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Relevos TLM","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3414097","DESCRIPCION_POSICION":"Relevo","ID_META_4":"DU33042995","OBJETO_DE_IMPUTACION":"EFF-FN1004","DESCRIPCION_PERSONA":"Escalona Saulo Hermogenes","GERENCIA_JEFATURA":"O&M Services - TLM","NOMBRE_JEFE":"Saffe Julian Agustín","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Relevos TLM","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3418971","DESCRIPCION_POSICION":"Trainee Plantas","ID_META_4":"DU45734542","OBJETO_DE_IMPUTACION":"EFF-FP0905","DESCRIPCION_PERSONA":"Fernandez Abel Nicolás","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. LTS FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3426983","DESCRIPCION_POSICION":"Well Services Supervisor","ID_META_4":"DU24829767","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Sanchez Burgos Fidel Facundo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Buzaglo Sebastian","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"WC","ENCUADRE":""},{"POSICION":"3418962","DESCRIPCION_POSICION":"Ayudante tareas generales","ID_META_4":"DU32529392","OBJETO_DE_IMPUTACION":"EFF-2E0929","DESCRIPCION_PERSONA":"Montiel Gabriel Alberto","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"T. Grales Serge LT2E","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3418963","DESCRIPCION_POSICION":"Operador Well Services","ID_META_4":"DU39355037","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Kochereschuk Brian Alexis","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3418964","DESCRIPCION_POSICION":"Operador Well Services","ID_META_4":"DU33238769","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Lopez Ramiro Alejandro Antonio","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3418965","DESCRIPCION_POSICION":"Operador Well Services","ID_META_4":"DU35597526","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Garcia Leandro Erik Maximiliano","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3418966","DESCRIPCION_POSICION":"Operador Well Services","ID_META_4":"DU31400064","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Prieto Hugo Ernesto","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3418967","DESCRIPCION_POSICION":"Operador Well Services","ID_META_4":"DU28003231","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Silva Diego Mauro","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3418968","DESCRIPCION_POSICION":"Operador Well Services","ID_META_4":"DU32722769","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Alderete Pablo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3418969","DESCRIPCION_POSICION":"Operador Well Services","ID_META_4":"DU35372033","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Matus Mondaca Gustavo Adan","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3418970","DESCRIPCION_POSICION":"Operador Well Services","ID_META_4":"DU39890914","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Firpo Gabriel Cesar Ivan","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3418978","DESCRIPCION_POSICION":"Relevo Well Services","ID_META_4":"DU41706851","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Canales Ruiz Axel Agustín","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3423202","DESCRIPCION_POSICION":"Oficial Mtto Well Services","ID_META_4":"DU28234455","OBJETO_DE_IMPUTACION":"EFF-FP0934","DESCRIPCION_PERSONA":"Benedetti Adolfo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Well Services FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3423203","DESCRIPCION_POSICION":"Oficial Mtto Well Services","ID_META_4":"DU43703072","OBJETO_DE_IMPUTACION":"EFF-FP0934","DESCRIPCION_PERSONA":"Castillo Guillermo Marcos","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Well Services FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3393013","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU35598771","OBJETO_DE_IMPUTACION":"EFF-FP0923","DESCRIPCION_PERSONA":"Figueroa Gabriel Maximiliano","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Instrumentos FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3423204","DESCRIPCION_POSICION":"Oficial Mtto Well Services","ID_META_4":"DU27986815","OBJETO_DE_IMPUTACION":"EFF-FP0934","DESCRIPCION_PERSONA":"Rivas Angel Adrian","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Well Services FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3423205","DESCRIPCION_POSICION":"Oficial Mtto Well Services","ID_META_4":"DU31316501","OBJETO_DE_IMPUTACION":"EFF-FP0934","DESCRIPCION_PERSONA":"Estrada Rodrigo Maximiliano","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Well Services FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3418977","DESCRIPCION_POSICION":"Ingresante sin experiencia","ID_META_4":"DU35886670","OBJETO_DE_IMPUTACION":"EFF-AS0908","DESCRIPCION_PERSONA":"Arias Francisco Ramon","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Garcia Pereira Maria Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. PTA SALA","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3418976","DESCRIPCION_POSICION":"Ingresante sin experiencia","ID_META_4":"","OBJETO_DE_IMPUTACION":"EFF-LB0921","DESCRIPCION_PERSONA":"Vacante relevo vacas LBAS (eliminar)","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Bechara Lucas Antonio","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Mecánico LBAS","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3418961","DESCRIPCION_POSICION":"Ingresante sin experiencia","ID_META_4":"DU44757443","OBJETO_DE_IMPUTACION":"EFF-2E0942","DESCRIPCION_PERSONA":"Lima Marcos","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Aux. Almacén LT2E","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3418974","DESCRIPCION_POSICION":"Ayudante de Oficio","ID_META_4":"","OBJETO_DE_IMPUTACION":"EFF-FP0921","DESCRIPCION_PERSONA":"Vacante relevo vacas FDP","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Mtto Mecánico FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3418973","DESCRIPCION_POSICION":"Ingresante sin experiencia","ID_META_4":"","OBJETO_DE_IMPUTACION":"EFF-FP0905","DESCRIPCION_PERSONA":"vacante relevo vacaciones plantas FP","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Cordova Daniela Emiliana","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. LTS FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3418972","DESCRIPCION_POSICION":"Trainee Plantas","ID_META_4":"DU47284823","OBJETO_DE_IMPUTACION":"EFF-FP0905","DESCRIPCION_PERSONA":"Valenzuela Wachnowski Juan Daniel","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper. LTS FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3424468","DESCRIPCION_POSICION":"Ayudante de oficio","ID_META_4":"DU45359605","OBJETO_DE_IMPUTACION":"EFF-FP0935","DESCRIPCION_PERSONA":"Orduña Marcelo Ruben","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Casal Gustavo","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Montaje y Soldadura FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3424469","DESCRIPCION_POSICION":"Ayudante de oficio","ID_META_4":"DU18839363","OBJETO_DE_IMPUTACION":"EFF-FP0935","DESCRIPCION_PERSONA":"Vaca Olarte Eulalio","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Casal Gustavo","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Montaje y Soldadura FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3424470","DESCRIPCION_POSICION":"Ayudante de oficio","ID_META_4":"DU32020376","OBJETO_DE_IMPUTACION":"EFF-FP0935","DESCRIPCION_PERSONA":"Soto Hector Damian","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Casal Gustavo","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Montaje y Soldadura FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3424471","DESCRIPCION_POSICION":"Ayudante de oficio","ID_META_4":"DU3276876","OBJETO_DE_IMPUTACION":"EFF-FP0935","DESCRIPCION_PERSONA":"Moreno Augusto Armando","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Casal Gustavo","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Montaje y Soldadura FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3424472","DESCRIPCION_POSICION":"Ayudante de oficio","ID_META_4":"DU24131621","OBJETO_DE_IMPUTACION":"EFF-FP0935","DESCRIPCION_PERSONA":"Medele Jose Gabriel","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Casal Gustavo","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Montaje y Soldadura FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3424473","DESCRIPCION_POSICION":"Ayudante de oficio","ID_META_4":"DU37946412","OBJETO_DE_IMPUTACION":"EFF-FP0935","DESCRIPCION_PERSONA":"Almendra Josue Damian","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Casal Gustavo","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Montaje y Soldadura FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3424474","DESCRIPCION_POSICION":"Ayudante de oficio","ID_META_4":"DU3551955","OBJETO_DE_IMPUTACION":"EFF-FP0935","DESCRIPCION_PERSONA":"Rios Ricardo Isaias","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Casal Gustavo","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Montaje y Soldadura FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3433389","DESCRIPCION_POSICION":"Oficial Especializado de Oficios","ID_META_4":"DU36945549","OBJETO_DE_IMPUTACION":"EFF-FP0935","DESCRIPCION_PERSONA":"Sierra Quezada Jorge Antonio","GERENCIA_JEFATURA":"","NOMBRE_JEFE":"Casal Gustavo","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Montaje y Soldadura FP","WC_BC":"","ENCUADRE":""},{"POSICION":"3424475","DESCRIPCION_POSICION":"Ayudante de oficio","ID_META_4":"DU31466831","OBJETO_DE_IMPUTACION":"EFF-FP0935","DESCRIPCION_PERSONA":"Vetoño Oscar Osvaldo","GERENCIA_JEFATURA":"O&M Services - Maintenance","NOMBRE_JEFE":"Casal Gustavo","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Montaje y Soldadura FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3424479","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU30941809","OBJETO_DE_IMPUTACION":"EFF-1N0901","DESCRIPCION_PERSONA":"Sandoval Sebastian Matias","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Mondaca Ruben Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LT1N","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3424480","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU37175343","OBJETO_DE_IMPUTACION":"EFF-1N0901","DESCRIPCION_PERSONA":"Barros Luis Maximiliano","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Mondaca Ruben Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LT1N","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3424481","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU39650102","OBJETO_DE_IMPUTACION":"EFF-1N0901","DESCRIPCION_PERSONA":"Martinez German Matias","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Mondaca Ruben Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LT1N","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3424482","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU29515759","OBJETO_DE_IMPUTACION":"EFF-1N0901","DESCRIPCION_PERSONA":"Escobar Santiago Esteban","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Mondaca Ruben Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LT1N","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3424483","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU37749280","OBJETO_DE_IMPUTACION":"EFF-1N0901","DESCRIPCION_PERSONA":"Martinez Jonathan Damian","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Mondaca Ruben Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LT1N","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3424484","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU30072565","OBJETO_DE_IMPUTACION":"EFF-1N0901","DESCRIPCION_PERSONA":"Muñoz Cristian Diego","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Mondaca Ruben Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LT1N","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3424485","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU28180782","OBJETO_DE_IMPUTACION":"EFF-1N0901","DESCRIPCION_PERSONA":"Nazario Walter","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Mondaca Ruben Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LT1N","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3424486","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU26084689","OBJETO_DE_IMPUTACION":"EFF-1N0901","DESCRIPCION_PERSONA":"Zara Gustavo Oscar","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Mondaca Ruben Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LT1N","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3424487","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU93387069","OBJETO_DE_IMPUTACION":"EFF-1N0901","DESCRIPCION_PERSONA":"Medel Omar Andres","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Mondaca Ruben Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LT1N","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3424488","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU25113854","OBJETO_DE_IMPUTACION":"EFF-1N0901","DESCRIPCION_PERSONA":"Fernandez Pablo Rodolfo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Mondaca Ruben Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LT1N","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3424489","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU35879316","OBJETO_DE_IMPUTACION":"EFF-1N0901","DESCRIPCION_PERSONA":"Coronel Hugo Martin","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Mondaca Ruben Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LT1N","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3424490","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU38205837","OBJETO_DE_IMPUTACION":"EFF-1N0901","DESCRIPCION_PERSONA":"Farias Franco Danilo","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Mondaca Ruben Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LT1N","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3424491","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU41438906","OBJETO_DE_IMPUTACION":"EFF-1N0901","DESCRIPCION_PERSONA":"Gonzalez Axel Gabriel","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Mondaca Ruben Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LT1N","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3424492","DESCRIPCION_POSICION":"Recorredor Especializado","ID_META_4":"DU42806968","OBJETO_DE_IMPUTACION":"EFF-1N0901","DESCRIPCION_PERSONA":"Blanco Saul Alberto","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Mondaca Ruben Jose","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper campo LT1N","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3425377","DESCRIPCION_POSICION":"Ayudante tareas generales","ID_META_4":"","OBJETO_DE_IMPUTACION":"EFF-FP0909","DESCRIPCION_PERSONA":"vacante cuadrilla temporal","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Tareas Generales Planta FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3425376","DESCRIPCION_POSICION":"Ayudante tareas generales","ID_META_4":"","OBJETO_DE_IMPUTACION":"EFF-FP0909","DESCRIPCION_PERSONA":"vacante cuadrilla temporal","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Casal Gustavo Daniel","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Tareas Generales Planta FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3430740","DESCRIPCION_POSICION":"Operador Well Services","ID_META_4":"DU36955491","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Jesus Carlos Abraham","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3430741","DESCRIPCION_POSICION":"Operador Well Services","ID_META_4":"DU31637775","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Diaz Jonatan Nicolas","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3430742","DESCRIPCION_POSICION":"Operador Well Services","ID_META_4":"DU30231611","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Rosas Diego Nicolas","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"BC","ENCUADRE":""},{"POSICION":"3430743","DESCRIPCION_POSICION":"Operador Well Services","ID_META_4":"DU31805538","OBJETO_DE_IMPUTACION":"EFF-FP0902","DESCRIPCION_PERSONA":"Cardenas Cristian Ivan","GERENCIA_JEFATURA":"O&M Services - Operations","NOMBRE_JEFE":"Macias Ceferino Oscar","SOCIEDAD":"Energy Field Services","FLAG_LICENCIA":"Oper Well Services FP","WC_BC":"BC","ENCUADRE":""}]
;

// ===== STATE =====
// _uid: stable unique id per row, independent of array index
let uidCounter = 0;
let data = JSON.parse(JSON.stringify(BASE)).map(r => ({...r, _uid: uidCounter++}));

// snapshots keyed by _uid
let snaps = {};
function getSnap(uid){ return snaps[uid] || []; }
function pushSnap(uid, row){ if(!snaps[uid]) snaps[uid]=[]; snaps[uid].push(JSON.parse(JSON.stringify(row))); if(snaps[uid].length>15) snaps[uid].shift(); }
function popSnap(uid){ return snaps[uid] && snaps[uid].length ? snaps[uid].pop() : null; }
function hasSnap(uid){ return snaps[uid] && snaps[uid].length > 0; }

let changelog = JSON.parse(localStorage.getItem('efis_cl4') || '[]');
let uploadPending = null;
let curPage = 0;
const PAGE = 50;
let sortF = 'GERENCIA_JEFATURA', sortA = true;
let onlyVac = false, onlyDup = false;
let editIdx = null, bajaIdx = null, rotIdx = null;

// ===== HELPERS =====
function isVac(r){ return !r.ID_META_4 || /^vacante|baja posici/i.test(r.DESCRIPCION_PERSONA || ''); }

function addCL(tipo, persona, desc, det){
  changelog.unshift({id: Date.now(), fecha: new Date().toLocaleString('es-AR'), tipo, persona, desc, det});
  localStorage.setItem('efis_cl4', JSON.stringify(changelog));
  document.getElementById('stMov').textContent = changelog.length;
}

// ===== DUPLICATES =====
function computeDups(){
  const posCount = {}, dniCount = {};
  data.forEach(r => {
    if(r.POSICION) posCount[r.POSICION] = (posCount[r.POSICION]||0)+1;
    if(r.ID_META_4 && !isVac(r)) dniCount[r.ID_META_4] = (dniCount[r.ID_META_4]||0)+1;
  });
  const dupPos = new Set(Object.keys(posCount).filter(k => posCount[k]>1));
  const dupDni = new Set(Object.keys(dniCount).filter(k => dniCount[k]>1));
  let total = 0;
  data.forEach(r => { if(getDupClass(r,dupPos,dupDni)) total++; });
  return {dupPos, dupDni, total};
}
function getDupClass(r, dupPos, dupDni){
  const dp = r.POSICION && dupPos.has(r.POSICION);
  const dd = r.ID_META_4 && !isVac(r) && dupDni.has(r.ID_META_4);
  if(dp && dd) return 'dup-both';
  if(dp) return 'dup-pos';
  if(dd) return 'dup-dni';
  return '';
}
function getDupTip(r, dupPos, dupDni){
  const t=[];
  if(r.POSICION && dupPos.has(r.POSICION)) t.push('Posición SAP duplicada');
  if(r.ID_META_4 && !isVac(r) && dupDni.has(r.ID_META_4)) t.push('DNI duplicado');
  return t.join(' + ');
}

// ===== INIT =====
function init(){
  const servs = [...new Set(data.map(r=>r.GERENCIA_JEFATURA).filter(Boolean))].sort();
  const cecos = [...new Set(data.map(r=>r.OBJETO_DE_IMPUTACION).filter(Boolean))].sort();
  const jefes = [...new Set(data.map(r=>r.NOMBRE_JEFE).filter(Boolean))].sort();

  function fillSel(id, arr){ arr.forEach(v=>{ const o=document.createElement('option'); o.value=v; o.textContent=v; document.getElementById(id).appendChild(o); }); }
  function fillDL(id, arr){ const dl=document.getElementById(id); arr.forEach(v=>{ const o=document.createElement('option'); o.value=v; dl.appendChild(o); }); }

  fillSel('fServ', servs); fillSel('fCeco', cecos);
  const flags = [...new Set(data.map(r=>r.FLAG_LICENCIA).filter(Boolean))].sort();
  fillSel('fFlag', flags);
  fillDL('dlCeco', cecos); fillDL('dlServ', servs); fillDL('dlJefe', jefes);

  updateStats(); renderPersonal(); renderVacantes(); renderServicios(); renderChangelog();
}

function updateStats(){
  const total = data.length;
  const vac = data.filter(isVac).length;
  const wc = data.filter(r=>r.WC_BC==='WC'&&!isVac(r)).length;
  const bc = data.filter(r=>r.WC_BC==='BC'&&!isVac(r)).length;
  const {total:dups} = computeDups();
  document.getElementById('stTotal').textContent = total;
  document.getElementById('stOcup').textContent = total - vac;
  document.getElementById('stVac').textContent = vac;
  document.getElementById('stWC').textContent = wc;
  document.getElementById('stBC').textContent = bc;
  document.getElementById('stDup').textContent = dups;
  document.getElementById('stMov').textContent = changelog.length;
}

// ===== FILTER / SORT =====
function getFiltered(){
  const s = document.getElementById('srch').value.toLowerCase();
  const serv = document.getElementById('fServ').value;
  const ceco = document.getElementById('fCeco').value;
  const wcbc = document.getElementById('fWCBC').value;
  const soc  = document.getElementById('fSoc').value;
  const flag = document.getElementById('fFlag').value;
  const {dupPos, dupDni} = computeDups();

  return data.filter(r => {
    if(onlyVac && !isVac(r)) return false;
    if(onlyDup && !getDupClass(r,dupPos,dupDni)) return false;
    if(serv && r.GERENCIA_JEFATURA !== serv) return false;
    if(ceco && r.OBJETO_DE_IMPUTACION !== ceco) return false;
    if(wcbc && r.WC_BC !== wcbc) return false;
    if(soc  && r.SOCIEDAD !== soc) return false;
    if(flag && r.FLAG_LICENCIA !== flag) return false;
    if(s){
      const hay = [r.DESCRIPCION_PERSONA,r.ID_META_4,r.POSICION,r.OBJETO_DE_IMPUTACION,r.DESCRIPCION_POSICION,r.GERENCIA_JEFATURA,r.NOMBRE_JEFE,r.FLAG_LICENCIA].join(' ').toLowerCase();
      if(!hay.includes(s)) return false;
    }
    return true;
  }).sort((a,b)=>{
    const va=(a[sortF]||'').toString().toLowerCase(), vb=(b[sortF]||'').toString().toLowerCase();
    return sortA ? va.localeCompare(vb) : vb.localeCompare(va);
  });
}
function sortBy(f){ if(sortF===f) sortA=!sortA; else{sortF=f;sortA=true;} curPage=0; renderPersonal(); }
function toggleFilter(type){
  if(type==='vac'){ onlyVac=!onlyVac; document.getElementById('btnVac').classList.toggle('on',onlyVac); }
  else { onlyDup=!onlyDup; document.getElementById('btnDup').classList.toggle('on-r',onlyDup); document.getElementById('dupLegend').style.display=onlyDup?'flex':'none'; }
  curPage=0; renderPersonal();
}
function changePage(d){
  const mp = Math.ceil(getFiltered().length/PAGE)-1;
  curPage = Math.max(0,Math.min(curPage+d,mp));
  renderPersonal();
}

// ===== RENDER PERSONAL =====
function renderPersonal(){
  const f = getFiltered();
  const s = curPage*PAGE;
  const pg = f.slice(s, s+PAGE);
  const mp = Math.ceil(f.length/PAGE);
  document.getElementById('pgInfo').textContent = f.length ? `${s+1}–${Math.min(s+PAGE,f.length)} de ${f.length}` : '0 resultados';
  document.getElementById('btnPrev').disabled = curPage===0;
  document.getElementById('btnNext').disabled = curPage>=mp-1;

  const {dupPos,dupDni} = computeDups();
  const tb = document.getElementById('tbPersonal');
  if(!pg.length){ tb.innerHTML='<tr><td colspan="12" class="empty">Sin resultados para los filtros aplicados</td></tr>'; return; }

  tb.innerHTML = pg.map(r => {
    const idx = data.indexOf(r);
    const vac = isVac(r);
    const dc = getDupClass(r,dupPos,dupDni);
    const tip = getDupTip(r,dupPos,dupDni);
    const dupIcon = dc ? `<span class="dup-icon" title="${tip}">⬥</span>` : '';
    const canRevert = hasSnap(r._uid);

    const wctag = r.WC_BC==='WC' ? '<span class="tag tb">WC</span>' : r.WC_BC==='BC' ? '<span class="tag tp">BC</span>' : '<span class="tag tgr">—</span>';
    const soctag = r.SOCIEDAD==='TECPETROL S.A.' ? '<span class="tag tb" title="TECPETROL S.A.">TECPE</span>' : '<span class="tag tgr" title="Energy Field Services">EFS</span>';
    const esttag = vac ? '<span class="tag ty">Vacante</span>' : '<span class="tag tg">Activo</span>';
    const persona = vac
      ? `<span class="vacl">⚠ ${(r.DESCRIPCION_PERSONA||'VACANTE').substring(0,28)}</span>${dupIcon}`
      : `<span class="pname">${(r.DESCRIPCION_PERSONA||'').substring(0,26)}</span>${dupIcon}`;

    return `<tr class="${vac?'vac':''} ${dc}">
      <td class="pos" title="${r.POSICION||''}">${r.POSICION||'—'}</td>
      <td title="${r.DESCRIPCION_PERSONA||''}">${persona}</td>
      <td class="pos">${r.ID_META_4||'—'}</td>
      <td class="ceco">${r.OBJETO_DE_IMPUTACION||'—'}</td>
      <td title="${r.DESCRIPCION_POSICION||''}">${(r.DESCRIPCION_POSICION||'—').substring(0,26)}</td>
      <td title="${r.GERENCIA_JEFATURA||''}">${(r.GERENCIA_JEFATURA||'—').substring(0,24)}</td>
      <td title="${r.NOMBRE_JEFE||''}">${(r.NOMBRE_JEFE||'—').substring(0,22)}</td>
      <td title="${r.FLAG_LICENCIA||''}"><span class="tag tgr" style="font-size:10px">${(r.FLAG_LICENCIA||'—').substring(0,22)}</span></td>
      <td>${wctag}</td>
      <td>${soctag}</td>
      <td>${esttag}</td>
      <td><div class="ract">
        <button class="ab ab-e" onclick="openEdit(${idx})">Editar</button>
        ${!vac ? `<button class="ab ab-m" onclick="openRot(${idx})">Mover</button>` : ''}
        ${!vac ? `<button class="ab ab-d" onclick="openBaja(${idx})">Baja</button>` : ''}
        ${canRevert ? `<button class="ab ab-u" onclick="revertir(${idx})" title="Deshacer último cambio">↩ Deshacer</button>` : ''}
      </div></td>
    </tr>`;
  }).join('');
}

// ===== RENDER VACANTES =====
function renderVacantes(){
  const vacs = data.filter(isVac);
  const tb = document.getElementById('tbVacantes');
  if(!vacs.length){ tb.innerHTML='<tr><td colspan="8" class="empty">No hay vacantes registradas. ¡Excelente!</td></tr>'; return; }
  tb.innerHTML = vacs.map(r => {
    const idx = data.indexOf(r);
    const wctag = r.WC_BC==='WC' ? '<span class="tag tb">WC</span>' : r.WC_BC==='BC' ? '<span class="tag tp">BC</span>' : '<span class="tag tgr">—</span>';
    return `<tr class="vac">
      <td class="pos">${r.POSICION||'—'}</td>
      <td title="${r.DESCRIPCION_PERSONA||''}" style="color:var(--warn);font-style:italic">${(r.DESCRIPCION_PERSONA||'—').substring(0,36)}</td>
      <td class="ceco">${r.OBJETO_DE_IMPUTACION||'—'}</td>
      <td title="${r.FLAG_LICENCIA||''}"><span class="tag tgr" style="font-size:10px">${(r.FLAG_LICENCIA||'—').substring(0,28)}</span></td>
      <td>${wctag}</td>
      <td>${r.SOCIEDAD==='TECPETROL S.A.'?'<span class="tag tb">TECPE</span>':'<span class="tag tgr">EFS</span>'}</td>
      <td title="${r.NOMBRE_JEFE||''}">${(r.NOMBRE_JEFE||'—').substring(0,24)}</td>
      <td><button class="btn btn-p" style="padding:3px 10px;font-size:11px" onclick="openEdit(${idx})">Cubrir</button></td>
    </tr>`;
  }).join('');
}

// ===== RENDER SERVICIOS =====
function initServiciosFilters(){
  const sel = document.getElementById('fFlagServ');
  if(sel.options.length > 1) return; // already populated
  const servs = [...new Set(data.map(r=>r.GERENCIA_JEFATURA).filter(Boolean))].sort();
  servs.forEach(s=>{ const o=document.createElement('option'); o.value=s; o.textContent=s; sel.appendChild(o); });
}

function renderServicios(){
  initServiciosFilters();
  const search = (document.getElementById('fFlag').value||'').toLowerCase();
  const servFilt = document.getElementById('fFlagServ').value;

  // Group by FLAG_LICENCIA
  const by = {};
  data.forEach(r => {
    const flag = r.FLAG_LICENCIA || 'Sin cuadrilla';
    const serv = r.GERENCIA_JEFATURA || 'Sin servicio';
    if(servFilt && serv !== servFilt) return;
    if(search && !flag.toLowerCase().includes(search)) return;
    if(!by[flag]) by[flag] = {t:0, o:0, v:0, wc:0, bc:0, servs: new Set()};
    by[flag].t++;
    by[flag].servs.add(serv);
    if(isVac(r)) by[flag].v++;
    else {
      by[flag].o++;
      if(r.WC_BC==='WC') by[flag].wc++;
      else if(r.WC_BC==='BC') by[flag].bc++;
    }
  });

  // Summary totals bar
  const allFlags = Object.values(by);
  const totT = allFlags.reduce((a,s)=>a+s.t,0);
  const totO = allFlags.reduce((a,s)=>a+s.o,0);
  const totV = allFlags.reduce((a,s)=>a+s.v,0);
  document.getElementById('flagSummary').innerHTML = `
    <div style="background:var(--surface);border:1px solid var(--border);border-radius:6px;padding:8px 14px;display:flex;gap:20px;align-items:center;box-shadow:var(--shadow);flex-wrap:wrap">
      <span style="font-size:11px;font-weight:700;color:var(--text2);letter-spacing:.05em">TOTALES VISIBLES</span>
      <span style="font-family:var(--mono);font-size:13px;font-weight:700;color:var(--accent)">${allFlags.length} cuadrillas</span>
      <span style="font-size:12px;color:var(--text2)">·</span>
      <span style="font-family:var(--mono);font-size:13px;font-weight:700;color:var(--text)">${totT} posiciones</span>
      <span style="font-size:12px;color:var(--text2)">·</span>
      <span style="font-family:var(--mono);font-size:13px;font-weight:700;color:var(--success)">${totO} ocupadas</span>
      <span style="font-size:12px;color:var(--text2)">·</span>
      <span style="font-family:var(--mono);font-size:13px;font-weight:700;color:${totV?'var(--warn)':'var(--muted)'}">${totV} vacantes</span>
    </div>`;

  if(!allFlags.length){
    document.getElementById('sGrid').innerHTML='<div class="empty" style="grid-column:1/-1">Sin cuadrillas para los filtros aplicados.</div>';
    return;
  }

  const mx = Math.max(...allFlags.map(s=>s.t));
  document.getElementById('sGrid').innerHTML = Object.entries(by)
    .sort((a,b) => b[1].t - a[1].t)
    .map(([flag, st]) => {
      const servList = [...st.servs].join(', ');
      return `
      <div class="sc" style="cursor:default">
        <div class="sch">
          <div class="sct" title="${flag}">${flag.length>36?flag.substring(0,34)+'…':flag}</div>
          ${st.v ? `<span class="tag ty">${st.v} vac.</span>` : '<span class="tag tg">Sin vac.</span>'}
        </div>
        <div style="font-size:10px;color:var(--muted);margin-top:-2px" title="${servList}">${servList.length>50?servList.substring(0,48)+'…':servList}</div>
        <div class="sb"><div class="sbf" style="width:${(st.t/mx*100).toFixed(1)}%"></div></div>
        <div class="sn">
          <div><div class="snv" style="color:var(--accent)">${st.t}</div><div class="snl">Total</div></div>
          <div><div class="snv" style="color:var(--success)">${st.o}</div><div class="snl">Ocup.</div></div>
          <div><div class="snv" style="color:${st.v?'var(--warn)':'var(--muted)'}">${st.v}</div><div class="snl">Vac.</div></div>
          <div><div class="snv" style="color:var(--accent2)">${st.wc}</div><div class="snl">WC</div></div>
          <div><div class="snv" style="color:var(--purple)">${st.bc}</div><div class="snl">BC</div></div>
        </div>
      </div>`;
    }).join('');
}

// ===== RENDER CHANGELOG =====
function renderChangelog(){
  const tipo = document.getElementById('fTipoMov').value;
  const list = tipo ? changelog.filter(e=>e.tipo===tipo) : changelog;
  const labels = {A:'ALTA',B:'BAJA',R:'ROTACIÓN',E:'EDICIÓN',M:'MASIVA',U:'REVERSIÓN'};
  const container = document.getElementById('clList');
  if(!list.length){ container.innerHTML='<div class="empty">No hay movimientos registrados aún.</div>'; return; }
  container.innerHTML = list.map(e=>`
    <div class="cli cl-${e.tipo}">
      <div style="display:flex;align-items:center;gap:10px">
        <span class="clt">[${labels[e.tipo]||e.tipo}]</span>
        <span class="cld">${e.fecha}</span>
      </div>
      <div class="cldesc">${e.desc}</div>
      ${e.det ? `<div class="cldet">${e.det}</div>` : ''}
      ${e.persona ? `<div class="cldet" style="color:var(--accent);font-weight:500">▸ ${e.persona}</div>` : ''}
    </div>`).join('');
}

// ===== NAV =====
function showPage(name, btn){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
  document.getElementById('page-'+name).classList.add('active');
  btn.classList.add('active');
  if(name==='vacantes') renderVacantes();
  if(name==='servicios') renderServicios();
  if(name==='changelog') renderChangelog();
}
function openModal(n){ document.getElementById('modal-'+n).classList.add('open'); }
function closeModal(n){ document.getElementById('modal-'+n).classList.remove('open'); }

// ===== ALTA =====
function saveAlta(){
  const g = id => document.getElementById(id).value.trim();
  const nom=g('a_nom'), ceco=g('a_ceco');
  if(!nom||!ceco){ alert('Nombre y CECO son obligatorios.'); return; }
  const uid = uidCounter++;
  data.push({POSICION:g('a_pos'),DESCRIPCION_POSICION:g('a_cargo'),ID_META_4:g('a_dni'),OBJETO_DE_IMPUTACION:ceco,DESCRIPCION_PERSONA:nom,GERENCIA_JEFATURA:g('a_serv'),NOMBRE_JEFE:g('a_jefe'),SOCIEDAD:g('a_soc'),FLAG_LICENCIA:g('a_flag'),WC_BC:g('a_wcbc'),ENCUADRE:'',_uid:uid});
  addCL('A',nom,`Alta: ${nom} en posición ${g('a_pos')||'(nueva)'} · CECO: ${ceco}`,g('a_obs')||`Serv: ${g('a_serv')}`);
  ['a_pos','a_dni','a_nom','a_ceco','a_serv','a_cargo','a_jefe','a_flag','a_obs'].forEach(id=>document.getElementById(id).value='');
  closeModal('alta'); updateStats(); renderPersonal(); renderVacantes(); renderServicios();
}

// ===== EDIT =====
function openEdit(idx){
  editIdx = idx;
  const r = data[idx];
  document.getElementById('editBody').innerHTML = `
    <div class="fr">
      <div class="fg"><label class="fl">Posición SAP</label><input class="finp" id="e_pos" value="${r.POSICION||''}"></div>
      <div class="fg"><label class="fl">DNI</label><input class="finp" id="e_dni" value="${r.ID_META_4||''}"></div>
    </div>
    <div class="fg"><label class="fl">Nombre y Apellido</label><input class="finp" id="e_nom" value="${(r.DESCRIPCION_PERSONA||'').replace(/"/g,'&quot;')}"></div>
    <div class="fr">
      <div class="fg"><label class="fl">CECO</label><input class="finp" id="e_ceco" value="${r.OBJETO_DE_IMPUTACION||''}" list="dlCeco"></div>
      <div class="fg"><label class="fl">Servicio</label><input class="finp" id="e_serv" value="${r.GERENCIA_JEFATURA||''}" list="dlServ"></div>
    </div>
    <div class="fg"><label class="fl">Cargo</label><input class="finp" id="e_cargo" value="${(r.DESCRIPCION_POSICION||'').replace(/"/g,'&quot;')}"></div>
    <div class="fr">
      <div class="fg"><label class="fl">Sociedad</label>
        <select class="finp" id="e_soc">
          <option ${r.SOCIEDAD==='Energy Field Services'?'selected':''}>Energy Field Services</option>
          <option ${r.SOCIEDAD==='TECPETROL S.A.'?'selected':''}>TECPETROL S.A.</option>
        </select>
      </div>
      <div class="fg"><label class="fl">WC / BC</label>
        <select class="finp" id="e_wcbc">
          <option value="WC" ${r.WC_BC==='WC'?'selected':''}>WC – Jerárquico</option>
          <option value="BC" ${r.WC_BC==='BC'?'selected':''}>BC – Petrolero</option>
        </select>
      </div>
    </div>
    <div class="fr">
      <div class="fg"><label class="fl">Jefe</label><input class="finp" id="e_jefe" value="${(r.NOMBRE_JEFE||'').replace(/"/g,'&quot;')}" list="dlJefe"></div>
      <div class="fg"><label class="fl">FLAG</label><input class="finp" id="e_flag" value="${r.FLAG_LICENCIA||''}"></div>
    </div>
    <div class="fg"><label class="fl">Observación del cambio</label><input class="finp" id="e_obs" placeholder="¿Por qué se edita?"></div>`;
  openModal('edit');
}
function saveEdit(){
  if(editIdx===null) return;
  const r = data[editIdx];
  pushSnap(r._uid, r);  // snapshot ANTES de modificar
  const g = id => { const el=document.getElementById(id); return el ? el.value.trim() : ''; };
  const np=g('e_pos'), nc=g('e_ceco'), ns=g('e_serv');
  const cambios=[];
  if(np && np!==r.POSICION) cambios.push(`Pos: ${r.POSICION}→${np}`);
  if(nc && nc!==r.OBJETO_DE_IMPUTACION) cambios.push(`CECO: ${r.OBJETO_DE_IMPUTACION}→${nc}`);
  if(ns && ns!==r.GERENCIA_JEFATURA) cambios.push(`Serv: ${r.GERENCIA_JEFATURA}→${ns}`);
  // apply
  if(np) r.POSICION=np;
  const nd=g('e_dni'); if(nd) r.ID_META_4=nd;
  const nn=g('e_nom'); if(nn) r.DESCRIPCION_PERSONA=nn;
  if(nc) r.OBJETO_DE_IMPUTACION=nc;
  if(ns) r.GERENCIA_JEFATURA=ns;
  const ncargo=g('e_cargo'); if(ncargo) r.DESCRIPCION_POSICION=ncargo;
  r.SOCIEDAD=g('e_soc')||r.SOCIEDAD;
  r.WC_BC=g('e_wcbc')||r.WC_BC;
  const nj=g('e_jefe'); if(nj) r.NOMBRE_JEFE=nj;
  const nf=g('e_flag'); if(nf) r.FLAG_LICENCIA=nf;
  addCL('E', r.DESCRIPCION_PERSONA, `Edición: ${r.DESCRIPCION_PERSONA}`, (cambios.length?cambios.join(' | '):'Cambios menores')+(g('e_obs')?` · ${g('e_obs')}` :''));
  editIdx=null; closeModal('edit'); updateStats(); renderPersonal(); renderVacantes(); renderServicios();
}

// ===== BAJA =====
function openBaja(idx){
  bajaIdx = idx;
  const r = data[idx];
  document.getElementById('b_per').value = r.DESCRIPCION_PERSONA||'';
  document.getElementById('b_pos').value = r.POSICION||'';
  document.getElementById('b_ceco').value = r.OBJETO_DE_IMPUTACION||'';
  document.getElementById('b_obs').value = '';
  openModal('baja');
}
function confirmarBaja(){
  if(bajaIdx===null) return;
  const r = data[bajaIdx];
  pushSnap(r._uid, r);  // snapshot antes de la baja
  const nom = r.DESCRIPCION_PERSONA;
  const motivo = document.getElementById('b_motivo').value;
  const obs = document.getElementById('b_obs').value.trim();
  addCL('B', nom, `Baja: ${nom} · Pos: ${r.POSICION}`, `Motivo: ${motivo} · CECO: ${r.OBJETO_DE_IMPUTACION} · Serv: ${r.GERENCIA_JEFATURA}`+(obs?` · ${obs}`:''));
  r.ID_META_4='';
  r.DESCRIPCION_PERSONA=`VACANTE (baja: ${nom})`;
  bajaIdx=null; closeModal('baja'); updateStats(); renderPersonal(); renderVacantes(); renderServicios();
}

// ===== ROTACIÓN =====
function openRot(idx){
  rotIdx = idx;
  const r = data[idx];
  document.getElementById('r_per').value = r.DESCRIPCION_PERSONA||'';
  document.getElementById('r_pos_from').value = r.POSICION||'';
  document.getElementById('r_ceco_from').value = r.OBJETO_DE_IMPUTACION||'';
  document.getElementById('r_serv_from').value = r.GERENCIA_JEFATURA||'';
  document.getElementById('r_jefe_from').value = r.NOMBRE_JEFE||'';
  ['r_pos_to','r_ceco_to','r_serv_to','r_jefe_to','r_obs'].forEach(id=>document.getElementById(id).value='');
  openModal('rot');
}
function saveRot(){
  if(rotIdx===null) return;
  const r = data[rotIdx];
  pushSnap(r._uid, r);  // snapshot antes de mover
  const g = id => document.getElementById(id).value.trim();
  const np=g('r_pos_to'), nc=g('r_ceco_to'), ns=g('r_serv_to'), nj=g('r_jefe_to');
  const cambios=[];
  if(np && np!==r.POSICION){ cambios.push(`Pos: ${r.POSICION}→${np}`); r.POSICION=np; }
  if(nc && nc!==r.OBJETO_DE_IMPUTACION){ cambios.push(`CECO: ${r.OBJETO_DE_IMPUTACION}→${nc}`); r.OBJETO_DE_IMPUTACION=nc; }
  if(ns && ns!==r.GERENCIA_JEFATURA){ cambios.push(`Serv: ${r.GERENCIA_JEFATURA}→${ns}`); r.GERENCIA_JEFATURA=ns; }
  if(nj && nj!==r.NOMBRE_JEFE){ cambios.push(`Jefe: ${r.NOMBRE_JEFE}→${nj}`); r.NOMBRE_JEFE=nj; }
  if(!cambios.length){ alert('No se detectaron cambios. Completá al menos un campo nuevo.'); return; }
  addCL('R', r.DESCRIPCION_PERSONA, `Movimiento: ${r.DESCRIPCION_PERSONA}`, cambios.join(' | ')+(g('r_obs')?` · ${g('r_obs')}`:''));
  rotIdx=null; closeModal('rot'); updateStats(); renderPersonal(); renderVacantes(); renderServicios();
}

// ===== REVERTIR =====
function revertir(idx){
  const r = data[idx];
  const uid = r._uid;
  if(!hasSnap(uid)){ alert('No hay versión anterior guardada para esta fila.'); return; }
  const nom = r.DESCRIPCION_PERSONA;
  if(!confirm(`¿Deshacer el último cambio en "${nom}"?
Esto restaurará el estado previo al último guardado.`)) return;
  const prev = popSnap(uid);
  if(!prev){ alert('Error al obtener el snapshot.'); return; }
  // restore all fields except _uid (keep the same uid)
  const myUid = r._uid;
  Object.keys(prev).forEach(k => { if(k !== '_uid') r[k] = prev[k]; });
  r._uid = myUid;
  addCL('U', r.DESCRIPCION_PERSONA, `Reversión: ${r.DESCRIPCION_PERSONA}`, 'Estado restaurado al anterior al último cambio guardado');
  updateStats(); renderPersonal(); renderVacantes(); renderServicios(); renderChangelog();
}

// ===== EDICIÓN MASIVA =====
function onMasivaFilterFieldChange(){
  const ff = document.getElementById('m_ff').value;
  const dl = document.getElementById('dlMF');
  dl.innerHTML = '';
  document.getElementById('m_fv').value = '';
  if(!ff) return;
  const vals = [...new Set(data.map(r=>(r[ff]||'')).filter(Boolean))].sort();
  vals.forEach(v=>{ const o=document.createElement('option'); o.value=v; dl.appendChild(o); });
  previewMasiva();
}
function onMasivaTargetFieldChange(){
  const tf = document.getElementById('m_tf').value;
  const dl = document.getElementById('dlMT');
  dl.innerHTML = '';
  document.getElementById('m_nv').value = '';
  if(!tf) return;
  const vals = [...new Set(data.map(r=>(r[tf]||'')).filter(Boolean))].sort();
  vals.forEach(v=>{ const o=document.createElement('option'); o.value=v; dl.appendChild(o); });
  previewMasiva();
}

function getMasivaMatches(){
  const ff = document.getElementById('m_ff').value;
  const fv = document.getElementById('m_fv').value.trim().toLowerCase();
  if(!ff) return [...data];  // todas las filas si no hay filtro
  if(!fv) return [];
  return data.filter(r => (r[ff]||'').toString().toLowerCase() === fv);
}

function previewMasiva(){
  const matches = getMasivaMatches();
  const tf = document.getElementById('m_tf').value;
  const nv = document.getElementById('m_nv').value.trim();
  const info = document.getElementById('m_info');
  const wrap = document.getElementById('m_preview');
  const btn  = document.getElementById('btnMasiva');

  if(!matches.length){
    info.textContent = document.getElementById('m_fv').value ? '0 filas coinciden con el filtro.' : 'Ingresá un valor de filtro.';
    wrap.innerHTML='<div class="empty">Sin coincidencias para el filtro.</div>';
    btn.disabled=true; return;
  }
  if(!tf || !nv){
    info.textContent = `${matches.length} fila${matches.length!==1?'s':''} coinciden. Elegí el campo a modificar y el valor nuevo.`;
    wrap.innerHTML='<div class="empty">Elegí el campo a modificar y el valor nuevo.</div>';
    btn.disabled=true; return;
  }

  info.textContent = `⚡ Se modificará "${tf}" en ${matches.length} fila${matches.length!==1?'s':''}.`;
  const show = matches.slice(0,25);
  wrap.innerHTML = `<table class="preview-table">
    <thead><tr><th>Persona</th><th>Posición</th><th>CECO</th><th>${tf} (actual)</th><th>Valor nuevo</th></tr></thead>
    <tbody>
      ${show.map(r=>`<tr class="ch">
        <td>${(r.DESCRIPCION_PERSONA||'—').substring(0,26)}</td>
        <td class="pos">${r.POSICION||'—'}</td>
        <td class="ceco">${r.OBJETO_DE_IMPUTACION||'—'}</td>
        <td>${(r[tf]||'—').toString().substring(0,28)}</td>
        <td class="new-val">${nv}</td>
      </tr>`).join('')}
      ${matches.length>25?`<tr><td colspan="5" style="text-align:center;padding:6px;color:var(--muted);font-size:11px">… y ${matches.length-25} filas más</td></tr>`:''}
    </tbody>
  </table>`;
  btn.disabled = false;
}

function aplicarMasiva(){
  const matches = getMasivaMatches();
  const tf = document.getElementById('m_tf').value;
  const nv = document.getElementById('m_nv').value.trim();
  const ff = document.getElementById('m_ff').value;
  const fv = document.getElementById('m_fv').value.trim();
  if(!tf || !nv || !matches.length){ alert('Faltan datos para aplicar el cambio.'); return; }
  if(!confirm(`¿Aplicar "${nv}" al campo "${tf}" en ${matches.length} fila(s)?`)) return;

  matches.forEach(r => {
    pushSnap(r._uid, r);  // snapshot individual para poder revertir
    r[tf] = nv;
  });

  addCL('M','(múltiples)',`Edición masiva: campo "${tf}" → "${nv}"`,`Filtro: ${ff||'Todas'}${fv?'='+fv:''} · ${matches.length} filas afectadas`);

  // reset form
  ['m_fv','m_nv'].forEach(id=>document.getElementById(id).value='');
  document.getElementById('m_ff').value='';
  document.getElementById('m_tf').value='';
  document.getElementById('m_info').textContent='';
  document.getElementById('m_preview').innerHTML='<div class="empty">Configurá el filtro y el campo destino para ver la previsualización.</div>';
  document.getElementById('btnMasiva').disabled=true;

  closeModal('masiva');
  updateStats(); renderPersonal(); renderVacantes(); renderServicios();
}

// ===== UPLOAD =====
function handleDrop(e){
  e.preventDefault();
  document.getElementById('dropzone').classList.remove('drag');
  const file = e.dataTransfer.files[0];
  if(file) processFile(file);
}
function handleFileUpload(file){ if(file) processFile(file); }

function processFile(file){
  const reader = new FileReader();
  reader.onload = function(e){
    try{
      const wb = XLSX.read(e.target.result, {type:'array'});
      const ws = wb.Sheets[wb.SheetNames[0]];
      const rows = XLSX.utils.sheet_to_json(ws, {defval:''});
      analyzeUpload(rows, file.name);
    } catch(err){
      document.getElementById('uploadResult').innerHTML=`<div class="alert al-r">Error al leer el archivo: ${err.message}</div>`;
    }
  };
  reader.readAsArrayBuffer(file);
}

function analyzeUpload(rows, fname){
  const norm = rows.map(r=>{ const o={}; Object.keys(r).forEach(k=>{ o[k.trim().toUpperCase().replace(/\s+/g,'_')]=String(r[k]||'').trim().replace(/\.0$/,''); }); return o; });
  const parsed = norm.map(r=>({
    POSICION: r.POSICION||'',
    ID_META_4: r.ID_META_4||'',
    DESCRIPCION_PERSONA: r.DESCRIPCION_PERSONA||'',
    OBJETO_DE_IMPUTACION: r.OBJETO_DE_IMPUTACION||'',
    GERENCIA_JEFATURA: r.GERENCIA_JEFATURA||'',
    NOMBRE_JEFE: r.NOMBRE_JEFE||'',
    SOCIEDAD: r.SOCIEDAD||'',
    FLAG_LICENCIA: r.FLAG_LICENCIA||'',
    WC_BC: r.WC_BC||'',
    DESCRIPCION_POSICION: r.DESCRIPCION_POSICION||''
  })).filter(r=>r.POSICION||r.ID_META_4||r.DESCRIPCION_PERSONA);

  const byPos={}, byDni={};
  data.forEach(r=>{ if(r.POSICION) byPos[r.POSICION]=r; if(r.ID_META_4&&!isVac(r)) byDni[r.ID_META_4]=r; });

  const newRows=[], updated=[], unchanged=[];
  parsed.forEach(nr=>{
    const existing = byPos[nr.POSICION] || byDni[nr.ID_META_4];
    if(!existing){ newRows.push(nr); return; }
    const diffs=[];
    ['OBJETO_DE_IMPUTACION','GERENCIA_JEFATURA','NOMBRE_JEFE','POSICION','WC_BC','SOCIEDAD'].forEach(f=>{
      if(nr[f] && nr[f]!==existing[f]) diffs.push({field:f, old:existing[f], nw:nr[f]});
    });
    if(diffs.length) updated.push({existing,nr,diffs});
    else unchanged.push(nr);
  });

  uploadPending = {newRows, updated, unchanged};

  document.getElementById('uploadResult').innerHTML=`
    <div class="upload-result">
      <div class="ur-row"><span class="ur-label">Archivo</span><span class="ur-val">${fname}</span></div>
      <div class="ur-row"><span class="ur-label">Filas leídas</span><span class="ur-val">${parsed.length}</span></div>
      <div class="ur-row"><span class="ur-label" style="color:var(--success)">Filas nuevas</span><span class="ur-val" style="color:var(--success)">${newRows.length}</span></div>
      <div class="ur-row"><span class="ur-label" style="color:var(--warn)">Con cambios detectados</span><span class="ur-val" style="color:var(--warn)">${updated.length}</span></div>
      <div class="ur-row"><span class="ur-label">Sin cambios</span><span class="ur-val">${unchanged.length}</span></div>
    </div>`;

  const show = [...newRows.slice(0,8).map(r=>({...r,_t:'NUEVA',_d:[]})), ...updated.slice(0,8).map(u=>({...u.nr,_t:'CAMBIO',_d:u.diffs}))];
  const prev = document.getElementById('uploadPreview');
  prev.style.display = show.length ? 'block' : 'none';
  prev.innerHTML = show.length ? `<table class="preview-table">
    <thead><tr><th>Tipo</th><th>Persona</th><th>Posición</th><th>Cambios</th></tr></thead>
    <tbody>${show.map(r=>`<tr class="${r._t==='NUEVA'?'ch':''}">
      <td><span class="tag ${r._t==='NUEVA'?'tg':'ty'}">${r._t}</span></td>
      <td>${(r.DESCRIPCION_PERSONA||'—').substring(0,26)}</td>
      <td class="pos">${r.POSICION||'—'}</td>
      <td style="color:var(--warn);font-size:10px">${r._d.map(d=>`${d.field}: ${d.old}→${d.nw}`).join(' | ')||'—'}</td>
    </tr>`).join('')}</tbody>
  </table>` : '';

  document.getElementById('btnApplyUpload').style.display = (newRows.length||updated.length) ? 'inline-flex' : 'none';
}

function applyUpload(){
  if(!uploadPending) return;
  const {newRows, updated} = uploadPending;
  updated.forEach(({existing,nr,diffs})=>{
    pushSnap(existing._uid, existing);
    diffs.forEach(d=>{ existing[d.field]=d.nw; });
  });
  newRows.forEach(nr=>{
    data.push({...nr, _uid: uidCounter++, ENCUADRE:''});
  });
  addCL('M','(carga Excel)',`Carga masiva: ${newRows.length} nuevas + ${updated.length} actualizadas`,`Total procesadas: ${newRows.length+updated.length}`);
  uploadPending=null;
  closeModal('upload');
  document.getElementById('uploadResult').innerHTML='';
  document.getElementById('uploadPreview').style.display='none';
  document.getElementById('btnApplyUpload').style.display='none';
  document.getElementById('fileInput').value='';
  updateStats(); renderPersonal(); renderVacantes(); renderServicios();
}

// ===== EXPORT =====
function exportCSV(){
  const f = getFiltered();
  const hdrs = ['POSICION','DESCRIPCION_PERSONA','ID_META_4','OBJETO_DE_IMPUTACION','DESCRIPCION_POSICION','GERENCIA_JEFATURA','NOMBRE_JEFE','WC_BC','SOCIEDAD','FLAG_LICENCIA'];
  const rows = [hdrs.join(',')];
  f.forEach(r=>rows.push(hdrs.map(h=>`"${(r[h]||'').toString().replace(/"/g,'""')}"`).join(',')));
  dlFile('EFiS_Estructura_'+new Date().toISOString().slice(0,10)+'.csv', rows.join('\n'));
}
function exportChangelogCSV(){
  const hdrs=['fecha','tipo','persona','desc','det'];
  const rows=[hdrs.join(',')];
  changelog.forEach(e=>rows.push(hdrs.map(h=>`"${(e[h]||'').replace(/"/g,'""')}"`).join(',')));
  dlFile('EFiS_Movimientos_'+new Date().toISOString().slice(0,10)+'.csv', rows.join('\n'));
}
function dlFile(name, content){
  const a=document.createElement('a');
  a.href='data:text/csv;charset=utf-8,\uFEFF'+encodeURIComponent(content);
  a.download=name; a.click();
}

init();
</script>
</body>
</html>
