
<style>
  .sr-only{position:absolute;width:1px;height:1px;padding:0;margin:-1px;overflow:hidden;clip:rect(0,0,0,0);border:0}
  .week-card{background:var(--color-background-primary);border:0.5px solid var(--color-border-tertiary);border-radius:var(--border-radius-lg);margin-bottom:10px;overflow:hidden}
  .week-header{display:flex;align-items:center;gap:10px;padding:10px 14px;cursor:pointer;user-select:none}
  .week-header:hover{background:var(--color-background-secondary)}
  .week-num{font-size:11px;font-weight:500;padding:3px 9px;border-radius:20px;white-space:nowrap;flex-shrink:0}
  .week-title{font-size:14px;font-weight:500;color:var(--color-text-primary);flex:1}
  .week-sub{font-size:12px;color:var(--color-text-secondary);flex-shrink:0}
  .chevron{font-size:16px;color:var(--color-text-secondary);transition:transform 0.2s;flex-shrink:0}
  .week-body{padding:0 14px 12px;display:none}
  .week-body.open{display:block}
  .day-row{display:grid;grid-template-columns:80px 1fr;gap:8px;padding:5px 0;border-top:0.5px solid var(--color-border-tertiary)}
  .day-label{font-size:12px;font-weight:500;color:var(--color-text-secondary);padding-top:2px}
  .blocks-wrap{display:flex;flex-direction:column;gap:4px}
  .block{display:flex;align-items:flex-start;gap:8px;padding:5px 8px;border-radius:var(--border-radius-md)}
  .block-icon{font-size:14px;flex-shrink:0;margin-top:1px}
  .block-text{font-size:12px;color:var(--color-text-primary);line-height:1.4}
  .block-time{font-size:11px;color:var(--color-text-secondary)}
  .phase-divider{text-align:center;padding:8px 0;font-size:11px;font-weight:500;letter-spacing:0.5px;margin:8px 0 4px}
  .stat-row{display:grid;grid-template-columns:repeat(4,1fr);gap:8px;margin-bottom:16px}
  .stat{background:var(--color-background-secondary);border-radius:var(--border-radius-md);padding:10px 12px;text-align:center}
  .stat-val{font-size:20px;font-weight:500;color:var(--color-text-primary)}
  .stat-lbl{font-size:11px;color:var(--color-text-secondary);margin-top:2px}
  .progress-bar{height:4px;background:var(--color-border-tertiary);border-radius:2px;margin-top:4px}
  .progress-fill{height:4px;border-radius:2px}
  .resource-pill{display:inline-block;font-size:11px;padding:2px 8px;border-radius:20px;margin:2px 2px 2px 0;background:#EEEDFE;color:#3C3489}
  .dom-badge{font-size:11px;padding:3px 9px;border-radius:20px;background:#E1F5EE;color:#085041;margin-left:6px}
</style>

<h2 class="sr-only">Plan de 90 días para aprender Marketing Digital con bloques de hábitos semanales</h2>

<div style="padding:1rem 0">

  <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:14px;flex-wrap:wrap;gap:8px">
    <div>
      <p style="font-size:18px;font-weight:500;margin:0;color:var(--color-text-primary)">Plan 90 días · Marketing Digital</p>
      <p style="font-size:13px;color:var(--color-text-secondary);margin:3px 0 0">13 semanas · 3 fases · haz clic en cada semana para ver el detalle</p>
    </div>
    <button onclick="sendPrompt('¿Cómo puedo medir mi progreso en marketing digital semana a semana? ↗')" style="font-size:12px">Ver cómo medir progreso ↗</button>
  </div>

  <div class="stat-row">
    <div class="stat"><div class="stat-val">90</div><div class="stat-lbl">días</div></div>
    <div class="stat"><div class="stat-val">13</div><div class="stat-lbl">semanas</div></div>
    <div class="stat"><div class="stat-val">45</div><div class="stat-lbl">min/día</div></div>
    <div class="stat"><div class="stat-val">3</div><div class="stat-lbl">fases</div></div>
  </div>

  <div class="phase-divider" style="color:#3C3489">— Fase 1: Fundamentos (sem. 1–4) —</div>

  <div id="weeks-container"></div>

  <div style="display:flex;gap:8px;margin-top:4px;flex-wrap:wrap">
    <button onclick="sendPrompt('Dame un resumen de todos los recursos gratuitos para el plan de 90 días de marketing digital ↗')" style="font-size:12px">Recursos gratuitos ↗</button>
    <button onclick="sendPrompt('¿Qué proyecto práctico puedo hacer mientras aprendo marketing digital sin tener un negocio? ↗')" style="font-size:12px">Proyecto práctico ↗</button>
    <button onclick="sendPrompt('¿Cómo adapto este plan si solo tengo 20 minutos al día? ↗')" style="font-size:12px">Adaptar a 20 min ↗</button>
  </div>
</div>

<script>
const phases = [
  {label:"Fase 1: fundamentos",color:"#EEEDFE",textColor:"#3C3489",divAfter:4},
  {label:"Fase 2: canales y herramientas",color:"#E1F5EE",textColor:"#085041",divAfter:10},
  {label:"Fase 3: estrategia real",color:"#FAEEDA",textColor:"#633806",divAfter:13}
];

const weeks = [
  {
    num:1,phase:0,title:"¿Qué es el marketing digital?",focus:"Panorama general + conceptos base",
    days:[
      {d:"Lun",blocks:[{icon:"ti-book",bg:"#EEEDFE",ic:"#534AB7",text:"Leer: qué es marketing digital y sus canales",time:"20 min · Google Digital Garage mod. 1–2"},{icon:"ti-pencil",bg:"#EEEDFE",ic:"#534AB7",text:"Anotar: 5 cosas que no sabías",time:"10 min · cuaderno o Notion"}]},
      {d:"Mar",blocks:[{icon:"ti-video",bg:"#EEEDFE",ic:"#534AB7",text:"Ver: video intro al embudo de ventas (TOFU/MOFU/BOFU)",time:"20 min · YouTube: HubSpot en español"},{icon:"ti-edit",bg:"#EEEDFE",ic:"#534AB7",text:"Dibujar tu propio embudo imaginario",time:"10 min"}]},
      {d:"Mié",blocks:[{icon:"ti-book",bg:"#EEEDFE",ic:"#534AB7",text:"Leer: qué es un buyer persona",time:"20 min · HubSpot Academy gratuito"},{icon:"ti-user",bg:"#EEEDFE",ic:"#534AB7",text:"Crear tu primer buyer persona ficticio",time:"15 min"}]},
      {d:"Jue",blocks:[{icon:"ti-chart-bar",bg:"#EEEDFE",ic:"#534AB7",text:"Estudiar: métricas básicas (CTR, CPM, conversión, ROI)",time:"20 min"},{icon:"ti-pencil",bg:"#EEEDFE",ic:"#534AB7",text:"Flashcards: 10 términos nuevos",time:"10 min"}]},
      {d:"Vie",blocks:[{icon:"ti-refresh",bg:"#EEEDFE",ic:"#534AB7",text:"Repasar lo aprendido en la semana",time:"15 min"},{icon:"ti-star",bg:"#EEEDFE",ic:"#534AB7",text:"Reflexión: ¿qué te generó más dudas?",time:"10 min"}]},
      {d:"Sáb",blocks:[{icon:"ti-eye",bg:"#EEEDFE",ic:"#534AB7",text:"Analizar: observar 3 marcas en redes sociales",time:"20 min · ¿cómo comunican? ¿qué publican?"}]},
      {d:"Dom",blocks:[{icon:"ti-player-pause",bg:"#F1EFE8",ic:"#5F5E5A",text:"Descanso activo",time:"Opcional: podcast de marketing 15 min"}]}
    ]
  },
  {
    num:2,phase:0,title:"Buyer persona y propuesta de valor",focus:"Investigación de audiencia",
    days:[
      {d:"Lun",blocks:[{icon:"ti-book",bg:"#EEEDFE",ic:"#534AB7",text:"Leer: cómo hacer investigación de audiencia",time:"20 min · HubSpot Academy"},{icon:"ti-pencil",bg:"#EEEDFE",ic:"#534AB7",text:"Completar plantilla de buyer persona detallada",time:"15 min"}]},
      {d:"Mar",blocks:[{icon:"ti-video",bg:"#EEEDFE",ic:"#534AB7",text:"Ver: propuesta de valor y diferenciación",time:"20 min"},{icon:"ti-edit",bg:"#EEEDFE",ic:"#534AB7",text:"Escribir propuesta de valor de una marca que conoces",time:"10 min"}]},
      {d:"Mié",blocks:[{icon:"ti-search",bg:"#EEEDFE",ic:"#534AB7",text:"Explorar: Google Trends para entender demanda",time:"20 min · busca temas de tu nicho de interés"},{icon:"ti-pencil",bg:"#EEEDFE",ic:"#534AB7",text:"Anotar 5 tendencias encontradas",time:"10 min"}]},
      {d:"Jue",blocks:[{icon:"ti-book",bg:"#EEEDFE",ic:"#534AB7",text:"Leer: customer journey / mapa de experiencia",time:"20 min"},{icon:"ti-edit",bg:"#EEEDFE",ic:"#534AB7",text:"Dibujar customer journey de tu buyer persona",time:"15 min"}]},
      {d:"Vie",blocks:[{icon:"ti-refresh",bg:"#EEEDFE",ic:"#534AB7",text:"Repaso semanal + preguntas abiertas",time:"20 min"}]},
      {d:"Sáb",blocks:[{icon:"ti-eye",bg:"#EEEDFE",ic:"#534AB7",text:"Analizar: 2 landing pages de marcas reales",time:"20 min · ¿a quién le hablan? ¿cuál es su CTA?"}]},
      {d:"Dom",blocks:[{icon:"ti-player-pause",bg:"#F1EFE8",ic:"#5F5E5A",text:"Descanso activo",time:"Opcional: podcast o artículo de blog"}]}
    ]
  },
  {
    num:3,phase:0,title:"Contenido y copywriting básico",focus:"Comunicar el mensaje correcto",
    days:[
      {d:"Lun",blocks:[{icon:"ti-book",bg:"#EEEDFE",ic:"#534AB7",text:"Leer: qué es el marketing de contenidos",time:"20 min · Google Digital Garage mod. 5"},{icon:"ti-pencil",bg:"#EEEDFE",ic:"#534AB7",text:"Listar 10 ideas de contenido para tu nicho",time:"10 min"}]},
      {d:"Mar",blocks:[{icon:"ti-video",bg:"#EEEDFE",ic:"#534AB7",text:"Ver: copywriting básico (AIDA, PAS)",time:"20 min"},{icon:"ti-edit",bg:"#EEEDFE",ic:"#534AB7",text:"Escribir 3 titulares con fórmula AIDA",time:"15 min"}]},
      {d:"Mié",blocks:[{icon:"ti-book",bg:"#EEEDFE",ic:"#534AB7",text:"Leer: formatos de contenido (post, video, infografía)",time:"20 min"},{icon:"ti-pencil",bg:"#EEEDFE",ic:"#534AB7",text:"Crear un borrador de post corto (200 palabras)",time:"15 min"}]},
      {d:"Jue",blocks:[{icon:"ti-tool",bg:"#EEEDFE",ic:"#534AB7",text:"Practicar: diseñar una imagen con Canva (gratis)",time:"25 min · post para redes sociales"}]},
      {d:"Vie",blocks:[{icon:"ti-refresh",bg:"#EEEDFE",ic:"#534AB7",text:"Repaso + mini portafolio: guarda lo que creaste",time:"20 min"}]},
      {d:"Sáb",blocks:[{icon:"ti-eye",bg:"#EEEDFE",ic:"#534AB7",text:"Analizar: 3 posts exitosos en Instagram/LinkedIn",time:"20 min · ¿qué tienen en común?"}]},
      {d:"Dom",blocks:[{icon:"ti-player-pause",bg:"#F1EFE8",ic:"#5F5E5A",text:"Descanso activo",time:"Opcional"}]}
    ]
  },
  {
    num:4,phase:0,title:"Certificación + cierre de fase 1",focus:"Consolidar fundamentos",
    days:[
      {d:"Lun",blocks:[{icon:"ti-book",bg:"#EEEDFE",ic:"#534AB7",text:"Completar módulos pendientes Google Digital Garage",time:"30 min"},{icon:"ti-pencil",bg:"#EEEDFE",ic:"#534AB7",text:"Repaso de conceptos clave de semanas 1–3",time:"15 min"}]},
      {d:"Mar",blocks:[{icon:"ti-certificate",bg:"#EEEDFE",ic:"#534AB7",text:"Rendir examen de certificación Google Digital Garage",time:"~45 min · es gratuito y online"}]},
      {d:"Mié",blocks:[{icon:"ti-edit",bg:"#EEEDFE",ic:"#534AB7",text:"Escribir: resumen personal de lo aprendido",time:"20 min · en tus propias palabras"}]},
      {d:"Jue",blocks:[{icon:"ti-star",bg:"#EEEDFE",ic:"#534AB7",text:"Definir: ¿en qué canal quieres enfocarte en fase 2?",time:"15 min · SEO, redes, email, o paid ads"}]},
      {d:"Vie",blocks:[{icon:"ti-calendar",bg:"#EEEDFE",ic:"#534AB7",text:"Planificar tu semana 5: qué recurso usarás",time:"15 min"}]},
      {d:"Sáb",blocks:[{icon:"ti-player-pause",bg:"#F1EFE8",ic:"#5F5E5A",text:"Celebra el logro · Fase 1 completada",time:"Comparte tu certificado en LinkedIn"}]},
      {d:"Dom",blocks:[{icon:"ti-player-pause",bg:"#F1EFE8",ic:"#5F5E5A",text:"Descanso completo",time:""}]}
    ]
  },
  {
    num:5,phase:1,title:"SEO: fundamentos",focus:"Cómo Google encuentra tu contenido",
    days:[
      {d:"Lun",blocks:[{icon:"ti-book",bg:"#E1F5EE",ic:"#0F6E56",text:"Leer: qué es el SEO y cómo funciona Google",time:"20 min · Moz Beginner's Guide (en español disponible)"},{icon:"ti-pencil",bg:"#E1F5EE",ic:"#0F6E56",text:"Anotar: diferencia entre SEO on-page y off-page",time:"10 min"}]},
      {d:"Mar",blocks:[{icon:"ti-search",bg:"#E1F5EE",ic:"#0F6E56",text:"Practicar: investigación de palabras clave con Google Keyword Planner (gratis)",time:"25 min · busca 10 keywords de tu nicho"},{icon:"ti-pencil",bg:"#E1F5EE",ic:"#0F6E56",text:"Organizar keywords por intención de búsqueda",time:"10 min"}]},
      {d:"Mié",blocks:[{icon:"ti-book",bg:"#E1F5EE",ic:"#0F6E56",text:"Leer: estructura de un artículo SEO (H1, H2, meta)",time:"20 min"},{icon:"ti-edit",bg:"#E1F5EE",ic:"#0F6E56",text:"Optimizar el post de la semana 3 para SEO",time:"20 min"}]},
      {d:"Jue",blocks:[{icon:"ti-tool",bg:"#E1F5EE",ic:"#0F6E56",text:"Explorar: Google Search Console (crear cuenta gratis)",time:"25 min · entender qué mide"},{icon:"ti-pencil",bg:"#E1F5EE",ic:"#0F6E56",text:"Anotar métricas que vas a seguir",time:"10 min"}]},
      {d:"Vie",blocks:[{icon:"ti-refresh",bg:"#E1F5EE",ic:"#0F6E56",text:"Repaso SEO + flashcards de términos",time:"20 min"}]},
      {d:"Sáb",blocks:[{icon:"ti-eye",bg:"#E1F5EE",ic:"#0F6E56",text:"Analizar: buscar en Google un tema de tu nicho",time:"20 min · ¿qué páginas salen primero y por qué?"}]},
      {d:"Dom",blocks:[{icon:"ti-player-pause",bg:"#F1EFE8",ic:"#5F5E5A",text:"Descanso activo",time:"Opcional"}]}
    ]
  },
  {
    num:6,phase:1,title:"Redes sociales orgánicas",focus:"Crear presencia sin pagar",
    days:[
      {d:"Lun",blocks:[{icon:"ti-book",bg:"#E1F5EE",ic:"#0F6E56",text:"Leer: algoritmos de Instagram y LinkedIn",time:"20 min"},{icon:"ti-pencil",bg:"#E1F5EE",ic:"#0F6E56",text:"Definir: ¿qué red social usarás para tu proyecto?",time:"10 min"}]},
      {d:"Mar",blocks:[{icon:"ti-calendar",bg:"#E1F5EE",ic:"#0F6E56",text:"Crear: calendario de contenido para 2 semanas",time:"25 min · 5 posts planeados"},{icon:"ti-tool",bg:"#E1F5EE",ic:"#0F6E56",text:"Diseñar: 2 posts con Canva usando plantillas",time:"20 min"}]},
      {d:"Mié",blocks:[{icon:"ti-book",bg:"#E1F5EE",ic:"#0F6E56",text:"Leer: cómo usar hashtags correctamente",time:"15 min"},{icon:"ti-edit",bg:"#E1F5EE",ic:"#0F6E56",text:"Publicar tu primer post en la red elegida",time:"20 min"}]},
      {d:"Jue",blocks:[{icon:"ti-chart-bar",bg:"#E1F5EE",ic:"#0F6E56",text:"Revisar métricas del post publicado",time:"15 min · alcance, interacción, seguidores"},{icon:"ti-book",bg:"#E1F5EE",ic:"#0F6E56",text:"Leer: comunidad y engagement vs alcance",time:"15 min"}]},
      {d:"Vie",blocks:[{icon:"ti-edit",bg:"#E1F5EE",ic:"#0F6E56",text:"Publicar segundo post + responder comentarios",time:"20 min"},{icon:"ti-refresh",bg:"#E1F5EE",ic:"#0F6E56",text:"Repaso de la semana",time:"10 min"}]},
      {d:"Sáb",blocks:[{icon:"ti-eye",bg:"#E1F5EE",ic:"#0F6E56",text:"Analizar: 3 cuentas exitosas en tu nicho",time:"20 min · horarios, formatos, tono"}]},
      {d:"Dom",blocks:[{icon:"ti-player-pause",bg:"#F1EFE8",ic:"#5F5E5A",text:"Descanso activo",time:""}]}
    ]
  },
  {
    num:7,phase:1,title:"Email marketing",focus:"La herramienta de mayor ROI",
    days:[
      {d:"Lun",blocks:[{icon:"ti-book",bg:"#E1F5EE",ic:"#0F6E56",text:"Leer: por qué el email marketing sigue siendo #1 en ROI",time:"20 min · Mailchimp Academy (gratis)"},{icon:"ti-pencil",bg:"#E1F5EE",ic:"#0F6E56",text:"Anotar: partes de un email de marketing efectivo",time:"10 min"}]},
      {d:"Mar",blocks:[{icon:"ti-tool",bg:"#E1F5EE",ic:"#0F6E56",text:"Crear cuenta gratuita en Mailchimp o Brevo",time:"20 min · explorar la interfaz"},{icon:"ti-edit",bg:"#E1F5EE",ic:"#0F6E56",text:"Diseñar tu primera plantilla de email",time:"20 min"}]},
      {d:"Mié",blocks:[{icon:"ti-book",bg:"#E1F5EE",ic:"#0F6E56",text:"Leer: segmentación y listas de suscriptores",time:"20 min"},{icon:"ti-edit",bg:"#E1F5EE",ic:"#0F6E56",text:"Escribir un email de bienvenida (welcome email)",time:"20 min"}]},
      {d:"Jue",blocks:[{icon:"ti-book",bg:"#E1F5EE",ic:"#0F6E56",text:"Leer: métricas de email (open rate, click rate, bounce)",time:"15 min"},{icon:"ti-pencil",bg:"#E1F5EE",ic:"#0F6E56",text:"Crear mini-secuencia de 3 emails para un producto ficticio",time:"25 min"}]},
      {d:"Vie",blocks:[{icon:"ti-refresh",bg:"#E1F5EE",ic:"#0F6E56",text:"Repaso + envía el email de prueba a ti mismo",time:"20 min"}]},
      {d:"Sáb",blocks:[{icon:"ti-eye",bg:"#E1F5EE",ic:"#0F6E56",text:"Analizar: suscríbete a 3 newsletters de tu industria",time:"20 min · ¿qué hacen bien?"}]},
      {d:"Dom",blocks:[{icon:"ti-player-pause",bg:"#F1EFE8",ic:"#5F5E5A",text:"Descanso activo",time:""}]}
    ]
  },
  {
    num:8,phase:1,title:"Publicidad pagada (intro)",focus:"Google Ads y Meta Ads desde cero",
    days:[
      {d:"Lun",blocks:[{icon:"ti-book",bg:"#E1F5EE",ic:"#0F6E56",text:"Leer: diferencia entre paid search y paid social",time:"20 min"},{icon:"ti-pencil",bg:"#E1F5EE",ic:"#0F6E56",text:"Anotar: tipos de campañas en Google Ads",time:"10 min"}]},
      {d:"Mar",blocks:[{icon:"ti-tool",bg:"#E1F5EE",ic:"#0F6E56",text:"Explorar Google Ads: crear cuenta (sin gastar dinero)",time:"20 min · modo simulación"},{icon:"ti-edit",bg:"#E1F5EE",ic:"#0F6E56",text:"Redactar 3 anuncios de búsqueda para marca ficticia",time:"20 min"}]},
      {d:"Mié",blocks:[{icon:"ti-book",bg:"#E1F5EE",ic:"#0F6E56",text:"Leer: cómo funciona el Ads Manager de Meta",time:"20 min"},{icon:"ti-pencil",bg:"#E1F5EE",ic:"#0F6E56",text:"Anotar: objetivos de campaña en Meta Ads",time:"10 min"}]},
      {d:"Jue",blocks:[{icon:"ti-edit",bg:"#E1F5EE",ic:"#0F6E56",text:"Diseñar: creativos de un anuncio (imagen + copy) con Canva",time:"25 min"},{icon:"ti-pencil",bg:"#E1F5EE",ic:"#0F6E56",text:"Definir público objetivo del anuncio",time:"10 min"}]},
      {d:"Vie",blocks:[{icon:"ti-refresh",bg:"#E1F5EE",ic:"#0F6E56",text:"Repaso paid ads + dudas frecuentes",time:"20 min"}]},
      {d:"Sáb",blocks:[{icon:"ti-eye",bg:"#E1F5EE",ic:"#0F6E56",text:"Analizar: identifica anuncios reales en tu feed",time:"20 min · ¿qué copywriting usan?"}]},
      {d:"Dom",blocks:[{icon:"ti-player-pause",bg:"#F1EFE8",ic:"#5F5E5A",text:"Descanso activo",time:""}]}
    ]
  },
  {
    num:9,phase:1,title:"Analítica web (Google Analytics 4)",focus:"Tomar decisiones con datos",
    days:[
      {d:"Lun",blocks:[{icon:"ti-book",bg:"#E1F5EE",ic:"#0F6E56",text:"Leer: qué mide GA4 y cómo instalarlo",time:"20 min · Google Skillshop (gratis)"},{icon:"ti-pencil",bg:"#E1F5EE",ic:"#0F6E56",text:"Anotar: diferencia entre sesiones, usuarios y eventos",time:"10 min"}]},
      {d:"Mar",blocks:[{icon:"ti-tool",bg:"#E1F5EE",ic:"#0F6E56",text:"Crear propiedad en GA4 y explorar el panel",time:"25 min · usar cuenta demo de Google"},{icon:"ti-pencil",bg:"#E1F5EE",ic:"#0F6E56",text:"Identificar 5 métricas clave para tu proyecto",time:"10 min"}]},
      {d:"Mié",blocks:[{icon:"ti-book",bg:"#E1F5EE",ic:"#0F6E56",text:"Leer: embudos de conversión en GA4",time:"20 min"},{icon:"ti-chart-bar",bg:"#E1F5EE",ic:"#0F6E56",text:"Practicar: crear un reporte personalizado básico",time:"20 min"}]},
      {d:"Jue",blocks:[{icon:"ti-book",bg:"#E1F5EE",ic:"#0F6E56",text:"Leer: UTMs para rastrear campañas",time:"20 min"},{icon:"ti-edit",bg:"#E1F5EE",ic:"#0F6E56",text:"Crear 3 URLs con UTMs para tus posts",time:"15 min"}]},
      {d:"Vie",blocks:[{icon:"ti-refresh",bg:"#E1F5EE",ic:"#0F6E56",text:"Repaso GA4 + quiz de conceptos",time:"20 min"}]},
      {d:"Sáb",blocks:[{icon:"ti-eye",bg:"#E1F5EE",ic:"#0F6E56",text:"Análisis real: explorar la cuenta demo de GA4",time:"30 min · responde: ¿de dónde viene el tráfico?"}]},
      {d:"Dom",blocks:[{icon:"ti-player-pause",bg:"#F1EFE8",ic:"#5F5E5A",text:"Descanso activo",time:""}]}
    ]
  },
  {
    num:10,phase:1,title:"Integración y cierre de fase 2",focus:"Conectar todos los canales",
    days:[
      {d:"Lun",blocks:[{icon:"ti-book",bg:"#E1F5EE",ic:"#0F6E56",text:"Leer: estrategia multicanal vs omnicanal",time:"20 min"},{icon:"ti-edit",bg:"#E1F5EE",ic:"#0F6E56",text:"Diseñar un mini funnel completo para tu proyecto",time:"20 min"}]},
      {d:"Mar",blocks:[{icon:"ti-tool",bg:"#E1F5EE",ic:"#0F6E56",text:"Conectar: GA4 + Search Console + redes",time:"25 min · solo vincular cuentas"},{icon:"ti-pencil",bg:"#E1F5EE",ic:"#0F6E56",text:"Hacer inventario de todo lo aprendido en fase 2",time:"15 min"}]},
      {d:"Mié",blocks:[{icon:"ti-certificate",bg:"#E1F5EE",ic:"#0F6E56",text:"Hacer certificación HubSpot Marketing Digital (gratis)",time:"~60 min · repartida en el día"}]},
      {d:"Jue",blocks:[{icon:"ti-edit",bg:"#E1F5EE",ic:"#0F6E56",text:"Definir proyecto para fase 3: tema, canal, objetivo",time:"25 min"},{icon:"ti-calendar",bg:"#E1F5EE",ic:"#0F6E56",text:"Planificar semanas 11–13 con tu proyecto real",time:"15 min"}]},
      {d:"Vie",blocks:[{icon:"ti-star",bg:"#E1F5EE",ic:"#0F6E56",text:"Reflexión: ¿qué canal se te dio mejor? ¿cuál cuesta más?",time:"20 min"}]},
      {d:"Sáb",blocks:[{icon:"ti-player-pause",bg:"#F1EFE8",ic:"#5F5E5A",text:"Celebra · Fase 2 completada",time:"Comparte tu certificado HubSpot"}]},
      {d:"Dom",blocks:[{icon:"ti-player-pause",bg:"#F1EFE8",ic:"#5F5E5A",text:"Descanso completo",time:""}]}
    ]
  },
  {
    num:11,phase:2,title:"Lanzamiento del proyecto real",focus:"Poner en práctica todo lo aprendido",
    days:[
      {d:"Lun",blocks:[{icon:"ti-rocket",bg:"#FAEEDA",ic:"#854F0B",text:"Publicar: primera pieza de contenido del proyecto real",time:"30 min · blog post, post o newsletter"},{icon:"ti-chart-bar",bg:"#FAEEDA",ic:"#854F0B",text:"Configurar seguimiento de métricas en GA4",time:"15 min"}]},
      {d:"Mar",blocks:[{icon:"ti-edit",bg:"#FAEEDA",ic:"#854F0B",text:"Crear y programar contenido de la semana",time:"30 min · 3 piezas en tu canal elegido"}]},
      {d:"Mié",blocks:[{icon:"ti-search",bg:"#FAEEDA",ic:"#854F0B",text:"Investigar: 5 keywords para optimizar tu contenido",time:"20 min"},{icon:"ti-edit",bg:"#FAEEDA",ic:"#854F0B",text:"Aplicar SEO on-page a una pieza ya publicada",time:"20 min"}]},
      {d:"Jue",blocks:[{icon:"ti-mail",bg:"#FAEEDA",ic:"#854F0B",text:"Enviar primera newsletter de tu proyecto",time:"25 min · aunque sea a ti mismo y a 3 amigos"}]},
      {d:"Vie",blocks:[{icon:"ti-chart-bar",bg:"#FAEEDA",ic:"#854F0B",text:"Revisar métricas de la semana",time:"15 min"},{icon:"ti-refresh",bg:"#FAEEDA",ic:"#854F0B",text:"Reflexión: ¿qué ajustar para la próxima semana?",time:"10 min"}]},
      {d:"Sáb",blocks:[{icon:"ti-eye",bg:"#FAEEDA",ic:"#854F0B",text:"Benchmarking: comparar tu proyecto con 2 referentes",time:"20 min"}]},
      {d:"Dom",blocks:[{icon:"ti-player-pause",bg:"#F1EFE8",ic:"#5F5E5A",text:"Descanso activo",time:""}]}
    ]
  },
  {
    num:12,phase:2,title:"Optimización y pruebas",focus:"Mejorar con datos reales",
    days:[
      {d:"Lun",blocks:[{icon:"ti-chart-bar",bg:"#FAEEDA",ic:"#854F0B",text:"Analizar: qué piezas tuvieron más alcance en sem. 11",time:"20 min"},{icon:"ti-edit",bg:"#FAEEDA",ic:"#854F0B",text:"Crear variante mejorada del contenido más exitoso",time:"20 min"}]},
      {d:"Mar",blocks:[{icon:"ti-book",bg:"#FAEEDA",ic:"#854F0B",text:"Leer: A/B testing básico en email y redes",time:"20 min"},{icon:"ti-edit",bg:"#FAEEDA",ic:"#854F0B",text:"Hacer prueba A/B con 2 titulares diferentes",time:"20 min"}]},
      {d:"Mié",blocks:[{icon:"ti-edit",bg:"#FAEEDA",ic:"#854F0B",text:"Publicar 2 piezas + responder comentarios activamente",time:"30 min"},{icon:"ti-pencil",bg:"#FAEEDA",ic:"#854F0B",text:"Documentar aprendizajes del A/B test",time:"10 min"}]},
      {d:"Jue",blocks:[{icon:"ti-book",bg:"#FAEEDA",ic:"#854F0B",text:"Leer: retargeting y audiencias personalizadas",time:"20 min"},{icon:"ti-pencil",bg:"#FAEEDA",ic:"#854F0B",text:"Diseñar estrategia de retargeting para tu proyecto",time:"15 min"}]},
      {d:"Vie",blocks:[{icon:"ti-refresh",bg:"#FAEEDA",ic:"#854F0B",text:"Revisión semanal de métricas + ajustes",time:"20 min"}]},
      {d:"Sáb",blocks:[{icon:"ti-edit",bg:"#FAEEDA",ic:"#854F0B",text:"Producir contenido de la próxima semana por adelantado",time:"30 min"}]},
      {d:"Dom",blocks:[{icon:"ti-player-pause",bg:"#F1EFE8",ic:"#5F5E5A",text:"Descanso activo",time:""}]}
    ]
  },
  {
    num:13,phase:2,title:"Portfolio y cierre de los 90 días",focus:"Documentar logros y siguiente paso",
    days:[
      {d:"Lun",blocks:[{icon:"ti-file",bg:"#FAEEDA",ic:"#854F0B",text:"Documentar: resultados de las 4 semanas del proyecto",time:"30 min · capturas, métricas, aprendizajes"},{icon:"ti-pencil",bg:"#FAEEDA",ic:"#854F0B",text:"Escribir resumen ejecutivo de tu proyecto",time:"20 min"}]},
      {d:"Mar",blocks:[{icon:"ti-edit",bg:"#FAEEDA",ic:"#854F0B",text:"Crear case study: problema, acción, resultado",time:"30 min · para tu portafolio o LinkedIn"}]},
      {d:"Mié",blocks:[{icon:"ti-user",bg:"#FAEEDA",ic:"#854F0B",text:"Actualizar LinkedIn con habilidades y certificaciones",time:"20 min"},{icon:"ti-edit",bg:"#FAEEDA",ic:"#854F0B",text:"Publicar tu case study en LinkedIn",time:"15 min"}]},
      {d:"Jue",blocks:[{icon:"ti-star",bg:"#FAEEDA",ic:"#854F0B",text:"Reflexión de 90 días: ¿qué aprendiste? ¿qué sigue?",time:"25 min · escríbelo como carta a ti mismo"}]},
      {d:"Vie",blocks:[{icon:"ti-calendar",bg:"#FAEEDA",ic:"#854F0B",text:"Planificar los próximos 90 días: ¿qué profundizar?",time:"25 min · ¿especializarte en SEO, paid ads o contenido?"}]},
      {d:"Sáb",blocks:[{icon:"ti-star",bg:"#FAEEDA",ic:"#854F0B",text:"Celebra el logro: 90 días completados",time:"Comparte tu journey en redes"}]},
      {d:"Dom",blocks:[{icon:"ti-player-pause",bg:"#F1EFE8",ic:"#5F5E5A",text:"Descanso completo. Te lo ganaste.",time:""}]}
    ]
  }
];

const phaseDividers = {
  5: {label:"— Fase 2: canales y herramientas (sem. 5–10) —", color:"#085041"},
  11: {label:"— Fase 3: estrategia real (sem. 11–13) —", color:"#633806"}
};

const container = document.getElementById('weeks-container');

weeks.forEach((w, i) => {
  if (phaseDividers[w.num]) {
    const div = document.createElement('div');
    div.className = 'phase-divider';
    div.style.color = phaseDividers[w.num].color;
    div.textContent = phaseDividers[w.num].label;
    container.appendChild(div);
  }

  const phaseColors = [
    {bg:"#EEEDFE",tc:"#3C3489"},
    {bg:"#E1F5EE",tc:"#085041"},
    {bg:"#FAEEDA",tc:"#633806"}
  ];
  const pc = phaseColors[w.phase];

  const card = document.createElement('div');
  card.className = 'week-card';

  const header = document.createElement('div');
  header.className = 'week-header';
  header.setAttribute('role','button');
  header.setAttribute('aria-expanded','false');
  header.innerHTML = `
    <span class="week-num" style="background:${pc.bg};color:${pc.tc}">Sem. ${w.num}</span>
    <span class="week-title">${w.title}</span>
    <span class="week-sub">${w.focus}</span>
    <i class="ti ti-chevron-down chevron" aria-hidden="true"></i>
  `;

  const body = document.createElement('div');
  body.className = 'week-body';

  w.days.forEach(day => {
    const row = document.createElement('div');
    row.className = 'day-row';
    let blocksHtml = day.blocks.map(b => `
      <div class="block" style="background:${b.bg}">
        <i class="ti ${b.icon} block-icon" aria-hidden="true" style="color:${b.ic}"></i>
        <div>
          <div class="block-text">${b.text}</div>
          ${b.time ? `<div class="block-time">${b.time}</div>` : ''}
        </div>
      </div>
    `).join('');
    row.innerHTML = `<div class="day-label">${day.d}</div><div class="blocks-wrap">${blocksHtml}</div>`;
    body.appendChild(row);
  });

  header.addEventListener('click', () => {
    const isOpen = body.classList.contains('open');
    body.classList.toggle('open', !isOpen);
    header.querySelector('.chevron').style.transform = isOpen ? '' : 'rotate(180deg)';
    header.setAttribute('aria-expanded', String(!isOpen));
  });

  card.appendChild(header);
  card.appendChild(body);
  container.appendChild(card);
});
</script>
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
