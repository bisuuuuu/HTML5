<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no" />
<meta http-equiv="X-UA-Compatible" content="IE=edge" />
<title>My Interactive HTML5 Portfolio</title>
<style>
  /* CSS Variables for theme colors */
  :root {
    --primary-color: #1e90ff;
    --primary-color-dark: #0f61d7;
    --background-color: #f0f2f5;
    --text-color: #333;
    --border-radius: 10px;
    --transition-speed: 0.3s;
  }

  /* Reset and base */
  * {
    box-sizing: border-box;
  }
  html, body {
    height: 100%;
    margin: 0;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: var(--background-color);
    color: var(--text-color);
    line-height: 1.6;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    -webkit-text-size-adjust: 100%;
    -moz-text-size-adjust: 100%;
    -ms-text-size-adjust: 100%;
    text-size-adjust: 100%;
  }
  a {
    color: var(--primary-color);
    text-decoration: none;
  }
  a:hover, a:focus {
    text-decoration: underline;
    outline-offset: 3px;
  }

  /* Container and layout */
  body > header, main, footer {
    max-width: 350px;
    margin: 8px auto;
    padding: 1rem 1rem 2rem 1rem;
    background: white;
    border-radius: var(--border-radius);
    box-shadow:
      0 8px 16px rgba(0,0,0,0.15),
      0 0 5px rgba(30, 144, 255, 0.2);
  }
  header {
    text-align: center;
    margin-bottom: 1rem;
  }
  header h1 {
    margin: 0.5rem 0 0.2rem 0;
    font-weight: 700;
    font-size: 1.8rem;
    color: var(--primary-color-dark);
  }
  header p {
    font-style: italic;
    color: #666;
    margin-top: 0;
    font-size: 0.95rem;
    letter-spacing: 0.03em;
  }

  /* Navigation styles */
  nav {
    margin-top: 10px;
    display: flex;
    justify-content: center;
    gap: 1rem;
    flex-wrap: wrap;
  }
  nav button {
    background: var(--primary-color);
    color: white;
    border: none;
    padding: 0.5rem 0.75rem;
    border-radius: 6px;
    cursor: pointer;
    font-size: 1rem;
    font-weight: 600;
    transition: background-color var(--transition-speed) ease, box-shadow var(--transition-speed) ease;
    box-shadow: 0 2px 6px rgba(0,0,0,0.15);
  }
  nav button:hover, nav button:focus {
    background: var(--primary-color-dark);
    outline: 2px solid var(--primary-color);
    outline-offset: 3px;
    box-shadow: 0 0 8px var(--primary-color-dark);
  }
  nav button:focus-visible {
    outline-offset: 3px;
  }

  /* Section styles */
  section {
    margin-top: 1.5rem;
    line-height: 1.5;
  }
  h2.section-title {
    border-bottom: 3px solid var(--primary-color);
    padding-bottom: 0.35rem;
    margin-bottom: 1rem;
    font-weight: 700;
    color: var(--primary-color-dark);
    font-size: 1.35rem;
  }

  /* Interactive Resume Section */
  #resume ul {
    padding-left: 1.2rem;
    margin: 0;
    list-style-type: disc;
  }
  #resume li {
    margin-bottom: 0.6rem;
    font-size: 1rem;
    color: var(--text-color);
  }

  /* Gallery Section */
  #gallery {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(90px,1fr));
    gap: 12px;
    margin-top: 0.5rem;
  }
  #gallery img {
    width: 100%;
    height: 90px;
    object-fit: cover;
    border-radius: 8px;
    cursor: pointer;
    box-shadow: 0 4px 8px rgba(0,0,0,0.12);
    transition: transform 0.25s ease, box-shadow 0.25s ease;
  }
  #gallery img:hover, #gallery img:focus {
    transform: scale(1.07);
    box-shadow: 0 8px 12px rgba(30,144,255,0.5);
    outline: 2px solid var(--primary-color);
    outline-offset: 2px;
  }
  #gallery img:focus-visible {
    outline-offset: 2px;
  }

  /* Modal for gallery image */
  #modal {
    position: fixed;
    top:0; left:0; right:0; bottom:0;
    background: rgba(0,0,0,0.85);
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 1rem;
    visibility: hidden;
    opacity: 0;
    transition: opacity var(--transition-speed) ease;
    z-index: 1000;
  }
  #modal.show {
    visibility: visible;
    opacity: 1;
  }
  #modal img {
    max-width: 90vw;
    max-height: 80vh;
    border-radius: var(--border-radius);
    box-shadow: 0 0 15px white;
    user-select: none;
  }
  #modal span.closebtn {
    position: absolute;
    top: 12px;
    right: 18px;
    font-size: 2.5rem;
    color: white;
    cursor: pointer;
    user-select: none;
    transition: color 0.2s ease;
  }
  #modal span.closebtn:hover, #modal span.closebtn:focus {
    color: var(--primary-color);
    outline-offset: 3px;
  }
  #modal span.closebtn:focus-visible {
    outline: 3px solid var(--primary-color);
    outline-offset: 3px;
  }

  /* Contact Form */
  form {
    display: flex;
    flex-direction: column;
  }
  label {
    margin-top: 1rem;
    margin-bottom: 0.25rem;
    font-weight: 600;
    font-size: 1rem;
  }
  input[type="text"], input[type="email"], textarea {
    padding: 0.5rem;
    border-radius: 6px;
    border: 1.5px solid #ccc;
    font-size: 1rem;
    resize: vertical;
    transition: border-color var(--transition-speed) ease, box-shadow var(--transition-speed) ease;
  }
  textarea {
    min-height: 80px;
  }
  input:focus, textarea:focus {
    border-color: var(--primary-color);
    outline: none;
    box-shadow: 0 0 6px var(--primary-color);
  }
  input:invalid {
    border-color: #e74c3c;
  }
  input:invalid:focus {
    box-shadow: 0 0 8px #e74c3c;
  }
  button[type="submit"] {
    margin-top: 1.5rem;
    background: var(--primary-color);
    color: white;
    border: none;
    padding: 0.75rem;
    border-radius: 8px;
    font-size: 1.1rem;
    font-weight: 700;
    cursor: pointer;
    transition: background-color var(--transition-speed) ease, box-shadow var(--transition-speed) ease;
    box-shadow: 0 3px 8px rgba(30, 144, 255, 0.7);
  }
  button[type="submit"]:hover, button[type="submit"]:focus {
    background: var(--primary-color-dark);
    outline: none;
    box-shadow: 0 0 14px var(--primary-color-dark);
  }
  button[type="submit"]:focus-visible {
    outline: 3px solid var(--primary-color);
    outline-offset: 3px;
  }

  /* Confirmation message */
  #confirmation {
    margin-top: 1rem;
    background: #d4edda;
    color: #155724;
    border: 1px solid #c3e6cb;
    padding: 0.75rem;
    border-radius: 6px;
    font-weight: 600;
    display: none;
  }

  /* Canvas Section */
  #canvas-section {
    margin-top: 2rem;
    background: #222;
    border-radius: var(--border-radius);
    overflow: hidden;
  }
  #myCanvas {
    width: 100%;
    height: 150px;
    display: block;
    cursor: crosshair;
  }

  /* Accessibility: focus outlines */
  :focus-visible {
    outline-offset: 3px;
  }

  /* Responsive adjustments */
  @media (max-width: 400px) {
    body > header, main, footer {
      max-width: 100vw;
      border-radius: 0;
      box-shadow: none;
      padding: 1rem 0.75rem 1.5rem 0.75rem;
    }
    nav {
      flex-wrap: wrap;
      gap: 0.5rem;
    }
    nav button {
      flex: 1 1 48%;
      padding: 0.6rem 0;
      font-size: 1rem;
    }
    #gallery {
      grid-template-columns: repeat(auto-fill, minmax(80px,1fr));
      gap: 8px;
    }
  }
