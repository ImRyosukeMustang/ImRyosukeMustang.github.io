<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>The Golden Shear — Premium Saloon</title>
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=Barlow:wght@300;400;500&display=swap" rel="stylesheet" />
  <style>
    *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

    :root {
      --gold: #c9a84c;
      --gold-light: #e8c96a;
      --dark: #0e0b08;
      --dark2: #1a1510;
      --dark3: #241d14;
      --cream: #f5ead8;
      --muted: #8a7a63;
    }

    html { scroll-behavior: smooth; }

    body {
      background: var(--dark);
      color: var(--cream);
      font-family: 'Barlow', sans-serif;
      font-weight: 300;
      overflow-x: hidden;
    }

    /* ── NOISE TEXTURE OVERLAY ── */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
      pointer-events: none;
      z-index: 999;
      opacity: 0.5;
    }

    /* ── NAV ── */
    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      z-index: 100;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 1.4rem 5vw;
      background: linear-gradient(to bottom, rgba(14,11,8,0.95), transparent);
    }

    .nav-logo {
      font-family: 'Playfair Display', serif;
      font-size: 1.3rem;
      color: var(--gold);
      letter-spacing: 0.05em;
      text-decoration: none;
    }

    .nav-links {
      display: flex;
      gap: 2.5rem;
      list-style: none;
    }

    .nav-links a {
      color: var(--cream);
      text-decoration: none;
      font-size: 0.82rem;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      opacity: 0.75;
      transition: opacity 0.2s, color 0.2s;
    }

    .nav-links a:hover { opacity: 1; color: var(--gold); }

    .nav-cta {
      background: transparent;
      border: 1px solid var(--gold);
      color: var(--gold) !important;
      padding: 0.5rem 1.2rem !important;
      opacity: 1 !important;
      transition: background 0.2s !important;
    }

    .nav-cta:hover { background: var(--gold) !important; color: var(--dark) !important; }

    /* ── HERO ── */
    #hero {
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
      position: relative;
      padding: 8rem 2rem 4rem;
      background:
        radial-gradient(ellipse 80% 60% at 50% 40%, rgba(201,168,76,0.08) 0%, transparent 70%),
        linear-gradient(180deg, #0e0b08 0%, #1a1510 100%);
    }

    .hero-tag {
      font-size: 0.72rem;
      letter-spacing: 0.25em;
      text-transform: uppercase;
      color: var(--gold);
      margin-bottom: 1.5rem;
      opacity: 0;
      animation: fadeUp 0.8s 0.2s forwards;
    }

    .hero-title {
      font-family: 'Playfair Display', serif;
      font-size: clamp(3rem, 8vw, 7rem);
      line-height: 1.05;
      color: var(--cream);
      opacity: 0;
      animation: fadeUp 0.9s 0.4s forwards;
    }

    .hero-title em {
      font-style: italic;
      color: var(--gold);
    }

    .hero-sub {
      margin-top: 1.5rem;
      max-width: 480px;
      font-size: 1rem;
      line-height: 1.7;
      color: var(--muted);
      opacity: 0;
      animation: fadeUp 0.9s 0.6s forwards;
    }

    .hero-btns {
      margin-top: 2.5rem;
      display: flex;
      gap: 1rem;
      flex-wrap: wrap;
      justify-content: center;
      opacity: 0;
      animation: fadeUp 0.9s 0.8s forwards;
    }

    .btn-primary {
      background: var(--gold);
      color: var(--dark);
      border: none;
      padding: 0.85rem 2.2rem;
      font-family: 'Barlow', sans-serif;
      font-size: 0.82rem;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      cursor: pointer;
      transition: background 0.2s, transform 0.15s;
      text-decoration: none;
    }

    .btn-primary:hover { background: var(--gold-light); transform: translateY(-2px); }

    .btn-outline {
      background: transparent;
      color: var(--cream);
      border: 1px solid rgba(245,234,216,0.3);
      padding: 0.85rem 2.2rem;
      font-family: 'Barlow', sans-serif;
      font-size: 0.82rem;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      cursor: pointer;
      transition: border-color 0.2s, color 0.2s;
      text-decoration: none;
    }

    .btn-outline:hover { border-color: var(--gold); color: var(--gold); }

    .hero-divider {
      position: absolute;
      bottom: 2.5rem;
      left: 50%;
      transform: translateX(-50%);
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 0.5rem;
      opacity: 0;
      animation: fadeIn 1s 1.5s forwards;
    }

    .hero-divider span {
      font-size: 0.65rem;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      color: var(--muted);
    }

    .scroll-line {
      width: 1px;
      height: 40px;
      background: linear-gradient(to bottom, var(--gold), transparent);
      animation: scrollPulse 2s infinite;
    }

    /* ── SECTION SHARED ── */
    section { padding: 6rem 5vw; }

    .section-label {
      font-size: 0.7rem;
      letter-spacing: 0.25em;
      text-transform: uppercase;
      color: var(--gold);
      margin-bottom: 1rem;
    }

    .section-title {
      font-family: 'Playfair Display', serif;
      font-size: clamp(2rem, 4vw, 3.2rem);
      line-height: 1.15;
      max-width: 600px;
    }

    .section-title em { font-style: italic; color: var(--gold); }

    /* ── ABOUT ── */
    #about {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 4rem;
      align-items: center;
      background: var(--dark2);
    }

    .about-image-wrap {
      position: relative;
    }

    .about-img-placeholder {
      width: 100%;
      aspect-ratio: 4/5;
      background: var(--dark3);
      border: 1px solid rgba(201,168,76,0.2);
      display: flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      gap: 1rem;
      color: var(--muted);
      font-size: 0.8rem;
      letter-spacing: 0.1em;
    }

    .about-img-placeholder svg { opacity: 0.3; }

    .gold-corner {
      position: absolute;
      top: -12px; left: -12px;
      width: 60px; height: 60px;
      border-top: 2px solid var(--gold);
      border-left: 2px solid var(--gold);
    }

    .about-text p {
      color: var(--muted);
      line-height: 1.8;
      margin-top: 1.5rem;
      font-size: 0.97rem;
    }

    .about-stats {
      display: flex;
      gap: 3rem;
      margin-top: 2.5rem;
    }

    .stat-num {
      font-family: 'Playfair Display', serif;
      font-size: 2.5rem;
      color: var(--gold);
      line-height: 1;
    }

    .stat-label {
      font-size: 0.75rem;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      color: var(--muted);
      margin-top: 0.3rem;
    }

    /* ── SERVICES ── */
    #services {
      background: var(--dark);
      text-align: center;
    }

    #services .section-title { margin: 0 auto 3rem; }

    .services-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 1.5rem;
      margin-top: 3rem;
    }

    .service-card {
      background: var(--dark2);
      border: 1px solid rgba(201,168,76,0.12);
      padding: 2.5rem 2rem;
      transition: border-color 0.3s, transform 0.2s;
      position: relative;
      overflow: hidden;
    }

    .service-card::before {
      content: '';
      position: absolute;
      bottom: 0; left: 0; right: 0;
      height: 2px;
      background: var(--gold);
      transform: scaleX(0);
      transition: transform 0.3s;
    }

    .service-card:hover { border-color: rgba(201,168,76,0.4); transform: translateY(-4px); }
    .service-card:hover::before { transform: scaleX(1); }

    .service-icon {
      font-size: 2rem;
      margin-bottom: 1rem;
    }

    .service-name {
      font-family: 'Playfair Display', serif;
      font-size: 1.2rem;
      margin-bottom: 0.5rem;
    }

    .service-desc {
      font-size: 0.85rem;
      color: var(--muted);
      line-height: 1.7;
    }

    .service-price {
      font-family: 'Playfair Display', serif;
      color: var(--gold);
      font-size: 1.1rem;
      margin-top: 1rem;
    }

    /* ── GALLERY ── */
    #gallery {
      background: var(--dark2);
    }

    .gallery-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      grid-template-rows: auto auto;
      gap: 1rem;
      margin-top: 3rem;
    }

    .gallery-item {
      background: var(--dark3);
      border: 1px solid rgba(201,168,76,0.1);
      aspect-ratio: 1;
      display: flex;
      align-items: center;
      justify-content: center;
      color: var(--muted);
      font-size: 0.75rem;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      transition: border-color 0.3s;
      cursor: pointer;
    }

    .gallery-item:hover { border-color: rgba(201,168,76,0.4); }
    .gallery-item.tall { grid-row: span 2; aspect-ratio: auto; min-height: 300px; }

    /* ── BOOKING ── */
    #booking {
      background: var(--dark);
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 5rem;
      align-items: start;
    }

    .booking-form {
      display: flex;
      flex-direction: column;
      gap: 1.2rem;
      margin-top: 2rem;
    }

    .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 1rem; }

    .form-group {
      display: flex;
      flex-direction: column;
      gap: 0.4rem;
    }

    label {
      font-size: 0.72rem;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      color: var(--muted);
    }

    input, select, textarea {
      background: var(--dark2);
      border: 1px solid rgba(201,168,76,0.2);
      color: var(--cream);
      padding: 0.85rem 1rem;
      font-family: 'Barlow', sans-serif;
      font-size: 0.9rem;
      outline: none;
      transition: border-color 0.2s;
      width: 100%;
    }

    input:focus, select:focus, textarea:focus { border-color: var(--gold); }
    select option { background: var(--dark2); }
    textarea { resize: vertical; min-height: 100px; }

    /* ── HOURS ── */
    .hours-block {
      margin-top: 2rem;
      display: flex;
      flex-direction: column;
      gap: 0.8rem;
    }

    .hours-row {
      display: flex;
      justify-content: space-between;
      font-size: 0.9rem;
      padding-bottom: 0.8rem;
      border-bottom: 1px solid rgba(201,168,76,0.1);
      color: var(--muted);
    }

    .hours-row .day { color: var(--cream); }
    .hours-row .closed { color: rgba(138,122,99,0.5); font-style: italic; }

    /* ── CONTACT STRIP ── */
    #contact {
      background: var(--dark3);
      padding: 4rem 5vw;
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 2rem;
      flex-wrap: wrap;
      border-top: 1px solid rgba(201,168,76,0.15);
    }

    .contact-item {
      display: flex;
      flex-direction: column;
      gap: 0.3rem;
    }

    .contact-label {
      font-size: 0.68rem;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      color: var(--gold);
    }

    .contact-value {
      font-size: 1rem;
      color: var(--cream);
    }

    /* ── FOOTER ── */
    footer {
      background: var(--dark);
      padding: 2rem 5vw;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-top: 1px solid rgba(201,168,76,0.1);
      font-size: 0.78rem;
      color: var(--muted);
      flex-wrap: wrap;
      gap: 1rem;
    }

    .footer-logo {
      font-family: 'Playfair Display', serif;
      font-size: 1rem;
      color: var(--gold);
    }

    .social-links { display: flex; gap: 1.2rem; }
    .social-links a { color: var(--muted); text-decoration: none; transition: color 0.2s; font-size: 0.78rem; letter-spacing: 0.1em; }
    .social-links a:hover { color: var(--gold); }

    /* ── ANIMATIONS ── */
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(24px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    @keyframes fadeIn {
      from { opacity: 0; }
      to   { opacity: 1; }
    }

    @keyframes scrollPulse {
      0%, 100% { opacity: 1; }
      50%       { opacity: 0.3; }
    }

    /* ── RESPONSIVE ── */
    @media (max-width: 768px) {
      #about, #booking { grid-template-columns: 1fr; gap: 2rem; }
      .gallery-grid { grid-template-columns: repeat(2, 1fr); }
      .gallery-item.tall { grid-row: span 1; aspect-ratio: 1; }
      .form-row { grid-template-columns: 1fr; }
      .nav-links { display: none; }
      .about-stats { gap: 1.5rem; }
    }
  </style>
</head>
<body>

  <!-- NAV -->
  <nav>
    <a href="#hero" class="nav-logo">The Golden Shear</a>
    <ul class="nav-links">
      <li><a href="#about">About</a></li>
      <li><a href="#services">Services</a></li>
      <li><a href="#gallery">Gallery</a></li>
      <li><a href="#booking" class="nav-cta">Book Now</a></li>
    </ul>
  </nav>

  <!-- HERO -->
  <section id="hero">
    <p class="hero-tag">Est. 2010 · Premium Grooming</p>
    <h1 class="hero-title">Where Style<br>Meets <em>Craft</em></h1>
    <p class="hero-sub">A refined experience for the modern gentleman. Expert cuts, classic shaves, and timeless grooming — all under one roof.</p>
    <div class="hero-btns">
      <a href="#booking" class="btn-primary">Book Appointment</a>
      <a href="#services" class="btn-outline">View Services</a>
    </div>
    <div class="hero-divider">
      <span>Scroll</span>
      <div class="scroll-line"></div>
    </div>
  </section>

  <!-- ABOUT -->
  <section id="about">
    <div class="about-image-wrap">
      <div class="gold-corner"></div>
      <div class="about-img-placeholder">
        <!-- Replace with: <img src="your-image.jpg" alt="Saloon Interior" style="width:100%;height:100%;object-fit:cover;"> -->
        <svg width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1">
          <rect x="3" y="3" width="18" height="18" rx="2"/><circle cx="8.5" cy="8.5" r="1.5"/><path d="m21 15-5-5L5 21"/>
        </svg>
        <span>Add your photo here</span>
      </div>
    </div>
    <div class="about-text">
      <p class="section-label">Our Story</p>
      <h2 class="section-title">More Than a Cut —<br><em>An Experience</em></h2>
      <p>Founded in the heart of the city, The Golden Shear has been the destination for those who appreciate the art of grooming. Our master barbers bring decades of experience and passion to every chair.</p>
      <p>We blend old-school barbering traditions with modern techniques to give you a look that's uniquely yours — every single visit.</p>
      <div class="about-stats">
        <div>
          <div class="stat-num">14+</div>
          <div class="stat-label">Years Open</div>
        </div>
        <div>
          <div class="stat-num">8</div>
          <div class="stat-label">Expert Barbers</div>
        </div>
        <div>
          <div class="stat-num">5★</div>
          <div class="stat-label">Avg. Rating</div>
        </div>
      </div>
    </div>
  </section>

  <!-- SERVICES -->
  <section id="services">
    <p class="section-label">What We Offer</p>
    <h2 class="section-title">Our <em>Services</em></h2>
    <div class="services-grid">
      <div class="service-card">
        <div class="service-icon">✂️</div>
        <div class="service-name">Classic Haircut</div>
        <div class="service-desc">Precision cut tailored to your face shape and personal style. Includes wash and blow-dry.</div>
        <div class="service-price">From €25</div>
      </div>
      <div class="service-card">
        <div class="service-icon">🪒</div>
        <div class="service-name">Hot Towel Shave</div>
        <div class="service-desc">The full traditional straight-razor shave with hot towel, pre-shave oil, and aftercare.</div>
        <div class="service-price">From €30</div>
      </div>
      <div class="service-card">
        <div class="service-icon">💈</div>
        <div class="service-name">Cut & Shave Combo</div>
        <div class="service-desc">The complete package — haircut plus a hot towel shave for the full gentleman experience.</div>
        <div class="service-price">From €50</div>
      </div>
      <div class="service-card">
        <div class="service-icon">🧔</div>
        <div class="service-name">Beard Trim & Shape</div>
        <div class="service-desc">Expert beard sculpting, shaping, and conditioning. Leave looking sharp.</div>
        <div class="service-price">From €18</div>
      </div>
      <div class="service-card">
        <div class="service-icon">💆</div>
        <div class="service-name">Scalp Treatment</div>
        <div class="service-desc">Deep conditioning scalp massage and treatment for healthy, strong hair growth.</div>
        <div class="service-price">From €35</div>
      </div>
      <div class="service-card">
        <div class="service-icon">👦</div>
        <div class="service-name">Kids Cut</div>
        <div class="service-desc">Gentle, patient cuts for children under 12. A fun, stress-free experience for the whole family.</div>
        <div class="service-price">From €15</div>
      </div>
    </div>
  </section>

  <!-- GALLERY -->
  <section id="gallery">
    <p class="section-label">Portfolio</p>
    <h2 class="section-title">Our <em>Work</em></h2>
    <div class="gallery-grid">
      <!-- Replace divs with <img> tags, e.g.: <img src="cut1.jpg" alt="Haircut 1"> -->
      <div class="gallery-item tall">Photo 1</div>
      <div class="gallery-item">Photo 2</div>
      <div class="gallery-item">Photo 3</div>
      <div class="gallery-item">Photo 4</div>
      <div class="gallery-item">Photo 5</div>
    </div>
  </section>

  <!-- BOOKING -->
  <section id="booking">
    <div>
      <p class="section-label">Reserve Your Spot</p>
      <h2 class="section-title">Book an<br><em>Appointment</em></h2>
      <div class="hours-block">
        <div class="hours-row"><span class="day">Monday</span><span class="closed">Closed</span></div>
        <div class="hours-row"><span class="day">Tue – Fri</span><span>9:00 – 19:00</span></div>
        <div class="hours-row"><span class="day">Saturday</span><span>9:00 – 18:00</span></div>
        <div class="hours-row"><span class="day">Sunday</span><span>10:00 – 15:00</span></div>
      </div>
    </div>
    <div class="booking-form">
      <div class="form-row">
        <div class="form-group">
          <label>First Name</label>
          <input type="text" placeholder="John" />
        </div>
        <div class="form-group">
          <label>Last Name</label>
          <input type="text" placeholder="Doe" />
        </div>
      </div>
      <div class="form-group">
        <label>Phone / Email</label>
        <input type="text" placeholder="+49 123 456 789" />
      </div>
      <div class="form-row">
        <div class="form-group">
          <label>Service</label>
          <select>
            <option>Classic Haircut</option>
            <option>Hot Towel Shave</option>
            <option>Cut & Shave Combo</option>
            <option>Beard Trim & Shape</option>
            <option>Scalp Treatment</option>
            <option>Kids Cut</option>
          </select>
        </div>
        <div class="form-group">
          <label>Preferred Date</label>
          <input type="date" />
        </div>
      </div>
      <div class="form-group">
        <label>Notes (optional)</label>
        <textarea placeholder="Any specific requests or preferences..."></textarea>
      </div>
      <button class="btn-primary" style="margin-top:0.5rem; font-size:0.82rem;">Confirm Booking</button>
    </div>
  </section>

  <!-- CONTACT STRIP -->
  <div id="contact">
    <div class="contact-item">
      <span class="contact-label">Address</span>
      <span class="contact-value">123 Main Street, Frankfurt, Germany</span>
    </div>
    <div class="contact-item">
      <span class="contact-label">Phone</span>
      <span class="contact-value">+49 69 123 456</span>
    </div>
    <div class="contact-item">
      <span class="contact-label">Email</span>
      <span class="contact-value">hello@goldenshear.de</span>
    </div>
    <a href="#booking" class="btn-primary">Book Now</a>
  </div>

  <!-- FOOTER -->
  <footer>
    <span class="footer-logo">The Golden Shear</span>
    <span>© 2026 · All rights reserved</span>
    <div class="social-links">
      <a href="#">Instagram</a>
      <a href="#">Facebook</a>
      <a href="#">WhatsApp</a>
    </div>
  </footer>

</body>
</html>
<button id="lang-toggle" class="btn-outline" style="padding: 0.5rem 1.2rem; font-size: 0.75rem;">
  🇩🇪 Deutsch
</button>
<div class="nav-links">
  <a href="#about">About</a>
  <a href="#services">Services</a>
  <a href="#gallery">Gallery</a>
  <a href="#booking">Booking</a>
  <button id="lang-toggle" class="btn-outline" style="padding: 0.5rem 1.2rem; font-size: 0.75rem;">
    🇩🇪 Deutsch
  </button>
</div>
<script>
  (function() {
    let currentLang = 'en';

    const translations = {
      en: {
        // Navigation
        navAbout: 'About',
        navServices: 'Services',
        navGallery: 'Gallery',
        navBooking: 'Booking',
        // Hero
        heroTag: 'Est. 2025',
        heroTitle: 'The Gilded Blade',
        heroSub: 'Traditional craftsmanship meets modern precision. Experience the finest grooming in an atmosphere of understated luxury.',
        heroBtn1: 'Book Appointment',
        heroBtn2: 'Explore Services',
        heroScroll: 'Scroll',
        // About
        aboutLabel: 'Our Legacy',
        aboutTitle: 'Where <em>craft</em> becomes ritual',
        aboutText: 'Founded by master barbers with decades of experience, The Gilded Blade revives the timeless art of gentlemen\'s grooming. Every cut, every shave, every detail — performed with unwavering precision and respect for tradition.',
        stat1: 'Years of Excellence',
        stat2: 'Master Barbers',
        stat3: 'Happy Guests',
        // Services
        servicesLabel: 'Services',
        servicesTitle: 'Precision <em>grooming</em>',
        service1Name: 'Signature Cut',
        service1Desc: 'Precision scissor work and tailored styling',
        service1Price: '€45',
        service2Name: 'Hot Towel Shave',
        service2Desc: 'Traditional straight razor shave with steam towels',
        service2Price: '€35',
        service3Name: 'King\'s Groom',
        service3Desc: 'Cut, shave, and premium treatment',
        service3Price: '€70',
        service4Name: 'Beard Sculpt',
        service4Desc: 'Shape, trim, and hot oil massage',
        service4Price: '€30',
        // Gallery
        galleryLabel: 'Portfolio',
        galleryTitle: 'Our <em>work</em>',
        galleryItem1: 'Classic Cut',
        galleryItem2: 'Hot Towel',
        galleryItem3: 'Beard Sculpt',
        galleryItem4: 'Razor Finish',
        galleryItem5: 'Style Studio',
        // Booking
        bookingLabel: 'Reserve',
        bookingTitle: 'Secure your <em>chair</em>',
        formName: 'Full Name',
        formEmail: 'Email',
        formPhone: 'Phone',
        formService: 'Select Service',
        formDate: 'Preferred Date',
        formTime: 'Preferred Time',
        formMessage: 'Special Requests',
        formSubmit: 'Request Appointment',
        serviceOption1: 'Signature Cut',
        serviceOption2: 'Hot Towel Shave',
        serviceOption3: 'King\'s Groom',
        serviceOption4: 'Beard Sculpt',
        // Hours
        hoursTitle: 'Opening Hours',
        monday: 'Monday',
        tuesday: 'Tuesday',
        wednesday: 'Wednesday',
        thursday: 'Thursday',
        friday: 'Friday',
        saturday: 'Saturday',
        sunday: 'Sunday',
        closed: 'Closed',
        // Contact
        contactLabel: 'Visit Us',
        contactAddress: '47 Gilded Lane, Berlin',
        contactPhone: '+49 30 123 45678',
        contactEmail: 'hello@gildedblade.com',
        // Footer
        footerRights: '© 2025 The Gilded Blade. All rights reserved.',
        footerPrivacy: 'Privacy',
        footerImprint: 'Imprint'
      },
      de: {
        // Navigation
        navAbout: 'Über uns',
        navServices: 'Leistungen',
        navGallery: 'Galerie',
        navBooking: 'Buchung',
        // Hero
        heroTag: 'Gegr. 2025',
        heroTitle: 'Die Vergoldete Klinge',
        heroSub: 'Traditionelles Handwerk trifft moderne Präzision. Erleben Sie die feinste Körperpflege in einer Atmosphäre zurückhaltenden Luxus.',
        heroBtn1: 'Termin buchen',
        heroBtn2: 'Leistungen entdecken',
        heroScroll: 'Scrollen',
        // About
        aboutLabel: 'Unser Erbe',
        aboutTitle: 'Wo <em>Handwerk</em> zur Zeremonie wird',
        aboutText: 'Gegründet von Meisterfriseuren mit jahrzehntelanger Erfahrung, belebt Die Vergoldete Klinge die zeitlose Kunst der Herrenpflege wieder. Jeder Schnitt, jede Rasur, jedes Detail – mit unerschütterlicher Präzision und Respekt vor der Tradition.',
        stat1: 'Jahre Exzellenz',
        stat2: 'Meisterfriseure',
        stat3: 'Zufriedene Gäste',
        // Services
        servicesLabel: 'Leistungen',
        servicesTitle: 'Präzisions-<em>pflege</em>',
        service1Name: 'Signature Schnitt',
        service1Desc: 'Präzise Scherenarbeit & individuelles Styling',
        service1Price: '45€',
        service2Name: 'Heißrasur',
        service2Desc: 'Traditionelle Rasiermesserrasur mit Dampftüchern',
        service2Price: '35€',
        service3Name: 'Königsrasur',
        service3Desc: 'Schnitt, Rasur & Premium-Behandlung',
        service3Price: '70€',
        service4Name: 'Bartskulptur',
        service4Desc: 'Formung, Trimmen & Heißöl-Massage',
        service4Price: '30€',
        // Gallery
        galleryLabel: 'Portfolio',
        galleryTitle: 'Unsere <em>Arbeit</em>',
        galleryItem1: 'Klassischer Schnitt',
        galleryItem2: 'Heißrasur',
        galleryItem3: 'Bartskulptur',
        galleryItem4: 'Rasur-Finish',
        galleryItem5: 'Style Studio',
        // Booking
        bookingLabel: 'Reservieren',
        bookingTitle: 'Sichern Sie sich Ihren <em>Platz</em>',
        formName: 'Vollständiger Name',
        formEmail: 'E-Mail',
        formPhone: 'Telefon',
        formService: 'Leistung wählen',
        formDate: 'Wunschtermin',
        formTime: 'Uhrzeit',
        formMessage: 'Besondere Wünsche',
        formSubmit: 'Terminanfrage senden',
        serviceOption1: 'Signature Schnitt',
        serviceOption2: 'Heißrasur',
        serviceOption3: 'Königsrasur',
        serviceOption4: 'Bartskulptur',
        // Hours
        hoursTitle: 'Öffnungszeiten',
        monday: 'Montag',
        tuesday: 'Dienstag',
        wednesday: 'Mittwoch',
        thursday: 'Donnerstag',
        friday: 'Freitag',
        saturday: 'Samstag',
        sunday: 'Sonntag',
        closed: 'Geschlossen',
        // Contact
        contactLabel: 'Besuchen Sie uns',
        contactAddress: 'Gilded Lane 47, Berlin',
        contactPhone: '+49 30 123 45678',
        contactEmail: 'hallo@gildedblade.com',
        // Footer
        footerRights: '© 2025 Die Vergoldete Klinge. Alle Rechte vorbehalten.',
        footerPrivacy: 'Datenschutz',
        footerImprint: 'Impressum'
      }
    };

    function translatePage(lang) {
      const t = translations[lang];

      // Navigation
      document.querySelectorAll('.nav-links a').forEach((link, idx) => {
        const href = link.getAttribute('href');
        if (href === '#about') link.textContent = t.navAbout;
        if (href === '#services') link.textContent = t.navServices;
        if (href === '#gallery') link.textContent = t.navGallery;
        if (href === '#booking') link.textContent = t.navBooking;
      });

      // Hero
      const heroTag = document.querySelector('.hero-tag');
      if (heroTag) heroTag.textContent = t.heroTag;
      const heroTitle = document.querySelector('.hero-title');
      if (heroTitle) heroTitle.innerHTML = t.heroTitle;
      const heroSub = document.querySelector('.hero-sub');
      if (heroSub) heroSub.textContent = t.heroSub;
      const heroBtns = document.querySelectorAll('.hero-btns .btn-primary, .hero-btns .btn-outline');
      if (heroBtns[0]) heroBtns[0].textContent = t.heroBtn1;
      if (heroBtns[1]) heroBtns[1].textContent = t.heroBtn2;
      const heroDividerSpan = document.querySelector('.hero-divider span');
      if (heroDividerSpan) heroDividerSpan.textContent = t.heroScroll;

      // About
      const aboutLabel = document.querySelector('#about .section-label');
      if (aboutLabel) aboutLabel.textContent = t.aboutLabel;
      const aboutTitle = document.querySelector('#about .section-title');
      if (aboutTitle) aboutTitle.innerHTML = t.aboutTitle;
      const aboutText = document.querySelector('#about .about-text p');
      if (aboutText) aboutText.textContent = t.aboutText;
      const statLabels = document.querySelectorAll('.about-stats .stat-label');
      if (statLabels[0]) statLabels[0].textContent = t.stat1;
      if (statLabels[1]) statLabels[1].textContent = t.stat2;
      if (statLabels[2]) statLabels[2].textContent = t.stat3;

      // Services
      const servicesLabel = document.querySelector('#services .section-label');
      if (servicesLabel) servicesLabel.textContent = t.servicesLabel;
      const servicesTitle = document.querySelector('#services .section-title');
      if (servicesTitle) servicesTitle.innerHTML = t.servicesTitle;
      const serviceNames = document.querySelectorAll('.service-name');
      if (serviceNames[0]) serviceNames[0].textContent = t.service1Name;
      if (serviceNames[1]) serviceNames[1].textContent = t.service2Name;
      if (serviceNames[2]) serviceNames[2].textContent = t.service3Name;
      if (serviceNames[3]) serviceNames[3].textContent = t.service4Name;
      const serviceDescs = document.querySelectorAll('.service-desc');
      if (serviceDescs[0]) serviceDescs[0].textContent = t.service1Desc;
      if (serviceDescs[1]) serviceDescs[1].textContent = t.service2Desc;
      if (serviceDescs[2]) serviceDescs[2].textContent = t.service3Desc;
      if (serviceDescs[3]) serviceDescs[3].textContent = t.service4Desc;
      const servicePrices = document.querySelectorAll('.service-price');
      if (servicePrices[0]) servicePrices[0].textContent = t.service1Price;
      if (servicePrices[1]) servicePrices[1].textContent = t.service2Price;
      if (servicePrices[2]) servicePrices[2].textContent = t.service3Price;
      if (servicePrices[3]) servicePrices[3].textContent = t.service4Price;

      // Gallery
      const galleryLabel = document.querySelector('#gallery .section-label');
      if (galleryLabel) galleryLabel.textContent = t.galleryLabel;
      const galleryTitle = document.querySelector('#gallery .section-title');
      if (galleryTitle) galleryTitle.innerHTML = t.galleryTitle;
      const galleryItems = document.querySelectorAll('.gallery-item');
      if (galleryItems[0]) galleryItems[0].textContent = t.galleryItem1;
      if (galleryItems[1]) galleryItems[1].textContent = t.galleryItem2;
      if (galleryItems[2]) galleryItems[2].textContent = t.galleryItem3;
      if (galleryItems[3]) galleryItems[3].textContent = t.galleryItem4;
      if (galleryItems[4]) galleryItems[4].textContent = t.galleryItem5;

      // Booking
      const bookingLabel = document.querySelector('#booking .section-label');
      if (bookingLabel) bookingLabel.textContent = t.bookingLabel;
      const bookingTitle = document.querySelector('#booking .section-title');
      if (bookingTitle) bookingTitle.innerHTML = t.bookingTitle;
      const formLabels = document.querySelectorAll('#booking label');
      if (formLabels[0]) formLabels[0].textContent = t.formName;
      if (formLabels[1]) formLabels[1].textContent = t.formEmail;
      if (formLabels[2]) formLabels[2].textContent = t.formPhone;
      if (formLabels[3]) formLabels[3].textContent = t.formService;
      if (formLabels[4]) formLabels[4].textContent = t.formDate;
      if (formLabels[5]) formLabels[5].textContent = t.formTime;
      if (formLabels[6]) formLabels[6].textContent = t.formMessage;
      const submitBtn = document.querySelector('#booking .btn-primary');
      if (submitBtn) submitBtn.textContent = t.formSubmit;
      const serviceOptions = document.querySelectorAll('#service-select option');
      if (serviceOptions[0]) serviceOptions[0].textContent = t.serviceOption1;
      if (serviceOptions[1]) serviceOptions[1].textContent = t.serviceOption2;
      if (serviceOptions[2]) serviceOptions[2].textContent = t.serviceOption3;
      if (serviceOptions[3]) serviceOptions[3].textContent = t.serviceOption4;

      // Hours
      const hoursRows = document.querySelectorAll('.hours-row');
      if (hoursRows[0]) hoursRows[0].querySelector('.day').textContent = t.monday;
      if (hoursRows[1]) hoursRows[1].querySelector('.day').textContent = t.tuesday;
      if (hoursRows[2]) hoursRows[2].querySelector('.day').textContent = t.wednesday;
      if (hoursRows[3]) hoursRows[3].querySelector('.day').textContent = t.thursday;
      if (hoursRows[4]) hoursRows[4].querySelector('.day').textContent = t.friday;
      if (hoursRows[5]) hoursRows[5].querySelector('.day').textContent = t.saturday;
      if (hoursRows[6]) hoursRows[6].querySelector('.day').textContent = t.sunday;
      hoursRows.forEach(row => {
        const timeSpan = row.querySelector('span:last-child');
        if (timeSpan && timeSpan.textContent.includes('Closed') || timeSpan.textContent.includes('Geschlossen')) {
          timeSpan.textContent = t.closed;
        }
      });

      // Contact
      const contactLabels = document.querySelectorAll('.contact-label');
      if (contactLabels[0]) contactLabels[0].textContent = t.contactLabel;
      const contactValues = document.querySelectorAll('.contact-value');
      if (contactValues[0]) contactValues[0].textContent = t.contactAddress;
      if (contactValues[1]) contactValues[1].textContent = t.contactPhone;
      if (contactValues[2]) contactValues[2].textContent = t.contactEmail;

      // Footer
      const footerRights = document.querySelector('footer p:first-child');
      if (footerRights) footerRights.textContent = t.footerRights;
      const footerLinks = document.querySelectorAll('.footer-links a');
      if (footerLinks[0]) footerLinks[0].textContent = t.footerPrivacy;
      if (footerLinks[1]) footerLinks[1].textContent = t.footerImprint;

      // Update button text
      const toggleBtn = document.getElementById('lang-toggle');
      if (toggleBtn) {
        toggleBtn.textContent = lang === 'en' ? '🇩🇪 Deutsch' : '🇬🇧 English';
      }
    }

    // Attach event listener
    document.addEventListener('DOMContentLoaded', () => {
      const toggleBtn = document.getElementById('lang-toggle');
      if (toggleBtn) {
        toggleBtn.addEventListener('click', () => {
          currentLang = currentLang === 'en' ? 'de' : 'en';
          translatePage(currentLang);
        });
      }
    });
  })();
</script>
## 🌐 Language Toggle

The website includes a built-in English/German toggle button.  
Click **🇩🇪 Deutsch** to switch to German, click again to return to English.  
No page reload required – instant translation of all content.
