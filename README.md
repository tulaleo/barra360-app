index.html
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="utf-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>Barra 360</title>
<style>
  :root{--bg:#0a0f12;--card:#121a20;--neon:#39ff14;--text:#e9f1f5;}
  body{margin:0;font-family:system-ui,-apple-system,Segoe UI,Roboto; background:var(--bg); color:var(--text);}
  .wrap{max-width:720px;margin:auto;padding:16px;}
  h1{margin:8px 0 16px;font-size:28px}
  .card{background:var(--card);border-radius:16px;padding:16px;margin-bottom:12px;box-shadow:0 0 0 1px #0f2a1a,0 0 18px rgba(57,255,20,.12);}
  .btn{display:block;width:100%;padding:14px;border:0;border-radius:12px;background:var(--neon);color:#001; font-weight:700;margin-top:10px}
  input,select{width:100%;padding:12px;border-radius:10px;border:1px solid #1e2a31;background:#0d1418;color:var(--text);margin-top:8px}
  .row{display:grid;grid-template-columns:1fr 1fr;gap:8px}
  .kpi{display:flex;justify-content:space-between;margin:6px 0}
  .pill{border:1px solid #1e2a31;border-radius:999px;padding:6px 10px;margin-right:6px}
  small{opacity:.8}
</style>
</head>
<body>
<div class="wrap">
  <h1>🍸 Barra 360</h1>

  <div class="card">
    <strong>Calculadora de evento</strong>
    <label>Invitados</label>
    <input id="inv" type="number" placeholder="Ej: 80"/>
    <label>Tipo</label>
    <select id="tipo">
      <option value="estandar">Estándar</option>
      <option value="premium">Premium</option>
      <option value="fluor">Flúor</option>
    </select>
    <button class="btn" onclick="calcular()">Calcular</button>
    <div id="res"></div>
  </div>

  <div class="card">
    <strong>Carta rápida</strong>
    <div class="pill">Mojito clásico</div>
    <div class="pill">Mojito frutal</div>
    <div class="pill">Tom Collins</div>
    <div class="pill">Tragos flúor</div>
    <small>Medidas estándar incluidas</small>
  </div>

  <div class="card">
    <strong>Contacto</strong>
    <button class="btn" onclick="wa()">WhatsApp</button>
  </div>
</div>

<script>
function calcular(){
  const n = parseInt(document.getElementById('inv').value||0);
  const t = document.getElementById('tipo').value;
  if(!n){alert('Ingresá cantidad');return;}
  const tragos = Math.ceil(n*3); // 3 tragos por persona
  const alcohol = (tragos*50)/1000; // litros (50ml c/u)
  const hielo = Math.ceil(n*0.5); // kg
  const vasos = Math.ceil(n*2);
  let precioBase = t==='premium'? 3500 : t==='fluor'? 3200 : 2800; // por persona ARS (ajustable)
  const total = n * precioBase;

  document.getElementById('res').innerHTML = `
    <div class="kpi"><span>Tragos</span><b>${tragos}</b></div>
    <div class="kpi"><span>Alcohol (L)</span><b>${alcohol.toFixed(1)}</b></div>
    <div class="kpi"><span>Hielo (kg)</span><b>${hielo}</b></div>
    <div class="kpi"><span>Vasos</span><b>${vasos}</b></div>
    <hr/>
    <div class="kpi"><span>Precio sugerido</span><b>$${total.toLocaleString('es-AR')}</b></div>
    <small>Podés ajustar el valor por persona según mercado.</small>
  `;
}

function wa(){
  const texto = "Hola, quiero info para un evento con Barra 360 🍸";
  if(confirm("Se abrirá WhatsApp con este mensaje:\n\n" + texto)){
    const msg = encodeURIComponent(texto);
    window.location.href = "https://wa.me/543854061931?text="+msg;
  }
}
}
</script>
</body>
</html>