</style>
</head>
<body>
<header role="banner">
  <h1 tabindex="0">Bisuuuu </h1>
  <p>Interactive HTML5 Developer Portfolio</p>
  <nav role="navigation" aria-label="Primary navigation">
    <button id="btnAbout" aria-controls="about" aria-expanded="false">About Me</button>
    <button id="btnResume" aria-controls="resume" aria-expanded="false">Resume</button>
    <button id="btnGallery" aria-controls="gallery-section" aria-expanded="false">Gallery</button>
    <button id="btnContact" aria-controls="contact" aria-expanded="false">Contact</button>
    <button id="btnCanvas" aria-controls="canvas-section" aria-expanded="false">Interactive Canvas</button>
  </nav>
</header>

<main>
  <section id="about" tabindex="-1" hidden>
    <h2 class="section-title">About Me</h2>
    <p>Hello! I'm Jane Doe, a passionate front-end developer with expertise in modern HTML5, CSS3, and JavaScript. I create interactive and accessible websites that look great on all devices.</p>
    <video controls width="320" preload="metadata" aria-label="Introduction video">
      <source src="https://interactive-examples.mdn.mozilla.net/media/cc0-videos/flower.webm" type="video/webm" />
      <source src="https://interactive-examples.mdn.mozilla.net/media/cc0-videos/flower.mp4" type="video/mp4" />
      Your browser does not support the video tag.
    </video>
  </section>

  <section id="resume" tabindex="-1" hidden>
    <h2 class="section-title">Interactive Resume</h2>
    <ul>
      <li><strong>Frontend Developer</strong> at Awesome Tech Co. (2022–Present)</li>
      <li><strong>UI/UX Designer</strong> at Creative Solutions (2020–2022)</li>
      <li><strong>Intern Developer</strong> at WebStart (2019–2020)</li>
    </ul>
    <p>Skilled in HTML5 semantics, CSS animations, JavaScript ES6+, and responsive design. Experienced with REST APIs, Git, and Agile methodologies.</p>
  </section>

  <section id="gallery-section" tabindex="-1" hidden>
    <h2 class="section-title">Gallery</h2>
    <p>Click on an image to enlarge.</p>
    <div id="gallery" role="list" aria-label="Portfolio images">
      <img src="https://picsum.photos/id/1018/100/100" alt="Sample project 1" tabindex="0" role="listitem" />
      <img src="https://picsum.photos/id/1025/100/100" alt="Sample project 2" tabindex="0" role="listitem" />
      <img src="https://picsum.photos/id/1033/100/100" alt="Sample project 3" tabindex="0" role="listitem" />
      <img src="https://picsum.photos/id/1057/100/100" alt="Sample project 4" tabindex="0" role="listitem" />
    </div>
  </section>

  <div id="modal" role="dialog" aria-modal="true" aria-labelledby="modalImageDesc" tabindex="-1">
    <span class="closebtn" role="button" aria-label="Close modal" tabindex="0">&times;</span>
    <img src="" alt="" id="modalImage" />
  </div>

  <section id="contact" tabindex="-1" hidden>
    <h2 class="section-title">Contact Me</h2>
    <form id="contactForm" aria-label="Contact form">
      <label for="nameInput">Name</label>
      <input type="text" id="nameInput" name="name" aria-required="true" required placeholder="Your name" />

      <label for="emailInput">Email</label>
      <input type="email" id="emailInput" name="email" aria-required="true" required placeholder="your.email@example.com" />

      <label for="messageInput">Message</label>
      <textarea id="messageInput" name="message" aria-required="true" required placeholder="Write your message here..."></textarea>

      <button type="submit">Send Message</button>
    </form>
    <div id="confirmation" role="alert" aria-live="polite">Thank you! Your message has been sent.</div>
  </section>

  <section id="canvas-section" tabindex="-1" hidden>
    <h2 class="section-title" id="canvasTitle">Interactive Canvas</h2>
    <canvas id="myCanvas" width="350" height="150" role="img" aria-labelledby="canvasTitle" aria-describedby="canvasDesc"></canvas>
    <p id="canvasDesc" style="font-size:0.9rem; color:#ccc; margin-top:8px;">Hover or tap on the canvas to draw colorful circles.</p>
  </section>
