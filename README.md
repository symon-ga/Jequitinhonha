<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ativo Ambiental Estratégico — Vale do Jequitinhonha</title>
  <style>
    :root {
      --dark:    #040c08;
      --green:   #163c24;
      --accent:  #237a49;
      --glow:    #3dbf72;
      --glow2:   #68dfa0;
      --gold:    #c9a84c;
      --text:    #e2f0ea;
      --muted:   #6ea882;
    }

    *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

    html { scroll-behavior: smooth; }

    body {
      background: var(--dark);
      color: var(--text);
      font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
      overflow-x: hidden;
      line-height: 1.6;
    }

    /* ── HERO ─────────────────────────────── */
    .hero {
      position: relative;
      height: 100vh;
      min-height: 600px;
      display: flex;
      align-items: center;
      overflow: hidden;
    }

    #terrain-canvas {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: 0;
      display: block;
    }

    .hero-overlay {
      position: absolute;
      inset: 0;
      background:
        radial-gradient(ellipse 55% 80% at 20% 50%, rgba(4,12,8,.92) 40%, transparent 100%),
        linear-gradient(to right, rgba(4,12,8,.7) 0%, transparent 60%);
      z-index: 1;
    }

    .hero-content {
      position: relative;
      z-index: 2;
      padding: 6rem 8vw 4rem;
      max-width: 660px;
    }

    .tag {
      display: inline-flex;
      align-items: center;
      gap: .5rem;
      border: 1px solid rgba(61,191,114,.45);
      background: rgba(61,191,114,.07);
      color: var(--glow2);
      font-size: .68rem;
      letter-spacing: .22em;
      text-transform: uppercase;
      padding: .35em 1.1em;
      border-radius: 99px;
      margin-bottom: 1.6rem;
    }

    .tag::before { content: ''; display: block; width: 6px; height: 6px; border-radius: 50%; background: var(--glow); box-shadow: 0 0 6px var(--glow); animation: blink 1.8s ease-in-out infinite; }
    @keyframes blink { 0%,100%{opacity:1} 50%{opacity:.2} }

    h1 {
      font-size: clamp(2.4rem, 5.5vw, 4.2rem);
      font-weight: 300;
      line-height: 1.1;
      letter-spacing: -.03em;
      margin-bottom: .9rem;
    }
    h1 strong {
      font-weight: 800;
      color: var(--glow);
    }

    .subtitle {
      font-size: 1.05rem;
      color: var(--muted);
      line-height: 1.75;
      margin-bottom: 2.8rem;
      max-width: 500px;
    }

    .metrics {
      display: flex;
      gap: 2.2rem;
      margin-bottom: 3rem;
      flex-wrap: wrap;
    }

    .metric { border-left: 2px solid var(--accent); padding-left: 1rem; }
    .metric-value { font-size: 1.9rem; font-weight: 800; color: #fff; line-height: 1; }
    .metric-label { font-size: .7rem; color: var(--muted); letter-spacing: .12em; text-transform: uppercase; margin-top: .3rem; }

    .cta-group { display: flex; gap: 1rem; flex-wrap: wrap; }

    .btn-primary {
      display: inline-flex; align-items: center; gap: .55rem;
      background: var(--glow); color: var(--dark);
      padding: .85em 1.9em; border-radius: 5px;
      font-weight: 700; text-decoration: none; font-size: .95rem;
      letter-spacing: .02em; transition: .2s;
    }
    .btn-primary:hover { background: var(--glow2); transform: translateY(-2px); box-shadow: 0 6px 24px rgba(61,191,114,.35); }

    .btn-ghost {
      display: inline-flex; align-items: center; gap: .55rem;
      border: 1px solid rgba(61,191,114,.35); color: var(--glow);
      padding: .85em 1.9em; border-radius: 5px;
      font-weight: 500; text-decoration: none; font-size: .95rem;
      letter-spacing: .02em; transition: .2s;
    }
    .btn-ghost:hover { background: rgba(61,191,114,.08); border-color: var(--glow); }

    /* ── SCROLL REVEAL ───────────────────── */
    .reveal { opacity: 0; transform: translateY(28px); transition: opacity .65s ease, transform .65s ease; }
    .reveal.in { opacity: 1; transform: none; }

    /* ── SECTION BASE ────────────────────── */
    section { padding: 5.5rem 8vw; }

    .sec-label {
      font-size: .68rem; letter-spacing: .22em; text-transform: uppercase;
      color: var(--glow); margin-bottom: .8rem; display: block;
    }
    .sec-title {
      font-size: clamp(1.6rem, 3vw, 2.6rem);
      font-weight: 300; line-height: 1.25; margin-bottom: 2.8rem;
    }
    .sec-title strong { font-weight: 800; }

    /* ── VALUE CARDS ─────────────────────── */
    .value-section {
      background: rgba(22,60,36,.18);
      border-top: 1px solid rgba(61,191,114,.08);
      border-bottom: 1px solid rgba(61,191,114,.08);
    }

    .cards {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(210px, 1fr));
      gap: 1.3rem;
    }

    .card {
      background: rgba(255,255,255,.025);
      border: 1px solid rgba(61,191,114,.12);
      border-radius: 10px; padding: 1.7rem 1.5rem;
      transition: .25s;
    }
    .card:hover {
      border-color: rgba(61,191,114,.38);
      background: rgba(61,191,114,.06);
      transform: translateY(-3px);
    }
    .card-icon { font-size: 2rem; margin-bottom: 1rem; line-height: 1; }
    .card h3 { font-size: .97rem; font-weight: 700; color: #fff; margin-bottom: .45rem; }
    .card p  { font-size: .84rem; color: var(--muted); line-height: 1.65; }

    /* ── DADOS TÉCNICOS ──────────────────── */
    .data-section { background: rgba(0,0,0,.25); }

    .data-table {
      width: 100%;
      border: 1px solid rgba(61,191,114,.2);
      border-radius: 10px;
      overflow: hidden;
      border-collapse: separate;
      border-spacing: 0;
    }
    .data-table tr:not(:last-child) td { border-bottom: 1px solid rgba(61,191,114,.1); }
    .data-table td { padding: 1rem 1.5rem; font-size: .9rem; vertical-align: top; }
    .data-table td:first-child {
      width: 38%;
      font-size: .77rem; text-transform: uppercase; letter-spacing: .09em;
      color: var(--glow2);
      font-weight: 600;
      background: rgba(61,191,114,.06);
      border-right: 1px solid rgba(61,191,114,.12);
    }
    .data-table td:last-child {
      color: #0d1f10;
      font-weight: 600;
      background: rgba(255,255,255,.78);
    }
    .data-table tr:hover td { background: rgba(61,191,114,.07); }
    .data-table tr:hover td:first-child { background: rgba(61,191,114,.1); }
    .data-table tr:hover td:last-child { color: #0d1f10; background: rgba(200,240,215,.7); }

    /* ── BUYERS ──────────────────────────── */
    .buyers-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(270px, 1fr));
      gap: 1.5rem;
    }

    .buyer-card {
      border: 1px solid rgba(201,168,76,.22);
      background: rgba(201,168,76,.03);
      border-radius: 10px; padding: 2rem;
      transition: .25s;
    }
    .buyer-card:hover {
      border-color: rgba(201,168,76,.5);
      background: rgba(201,168,76,.06);
      transform: translateY(-3px);
    }
    .buyer-type {
      font-size: .68rem; letter-spacing: .18em; text-transform: uppercase;
      color: var(--gold); margin-bottom: .7rem;
    }
    .buyer-card h3 { font-size: 1.05rem; color: #fff; margin-bottom: .9rem; font-weight: 700; }
    .buyer-card ul { list-style: none; }
    .buyer-card ul li { font-size: .85rem; color: var(--muted); padding: .28rem 0; }
    .buyer-card ul li::before { content: '→ '; color: var(--gold); }

    /* ── CONTACT ─────────────────────────── */
    .contact-section {
      text-align: center;
      background: linear-gradient(160deg, rgba(22,60,36,.3) 0%, transparent 60%);
    }
    .contact-wrap {
      display: inline-flex; flex-direction: column; align-items: center;
      background: rgba(61,191,114,.07);
      border: 1px solid rgba(61,191,114,.28);
      border-radius: 14px; padding: 3rem 5rem; gap: .4rem;
      margin-top: 1rem;
    }
    .contact-name { font-size: .75rem; letter-spacing: .18em; text-transform: uppercase; color: var(--muted); }
    .contact-num  { font-size: 2.2rem; font-weight: 800; color: #fff; letter-spacing: .06em; }
    .btn-whatsapp {
      display: inline-flex; align-items: center; gap: .55rem;
      margin-top: 1.2rem;
      background: #25D366; color: #fff;
      padding: .8em 2.2em; border-radius: 99px;
      font-weight: 700; text-decoration: none; font-size: .9rem;
      transition: .2s;
    }
    .btn-whatsapp:hover { background: #1db954; transform: translateY(-2px); box-shadow: 0 6px 20px rgba(37,211,102,.4); }

    /* ── FOOTER ──────────────────────────── */
    footer {
      padding: 2rem 8vw;
      border-top: 1px solid rgba(255,255,255,.05);
      display: flex; justify-content: space-between; align-items: center;
      color: rgba(255,255,255,.18); font-size: .77rem; flex-wrap: wrap; gap: .5rem;
    }

    /* ── RESPONSIVE ──────────────────────── */
    @media (max-width: 640px) {
      .metrics   { gap: 1.2rem; }
      .contact-wrap { padding: 2.2rem 2rem; }
      footer     { flex-direction: column; text-align: center; }
      .data-table td:first-child { width: 44%; }
    }
  </style>
</head>
<body>

<!-- ═══════════ HERO ════════════════════════════════════ -->
<section class="hero">
  <canvas id="terrain-canvas"></canvas>
  <div class="hero-overlay"></div>

  <div class="hero-content">
    <div class="tag">Ativo Ambiental Estratégico</div>

    <h1>Vale do<br><strong>Jequitinhonha</strong></h1>

    <p class="subtitle">
      669 hectares com nascentes preservadas, mata nativa e potencial institucional para
      compensação ambiental, ESG e crédito de carbono em Minas Gerais.
    </p>

    <div class="metrics">
      <div class="metric">
        <div class="metric-value">669,4</div>
        <div class="metric-label">Hectares</div>
      </div>
      <div class="metric">
        <div class="metric-value">3</div>
        <div class="metric-label">Nascentes</div>
      </div>
      <div class="metric">
        <div class="metric-value">2</div>
        <div class="metric-label">Biomas</div>
      </div>
    </div>

    <div class="cta-group">
      <a href="https://wa.me/5531984019395" class="btn-primary" target="_blank" rel="noopener">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
        Solicitar dossiê completo
      </a>
      <a href="#dados" class="btn-ghost">Ver dados técnicos</a>
    </div>
  </div>
</section>

<!-- ═══════════ VALOR ════════════════════════════════════ -->
<section class="value-section">
  <span class="sec-label">Potencial estratégico</span>
  <h2 class="sec-title reveal">Um dos poucos ativos ambientais<br><strong>estruturados no Brasil</strong></h2>

  <div class="cards">
    <div class="card reveal">
      <div class="card-icon">🌊</div>
      <h3>Proteção Hídrica</h3>
      <p>3 nascentes catalogadas e APPs intactas. Recurso hídrico de alto valor institucional e regulatório em bioma de transição.</p>
    </div>
    <div class="card reveal">
      <div class="card-icon">🌿</div>
      <h3>Reserva Legal & CRA</h3>
      <p>Elegível à emissão de Cotas de Reserva Ambiental. Instrumento de compensação imediata para produtores e empresas com passivo florestal.</p>
    </div>
    <div class="card reveal">
      <div class="card-icon">🏛️</div>
      <h3>ESG Corporativo</h3>
      <p>Aquisição aplicável a relatórios ESG, neutralização de emissões e metas de mitigação ambiental para grupos industriais.</p>
    </div>
    <div class="card reveal">
      <div class="card-icon">♻️</div>
      <h3>Crédito de Carbono</h3>
      <p>Mata nativa com potencial de certificação REDD+/VCS. Geração de receita contínua por sequestro de carbono verificado.</p>
    </div>
    <div class="card reveal">
      <div class="card-icon">📋</div>
      <h3>RPPN</h3>
      <p>Área elegível à criação de Reserva Particular do Patrimônio Natural, com status de Unidade de Conservação privada.</p>
    </div>
    <div class="card reveal">
      <div class="card-icon">📐</div>
      <h3>Documentação Sólida</h3>
      <p>Área georreferenciada, KML disponível e estrutura documental organizada para due diligence imediata.</p>
    </div>
  </div>
</section>

<!-- ═══════════ DADOS TÉCNICOS ═══════════════════════════ -->
<section class="data-section" id="dados">
  <span class="sec-label">Dados técnicos</span>
  <h2 class="sec-title reveal"><strong>Especificações</strong> do ativo</h2>

  <table class="data-table reveal">
    <tr><td>Nome</td><td>Fazenda Chapada das Dornelas</td></tr>
    <tr><td>Localização</td><td>Vale do Jequitinhonha, Minas Gerais</td></tr>
    <tr><td>Região</td><td>Norte de Minas Gerais</td></tr>
    <tr><td>Bioma</td><td>Transição Cerrado / Mata Atlântica</td></tr>
    <tr><td>Área total</td><td>~669,4 hectares</td></tr>
    <tr><td>Recursos hídricos</td><td>3 nascentes catalogadas + Áreas de Preservação Permanente</td></tr>
    <tr><td>Cobertura vegetal</td><td>Mata nativa preservada</td></tr>
    <tr><td>Georreferenciamento</td><td>Concluído — material KML disponível</td></tr>
    <tr><td>Uso potencial</td><td>Reserva Legal · CRA · Carbono · RPPN · ESG · PSA</td></tr>
    <tr><td>Coordenadas centrais</td><td>16°22'S, 41°14'W — Norte de Minas Gerais</td></tr>
  </table>
</section>

<!-- ═══════════ COMPRADORES ══════════════════════════════ -->
<section>
  <span class="sec-label">Para quem é este ativo</span>
  <h2 class="sec-title reveal">Perfis de <strong>compradores estratégicos</strong></h2>

  <div class="buyers-grid">
    <div class="buyer-card reveal">
      <div class="buyer-type">Empresas com passivo florestal</div>
      <h3>Compensação de Reserva Legal</h3>
      <ul>
        <li>Regularização via CRA ou compra direta</li>
        <li>Evitar recomposição interna de área produtiva</li>
        <li>Conformidade com Código Florestal</li>
        <li>Cumprimento de TACs e licenças ambientais</li>
      </ul>
    </div>
    <div class="buyer-card reveal">
      <div class="buyer-type">Mineração · Siderurgia · Energia</div>
      <h3>Mitigação Ambiental Institucional</h3>
      <ul>
        <li>Atendimento a exigências de licenciamento</li>
        <li>Criação de RPPNs corporativas</li>
        <li>Proteção de bacias hidrográficas</li>
        <li>Relatórios ESG e neutralização de emissões</li>
      </ul>
    </div>
    <div class="buyer-card reveal">
      <div class="buyer-type">Fundos Verdes · Gestoras · Investidores</div>
      <h3>Ativo Natural com Retorno</h3>
      <ul>
        <li>Portfólio de ativos ambientais preservados</li>
        <li>Crédito de carbono certificado (REDD+/VCS)</li>
        <li>Pagamento por Serviços Ambientais (PSA)</li>
        <li>Elegível a fundos BNDES Economia Verde</li>
      </ul>
    </div>
  </div>
</section>

<!-- ═══════════ CONTATO ═══════════════════════════════════ -->
<section class="contact-section">
  <span class="sec-label">Contato exclusivo</span>
  <h2 class="sec-title reveal">Inicie uma <strong>conversa estratégica</strong></h2>
  <p class="reveal" style="color:var(--muted);margin-bottom:2.5rem;font-size:1rem;max-width:480px;margin-left:auto;margin-right:auto;">
    Este ativo é apresentado por convite a compradores qualificados. Entre em contato para receber o dossiê técnico completo.
  </p>

  <div class="contact-wrap reveal">
    <span class="contact-name">Responsável pelo ativo — Dedé</span>
    <span class="contact-num">+55 31 98401-9395</span>
    <a href="https://wa.me/5531984019395" class="btn-whatsapp" target="_blank" rel="noopener">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
      Falar pelo WhatsApp
    </a>
  </div>
</section>

<!-- ═══════════ FOOTER ════════════════════════════════════ -->
<footer>
  <span>Ativo Ambiental Estratégico — Vale do Jequitinhonha, MG</span>
  <span>Documento confidencial. Informações sujeitas a due diligence.</span>
</footer>

<script>
// ─────────────────────────────────────────────
//  TERRAIN CANVAS — motion background
// ─────────────────────────────────────────────
const canvas = document.getElementById('terrain-canvas');
const ctx = canvas.getContext('2d');

const KML = [
  [-41.24157408021180,-16.35871916628119],
  [-41.23697413103431,-16.35948457060619],
  [-41.23288227985831,-16.36036017436003],
  [-41.22603627982108,-16.36168517750197],
  [-41.22020535879830,-16.36015462441980],
  [-41.21917171855716,-16.35987901241211],
  [-41.21278143282737,-16.36528892380832],
  [-41.21194915967378,-16.36601579394231],
  [-41.21209099164152,-16.36648910051493],
  [-41.21249398778585,-16.36738110431585],
  [-41.21340921942644,-16.36811178752243],
  [-41.21422860851112,-16.36845062396701],
  [-41.21436957562284,-16.36861913976561],
  [-41.21452889404864,-16.36977909789862],
  [-41.21470048724678,-16.36999662407410],
  [-41.21515013789436,-16.37002336638031],
  [-41.21544504707198,-16.37057773926756],
  [-41.21551122954077,-16.37223155973622],
  [-41.21538284233142,-16.37348425552779],
  [-41.21546894698477,-16.37363718725911],
  [-41.21662135744973,-16.37983036713758],
  [-41.21684151104886,-16.38045729827080],
  [-41.21681871461655,-16.38073652963350],
  [-41.21745599348817,-16.38080843447131],
  [-41.21854498741154,-16.38083277105119],
  [-41.22033392423565,-16.38088407020013],
  [-41.22150125060113,-16.37793487670923],
  [-41.22164550767187,-16.37761360112446],
  [-41.23196498568152,-16.37969941361992],
  [-41.23213598725943,-16.37970391018544],
  [-41.23406647961712,-16.37893730037541],
  [-41.23752418090592,-16.37736490668485],
  [-41.24361185182342,-16.37452085990848],
  [-41.24377308730194,-16.37463552251803],
  [-41.24402858313445,-16.37433199239873],
  [-41.24880285664147,-16.37205369563381],
  [-41.24894158754107,-16.37193816219293],
  [-41.25330395038859,-16.36795532717940],
  [-41.25389153984373,-16.36756241421106],
  [-41.25327773348214,-16.36673967583893],
  [-41.25271779399833,-16.36591266782980],
  [-41.25253673912766,-16.36555351553152],
  [-41.25234950463539,-16.36457868282990],
  [-41.25235656358515,-16.36434378441931],
  [-41.25246344292757,-16.36366330989748],
  [-41.25220208910907,-16.36266667118746],
  [-41.25084763953333,-16.36148933654444],
  [-41.25037416542619,-16.36108696013472],
  [-41.24990922520146,-16.36056560773766],
  [-41.24973530872445,-16.36016588712296],
  [-41.24940458950984,-16.36003358119756],
  [-41.24833471959808,-16.35923304489606],
  [-41.24708396818383,-16.35885732762478],
  [-41.24631516405518,-16.35870571937349],
  [-41.24594142762399,-16.35910606207177],
  [-41.24579499920963,-16.35918870072684],
  [-41.24545624260633,-16.35926820841262],
  [-41.24157408021180,-16.35871916628119],
];

const lons = KML.map(c => c[0]);
const lats = KML.map(c => c[1]);
const lonMin = Math.min(...lons), lonMax = Math.max(...lons);
const latMin = Math.min(...lats), latMax = Math.max(...lats);
const lonRange = lonMax - lonMin;
const latRange = latMax - latMin;

const PARTICLE_COUNT = 65;
let particles = [];

function resize() {
  const hero = canvas.parentElement;
  canvas.width  = hero.offsetWidth;
  canvas.height = hero.offsetHeight;
  spawnParticles();
}

function project(lon, lat, W, H) {
  const pad = Math.min(W, H) * 0.06;
  const rx = W * 0.36, ry = pad, rw = W * 0.62 - pad, rh = H - pad * 2;

  const aspect = lonRange / latRange;
  let dw, dh, ox, oy;
  if (rw / rh > aspect) {
    dh = rh; dw = dh * aspect;
    ox = rx + (rw - dw) / 2; oy = ry;
  } else {
    dw = rw; dh = dw / aspect;
    ox = rx; oy = ry + (rh - dh) / 2;
  }

  return [
    ox + (lon - lonMin) / lonRange * dw,
    oy + (latMax - lat) / latRange * dh,
  ];
}

function getPoints(W, H) {
  return KML.map(([lon, lat]) => project(lon, lat, W, H));
}

function centroid(pts) {
  const cx = pts.reduce((s, p) => s + p[0], 0) / pts.length;
  const cy = pts.reduce((s, p) => s + p[1], 0) / pts.length;
  return [cx, cy];
}

function spawnParticles() {
  particles = [];
  const pts = getPoints(canvas.width, canvas.height);
  const [cx, cy] = centroid(pts);
  for (let i = 0; i < PARTICLE_COUNT; i++) {
    const angle = Math.random() * Math.PI * 2;
    const rad   = Math.random() * Math.min(canvas.width, canvas.height) * 0.22;
    particles.push({
      x:     cx + Math.cos(angle) * rad,
      y:     cy + Math.sin(angle) * rad,
      vx:    (Math.random() - 0.5) * 0.25,
      vy:    -(0.25 + Math.random() * 0.55),
      r:     0.8 + Math.random() * 1.8,
      alpha: 0.25 + Math.random() * 0.5,
      life:  Math.random(),
      reset() {
        const a = Math.random() * Math.PI * 2;
        const d = Math.random() * Math.min(canvas.width, canvas.height) * 0.22;
        this.x = cx + Math.cos(a) * d;
        this.y = cy + Math.sin(a) * d;
        this.life = 0;
      }
    });
  }
}

let scanOffset = 0;

function draw(t) {
  const W = canvas.width, H = canvas.height;
  const pts = getPoints(W, H);
  const [cx, cy] = centroid(pts);
  const pulse = Math.sin(t * 0.7) * 0.5 + 0.5;

  ctx.clearRect(0, 0, W, H);

  ctx.fillStyle = '#040c08';
  ctx.fillRect(0, 0, W, H);

  for (let ring = 5; ring >= 1; ring--) {
    ctx.beginPath();
    pts.forEach(([x, y], i) => i ? ctx.lineTo(x, y) : ctx.moveTo(x, y));
    ctx.closePath();
    const a = (0.018 + pulse * 0.012) * (ring / 5);
    ctx.strokeStyle = `rgba(61,191,114,${a})`;
    ctx.lineWidth = ring * 14;
    ctx.lineJoin = 'round';
    ctx.stroke();
  }

  const gFill = ctx.createLinearGradient(cx - W * 0.2, cy - H * 0.3, cx + W * 0.15, cy + H * 0.3);
  gFill.addColorStop(0,   `rgba(26,75,46,${0.52 + pulse * 0.1})`);
  gFill.addColorStop(0.5, `rgba(18,54,32,${0.46})`);
  gFill.addColorStop(1,   `rgba(10,30,18,${0.5})`);

  ctx.beginPath();
  pts.forEach(([x, y], i) => i ? ctx.lineTo(x, y) : ctx.moveTo(x, y));
  ctx.closePath();
  ctx.fillStyle = gFill;
  ctx.fill();

  ctx.save();
  ctx.beginPath();
  pts.forEach(([x, y], i) => i ? ctx.lineTo(x, y) : ctx.moveTo(x, y));
  ctx.closePath();
  ctx.clip();

  const gs = 28;
  ctx.strokeStyle = 'rgba(61,191,114,0.045)';
  ctx.lineWidth = 0.5;
  for (let gx = 0; gx < W; gx += gs) { ctx.beginPath(); ctx.moveTo(gx,0); ctx.lineTo(gx,H); ctx.stroke(); }
  for (let gy = 0; gy < H; gy += gs) { ctx.beginPath(); ctx.moveTo(0,gy); ctx.lineTo(W,gy); ctx.stroke(); }

  scanOffset = (scanOffset + 0.5) % (H + 120);
  const sy = scanOffset - 60;
  const gScan = ctx.createLinearGradient(0, sy - 70, 0, sy + 70);
  gScan.addColorStop(0,   'rgba(61,191,114,0)');
  gScan.addColorStop(0.5, `rgba(61,191,114,${0.07 + pulse * 0.05})`);
  gScan.addColorStop(1,   'rgba(61,191,114,0)');
  ctx.fillStyle = gScan;
  ctx.fillRect(0, sy - 70, W, 140);

  ctx.restore();

  ctx.beginPath();
  pts.forEach(([x, y], i) => i ? ctx.lineTo(x, y) : ctx.moveTo(x, y));
  ctx.closePath();
  ctx.strokeStyle = `rgba(61,191,114,${0.55 + pulse * 0.3})`;
  ctx.lineWidth = 1.5;
  ctx.lineJoin = 'round';
  ctx.stroke();

  pts.forEach(([x, y]) => {
    ctx.beginPath();
    ctx.arc(x, y, 2.2, 0, Math.PI * 2);
    ctx.fillStyle = `rgba(104,223,160,${0.45 + pulse * 0.35})`;
    ctx.fill();
  });

  ctx.save();
  ctx.globalAlpha = 0.7 + pulse * 0.2;
  ctx.font = `bold ${Math.max(11, Math.min(14, W * 0.012))}px 'Segoe UI', sans-serif`;
  ctx.fillStyle = 'rgba(61,191,114,0.9)';
  ctx.textAlign = 'center';
  ctx.fillText('669,4 ha', cx, cy - 8);
  ctx.font = `${Math.max(9, Math.min(11, W * 0.009))}px 'Segoe UI', sans-serif`;
  ctx.fillStyle = 'rgba(110,168,130,0.7)';
  ctx.fillText('Fazenda Chapada das Dornelas', cx, cy + 12);
  ctx.restore();

  const [cx2, cy2] = centroid(getPoints(W, H));
  particles.forEach(p => {
    p.x += p.vx; p.y += p.vy;
    p.life += 0.0045;
    if (p.life >= 1) p.reset();
    const alpha = p.alpha * Math.sin(p.life * Math.PI) * 0.85;
    ctx.beginPath();
    ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
    ctx.fillStyle = `rgba(61,191,114,${alpha})`;
    ctx.fill();
  });

  const [cr_x, cr_y] = [pts.reduce((m,p) => Math.max(m,p[0]),0) - 30, pts.reduce((m,p) => Math.min(m,p[1]),H) + 22];
  drawCompass(cr_x, cr_y, 12, t, pulse);
}

function drawCompass(x, y, r, t, pulse) {
  ctx.save();
  ctx.globalAlpha = 0.55 + pulse * 0.2;
  ctx.beginPath();
  ctx.moveTo(x, y - r); ctx.lineTo(x - 4, y + 4); ctx.lineTo(x, y + 1); ctx.lineTo(x + 4, y + 4); ctx.closePath();
  ctx.fillStyle = 'rgba(61,191,114,0.9)';
  ctx.fill();
  ctx.font = `bold ${r - 2}px 'Segoe UI',sans-serif`;
  ctx.fillStyle = 'rgba(61,191,114,0.8)';
  ctx.textAlign = 'center';
  ctx.fillText('N', x, y - r - 4);
  ctx.restore();
}

function animate(ts) {
  draw(ts / 1000);
  requestAnimationFrame(animate);
}

window.addEventListener('resize', resize);
resize();
requestAnimationFrame(animate);

// ─────────────────────────────────────────────
//  SCROLL REVEAL
// ─────────────────────────────────────────────
const obs = new IntersectionObserver(entries => {
  entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('in'); });
}, { threshold: 0.1 });
document.querySelectorAll('.reveal').forEach(el => obs.observe(el));
</script>
</body>
</html>
