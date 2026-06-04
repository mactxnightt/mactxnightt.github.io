Progreso semanal.
<style>
.sr-only{position:absolute;width:1px;height:1px;padding:0;margin:-1px;overflow:hidden;clip:rect(0,0,0,0);border:0}
.card{background:var(--color-background-primary);border:0.5px solid var(--color-border-tertiary);border-radius:var(--border-radius-lg);padding:1rem 1.25rem;margin-bottom:10px}
.section-label{font-size:11px;font-weight:500;color:var(--color-text-secondary);text-transform:uppercase;letter-spacing:0.5px;margin:0 0 8px}
.metric-row{display:grid;grid-template-columns:1fr auto 90px;gap:8px;align-items:center;padding:7px 0;border-top:0.5px solid var(--color-border-tertiary)}
.metric-name{font-size:13px;color:var(--color-text-primary)}
.metric-tool{font-size:11px;color:var(--color-text-secondary)}
.metric-input{width:80px;font-size:13px;text-align:right;padding:4px 8px;border:0.5px solid var(--color-border-secondary);border-radius:var(--border-radius-md);background:var(--color-background-secondary);color:var(--color-text-primary)}
.metric-input:focus{outline:none;border-color:var(--color-border-primary)}
.week-tab{padding:6px 14px;font-size:12px;border-radius:var(--border-radius-md);border:0.5px solid var(--color-border-secondary);cursor:pointer;background:transparent;color:var(--color-text-secondary)}
.week-tab.active{background:#EEEDFE;color:#3C3489;border-color:#AFA9EC;font-weight:500}
.week-tab.p2{background:#E1F5EE;color:#085041;border-color:#5DCAA5}
.week-tab.p3{background:#FAEEDA;color:#633806;border-color:#EF9F27}
.score-box{display:flex;align-items:center;gap:12px;padding:10px 14px;border-radius:var(--border-radius-md);background:var(--color-background-secondary);margin-bottom:10px}
.score-num{font-size:28px;font-weight:500;color:var(--color-text-primary)}
.score-label{font-size:12px;color:var(--color-text-secondary);line-height:1.4}
.bar-wrap{height:6px;background:var(--color-border-tertiary);border-radius:3px;margin-top:6px;flex:1}
.bar-fill{height:6px;border-radius:3px;transition:width 0.4s ease}
.habit-check{display:flex;align-items:center;gap:8px;padding:6px 0;border-top:0.5px solid var(--color-border-tertiary);font-size:13px;color:var(--color-text-primary);cursor:pointer}
.habit-check input{width:16px;height:16px;accent-color:#534AB7;cursor:pointer}
.reflection-box{width:100%;min-height:60px;font-size:13px;padding:8px 10px;border:0.5px solid var(--color-border-secondary);border-radius:var(--border-radius-md);background:var(--color-background-secondary);color:var(--color-text-primary);resize:vertical;font-family:var(--font-sans)}
.reflection-box:focus{outline:none;border-color:var(--color-border-primary)}
.tabs-wrap{display:flex;gap:6px;flex-wrap:wrap;margin-bottom:14px}
.phase-label{font-size:11px;font-weight:500;padding:3px 8px;border-radius:20px;margin-right:4px}
</style>

<h2 class="sr-only">Tracker interactivo de progreso semanal para aprender marketing digital en 90 días</h2>

<div style="padding:1rem 0">

  <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:4px;flex-wrap:wrap;gap:8px">
    <div>
      <p style="font-size:18px;font-weight:500;margin:0;color:var(--color-text-primary)">Tracker semanal de progreso</p>
      <p style="font-size:13px;color:var(--color-text-secondary);margin:3px 0 0">Registra tus métricas cada viernes · 90 días</p>
    </div>
    <button onclick="saveAll()" style="font-size:12px"><i class="ti ti-download" aria-hidden="true" style="font-size:14px;margin-right:4px"></i>Guardar registro ↗</button>
  </div>

  <div class="tabs-wrap" id="tabs"></div>

  <div id="main-content"></div>

</div>

<script>
const phases = [
  {num:1,weeks:[1,2,3,4],label:"Fase 1",tabClass:"",color:"#534AB7"},
  {num:2,weeks:[5,6,7,8,9,10],label:"Fase 2",tabClass:"p2",color:"#0F6E56"},
  {num:3,weeks:[11,12,13],label:"Fase 3",tabClass:"p3",color:"#854F0B"}
];

const weekData = {
  1:{title:"Fundamentos generales",metrics:[
    {id:"concepts",name:"Conceptos anotados",tool:"Cuaderno / Notion",unit:"conceptos",ph:"ej. 12"},
    {id:"modules",name:"Módulos completados",tool:"Google Digital Garage",unit:"módulos",ph:"ej. 3"},
    {id:"time",name:"Minutos de estudio",tool:"Cualquier timer",unit:"min",ph:"ej. 180"},
  ],habits:[
    "Leí al menos 1 recurso por día",
    "Tomé notas o resumen cada día",
    "Analicé una marca real el sábado"
  ]},
  2:{title:"Buyer persona",metrics:[
    {id:"concepts",name:"Conceptos anotados",tool:"Cuaderno / Notion",unit:"conceptos",ph:"ej. 15"},
    {id:"personas",name:"Buyer personas creados",tool:"Plantilla propia",unit:"personas",ph:"ej. 2"},
    {id:"time",name:"Minutos de estudio",tool:"Cualquier timer",unit:"min",ph:"ej. 200"},
  ],habits:[
    "Completé al menos 1 buyer persona",
    "Exploré Google Trends",
    "Dibujé un customer journey"
  ]},
  3:{title:"Contenido y copywriting",metrics:[
    {id:"posts",name:"Piezas de contenido creadas",tool:"Canva / Google Docs",unit:"piezas",ph:"ej. 3"},
    {id:"copies",name:"Titulares escritos con fórmulas",tool:"Cuaderno",unit:"titulares",ph:"ej. 6"},
    {id:"time",name:"Minutos de estudio",tool:"Cualquier timer",unit:"min",ph:"ej. 210"},
  ],habits:[
    "Diseñé al menos 1 imagen con Canva",
    "Escribí al menos 1 post completo",
    "Analicé 3 posts exitosos el sábado"
  ]},
  4:{title:"Cierre Fase 1 · Certificación",metrics:[
    {id:"cert",name:"Certificación Google completada",tool:"Google Digital Garage",unit:"(0 o 1)",ph:"0 o 1"},
    {id:"modules",name:"Módulos totales completados",tool:"Google Digital Garage",unit:"módulos",ph:"ej. 26"},
    {id:"time",name:"Minutos totales Fase 1",tool:"Suma de semanas",unit:"min",ph:"ej. 800"},
  ],habits:[
    "Rendí el examen de certificación",
    "Definí mi canal para Fase 2",
    "Compartí el certificado en LinkedIn"
  ]},
  5:{title:"SEO fundamentos",metrics:[
    {id:"keywords",name:"Keywords investigadas",tool:"Google Keyword Planner",unit:"keywords",ph:"ej. 20"},
    {id:"articles",name:"Artículos optimizados con SEO",tool:"Blog / Google Docs",unit:"artículos",ph:"ej. 1"},
    {id:"time",name:"Minutos de práctica SEO",tool:"Timer",unit:"min",ph:"ej. 200"},
  ],habits:[
    "Creé cuenta en Google Search Console",
    "Optimicé al menos 1 pieza de contenido",
    "Analicé páginas top en mi nicho"
  ]},
  6:{title:"Redes sociales orgánicas",metrics:[
    {id:"posts",name:"Posts publicados",tool:"Instagram / LinkedIn",unit:"posts",ph:"ej. 3"},
    {id:"reach",name:"Alcance total",tool:"Estadísticas de la red",unit:"personas",ph:"ej. 150"},
    {id:"engagement",name:"Interacciones totales",tool:"Estadísticas de la red",unit:"interacciones",ph:"ej. 20"},
  ],habits:[
    "Publiqué al menos 2 posts esta semana",
    "Respondí todos los comentarios",
    "Creé un calendario de contenido"
  ]},
  7:{title:"Email marketing",metrics:[
    {id:"subs",name:"Suscriptores en lista",tool:"Mailchimp / Brevo",unit:"contactos",ph:"ej. 10"},
    {id:"emails",name:"Emails diseñados",tool:"Mailchimp / Brevo",unit:"emails",ph:"ej. 3"},
    {id:"openrate",name:"Open rate del email de prueba",tool:"Mailchimp stats",unit:"%",ph:"ej. 40"},
  ],habits:[
    "Creé cuenta en Mailchimp o Brevo",
    "Envié al menos 1 email de prueba",
    "Me suscribí a 3 newsletters del nicho"
  ]},
  8:{title:"Publicidad pagada (intro)",metrics:[
    {id:"ads",name:"Anuncios redactados",tool:"Google Docs",unit:"anuncios",ph:"ej. 3"},
    {id:"creatives",name:"Creativos diseñados",tool:"Canva",unit:"creativos",ph:"ej. 2"},
    {id:"time",name:"Minutos explorando Ads Manager",tool:"Meta / Google",unit:"min",ph:"ej. 90"},
  ],habits:[
    "Exploré Google Ads sin gastar dinero",
    "Diseñé creativos de un anuncio",
    "Identifiqué anuncios reales en mi feed"
  ]},
  9:{title:"Google Analytics 4",metrics:[
    {id:"events",name:"Eventos configurados en GA4",tool:"Google Analytics 4",unit:"eventos",ph:"ej. 4"},
    {id:"utms",name:"URLs con UTMs creadas",tool:"Campaign URL Builder",unit:"URLs",ph:"ej. 3"},
    {id:"time",name:"Minutos explorando GA4",tool:"Timer",unit:"min",ph:"ej. 120"},
  ],habits:[
    "Exploré la cuenta demo de GA4",
    "Creé al menos 3 URLs con UTMs",
    "Identifiqué mis 5 métricas clave"
  ]},
  10:{title:"Cierre Fase 2 · Certificación",metrics:[
    {id:"cert",name:"Certificación HubSpot completada",tool:"HubSpot Academy",unit:"(0 o 1)",ph:"0 o 1"},
    {id:"channels",name:"Canales dominados",tool:"Autoevaluación",unit:"canales",ph:"ej. 3"},
    {id:"pieces",name:"Piezas creadas en Fase 2",tool:"Portafolio",unit:"piezas",ph:"ej. 12"},
  ],habits:[
    "Rendí la certificación de HubSpot",
    "Definí mi proyecto para Fase 3",
    "Conecté GA4 + Search Console"
  ]},
  11:{title:"Lanzamiento del proyecto",metrics:[
    {id:"posts",name:"Piezas publicadas",tool:"Canal elegido",unit:"piezas",ph:"ej. 3"},
    {id:"reach",name:"Alcance total",tool:"GA4 / redes",unit:"personas",ph:"ej. 80"},
    {id:"subs",name:"Suscriptores / seguidores nuevos",tool:"Canal elegido",unit:"personas",ph:"ej. 5"},
  ],habits:[
    "Publiqué la primera pieza del proyecto",
    "Configuré el seguimiento en GA4",
    "Envié mi primera newsletter real"
  ]},
  12:{title:"Optimización y pruebas",metrics:[
    {id:"abtest",name:"Pruebas A/B realizadas",tool:"Email / redes",unit:"pruebas",ph:"ej. 2"},
    {id:"growth",name:"Crecimiento de alcance vs sem 11",tool:"GA4 / redes",unit:"%",ph:"ej. 15"},
    {id:"pieces",name:"Piezas publicadas esta semana",tool:"Canal elegido",unit:"piezas",ph:"ej. 4"},
  ],habits:[
    "Hice al menos 1 prueba A/B",
    "Documenté los resultados del test",
    "Programé contenido para sem. 13"
  ]},
  13:{title:"Portfolio y cierre de 90 días",metrics:[
    {id:"casestudy",name:"Case study redactado",tool:"LinkedIn / Notion",unit:"(0 o 1)",ph:"0 o 1"},
    {id:"totalpieces",name:"Total de piezas creadas (90 días)",tool:"Portafolio",unit:"piezas",ph:"ej. 25"},
    {id:"certs",name:"Certificaciones obtenidas",tool:"Google / HubSpot",unit:"certs",ph:"ej. 2"},
  ],habits:[
    "Publiqué mi case study en LinkedIn",
    "Actualicé mi perfil con habilidades",
    "Planifiqué los próximos 90 días"
  ]},
};

function getPhaseForWeek(w){
  for(const p of phases) if(p.weeks.includes(w)) return p;
  return phases[0];
}

function getStorage(){
  try{return JSON.parse(localStorage.getItem('md_tracker')||'{}')}catch(e){return{}}
}
function setStorage(d){
  try{localStorage.setItem('md_tracker',JSON.stringify(d))}catch(e){}
}

let currentWeek = 1;
const store = getStorage();

function renderTabs(){
  const tabs = document.getElementById('tabs');
  tabs.innerHTML = '';
  phases.forEach(ph => {
    const grp = document.createElement('div');
    grp.style.cssText = 'display:flex;align-items:center;gap:4px;flex-wrap:wrap';
    const lbl = document.createElement('span');
    lbl.className = 'phase-label';
    const colors = [{bg:'#EEEDFE',tc:'#3C3489'},{bg:'#E1F5EE',tc:'#085041'},{bg:'#FAEEDA',tc:'#633806'}];
    const c = colors[ph.num-1];
    lbl.style.cssText = `background:${c.bg};color:${c.tc}`;
    lbl.textContent = ph.label;
    grp.appendChild(lbl);
    ph.weeks.forEach(w => {
      const btn = document.createElement('button');
      btn.className = 'week-tab' + (ph.num>1?' '+['','p2','p3'][ph.num-1]:'');
      if(w===currentWeek) btn.classList.add('active');
      btn.textContent = `S${w}`;
      btn.onclick = () => { currentWeek = w; renderTabs(); renderContent(); };
      grp.appendChild(btn);
    });
    tabs.appendChild(grp);
  });
}

function getScore(){
  const d = store[currentWeek]||{};
  const wd = weekData[currentWeek];
  let filled = 0, total = wd.metrics.length + wd.habits.length;
  wd.metrics.forEach(m => { if(d['m_'+m.id] && d['m_'+m.id]!=='') filled++; });
  wd.habits.forEach((h,i) => { if(d['h_'+i]) filled++; });
  return {filled, total, pct: total>0 ? Math.round(filled/total*100) : 0};
}

function renderContent(){
  const wd = weekData[currentWeek];
  const ph = getPhaseForWeek(currentWeek);
  const d = store[currentWeek]||{};
  const score = getScore();
  const colors = [{bg:'#534AB7'},{bg:'#0F6E56'},{bg:'#854F0B'}];
  const barColor = colors[ph.num-1].bg;

  let html = `
  <div class="score-box">
    <div>
      <div class="score-num">${score.pct}%</div>
      <div style="font-size:11px;color:var(--color-text-secondary)">completado esta semana</div>
    </div>
    <div style="flex:1">
      <div style="font-size:13px;font-weight:500;color:var(--color-text-primary);margin-bottom:6px">Semana ${currentWeek} · ${wd.title}</div>
      <div class="bar-wrap"><div class="bar-fill" style="width:${score.pct}%;background:${barColor}"></div></div>
      <div style="font-size:11px;color:var(--color-text-secondary);margin-top:4px">${score.filled} de ${score.total} ítems registrados</div>
    </div>
  </div>

  <div class="card">
    <div class="section-label"><i class="ti ti-chart-bar" aria-hidden="true" style="font-size:13px;margin-right:4px"></i>Métricas de la semana</div>
    <div style="display:grid;grid-template-columns:1fr auto 90px;gap:6px;padding-bottom:4px">
      <span style="font-size:11px;color:var(--color-text-secondary)">Qué medir</span>
      <span style="font-size:11px;color:var(--color-text-secondary)">Dónde encontrarlo</span>
      <span style="font-size:11px;color:var(--color-text-secondary);text-align:right">Tu número</span>
    </div>
  `;

  wd.metrics.forEach(m => {
    html += `
    <div class="metric-row">
      <div><div class="metric-name">${m.name}</div><div class="metric-tool">${m.tool} · ${m.unit}</div></div>
      <div></div>
      <input class="metric-input" type="number" placeholder="${m.ph}" value="${d['m_'+m.id]||''}" 
        onchange="saveMetric('${m.id}', this.value)" oninput="saveMetric('${m.id}', this.value)" />
    </div>`;
  });

  html += `</div>
  <div class="card">
    <div class="section-label"><i class="ti ti-check" aria-hidden="true" style="font-size:13px;margin-right:4px"></i>Hábitos de la semana</div>`;

  wd.habits.forEach((h,i) => {
    html += `
    <label class="habit-check">
      <input type="checkbox" ${d['h_'+i]?'checked':''} onchange="saveHabit(${i}, this.checked)"/>
      <span>${h}</span>
    </label>`;
  });

  html += `</div>
  <div class="card">
    <div class="section-label"><i class="ti ti-edit" aria-hidden="true" style="font-size:13px;margin-right:4px"></i>Reflexión semanal</div>
    <p style="font-size:12px;color:var(--color-text-secondary);margin:0 0 8px">¿Qué aprendiste? ¿Qué fue difícil? ¿Qué cambiarías?</p>
    <textarea class="reflection-box" placeholder="Escribe tu reflexión aquí..." 
      onchange="saveReflection(this.value)" oninput="saveReflection(this.value)">${d['reflection']||''}</textarea>
  </div>
  <div style="display:flex;gap:8px;flex-wrap:wrap">
    <button onclick="sendPrompt('¿Cómo puedo mejorar mi métrica de alcance en redes sociales? ↗')" style="font-size:12px">Mejorar alcance ↗</button>
    <button onclick="sendPrompt('¿Cuáles son los benchmarks promedio de open rate en email marketing para principiantes? ↗')" style="font-size:12px">Benchmarks de email ↗</button>
    <button onclick="sendPrompt('Tengo dudas sobre cómo interpretar mis métricas de GA4, ¿me ayudas? ↗')" style="font-size:12px">Interpretar GA4 ↗</button>
  </div>`;

  document.getElementById('main-content').innerHTML = html;
}

function saveMetric(id, val){
  if(!store[currentWeek]) store[currentWeek]={};
  store[currentWeek]['m_'+id] = val;
  setStorage(store);
  updateScore();
}

function saveHabit(i, checked){
  if(!store[currentWeek]) store[currentWeek]={};
  store[currentWeek]['h_'+i] = checked;
  setStorage(store);
  updateScore();
}

function saveReflection(val){
  if(!store[currentWeek]) store[currentWeek]={};
  store[currentWeek]['reflection'] = val;
  setStorage(store);
}

function updateScore(){
  const s = getScore();
  const colors = [{bg:'#534AB7'},{bg:'#0F6E56'},{bg:'#854F0B'}];
  const ph = getPhaseForWeek(currentWeek);
  const barColor = colors[ph.num-1].bg;
  const numEl = document.querySelector('.score-num');
  const barEl = document.querySelector('.bar-fill');
  const subEl = document.querySelector('.score-box .bar-wrap').nextElementSibling;
  if(numEl) numEl.textContent = s.pct+'%';
  if(barEl){ barEl.style.width = s.pct+'%'; barEl.style.background = barColor; }
  if(subEl) subEl.textContent = `${s.filled} de ${s.total} ítems registrados`;
}

function saveAll(){
  sendPrompt('Mis métricas de la semana '+currentWeek+' están guardadas. ¿Cómo interpreto si mi progreso en marketing digital va bien o necesita ajustes? ↗');
}

renderTabs();
renderContent();
</script>