</main>

<script>
  // Simple navigation controls to show/hide sections
  const sections = {
    about: document.getElementById('about'),
    resume: document.getElementById('resume'),
    'gallery-section': document.getElementById('gallery-section'),
    contact: document.getElementById('contact'),
    'canvas-section': document.getElementById('canvas-section'),
  };

  const buttons = {
    btnAbout: document.getElementById('btnAbout'),
    btnResume: document.getElementById('btnResume'),
    btnGallery: document.getElementById('btnGallery'),
    btnContact: document.getElementById('btnContact'),
    btnCanvas: document.getElementById('btnCanvas'),
  };

  function hideAllSections() {
    for (const key in sections) {
      sections[key].hidden = true;
      const btnKey = "btn" + key.charAt(0).toUpperCase() + key.slice(1).replace(/-([a-z])/g, (m, w) => w.toUpperCase());
      if (buttons[btnKey]) {
        buttons[btnKey].setAttribute('aria-expanded', 'false');
      }
    }
  }

  // Show section on button click
  Object.entries(buttons).forEach(([btnId, btn]) => {
    btn.addEventListener('click', () => {
      hideAllSections();
      const secId = btn.getAttribute('aria-controls');
      const section = document.getElementById(secId);
      if (section) {
        section.hidden = false;
        btn.setAttribute('aria-expanded', 'true');
        section.focus();
      }
    });
  });

  // Gallery modal functionality
  const gallery = document.getElementById('gallery');
  const modal = document.getElementById('modal');
  const modalImage = document.getElementById('modalImage');
  const closeBtn = modal.querySelector('.closebtn');

  function openModal(src, alt) {
    modalImage.src = src;
    modalImage.alt = alt;
    modal.classList.add('show');
    modal.focus();
  }

  function closeModal() {
    modal.classList.remove('show');
    modalImage.src = '';
    modalImage.alt = '';
    gallery.querySelector('img[tabindex="0"]').focus();
  }

  gallery.addEventListener('click', e => {
    if (e.target.tagName === 'IMG') {
      openModal(e.target.src.replace('/100/100', '/600/400'), e.target.alt);
    }
  });

  // Keyboard accessibility for gallery images (Enter or Space opens modal)
  gallery.addEventListener('keydown', e => {
    if ((e.key === 'Enter' || e.key === ' ') && e.target.tagName === 'IMG') {
      e.preventDefault();
      openModal(e.target.src.replace('/100/100', '/600/400'), e.target.alt);
    }
  });

  closeBtn.addEventListener('click', closeModal);
  closeBtn.addEventListener('keydown', e => {
    if (e.key === 'Enter' || e.key === ' ') {
      e.preventDefault();
      closeModal();
    }
  });

  // Close modal when clicking outside the image
  modal.addEventListener('click', e => {
    if (e.target === modal) {
      closeModal();
    }
  });

  // Close modal on Escape key
  document.addEventListener('keydown', e => {
    if (e.key === 'Escape' && modal.classList.contains('show')) {
      closeModal();
    }
  });

  // Contact form localStorage saving & confirmation
  const form = document.getElementById('contactForm');
  const confirmation = document.getElementById('confirmation');

  // Load saved form data from localStorage
  window.addEventListener('load', () => {
    if (localStorage.getItem('contactFormData')) {
      const data = JSON.parse(localStorage.getItem('contactFormData'));
      form.name.value = data.name || '';
      form.email.value = data.email || '';
      form.message.value = data.message || '';
    }
  });

  // Save data on input
  form.addEventListener('input', () => {
    const data = {
      name: form.name.value,
      email: form.email.value,
      message: form.message.value,
    };
    localStorage.setItem('contactFormData', JSON.stringify(data));
  });

  // Handle form submission
  form.addEventListener('submit', e => {
    e.preventDefault();
    if (!form.checkValidity()) {
      form.reportValidity();
      return;
    }
    // Simulate sending
    confirmation.style.display = 'block';
    setTimeout(() => {
      confirmation.style.display = 'none';
    }, 4000);
    form.reset();
    localStorage.removeItem('contactFormData');
  });

  // Canvas drawing interactive area
  const canvas = document.getElementById('myCanvas');
  const ctx = canvas.getContext('2d');

  // Resize canvas for high DPI displays
  function resizeCanvas() {
    const dpr = window.devicePixelRatio || 1;
    const rect = canvas.getBoundingClientRect();
    canvas.width = rect.width * dpr;
    canvas.height = rect.height * dpr;
    ctx.setTransform(1, 0, 0, 1, 0, 0);
    ctx.scale(dpr, dpr);
    drawBackground();
  }

  // Draw background gradient
  function drawBackground() {
    const width = canvas.width / (window.devicePixelRatio || 1);
    const height = canvas.height / (window.devicePixelRatio || 1);
    const gradient = ctx.createLinearGradient(0, 0, width, height);
    gradient.addColorStop(0, '#1e90ff');
    gradient.addColorStop(1, '#6a11cb');
    ctx.fillStyle = gradient;
    ctx.fillRect(0, 0, width, height);
  }

  resizeCanvas();
  window.addEventListener('resize', resizeCanvas);

  // Draw colorful circles on mouse/touch move or click
  function drawCircle(x, y) {
    const radius = 15 + Math.random() * 10;
    const colors = ['#ffc107', '#28a745', '#e83e8c', '#17a2b8', '#fd7e14', '#6f42c1', '#20c997'];
    const color = colors[Math.floor(Math.random() * colors.length)];
    ctx.beginPath();
    ctx.arc(x, y, radius, 0, 2 * Math.PI);
    ctx.fillStyle = color;
    ctx.shadowColor = color;
    ctx.shadowBlur = 15;
    ctx.fill();
  }

  function handlePointer(event) {
    let x, y;
    if (event.touches) {
      x = event.touches[0].clientX - canvas.getBoundingClientRect().left;
      y = event.touches[0].clientY - canvas.getBoundingClientRect().top;
    } else {
      x = event.offsetX;
      y = event.offsetY;
    }
    drawCircle(x, y);
  }

  canvas.addEventListener('mousemove', e => {
    if (e.buttons === 1) {
      handlePointer(e);
    }
  });
  canvas.addEventListener('click', handlePointer);
  canvas.addEventListener('touchmove', e => {
    e.preventDefault();
    handlePointer(e);
  }, {passive:false});
  canvas.addEventListener('touchstart', e => {
    e.preventDefault();
    handlePointer(e);
  }, {passive:false});
</script>
</body>
</html>

