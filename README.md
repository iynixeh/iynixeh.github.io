# Medicine Tracker

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>My Medicine Reminder</title>
<style>
:root{--s:1.15;--bg:#f6f4ee;--card:#fff;--text:#14213d;--muted:#4a5568;--line:#9aa5b1;--accent:#0b4f9e;--accent-t:#fff;--ok:#146c2e;--okbg:#e3f4e8;--bad:#a4161a;--badbg:#fde8e8;--soon:#7a4b00;--soonbg:#fff3d6;
box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#10151c;--card:#1b2430;--text:#f3f5f8;--muted:#c0c8d2;--line:#6b7886;--accent:#7db7ff;--accent-t:#06182e;--ok:#7fe0a0;--okbg:#14301e;--bad:#ff9d9d;--badbg:#3a1618;--soon:#ffd27a;--soonbg:#3a2c0e}}
:root[data-theme="dark"]{--bg:#10151c;--card:#1b2430;--text:#f3f5f8;--muted:#c0c8d2;--line:#6b7886;--accent:#7db7ff;--accent-t:#06182e;--ok:#7fe0a0;--okbg:#14301e;--bad:#ff9d9d;--badbg:#3a1618;--soon:#ffd27a;--soonbg:#3a2c0e}
*{box-sizing:border-box}
html{font-size:calc(18px * var(--s));scroll-padding-top:env(safe-area-inset-top,0px)}
body{margin:0;background:var(--bg);color:var(--text);font-family:"Atkinson Hyperlegible",Verdana,Tahoma,Arial,sans-serif;line-height:1.45;padding-bottom:110px}
main{max-width:720px;margin:0 auto;padding:14px}
h1{font-size:1.6rem;margin:.3rem 0 .6rem}h2{font-size:1.25rem;margin:1.3rem 0 .5rem}
.card{background:var(--card);border:2px solid var(--line);border-radius:16px;padding:14px;margin:12px 0}
.clock{text-align:center}.clock b{display:block;font-size:2.6rem;line-height:1.1}.clock span{font-size:1.1rem;color:var(--muted)}
button{font:inherit;font-weight:700;min-height:60px;padding:10px 18px;border-radius:14px;border:3px solid var(--accent);background:var(--card);color:var(--accent);cursor:pointer;width:100%;margin:6px 0}
button.primary{background:var(--accent);color:var(--accent-t)}
button.small{width:auto;min-height:48px;font-size:.9rem;padding:6px 14px}
button.danger{border-color:var(--bad);color:var(--bad)}
button:focus-visible,input:focus-visible,select:focus-visible{outline:4px solid #f5a300;outline-offset:2px}
label{display:block;font-weight:700;margin:12px 0 4px}
input,select{font:inherit;width:100%;min-height:56px;padding:8px 12px;border:3px solid var(--line);border-radius:12px;background:var(--card);color:var(--text)}
.now{border-width:4px}.now.due{border-color:var(--bad);background:var(--badbg)}.now.ok{border-color:var(--ok);background:var(--okbg)}
.now .big{font-size:1.5rem;font-weight:800}.now .lbl{font-weight:700;color:var(--muted)}
.row{border:2px solid var(--line);border-radius:14px;padding:12px;margin:10px 0;background:var(--card)}
.row .top{display:flex;gap:12px;align-items:baseline;flex-wrap:wrap}.row .t{font-size:1.3rem;font-weight:800}
.row small{display:block;color:var(--muted);font-size:.9rem}
.badge{display:inline-block;font-weight:800;padding:4px 10px;border-radius:999px;margin-top:6px}
.st-ok .badge{background:var(--okbg);color:var(--ok)}.st-late .badge,.st-due .badge{background:var(--badbg);color:var(--bad)}.st-later .badge{background:var(--soonbg);color:var(--soon)}
.chips{display:flex;flex-wrap:wrap;gap:8px;margin:8px 0}.chip{display:inline-flex;align-items:center;gap:6px;border:2px solid var(--line);border-radius:999px;padding:4px 12px;font-weight:700}
.chip button{min-height:40px;width:40px;padding:0;margin:0;border-radius:50%;border-width:2px}
nav{position:fixed;left:0;right:0;bottom:0;display:grid;grid-template-columns:repeat(4,1fr);background:var(--card);border-top:3px solid var(--line);padding:6px 6px calc(6px + env(safe-area-inset-bottom,0px));gap:6px;z-index:5}
nav button{margin:0;min-height:68px;font-size:15px;border-width:2px;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:2px;padding:4px}
nav button span{font-size:24px;line-height:1}nav button[aria-current="page"]{background:var(--accent);color:var(--accent-t)}
#al{position:fixed;inset:0;background:rgba(0,0,0,.7);display:flex;align-items:center;justify-content:center;padding:16px;z-index:10}
#al[hidden]{display:none}#al .box{background:var(--card);border:5px solid var(--bad);border-radius:20px;padding:18px;max-width:560px;width:100%;max-height:90%;overflow:auto}
#al h2{margin-top:0;font-size:1.6rem}.note{color:var(--muted);font-size:.9rem}.msg{font-weight:800;color:var(--bad);margin:6px 0}
.pair{display:grid;grid-template-columns:1fr 1fr;gap:10px}
input[type=file]{padding:10px}input[type=file]::file-selector-button{font:inherit;font-weight:700;min-height:48px;padding:6px 16px;margin-right:12px;border-radius:12px;border:3px solid var(--accent);background:var(--card);color:var(--accent);cursor:pointer}
textarea{font:inherit;font-size:.8rem;width:100%;min-height:130px;padding:10px;border:3px solid var(--line);border-radius:12px;background:var(--card);color:var(--text)}
details{margin-top:10px}summary{font-weight:700;min-height:48px;display:flex;align-items:center;cursor:pointer}
.okmsg{font-weight:800;color:var(--ok);margin:8px 0}
#pr{display:none}
@media print{
:root{padding:0!important}html{font-size:12pt!important}
body{background:#fff!important;color:#000!important;padding:0!important}
body>*{display:none!important}body>#pr{display:block!important}
#pr{color:#000;background:#fff;font-family:Arial,Helvetica,sans-serif;line-height:1.35;padding:0}
#pr h1{font-size:1.6rem;margin:0 0 .2rem}#pr h2{font-size:1.1rem;margin:1.1rem 0 .4rem;border-bottom:2px solid #000}
#pr table{width:100%;border-collapse:collapse}#pr th,#pr td{border:1px solid #000;padding:5px 8px;text-align:left;vertical-align:top}
#pr th{background:#e8e8e8}#pr tr{break-inside:avoid}#pr .sm{font-size:.85rem}
#pr .lines div{border-bottom:1px solid #000;height:2rem}
}
</style>
</head>
<body>
<main id="app"></main>
<div id="al" hidden role="alertdialog" aria-modal="true" aria-labelledby="alt"><div class="box" id="alb"></div></div>
<nav aria-label="Main menu" id="nav"></nav>
<div id="pr" aria-hidden="true"></div>
<script>
const $=s=>document.querySelector(s);
const esc=s=>String(s).replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
const def={scale:1.15,repeat:10,sound:true};
let S={meds:[],logs:[],set:{...def}};
try{const r=localStorage.getItem('medreminder');if(r){const p=JSON.parse(r);S.meds=p.meds||[];S.logs=p.logs||[];S.set={...def,...(p.set||{})}}}catch(e){}
const save=()=>{try{localStorage.setItem('medreminder',JSON.stringify(S))}catch(e){}};
const pad=n=>String(n).padStart(2,'0');
const dstr=(d=new Date())=>d.getFullYear()+'-'+pad(d.getMonth()+1)+'-'+pad(d.getDate());
const nowM=()=>{const d=new Date();return d.getHours()*60+d.getMinutes()};
const fmt=m=>{const h=Math.floor(m/60);return (h%12||12)+':'+pad(m%60)+(h<12?' AM':' PM')};
const parse=v=>{const p=/^(\d{1,2}):(\d{2})/.exec(v||'');return p?(+p[1])*60+(+p[2]):null};
let tab='today',draft={name:'',dose:'',t:'08:00',times:[]},note='',confirmId=null,confirmClear=false,lastMin=-1;
const tabs=[['today','📅','Today'],['meds','💊','Medicines'],['hist','📖','History'],['set','⚙️','Settings']];

function slots(){const t=dstr(),o=[];S.meds.forEach(m=>m.times.forEach(tm=>o.push({m,tm,l:S.logs.find(x=>x.date===t&&x.medId===m.id&&x.sched===tm)})));return o.sort((a,b)=>a.tm-b.tm||a.m.name.localeCompare(b.m.name))}
function take(id,sc){const m=S.meds.find(x=>x.id===id);if(!m)return;S.logs.push({date:dstr(),at:nowM(),medId:id,sched:sc,n:m.name+(m.dose?' '+m.dose:'')});save();render();refreshAlert()}
function undo(id,sc){const t=dstr(),i=S.logs.findIndex(x=>x.date===t&&x.medId===id&&x.sched===sc);if(i>=0)S.logs.splice(i,1);save();render()}
function status(s){const n=nowM();if(s.l)return['ok','✔ Taken at '+fmt(s.l.at)];if(s.tm<n)return['late','⚠ Overdue'];if(s.tm===n)return['due','⏰ Time now'];return['later','🕑 Later today']}

function render(){
  document.documentElement.style.setProperty('--s',S.set.scale);
  $('#nav').innerHTML=tabs.map(t=>`<button onclick="go('${t[0]}')" ${tab===t[0]?'aria-current="page"':''}><span aria-hidden="true">${t[1]}</span>${t[2]}</button>`).join('');
  $('#app').innerHTML=({today:vToday,meds:vMeds,hist:vHist,set:vSet})[tab]();
}
function go(t){tab=t;confirmId=null;confirmClear=false;note='';bmsg='';pend=null;render();window.scrollTo(0,0)}

function vToday(){
  const d=new Date(),sl=slots();
  let h=`<div class="card clock"><b id="clk">${fmt(nowM())}</b><span>${d.toLocaleDateString(undefined,{weekday:'long',month:'long',day:'numeric'})}</span></div>`;
  const lb=S.set.lastBackup,stale=!lb||(new Date(dstr())-new Date(lb))/864e5>14;
  if(S.meds.length&&stale)h+=`<div class="card"><b>💾 Tip:</b> save a backup copy so you never lose your list.<button class="small" onclick="go('set')">Go to backup</button></div>`;
  if(!S.meds.length)return h+`<div class="card"><h1>Welcome!</h1><p>This helper reminds you when to take your medicine and keeps a record.</p><button class="primary" onclick="go('meds')">＋ Add my first medicine</button><p class="note">Reminders only sound while this page is open on your screen.</p></div>`;
  const next=sl.find(s=>!s.l);
  if(!sl.length)h+=`<div class="card">No times are set yet. Go to “Medicines” to add one.</div>`;
  else if(!next)h+=`<div class="card now ok"><div class="big">🎉 All done for today!</div><div class="lbl">You have taken every dose.</div></div>`;
  else{const st=status(next)[0],isDue=st==='late'||st==='due';
    h+=`<div class="card now ${isDue?'due':''}"><div class="lbl">${isDue?'TAKE NOW':'NEXT MEDICINE'} — ${fmt(next.tm)}</div><div class="big">${esc(next.m.name)}</div><div>${esc(next.m.dose)}</div><button class="primary" onclick="take(${next.m.id},${next.tm})">✔ I took it</button></div>`}
  if(sl.length){h+=`<h2>Today’s medicines</h2>`;
    h+=sl.map(s=>{const[c,l]=status(s);return `<div class="row st-${c}"><div class="top"><span class="t">${fmt(s.tm)}</span><span><b>${esc(s.m.name)}</b><small>${esc(s.m.dose)}</small></span></div><span class="badge">${l}</span>${s.l?`<button class="small" onclick="undo(${s.m.id},${s.tm})">Undo (tapped by mistake)</button>`:`<button onclick="take(${s.m.id},${s.tm})">I took this one</button>`}</div>`}).join('')}
  return h}

function vMeds(){
  let h=`<h1>My medicines</h1>`;
  if(!S.meds.length)h+=`<div class="card">Nothing added yet. Use the form below.</div>`;
  h+=S.meds.map(m=>`<div class="card"><b style="font-size:1.3rem">${esc(m.name)}</b><div>${esc(m.dose)}</div><div class="chips">${m.times.map(t=>`<span class="chip">${fmt(t)}</span>`).join('')||'<span class="note">No set times</span>'}</div><button onclick="extra(${m.id})">I took an extra dose now</button>${confirmId===m.id?`<button class="danger" onclick="removeMed(${m.id})">Tap again to remove for good</button>`:`<button class="danger" onclick="confirmId=${m.id};render()">Remove this medicine</button>`}</div>`).join('');
  h+=`<h2>Add a medicine</h2><div class="card"><label for="dn">Medicine name</label><input id="dn" value="${esc(draft.name)}" oninput="draft.name=this.value" autocomplete="off">
<label for="dd">Dose (for example 500 mg, or 10 units)</label><input id="dd" value="${esc(draft.dose)}" oninput="draft.dose=this.value" autocomplete="off">
<label for="dt">What time do you take it?</label><input id="dt" type="time" value="${draft.t}" oninput="draft.t=this.value">
<button onclick="addTime()">＋ Add this time</button>
<div class="chips">${draft.times.map(t=>`<span class="chip">${fmt(t)}<button aria-label="Remove ${fmt(t)}" onclick="delTime(${t})">✕</button></span>`).join('')}</div>
${note?`<div class="msg" role="alert">${esc(note)}</div>`:''}
<button class="primary" onclick="saveMed()">✔ Save this medicine</button></div>`;
  return h}
function addTime(){const t=parse(draft.t);if(t===null){note='Please choose a time first.';return render()}if(!draft.times.includes(t))draft.times.push(t);draft.times.sort((a,b)=>a-b);note='';render()}
function delTime(t){draft.times=draft.times.filter(x=>x!==t);render()}
function saveMed(){if(!draft.name.trim()){note='Please type the medicine name.';return render()}
  const t=parse(draft.t);if(!draft.times.length&&t!==null&&!note)draft.times.push(t);
  if(!draft.times.length){note='Please add at least one time.';return render()}
  const id=S.meds.reduce((a,m)=>Math.max(a,m.id),0)+1;S.meds.push({id,name:draft.name.trim(),dose:draft.dose.trim(),times:[...draft.times]});save();
  draft={name:'',dose:'',t:'08:00',times:[]};note='';go('today')}
function removeMed(id){S.meds=S.meds.filter(m=>m.id!==id);confirmId=null;save();render()}
function extra(id){take(id,-1);go('today')}

function vHist(){
  let h=`<h1>History</h1><p class="note">The last 7 days.</p>`,any=false;
  for(let i=0;i<7;i++){const d=new Date();d.setDate(d.getDate()-i);const k=dstr(d);
    const es=S.logs.filter(x=>x.date===k).sort((a,b)=>a.at-b.at);if(!es.length)continue;any=true;
    const lab=i===0?'Today':i===1?'Yesterday':d.toLocaleDateString(undefined,{weekday:'long',month:'long',day:'numeric'});
    h+=`<h2>${lab}</h2>`+es.map(e=>`<div class="row"><b>${fmt(e.at)}</b> — ${esc(e.n)}<small>${e.sched<0?'Extra dose':(e.at-e.sched>30?'Taken late (planned '+fmt(e.sched)+')':'On time')}</small></div>`).join('')}
  return h+(any?'':`<div class="card">Nothing recorded yet.</div>`)+`<h2>Print a report</h2><div class="card"><b>🖨 For my doctor</b>
<label for="rn">My name (optional)</label><input id="rn" value="${esc(rep.name)}" oninput="rep.name=this.value" autocomplete="off">
<label for="rd">How far back?</label><select id="rd" onchange="rep.days=+this.value">${[[7,'Last 7 days'],[14,'Last 14 days'],[30,'Last 30 days'],[90,'Last 90 days']].map(o=>`<option value="${o[0]}" ${rep.days===o[0]?'selected':''}>${o[1]}</option>`).join('')}</select>
<button class="primary" onclick="printReport()">🖨 Print this report</button>
<p class="note">The print window on your device also lets you save the report as a PDF to email.</p></div>`}

function vSet(){
  const perm='Notification' in window?Notification.permission:'unsupported';
  return `<h1>Settings</h1>
<div class="card"><b>Text size</b><div class="pair"><button onclick="size(-.15)">A− Smaller</button><button onclick="size(.15)">A+ Larger</button></div></div>
<div class="card"><label for="rp">If I forget, remind me again</label><select id="rp" onchange="S.set.repeat=+this.value;save()">${[[5,'every 5 minutes'],[10,'every 10 minutes'],[15,'every 15 minutes'],[30,'every 30 minutes'],[0,'never (only once)']].map(o=>`<option value="${o[0]}" ${S.set.repeat===o[0]?'selected':''}>${o[1]}</option>`).join('')}</select>
<button onclick="S.set.sound=!S.set.sound;save();render()">🔔 Sound: ${S.set.sound?'ON':'OFF'} (tap to change)</button>
<button onclick="askPerm()">📲 Pop-up alerts: ${perm==='granted'?'ON':perm==='denied'?'Blocked in browser':perm==='unsupported'?'Not available':'Tap to turn on'}</button>
<button onclick="testAlert()">▶ Try a test reminder</button>
<p class="note">Reminders only work while this page is open. Keep it open on your phone or computer during the day, with the sound turned up.</p></div>
${vBackup()}
<div class="card"><p class="note">Your information stays on this device only. This is a record-keeping helper, not medical advice. Always follow your doctor’s instructions.</p>
${confirmClear?`<button class="danger" onclick="S.meds=[];S.logs=[];save();confirmClear=false;go('today')">Tap again to erase everything</button>`:`<button class="danger" onclick="confirmClear=true;render()">Erase all my information</button>`}</div>`}
function size(d){S.set.scale=Math.min(1.6,Math.max(.95,+(S.set.scale+d).toFixed(2)));save();render()}
function askPerm(){try{Notification.requestPermission().then(render)}catch(e){}}
function testAlert(){beep();showAlert([],true)}

/* ---- Backup & restore ---- */
let bmsg='',bok=false,pend=null,bkText='',bkOpen=false;
function backupData(){return JSON.stringify({app:'medreminder',v:1,saved:new Date().toISOString(),meds:S.meds,logs:S.logs,set:S.set},null,1)}
function vBackup(){
  const lb=S.set.lastBackup;
  if(pend)return `<div class="card now due"><div class="big">Replace what is on this device?</div><p>The backup has <b>${pend.meds.length}</b> medicine(s) and <b>${pend.logs.length}</b> dose record(s). Your current list on this device will be replaced.</p><button class="primary" onclick="applyRestore()">Yes, restore the backup</button><button onclick="pend=null;bmsg='';render()">No, cancel</button></div>`;
  return `<div class="card"><b>💾 Backup</b><p class="note">${lb?'Last backup: '+esc(lb):'You have not saved a backup yet.'} A backup lets you move to a new phone or recover your list.</p>
<button class="primary" onclick="saveBackup()">💾 Save a backup file</button>
<label for="bf">Restore from a backup file</label><input id="bf" type="file" accept=".json,application/json" onchange="onFile(this)">
${bmsg?`<div class="${bok?'okmsg':'msg'}" role="status">${esc(bmsg)}</div>`:''}
<details ${bkOpen?'open':''} ontoggle="bkOpen=this.open"><summary>Other way: copy and paste</summary>
<button onclick="bkText=backupData();bkOpen=true;render()">Show my backup as text</button>
<textarea id="bk" aria-label="Backup text" oninput="bkText=this.value">${esc(bkText)}</textarea>
<button onclick="copyText()">Copy this text</button><button onclick="restoreText()">Restore from the text in the box</button></details></div>`}
async function saveBackup(){
  const name='medicine-backup-'+dstr()+'.json',data=backupData();bok=false;
  try{
    let dl=null;try{dl=window.claude&&await claude.use('downloads')}catch(e){}
    if(dl)await dl.save({filename:name,data});
    else if(window.claude)throw{code:'unavailable'};
    else{const a=document.createElement('a');a.href=URL.createObjectURL(new Blob([data],{type:'application/json'}));a.download=name;document.body.appendChild(a);a.click();a.remove()}
    S.set.lastBackup=dstr();save();bok=true;bmsg='✔ Backup saved. Keep the file somewhere safe, such as in an email to yourself.'
  }catch(e){bmsg=e&&e.code==='declined'?'Backup was cancelled.':'Saving a file is not available here. Please use “Other way: copy and paste” below.'}
  render()}
function readBackup(txt){let o;try{o=JSON.parse(txt)}catch(e){return null}
  if(!o||o.app!=='medreminder'||!Array.isArray(o.meds)||!Array.isArray(o.logs))return null;
  const n=Number.isFinite,st=o.set&&typeof o.set==='object'?o.set:{};
  return{meds:o.meds.filter(m=>m&&n(m.id)&&typeof m.name==='string'&&Array.isArray(m.times)).map(m=>({id:m.id,name:m.name.slice(0,80),dose:String(m.dose||'').slice(0,80),times:m.times.filter(t=>n(t)&&t>=0&&t<1440)})),
   logs:o.logs.filter(l=>l&&typeof l.date==='string'&&n(l.at)&&n(l.medId)&&n(l.sched)).map(l=>({date:l.date,at:l.at,medId:l.medId,sched:l.sched,n:String(l.n||'').slice(0,160)})),
   set:{scale:n(st.scale)?Math.min(1.6,Math.max(.95,st.scale)):def.scale,repeat:n(st.repeat)?st.repeat:def.repeat,sound:st.sound!==false,lastBackup:typeof st.lastBackup==='string'?st.lastBackup:undefined}}}
function tryRestore(txt){pend=readBackup(txt);bok=false;bmsg=pend?'':'That does not look like a backup from this app.';render()}
function onFile(inp){const f=inp.files&&inp.files[0];if(!f)return;const r=new FileReader();r.onload=()=>tryRestore(String(r.result));r.onerror=()=>{bok=false;bmsg='Could not read that file.';render()};r.readAsText(f)}
function restoreText(){tryRestore(bkText)}
function applyRestore(){S.meds=pend.meds;S.logs=pend.logs;S.set=pend.set;pend=null;save();bok=true;bmsg='✔ Your information was restored.';bkText='';render()}
async function copyText(){const t=bkText||backupData();bkText=t;bok=false;try{await navigator.clipboard.writeText(t);bok=true;bmsg='✔ Copied. Paste it into an email or note to yourself.'}catch(e){bmsg='Could not copy automatically. Press and hold the text in the box, then choose Select All and Copy.'}render()}

/* ---- Printable report ---- */
let rep={days:7,name:''};
function buildReport(){
  const f=d=>d.toLocaleDateString(undefined,{month:'short',day:'numeric',year:'numeric'});
  const keys=[];for(let i=rep.days-1;i>=0;i--){const d=new Date();d.setDate(d.getDate()-i);keys.push([dstr(d),d])}
  const set=new Set(keys.map(k=>k[0])),L=S.logs.filter(l=>set.has(l.date));
  const sc=L.filter(l=>l.sched>=0),on=sc.filter(l=>l.at-l.sched<=30).length,late=sc.length-on,ex=L.length-sc.length;
  const rows=keys.map(([k,d])=>{const es=L.filter(l=>l.date===k).sort((a,b)=>a.at-b.at),ds=d.toLocaleDateString(undefined,{weekday:'short',month:'short',day:'numeric'});
    if(!es.length)return `<tr><td>${ds}</td><td colspan="3" class="sm">No doses recorded</td></tr>`;
    return es.map((e,i)=>`<tr><td>${i?'':ds}</td><td>${fmt(e.at)}</td><td>${esc(e.n)}</td><td class="sm">${e.sched<0?'Extra dose':e.at-e.sched>30?'Late (planned '+fmt(e.sched)+')':'On time'}</td></tr>`).join('')}).join('');
  const meds=S.meds.length?S.meds.map(m=>`<tr><td>${esc(m.name)}</td><td>${esc(m.dose)}</td><td>${m.times.map(fmt).join(', ')||'As needed'}</td></tr>`).join(''):'<tr><td colspan="3">None saved</td></tr>';
  return `<h1>Medicine Record</h1><div>${rep.name.trim()?'<b>Name:</b> '+esc(rep.name.trim())+' &nbsp; ':''}<b>Period:</b> ${f(keys[0][1])} – ${f(keys[keys.length-1][1])} &nbsp; <b>Printed:</b> ${f(new Date())}</div>
<h2>Current medicines</h2><table><tr><th>Medicine</th><th>Dose</th><th>Daily times</th></tr>${meds}</table>
<h2>Summary</h2><div>Doses recorded: <b>${L.length}</b> &nbsp;|&nbsp; On time: <b>${on}</b> &nbsp;|&nbsp; Taken late (over 30 min): <b>${late}</b> &nbsp;|&nbsp; Extra doses: <b>${ex}</b></div>
<h2>Day by day</h2><table><tr><th>Date</th><th>Time taken</th><th>Medicine</th><th>Note</th></tr>${rows}</table>
<h2>Notes for my doctor</h2><div class="lines"><div></div><div></div><div></div></div>
<p class="sm">Recorded by the patient in the My Medicine Reminder app. It is a personal log, not an official medical record.</p>`}
function printReport(){$('#pr').innerHTML=buildReport();try{window.print()}catch(e){alert('Printing is not available here. Try opening this page in your browser.')}}

/* ---- Reminders (ping) ---- */
const last={};
function beep(){if(!S.set.sound)return;try{const a=new(window.AudioContext||window.webkitAudioContext)();[0,.4,.8].forEach(d=>{const o=a.createOscillator(),g=a.createGain();o.frequency.value=880;g.gain.value=.25;o.connect(g);g.connect(a.destination);o.start(a.currentTime+d);o.stop(a.currentTime+d+.25)})}catch(e){}try{navigator.vibrate&&navigator.vibrate([300,150,300])}catch(e){}}
function pending(){const n=nowM();return slots().filter(s=>!s.l&&s.tm<=n)}
function showAlert(list,test){
  const body=test?`<p>This is a test. Real reminders look like this.</p><button class="primary" onclick="closeAlert()">OK</button>`:
  list.map(s=>`<div class="card"><div class="lbl">${fmt(s.tm)}</div><div style="font-size:1.4rem;font-weight:800">${esc(s.m.name)}</div><div>${esc(s.m.dose)}</div><button class="primary" onclick="take(${s.m.id},${s.tm})">✔ I took it</button></div>`).join('')+`<button onclick="closeAlert()">Remind me again later</button>`;
  $('#alb').innerHTML=`<h2 id="alt">⏰ Time for your medicine</h2>`+body;$('#al').hidden=false;const b=$('#alb button');b&&b.focus()}
function closeAlert(){$('#al').hidden=true}
function refreshAlert(){if($('#al').hidden)return;const p=pending();p.length?showAlert(p):closeAlert()}
function check(){const t=dstr(),n=nowM();let fresh=false;
  pending().forEach(s=>{const k=t+'_'+s.m.id+'_'+s.tm,r=S.set.repeat;if(last[k]===undefined||(r>0&&n-last[k]>=r)){last[k]=n;fresh=true}});
  if(!fresh)return;const p=pending();beep();showAlert(p);
  try{if('Notification' in window&&Notification.permission==='granted')new Notification('Time for your medicine',{body:p.map(s=>s.m.name+' '+s.m.dose).join(', ')})}catch(e){}}
setInterval(()=>{const c=$('#clk');if(c)c.textContent=fmt(nowM());const m=nowM();if(m!==lastMin){lastMin=m;if(tab==='today'&&$('#al').hidden)render()}check()},10000);
render();setTimeout(check,1500);
</script>
</body>
</html>
