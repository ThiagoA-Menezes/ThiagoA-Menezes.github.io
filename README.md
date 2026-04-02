<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Thiago Menezes · Data Intelligence</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=JetBrains+Mono:wght@300;400;500&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet" />
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --bg:       #080c14;
      --surface:  #0d1421;
      --border:   #1a2540;
      --ibm:      #0f62fe;
      --ibm-dim:  #0043ce;
      --gold:     #f1c21b;
      --text:     #e2e8f0;
      --muted:    #64748b;
      --mono:     'JetBrains Mono', monospace;
      --sans:     'DM Sans', sans-serif;
      --display:  'Syne', sans-serif;
    }

    html { scroll-behavior: smooth; }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: var(--sans);
      font-size: 16px;
      line-height: 1.6;
      overflow-x: hidden;
    }

    /* ── NOISE OVERLAY ── */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.03'/%3E%3C/svg%3E");
      pointer-events: none;
      z-index: 0;
      opacity: .4;
    }

    /* ── GRID LINES ── */
    body::after {
      content: '';
      position: fixed;
      inset: 0;
      background-image:
        linear-gradient(rgba(15,98,254,.04) 1px, transparent 1px),
        linear-gradient(90deg, rgba(15,98,254,.04) 1px, transparent 1px);
      background-size: 48px 48px;
      pointer-events: none;
      z-index: 0;
    }

    /* ── NAV ── */
    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      z-index: 100;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 1.25rem 4rem;
      background: rgba(8,12,20,.85);
      backdrop-filter: blur(16px);
      border-bottom: 1px solid var(--border);
    }

    .nav-logo {
      font-family: var(--mono);
      font-size: .85rem;
      color: var(--ibm);
      letter-spacing: .08em;
    }

    .nav-links {
      display: flex;
      gap: 2.5rem;
      list-style: none;
    }

    .nav-links a {
      font-family: var(--mono);
      font-size: .78rem;
      color: var(--muted);
      text-decoration: none;
      letter-spacing: .1em;
      text-transform: uppercase;
      transition: color .2s;
    }

    .nav-links a:hover { color: var(--text); }

    /* ── HERO ── */
    #hero {
      position: relative;
      z-index: 1;
      min-height: 100vh;
      display: grid;
      place-items: center;
      padding: 8rem 4rem 4rem;
      overflow: hidden;
    }

    .hero-glow {
      position: absolute;
      width: 700px;
      height: 700px;
      border-radius: 50%;
      background: radial-gradient(circle, rgba(15,98,254,.12) 0%, transparent 70%);
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      pointer-events: none;
      animation: pulse-glow 6s ease-in-out infinite alternate;
    }

    @keyframes pulse-glow {
      from { opacity: .6; transform: translate(-50%,-50%) scale(1); }
      to   { opacity: 1;  transform: translate(-50%,-50%) scale(1.15); }
    }

    .hero-content {
      text-align: center;
      max-width: 800px;
      animation: fadeUp .9s ease both;
    }

    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(32px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    .hero-tag {
      font-family: var(--mono);
      font-size: .78rem;
      color: var(--ibm);
      letter-spacing: .15em;
      text-transform: uppercase;
      margin-bottom: 1.5rem;
      display: inline-flex;
      align-items: center;
      gap: .6rem;
    }

    .hero-tag::before {
      content: '';
      display: inline-block;
      width: 24px; height: 1px;
      background: var(--ibm);
    }

    h1 {
      font-family: var(--display);
      font-weight: 800;
      font-size: clamp(3rem, 8vw, 5.5rem);
      line-height: 1.0;
      letter-spacing: -.03em;
      margin-bottom: 1rem;
      background: linear-gradient(135deg, #e2e8f0 0%, #a0b0c8 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    .hero-sub {
      font-family: var(--sans);
      font-weight: 300;
      font-size: 1.1rem;
      color: var(--muted);
      max-width: 560px;
      margin: 0 auto 2.5rem;
      line-height: 1.75;
    }

    .hero-cta {
      display: flex;
      gap: 1rem;
      justify-content: center;
      flex-wrap: wrap;
    }

    .btn {
      display: inline-flex;
      align-items: center;
      gap: .5rem;
      padding: .75rem 1.75rem;
      border-radius: 4px;
      font-family: var(--mono);
      font-size: .82rem;
      letter-spacing: .08em;
      text-decoration: none;
      transition: all .2s;
      cursor: pointer;
    }

    .btn-primary {
      background: var(--ibm);
      color: #fff;
      border: 1px solid var(--ibm);
    }

    .btn-primary:hover { background: var(--ibm-dim); border-color: var(--ibm-dim); transform: translateY(-2px); }

    .btn-ghost {
      background: transparent;
      color: var(--text);
      border: 1px solid var(--border);
    }

    .btn-ghost:hover { border-color: var(--muted); transform: translateY(-2px); }

    /* ── SECTION SHELL ── */
    section {
      position: relative;
      z-index: 1;
      padding: 6rem 4rem;
      max-width: 1100px;
      margin: 0 auto;
    }

    .section-label {
      font-family: var(--mono);
      font-size: .72rem;
      color: var(--ibm);
      letter-spacing: .2em;
      text-transform: uppercase;
      margin-bottom: .75rem;
    }

    h2 {
      font-family: var(--display);
      font-weight: 700;
      font-size: clamp(1.8rem, 4vw, 2.6rem);
      letter-spacing: -.02em;
      margin-bottom: 1rem;
    }

    .section-divider {
      width: 48px;
      height: 2px;
      background: var(--ibm);
      margin-bottom: 3rem;
    }

    /* ── ABOUT ── */
    #about .about-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 4rem;
      align-items: start;
    }

    #about p {
      color: #94a3b8;
      line-height: 1.85;
      margin-bottom: 1rem;
      font-weight: 300;
    }

    #about p strong {
      color: var(--text);
      font-weight: 500;
    }

    .stat-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 1.25rem;
    }

    .stat-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 6px;
      padding: 1.25rem;
      transition: border-color .2s;
    }

    .stat-card:hover { border-color: var(--ibm); }

    .stat-num {
      font-family: var(--display);
      font-weight: 800;
      font-size: 2rem;
      color: var(--ibm);
      line-height: 1;
      margin-bottom: .25rem;
    }

    .stat-label {
      font-family: var(--mono);
      font-size: .72rem;
      color: var(--muted);
      letter-spacing: .08em;
      text-transform: uppercase;
    }

    /* ── EXPERTISE ── */
    #expertise .expertise-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
      gap: 1.25rem;
    }

    .expertise-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 6px;
      padding: 1.75rem;
      transition: border-color .2s, transform .2s;
      position: relative;
      overflow: hidden;
    }

    .expertise-card::before {
      content: '';
      position: absolute;
      top: 0; left: 0;
      width: 3px; height: 100%;
      background: var(--ibm);
      opacity: 0;
      transition: opacity .2s;
    }

    .expertise-card:hover { border-color: var(--ibm); transform: translateY(-3px); }
    .expertise-card:hover::before { opacity: 1; }

    .expertise-icon {
      font-size: 1.5rem;
      margin-bottom: 1rem;
    }

    .expertise-card h3 {
      font-family: var(--display);
      font-weight: 600;
      font-size: 1rem;
      margin-bottom: .75rem;
      color: var(--text);
    }

    .tag-list {
      display: flex;
      flex-wrap: wrap;
      gap: .4rem;
    }

    .tag {
      font-family: var(--mono);
      font-size: .68rem;
      padding: .25rem .6rem;
      border-radius: 3px;
      background: rgba(15,98,254,.1);
      color: #93c5fd;
      border: 1px solid rgba(15,98,254,.2);
      letter-spacing: .05em;
    }

    .tag.gold {
      background: rgba(241,194,27,.08);
      color: #fbbf24;
      border-color: rgba(241,194,27,.2);
    }

    /* ── PROJECTS ── */
    #projects .projects-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
      gap: 1.25rem;
    }

    .project-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 6px;
      padding: 1.75rem;
      text-decoration: none;
      color: inherit;
      display: flex;
      flex-direction: column;
      gap: .75rem;
      transition: border-color .2s, transform .2s;
      position: relative;
    }

    .project-card:hover { border-color: var(--ibm); transform: translateY(-3px); }

    .project-card-top {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
    }

    .project-icon {
      font-size: 1.25rem;
    }

    .project-arrow {
      font-size: .9rem;
      color: var(--muted);
      transition: color .2s, transform .2s;
    }

    .project-card:hover .project-arrow { color: var(--ibm); transform: translate(3px, -3px); }

    .project-card h3 {
      font-family: var(--display);
      font-weight: 600;
      font-size: .95rem;
      color: var(--text);
    }

    .project-desc {
      font-size: .875rem;
      color: var(--muted);
      line-height: 1.65;
      flex: 1;
    }

    .project-lang {
      font-family: var(--mono);
      font-size: .7rem;
      color: var(--muted);
      display: flex;
      align-items: center;
      gap: .4rem;
    }

    .lang-dot {
      width: 8px; height: 8px;
      border-radius: 50%;
      background: #3572A5;
    }

    .lang-dot.js { background: #f1e05a; }
    .lang-dot.java { background: #b07219; }
    .lang-dot.html { background: #e34c26; }
    .lang-dot.nb { background: #DA5B0B; }

    /* ── TERMINAL CALLOUT ── */
    .terminal-block {
      background: #060a10;
      border: 1px solid var(--border);
      border-radius: 6px;
      padding: 1.5rem 2rem;
      font-family: var(--mono);
      font-size: .82rem;
      color: #64748b;
      margin-top: 3rem;
    }

    .terminal-block .prompt { color: var(--ibm); }
    .terminal-block .value  { color: #34d399; }
    .terminal-block .comment { color: #334155; }

    /* ── CONTACT ── */
    #contact {
      text-align: center;
    }

    #contact p {
      font-size: 1rem;
      color: var(--muted);
      max-width: 480px;
      margin: 0 auto 2.5rem;
      font-weight: 300;
    }

    .contact-links {
      display: flex;
      gap: 1rem;
      justify-content: center;
      flex-wrap: wrap;
    }

    /* ── FOOTER ── */
    footer {
      position: relative;
      z-index: 1;
      border-top: 1px solid var(--border);
      padding: 2rem 4rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-family: var(--mono);
      font-size: .72rem;
      color: var(--muted);
    }

    /* ── SCROLL ANIMATIONS ── */
    .reveal {
      opacity: 0;
      transform: translateY(24px);
      transition: opacity .7s ease, transform .7s ease;
    }

    .reveal.visible {
      opacity: 1;
      transform: translateY(0);
    }

    /* ── RESPONSIVE ── */
    @media (max-width: 768px) {
      nav { padding: 1rem 1.5rem; }
      .nav-links { display: none; }
      section { padding: 4rem 1.5rem; }
      #hero { padding: 6rem 1.5rem 3rem; }
      #about .about-grid { grid-template-columns: 1fr; gap: 2.5rem; }
      footer { flex-direction: column; gap: .75rem; text-align: center; }
    }
  </style>
</head>
<body>

  <!-- NAV -->
  <nav>
    <span class="nav-logo">TM / <span style="color:#64748b">data-intelligence</span></span>
    <ul class="nav-links">
      <li><a href="#about">About</a></li>
      <li><a href="#expertise">Expertise</a></li>
      <li><a href="#projects">Projects</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </nav>

  <!-- HERO -->
  <section id="hero">
    <div class="hero-glow"></div>
    <div class="hero-content">
      <div class="hero-tag">IBM · São Paulo, Brazil</div>
      <h1>Thiago<br/>Menezes</h1>
      <p class="hero-sub">
        Data Intelligence Specialist bridging advanced analytics, AI governance, and enterprise architecture. Turning data complexity into competitive advantage — at scale.
      </p>
      <div class="hero-cta">
        <a href="https://linkedin.com/in/thiagoamenezes" target="_blank" class="btn btn-primary">
          ↗ Connect on LinkedIn
        </a>
        <a href="https://github.com/ThiagoA-Menezes" target="_blank" class="btn btn-ghost">
          ⌥ View GitHub
        </a>
      </div>
    </div>
  </section>

  <!-- ABOUT -->
  <section id="about">
    <div class="reveal">
      <div class="section-label">// 01 · About</div>
      <h2>Who I am</h2>
      <div class="section-divider"></div>
      <div class="about-grid">
        <div>
          <p>
            I'm a <strong>Data Intelligence Specialist at IBM Brazil</strong>, focused on the watsonx portfolio — covering AI, data lakes, and AI governance for enterprise clients across the country.
          </p>
          <p>
            My work sits at the intersection of <strong>pre-sales engineering, competitive intelligence, and solution architecture</strong>. I translate technical complexity into business value at C-level engagements, and I build the tools and battle cards that help teams win.
          </p>
          <p>
            Beyond the IBM ecosystem, I build Python automations, data pipelines, and productivity tooling — because the best way to understand data engineering is to <strong>do data engineering</strong>.
          </p>
        </div>
        <div class="stat-grid">
          <div class="stat-card">
            <div class="stat-num">3+</div>
            <div class="stat-label">watsonx Products</div>
          </div>
          <div class="stat-card">
            <div class="stat-num">31</div>
            <div class="stat-label">GitHub Repos</div>
          </div>
          <div class="stat-card">
            <div class="stat-num">AWS</div>
            <div class="stat-label">+ Azure + GCP</div>
          </div>
          <div class="stat-card">
            <div class="stat-num">SP</div>
            <div class="stat-label">São Paulo, Brazil</div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- EXPERTISE -->
  <section id="expertise">
    <div class="reveal">
      <div class="section-label">// 02 · Expertise</div>
      <h2>What I do</h2>
      <div class="section-divider"></div>
      <div class="expertise-grid">

        <div class="expertise-card">
          <div class="expertise-icon">⚙️</div>
          <h3>Data Engineering & Integration</h3>
          <div class="tag-list">
            <span class="tag">ETL / ELT</span>
            <span class="tag">Apache Spark</span>
            <span class="tag">Apache Kafka</span>
            <span class="tag">Apache Airflow</span>
            <span class="tag">dbt</span>
            <span class="tag">CDC</span>
            <span class="tag">Data Pipelines</span>
          </div>
        </div>

        <div class="expertise-card">
          <div class="expertise-icon">🤖</div>
          <h3>IBM watsonx Portfolio</h3>
          <div class="tag-list">
            <span class="tag gold">watsonx.ai</span>
            <span class="tag gold">watsonx.data</span>
            <span class="tag gold">watsonx.governance</span>
            <span class="tag">Pre-Sales</span>
            <span class="tag">Solution Architecture</span>
          </div>
        </div>

        <div class="expertise-card">
          <div class="expertise-icon">☁️</div>
          <h3>Cloud Platforms</h3>
          <div class="tag-list">
            <span class="tag">AWS</span>
            <span class="tag">Azure</span>
            <span class="tag">Google Cloud</span>
            <span class="tag">Kubernetes</span>
            <span class="tag">OpenShift</span>
            <span class="tag">Rancher</span>
          </div>
        </div>

        <div class="expertise-card">
          <div class="expertise-icon">🐍</div>
          <h3>Python & Automation</h3>
          <div class="tag-list">
            <span class="tag">Python</span>
            <span class="tag">Pandas</span>
            <span class="tag">Selenium</span>
            <span class="tag">Scikit-learn</span>
            <span class="tag">Salesforce Automation</span>
            <span class="tag">Bash</span>
          </div>
        </div>

        <div class="expertise-card">
          <div class="expertise-icon">📊</div>
          <h3>Analytics & BI</h3>
          <div class="tag-list">
            <span class="tag">SQL</span>
            <span class="tag">Power BI</span>
            <span class="tag">Matplotlib</span>
            <span class="tag">NumPy</span>
            <span class="tag">Data Analysis</span>
            <span class="tag">ElasticSearch</span>
          </div>
        </div>

        <div class="expertise-card">
          <div class="expertise-icon">🎯</div>
          <h3>Sales & Strategy</h3>
          <div class="tag-list">
            <span class="tag">Competitive Intelligence</span>
            <span class="tag">Battle Cards</span>
            <span class="tag">C-Level Engagement</span>
            <span class="tag">Salesforce ISC</span>
            <span class="tag">RPA</span>
          </div>
        </div>

      </div>
    </div>
  </section>

  <!-- PROJECTS -->
  <section id="projects">
    <div class="reveal">
      <div class="section-label">// 03 · Projects</div>
      <h2>Featured work</h2>
      <div class="section-divider"></div>
      <div class="projects-grid">

        <a href="https://github.com/ThiagoA-Menezes/quick-openshift-kogito" target="_blank" class="project-card">
          <div class="project-card-top">
            <div class="project-icon">🚀</div>
            <div class="project-arrow">↗</div>
          </div>
          <h3>Quick OpenShift Kogito</h3>
          <p class="project-desc">
            Demonstração de deploy do Kogito em OpenShift — automação de decisões de negócio via regras e workflows na plataforma IBM.
          </p>
          <div class="tag-list" style="margin-bottom:.5rem">
            <span class="tag">OpenShift</span>
            <span class="tag">Kogito</span>
            <span class="tag">BPMN</span>
          </div>
          <div class="project-lang"><span class="lang-dot html"></span> HTML</div>
        </a>

        <a href="https://github.com/ThiagoA-Menezes/P4DS4D2" target="_blank" class="project-card">
          <div class="project-card-top">
            <div class="project-icon">📓</div>
            <div class="project-arrow">↗</div>
          </div>
          <h3>Python for Data Science</h3>
          <p class="project-desc">
            Notebooks de estudo e prática em Python para ciência de dados — análise exploratória, manipulação com Pandas e visualizações.
          </p>
          <div class="tag-list" style="margin-bottom:.5rem">
            <span class="tag">Python</span>
            <span class="tag">Pandas</span>
            <span class="tag">Jupyter</span>
          </div>
          <div class="project-lang"><span class="lang-dot nb"></span> Jupyter Notebook</div>
        </a>

        <a href="https://github.com/ThiagoA-Menezes/business-automation-cicd-showcase" target="_blank" class="project-card">
          <div class="project-card-top">
            <div class="project-icon">⚡</div>
            <div class="project-arrow">↗</div>
          </div>
          <h3>Business Automation CI/CD</h3>
          <p class="project-desc">
            Showcase de automação de negócio com pipeline CI/CD — integração de decisões, regras e processos com Red Hat toolchain.
          </p>
          <div class="tag-list" style="margin-bottom:.5rem">
            <span class="tag">CI/CD</span>
            <span class="tag">Jenkins</span>
            <span class="tag">Business Rules</span>
          </div>
          <div class="project-lang"><span class="lang-dot java"></span> Java</div>
        </a>

        <a href="https://github.com/ThiagoA-Menezes/amq-examples" target="_blank" class="project-card">
          <div class="project-card-top">
            <div class="project-icon">📨</div>
            <div class="project-arrow">↗</div>
          </div>
          <h3>AMQ Messaging Examples</h3>
          <p class="project-desc">
            Exemplos práticos com Red Hat AMQ — messaging assíncrono, brokers e integração de sistemas via eventos.
          </p>
          <div class="tag-list" style="margin-bottom:.5rem">
            <span class="tag">Messaging</span>
            <span class="tag">ActiveMQ</span>
            <span class="tag">Event-Driven</span>
          </div>
          <div class="project-lang"><span class="lang-dot html"></span> HTML</div>
        </a>

      </div>

      <!-- Terminal easter egg -->
      <div class="terminal-block">
        <div><span class="prompt">$</span> git log --oneline --graph <span class="comment"># always learning, always shipping</span></div>
        <div style="margin-top:.75rem">
          <div><span style="color:#1d4ed8">*</span> <span class="value">a3f91bc</span> <span style="color:#475569">feat: watsonx.data competitive positioning</span></div>
          <div><span style="color:#1d4ed8">*</span> <span class="value">7c22de1</span> <span style="color:#475569">feat: salesforce automation with python + selenium</span></div>
          <div><span style="color:#1d4ed8">*</span> <span class="value">9ba45f0</span> <span style="color:#475569">feat: battle card framework for C-level engagement</span></div>
          <div><span style="color:#1d4ed8">*</span> <span class="value">3e10aa2</span> <span style="color:#475569">feat: data engineering design patterns study</span></div>
          <div><span style="color:#475569">…</span></div>
        </div>
      </div>

    </div>
  </section>

  <!-- CONTACT -->
  <section id="contact">
    <div class="reveal">
      <div class="section-label">// 04 · Contact</div>
      <h2>Let's connect</h2>
      <div class="section-divider" style="margin: 0 auto 2rem;"></div>
      <p>
        Whether you want to talk data architecture, IBM watsonx, a technical challenge, or just exchange ideas — I'm always open to a good conversation.
      </p>
      <div class="contact-links">
        <a href="https://linkedin.com/in/thiagoamenezes" target="_blank" class="btn btn-primary">
          ↗ LinkedIn
        </a>
        <a href="https://github.com/ThiagoA-Menezes" target="_blank" class="btn btn-ghost">
          ⌥ GitHub
        </a>
      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <footer>
    <span>© 2025 Thiago Menezes · São Paulo, Brazil</span>
    <span style="color:#1a2540">built with intent, not templates</span>
  </footer>

  <script>
    // Intersection Observer for scroll reveals
    const observer = new IntersectionObserver(
      entries => entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible'); }),
      { threshold: 0.1 }
    );
    document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
  </script>

</body>
</html>
