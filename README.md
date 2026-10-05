# Sher_schedule
<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>My Little School - ตารางเรียนปิดเทอม</title>
<style>
:root{
  --bg:#fff8ef; --card:#fff; --text:#384152; --muted:#7b8495;
  --pink:#ff8fab; --yellow:#ffd166; --blue:#7bdff2; --green:#95d5b2;
  --purple:#b8a1ff; --orange:#ffb86b; --shadow:0 10px 30px rgba(75,65,90,.10);
}
*{box-sizing:border-box}
body{margin:0;font-family:"Trebuchet MS","Noto Sans Thai",system-ui,sans-serif;background:linear-gradient(135deg,#fff8ef,#f5fbff 55%,#fff4fa);color:var(--text)}
button,input{font:inherit}
.app{max-width:1450px;margin:auto;padding:22px}
header{display:flex;align-items:center;justify-content:space-between;gap:20px;margin-bottom:18px}
.brand{display:flex;align-items:center;gap:14px}
.logo{width:62px;height:62px;border-radius:22px;background:linear-gradient(135deg,#ffd166,#ff8fab);display:grid;place-items:center;font-size:34px;box-shadow:var(--shadow)}
h1{margin:0;font-size:clamp(25px,4vw,38px);color:#30394a}
.subtitle{color:var(--muted);margin-top:3px}
.actions{display:flex;gap:8px;flex-wrap:wrap}
.btn{border:0;border-radius:14px;padding:11px 16px;cursor:pointer;font-weight:700;transition:.2s;box-shadow:0 4px 12px rgba(50,50,70,.08)}
.btn:hover{transform:translateY(-1px)}
.btn.primary{background:#ff8fab;color:white}.btn.secondary{background:#fff;border:2px solid #eee;color:#596275}.btn.danger{background:#ffe3e8;color:#d94d68}
.layout{display:grid;grid-template-columns:310px 1fr;gap:18px}
.panel,.schedule{background:rgba(255,255,255,.9);border:1px solid rgba(255,255,255,.8);border-radius:24px;box-shadow:var(--shadow)}
.panel{padding:18px}
.panel h2,.schedule h2{margin:0 0 13px;font-size:20px}
.form{display:flex;gap:8px;margin-bottom:14px}.form input{min-width:0;flex:1;padding:12px 13px;border:2px solid #eee;border-radius:14px;outline:none}.form input:focus{border-color:var(--blue)}
.category{display:flex;gap:6px;flex-wrap:wrap;margin-bottom:15px}
.chip{border:2px solid #eee;background:#fff;border-radius:999px;padding:7px 10px;cursor:pointer;color:#667085}.chip.active{border-color:#b8a1ff;background:#f1edff;color:#654dcc}
.subject-list{display:flex;flex-direction:column;gap:9px;max-height:570px;overflow:auto;padding:2px}
.subject{display:flex;align-items:center;gap:10px;padding:12px;border-radius:16px;background:#fff;border:2px solid #f0f0f4;cursor:grab;user-select:none;box-shadow:0 3px 8px rgba(60,60,80,.04)}
.subject:active{cursor:grabbing}.subject.dragging{opacity:.45}.dot{width:13px;height:13px;border-radius:50%;flex:0 0 auto}.subject-name{font-weight:700;flex:1}.small{font-size:12px;color:var(--muted)}
.empty-list{padding:22px;text-align:center;color:#929aaa;border:2px dashed #e3e5ec;border-radius:16px}
.schedule{padding:18px;overflow:hidden}
.schedule-top{display:flex;justify-content:space-between;align-items:center;gap:10px;margin-bottom:12px}
.progress-wrap{display:flex;align-items:center;gap:10px}.progress{width:170px;height:10px;background:#eee;border-radius:99px;overflow:hidden}.progress > div{height:100%;background:linear-gradient(90deg,#95d5b2,#7bdff2);transition:.4s}
.table-wrap{overflow-x:auto}
.grid{display:grid;grid-template-columns:125px repeat(5,minmax(150px,1fr));min-width:900px;gap:8px}
.cell{min-height:155px;border-radius:18px;padding:10px;background:#fbfbfd;border:2px dashed #e5e6ec}
.head{min-height:58px;border:0;background:#f2edff;text-align:center;font-weight:800;display:flex;align-items:center;justify-content:center}
.head.mon{background:#fff0f5}.head.tue{background:#fff8dd}.head.wed{background:#eafcff}.head.thu{background:#effbee}.head.fri{background:#f2edff}
.time{background:#f7f7fa;border-style:solid;display:flex;align-items:center;justify-content:center;flex-direction:column;font-weight:800}.time span{font-size:28px}.time small{color:var(--muted)}
.dropzone.dragover{background:#eefaff;border-color:#7bdff2;transform:scale(1.01)}
.slot{height:100%;min-height:130px;position:relative}
.slot-card{height:100%;min-height:130px;border-radius:15px;padding:12px;display:flex;flex-direction:column;justify-content:space-between;color:#394150;box-shadow:0 5px 13px rgba(60,60,80,.08);animation:pop .2s ease}
@keyframes pop{from{transform:scale(.94);opacity:.5}to{transform:scale(1);opacity:1}}
.slot-card.done{background:#b9f3c6 !important;border:4px solid #35b85a;box-shadow:0 0 0 3px #e2f9e7,0 8px 18px rgba(53,184,90,.22);opacity:1;position:relative}.slot-card.done:after{content:'✓ เรียนแล้ว';position:absolute;top:-12px;right:10px;background:#35b85a;color:#fff;font-weight:900;font-size:13px;padding:6px 11px;border-radius:999px;box-shadow:0 3px 8px rgba(53,184,90,.25)}
.slot-title{font-size:17px;font-weight:900}.done .slot-title{text-decoration:line-through}
.slot-actions{display:flex;gap:6px;align-items:center}.complete{border:0;border-radius:10px;padding:8px 9px;background:#fff;color:#536071;cursor:pointer;font-weight:800;flex:1}.complete:hover{background:#f7f7f7}.remove{border:0;background:rgba(255,255,255,.7);border-radius:10px;width:36px;height:36px;cursor:pointer}
.badge{display:inline-flex;align-items:center;gap:5px;margin-top:6px;padding:5px 8px;border-radius:999px;background:rgba(255,255,255,.7);font-size:12px;font-weight:800}
.tip{margin-top:14px;padding:12px 14px;border-radius:15px;background:#fff8dd;color:#6c5a20;font-size:13px}
.footer-note{text-align:center;color:#9aa2b0;font-size:12px;margin-top:16px}
.confetti{position:fixed;pointer-events:none;z-index:20;font-size:30px;animation:fall 900ms ease-out forwards}
@keyframes fall{0%{transform:translateY(0) scale(.5);opacity:1}100%{transform:translateY(130px) rotate(25deg) scale(1.2);opacity:0}}
@media(max-width:900px){.layout{grid-template-columns:1fr}.subject-list{max-height:300px}header{align-items:flex-start;flex-direction:column}.actions{width:100%}}


/* iPhone landscape optimization */
@media (orientation: landscape) and (max-height: 500px) {
  body { padding: 8px; }
  .app { max-width: 100%; }
  header { padding: 10px 14px !important; margin-bottom: 8px !important; }
  header h1 { font-size: 20px !important; }
  header p { font-size: 11px !important; margin: 2px 0 !important; }
  .main-grid { grid-template-columns: 220px 1fr !important; gap: 8px !important; }
  .panel { padding: 10px !important; border-radius: 14px !important; }
  .panel h2 { font-size: 14px !important; margin-bottom: 7px !important; }
  .subject-list { max-height: 240px !important; overflow-y: auto; }
  .subject-card { padding: 7px !important; margin-bottom: 6px !important; min-height: 42px; }
  .subject-card .name { font-size: 12px !important; }
  .subject-card .tag { font-size: 9px !important; }
  .schedule-wrap { overflow-x: auto; }
  .schedule { min-width: 650px !important; gap: 5px !important; }
  .day-header { padding: 6px 4px !important; font-size: 12px !important; }
  .slot { min-height: 82px !important; padding: 4px !important; }
  .slot-label { font-size: 9px !important; }
  .slot-card { padding: 7px !important; min-height: 62px !important; border-radius: 10px !important; }
  .slot-card .subject-name { font-size: 11px !important; }
  .slot-card button { font-size: 9px !important; padding: 4px 6px !important; }
  .slot-card.done:after { font-size: 8px !important; padding: 2px 5px !important; top: -7px !important; right: -4px !important; }
  .empty { font-size: 10px !important; }
  .toolbar { gap: 5px !important; }
  button { min-height: 32px !important; }
}

/* iPhone portrait: keep schedule usable with horizontal scrolling */
@media (max-width: 700px) {
  body { padding: 8px; }
  .main-grid { grid-template-columns: 1fr !important; }
  .schedule-wrap { overflow-x: auto; -webkit-overflow-scrolling: touch; }
  .schedule { min-width: 720px; }
  .subject-list { max-height: 180px; overflow-y: auto; }
}

/* True iPhone landscape: everything fits in one screen, no horizontal/vertical scrolling */
@media screen and (orientation: landscape) and (max-height: 500px) {
  html, body { width:100%; height:100%; overflow:hidden; }
  body { padding:0; }
  .app { width:100%; max-width:none; height:100vh; padding:6px 8px 4px; display:flex; flex-direction:column; overflow:hidden; }

  header { flex:0 0 48px; height:48px; margin:0 0 6px; padding:0 4px; gap:8px; }
  .brand { gap:7px; min-width:0; }
  .logo { width:40px; height:40px; border-radius:13px; font-size:22px; flex:0 0 40px; }
  h1, header h1 { font-size:17px !important; line-height:1.1; white-space:nowrap; }
  .subtitle, header p { font-size:9px !important; margin:2px 0 0 !important; white-space:nowrap; }
  .actions { gap:4px; flex-wrap:nowrap; }
  .btn { padding:6px 8px; border-radius:9px; font-size:9px; white-space:nowrap; box-shadow:none; }

  .layout { flex:1 1 auto; min-height:0; width:100%; grid-template-columns:145px minmax(0,1fr) !important; gap:7px; overflow:hidden; }
  .panel, .schedule { min-width:0; min-height:0; border-radius:13px; }
  .panel { padding:8px; overflow:hidden; }
  .panel h2, .schedule h2 { font-size:12px; margin:0 0 6px; }
  .form { gap:4px; margin-bottom:6px; }
  .form input { padding:6px 7px; border-radius:8px; border-width:1px; font-size:10px; }
  .form .btn { padding:5px 7px; }
  .category { gap:3px; margin-bottom:6px; flex-wrap:nowrap; }
  .chip { padding:4px 5px; border-width:1px; font-size:8px; }
  .subject-list { max-height:none !important; height:calc(100% - 88px); overflow:hidden !important; gap:4px; padding:0; }
  .subject { min-height:0; height:36px; padding:5px 6px; gap:5px; border-radius:9px; border-width:1px; box-shadow:none; }
  .dot { width:8px; height:8px; }
  .subject-name { font-size:9px; line-height:1.1; min-width:0; overflow:hidden; text-overflow:ellipsis; white-space:nowrap; }
  .small { font-size:7px; line-height:1; }
  .remove-sub { font-size:12px !important; padding:0 !important; }

  .schedule { padding:8px; overflow:hidden; display:flex; flex-direction:column; }
  .schedule-top { flex:0 0 24px; height:24px; margin-bottom:5px; gap:5px; }
  .schedule-top h2 { margin:0; white-space:nowrap; }
  .progress-wrap { gap:4px; font-size:8px; white-space:nowrap; }
  .progress { width:65px; height:6px; }
  .table-wrap { flex:1 1 auto; min-height:0; overflow:hidden !important; }
  .grid { width:100%; min-width:0 !important; height:100%; grid-template-columns:42px repeat(5, minmax(0,1fr)); grid-template-rows:34px repeat(2, minmax(0,1fr)); gap:3px; }
  .cell { min-height:0 !important; height:auto; padding:4px; border-radius:8px; border-width:1px; overflow:hidden; }
  .head { min-height:0; font-size:9px; line-height:1; }
  .time { font-size:8px; }
  .time span { font-size:15px; }
  .time small { font-size:6px; }
  .slot { min-height:0 !important; height:100%; }
  .slot-card { min-height:0 !important; height:100%; padding:5px; border-radius:7px; box-shadow:none; }
  .slot-title { font-size:9px; line-height:1.15; display:-webkit-box; -webkit-line-clamp:2; -webkit-box-orient:vertical; overflow:hidden; }
  .badge { margin-top:2px; padding:2px 4px; font-size:6px; max-width:100%; overflow:hidden; white-space:nowrap; }
  .slot-actions { gap:3px; }
  .complete { padding:4px 3px; min-height:23px !important; border-radius:6px; font-size:7px; line-height:1; white-space:nowrap; }
  .remove { width:23px; height:23px; min-height:23px !important; padding:0; border-radius:6px; font-size:10px; }
  .slot-card.done { border-width:2px; box-shadow:0 0 0 1px #e2f9e7; }
  .slot-card.done:after { top:2px; right:2px; font-size:6px; padding:2px 4px; }
  .done .slot-title { padding-top:8px; }
  .tip, .footer-note { display:none; }
  .empty-list { padding:10px 4px; font-size:8px; }
}
</style>
</head>
<body>
<div class="app">
<header>
  <div class="brand">
    <div class="logo">🎒</div>
    <div><h1>My Little School 🌈</h1><div class="subtitle">ตารางเรียนปิดเทอมของหนูน้อย</div></div>
  </div>
  <div class="actions">
    <button class="btn secondary" id="resetWeek">🔄 รีเซ็ตตาราง</button>
    <button class="btn danger" id="clearAll">🗑️ ล้างข้อมูลทั้งหมด</button>
  </div>
</header>

<div class="layout">
  <aside class="panel">
    <h2>🧩 เนื้อหาที่จะเรียน</h2>
    <div class="form">
      <input id="subjectInput" placeholder="เช่น ฝึกอ่าน ก-ฮ, วาดรูป..." maxlength="40">
      <button class="btn primary" id="addBtn">＋ เพิ่ม</button>
    </div>
    <div class="category" id="categories">
      <button class="chip active" data-cat="ทั้งหมด">ทั้งหมด</button>
      <button class="chip" data-cat="วิชาการ">📚 วิชาการ</button>
      <button class="chip" data-cat="สร้างสรรค์">🎨 สร้างสรรค์</button>
      <button class="chip" data-cat="กิจกรรม">🏃 กิจกรรม</button>
    </div>
    <div class="subject-list" id="subjectList"></div>
    <div class="tip">💡 <b>วิธีใช้:</b> กดค้างที่ก้อนเนื้อหา แล้วลากไปใส่ช่อง <b>เช้า</b> หรือ <b>บ่าย</b> ของวันนั้นได้เลย</div>
  </aside>

  <main class="schedule">
    <div class="schedule-top">
      <div><h2>📅 ตารางเรียนสัปดาห์นี้</h2><div class="small">จันทร์ – ศุกร์ · เช้า 1 วิชา · บ่าย 1 วิชา</div></div>
      <div class="progress-wrap"><b id="progressText">0 / 10 เสร็จแล้ว</b><div class="progress"><div id="progressBar" style="width:0%"></div></div></div>
    </div>
    <div class="table-wrap"><div class="grid" id="grid"></div></div>
  </main>
</div>
<div class="footer-note">ข้อมูลจะบันทึกอัตโนมัติในเครื่องนี้ 💾 · ไม่ต้องติดตั้งโปรแกรมเพิ่มเติม</div>
</div>

<script>
const uid=()=>('id-'+Date.now().toString(36)+'-'+Math.random().toString(36).slice(2,10));
const DAYS=[
  {key:'mon',name:'จันทร์',emoji:'🌸'},
  {key:'tue',name:'อังคาร',emoji:'☀️'},
  {key:'wed',name:'พุธ',emoji:'🌊'},
  {key:'thu',name:'พฤหัสบดี',emoji:'🌱'},
  {key:'fri',name:'ศุกร์',emoji:'⭐'}
];
const TIMES=[
  {key:'morning',name:'เช้า',emoji:'🌞'},
  {key:'afternoon',name:'บ่าย',emoji:'🌤️'}
];
const colors=['#ffdce7','#fff0b8','#d8f7ff','#dff5df','#e6ddff','#ffe0c2','#d9efff','#f7d9ff'];
let state=JSON.parse(localStorage.getItem('littleSchoolV1')||'null')||{
  subjects:[
    {id:uid(),name:'ฝึกอ่าน ก-ฮ',cat:'วิชาการ'},
    {id:uid(),name:'นับเลข 1-20',cat:'วิชาการ'},
    {id:uid(),name:'วาดรูประบายสี',cat:'สร้างสรรค์'},
    {id:uid(),name:'ตัด-แปะกระดาษ',cat:'สร้างสรรค์'},
    {id:uid(),name:'เต้นประกอบเพลง',cat:'กิจกรรม'},
    {id:uid(),name:'ออกกำลังกาย',cat:'กิจกรรม'}
  ],
  schedule:{}
};
let activeCat='ทั้งหมด';
const save=()=>localStorage.setItem('littleSchoolV1',JSON.stringify(state));
const esc=s=>s.replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
function renderSubjects(){
  const box=document.getElementById('subjectList');
  const list=state.subjects.filter(s=>activeCat==='ทั้งหมด'||s.cat===activeCat);
  if(!list.length){box.innerHTML='<div class="empty-list">ยังไม่มีเนื้อหาในหมวดนี้ 😊</div>';return}
  box.innerHTML=list.map((s,i)=>`<div class="subject" draggable="true" data-id="${s.id}">
    <span class="dot" style="background:${colors[i%colors.length]}"></span>
    <div class="subject-name">${esc(s.name)}<div class="small">${s.cat}</div></div>
    <button class="remove-sub" title="ลบ" style="border:0;background:transparent;cursor:pointer;font-size:18px">×</button>
  </div>`).join('');
  box.querySelectorAll('.subject').forEach(el=>{
    el.addEventListener('dragstart',e=>{e.dataTransfer.setData('text/plain',el.dataset.id);el.classList.add('dragging')});
    el.addEventListener('dragend',()=>el.classList.remove('dragging'));
    el.querySelector('.remove-sub').addEventListener('click',e=>{
      e.stopPropagation(); if(confirm('ลบเนื้อหานี้ออกหรือไม่?')){state.subjects=state.subjects.filter(x=>x.id!==el.dataset.id);Object.keys(state.schedule).forEach(k=>{if(state.schedule[k].subjectId===el.dataset.id)delete state.schedule[k]});save();renderAll()}
    });
  });
}
function renderGrid(){
  const grid=document.getElementById('grid');
  grid.innerHTML='<div class="cell head">เวลา</div>'+DAYS.map(d=>`<div class="cell head ${d.key}">${d.emoji}<br>${d.name}</div>`).join('');
  TIMES.forEach(t=>{
    grid.innerHTML+=`<div class="cell time"><span>${t.emoji}</span>${t.name}<small>1 วิชา</small></div>`;
    DAYS.forEach(d=>{
      const key=d.key+'_'+t.key, item=state.schedule[key];
      grid.innerHTML+=`<div class="cell dropzone" data-slot="${key}">${item?renderSlot(item,key):'<div class="slot" style="display:grid;place-items:center;color:#b4bac5">ลากเนื้อหามาวางที่นี่ ✨</div>'}</div>`;
    });
  });
  grid.querySelectorAll('.dropzone').forEach(zone=>{
    zone.addEventListener('dragover',e=>{e.preventDefault();zone.classList.add('dragover')});
    zone.addEventListener('dragleave',()=>zone.classList.remove('dragover'));
    zone.addEventListener('drop',e=>{
      e.preventDefault();zone.classList.remove('dragover');
      const id=e.dataTransfer.getData('text/plain'), sub=state.subjects.find(s=>s.id===id); if(!sub)return;
      state.schedule[zone.dataset.slot]={subjectId:sub.id,name:sub.name,cat:sub.cat,done:false};
      save();renderAll();
    });
  });
  grid.querySelectorAll('.complete').forEach(btn=>btn.addEventListener('click',()=>{
    const k=btn.dataset.slot; state.schedule[k].done=!state.schedule[k].done;save();renderAll();
    if(state.schedule[k].done)celebrate(btn);
  }));
  grid.querySelectorAll('.remove-slot').forEach(btn=>btn.addEventListener('click',()=>{
    delete state.schedule[btn.dataset.slot];save();renderAll();
  }));
}
function renderSlot(item,key){
  const idx=Math.max(0,state.subjects.findIndex(s=>s.id===item.subjectId));
  return `<div class="slot-card ${item.done?'done':''}" style="background:${item.done?'#b9f3c6':colors[idx%colors.length]}">
    <div><div class="slot-title">${item.done?'✅ ':''}${esc(item.name)}</div><div class="badge">${esc(item.cat)}</div></div>
    <div class="slot-actions">
      <button class="complete" data-slot="${key}">${item.done?'↩️ ยกเลิกสถานะ':'✓ เรียนเสร็จแล้ว'}</button>
      <button class="remove remove-slot" data-slot="${key}" title="นำออก">🗑️</button>
    </div>
  </div>`;
}
function updateProgress(){
  const total=10, done=Object.values(state.schedule).filter(x=>x.done).length;
  document.getElementById('progressText').textContent=`${done} / ${total} เสร็จแล้ว`;
  document.getElementById('progressBar').style.width=(done/total*100)+'%';
}
function renderAll(){renderSubjects();renderGrid();updateProgress()}
function celebrate(el){
  ['🎉','⭐','🌈','👏','✨'].forEach((x,i)=>{
    const s=document.createElement('div');s.className='confetti';s.textContent=x;
    const r=el.getBoundingClientRect();s.style.left=(r.left+Math.random()*r.width)+'px';s.style.top=r.top+'px';s.style.animationDelay=(i*60)+'ms';
    document.body.appendChild(s);setTimeout(()=>s.remove(),1000);
  });
}
document.getElementById('addBtn').onclick=()=>{
  const input=document.getElementById('subjectInput'), name=input.value.trim(); if(!name)return;
  state.subjects.push({id:uid(),name,cat:activeCat==='ทั้งหมด'?'วิชาการ':activeCat});input.value='';save();renderAll();input.focus();
};
document.getElementById('subjectInput').addEventListener('keydown',e=>{if(e.key==='Enter')document.getElementById('addBtn').click()});
document.querySelectorAll('.chip').forEach(c=>c.onclick=()=>{
  document.querySelectorAll('.chip').forEach(x=>x.classList.remove('active'));c.classList.add('active');activeCat=c.dataset.cat;renderSubjects();
});
document.getElementById('resetWeek').onclick=()=>{
  if(confirm('ต้องการล้างเฉพาะตารางเรียนสัปดาห์นี้หรือไม่? เนื้อหาที่สร้างไว้จะยังอยู่')){
    state.schedule={};save();renderAll();
  }
};
document.getElementById('clearAll').onclick=()=>{
  if(confirm('ล้างเนื้อหาและตารางทั้งหมด?')){localStorage.removeItem('littleSchoolV1');location.reload()}
};
renderAll();
</script>
</body>
</html>
