<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-title" content="Belle's Honey">
<title>Belle's Honey — Hive Inspections</title>
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;500&family=IBM+Plex+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent}
:root{
  --amber:#BA7517;--amber-l:#FAEEDA;--amber-d:#633806;
  --green:#3B6D11;--green-l:#C0DD97;
  --red:#A32D2D;--red-l:#F7C1C1;
  --blue:#185FA5;--blue-l:#B5D4F4;
  --bg:#FFFDF7;--surf:#FFFFFF;--surf2:#F5F3EE;
  --border:#D3D1C7;--border2:#B4B2A9;
  --text:#2C2C2A;--text2:#5F5E5A;--muted:#888780;
  --pill-bg:#FFFFFF;--pill-text:#2C2C2A;
  --btn-bg:#FFFFFF;--btn-text:#2C2C2A;
  --score-bg:#F5F3EE;--input-bg:#FFFFFF;--mbox-bg:#F1EFE8;
  --tag-g-bg:#EAF3DE;--tag-g-txt:#3B6D11;
  --tag-y-bg:#FAEEDA;--tag-y-txt:#633806;
  --tag-r-bg:#FCEBEB;--tag-r-txt:#A32D2D;
  --tag-b-bg:#E6F1FB;--tag-b-txt:#185FA5;
  --tag-x-bg:#F1EFE8;--tag-x-txt:#5F5E5A;
}
@media(prefers-color-scheme:dark){
  :root{
    --amber:#FAC775;--amber-l:#2d2010;--amber-d:#FAC775;
    --green:#C0DD97;--green-l:#162008;
    --red:#F09595;--red-l:#2a1010;
    --blue:#85B7EB;--blue-l:#042C53;
    --bg:#1A1917;--surf:#252320;--surf2:#2E2C28;
    --border:#3a3835;--border2:#4a4845;
    --text:#F0EDE4;--text2:#B4B2A9;--muted:#6a6865;
    --pill-bg:#2E2C28;--pill-text:#F0EDE4;
    --btn-bg:#2E2C28;--btn-text:#F0EDE4;
    --score-bg:#2E2C28;--input-bg:#252320;--mbox-bg:#2E2C28;
    --tag-g-bg:#162008;--tag-g-txt:#C0DD97;
    --tag-y-bg:#2d2010;--tag-y-txt:#FAC775;
    --tag-r-bg:#2a1010;--tag-r-txt:#F09595;
    --tag-b-bg:#042C53;--tag-b-txt:#85B7EB;
    --tag-x-bg:#2E2C28;--tag-x-txt:#B4B2A9;
  }
}
body{font-family:'IBM Plex Sans',system-ui,sans-serif;background:var(--bg);color:var(--text);font-size:15px;line-height:1.5;min-height:100vh}
#app{max-width:480px;margin:0 auto;padding-bottom:80px}
.hdr{background:var(--surf);border-bottom:1px solid var(--border);padding:13px 16px;position:sticky;top:0;z-index:50;display:flex;align-items:center;justify-content:space-between}
.hdr-title{font-family:'IBM Plex Mono',monospace;font-size:14px;font-weight:500;color:var(--amber);letter-spacing:.03em}
.hdr-sub{font-size:11px;color:var(--muted);font-family:'IBM Plex Mono',monospace}
.tabs{display:flex;background:var(--surf);border-bottom:1px solid var(--border)}
.tab{flex:1;padding:11px 8px;text-align:center;font-size:13px;font-weight:500;color:var(--muted);border:none;background:none;cursor:pointer;border-bottom:2px solid transparent}
.tab.on{color:var(--amber);border-bottom-color:var(--amber)}
.scr{display:none;padding:16px}.scr.on{display:block}
.slbl{font-family:'IBM Plex Mono',monospace;font-size:11px;font-weight:500;color:var(--muted);letter-spacing:.08em;text-transform:uppercase;margin:0 0 8px}
.card{background:var(--surf);border:1px solid var(--border);border-radius:10px;padding:14px 16px;margin-bottom:12px}
.card-t{font-weight:500;font-size:14px;margin-bottom:14px;color:var(--text)}
.hcard{background:var(--surf);border:1px solid var(--border);border-radius:10px;padding:14px 16px;display:flex;align-items:center;justify-content:space-between;cursor:pointer;margin-bottom:10px}
.hcard.sel{border-color:var(--amber);background:var(--amber-l)}
.hcard-name{font-weight:500;font-size:15px;color:var(--text)}
.hcard-meta{font-size:12px;color:var(--muted);margin-top:2px}
.dot{width:12px;height:12px;border-radius:50%;flex-shrink:0;margin-left:12px}
.dot-g{background:#639922}.dot-y{background:#EF9F27}.dot-r{background:#E24B4A}.dot-x{background:var(--border2)}
.stats{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-bottom:16px}
.stat{background:var(--surf);border:1px solid var(--border);border-radius:10px;padding:10px 12px;text-align:center}
.stat-n{font-family:'IBM Plex Mono',monospace;font-size:22px;font-weight:500;color:var(--amber)}
.stat-l{font-size:11px;color:var(--muted);margin-top:2px}
.btn{display:flex;align-items:center;justify-content:center;padding:11px 18px;border-radius:10px;font-family:'IBM Plex Sans',sans-serif;font-size:14px;font-weight:500;cursor:pointer;border:1px solid var(--border2);background:var(--btn-bg);color:var(--btn-text);width:100%;margin-bottom:8px}
.btn-p{background:var(--amber);border-color:var(--amber);color:#1A1510}
.btn-d{border-color:var(--red);color:var(--red);background:transparent}
.btn-s{background:var(--green);border-color:var(--green);color:#0A1A03}
.btn-sm{padding:7px 14px;font-size:13px;width:auto;margin-bottom:0}
.btn-row{display:flex;gap:8px;margin-top:20px}
.btn-row .btn{margin-bottom:0;flex:1}
.fg{margin-bottom:16px}.fg:last-child{margin-bottom:0}
label{display:block;font-size:13px;font-weight:500;color:var(--muted);margin-bottom:6px}
input[type=text],input[type=date],input[type=number],select,textarea{width:100%;padding:10px 12px;border:1px solid var(--border);border-radius:10px;font-family:inherit;font-size:15px;color:var(--text);background:var(--input-bg);-webkit-appearance:none;appearance:none;outline:none}
input:focus,select:focus,textarea:focus{border-color:var(--amber)}
textarea{resize:vertical;min-height:76px}
select{background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='8' viewBox='0 0 12 8'%3E%3Cpath d='M1 1l5 5 5-5' stroke='%23888780' stroke-width='1.5' fill='none' stroke-linecap='round'/%3E%3C/svg%3E");background-repeat:no-repeat;background-position:right 12px center;padding-right:36px}
.pills{display:flex;gap:7px;flex-wrap:wrap}
.pill{padding:7px 13px;border:1px solid var(--border2);border-radius:20px;font-size:13px;cursor:pointer;background:var(--pill-bg);color:var(--pill-text);user-select:none;font-family:inherit}
.pill.on{background:var(--amber);border-color:var(--amber);color:#1A1510}
.pill-sm{padding:6px 10px;font-size:12px}
.srow{display:flex;gap:6px}
.sbtn{flex:1;padding:10px 4px;border:1px solid var(--border2);border-radius:10px;font-size:13px;font-weight:500;text-align:center;cursor:pointer;background:var(--score-bg);color:var(--text);user-select:none;font-family:inherit}
.sbtn.sg{background:var(--tag-g-bg);border-color:var(--green);color:var(--green)}
.sbtn.sy{background:var(--tag-y-bg);border-color:var(--amber);color:var(--amber-d)}
.sbtn.sr{background:var(--tag-r-bg);border-color:var(--red);color:var(--red)}
.trow{display:flex;align-items:center;justify-content:space-between;padding:10px 0;border-bottom:1px solid var(--border)}
.trow:last-child{border-bottom:none}
.trow-lbl{font-size:15px;color:var(--text)}
.tog{position:relative;width:44px;height:26px;flex-shrink:0}
.tog input{opacity:0;width:0;height:0}
.tog-tr{position:absolute;inset:0;background:var(--border2);border-radius:13px;cursor:pointer;transition:background .2s}
.tog input:checked+.tog-tr{background:var(--amber)}
.tog-tr::after{content:'';position:absolute;top:3px;left:3px;width:20px;height:20px;border-radius:50%;background:#fff;transition:transform .2s}
.tog input:checked+.tog-tr::after{transform:translateX(18px)}
.tags{display:flex;flex-wrap:wrap;gap:4px;margin-top:6px}
.tag{font-size:11px;padding:3px 8px;border-radius:10px;font-family:'IBM Plex Mono',monospace}
.tag-g{background:var(--tag-g-bg);color:var(--tag-g-txt)}
.tag-y{background:var(--tag-y-bg);color:var(--tag-y-txt)}
.tag-r{background:var(--tag-r-bg);color:var(--tag-r-txt)}
.tag-b{background:var(--tag-b-bg);color:var(--tag-b-txt)}
.tag-x{background:var(--tag-x-bg);color:var(--tag-x-txt)}
.iitem{background:var(--surf);border:1px solid var(--border);border-radius:10px;padding:12px 14px;margin-bottom:8px;cursor:pointer}
.iitem-hdr{display:flex;justify-content:space-between;align-items:flex-start}
.iitem-hive{font-weight:500;font-size:14px;color:var(--text)}
.iitem-date{font-family:'IBM Plex Mono',monospace;font-size:12px;color:var(--muted)}
.iitem-note{font-size:13px;color:var(--muted);margin-top:3px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.mbox{display:none;margin-top:4px;margin-bottom:12px;padding:12px;border-radius:10px;border:1px solid var(--border);background:var(--mbox-bg)}
.mbox-rate{font-family:'IBM Plex Mono',monospace;font-size:24px;font-weight:500;color:var(--text)}
.mbox-unit{font-size:13px;color:var(--muted);margin-left:4px}
.mbox-lbl{display:inline-block;font-size:12px;font-weight:500;padding:3px 9px;border-radius:8px;margin-left:8px;font-family:'IBM Plex Mono',monospace}
.mbox-note{font-size:12px;color:var(--muted);margin-top:5px}
.overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,.55);z-index:200;overflow-y:auto;padding:20px 12px;align-items:flex-start;justify-content:center}
.overlay.on{display:flex}
.modal{background:var(--bg);border-radius:14px;width:100%;max-width:460px;padding:20px 16px 28px;border:1px solid var(--border)}
.modal-hdr{display:flex;align-items:center;justify-content:space-between;margin-bottom:18px}
.modal-t{font-family:'IBM Plex Mono',monospace;font-size:14px;font-weight:500;color:var(--amber)}
.modal-x{background:none;border:none;font-size:22px;cursor:pointer;color:var(--muted);line-height:1;padding:4px}
.dtbl{width:100%;border-collapse:collapse;font-size:14px}
.dtbl td{padding:6px 0;vertical-align:top;color:var(--text)}
.dtbl .k{color:var(--muted);font-size:13px;width:44%}
.dtbl .v{font-weight:500}
.sub{display:none;margin-top:10px;padding-top:12px;border-top:1px solid var(--border)}
.sub.on{display:block}
.fab{position:fixed;bottom:20px;right:20px;width:56px;height:56px;border-radius:50%;background:var(--amber);color:#1A1510;font-size:28px;display:flex;align-items:center;justify-content:center;cursor:pointer;border:none;z-index:100;box-shadow:0 2px 12px rgba(0,0,0,.3);font-weight:300;line-height:1}
.empty{text-align:center;padding:40px 20px;color:var(--muted)}
.empty-i{font-size:36px;margin-bottom:10px}
hr.div{border:none;border-top:1px solid var(--border);margin:4px 0 16px}
 
/* ── Edit button ── */
.edit-btn{background:none;border:1px solid var(--border2);border-radius:8px;color:var(--muted);font-size:15px;padding:4px 8px;cursor:pointer;flex-shrink:0;margin-left:6px;line-height:1}
.edit-btn:active{background:var(--surf2)}
 
/* ── Splits ── */
.split-item{background:var(--surf);border:1px solid var(--border);border-radius:10px;padding:12px 14px;margin-bottom:10px;cursor:pointer}
.split-hdr{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:6px}
.split-title{font-weight:500;font-size:14px;color:var(--text)}
.split-date{font-family:'IBM Plex Mono',monospace;font-size:12px;color:var(--muted)}
.split-meta{font-size:13px;color:var(--muted);margin-top:2px}
.split-source-badge{display:inline-block;font-size:11px;padding:3px 8px;border-radius:10px;font-family:'IBM Plex Mono',monospace;margin-top:5px;background:var(--blue-l);color:var(--blue)}
 
/* ── Lineage tree ── */
.lineage-node{padding:10px 12px;border-radius:10px;border:1px solid var(--border);background:var(--surf);margin-bottom:6px;position:relative}
.lineage-node.current{border-color:var(--amber);background:var(--amber-l)}
.lineage-node.ancestor{border-color:var(--blue);background:var(--blue-l)}
.lineage-node.descendant{border-color:var(--green);background:var(--green-l)}
.lineage-connector{width:2px;height:14px;background:var(--border2);margin:0 auto 0 20px}
.lineage-label{font-size:10px;font-family:'IBM Plex Mono',monospace;color:var(--muted);text-transform:uppercase;letter-spacing:.06em;margin-bottom:4px}
.lineage-name{font-weight:500;font-size:14px;color:var(--text)}
.lineage-detail{font-size:12px;color:var(--muted);margin-top:2px}
.qcolor-swatch{display:flex;flex-direction:column;align-items:center;gap:5px;cursor:pointer;padding:6px 8px;border-radius:10px;border:2px solid transparent;transition:border-color .15s;user-select:none;-webkit-tap-highlight-color:transparent}
.qcolor-swatch.on{border-color:var(--amber) !important;background:var(--amber-l)}
.qcolor-dot{width:32px;height:32px;border-radius:50%;display:block;box-shadow:0 1px 3px rgba(0,0,0,.2)}
.qcolor-lbl{font-size:11px;font-weight:500;color:var(--text);font-family:'IBM Plex Mono',monospace}
 
/* ── Photo styles ── */
.photo-upload-area{border:2px dashed var(--border2);border-radius:10px;padding:20px;text-align:center;cursor:pointer;transition:border-color .15s;margin-bottom:10px;background:var(--surf2)}
.photo-upload-area:active{border-color:var(--amber)}
.photo-upload-icon{font-size:28px;margin-bottom:6px}
.photo-upload-txt{font-size:13px;color:var(--muted)}
.photo-upload-txt strong{color:var(--amber);font-weight:500}
.photo-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-top:10px}
.photo-thumb-wrap{position:relative;aspect-ratio:1;border-radius:8px;overflow:hidden;background:var(--surf2)}
.photo-thumb{width:100%;height:100%;object-fit:cover;display:block;cursor:pointer}
.photo-thumb-del{position:absolute;top:4px;right:4px;width:22px;height:22px;border-radius:50%;background:rgba(0,0,0,.65);color:#fff;border:none;font-size:14px;line-height:1;cursor:pointer;display:flex;align-items:center;justify-content:center}
.photo-thumb-lbl{position:absolute;bottom:0;left:0;right:0;background:rgba(0,0,0,.55);color:#fff;font-size:10px;padding:3px 5px;font-family:'IBM Plex Mono',monospace;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.photo-count-tag{font-size:11px;padding:3px 8px;border-radius:10px;font-family:'IBM Plex Mono',monospace;background:var(--blue-l);color:var(--blue-l);background:var(--tag-b-bg);color:var(--tag-b-txt);display:inline-block}
 
/* Photo lightbox */
.lightbox{display:none;position:fixed;inset:0;background:rgba(0,0,0,.92);z-index:500;align-items:center;justify-content:center;flex-direction:column}
.lightbox.on{display:flex}
.lightbox-img{max-width:95vw;max-height:80vh;object-fit:contain;border-radius:8px}
.lightbox-cap{color:#fff;font-size:13px;margin-top:12px;opacity:.75;font-family:'IBM Plex Mono',monospace}
.lightbox-close{position:absolute;top:16px;right:20px;background:none;border:none;color:#fff;font-size:30px;cursor:pointer;opacity:.8;line-height:1}
.lightbox-nav{display:flex;gap:16px;margin-top:14px}
.lightbox-nav button{background:rgba(255,255,255,.15);border:none;color:#fff;padding:8px 20px;border-radius:20px;font-size:14px;cursor:pointer}
 
/* Photo grid in detail modal */
.detail-photo-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:8px;margin-top:8px}
.detail-photo-wrap{position:relative;aspect-ratio:4/3;border-radius:8px;overflow:hidden;cursor:pointer}
.detail-photo{width:100%;height:100%;object-fit:cover}
.detail-photo-lbl{position:absolute;bottom:0;left:0;right:0;background:rgba(0,0,0,.6);color:#fff;font-size:10px;padding:4px 6px;font-family:'IBM Plex Mono',monospace}
</style>
</head>
<body>
<div id="app">
  <div class="hdr">
    <div style="display:flex;align-items:center;gap:10px">
      <img src="data:image/jpeg;base64,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" alt="Belle's Bees" style="height:42px;width:42px;object-fit:cover;border-radius:6px">
      <div><div class="hdr-title">Belle's Honey</div><div class="hdr-sub">hive inspection log</div></div>
    </div>
    <button class="btn btn-sm" style="width:auto;margin-bottom:0" onclick="UI.showExport()">Export CSV</button>
  </div>
  <div class="tabs">
    <button class="tab on" onclick="UI.tab('hives',this)">Hives</button>
    <button class="tab" onclick="UI.tab('yards',this)">Yards</button>
    <button class="tab" onclick="UI.tab('log',this)">Log</button>
    <button class="tab" onclick="UI.tab('splits',this)">Splits</button>
    <button class="tab" onclick="UI.tab('history',this)">History</button>
  </div>
 
  <div id="scr-hives" class="scr on">
    <div class="stats" id="stats"></div>
    <div class="slbl">Your hives</div>
    <div id="hive-list"></div>
    <button class="btn" onclick="UI.openAddHive()">+ Add hive</button>
  </div>
 
  <div id="scr-yards" class="scr">
    <div class="slbl">Your yards</div>
    <div id="yard-list"></div>
    <button class="btn" onclick="UI.openAddYard()">+ Add yard</button>
  </div>
 
  <div id="scr-splits" class="scr">
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:12px">
      <div class="slbl" style="margin:0">Split log</div>
      <button class="btn btn-sm btn-p" style="margin:0" onclick="UI.openAddSplit()">+ Log split</button>
    </div>
    <div id="split-list"></div>
  </div>
 
  <div id="scr-log" class="scr">
    <div class="slbl">Select hive to inspect</div>
    <div id="log-hives"></div>
    <div id="log-form"></div>
  </div>
 
  <div id="scr-history" class="scr">
    <div style="display:flex;gap:8px;margin-bottom:12px">
      <select id="hist-filter-yard" onchange="UI.renderHistory()" style="flex:1"><option value="">All yards</option></select>
      <select id="hist-filter" onchange="UI.renderHistory()" style="flex:1"><option value="">All hives</option></select>
    </div>
    <div id="hist-list"></div>
  </div>
</div>
 
<button class="fab" onclick="UI.tab('log',document.querySelectorAll('.tab')[2])">+</button>
 
<!-- ADD HIVE -->
<div class="overlay" id="m-add">
  <div class="modal">
    <div class="modal-hdr"><span class="modal-t">Add hive</span><button class="modal-x" onclick="UI.closeModal('m-add')">×</button></div>
    <div class="fg"><label>Hive name / number</label><input type="text" id="new-name" placeholder="e.g. Hive 3, South Yard #1"></div>
    <div class="fg"><label>Yard</label><select id="new-yard"><option value="">No yard assigned</option></select></div>
    <div class="fg"><label>Location / notes</label><input type="text" id="new-loc" placeholder="e.g. Back orchard, Langstroth 10-frame"></div>
    <div class="btn-row">
      <button class="btn" onclick="UI.closeModal('m-add')">Cancel</button>
      <button class="btn btn-p" onclick="UI.saveHive()">Add hive</button>
    </div>
  </div>
</div>
 
<!-- EDIT HIVE -->
<div class="overlay" id="m-edit-hive">
  <div class="modal">
    <div class="modal-hdr"><span class="modal-t">Edit hive</span><button class="modal-x" onclick="UI.closeModal('m-edit-hive')">×</button></div>
    <div class="fg"><label>Hive name / number</label><input type="text" id="edit-hive-name" placeholder="e.g. Hive 3"></div>
    <div class="fg"><label>Yard</label><select id="edit-hive-yard"><option value="">No yard assigned</option></select></div>
    <div class="fg"><label>Location / notes</label><input type="text" id="edit-hive-loc" placeholder="e.g. Back orchard, Langstroth 10-frame"></div>
    <div class="btn-row">
      <button class="btn" onclick="UI.closeModal('m-edit-hive')">Cancel</button>
      <button class="btn btn-p" onclick="UI.saveEditHive()">Save changes</button>
    </div>
  </div>
</div>
 
<!-- ADD YARD -->
<div class="overlay" id="m-add-yard">
  <div class="modal">
    <div class="modal-hdr"><span class="modal-t">Add yard</span><button class="modal-x" onclick="UI.closeModal('m-add-yard')">×</button></div>
    <div class="fg"><label>Yard name</label><input type="text" id="new-yard-name" placeholder="e.g. Back Yard, South Yard, Orchard"></div>
    <div class="fg"><label>Location / notes</label><input type="text" id="new-yard-loc" placeholder="e.g. 48 hives, behind barn"></div>
    <div class="btn-row">
      <button class="btn" onclick="UI.closeModal('m-add-yard')">Cancel</button>
      <button class="btn btn-p" onclick="UI.saveYard()">Add yard</button>
    </div>
  </div>
</div>
 
<!-- EDIT YARD -->
<div class="overlay" id="m-edit-yard">
  <div class="modal">
    <div class="modal-hdr"><span class="modal-t">Edit yard</span><button class="modal-x" onclick="UI.closeModal('m-edit-yard')">×</button></div>
    <div class="fg"><label>Yard name</label><input type="text" id="edit-yard-name" placeholder="e.g. Back Yard"></div>
    <div class="fg"><label>Location / notes</label><input type="text" id="edit-yard-loc" placeholder="e.g. 48 hives, behind barn"></div>
    <div class="btn-row">
      <button class="btn btn-d btn-sm" onclick="UI.deleteYard()">Delete yard</button>
      <button class="btn btn-p" onclick="UI.saveEditYard()" style="flex:2">Save changes</button>
    </div>
  </div>
</div>
 
<!-- LOG SPLIT -->
<div class="overlay" id="m-add-split">
  <div class="modal">
    <div class="modal-hdr"><span class="modal-t">Log split</span><button class="modal-x" onclick="UI.closeModal('m-add-split')">×</button></div>
    <div class="fg"><label>Date</label><input type="date" id="split-date"></div>
    <div class="fg"><label>Parent colony <span style="font-size:11px;color:var(--muted);font-weight:400">— hive being split</span></label><select id="split-parent"><option value="">Select parent colony…</option></select></div>
    <div class="fg"><label>Daughter colony <span style="font-size:11px;color:var(--muted);font-weight:400">— new hive created</span></label><select id="split-daughter"><option value="">Select daughter colony…</option></select></div>
    <div class="fg"><label>Queen source</label>
      <div class="pills" id="pg-qsource" style="flex-wrap:wrap;gap:6px">
        <div class="pill pill-sm" onclick="pickPill(this,'pg-qsource');showSplitSource()">Walk-away</div>
        <div class="pill pill-sm" onclick="pickPill(this,'pg-qsource');showSplitSource()">Queen cells from parent</div>
        <div class="pill pill-sm" onclick="pickPill(this,'pg-qsource');showSplitSource()">Grafted</div>
        <div class="pill pill-sm" onclick="pickPill(this,'pg-qsource');showSplitSource()">Mated from own yard</div>
        <div class="pill pill-sm" onclick="pickPill(this,'pg-qsource');showSplitSource()">Purchased queen</div>
      </div>
    </div>
    <div id="split-source-detail" style="display:none">
      <div class="fg" id="split-source-hive-wrap">
        <label id="split-source-hive-lbl">Source colony <span style="font-size:11px;color:var(--muted);font-weight:400">— colony that provided genetics</span></label>
        <select id="split-source-hive"><option value="">Select colony…</option></select>
      </div>
      <div class="fg" id="split-purchased-wrap" style="display:none">
        <label>Queen source / supplier</label>
        <input type="text" id="split-purchased-src" placeholder="e.g. Mann Lake, local breeder, VSH line">
      </div>
    </div>
    <div class="fg"><label>Parent queen action <span style="font-size:11px;color:var(--muted);font-weight:400">— what happened to the original queen</span></label>
      <div class="pills" id="pg-parent-queen">
        <div class="pill pill-sm" onclick="pickPill(this,'pg-parent-queen')">Stayed in parent</div>
        <div class="pill pill-sm" onclick="pickPill(this,'pg-parent-queen')">Went with split</div>
        <div class="pill pill-sm" onclick="pickPill(this,'pg-parent-queen')">Removed</div>
        <div class="pill pill-sm" onclick="pickPill(this,'pg-parent-queen')">Unknown</div>
      </div>
    </div>
    <div class="fg"><label>Notes</label><textarea id="split-notes" placeholder="Frame count, condition of split, follow-up needed…" style="min-height:60px"></textarea></div>
    <div class="btn-row">
      <button class="btn" onclick="UI.closeModal('m-add-split')">Cancel</button>
      <button class="btn btn-p" onclick="UI.saveSplit()">Save split</button>
    </div>
  </div>
</div>
 
<!-- SPLIT DETAIL -->
<div class="overlay" id="m-split-detail">
  <div class="modal">
    <div class="modal-hdr"><span class="modal-t" id="m-split-t">Split detail</span><button class="modal-x" onclick="UI.closeModal('m-split-detail')">×</button></div>
    <div id="m-split-body"></div>
    <div class="btn-row" style="margin-top:16px">
      <button class="btn btn-d btn-sm" onclick="UI.deleteSplit()">Delete</button>
      <button class="btn btn-sm" onclick="UI.closeModal('m-split-detail')">Close</button>
    </div>
  </div>
</div>
 
<!-- LINEAGE TREE -->
<div class="overlay" id="m-lineage">
  <div class="modal">
    <div class="modal-hdr"><span class="modal-t" id="m-lineage-t">Queen lineage</span><button class="modal-x" onclick="UI.closeModal('m-lineage')">×</button></div>
    <div id="m-lineage-body"></div>
    <div class="btn-row" style="margin-top:16px">
      <button class="btn" onclick="UI.closeModal('m-lineage')">Close</button>
    </div>
  </div>
</div>
 
<!-- DETAIL -->
<div class="overlay" id="m-detail">
  <div class="modal">
    <div class="modal-hdr"><span class="modal-t" id="m-detail-t">Detail</span><button class="modal-x" onclick="UI.closeModal('m-detail')">×</button></div>
    <div id="m-detail-body"></div>
    <div class="btn-row" style="margin-top:16px">
      <button class="btn btn-d btn-sm" id="m-detail-del" onclick="UI.deleteItem()">Delete</button>
      <button class="btn btn-sm" onclick="UI.closeModal('m-detail')">Close</button>
    </div>
  </div>
</div>
 
<!-- EXPORT -->
<div class="overlay" id="m-export">
  <div class="modal">
    <div class="modal-hdr"><span class="modal-t">Export CSV</span><button class="modal-x" onclick="UI.closeModal('m-export')">×</button></div>
    <p style="font-size:14px;color:var(--muted);margin-bottom:14px">Download all inspections for Excel or Google Sheets.</p>
    <div class="fg"><label>Filter by hive</label><select id="exp-filter"><option value="">All hives</option></select></div>
    <div class="btn-row">
      <button class="btn" onclick="UI.closeModal('m-export')">Cancel</button>
      <button class="btn btn-s" onclick="UI.doExport()">Download CSV</button>
    </div>
  </div>
</div>
 
<!-- LIGHTBOX -->
<div class="lightbox" id="lightbox" onclick="Photos.closeLightbox()">
  <button class="lightbox-close" onclick="Photos.closeLightbox()">×</button>
  <img class="lightbox-img" id="lb-img" src="" alt="">
  <div class="lightbox-cap" id="lb-cap"></div>
  <div class="lightbox-nav" onclick="event.stopPropagation()">
    <button onclick="Photos.lbNav(-1)">← Prev</button>
    <button onclick="Photos.lbNav(1)">Next →</button>
  </div>
</div>
 
<script>
// ── Storage ───────────────────────────────────────────────────────────────────
const DB={
  hives(){try{return JSON.parse(localStorage.getItem('bh_hives'))||[];}catch{return[];}},
  insps(){try{return JSON.parse(localStorage.getItem('bh_insps'))||[];}catch{return[];}},
  yards(){try{return JSON.parse(localStorage.getItem('bh_yards'))||[];}catch{return[];}},
  splits(){try{return JSON.parse(localStorage.getItem('bh_splits'))||[];}catch{return[];}},
  setHives(v){localStorage.setItem('bh_hives',JSON.stringify(v));},
  setInsps(v){localStorage.setItem('bh_insps',JSON.stringify(v));},
  setYards(v){localStorage.setItem('bh_yards',JSON.stringify(v));},
  setSplits(v){localStorage.setItem('bh_splits',JSON.stringify(v));},
};
 
// ── Photo storage — kept separate to avoid hitting localStorage size limits ──
// Photos stored as: bh_photos_{inspId} = [{id, label, dataUrl}]
const PhotoDB={
  get(inspId){try{return JSON.parse(localStorage.getItem('bh_photos_'+inspId))||[];}catch{return[];}},
  set(inspId,arr){
    try{localStorage.setItem('bh_photos_'+inspId,JSON.stringify(arr));}
    catch(e){
      if(e.name==='QuotaExceededError'){
        alert('Storage full — photo not saved. Try taking fewer or smaller photos.');
      }
    }
  },
  del(inspId){localStorage.removeItem('bh_photos_'+inspId);},
  count(inspId){return this.get(inspId).length;},
};
 
// ── Photo labels ──────────────────────────────────────────────────────────────
const PHOTO_LABELS = ['Queen','Brood pattern','Queen cells','Varroa wash','Honey stores','Equipment','Other'];
 
// ── In-memory staging for current inspection form ─────────────────────────────
let stagedPhotos = []; // [{id, label, dataUrl}]
 
// ── Photo module ──────────────────────────────────────────────────────────────
const Photos = {
  lbPhotos: [],
  lbIdx: 0,
 
  // Compress image to reasonable size for localStorage
  compress(file, cb) {
    const reader = new FileReader();
    reader.onload = e => {
      const img = new Image();
      img.onload = () => {
        const MAX = 1000;
        let w = img.width, h = img.height;
        if (w > MAX || h > MAX) {
          if (w > h) { h = Math.round(h * MAX / w); w = MAX; }
          else { w = Math.round(w * MAX / h); h = MAX; }
        }
        const canvas = document.createElement('canvas');
        canvas.width = w; canvas.height = h;
        canvas.getContext('2d').drawImage(img, 0, 0, w, h);
        cb(canvas.toDataURL('image/jpeg', 0.72));
      };
      img.src = e.target.result;
    };
    reader.readAsDataURL(file);
  },
 
  // Called when user picks files in the form
  handleFiles(files) {
    Array.from(files).forEach(file => {
      if (!file.type.startsWith('image/')) return;
      this.compress(file, dataUrl => {
        const photo = { id: '_p' + Date.now() + Math.random().toString(36).slice(2,5), label: 'Other', dataUrl };
        stagedPhotos.push(photo);
        this.renderStagedGrid();
      });
    });
  },
 
  // Render the photo grid inside the inspection form
  renderStagedGrid() {
    const grid = document.getElementById('staged-photo-grid');
    if (!grid) return;
    if (!stagedPhotos.length) {
      grid.innerHTML = '';
      return;
    }
    grid.innerHTML = stagedPhotos.map((p, i) => `
      <div class="photo-thumb-wrap">
        <img class="photo-thumb" src="${p.dataUrl}" onclick="Photos.openLightboxFromStaged(${i})">
        <button class="photo-thumb-del" onclick="Photos.deleteStagedPhoto('${p.id}')">×</button>
        <div class="photo-thumb-lbl">${p.label}</div>
      </div>
    `).join('');
    // Update label selects below
    this.renderLabelSelects();
  },
 
  // Render label selectors under the grid
  renderLabelSelects() {
    const wrap = document.getElementById('staged-label-wrap');
    if (!wrap || !stagedPhotos.length) { if (wrap) wrap.innerHTML = ''; return; }
    wrap.innerHTML = stagedPhotos.map((p, i) => `
      <div style="display:flex;align-items:center;gap:8px;margin-bottom:8px">
        <img src="${p.dataUrl}" style="width:40px;height:40px;object-fit:cover;border-radius:6px;flex-shrink:0">
        <select onchange="Photos.setLabel('${p.id}',this.value)" style="flex:1;font-size:13px;padding:7px 10px">
          ${PHOTO_LABELS.map(l => `<option value="${l}" ${l===p.label?'selected':''}>${l}</option>`).join('')}
        </select>
      </div>
    `).join('');
  },
 
  setLabel(id, label) {
    const p = stagedPhotos.find(x => x.id === id);
    if (p) { p.label = label; this.renderStagedGrid(); }
  },
 
  deleteStagedPhoto(id) {
    stagedPhotos = stagedPhotos.filter(p => p.id !== id);
    this.renderStagedGrid();
    this.renderLabelSelects();
  },
 
  // Save staged photos to storage under an inspId
  saveForInsp(inspId) {
    if (stagedPhotos.length) PhotoDB.set(inspId, stagedPhotos);
    stagedPhotos = [];
  },
 
  // Lightbox from staged grid
  openLightboxFromStaged(idx) {
    this.lbPhotos = stagedPhotos;
    this.lbIdx = idx;
    this.showLightbox();
  },
 
  // Lightbox from detail view
  openLightbox(photos, idx) {
    this.lbPhotos = photos;
    this.lbIdx = idx;
    this.showLightbox();
  },
 
  showLightbox() {
    const p = this.lbPhotos[this.lbIdx];
    if (!p) return;
    document.getElementById('lb-img').src = p.dataUrl;
    document.getElementById('lb-cap').textContent = p.label + (this.lbPhotos.length > 1 ? ` (${this.lbIdx+1}/${this.lbPhotos.length})` : '');
    document.getElementById('lightbox').classList.add('on');
  },
 
  closeLightbox() {
    document.getElementById('lightbox').classList.remove('on');
    document.getElementById('lb-img').src = '';
  },
 
  lbNav(dir) {
    this.lbIdx = (this.lbIdx + dir + this.lbPhotos.length) % this.lbPhotos.length;
    this.showLightbox();
  },
 
  // Render photos in the detail modal
  renderDetailPhotos(inspId) {
    const photos = PhotoDB.get(inspId);
    if (!photos.length) return '';
    return `
      <div style="margin-top:14px">
        <div style="font-size:13px;font-weight:500;color:var(--muted);margin-bottom:8px;font-family:'IBM Plex Mono',monospace;letter-spacing:.05em;text-transform:uppercase;font-size:11px">Photos (${photos.length})</div>
        <div class="detail-photo-grid">
          ${photos.map((p,i) => `
            <div class="detail-photo-wrap" onclick="Photos.openLightbox(${JSON.stringify(photos).replace(/"/g,'&quot;')},${i})">
              <img class="detail-photo" src="${p.dataUrl}">
              <div class="detail-photo-lbl">${p.label}</div>
            </div>
          `).join('')}
        </div>
      </div>`;
  },
 
  // Photo card HTML for inside the inspection form
  formCard() {
    return `
    <div class="card">
      <div class="card-t">Photos</div>
      <div class="photo-upload-area" onclick="document.getElementById('photo-input').click()">
        <div class="photo-upload-icon">📷</div>
        <div class="photo-upload-txt">Tap to add photos<br><strong>Queen · Brood · Anything interesting</strong></div>
      </div>
      <input type="file" id="photo-input" accept="image/*" multiple capture="environment"
        style="display:none" onchange="Photos.handleFiles(this.files);this.value=''">
      <div id="staged-photo-grid" class="photo-grid"></div>
      <div id="staged-label-wrap" style="margin-top:10px"></div>
    </div>`;
  },
};
 
// ── App state ─────────────────────────────────────────────────────────────────
let activeHive=null,detailId=null,detailType=null,editingYardId=null,editingHiveId=null;
 
function uid(){return '_'+Date.now()+Math.random().toString(36).slice(2,6);}
function fmtDate(d){if(!d)return'';const p=d.split('-');return['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'][+p[1]-1]+' '+parseInt(p[2])+', '+p[0];}
function el(id){return document.getElementById(id);}
function qa(sel,ctx){return[...(ctx||document).querySelectorAll(sel)];}
function gv(id){const e=el(id);return e?e.value.trim():'';}
function gc(id){const e=el(id);return e?e.checked:false;}
function pillVal(gid){const s=document.querySelector('#'+gid+' .pill.on');return s?s.textContent.trim():'';}
function multiPillVal(gid){return qa('#'+gid+' .pill.on').map(p=>p.textContent.trim()).join(', ');}
function scoreVal(id){const e=el(id);return e?e.value:'';}
function lastInsp(hiveId,insps){return insps.filter(i=>i.hiveId===hiveId).sort((a,b)=>new Date(b.date)-new Date(a.date))[0]||null;}
function hiveStatus(hiveId,insps){
  const l=lastInsp(hiveId,insps);if(!l)return'x';
  if(l.overall==='poor')return'r';if(l.overall==='fair')return'y';if(l.overall==='good')return'g';
  const sc=[l.queenScore,l.broodScore,l.honeyScore,l.pestScore].filter(Boolean);
  if(sc.includes('poor'))return'r';if(sc.includes('fair'))return'y';if(sc.length)return'g';return'x';
}
function scoreTag(v){
  if(!v)return'tag-x';const lo=v.toLowerCase();
  if(['good','none','solid','full','calm'].includes(lo))return'tag-g';
  if(['fair','monitor','spotty','adequate','moderate'].includes(lo))return'tag-y';
  return'tag-r';
}
function pickPill(el,gid){qa('#'+gid+' .pill').forEach(p=>p.classList.remove('on'));el.classList.add('on');}
function pickColor(el){qa('#pg-qcolor .qcolor-swatch').forEach(s=>s.classList.remove('on'));el.classList.add('on');}
function showSplitSource(){
  const val=pillVal('pg-qsource');
  const detail=el('split-source-detail');
  const hiveWrap=el('split-source-hive-wrap');
  const purchasedWrap=el('split-purchased-wrap');
  const lbl=el('split-source-hive-lbl');
  if(!val||val==='Walk-away'||val==='Queen cells from parent'){
    detail.style.display='none'; return;
  }
  detail.style.display='block';
  if(val==='Purchased queen'){
    hiveWrap.style.display='none';
    purchasedWrap.style.display='block';
  } else {
    hiveWrap.style.display='block';
    purchasedWrap.style.display='none';
    if(lbl) lbl.innerHTML=val==='Grafted'
      ?'Grafted from colony <span style="font-size:11px;color:var(--muted);font-weight:400">— source of larvae</span>'
      :'Mated from colony <span style="font-size:11px;color:var(--muted);font-weight:400">— source of genetics</span>';
  }
}
function multiPill(el){el.classList.toggle('on');}
function pickScore(el,rowId,hidId,val){
  qa('#'+rowId+' .sbtn').forEach(b=>b.classList.remove('sg','sy','sr'));
  el.classList.add(val==='good'||val==='none'?'sg':val==='fair'||val==='monitor'?'sy':'sr');
  const h=document.getElementById(hidId);if(h)h.value=val;
}
function showSub(subId,show){const s=el(subId);if(s)s.classList.toggle('on',show);}
function calcMites(){
  const inp=el('f-mites');if(!inp)return;
  const mites=inp.value.trim();const mbox=el('mbox');if(!mbox)return;
  if(mites===''||isNaN(+mites)){mbox.style.display='none';return;}
  const sampleTxt=pillVal('pg-sample');
  const sz=sampleTxt.includes('200')?200:sampleTxt.includes('100')?100:300;
  const rate=(+mites/sz)*100;
  mbox.style.display='block';
  el('mbox-rate').textContent=rate.toFixed(1)+'%';
  const lbl=el('mbox-lbl');
  if(rate<2){lbl.textContent='Low';lbl.className='mbox-lbl tag tag-g';}
  else if(rate<3){lbl.textContent='Borderline';lbl.className='mbox-lbl tag tag-y';}
  else{lbl.textContent='Treat now';lbl.className='mbox-lbl tag tag-r';}
}
 
const UI={
  tab(name,btn){
    qa('.tab').forEach(t=>t.classList.remove('on'));btn.classList.add('on');
    qa('.scr').forEach(s=>s.classList.remove('on'));el('scr-'+name).classList.add('on');
    if(name==='hives')  this.renderHives();
    if(name==='yards')  this.renderYards();
    if(name==='log')    this.renderLogHives();
    if(name==='splits') this.renderSplits();
    if(name==='history')this.renderHistory();
  },
 
  renderHives(){
    const hives=DB.hives(),insps=DB.insps(),yards=DB.yards();
    const weekAgo=new Date(Date.now()-7*864e5);
    const recent=insps.filter(i=>new Date(i.date)>=weekAgo).length;
    const healthy=hives.filter(h=>hiveStatus(h.id,insps)==='g').length;
    el('stats').innerHTML=`<div class="stat"><div class="stat-n">${hives.length}</div><div class="stat-l">Hives</div></div><div class="stat"><div class="stat-n">${healthy}</div><div class="stat-l">Healthy</div></div><div class="stat"><div class="stat-n">${recent}</div><div class="stat-l">This week</div></div>`;
    const list=el('hive-list');
    if(!hives.length){list.innerHTML='<div class="empty"><div class="empty-i">🐝</div><p>No hives yet.</p></div>';return;}
    list.innerHTML=hives.map(h=>{
      const st=hiveStatus(h.id,insps);
      const li=lastInsp(h.id,insps);
      const yard=yards.find(y=>y.id===h.yardId);
      const meta=[yard?yard.name:h.loc||'',li?'Last: '+fmtDate(li.date):'Never inspected'].filter(Boolean).join(' · ');
      return`<div class="hcard" onclick="UI.openHiveDetail('${h.id}')">
        <div style="flex:1"><div class="hcard-name">${h.name}</div><div class="hcard-meta">${meta}</div></div>
        <button class="edit-btn" onclick="event.stopPropagation();UI.openEditHive('${h.id}')" title="Edit hive">✎</button>
        <div class="dot dot-${st}" style="margin-left:8px"></div>
      </div>`;
    }).join('');
  },
 
  openAddHive(){
    el('new-name').value='';el('new-loc').value='';
    this.populateYardSelect('new-yard','');
    this.openModal('m-add');setTimeout(()=>el('new-name').focus(),80);
  },
 
  saveHive(){
    const name=gv('new-name');if(!name){alert('Please enter a hive name.');return;}
    const hives=DB.hives();
    hives.push({id:uid(),name,yardId:el('new-yard').value,loc:gv('new-loc'),created:new Date().toISOString()});
    DB.setHives(hives);this.closeModal('m-add');this.renderHives();this.populateSelects();
  },
 
  openEditHive(hiveId){
    const hive=DB.hives().find(h=>h.id===hiveId);if(!hive)return;
    editingHiveId=hiveId;
    el('edit-hive-name').value=hive.name||'';
    el('edit-hive-loc').value=hive.loc||'';
    this.populateYardSelect('edit-hive-yard',hive.yardId||'');
    this.openModal('m-edit-hive');
    setTimeout(()=>el('edit-hive-name').focus(),80);
  },
 
  saveEditHive(){
    const name=gv('edit-hive-name');if(!name){alert('Please enter a hive name.');return;}
    const hives=DB.hives();
    const h=hives.find(h=>h.id===editingHiveId);if(!h)return;
    h.name=name;h.yardId=el('edit-hive-yard').value;h.loc=gv('edit-hive-loc');
    DB.setHives(hives);this.closeModal('m-edit-hive');editingHiveId=null;
    this.renderHives();this.populateSelects();
  },
 
  // ── Yards ──────────────────────────────────────────────────────────────────
  renderYards(){
    const yards=DB.yards(),hives=DB.hives();
    const list=el('yard-list');
    if(!yards.length){
      list.innerHTML='<div class="empty"><div class="empty-i">📍</div><p>No yards yet. Add a yard to group your hives by location.</p></div>';
      return;
    }
    list.innerHTML=yards.map(y=>{
      const count=hives.filter(h=>h.yardId===y.id).length;
      return`<div class="hcard">
        <div style="flex:1" onclick="UI.openEditYard('${y.id}')">
          <div class="hcard-name">${y.name}</div>
          <div class="hcard-meta">${y.loc||''} · ${count} hive${count!==1?'s':''}</div>
        </div>
        <button class="edit-btn" onclick="UI.openEditYard('${y.id}')" title="Edit yard">✎</button>
      </div>`;
    }).join('');
  },
 
  openAddYard(){
    el('new-yard-name').value='';el('new-yard-loc').value='';
    this.openModal('m-add-yard');setTimeout(()=>el('new-yard-name').focus(),80);
  },
 
  saveYard(){
    const name=gv('new-yard-name');if(!name){alert('Please enter a yard name.');return;}
    const yards=DB.yards();
    yards.push({id:uid(),name,loc:gv('new-yard-loc'),created:new Date().toISOString()});
    DB.setYards(yards);this.closeModal('m-add-yard');this.renderYards();this.populateSelects();
  },
 
  openEditYard(yardId){
    const yard=DB.yards().find(y=>y.id===yardId);if(!yard)return;
    editingYardId=yardId;
    el('edit-yard-name').value=yard.name||'';
    el('edit-yard-loc').value=yard.loc||'';
    this.openModal('m-edit-yard');setTimeout(()=>el('edit-yard-name').focus(),80);
  },
 
  saveEditYard(){
    const name=gv('edit-yard-name');if(!name){alert('Please enter a yard name.');return;}
    const yards=DB.yards();
    const y=yards.find(y=>y.id===editingYardId);if(!y)return;
    y.name=name;y.loc=gv('edit-yard-loc');
    DB.setYards(yards);this.closeModal('m-edit-yard');editingYardId=null;
    this.renderYards();this.populateSelects();
  },
 
  deleteYard(){
    if(!editingYardId)return;
    const yards=DB.yards();
    const yard=yards.find(y=>y.id===editingYardId);
    const hiveCount=DB.hives().filter(h=>h.yardId===editingYardId).length;
    const msg=hiveCount>0
      ? `Delete "${yard?.name}"? The ${hiveCount} hive(s) in this yard will have their yard cleared but will NOT be deleted.`
      : `Delete "${yard?.name}"?`;
    if(!confirm(msg))return;
    // Clear yardId from hives in this yard
    const hives=DB.hives().map(h=>h.yardId===editingYardId?{...h,yardId:''}:h);
    DB.setHives(hives);
    DB.setYards(yards.filter(y=>y.id!==editingYardId));
    this.closeModal('m-edit-yard');editingYardId=null;
    this.renderYards();this.renderHives();this.populateSelects();
  },
 
  populateYardSelect(selectId, selectedId){
    const yards=DB.yards();
    const opts='<option value="">No yard assigned</option>'+
      yards.map(y=>`<option value="${y.id}"${y.id===selectedId?' selected':''}>${y.name}</option>`).join('');
    const e=el(selectId);if(e)e.innerHTML=opts;
  },
 
  // ── Splits ────────────────────────────────────────────────────────────────
  renderSplits(){
    const splits=DB.splits().sort((a,b)=>new Date(b.date)-new Date(a.date));
    const hives=DB.hives();
    const list=el('split-list');
    if(!splits.length){
      list.innerHTML='<div class="empty"><div class="empty-i">✂️</div><p>No splits logged yet.</p></div>';
      return;
    }
    list.innerHTML=splits.map(s=>{
      const parent=hives.find(h=>h.id===s.parentHiveId);
      const daughter=hives.find(h=>h.id===s.daughterHiveId);
      const srcHive=hives.find(h=>h.id===s.queenSourceHiveId);
      let sourceStr=s.queenSource||'';
      if(srcHive&&(s.queenSource==='Grafted'||s.queenSource==='Mated from own yard'))
        sourceStr+=` (from ${srcHive.name})`;
      if(s.queenSource==='Purchased queen'&&s.purchasedSource)
        sourceStr+=` — ${s.purchasedSource}`;
      return`<div class="split-item" onclick="UI.openSplitDetail('${s.id}')">
        <div class="split-hdr">
          <div class="split-title">${parent?parent.name:'?'} → ${daughter?daughter.name:'?'}</div>
          <div class="split-date">${fmtDate(s.date)}</div>
        </div>
        <div class="split-meta">${sourceStr}</div>
        ${s.notes?`<div class="split-meta" style="margin-top:2px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap">${s.notes}</div>`:''}
        <span class="split-source-badge">${s.queenSource||'Queen source unset'}</span>
      </div>`;
    }).join('');
  },
 
  openAddSplit(){
    const today=new Date().toISOString().split('T')[0];
    el('split-date').value=today;
    this.populateSplitHiveSelects();
    qa('#pg-qsource .pill').forEach(p=>p.classList.remove('on'));
    qa('#pg-parent-queen .pill').forEach(p=>p.classList.remove('on'));
    el('split-notes').value='';
    el('split-source-detail').style.display='none';
    el('split-purchased-wrap').style.display='none';
    this.openModal('m-add-split');
  },
 
  populateSplitHiveSelects(){
    const hives=DB.hives();
    const opts='<option value="">Select colony…</option>'+hives.map(h=>`<option value="${h.id}">${h.name}</option>`).join('');
    ['split-parent','split-daughter','split-source-hive'].forEach(id=>{const e=el(id);if(e)e.innerHTML=opts;});
  },
 
  saveSplit(){
    const date=gv('split-date');
    if(!date){alert('Please select a date.');return;}
    const parentId=el('split-parent').value;
    const daughterId=el('split-daughter').value;
    if(!parentId||!daughterId){alert('Please select both parent and daughter colonies.');return;}
    if(parentId===daughterId){alert('Parent and daughter must be different colonies.');return;}
    const queenSource=pillVal('pg-qsource');
    if(!queenSource){alert('Please select a queen source.');return;}
    const rec={
      id:uid(),date,
      parentHiveId:parentId,
      daughterHiveId:daughterId,
      queenSource,
      queenSourceHiveId:el('split-source-hive').value||'',
      purchasedSource:gv('split-purchased-src'),
      parentQueenAction:pillVal('pg-parent-queen'),
      notes:gv('split-notes'),
      savedAt:new Date().toISOString()
    };
    const splits=DB.splits();splits.push(rec);DB.setSplits(splits);
    this.closeModal('m-add-split');
    this.renderSplits();
  },
 
  openSplitDetail(splitId){
    const splits=DB.splits(),hives=DB.hives();
    const s=splits.find(x=>x.id===splitId);if(!s)return;
    const parent=hives.find(h=>h.id===s.parentHiveId);
    const daughter=hives.find(h=>h.id===s.daughterHiveId);
    const srcHive=hives.find(h=>h.id===s.queenSourceHiveId);
    detailId=splitId; detailType='split';
    el('m-split-t').textContent=`Split — ${fmtDate(s.date)}`;
    const rows=[
      ['Date',fmtDate(s.date)],
      ['Parent colony',parent?parent.name:'—'],
      ['Daughter colony',daughter?daughter.name:'—'],
      ['Queen source',s.queenSource||'—'],
      ['Source colony',srcHive?srcHive.name:'—'],
      ['Purchased from',s.purchasedSource||'—'],
      ['Parent queen',s.parentQueenAction||'—'],
      ['Notes',s.notes||'—'],
    ];
    el('m-split-body').innerHTML=`
      <table class="dtbl">${rows.map(([k,v])=>`<tr><td class="k">${k}</td><td class="v">${v}</td></tr>`).join('')}</table>
      <div style="margin-top:14px;display:flex;gap:8px">
        ${parent?`<button class="btn btn-sm" style="flex:1" onclick="UI.closeModal('m-split-detail');UI.openLineage('${parent.id}')">🌿 ${parent.name} lineage</button>`:''}
        ${daughter?`<button class="btn btn-sm" style="flex:1" onclick="UI.closeModal('m-split-detail');UI.openLineage('${daughter.id}')">🌿 ${daughter.name} lineage</button>`:''}
      </div>`;
    this.openModal('m-split-detail');
  },
 
  deleteSplit(){
    if(!detailId||detailType!=='split')return;
    if(!confirm('Delete this split record?'))return;
    DB.setSplits(DB.splits().filter(s=>s.id!==detailId));
    detailId=null;detailType=null;
    this.closeModal('m-split-detail');
    this.renderSplits();
  },
 
  // ── Lineage tree ──────────────────────────────────────────────────────────
  openLineage(hiveId){
    const hives=DB.hives(),splits=DB.splits();
    const hive=hives.find(h=>h.id===hiveId);if(!hive)return;
    el('m-lineage-t').textContent=`${hive.name} — Queen Lineage`;
 
    // Build ancestor chain (walk up through queen source)
    const ancestors=[];
    let current=hiveId;
    const visited=new Set();
    while(current&&!visited.has(current)){
      visited.add(current);
      // Find the split that created this colony (where it was the daughter)
      const originSplit=splits.find(s=>s.daughterHiveId===current);
      if(!originSplit)break;
      const srcId=originSplit.queenSourceHiveId||originSplit.parentHiveId;
      if(!srcId)break;
      ancestors.push({split:originSplit,hiveId:srcId});
      current=srcId;
    }
 
    // Build descendant tree (colonies whose queens trace back to this hive)
    const findDescendants=(hId,depth=0)=>{
      if(depth>10)return[];
      const results=[];
      splits.filter(s=>(s.queenSourceHiveId===hId||s.parentHiveId===hId)&&s.daughterHiveId!==hId)
        .forEach(s=>{
          const dh=hives.find(h=>h.id===s.daughterHiveId);
          if(dh){
            results.push({hive:dh,split:s,depth,children:findDescendants(dh.id,depth+1)});
          }
        });
      return results;
    };
    const descendants=findDescendants(hiveId);
 
    // Render
    const renderDesc=(nodes,depth=0)=>nodes.map(n=>`
      <div style="margin-left:${depth*16}px">
        <div class="lineage-connector"></div>
        <div class="lineage-node descendant">
          <div class="lineage-label">↓ Split ${fmtDate(n.split.date)} · ${n.split.queenSource||''}</div>
          <div class="lineage-name">${n.hive.name}</div>
          ${n.split.parentQueenAction?`<div class="lineage-detail">Parent queen: ${n.split.parentQueenAction}</div>`:''}
          <button class="btn btn-sm" style="margin-top:6px;width:auto" onclick="UI.closeModal('m-lineage');UI.openLineage('${n.hive.id}')">View ${n.hive.name} lineage →</button>
        </div>
        ${n.children.length?renderDesc(n.children,0):''}
      </div>`).join('');
 
    let html='';
    // Ancestors (top to bottom = oldest to most recent)
    [...ancestors].reverse().forEach((a,i)=>{
      const ah=hives.find(h=>h.id===a.hiveId);
      if(!ah)return;
      html+=`<div class="lineage-node ancestor">
        <div class="lineage-label">Ancestor colony</div>
        <div class="lineage-name">${ah.name}</div>
        <div class="lineage-detail">${a.split.queenSource||''} · ${fmtDate(a.split.date)}</div>
        <button class="btn btn-sm" style="margin-top:6px;width:auto" onclick="UI.closeModal('m-lineage');UI.openLineage('${ah.id}')">View ${ah.name} lineage →</button>
      </div>
      <div class="lineage-connector"></div>`;
    });
 
    // Current hive
    html+=`<div class="lineage-node current">
      <div class="lineage-label">This colony</div>
      <div class="lineage-name">${hive.name}</div>
      ${ancestors.length?`<div class="lineage-detail">Queen from: ${(()=>{const s=ancestors[0]?.split;const src=hives.find(h=>h.id===s?.queenSourceHiveId)||hives.find(h=>h.id===s?.parentHiveId);return src?src.name+' ('+fmtDate(s.date)+')':'unknown';})()}</div>`:'<div class="lineage-detail">No recorded queen lineage</div>'}
    </div>`;
 
    // Descendants
    if(descendants.length){
      html+=renderDesc(descendants);
    } else if(!ancestors.length){
      html+=`<div style="font-size:13px;color:var(--muted);text-align:center;margin-top:12px">No splits recorded from this colony yet.</div>`;
    }
 
    el('m-lineage-body').innerHTML=html;
    this.openModal('m-lineage');
  },
 
  openHiveDetail(hiveId){
    const hives=DB.hives(),insps=DB.insps(),yards=DB.yards(),splits=DB.splits();
    const hive=hives.find(h=>h.id===hiveId);if(!hive)return;
    detailType='hive';detailId=hiveId;
    el('m-detail-t').textContent=hive.name;
    el('m-detail-del').textContent='Remove hive';
    const yard=yards.find(y=>y.id===hive.yardId);
    const hi=insps.filter(i=>i.hiveId===hiveId).sort((a,b)=>new Date(b.date)-new Date(a.date));
    // Lineage summary
    const originSplit=splits.find(s=>s.daughterHiveId===hiveId);
    const parentHive=originSplit?hives.find(h=>h.id===originSplit.parentHiveId):null;
    const queenSrcHive=originSplit?hives.find(h=>h.id===originSplit.queenSourceHiveId):null;
    const lineageStr=originSplit
      ?`Split from ${parentHive?parentHive.name:'unknown'} on ${fmtDate(originSplit.date)} · ${originSplit.queenSource||''}`
      :'No split origin recorded';
    const descendants=splits.filter(s=>s.parentHiveId===hiveId||s.queenSourceHiveId===hiveId);
    el('m-detail-body').innerHTML=`
      <div class="fg"><label>Yard</label><div style="color:var(--text)">${yard?yard.name:'—'}</div></div>
      <div class="fg"><label>Location</label><div style="color:var(--text)">${hive.loc||'—'}</div></div>
      <div class="fg"><label>Queen origin</label><div style="color:var(--text);font-size:13px">${lineageStr}</div></div>
      <div class="fg"><label>Descendants</label><div style="color:var(--text)">${descendants.length} split${descendants.length!==1?'s':''} recorded from this colony</div></div>
      <div style="display:flex;gap:8px;margin-bottom:12px">
        <button class="btn btn-sm" style="flex:1" onclick="UI.closeModal('m-detail');UI.openEditHive('${hiveId}')">✎ Edit hive</button>
        <button class="btn btn-sm" style="flex:1" onclick="UI.closeModal('m-detail');UI.openLineage('${hiveId}')">🌿 View lineage</button>
      </div>
      <div class="fg"><label>Inspections</label><div style="color:var(--text)">${hi.length}</div></div>
      ${hi.slice(0,3).map(i=>this.inspCard(i,hives,false)).join('')}
      ${hi.length>3?`<p style="font-size:13px;color:var(--muted);text-align:center;margin-top:6px">+${hi.length-3} more in History</p>`:''}`;
    this.openModal('m-detail');
  },
 
  renderLogHives(){
    const hives=DB.hives(),yards=DB.yards();
    const list=el('log-hives');
    if(!hives.length){list.innerHTML='<div class="empty"><p>Add a hive first on the Hives tab.</p></div>';el('log-form').innerHTML='';return;}
    list.innerHTML=hives.map(h=>{
      const yard=yards.find(y=>y.id===h.yardId);
      const meta=yard?yard.name:h.loc||'';
      return`<div class="hcard ${activeHive===h.id?'sel':''}" onclick="UI.selectHive('${h.id}')">
        <div><div class="hcard-name">${h.name}</div><div class="hcard-meta">${meta}</div></div>
      </div>`;
    }).join('');
    if(activeHive)this.renderForm();
  },
 
  selectHive(id){stagedPhotos=[];activeHive=id;this.renderLogHives();},
 
  renderForm(){
    const today=new Date().toISOString().split('T')[0];
    el('log-form').innerHTML=`<hr class="div"><div class="slbl">Inspection details</div>
<div class="card"><div class="card-t">Overall rating</div><div class="srow" id="sr-overall"><div class="sbtn" onclick="pickScore(this,'sr-overall','f-overall','good')">Good</div><div class="sbtn" onclick="pickScore(this,'sr-overall','f-overall','fair')">Fair</div><div class="sbtn" onclick="pickScore(this,'sr-overall','f-overall','poor')">Poor</div></div><input type="hidden" id="f-overall" value=""><div class="fg" style="margin-top:14px;margin-bottom:0"><label>Date</label><input type="date" id="f-date" value="${today}"></div></div>
<div class="card"><div class="card-t">Queen</div><div class="fg"><label>Queen seen?</label><div class="pills" id="pg-qseen"><div class="pill" onclick="pickPill(this,'pg-qseen')">Yes</div><div class="pill" onclick="pickPill(this,'pg-qseen')">No</div><div class="pill" onclick="pickPill(this,'pg-qseen')">Eggs only</div></div></div><div class="fg"><label>Queen marked?</label><div class="pills" id="pg-qmarked"><div class="pill" onclick="pickPill(this,'pg-qmarked')">Yes</div><div class="pill" onclick="pickPill(this,'pg-qmarked')">No</div><div class="pill" onclick="pickPill(this,'pg-qmarked')">Marked this visit</div></div></div><div class="fg"><label>Mark color <span style="font-size:11px;color:var(--muted);font-weight:400">(W=1/6 · Y=2/7 · R=3/8 · G=4/9 · B=5/0)</span></label><div class="qcolor-group" id="pg-qcolor" style="display:flex;gap:10px;flex-wrap:wrap;margin-top:2px"><div class="qcolor-swatch" data-color="White" onclick="pickColor(this)" style="--c:#e5e7eb;--b:#9ca3af"><span class="qcolor-dot" style="background:#e5e7eb;border:2px solid #9ca3af"></span><span class="qcolor-lbl">White</span></div><div class="qcolor-swatch" data-color="Yellow" onclick="pickColor(this)" style="--c:#fef08a;--b:#ca8a04"><span class="qcolor-dot" style="background:#fef08a;border:2px solid #ca8a04"></span><span class="qcolor-lbl">Yellow</span></div><div class="qcolor-swatch" data-color="Red" onclick="pickColor(this)" style="--c:#fca5a5;--b:#dc2626"><span class="qcolor-dot" style="background:#fca5a5;border:2px solid #dc2626"></span><span class="qcolor-lbl">Red</span></div><div class="qcolor-swatch" data-color="Green" onclick="pickColor(this)" style="--c:#86efac;--b:#16a34a"><span class="qcolor-dot" style="background:#86efac;border:2px solid #16a34a"></span><span class="qcolor-lbl">Green</span></div><div class="qcolor-swatch" data-color="Blue" onclick="pickColor(this)" style="--c:#93c5fd;--b:#2563eb"><span class="qcolor-dot" style="background:#93c5fd;border:2px solid #2563eb"></span><span class="qcolor-lbl">Blue</span></div></div></div><div class="fg"><label>Queen status</label><div class="srow" id="sr-queen"><div class="sbtn" onclick="pickScore(this,'sr-queen','f-queenscore','good')">Good</div><div class="sbtn" onclick="pickScore(this,'sr-queen','f-queenscore','fair')">Fair</div><div class="sbtn" onclick="pickScore(this,'sr-queen','f-queenscore','poor')">Poor</div></div><input type="hidden" id="f-queenscore" value=""></div><div class="fg"><label>Queen cells present?</label><div class="pills" id="pg-qcells"><div class="pill" onclick="pickPill(this,'pg-qcells');showSub('sub-qc',false)">None</div><div class="pill" onclick="pickPill(this,'pg-qcells');showSub('sub-qc',true)">Yes</div></div></div><div class="sub" id="sub-qc"><div class="fg"><label>Cell type — select all that apply</label><div class="pills" id="pg-qctype"><div class="pill pill-sm" onclick="multiPill(this)">Swarm</div><div class="pill pill-sm" onclick="multiPill(this)">Supersedure</div><div class="pill pill-sm" onclick="multiPill(this)">Emergency</div><div class="pill pill-sm" onclick="multiPill(this)">Capped</div><div class="pill pill-sm" onclick="multiPill(this)">Open</div><div class="pill pill-sm" onclick="multiPill(this)">Removed</div></div></div><div class="fg" style="margin-bottom:0"><label>Number of cells</label><input type="text" id="f-qccount" placeholder="e.g. 3"></div></div></div>
<div class="card"><div class="card-t">Brood</div><div class="fg" style="margin-bottom:0"><label>Brood pattern</label><div class="srow" id="sr-brood"><div class="sbtn" onclick="pickScore(this,'sr-brood','f-broodscore','good')">Solid</div><div class="sbtn" onclick="pickScore(this,'sr-brood','f-broodscore','fair')">Spotty</div><div class="sbtn" onclick="pickScore(this,'sr-brood','f-broodscore','poor')">Poor</div></div><input type="hidden" id="f-broodscore" value=""></div></div>
<div class="card"><div class="card-t">Colony</div><div class="fg"><label>Population strength</label><div class="pills" id="pg-pop"><div class="pill pill-sm" onclick="pickPill(this,'pg-pop')">Light</div><div class="pill pill-sm" onclick="pickPill(this,'pg-pop')">Medium</div><div class="pill pill-sm" onclick="pickPill(this,'pg-pop')">Strong</div><div class="pill pill-sm" onclick="pickPill(this,'pg-pop')">Booming</div></div></div><div class="fg" style="margin-bottom:0"><label>Temperament</label><div class="pills" id="pg-temp"><div class="pill pill-sm" onclick="pickPill(this,'pg-temp')">Calm</div><div class="pill pill-sm" onclick="pickPill(this,'pg-temp')">Moderate</div><div class="pill pill-sm" onclick="pickPill(this,'pg-temp')">Defensive</div></div></div></div>
<div class="card"><div class="card-t">Honey & stores</div><div class="fg" style="margin-bottom:0"><label>Store level</label><div class="srow" id="sr-honey"><div class="sbtn" onclick="pickScore(this,'sr-honey','f-honeyscore','good')">Full</div><div class="sbtn" onclick="pickScore(this,'sr-honey','f-honeyscore','fair')">Adequate</div><div class="sbtn" onclick="pickScore(this,'sr-honey','f-honeyscore','poor')">Low</div></div><input type="hidden" id="f-honeyscore" value=""></div></div>
<div class="card"><div class="card-t">Varroa — alcohol wash</div><div class="fg"><label>Mites counted</label><input type="number" id="f-mites" min="0" placeholder="# of mites" oninput="calcMites()"></div><div class="fg"><label>Sample size</label><div class="pills" id="pg-sample"><div class="pill pill-sm on" onclick="pickPill(this,'pg-sample');calcMites()">300 bees (1 cup)</div><div class="pill pill-sm" onclick="pickPill(this,'pg-sample');calcMites()">200 bees</div><div class="pill pill-sm" onclick="pickPill(this,'pg-sample');calcMites()">100 bees</div></div></div><div class="mbox" id="mbox"><div><span class="mbox-rate" id="mbox-rate"></span><span class="mbox-unit">mites / 100 bees</span><span class="mbox-lbl" id="mbox-lbl"></span></div><div class="mbox-note">Threshold: treat at ≥2% spring/summer · ≥3% fall</div></div><div class="fg"><label>Other pest / disease notes</label><input type="text" id="f-pest" placeholder="SHB, nosema, chalkbrood, EFB…"></div><div class="fg" style="margin-top:4px;margin-bottom:0"><label>Pest concern level</label><div class="srow" id="sr-pest"><div class="sbtn" onclick="pickScore(this,'sr-pest','f-pestscore','good')">None</div><div class="sbtn" onclick="pickScore(this,'sr-pest','f-pestscore','fair')">Monitor</div><div class="sbtn" onclick="pickScore(this,'sr-pest','f-pestscore','poor')">Treat</div></div><input type="hidden" id="f-pestscore" value=""></div></div>
<div class="card"><div class="card-t">Swarm activity</div><div class="fg" style="margin-bottom:0"><label>Signs of swarming?</label><div class="pills" id="pg-swarm"><div class="pill pill-sm" onclick="pickPill(this,'pg-swarm')">None</div><div class="pill pill-sm" onclick="pickPill(this,'pg-swarm')">Suspected</div><div class="pill pill-sm" onclick="pickPill(this,'pg-swarm')">Swarmed</div><div class="pill pill-sm" onclick="pickPill(this,'pg-swarm')">Caught swarm</div></div></div></div>
<div class="card"><div class="card-t">Equipment</div><div class="trow" style="border-bottom:none"><span class="trow-lbl">Equipment changes made?</span><label class="tog"><input type="checkbox" id="f-equip" onchange="showSub('sub-equip',this.checked)"><span class="tog-tr"></span></label></div><div class="sub" id="sub-equip"><div class="fg" style="margin-top:10px;margin-bottom:0"><label>What changed?</label><input type="text" id="f-equip-notes" placeholder="e.g. Added honey super, replaced bottom board"></div></div></div>
<div class="card"><div class="card-t">Feeding</div><div class="trow"><span class="trow-lbl">Fed this visit?</span><label class="tog"><input type="checkbox" id="f-fed"><span class="tog-tr"></span></label></div><div class="fg" style="margin-top:12px;margin-bottom:0"><label>Feed type / amount</label><input type="text" id="f-feedtype" placeholder="e.g. 1:1 syrup 1 qt · pollen patty"></div></div>
<div class="card"><div class="card-t">Treatment</div><div class="trow"><span class="trow-lbl">Treated this visit?</span><label class="tog"><input type="checkbox" id="f-treated"><span class="tog-tr"></span></label></div><div class="fg" style="margin-top:12px;margin-bottom:0"><label>Treatment used</label><input type="text" id="f-treatment" placeholder="e.g. Apivar strips, OA dribble, HopGuard"></div></div>
<div class="card"><div class="fg" style="margin-bottom:0"><label>Notes</label><textarea id="f-notes" placeholder="Follow-up needed, observations, concerns…"></textarea></div></div>
${Photos.formCard()}
<button class="btn btn-p" style="margin-top:4px" onclick="UI.saveInsp()">Save inspection</button><div style="height:20px"></div>`;
  },
 
  saveInsp(){
    const date=gv('f-date');if(!date){alert('Please select a date.');return;}
    const mites=el('f-mites')?el('f-mites').value.trim():'';
    const sampleTxt=pillVal('pg-sample');
    const sz=sampleTxt.includes('200')?200:sampleTxt.includes('100')?100:300;
    const miteRate=mites!==''&&!isNaN(+mites)?((+mites/sz)*100).toFixed(1)+'%':'';
    const hiveRec=DB.hives().find(h=>h.id===activeHive)||{};
    const yardRec=DB.yards().find(y=>y.id===hiveRec.yardId)||{};
    const rec={id:uid(),hiveId:activeHive,yard:yardRec.name||hiveRec.loc||'',date,overall:scoreVal('f-overall'),queenSeen:pillVal('pg-qseen'),queenMarked:pillVal('pg-qmarked'),queenColor:(()=>{const s=document.querySelector('#pg-qcolor .qcolor-swatch.on');return s?s.getAttribute('data-color'):'';})(),queenScore:scoreVal('f-queenscore'),queenCells:pillVal('pg-qcells'),qcType:multiPillVal('pg-qctype'),qcCount:gv('f-qccount'),broodScore:scoreVal('f-broodscore'),population:pillVal('pg-pop'),temperament:pillVal('pg-temp'),honeyScore:scoreVal('f-honeyscore'),mites,mitesSample:sampleTxt,miteRate,pestNotes:gv('f-pest'),pestScore:scoreVal('f-pestscore'),swarm:pillVal('pg-swarm'),equipChanged:gc('f-equip'),equipNotes:gv('f-equip-notes'),fed:gc('f-fed'),feedType:gv('f-feedtype'),treated:gc('f-treated'),treatment:gv('f-treatment'),notes:gv('f-notes'),savedAt:new Date().toISOString()};
    const insps=DB.insps();insps.push(rec);DB.setInsps(insps);
    Photos.saveForInsp(rec.id);
    activeHive=null;
    el('log-form').innerHTML=`<div style="text-align:center;padding:40px 0;color:var(--text)"><div style="font-size:40px">✓</div><p style="font-weight:500;margin-top:10px">Inspection saved!</p></div>`;
    this.renderLogHives();setTimeout(()=>{el('log-form').innerHTML='';this.renderLogHives();},2000);
  },
 
  renderHistory(){
    const hives=DB.hives(),yards=DB.yards();
    const filterHive=el('hist-filter').value;
    const filterYard=el('hist-filter-yard').value;
    let insps=DB.insps().sort((a,b)=>new Date(b.date)-new Date(a.date));
    if(filterHive) insps=insps.filter(i=>i.hiveId===filterHive);
    else if(filterYard){
      const yardHiveIds=hives.filter(h=>h.yardId===filterYard).map(h=>h.id);
      insps=insps.filter(i=>yardHiveIds.includes(i.hiveId));
    }
    const list=el('hist-list');
    if(!insps.length){list.innerHTML='<div class="empty"><div class="empty-i">📋</div><p>No inspections yet.</p></div>';return;}
    list.innerHTML=insps.map(i=>this.inspCard(i,hives,true)).join('');
  },
 
  inspCard(i,hives,clickable){
    const hive=hives.find(h=>h.id===i.hiveId);
    const photoCount=PhotoDB.count(i.id);
    const tags=[];
    if(i.overall)tags.push({l:'Overall: '+i.overall,c:scoreTag(i.overall)});
    if(i.queenScore)tags.push({l:'Queen: '+i.queenScore,c:scoreTag(i.queenScore)});
    if(i.queenMarked==='Marked this visit')tags.push({l:'Queen marked'+(i.queenColor?' — '+i.queenColor:''),c:'tag-b'});
    if(i.queenCells==='Yes')tags.push({l:'Queen cells'+(i.qcType?': '+i.qcType:''),c:'tag-y'});
    if(i.broodScore)tags.push({l:'Brood: '+i.broodScore,c:scoreTag(i.broodScore)});
    if(i.honeyScore)tags.push({l:'Stores: '+i.honeyScore,c:scoreTag(i.honeyScore)});
    if(i.miteRate)tags.push({l:'Varroa: '+i.miteRate,c:parseFloat(i.miteRate)>=3?'tag-r':parseFloat(i.miteRate)>=2?'tag-y':'tag-g'});
    if(i.pestScore)tags.push({l:'Pests: '+i.pestScore,c:scoreTag(i.pestScore)});
    if(i.population)tags.push({l:i.population,c:'tag-x'});
    if(i.swarm&&i.swarm!=='None')tags.push({l:'Swarm: '+i.swarm,c:'tag-r'});
    if(i.fed)tags.push({l:'Fed',c:'tag-x'});
    if(i.treated)tags.push({l:'Treated',c:'tag-b'});
    if(i.equipChanged)tags.push({l:'Equipment',c:'tag-x'});
    if(photoCount>0)tags.push({l:'📷 '+photoCount+' photo'+(photoCount>1?'s':''),c:'tag-b'});
    const click=clickable?`onclick="UI.openInspDetail('${i.id}')"` :'';
    return`<div class="iitem" ${click}><div class="iitem-hdr"><div class="iitem-hive">${hive?hive.name:'Unknown'}</div><div class="iitem-date">${fmtDate(i.date)}</div></div>${i.notes?`<div class="iitem-note">${i.notes}</div>`:''}<div class="tags">${tags.map(t=>`<span class="tag ${t.c}">${t.l}</span>`).join('')}</div></div>`;
  },
 
  openInspDetail(id){
    const insps=DB.insps(),hives=DB.hives();
    const i=insps.find(x=>x.id===id);if(!i)return;
    const hive=hives.find(h=>h.id===i.hiveId);
    detailType='insp';detailId=id;
    el('m-detail-t').textContent=(hive?hive.name:'?')+' · '+fmtDate(i.date);
    el('m-detail-del').textContent='Delete inspection';
    const rows=[['Overall',i.overall||'—'],['Queen seen',i.queenSeen||'—'],['Queen marked',i.queenMarked||'—'],['Mark color',i.queenColor||'—'],['Queen status',i.queenScore||'—'],['Queen cells',i.queenCells||'—'],['Cell type',i.qcType||'—'],['Cell count',i.qcCount||'—'],['Brood pattern',i.broodScore||'—'],['Population',i.population||'—'],['Temperament',i.temperament||'—'],['Honey stores',i.honeyScore||'—'],['Varroa mites',i.mites?(i.mites+' / '+i.mitesSample):'—'],['Mite rate',i.miteRate||'—'],['Other pests',i.pestNotes||'—'],['Pest level',i.pestScore||'—'],['Swarm',i.swarm||'—'],['Equipment',i.equipChanged?('Yes'+(i.equipNotes?': '+i.equipNotes:'')):'No'],['Fed',i.fed?('Yes'+(i.feedType?': '+i.feedType:'')):'No'],['Treated',i.treated?('Yes'+(i.treatment?': '+i.treatment:'')):'No'],['Notes',i.notes||'—']];
    el('m-detail-body').innerHTML=`<table class="dtbl">${rows.map(([k,v])=>`<tr><td class="k">${k}</td><td class="v">${v}</td></tr>`).join('')}</table>${Photos.renderDetailPhotos(id)}`;
    this.openModal('m-detail');
  },
 
  deleteItem(){
    if(!detailId)return;
    if(detailType==='split'){
      this.deleteSplit(); return;
    } else if(detailType==='insp'){
      if(!confirm('Delete this inspection?'))return;
      PhotoDB.del(detailId);
      DB.setInsps(DB.insps().filter(i=>i.id!==detailId));
      this.closeModal('m-detail');this.renderHistory();this.renderHives();
    }else{
      if(!confirm('Remove this hive and ALL its inspections?'))return;
      DB.insps().filter(i=>i.hiveId===detailId).forEach(i=>PhotoDB.del(i.id));
      DB.setHives(DB.hives().filter(h=>h.id!==detailId));
      DB.setInsps(DB.insps().filter(i=>i.hiveId!==detailId));
      this.closeModal('m-detail');this.renderHives();this.populateSelects();
    }
    detailId=null;detailType=null;
  },
 
  showExport(){this.populateSelects();this.openModal('m-export');},
 
  doExport(){
    const hives=DB.hives(),filter=el('exp-filter').value;
    let insps=DB.insps().sort((a,b)=>new Date(a.date)-new Date(b.date));
    if(filter)insps=insps.filter(i=>i.hiveId===filter);
    if(!insps.length){alert('No inspections to export.');return;}
    const hdrs=['Date','Hive','Overall','Queen Seen','Queen Marked','Queen Mark Color','Queen Status','Queen Cells','Cell Type','Cell Count','Brood','Population','Temperament','Honey Stores','Varroa Mites','Varroa Sample','Mite Rate','Other Pest Notes','Pest Level','Swarm','Equipment Changed','Equipment Notes','Fed','Feed Type','Treated','Treatment','Notes','Photo Count'];
    const rows=insps.map(i=>{const hive=hives.find(h=>h.id===i.hiveId);return[i.date,hive?hive.name:i.hiveId,i.overall,i.queenSeen,i.queenMarked,i.queenColor,i.queenScore,i.queenCells,i.qcType,i.qcCount,i.broodScore,i.population,i.temperament,i.honeyScore,i.mites,i.mitesSample,i.miteRate,i.pestNotes,i.pestScore,i.swarm,i.equipChanged?'Yes':'No',i.equipNotes,i.fed?'Yes':'No',i.feedType,i.treated?'Yes':'No',i.treatment,i.notes,PhotoDB.count(i.id)].map(v=>'"'+(v||'').toString().replace(/"/g,'""')+'"');});
    const csv=[hdrs,...rows].map(r=>r.join(',')).join('\n');
    const a=document.createElement('a');
    a.href='data:text/csv;charset=utf-8,'+encodeURIComponent(csv);
    a.download='belles-honey-inspections.csv';a.click();
    this.closeModal('m-export');
  },
 
  openModal(id){el(id).classList.add('on');},
  closeModal(id){el(id).classList.remove('on');},
  populateSelects(){
    const hives=DB.hives(),yards=DB.yards();
    const hiveOpts='<option value="">All hives</option>'+hives.map(h=>`<option value="${h.id}">${h.name}</option>`).join('');
    const yardOpts='<option value="">All yards</option>'+yards.map(y=>`<option value="${y.id}">${y.name}</option>`).join('');
    const expOpts='<option value="">All hives</option>'+hives.map(h=>`<option value="${h.id}">${h.name}</option>`).join('');
    ['hist-filter'].forEach(id=>{const e=el(id);if(e)e.innerHTML=hiveOpts;});
    ['hist-filter-yard'].forEach(id=>{const e=el(id);if(e)e.innerHTML=yardOpts;});
    ['exp-filter'].forEach(id=>{const e=el(id);if(e)e.innerHTML=expOpts;});
  },
};
 
UI.renderHives();
UI.populateSelects();
</script>
</body>
</html>
