<!doctype html>
<html lang="de">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>FlowForge Studio – Software für smarte Workflows</title>
  <meta name="description" content="FlowForge Studio ist ein moderner Webshop für Workflow-Automatisierungssoftware für Start-ups, Agenturen und kleine Unternehmen.">
  <style>
    :root {
      --bg: #f6f8fb;
      --surface: #ffffff;
      --surface-soft: #eef5f2;
      --text: #111827;
      --muted: #526173;
      --brand: #126049;
      --brand-dark: #07382d;
      --blue: #2257c8;
      --accent: #ffc857;
      --border: #d8e1e8;
      --shadow: 0 22px 60px rgba(17, 24, 39, .12);
      --radius: 24px;
      --max: 1180px;
    }

    * { box-sizing: border-box; }
    html { scroll-behavior: smooth; }
    body {
      margin: 0;
      font-family: Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      background: var(--bg);
      color: var(--text);
      line-height: 1.6;
      font-size: 17px;
    }

    a { color: var(--blue); text-underline-offset: .22em; }
    a:hover { text-decoration-thickness: .15em; }
    button, input, textarea, select { font: inherit; }
    img, svg { max-width: 100%; height: auto; }
    :focus-visible { outline: 4px solid var(--accent); outline-offset: 4px; border-radius: 10px; }

    .skip-link {
      position: absolute;
      left: 1rem;
      top: .5rem;
      transform: translateY(-180%);
      background: #111827;
      color: white;
      padding: .8rem 1rem;
      border-radius: 999px;
      z-index: 1000;
    }
    .skip-link:focus { transform: translateY(0); }

    header {
      background:
        radial-gradient(circle at 20% 20%, rgba(255, 200, 87, .34), transparent 26%),
        radial-gradient(circle at 82% 18%, rgba(69, 130, 246, .22), transparent 28%),
        linear-gradient(135deg, #062d25 0%, #126049 58%, #1a7b5e 100%);
      color: white;
      overflow: hidden;
    }

    .topbar {
      max-width: var(--max);
      margin: auto;
      padding: 1rem;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 1rem;
      flex-wrap: wrap;
    }

    .logo {
      display: inline-flex;
      align-items: center;
      gap: .75rem;
      color: white;
      font-weight: 900;
      font-size: 1.28rem;
      letter-spacing: -.04em;
      text-decoration: none;
    }

    nav ul {
      list-style: none;
      padding: 0;
      margin: 0;
      display: flex;
      gap: .35rem;
      flex-wrap: wrap;
      align-items: center;
    }

    nav a {
      color: white;
      text-decoration: none;
      display: inline-flex;
      padding: .55rem .8rem;
      border-radius: 999px;
      font-weight: 700;
      font-size: .95rem;
    }

    nav a:hover { background: rgba(255,255,255,.16); }

    .hero {
      max-width: var(--max);
      margin: auto;
      padding: 4.5rem 1rem 6rem;
      display: grid;
      grid-template-columns: minmax(0, 1.05fr) minmax(320px, .95fr);
      gap: 2rem;
      align-items: center;
    }

    .eyebrow {
      display: inline-flex;
      align-items: center;
      gap: .5rem;
      background: rgba(255,255,255,.14);
      border: 1px solid rgba(255,255,255,.28);
      border-radius: 999px;
      padding: .45rem .75rem;
      font-weight: 800;
      margin-bottom: 1rem;
    }

    h1, h2, h3 { line-height: 1.08; }
    h1 {
      font-size: clamp(2.7rem, 7vw, 5.7rem);
      max-width: 11ch;
      letter-spacing: -.075em;
      margin: 0 0 1.1rem;
    }
    .hero p {
      font-size: 1.22rem;
      max-width: 62ch;
      color: #edf8f3;
      margin: 0;
    }

    .actions { display: flex; gap: .8rem; flex-wrap: wrap; margin-top: 1.6rem; }
    .btn {
      border: 0;
      border-radius: 999px;
      padding: .9rem 1.2rem;
      font-weight: 900;
      text-decoration: none;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: .45rem;
      cursor: pointer;
      min-height: 48px;
    }
    .btn-primary { background: var(--accent); color: #15110a; }
    .btn-light { background: white; color: var(--brand); }
    .btn-outline { background: transparent; color: var(--brand); border: 2px solid var(--border); }
    .btn-dark { background: var(--brand-dark); color: white; }

    .hero-card {
      background: rgba(255,255,255,.95);
      color: var(--text);
      border-radius: 32px;
      padding: 1rem;
      box-shadow: var(--shadow);
      transform: rotate(1deg);
    }
    .app-window {
      border: 1px solid var(--border);
      border-radius: 24px;
      background: white;
      overflow: hidden;
    }
    .window-top {
      display: flex;
      justify-content: space-between;
      align-items: center;
      background: #eef3f7;
      padding: .75rem;
    }
    .traffic { display: flex; gap: .35rem; }
    .dot { width: .75rem; height: .75rem; border-radius: 999px; background: var(--brand); opacity: .65; }
    .app-body { padding: 1rem; display: grid; gap: .85rem; }
    .metric-row { display: grid; grid-template-columns: repeat(3, 1fr); gap: .65rem; }
    .metric { background: var(--surface-soft); border-radius: 18px; padding: .85rem; }
    .metric strong { display: block; font-size: 1.4rem; }
    .flow-node {
      display: grid;
      grid-template-columns: auto 1fr auto;
      gap: .75rem;
      align-items: center;
      border: 1px solid var(--border);
      border-radius: 18px;
      padding: .85rem;
    }
    .pulse { width: 1rem; height: 1rem; border-radius: 999px; background: var(--accent); animation: pulse 1.8s infinite; }
    @keyframes pulse { 0%, 100% { transform: scale(1); opacity: 1; } 50% { transform: scale(1.3); opacity: .55; } }
    @media (prefers-reduced-motion: reduce) {
      html { scroll-behavior: auto; }
      *, *::before, *::after { animation-duration: .01ms !important; animation-iteration-count: 1 !important; transition-duration: .01ms !important; }
    }

    main section, footer section {
      max-width: var(--max);
      margin: auto;
      padding: 4.5rem 1rem;
    }
    .section-head { max-width: 780px; margin-bottom: 2.2rem; }
    .section-head h2 {
      font-size: clamp(2rem, 4vw, 3.6rem);
      letter-spacing: -.06em;
      margin: 0 0 .8rem;
    }
    .section-head p { margin: 0; color: var(--muted); font-size: 1.08rem; }

    .grid-3 { display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 1rem; }
    .grid-2 { display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 1rem; }
    .card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 1.35rem;
      box-shadow: 0 8px 28px rgba(17, 24, 39, .055);
    }
    .card h3 { margin-top: .1rem; font-size: 1.38rem; letter-spacing: -.025em; }
    .muted { color: var(--muted); }
    .tag {
      display: inline-flex;
      align-items: center;
      background: var(--surface-soft);
      color: var(--brand);
      padding: .28rem .65rem;
      border-radius: 999px;
      font-weight: 900;
      font-size: .88rem;
    }

    .feature-list { padding-left: 1.2rem; margin-bottom: 0; }
    .feature-list li { margin-bottom: .35rem; }
    .pricing-card { position: relative; display: flex; flex-direction: column; }
    .pricing-card.highlight {
      border: 2px solid var(--brand);
      box-shadow: 0 22px 55px rgba(18, 96, 73, .16);
    }
    .price { font-weight: 950; letter-spacing: -.06em; font-size: 2.7rem; margin: .6rem 0; }
    .price small { font-size: 1rem; letter-spacing: 0; color: var(--muted); }
    .pricing-card .btn { margin-top: auto; }

    .showcase {
      background: #101827;
      color: white;
      border-radius: 36px;
      padding: 2rem;
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 1rem;
      align-items: center;
      overflow: hidden;
    }
    .showcase p { color: #d7e2ed; }
    .showcase-visual {
      min-height: 260px;
      border-radius: 28px;
      background: radial-gradient(circle at 25% 20%, rgba(255,200,87,.8), transparent 22%), linear-gradient(135deg, #dff3ec, #ffffff);
      display: grid;
      place-items: center;
      border: 1px solid rgba(255,255,255,.2);
    }

    form { display: grid; gap: 1rem; }
    label { display: block; font-weight: 850; margin-bottom: .25rem; }
    input, textarea, select {
      width: 100%;
      padding: .85rem;
      border-radius: 14px;
      border: 2px solid var(--border);
      background: white;
      color: var(--text);
    }
    textarea { resize: vertical; }
    .inline-check { display: flex; align-items: flex-start; gap: .6rem; }
    .inline-check input { width: auto; margin-top: .35rem; }
    .notice {
      background: var(--surface-soft);
      border-left: 5px solid var(--brand);
      border-radius: 14px;
      padding: 1rem;
    }
    .legal-box {
      background: white;
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 1.35rem;
      margin: 1rem 0;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      background: white;
      border-radius: var(--radius);
      overflow: hidden;
      border: 1px solid var(--border);
    }
    th, td { padding: .85rem; text-align: left; border-bottom: 1px solid var(--border); vertical-align: top; }
    th { background: var(--surface-soft); }

    .cart {
      position: sticky;
      bottom: 1rem;
      z-index: 80;
      max-width: var(--max);
      margin: auto;
      padding: 0 1rem 1rem;
    }
    .cart-inner {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 1rem;
      flex-wrap: wrap;
      background: #111827;
      color: white;
      border-radius: 999px;
      padding: .75rem 1rem;
      box-shadow: var(--shadow);
    }
    .cart-inner strong { color: white; }

    footer {
      background: #101827;
      color: #eaf0f6;
      margin-top: 3rem;
    }
    footer a { color: #ffe08a; }
    .footer-grid { display: grid; grid-template-columns: 1.3fr 1fr 1fr; gap: 1.2rem; }

    @media (max-width: 900px) {
      .hero, .grid-3, .grid-2, .showcase, .footer-grid { grid-template-columns: 1fr; }
      .hero { padding-top: 3rem; }
      .metric-row { grid-template-columns: 1fr; }
      .hero-card { transform: none; }
      body { font-size: 16px; }
      .cart-inner { border-radius: 24px; }
    }
  </style>
</head>
<body>
  <a class="skip-link" href="#main">Zum Hauptinhalt springen</a>

  <header id="home">
    <div class="topbar">
      <a class="logo" href="#home" aria-label="FlowForge Startseite">
        <svg width="44" height="44" viewBox="0 0 64 64" role="img" aria-labelledby="logoTitle">
          <title id="logoTitle">FlowForge Logo: verbundenes Sechseck mit drei Knoten</title>
          <rect width="64" height="64" rx="17" fill="#ffc857"></rect>
          <path d="M18 34 L30 18 L46 24 L42 44 L24 46 Z" fill="none" stroke="#07382d" stroke-width="5" stroke-linejoin="round"></path>
          <circle cx="30" cy="18" r="4.2" fill="#07382d"></circle>
          <circle cx="46" cy="24" r="4.2" fill="#07382d"></circle>
          <circle cx="24" cy="46" r="4.2" fill="#07382d"></circle>
        </svg>
        <span>FlowForge</span>
      </a>
      <nav aria-label="Hauptnavigation">
        <ul>
          <li><a href="#features">Funktionen</a></li>
          <li><a href="#shop">Preise</a></li>
          <li><a href="#about">Über uns</a></li>
          <li><a href="#lizenz">Lizenz</a></li>
          <li><a href="#kontakt">Kontakt</a></li>
        </ul>
      </nav>
    </div>

    <div class="hero">
      <div>
        <span class="eyebrow">Workflow-Software für kleine Teams</span>
        <h1>Mehr Flow. Weniger Routine.</h1>
        <p>FlowForge Studio automatisiert wiederkehrende Büroprozesse: Anfragen, Aufgaben, Rechnungen und Kundenkommunikation laufen in klaren Workflows zusammen.</p>
        <div class="actions">
          <a class="btn btn-primary" href="#shop">Pakete ansehen</a>
          <a class="btn btn-light" href="#features">Demo entdecken</a>
        </div>
      </div>

      <div class="hero-card" aria-label="Vorschau der FlowForge Softwareoberfläche">
        <div class="app-window">
          <div class="window-top">
            <div class="traffic" aria-hidden="true"><span class="dot"></span><span class="dot"></span><span class="dot"></span></div>
            <strong>Live Dashboard</strong>
          </div>
          <div class="app-body">
            <div class="metric-row" aria-label="Beispielhafte Kennzahlen">
              <div class="metric"><span class="muted">Zeit gespart</span><strong>12h</strong></div>
              <div class="metric"><span class="muted">Workflows</span><strong>24</strong></div>
              <div class="metric"><span class="muted">Erledigt</span><strong>91%</strong></div>
            </div>
            <div class="flow-node"><span class="pulse" aria-hidden="true"></span><strong>Neue Anfrage</strong><span class="tag">Trigger</span></div>
            <div class="flow-node"><span class="pulse" aria-hidden="true"></span><strong>Ticket erstellen</strong><span class="tag">Auto</span></div>
            <div class="flow-node"><span class="pulse" aria-hidden="true"></span><strong>Antwort senden</strong><span class="tag">E-Mail</span></div>
          </div>
        </div>
      </div>
    </div>
  </header>

  <main id="main">
    <section id="features">
      <div class="section-head">
        <h2>Alles, was dein Team für klare Prozesse braucht.</h2>
        <p>FlowForge Studio ist eine fiktive SaaS-Businessanwendung für Start-ups, Agenturen, Freelancer und kleine Unternehmen.</p>
      </div>
      <div class="grid-3">
        <article class="card">
          <span class="tag">No-Code</span>
          <h3>Workflow Builder</h3>
          <p>Erstelle Abläufe mit einfachen Wenn-Dann-Regeln, ohne Programmierung. Ideal für Angebote, Rechnungen, Support und interne Freigaben.</p>
        </article>
        <article class="card">
          <span class="tag">Teamwork</span>
          <h3>Aufgaben & Rollen</h3>
          <p>Weise Aufgaben automatisch zu, vergib Rollen und behalte im Dashboard den Überblick über offene Schritte.</p>
        </article>
        <article class="card">
          <span class="tag">Reports</span>
          <h3>Klare Auswertungen</h3>
          <p>Sieh, welche Prozesse Zeit sparen, wo Engpässe entstehen und welche Workflows optimiert werden sollten.</p>
        </article>
      </div>
    </section>

    <section>
      <div class="showcase">
        <div>
          <span class="tag">Produktdemo</span>
          <h2>Vom Auftrag zur Rechnung in einem Flow.</h2>
          <p>Neue Bestellungen können automatisch in Aufgaben, Benachrichtigungen und Rechnungsentwürfe umgewandelt werden. In dieser Demo ist der Prozess vollständig gemockt und sendet keine echten Daten.</p>
          <button class="btn btn-primary" onclick="playSonicLogo()">Hörmarke abspielen</button>
        </div>
        <div class="showcase-visual" role="img" aria-label="Illustration eines automatisierten Workflows von Lead zu Flow zu Done">
          <svg viewBox="0 0 640 300" aria-hidden="true">
            <defs><linearGradient id="g" x1="0" x2="1"><stop stop-color="#126049"/><stop offset="1" stop-color="#2257c8"/></linearGradient></defs>
            <rect x="40" y="54" width="160" height="86" rx="22" fill="#fff" stroke="#126049" stroke-width="5"/>
            <rect x="240" y="108" width="160" height="86" rx="22" fill="#fff" stroke="#2257c8" stroke-width="5"/>
            <rect x="440" y="54" width="160" height="86" rx="22" fill="#fff" stroke="#126049" stroke-width="5"/>
            <path d="M200 98 C230 98 220 152 240 152 M400 152 C430 152 410 98 440 98" fill="none" stroke="url(#g)" stroke-width="8" stroke-linecap="round"/>
            <text x="78" y="108" font-size="28" fill="#111827" font-weight="800">Lead</text>
            <text x="278" y="162" font-size="28" fill="#111827" font-weight="800">Flow</text>
            <text x="470" y="108" font-size="28" fill="#111827" font-weight="800">Done</text>
          </svg>
        </div>
      </div>
    </section>

    <section id="shop">
      <div class="section-head">
        <h2>Wähle dein Paket.</h2>
        <p>Starte kostenlos und erweitere dein Team, sobald deine Prozesse wachsen. Der Checkout ist eine Demo und löst keine Zahlung aus.</p>
      </div>
      <div class="grid-3" aria-label="Preispläne">
        <article class="card pricing-card">
          <span class="tag">Starter</span>
          <h3>Free</h3>
          <p class="price">0 € <small>/ Monat</small></p>
          <p class="muted">Für Einzelpersonen, die Workflows testen möchten.</p>
          <ul class="feature-list">
            <li>3 aktive Workflows</li>
            <li>1 Nutzerkonto</li>
            <li>Community-Support</li>
          </ul>
          <button class="btn btn-outline" data-plan="Free" data-price="0">Auswählen</button>
        </article>

        <article class="card pricing-card highlight">
          <span class="tag">Beliebt</span>
          <h3>Pro</h3>
          <p class="price">19 € <small>/ Monat</small></p>
          <p class="muted">Für kleine Teams mit regelmäßigen Abläufen.</p>
          <ul class="feature-list">
            <li>Unbegrenzte Workflows</li>
            <li>5 Nutzerkonten</li>
            <li>E-Mail-Support</li>
            <li>CSV-Export</li>
          </ul>
          <button class="btn btn-primary" data-plan="Pro" data-price="19">Auswählen</button>
        </article>

        <article class="card pricing-card">
          <span class="tag">Scale</span>
          <h3>Business</h3>
          <p class="price">49 € <small>/ Monat</small></p>
          <p class="muted">Für wachsende Firmen mit mehreren Teams.</p>
          <ul class="feature-list">
            <li>20 Nutzerkonten</li>
            <li>Rollen & Rechte</li>
            <li>Priorisierter Support</li>
            <li>Erweiterte Reports</li>
          </ul>
          <button class="btn btn-outline" data-plan="Business" data-price="49">Auswählen</button>
        </article>
      </div>

      <div class="legal-box" id="checkout" aria-live="polite">
        <h3>Checkout</h3>
        <p class="muted">Demo-Bestellung: Es werden keine echten Daten übertragen und keine Zahlungen verarbeitet.</p>
        <form onsubmit="event.preventDefault(); fakeOrder();">
          <div class="grid-2">
            <div>
              <label for="name">Name</label>
              <input id="name" name="name" autocomplete="name" required>
            </div>
            <div>
              <label for="email">E-Mail-Adresse</label>
              <input id="email" name="email" type="email" autocomplete="email" required>
            </div>
          </div>
          <div>
            <label for="payment">Zahlungsart</label>
            <select id="payment" name="payment">
              <option>Rechnung</option>
              <option>Kreditkarte (Demo)</option>
              <option>SEPA (Demo)</option>
            </select>
          </div>
          <div class="inline-check">
            <input id="terms" type="checkbox" required>
            <label for="terms">Ich akzeptiere die Lizenzbedingungen und die Hinweise zur Datenverarbeitung.</label>
          </div>
          <button class="btn btn-dark" type="submit">Bestellung simulieren</button>
          <p id="orderStatus" class="notice" hidden></p>
        </form>
      </div>
    </section>

    <section id="about">
      <div class="section-head">
        <h2>Gebaut in Wien. Gemacht für Teams mit Tempo.</h2>
        <p>FlowForge Studio ist ein fiktives Start-up aus Wien. Inhaber ist Lukas Haindl. Das Unternehmen entwickelt eine Softwarelösung für kleine Teams, die wiederkehrende Büroprozesse einfacher automatisieren möchten.</p>
      </div>
      <div class="grid-3">
        <article class="card">
          <h3>Unsere Wortmarke</h3>
          <p><strong>FlowForge</strong> steht für fließende Prozesse und das gezielte Formen digitaler Abläufe. Die Marke ist bewusst eigenständig gewählt und nicht an bekannte Softwaremarken angelehnt.</p>
          <p class="muted">Passende Nizza-Klassen: 9, 35 und 42.</p>
        </article>
        <article class="card">
          <h3>Unsere Bildmarke</h3>
          <p>Das Prozess-Sechseck zeigt verbundene Knoten und steht für stabile, wiederholbare Workflows. Die Form wurde als eigenständige SVG-Grafik erstellt.</p>
          <p class="muted">Passende Nizza-Klassen: 9, 35 und 42.</p>
        </article>
        <article class="card">
          <h3>Unsere Hörmarke</h3>
          <p>Drei kurze, aufsteigende Töne symbolisieren Start, Automatisierung und Abschluss. Sie kann im Demo-Bereich abgespielt werden.</p>
          <p class="muted">Passende Nizza-Klassen: 9, 35 und 42.</p>
        </article>
      </div>
    </section>

    <section id="barrierefreiheit">
      <div class="section-head">
        <h2>Barrierefreiheit</h2>
        <p>Der Shop wurde so gestaltet, dass er für möglichst viele Menschen gut nutzbar ist.</p>
      </div>
      <div class="grid-2">
        <div class="card">
          <h3>Umgesetzte Maßnahmen</h3>
          <ul class="feature-list">
            <li>Semantische HTML-Struktur mit klaren Überschriften.</li>
            <li>Skip-Link zum Hauptinhalt.</li>
            <li>Tastaturbedienbare Navigation und Formulare.</li>
            <li>Sichtbare Fokuszustände.</li>
            <li>Beschriftete Formularfelder und verständliche Fehlvermeidung.</li>
            <li>Ausreichende Farbkontraste und keine Information nur über Farbe.</li>
            <li>Reduzierte Animationen bei aktivierter Systemeinstellung.</li>
          </ul>
        </div>
        <div class="card">
          <h3>Erklärung</h3>
          <p>Diese Website orientiert sich an WCAG 2.2 AA. Vor einer echten Veröffentlichung sollten zusätzlich Tests mit Tastatur, Screenreader, Browser-Zoom, WAVE und axe DevTools durchgeführt werden.</p>
          <p>Feedback zur Barrierefreiheit: accessibility@flowforge.example</p>
        </div>
      </div>
    </section>

    <section id="lizenz">
      <div class="section-head">
        <h2>Lizenzbedingungen</h2>
        <p>Die folgenden Bedingungen beschreiben, welche Rechte Kundinnen und Kunden beim Kauf eines Pakets erhalten.</p>
      </div>
      <div class="legal-box">
        <h3>Nutzungsrechte</h3>
        <p>Mit Abschluss eines kostenpflichtigen Abos erhält die Kundin oder der Kunde ein einfaches, nicht ausschließliches, nicht übertragbares und zeitlich auf die Vertragsdauer beschränktes Recht, FlowForge Studio im gebuchten Umfang zu nutzen.</p>
      </div>
      <div class="legal-box">
        <h3>Rechte des Unternehmens</h3>
        <p>Alle Rechte an Software, Benutzeroberfläche, Logo, Texten, Grafiken, Workflows, Dokumentation und Marken verbleiben bei der FlowForge Labs GmbH. Eine Weiterveräußerung, Unterlizenzierung, Dekompilierung oder öffentliche Bereitstellung ist nicht erlaubt, soweit gesetzlich nichts anderes zwingend gilt.</p>
      </div>
      <div class="legal-box">
        <h3>Haftung</h3>
        <p>FlowForge Labs haftet bei Vorsatz und grober Fahrlässigkeit nach den gesetzlichen Vorschriften. Bei leichter Fahrlässigkeit ist die Haftung, soweit zulässig, auf typische und vorhersehbare Schäden beschränkt. Die Software ersetzt keine Rechts-, Steuer- oder Unternehmensberatung. Für Datenverlust haftet FlowForge Labs nur, soweit der Schaden auch bei angemessener Datensicherung entstanden wäre.</p>
      </div>
    </section>

    <section id="rechte">
      <div class="section-head">
        <h2>Medien & Rechte</h2>
        <p>Alle Medien dieses Shops sind selbst erstellt oder nutzen Systemressourcen. Dadurch bleiben die Verwertungsrechte klar beim fiktiven Unternehmen.</p>
      </div>
      <table aria-label="Medien und Rechte">
        <thead><tr><th>Medium</th><th>Quelle</th><th>Rechte/Lizenz</th></tr></thead>
        <tbody>
          <tr><td>Logo und Bildmarke</td><td>Selbst erstelltes Inline-SVG</td><td>Alle Rechte bei FlowForge Labs GmbH</td></tr>
          <tr><td>Workflow-Illustration</td><td>Selbst erstelltes Inline-SVG</td><td>Alle Rechte bei FlowForge Labs GmbH</td></tr>
          <tr><td>Animationen</td><td>Selbst erstelltes CSS</td><td>Alle Rechte bei FlowForge Labs GmbH</td></tr>
          <tr><td>Hörmarke</td><td>Selbst erstellt per Web-Audio-API</td><td>Alle Rechte bei FlowForge Labs GmbH</td></tr>
          <tr><td>Schriftarten</td><td>Systemschriftarten des Betriebssystems</td><td>Keine extern eingebetteten Font-Dateien</td></tr>
          <tr><td>Texte</td><td>Selbst verfasst</td><td>Alle Rechte bei FlowForge Labs GmbH</td></tr>
        </tbody>
      </table>
    </section>

    <section id="kontakt">
      <div class="section-head">
        <h2>Kontakt</h2>
        <p>Fragen zu Produkt, Lizenz oder Support? Schreib uns. Das Formular ist in dieser Demo ohne echte Übertragung.</p>
      </div>
      <div class="grid-2">
        <form class="card" onsubmit="event.preventDefault(); contactSent();">
          <div>
            <label for="contactName">Name</label>
            <input id="contactName" name="contactName" autocomplete="name" required>
          </div>
          <div>
            <label for="contactEmail">E-Mail-Adresse</label>
            <input id="contactEmail" name="contactEmail" type="email" autocomplete="email" required>
          </div>
          <div>
            <label for="message">Nachricht</label>
            <textarea id="message" name="message" rows="5" required></textarea>
          </div>
          <button class="btn btn-dark" type="submit">Nachricht senden</button>
          <p id="contactStatus" class="notice" hidden></p>
        </form>
        <div class="card">
          <h3>FlowForge Studio GmBH</h3>
          <p>Mariahilfer Straße 88a<br>1070 Wien<br>Österreich</p>
          <p>E-Mail: hello@flowforge.example<br>Telefon: +43 316 000000</p>
          <p>Supportzeiten: Montag bis Freitag, 09:00–17:00 Uhr.</p>
        </div>
      </div>
    </section>

    <section id="datenschutz">
      <div class="section-head">
        <h2>Datenschutzerklärung</h2>
        <p>Hier erklären wir einfach und verständlich, welche Daten bei der Nutzung unseres Demo-Webshops verarbeitet werden können.</p>
      </div>

      <div class="legal-box">
        <h3>Verantwortlicher</h3>
        <p>Verantwortlich für diese Website ist:</p>
        <p><strong>Lukas Haindl</strong><br>
        FlowForge Studio GmBH<br>
        Mariahilfer Straße 88a<br>
        1070 Wien<br>
        Österreich</p>
        <p>E-Mail: datenschutz@flowforge.example</p>
      </div>

      <div class="legal-box">
        <h3>Welche Daten verarbeitet werden</h3>
        <p>Wenn diese Website als echter Webshop betrieben wird, können je nach Nutzung folgende personenbezogene Daten verarbeitet werden:</p>
        <ul class="feature-list">
          <li>Name und Vorname</li>
          <li>E-Mail-Adresse</li>
          <li>Adresse und Rechnungsdaten</li>
          <li>Bestelldaten, zum Beispiel ausgewähltes Paket und Zahlungsart</li>
          <li>Nachrichten aus dem Kontaktformular</li>
          <li>technische Daten wie IP-Adresse, Browser, Gerätetyp und Zeitpunkt des Aufrufs</li>
        </ul>
        <p>In dieser abgegebenen Demo-Version werden keine echten Bestellungen verarbeitet. Die Formulare zeigen nur eine lokale Bestätigung im Browser an.</p>
      </div>

      <div class="legal-box">
        <h3>Zwecke der Verarbeitung</h3>
        <p>Die Daten würden in einem echten Webshop verwendet werden, um Bestellungen abzuwickeln, Kundenanfragen zu beantworten, Rechnungen zu erstellen und den Zugang zur Software bereitzustellen. Außerdem könnten technische Daten benötigt werden, damit die Website sicher und fehlerfrei funktioniert.</p>
      </div>

      <div class="legal-box">
        <h3>Rechtsgrundlagen</h3>
        <p>Die Verarbeitung erfolgt, soweit sie für den Kauf oder die Nutzung der Software notwendig ist, zur Vertragserfüllung bzw. für vorvertragliche Maßnahmen. Wenn gesetzliche Aufbewahrungspflichten bestehen, werden Daten aufgrund einer rechtlichen Verpflichtung gespeichert. Bei freiwilligen Anfragen über das Kontaktformular erfolgt die Verarbeitung, weil ein berechtigtes Interesse daran besteht, die Anfrage zu beantworten.</p>
        <p>Falls später ein Newsletter oder Tracking-Tool eingebaut wird, müsste dafür vorher eine passende Einwilligung eingeholt werden.</p>
      </div>

      <div class="legal-box">
        <h3>Kontaktformular</h3>
        <p>Wenn jemand das Kontaktformular nutzt, würden Name, E-Mail-Adresse und Nachricht verarbeitet werden, damit die Anfrage beantwortet werden kann. In dieser statischen Version wird die Nachricht aber nicht wirklich versendet und auch nicht auf einem Server gespeichert.</p>
      </div>

      <div class="legal-box">
        <h3>Cookies und Analyse</h3>
        <p>Diese Demo-Website setzt keine echten Tracking-Cookies und verwendet kein echtes Analyse-Tool. Wenn in einer echten Version Analyse-Tools verwendet werden, müssten Besucherinnen und Besucher klar informiert werden. Falls notwendig, müsste vorher eine Einwilligung über ein Cookie-Banner eingeholt werden.</p>
      </div>

      <div class="legal-box">
        <h3>Zahlungsdaten</h3>
        <p>Der Checkout ist nur ein Mock-up. Es werden keine echten Zahlungsdaten verarbeitet. In einem echten Webshop würden Zahlungsdaten nur soweit verarbeitet werden, wie es für die Zahlung und die Abrechnung notwendig ist. Meist würde dafür ein externer Zahlungsanbieter eingesetzt werden.</p>
      </div>

      <div class="legal-box">
        <h3>Weitergabe von Daten</h3>
        <p>Daten würden nur weitergegeben werden, wenn das für den Betrieb des Webshops notwendig ist, zum Beispiel an Hosting-Anbieter, Zahlungsanbieter oder Steuerberatung. In dieser Demo findet keine solche Weitergabe statt.</p>
      </div>

      <div class="legal-box">
        <h3>Speicherdauer</h3>
        <p>Daten werden nur so lange gespeichert, wie sie für den jeweiligen Zweck notwendig sind. Rechnungs- und Buchhaltungsdaten müssten in einem echten Betrieb entsprechend den gesetzlichen Aufbewahrungspflichten gespeichert werden. Kontaktanfragen würden gelöscht werden, sobald sie erledigt sind und keine weitere Aufbewahrung notwendig ist.</p>
      </div>

      <div class="legal-box">
        <h3>Keine automatisierte Entscheidung</h3>
        <p>Es findet keine automatisierte Entscheidungsfindung und kein Profiling statt, das rechtliche Auswirkungen auf Besucherinnen oder Besucher hätte.</p>
      </div>

      <div class="legal-box">
        <h3>Rechte der betroffenen Personen</h3>
        <p>Betroffene Personen haben nach der DSGVO insbesondere das Recht auf Auskunft, Berichtigung, Löschung, Einschränkung der Verarbeitung, Datenübertragbarkeit und Widerspruch. Wenn eine Verarbeitung auf Einwilligung beruht, kann diese Einwilligung jederzeit widerrufen werden.</p>
        <p>Für Anfragen dazu kann man sich an Lukas Haindl unter datenschutz@flowforge.example wenden.</p>
      </div>

      <div class="legal-box">
        <h3>Beschwerderecht</h3>
        <p>Wenn jemand der Meinung ist, dass die Verarbeitung personenbezogener Daten gegen Datenschutzrecht verstößt, kann eine Beschwerde bei der österreichischen Datenschutzbehörde eingebracht werden:</p>
        <p>Österreichische Datenschutzbehörde<br>
        Barichgasse 40-42<br>
        1030 Wien<br>
        E-Mail: dsb@dsb.gv.at<br>
        Website: www.dsb.gv.at</p>
      </div>

      <div class="legal-box">
        <h3>Stand</h3>
        <p>Diese Datenschutzerklärung wurde für eine schulische Webshop-Demo erstellt. Stand: Mai 2026.</p>
      </div>
    </section>

<section id="impressum">
  <div class="section-head">
    <h2>Impressum</h2>
  </div>
  <div class="legal-box">
    <h3>Medieninhaber und Betreiber der Website</h3>
    <p>
      FlowForge Studio<br>
      Inhaber: Lukas Haindl<br>
      Mariahilfer Straße 88a<br>
      1070 Wien<br>
      Österreich
    </p>

    <h3>Kontakt</h3>
    <p>
      E-Mail: office@flowforge.example<br>
      Telefon: +43 1 234 56 78
    </p>

    <h3>Unternehmensgegenstand</h3>
    <p>
      Entwicklung und Vertrieb von Softwarelösungen, insbesondere Workflow-Software für kleine Unternehmen und Start-ups.
    </p>

    <h3>Blattlinie</h3>
    <p>
      Diese Website informiert über das fiktive Softwareprodukt FlowForge Studio, Preise, Lizenzbedingungen, Kontaktmöglichkeiten und rechtliche Hinweise.
    </p>

    <h3>Hinweis</h3>
    <p>
      Diese Website wurde im Rahmen einer schulischen Übung erstellt. Es handelt sich um keinen echten Webshop.
    </p>
  </div>
</section>
  </main>

  <div class="cart" aria-live="polite">
    <div class="cart-inner">
      <strong id="cartText">Warenkorb: leer</strong>
      <a class="btn btn-primary" href="#checkout">Zum Checkout</a>
    </div>
  </div>

  <footer>
    <section>
      <div class="footer-grid">
        <div>
          <h2>FlowForge</h2>
          <p>Moderner Software-Webshop für Workflow-Automatisierung. Diese Website ist eine statische Demo ohne echte Zahlungs- oder Datenverarbeitung.</p>
        </div>
        <div>
          <h3>Shop</h3>
          <p><a href="#features">Funktionen</a><br><a href="#shop">Preise</a><br><a href="#about">Über uns</a><br><a href="#kontakt">Kontakt</a></p>
        </div>
        <div>
          <h3>Rechtliches</h3>
          <p><a href="#lizenz">Lizenz</a><br><a href="#rechte">Medien & Rechte</a><br><a href="#barrierefreiheit">Barrierefreiheit</a><br><a href="#datenschutz">Datenschutz</a><br><a href="#impressum">Impressum</a></p>
        </div>
      </div>
    </section>
  </footer>

  <script>
    const cartText = document.getElementById('cartText');
    let selectedPlan = null;

    document.querySelectorAll('[data-plan]').forEach(button => {
      button.addEventListener('click', () => {
        selectedPlan = { plan: button.dataset.plan, price: button.dataset.price };
        cartText.textContent = `Warenkorb: ${selectedPlan.plan} – ${selectedPlan.price} € / Monat`;
      });
    });

    function fakeOrder() {
      const status = document.getElementById('orderStatus');
      const plan = selectedPlan ? selectedPlan.plan : 'kein Paket ausgewählt';
      status.hidden = false;
      status.textContent = `Danke! Deine Demo-Bestellung wurde simuliert. Ausgewähltes Paket: ${plan}. Es wurden keine Daten übertragen.`;
    }

    function contactSent() {
      const status = document.getElementById('contactStatus');
      status.hidden = false;
      status.textContent = 'Danke! Die Nachricht wurde in dieser Demo nur lokal angezeigt und nicht versendet.';
    }

    function playSonicLogo() {
      const AudioContext = window.AudioContext || window.webkitAudioContext;
      if (!AudioContext) return;
      const ctx = new AudioContext();
      [440, 554, 659].forEach((frequency, index) => {
        const oscillator = ctx.createOscillator();
        const gain = ctx.createGain();
        oscillator.type = 'sine';
        oscillator.frequency.value = frequency;
        gain.gain.setValueAtTime(0.0001, ctx.currentTime + index * 0.18);
        gain.gain.exponentialRampToValueAtTime(0.12, ctx.currentTime + index * 0.18 + 0.03);
        gain.gain.exponentialRampToValueAtTime(0.0001, ctx.currentTime + index * 0.18 + 0.16);
        oscillator.connect(gain).connect(ctx.destination);
        oscillator.start(ctx.currentTime + index * 0.18);
        oscillator.stop(ctx.currentTime + index * 0.18 + 0.18);
      });
    }
  </script>
</body>
</html>
