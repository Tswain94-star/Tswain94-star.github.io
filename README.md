<!DOCTYPE html>
<html lang="en" class="dark">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Ma'at-Goral — The Balance of the Lot</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@500;600;700&family=Cormorant+Garamond:ital,wght@0,400;0,600;0,700;1,400&family=Frank+Ruhl+Libre:wght@500;700&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          colors: {
            obsidian: '#0b0d14',
            lapis: '#111625',
            lapisLight: '#182036',
            gold: '#d4af37',
            goldDim: '#9c7c1c',
            goldBright: '#f3d46b',
            parchment: '#e8dec8',
            limestone: '#b8ae98',
            crimson: '#9e2a2b',
            turquoise: '#2a9d8f'
          },
          fontFamily: {
            display: ['Cinzel', 'serif'],
            serif: ['Cormorant Garamond', 'serif'],
            hebrew: ['Frank Ruhl Libre', 'serif'],
            mono: ['JetBrains Mono', 'monospace']
          }
        }
      }
    }
  </script>
  <style>
    body {
      background-color: #0b0d14;
      color: #e8dec8;
      font-family: 'Cormorant Garamond', serif;
      overflow-x: hidden;
    }

    /* Subtle Sacred Geometry Background */
    .sacred-bg {
      background-image: radial-gradient(circle at 50% 15%, rgba(212, 175, 55, 0.08) 0%, rgba(11, 13, 20, 0) 60%),
                        radial-gradient(circle at 85% 80%, rgba(42, 157, 143, 0.05) 0%, rgba(11, 13, 20, 0) 50%);
    }

    /* Animations */
    @keyframes floatSlow {
      0%, 100% { transform: translateY(0px) rotate(0deg); }
      50% { transform: translateY(-6px) rotate(1deg); }
    }

    @keyframes staveDrop {
      0% { transform: translateY(-30px) rotateX(180deg) scale(0.9); opacity: 0; }
      60% { transform: translateY(4px) rotateX(-15deg) scale(1.02); opacity: 1; }
      100% { transform: translateY(0) rotateX(0deg) scale(1); opacity: 1; }
    }

    @keyframes stoneReveal {
      0% { transform: scale(0.5) rotate(-25deg); opacity: 0; filter: blur(6px); }
      70% { transform: scale(1.06) rotate(4deg); opacity: 1; filter: blur(0px); }
      100% { transform: scale(1) rotate(0deg); opacity: 1; }
    }

    @keyframes tokenFlip {
      0% { transform: perspective(800px) rotateY(90deg) scale(0.92); opacity: 0; }
      100% { transform: perspective(800px) rotateY(0deg) scale(1); opacity: 1; }
    }

    .animate-stave {
      animation: staveDrop 0.65s cubic-bezier(0.22, 1, 0.36, 1) forwards;
    }

    .animate-stone {
      animation: stoneReveal 0.6s cubic-bezier(0.22, 1, 0.36, 1) forwards;
    }

    .animate-token {
      animation: tokenFlip 0.6s cubic-bezier(0.22, 1, 0.36, 1) forwards;
    }

    .gold-border-glow {
      box-shadow: 0 0 20px rgba(212, 175, 55, 0.08), inset 0 0 12px rgba(212, 175, 55, 0.04);
    }

    .gold-border-glow:hover {
      box-shadow: 0 0 25px rgba(212, 175, 55, 0.16), inset 0 0 15px rgba(212, 175, 55, 0.07);
    }

    /* Custom Scrollbar */
    ::-webkit-scrollbar {
      width: 8px;
      height: 8px;
    }
    ::-webkit-scrollbar-track {
      background: #0b0d14;
    }
    ::-webkit-scrollbar-thumb {
      background: #283149;
      border-radius: 4px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: #d4af37;
    }
  </style>
</head>
<body class="sacred-bg min-h-screen flex flex-col selection:bg-gold/30 selection:text-goldBright">

  <!-- Decorative Sacred Geometry Watermark -->
  <div class="fixed inset-0 pointer-events-none flex items-center justify-center opacity-[0.035] z-0 overflow-hidden">
    <svg viewBox="0 0 600 600" class="w-[820px] h-[820px] text-gold" fill="none" stroke="currentColor" stroke-width="1">
      <circle cx="300" cy="300" r="280" />
      <circle cx="300" cy="300" r="220" stroke-dasharray="4 6" />
      <circle cx="300" cy="300" r="140" />
      <polygon points="300,20 542,440 58,440" />
      <polygon points="300,580 542,160 58,160" />
      <rect x="102" y="102" width="396" height="396" />
      <rect x="102" y="102" width="396" height="396" transform="rotate(45 300 300)" />
      <line x1="300" y1="0" x2="300" y2="600" />
      <line x1="0" y1="300" x2="600" y2="300" />
    </svg>
  </div>

  <!-- Toast Notification -->
  <div id="toast" class="fixed bottom-6 right-6 z-50 transform translate-y-20 opacity-0 transition-all duration-300 pointer-events-none">
    <div class="bg-lapis border border-gold/60 text-parchment px-5 py-3 rounded-lg shadow-2xl flex items-center gap-3 font-mono text-xs">
      <span class="w-2 h-2 rounded-full bg-gold animate-pulse"></span>
      <span id="toast-msg">Notification</span>
    </div>
  </div>

  <!-- Header -->
  <header class="relative z-10 border-b border-gold/20 bg-obsidian/80 backdrop-blur-md">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 py-5 flex flex-col md:flex-row items-center justify-between gap-4">
      <div class="flex items-center gap-4 text-center md:text-left">
        <!-- Balance Scale & Aleph Emblem -->
        <div class="w-12 h-12 rounded-xl bg-lapis border border-gold/40 flex items-center justify-center shadow-lg shrink-0">
          <svg viewBox="0 0 40 40" class="w-7 h-7 text-gold" fill="none" stroke="currentColor" stroke-width="1.6">
            <path d="M20 5V35M12 35H28M8 13H32" stroke-linecap="round"/>
            <path d="M8 13L4 22H12L8 13Z" fill="rgba(212,175,55,0.15)"/>
            <path d="M32 13L28 22H36L32 13Z" fill="rgba(212,175,55,0.15)"/>
            <circle cx="20" cy="13" r="2.5" fill="#d4af37"/>
          </svg>
        </div>
        <div>
          <h1 class="font-display text-xl sm:text-2xl md:text-3xl font-bold tracking-wider text-gold uppercase">
            Ma'at-Goral
          </h1>
          <p class="text-limestone text-sm sm:text-base tracking-wide italic">
            The Balance of the Lot • Synthesized Egyptian Cleromancy &amp; Hebrew Gematria Oracle
          </p>
        </div>
      </div>

      <div class="flex items-center gap-2.5">
        <button id="btn-reference" onclick="toggleReferenceModal(true)" class="px-4 py-2 rounded-lg bg-lapis hover:bg-lapisLight border border-gold/30 hover:border-gold text-parchment font-display text-xs tracking-wider uppercase transition flex items-center gap-2 cursor-pointer">
          <svg class="w-4 h-4 text-gold" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.8" d="M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.747 0 3.332.477 4.5 1.253v13C19.832 18.477 18.247 18 16.5 18c-1.746 0-3.332.477-4.5 1.253"/></svg>
          System Codex &amp; Lore
        </button>
      </div>
    </div>
  </header>

  <!-- Main Workspace -->
  <main class="relative z-10 flex-1 max-w-6xl w-full mx-auto px-4 sm:px-6 py-8 space-y-8">

    <!-- Query & Master Controls Section -->
    <section class="bg-lapis/90 border border-gold/25 rounded-2xl p-5 sm:p-6 gold-border-glow">
      <div class="flex flex-col lg:flex-row gap-4 items-stretch lg:items-end justify-between">
        <div class="flex-1 space-y-2">
          <label for="query-input" class="block font-display text-xs uppercase tracking-widest text-gold">
            Focus Your Query <span class="text-limestone/70 font-serif normal-case italic text-sm ml-1">(Frame around structure, timing, or alignment rather than passive fate)</span>
          </label>
          <input
            type="text"
            id="query-input"
            placeholder="e.g., What hidden structure governs my current endeavor, and how should I align with it?"
            class="w-full bg-obsidian/90 border border-gold/30 focus:border-gold rounded-xl px-4 py-3 text-parchment placeholder-limestone/40 text-base sm:text-lg focus:outline-none transition"
          />
        </div>

        <div class="flex flex-wrap sm:flex-nowrap gap-3 shrink-0">
          <button
            id="btn-cast-all"
            onclick="castAllSteps()"
            class="flex-1 sm:flex-initial px-6 py-3 rounded-xl bg-gradient-to-r from-goldDim via-gold to-goldDim hover:brightness-110 text-obsidian font-display font-bold text-xs sm:text-sm uppercase tracking-wider shadow-lg transition cursor-pointer flex items-center justify-center gap-2"
          >
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"/></svg>
            Cast All at Once
          </button>

          <button
            id="btn-reset"
            onclick="resetCast()"
            class="flex-1 sm:flex-initial px-5 py-3 rounded-xl bg-obsidian hover:bg-lapisLight border border-gold/30 hover:border-gold text-limestone hover:text-parchment font-display text-xs sm:text-sm uppercase tracking-wider transition cursor-pointer flex items-center justify-center gap-2"
          >
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15"/></svg>
            Reset / New Cast
          </button>
        </div>
      </div>

      <!-- Progress Stepper Bar -->
      <div class="mt-6 pt-4 border-t border-gold/15 grid grid-cols-2 sm:grid-cols-4 gap-2 text-xs font-mono">
        <div id="prog-1" class="flex items-center gap-2 px-3 py-1.5 rounded-lg bg-obsidian/60 border border-gold/30 text-gold">
          <span class="w-5 h-5 rounded-full bg-gold/20 flex items-center justify-center font-bold">1</span>
          <span>Binary Gate</span>
        </div>
        <div id="prog-2" class="flex items-center gap-2 px-3 py-1.5 rounded-lg bg-obsidian/40 border border-white/10 text-limestone/50">
          <span class="w-5 h-5 rounded-full bg-white/5 flex items-center justify-center font-bold">2</span>
          <span>Quadrature Drop</span>
        </div>
        <div id="prog-3" class="flex items-center gap-2 px-3 py-1.5 rounded-lg bg-obsidian/40 border border-white/10 text-limestone/50">
          <span class="w-5 h-5 rounded-full bg-white/5 flex items-center justify-center font-bold">3</span>
          <span>Triadic Draw</span>
        </div>
        <div id="prog-4" class="flex items-center gap-2 px-3 py-1.5 rounded-lg bg-obsidian/40 border border-white/10 text-limestone/50">
          <span class="w-5 h-5 rounded-full bg-white/5 flex items-center justify-center font-bold">4</span>
          <span>Gematria Root</span>
        </div>
      </div>
    </section>

    <!-- Top Grid: Step 1 (Binary Gate) & Step 2 (Quadrature Drop) -->
    <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">

      <!-- STEP 1: The Binary Gate (Urim & Thummim) -->
      <section id="card-step-1" class="lg:col-span-5 bg-lapis/90 border border-gold/30 rounded-2xl p-6 flex flex-col justify-between gold-border-glow transition-all">
        <div>
          <div class="flex items-center justify-between border-b border-gold/20 pb-3 mb-5">
            <div>
              <span class="font-mono text-[11px] uppercase tracking-widest text-gold/80">Step I • Hebrew Cleromancy</span>
              <h2 class="font-display text-lg sm:text-xl font-bold text-parchment">The Binary Gate</h2>
            </div>
            <span class="text-xs font-mono px-2.5 py-1 rounded bg-obsidian border border-gold/20 text-limestone">Urim &amp; Thummim</span>
          </div>

          <!-- Interactive Vessel / Result Area -->
          <div id="step-1-stage" class="min-h-[210px] flex flex-col items-center justify-center text-center p-4 rounded-xl bg-obsidian/70 border border-gold/15">
            <!-- Initial Uncast Vessel -->
            <div id="step-1-uncast" class="space-y-4">
              <div class="w-20 h-20 mx-auto rounded-full bg-gradient-to-b from-lapisLight to-obsidian border border-gold/40 flex items-center justify-center shadow-inner relative group">
                <div class="absolute inset-1 rounded-full border border-dashed border-gold/30 animate-spin" style="animation-duration: 18s;"></div>
                <svg class="w-9 h-9 text-gold" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4"/>
                </svg>
              </div>
              <p class="text-limestone text-base max-w-xs mx-auto">
                Reach into the concealed vessel (<em class="text-parchment">The Kli</em>) to draw one of the two Anchor Stones.
              </p>
            </div>

            <!-- Cast Stone Result -->
            <div id="step-1-result" class="hidden w-full space-y-4">
              <!-- Populated dynamically -->
            </div>
          </div>
        </div>

        <div class="mt-5 pt-4 border-t border-gold/15 flex justify-center">
          <button
            id="btn-step-1"
            onclick="performStep1()"
            class="w-full py-3 px-4 rounded-xl bg-lapisLight hover:bg-gold hover:text-obsidian border border-gold/50 text-gold font-display font-semibold text-xs uppercase tracking-widest transition cursor-pointer"
          >
            Draw Anchor Stone from Vessel
          </button>
        </div>
      </section>

      <!-- STEP 2: The Quadrature Drop (Egyptian Staves) -->
      <section id="card-step-2" class="lg:col-span-7 bg-lapis/90 border border-white/10 rounded-2xl p-6 flex flex-col justify-between transition-all opacity-75">
        <div>
          <div class="flex items-center justify-between border-b border-gold/20 pb-3 mb-5">
            <div>
              <span class="font-mono text-[11px] uppercase tracking-widest text-gold/80">Step II • Egyptian Casting Sticks</span>
              <h2 class="font-display text-lg sm:text-xl font-bold text-parchment">The Quadrature Drop</h2>
            </div>
            <span id="stave-counter-badge" class="text-xs font-mono px-2.5 py-1 rounded bg-obsidian border border-gold/20 text-limestone">4 Staves • 0–4 Scale</span>
          </div>

          <!-- Staves Visual Arena -->
          <div class="min-h-[210px] flex flex-col justify-between p-4 rounded-xl bg-obsidian/70 border border-gold/15">
            <!-- 4 Staves Visual Row -->
            <div id="staves-container" class="grid grid-cols-4 gap-3 sm:gap-5 my-auto py-3 px-2">
              <!-- Placeholder Staves -->
              <div class="h-28 rounded-lg border border-dashed border-gold/25 bg-lapis/40 flex flex-col items-center justify-center text-limestone/40 font-mono text-xs">
                <span>STAVE I</span>
              </div>
              <div class="h-28 rounded-lg border border-dashed border-gold/25 bg-lapis/40 flex flex-col items-center justify-center text-limestone/40 font-mono text-xs">
                <span>STAVE II</span>
              </div>
              <div class="h-28 rounded-lg border border-dashed border-gold/25 bg-lapis/40 flex flex-col items-center justify-center text-limestone/40 font-mono text-xs">
                <span>STAVE III</span>
              </div>
              <div class="h-28 rounded-lg border border-dashed border-gold/25 bg-lapis/40 flex flex-col items-center justify-center text-limestone/40 font-mono text-xs">
                <span>STAVE IV</span>
              </div>
            </div>

            <!-- Alignment Output -->
            <div id="step-2-result" class="mt-3 pt-3 border-t border-white/10 text-center">
              <p class="text-limestone/70 text-base italic">
                Complete Step I first, then cast the four two-sided staves to weigh the energetic momentum.
              </p>
            </div>
          </div>
        </div>

        <div class="mt-5 pt-4 border-t border-gold/15 flex justify-center">
          <button
            id="btn-step-2"
            onclick="performStep2()"
            disabled
            class="w-full py-3 px-4 rounded-xl bg-lapisLight border border-white/15 text-limestone/40 font-display font-semibold text-xs uppercase tracking-widest transition disabled:cursor-not-allowed enabled:hover:bg-gold enabled:hover:text-obsidian enabled:border-gold/50 enabled:text-gold enabled:cursor-pointer"
          >
            Cast Four Egyptian Staves
          </button>
        </div>
      </section>
    </div>

    <!-- STEP 3: The Triadic Draw (Sefer Yetzirah - Right to Left) -->
    <section id="card-step-3" class="bg-lapis/90 border border-white/10 rounded-2xl p-6 transition-all opacity-75">
      <div class="flex flex-col sm:flex-row sm:items-center justify-between border-b border-gold/20 pb-3 mb-5 gap-2">
        <div>
          <span class="font-mono text-[11px] uppercase tracking-widest text-gold/80">Step III • Sefer Yetzirah Matrix</span>
          <h2 class="font-display text-lg sm:text-xl font-bold text-parchment">The Triadic Draw (22 Hebrew Letters)</h2>
        </div>
        <div class="flex items-center gap-2 text-xs font-mono text-gold bg-obsidian px-3 py-1.5 rounded-lg border border-gold/25">
          <span>← READ RIGHT TO LEFT</span>
          <span class="text-limestone/50">|</span>
          <span class="text-limestone">Hebrew Script Order</span>
        </div>
      </div>

      <!-- 3 Slots Grid (Visually Ordered Left-to-Right in DOM so Slot 3 is Left, Slot 2 is Center, Slot 1 is Right) -->
      <div id="triadic-grid" class="grid grid-cols-1 md:grid-cols-3 gap-5">
        <!-- LEFT SLOT: Position 3 (The Fruit) -->
        <div id="token-slot-2" class="rounded-xl bg-obsidian/70 border border-dashed border-gold/25 p-5 min-h-[260px] flex flex-col items-center justify-center text-center">
          <span class="font-mono text-[11px] uppercase tracking-widest text-limestone/60 mb-1">Left Position (3rd Drawn)</span>
          <h3 class="font-display text-base text-gold/80 mb-2">The Fruit</h3>
          <p class="text-sm text-limestone/60 max-w-[220px]">Trajectory &amp; outcome if the current pattern holds.</p>
        </div>

        <!-- CENTER SLOT: Position 2 (The Fulcrum) -->
        <div id="token-slot-1" class="rounded-xl bg-obsidian/70 border border-dashed border-gold/25 p-5 min-h-[260px] flex flex-col items-center justify-center text-center">
          <span class="font-mono text-[11px] uppercase tracking-widest text-limestone/60 mb-1">Center Position (2nd Drawn)</span>
          <h3 class="font-display text-base text-gold/80 mb-2">The Fulcrum</h3>
          <p class="text-sm text-limestone/60 max-w-[220px]">Present tension, active mechanism, or pivot point.</p>
        </div>

        <!-- RIGHT SLOT: Position 1 (The Root) -->
        <div id="token-slot-0" class="rounded-xl bg-obsidian/70 border border-dashed border-gold/25 p-5 min-h-[260px] flex flex-col items-center justify-center text-center">
          <span class="font-mono text-[11px] uppercase tracking-widest text-limestone/60 mb-1">Right Position (1st Drawn)</span>
          <h3 class="font-display text-base text-gold/80 mb-2">The Root</h3>
          <p class="text-sm text-limestone/60 max-w-[220px]">Past cause, origin, or foundational reality.</p>
        </div>
      </div>

      <div class="mt-6 pt-4 border-t border-gold/15 flex justify-center">
        <button
          id="btn-step-3"
          onclick="performStep3()"
          disabled
          class="w-full sm:w-auto sm:min-w-[320px] py-3 px-6 rounded-xl bg-lapisLight border border-white/15 text-limestone/40 font-display font-semibold text-xs uppercase tracking-widest transition disabled:cursor-not-allowed enabled:hover:bg-gold enabled:hover:text-obsidian enabled:border-gold/50 enabled:text-gold enabled:cursor-pointer"
        >
          Draw 3 Letter Tokens (Right → Left)
        </button>
      </div>
    </section>

    <!-- STEP 4: The Gematria Reduction -->
    <section id="card-step-4" class="bg-lapis/90 border border-white/10 rounded-2xl p-6 transition-all opacity-75">
      <div class="flex items-center justify-between border-b border-gold/20 pb-3 mb-5">
        <div>
          <span class="font-mono text-[11px] uppercase tracking-widest text-gold/80">Step IV • Alphanumeric Synthesis</span>
          <h2 class="font-display text-lg sm:text-xl font-bold text-parchment">The Gematria Reduction</h2>
        </div>
        <span class="text-xs font-mono px-2.5 py-1 rounded bg-obsidian border border-gold/20 text-limestone">Mispar Katan • 1–9 Root</span>
      </div>

      <div id="step-4-content" class="rounded-xl bg-obsidian/70 border border-gold/15 p-6 text-center">
        <p class="text-limestone/70 text-base italic">
          Automatically calculates once the three Hebrew Letter Tokens are drawn in Step III.
        </p>
      </div>
    </section>

    <!-- SYNTHESIS & READING LOG -->
    <section id="synthesis-section" class="hidden bg-gradient-to-b from-lapis to-obsidian border border-gold/40 rounded-2xl p-6 sm:p-8 gold-border-glow space-y-6">
      <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4 border-b border-gold/25 pb-4">
        <div>
          <span class="font-mono text-xs uppercase tracking-widest text-gold">Complete Oracle Synthesis</span>
          <h2 class="font-display text-2xl font-bold text-parchment">Ma'at-Goral — The Balance of the Lot</h2>
        </div>
        <button
          onclick="copyReadingToClipboard()"
          class="px-4 py-2.5 rounded-xl bg-gold/15 hover:bg-gold hover:text-obsidian border border-gold/50 text-gold font-display font-semibold text-xs uppercase tracking-wider transition cursor-pointer flex items-center justify-center gap-2 shrink-0"
        >
          <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 5H6a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2v-1M8 5a2 2 0 002 2h2a2 2 0 002-2M8 5a2 2 0 012-2h2a2 2 0 012 2m0 0h2a2 2 0 012 2v3m2 4H10m0 0l3-3m-3 3l3 3"/></svg>
          Copy Reading
        </button>
      </div>

      <div id="synthesis-body" class="space-y-4 text-lg leading-relaxed text-parchment/95">
        <!-- Populated dynamically -->
      </div>
    </section>

  </main>

  <!-- Footer -->
  <footer class="relative z-10 border-t border-gold/15 py-6 px-4 text-center text-limestone/60 text-sm">
    <p class="font-serif italic">
      Ma'at-Goral (The Balance of the Lot) • Synthesizing Egyptian Ma'at Cleromancy, Hebrew Goral, and Sefer Yetzirah Gematria.
    </p>
  </footer>

  <!-- Reference & Historical Friction Modal -->
  <div id="reference-modal" class="fixed inset-0 z-50 hidden bg-black/80 backdrop-blur-sm flex items-center justify-center p-4">
    <div class="bg-lapis border border-gold/40 rounded-2xl max-w-4xl w-full max-h-[88vh] flex flex-col shadow-2xl overflow-hidden">
      <!-- Modal Header -->
      <div class="px-6 py-4 bg-obsidian border-b border-gold/25 flex items-center justify-between">
        <div>
          <span class="font-mono text-[11px] uppercase tracking-widest text-gold">Archive &amp; Compendium</span>
          <h3 class="font-display text-xl font-bold text-parchment">System Codex &amp; Historical Friction</h3>
        </div>
        <button onclick="toggleReferenceModal(false)" class="p-2 rounded-lg text-limestone hover:text-gold hover:bg-lapisLight transition cursor-pointer" aria-label="Close modal">
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/></svg>
        </button>
      </div>

      <!-- Modal Tabs -->
      <div class="flex border-b border-gold/20 bg-obsidian/50 px-6 gap-4 font-display text-xs uppercase tracking-wider">
        <button id="tab-letters" onclick="switchCodexTab('letters')" class="py-3 border-b-2 border-gold text-gold cursor-pointer">22 Hebrew Letters</button>
        <button id="tab-rules" onclick="switchCodexTab('rules')" class="py-3 border-b-2 border-transparent text-limestone hover:text-parchment cursor-pointer">Staves &amp; Frequencies</button>
        <button id="tab-history" onclick="switchCodexTab('history')" class="py-3 border-b-2 border-transparent text-limestone hover:text-parchment cursor-pointer">Historical Friction</button>
      </div>

      <!-- Modal Body -->
      <div class="p-6 overflow-y-auto space-y-6 text-parchment/90">
        <!-- Tab 1: 22 Letters -->
        <div id="codex-letters" class="space-y-4">
          <p class="text-base text-limestone">
            According to the <em class="text-parchment">Sefer Yetzirah</em> (Book of Formation), the 22 Hebrew letters divide into <strong class="text-gold">3 Mothers</strong> (Elemental forces), <strong class="text-gold">7 Doubles</strong> (Dualities governed by the Urim/Light or Thummim/Shadow Anchor Stone), and <strong class="text-gold">12 Simples</strong> (Human faculties &amp; directions).
          </p>
          <div id="codex-letters-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-3">
            <!-- Populated via JS -->
          </div>
        </div>

        <!-- Tab 2: Staves & Frequencies -->
        <div id="codex-rules" class="hidden space-y-6">
          <div>
            <h4 class="font-display text-gold text-base uppercase tracking-wider mb-3">Step II: Egyptian Quadrature Alignments (0–4 Marked Staves)</h4>
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-3 text-sm">
              <div class="p-3.5 rounded-xl bg-obsidian border border-gold/20">
                <span class="font-mono text-gold font-bold">0 Marked — Nun (The Abyss)</span>
                <p class="text-limestone mt-1">Stagnation; the matter has not yet entered form. Wait.</p>
              </div>
              <div class="p-3.5 rounded-xl bg-obsidian border border-gold/20">
                <span class="font-mono text-gold font-bold">1 Marked — Shu (Air/Space)</span>
                <p class="text-limestone mt-1">Initiation; a single spark or fragile beginning requiring protection.</p>
              </div>
              <div class="p-3.5 rounded-xl bg-obsidian border border-gold/20">
                <span class="font-mono text-gold font-bold">2 Marked — Ma'at (Equilibrium)</span>
                <p class="text-limestone mt-1">Balance; opposing forces are equal. The outcome depends entirely on your next action.</p>
              </div>
              <div class="p-3.5 rounded-xl bg-obsidian border border-gold/20">
                <span class="font-mono text-gold font-bold">3 Marked — Ra (Solar Momentum)</span>
                <p class="text-limestone mt-1">Acceleration; strong forward current, high visibility, rapid execution.</p>
              </div>
              <div class="p-3.5 rounded-xl bg-obsidian border border-gold/20 sm:col-span-2">
                <span class="font-mono text-gold font-bold">4 Marked — Atum (Completion)</span>
                <p class="text-limestone mt-1">Saturation; the cycle is peaking or ending. Harvest or pivot immediately.</p>
              </div>
            </div>
          </div>

          <div>
            <h4 class="font-display text-gold text-base uppercase tracking-wider mb-3">Step IV: Gematria Root Frequencies (1–9)</h4>
            <div id="codex-frequencies-grid" class="grid grid-cols-1 sm:grid-cols-3 gap-2.5 text-sm">
              <!-- Populated via JS -->
            </div>
          </div>
        </div>

        <!-- Tab 3: Historical Friction -->
        <div id="codex-history" class="hidden space-y-4 text-lg leading-relaxed">
          <div class="p-5 rounded-xl bg-obsidian border border-gold/30 mb-4">
            <h4 class="font-display text-gold text-base uppercase tracking-wider mb-2">Etymology: Ma'at-Goral (The Balance of the Lot)</h4>
            <p class="text-parchment/90 text-base">
              The title <strong>Ma'at-Goral</strong> merges two foundational pillars of ancient Near Eastern sacred architecture: Egyptian <em>Ma'at</em> (cosmic order, truth, equilibrium, and the weighing of the scales) and Biblical Hebrew <em>Goral</em> (the cast lot or apportioned destiny drawn under divine oversight).
            </p>
          </div>
          <div class="p-5 rounded-xl bg-obsidian border border-crimson/40">
            <h4 class="font-display text-gold text-base uppercase tracking-wider mb-2">Philosophical Tension: Cosmic Determinism vs. Covenantal Free Will</h4>
            <p class="text-parchment/90 mb-3">
              While synthesizing Egyptian, Biblical Hebrew, and Kabbalistic mechanics produces a clean mathematical oracle, <strong>historically these traditions stood in direct opposition regarding the nature of divination.</strong>
            </p>
            <p class="text-limestone text-base mb-3">
              <strong>Ancient Egyptian <em>Heka</em> &amp; Temple Oracles:</strong> Operated on the premise that the cosmos is a unified sympathetic web. By reading omens or manipulating ritual symbols, the practitioner aligns with or influences the netjeru (deities) within the order of <em>Ma'at</em>.
            </p>
            <p class="text-limestone text-base">
              <strong>Biblical Hebrew &amp; Rabbinic Judaism:</strong> Explicitly prohibited <em>kosem</em> (divination) and <em>menachesh</em> (omen-reading) in Deuteronomy 18:10, viewing them as attempts to bypass human moral agency and divine sovereignty. Sanctioned Hebrew lot-casting—such as the High Priest's <em>Urim and Thummim</em> or the biblical <em>Goral</em>—was strictly treated as an administrative binary decision under divine oversight rather than a mystical map of fixed destiny.
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>

  <script>
    // =========================================================================
    // DATA DEFINITIONS: Hebrew Letters (Sefer Yetzirah), Staves, & Frequencies
    // =========================================================================

    const HEBREW_LETTERS = [
      {
        glyph: 'א', name: 'Aleph', value: 1, category: 'Mother',
        elementOrFaculty: 'Element of Air / Breath (Ruach)',
        meaning: 'Primordial unity, silent origin, spiritual breath mediating between heaven and earth. A non-negotiable foundational shift.'
      },
      {
        glyph: 'ב', name: 'Bet', value: 2, category: 'Double',
        elementOrFaculty: 'Duality: Wisdom vs. Folly',
        lightPole: 'Wisdom (Chokhmah) — Building a sacred container, clarity of discernment, constructive shelter.',
        shadowPole: 'Folly (Ivvelet) — Narrow-mindedness, enclosed echo chambers, mistaking the vessel for the essence.'
      },
      {
        glyph: 'ג', name: 'Gimel', value: 3, category: 'Double',
        elementOrFaculty: 'Duality: Wealth vs. Poverty',
        lightPole: 'Wealth (Osher) — Generous flow, nourishment in motion, bridging distance with abundance.',
        shadowPole: 'Poverty (Oni) — Scarcity mindset, withholding resources, isolation from mutual aid.'
      },
      {
        glyph: 'ד', name: 'Dalet', value: 4, category: 'Double',
        elementOrFaculty: 'Duality: Seed / Fertility vs. Desolation',
        lightPole: 'Fertility (Zera) — An open threshold, receptivity, planting seeds that yield generational growth.',
        shadowPole: 'Desolation (Shemamah) — Barrenness, refusal to cross a necessary threshold, stagnation at the door.'
      },
      {
        glyph: 'ה', name: 'He', value: 5, category: 'Simple',
        elementOrFaculty: 'Faculty of Speech & Revelation',
        meaning: 'Window of awareness, breath made audible, expressing inner truth into tangible form.'
      },
      {
        glyph: 'ו', name: 'Vav', value: 6, category: 'Simple',
        elementOrFaculty: 'Faculty of Thought & Connection',
        meaning: 'The hook or nail that binds separate realms; continuity, lineage, and bridging past to future.'
      },
      {
        glyph: 'ז', name: 'Zayin', value: 7, category: 'Simple',
        elementOrFaculty: 'Faculty of Motion & Discernment',
        meaning: 'The crowned sword; decisive cutting away of distraction, rhythmic movement, and focused sustenance.'
      },
      {
        glyph: 'ח', name: 'Chet', value: 8, category: 'Simple',
        elementOrFaculty: 'Faculty of Sight & Boundary',
        meaning: 'Sacred enclosure (Chuppah); protective boundary that incubates life force and transcendent grace.'
      },
      {
        glyph: 'ט', name: 'Tet', value: 9, category: 'Simple',
        elementOrFaculty: 'Faculty of Hearing & Hidden Good',
        meaning: 'Introverted potential; goodness coiled within concealment, requiring deep listening before emergence.'
      },
      {
        glyph: 'י', name: 'Yod', value: 10, category: 'Simple',
        elementOrFaculty: 'Faculty of Action & Craft',
        meaning: 'The metaphysical point of creation; precision, humility, and concentrated seed-power.'
      },
      {
        glyph: 'כ', name: 'Kaf', value: 20, category: 'Double',
        elementOrFaculty: 'Duality: Life vs. Death',
        lightPole: 'Life (Chayyim) — The open palm shaping potential into living reality, crown of vitality.',
        shadowPole: 'Death (Mavet) — Rigid grasping, suppressing vitality, clinging to a form whose time has passed.'
      },
      {
        glyph: 'ל', name: 'Lamed', value: 30, category: 'Simple',
        elementOrFaculty: 'Faculty of Coition / Aspiration',
        meaning: 'The ox-goad and tower soaring upward; continuous learning, teaching, and heart-directed elevation.'
      },
      {
        glyph: 'מ', name: 'Mem', value: 40, category: 'Mother',
        elementOrFaculty: 'Element of Water (Mayim)',
        meaning: 'Deep currents, purification, womb of transformation, and cleansing dissolution of rigid structures.'
      },
      {
        glyph: 'נ', name: 'Nun', value: 50, category: 'Simple',
        elementOrFaculty: 'Faculty of Smell & Faithfulness',
        meaning: 'The seed germinating in darkness; endurance, humility, and rising after a fall.'
      },
      {
        glyph: 'ס', name: 'Samekh', value: 60, category: 'Simple',
        elementOrFaculty: 'Faculty of Sleep & Support',
        meaning: 'The closed circle of divine scaffolding; cyclical protection, trust, and structural reinforcement.'
      },
      {
        glyph: 'ע', name: 'Ayin', value: 70, category: 'Simple',
        elementOrFaculty: 'Faculty of Anger / Deep Perception',
        meaning: 'The eye and the wellspring; looking beneath surface appearances to uncover hidden fountains.'
      },
      {
        glyph: 'פ', name: 'Peh', value: 80, category: 'Double',
        elementOrFaculty: 'Duality: Dominance vs. Subjugation',
        lightPole: 'Dominance (Memshalah) — Sovereign voice, articulate leadership, speaking truth with authority.',
        shadowPole: 'Subjugation (Avdut) — Silenced voice, reactivity, allowing external narratives to dictate agency.'
      },
      {
        glyph: 'צ', name: 'Tzadi', value: 90, category: 'Simple',
        elementOrFaculty: 'Faculty of Taste & Righteousness',
        meaning: 'Alignment with moral and cosmic order (Tzedek); disciplined integrity anchoring high ideals.'
      },
      {
        glyph: 'ק', name: 'Qof', value: 100, category: 'Simple',
        elementOrFaculty: 'Faculty of Laughter & Holiness',
        meaning: 'The back of the head / needle’s eye; discerning authentic holiness from mere imitation in the mundane.'
      },
      {
        glyph: 'ר', name: 'Resh', value: 200, category: 'Double',
        elementOrFaculty: 'Duality: Peace vs. War',
        lightPole: 'Peace (Shalom) — Wholeness, integration of opposites, clear-headed leadership.',
        shadowPole: 'War (Milchamah) — Internal fragmentation, ego-driven conflict, fractured priorities.'
      },
      {
        glyph: 'ש', name: 'Shin', value: 300, category: 'Mother',
        elementOrFaculty: 'Element of Fire (Esh)',
        meaning: 'Three-pronged flame of spirit; rapid purification, catalytic transformation, and consuming truth.'
      },
      {
        glyph: 'ת', name: 'Tav', value: 400, category: 'Double',
        elementOrFaculty: 'Duality: Grace / Truth vs. Ugliness / Distortion',
        lightPole: 'Grace & Truth (Chen / Emet) — The seal of completion, enduring legacy, authentic alignment.',
        shadowPole: 'Distortion (Kiyyur) — Unfinished cycles, superficiality, resisting final accountability.'
      }
    ];

    const EGYPTIAN_ALIGNMENTS = [
      {
        count: 0,
        deity: 'Nun',
        title: 'The Primordial Abyss',
        state: 'Stagnation',
        meaning: 'Stagnation; the matter has not yet entered form. Wait and conserve energy before initiating movement.'
      },
      {
        count: 1,
        deity: 'Shu',
        title: 'Air & Luminous Space',
        state: 'Initiation',
        meaning: 'Initiation; a single spark or fragile beginning requiring careful protection and room to breathe.'
      },
      {
        count: 2,
        deity: "Ma'at",
        title: 'Cosmic Equilibrium',
        state: 'Balance',
        meaning: 'Balance; opposing forces are equal on the scales. The outcome depends entirely on your next conscious action.'
      },
      {
        count: 3,
        deity: 'Ra',
        title: 'Solar Momentum',
        state: 'Acceleration',
        meaning: 'Acceleration; strong forward current, high visibility, and rapid execution are favored.'
      },
      {
        count: 4,
        deity: 'Atum',
        title: 'Solar Completion',
        state: 'Saturation',
        meaning: 'Saturation; the cycle is peaking or reaching fullness. Harvest the results or pivot immediately.'
      }
    ];

    const ROOT_FREQUENCIES = {
      1: { title: 'Unity & Origin', desc: 'Singular focus, undivided will, and returning to the primary source of the matter.' },
      2: { title: 'Duality & Partnership', desc: 'Polarity, reflection, discernment between two paths, and relational calibration.' },
      3: { title: 'Synthesis & Stability', desc: 'Reconciliation of opposites, creative manifestation, and three-fold structural stability.' },
      4: { title: 'Material Structure', desc: 'Boundaries, four corners of manifestation, practical grounding, and disciplined order.' },
      5: { title: 'Disruption & Agency', desc: 'Dynamic movement, breaking rigid symmetry, human choice, and catalytic breath.' },
      6: { title: 'Harmony & Connection', desc: 'Integration, beauty (Tiferet), mutual responsibility, and symmetrical alignment.' },
      7: { title: 'Cycles & Hidden Depth', desc: 'Temporal completion, inner sanctuary, and unseen currents ripening beneath the surface.' },
      8: { title: 'Transcendence & Regeneration', desc: 'Operating beyond natural limits, infinite continuity, and regenerative power.' },
      9: { title: 'Culmination & Truth', desc: 'Full gestation of a cycle, enduring truth (Emet), and the foundation of the next era.' }
    };

    // =========================================================================
    // APPLICATION STATE
    // =========================================================================
    const oracleState = {
      step: 0, // 0 = ready, 1 = stone drawn, 2 = staves dropped, 3 & 4 = letters & gematria complete
      stone: null, // 'urim' | 'thummim'
      staves: [], // array of 4 booleans (true = marked/1, false = blank/0)
      markedCount: 0,
      letters: [], // array of 3 objects from HEBREW_LETTERS (index 0 = Right/Root, 1 = Center/Fulcrum, 2 = Left/Fruit)
      gematria: null // { rawSum, steps, rootDigit }
    };

    // =========================================================================
    // INITIALIZATION
    // =========================================================================
    document.addEventListener('DOMContentLoaded', () => {
      populateCodexModal();
    });

    function showToast(msg) {
      const toast = document.getElementById('toast');
      const toastMsg = document.getElementById('toast-msg');
      toastMsg.textContent = msg;
      toast.classList.remove('translate-y-20', 'opacity-0');
      setTimeout(() => {
        toast.classList.add('translate-y-20', 'opacity-0');
      }, 2800);
    }

    // =========================================================================
    // STEP 1: THE BINARY GATE (URIM & THUMMIM)
    // =========================================================================
    function performStep1() {
      const isUrim = Math.random() < 0.5;
      oracleState.stone = isUrim ? 'urim' : 'thummim';
      oracleState.step = Math.max(oracleState.step, 1);

      const uncastEl = document.getElementById('step-1-uncast');
      const resultEl = document.getElementById('step-1-result');
      uncastEl.classList.add('hidden');
      resultEl.classList.remove('hidden');

      if (isUrim) {
        resultEl.innerHTML = `
          <div class="animate-stone flex flex-col items-center">
            <div class="w-20 h-20 rounded-full bg-gradient-to-br from-white via-parchment to-limestone shadow-[0_0_30px_rgba(243,212,107,0.5)] border-2 border-gold flex items-center justify-center mb-3">
              <span class="font-hebrew text-3xl font-bold text-obsidian">אורים</span>
            </div>
            <span class="font-mono text-xs uppercase tracking-widest text-goldBright">White Stone • Urim ("Lights")</span>
            <h3 class="font-display text-xl font-bold text-parchment mt-1">Expansion &amp; Ma'at</h3>
            <p class="text-sm sm:text-base text-limestone mt-2 leading-snug">
              The query is <strong class="text-parchment">active and affirmed</strong>. Proceed to cast for <em class="text-goldBright">how to move forward</em>. Double letters favor their <strong class="text-goldBright">Light Pole</strong>.
            </p>
          </div>
        `;
      } else {
        resultEl.innerHTML = `
          <div class="animate-stone flex flex-col items-center">
            <div class="w-20 h-20 rounded-full bg-gradient-to-br from-slate-800 via-obsidian to-black shadow-[0_0_25px_rgba(158,42,43,0.45)] border-2 border-crimson flex items-center justify-center mb-3">
              <span class="font-hebrew text-3xl font-bold text-parchment">תמים</span>
            </div>
            <span class="font-mono text-xs uppercase tracking-widest text-rose-400">Black Stone • Thummim ("Completions")</span>
            <h3 class="font-display text-xl font-bold text-parchment mt-1">Contraction &amp; Din</h3>
            <p class="text-sm sm:text-base text-limestone mt-2 leading-snug">
              The query is <strong class="text-parchment">bound or premature</strong>. Proceed to cast for <em class="text-rose-300">what is hidden or must be resolved</em>. Double letters highlight their <strong class="text-rose-300">Shadow Pole</strong>.
            </p>
          </div>
        `;
      }

      // Update Step 1 button
      const btn1 = document.getElementById('btn-step-1');
      btn1.textContent = 'Anchor Stone Drawn ✓';
      btn1.disabled = true;
      btn1.classList.add('opacity-50', 'cursor-default');

      // Unlock Step 2
      unlockStep(2);
      updateProgressUI();

      // If user re-drew or cast all, refresh step 3 if already drawn
      if (oracleState.letters.length === 3) {
        renderStep3Tokens();
        renderSynthesis();
      }
    }

    // =========================================================================
    // STEP 2: THE QUADRATURE DROP (EGYPTIAN STAVES)
    // =========================================================================
    function performStep2() {
      if (oracleState.step < 1) return;

      const staves = Array.from({ length: 4 }, () => Math.random() < 0.5);
      const markedCount = staves.filter(Boolean).length;
      oracleState.staves = staves;
      oracleState.markedCount = markedCount;
      oracleState.step = Math.max(oracleState.step, 2);

      const container = document.getElementById('staves-container');
      container.innerHTML = staves.map((isMarked, idx) => {
        const delay = idx * 90;
        if (isMarked) {
          // Marked side (Value = 1) with Egyptian solar notch & gold pigment
          return `
            <div style="animation-delay: ${delay}ms" class="animate-stave h-28 sm:h-32 rounded-xl bg-gradient-to-b from-[#3b2c1a] via-[#261c10] to-[#1a130b] border-2 border-gold shadow-lg flex flex-col items-center justify-between py-2.5 px-2 relative overflow-hidden">
              <span class="font-mono text-[10px] text-gold/80">STAVE ${idx + 1}</span>
              <!-- Carved Egyptian Pigment Motifs -->
              <div class="flex flex-col items-center gap-1.5 my-auto">
                <span class="w-6 h-1.5 rounded-full bg-gold shadow-[0_0_8px_#d4af37]"></span>
                <span class="w-4 h-4 rotate-45 border-2 border-gold bg-gold/25"></span>
                <span class="w-6 h-1.5 rounded-full bg-gold shadow-[0_0_8px_#d4af37]"></span>
              </div>
              <span class="font-mono text-xs font-bold text-goldBright">MARKED (1)</span>
            </div>
          `;
        } else {
          // Blank side (Value = 0)
          return `
            <div style="animation-delay: ${delay}ms" class="animate-stave h-28 sm:h-32 rounded-xl bg-gradient-to-b from-lapisLight to-obsidian border border-limestone/25 shadow-inner flex flex-col items-center justify-between py-2.5 px-2">
              <span class="font-mono text-[10px] text-limestone/50">STAVE ${idx + 1}</span>
              <div class="w-1 h-10 rounded-full bg-white/5 my-auto"></div>
              <span class="font-mono text-xs text-limestone/60">BLANK (0)</span>
            </div>
          `;
        }
      }).join('');

      const alignment = EGYPTIAN_ALIGNMENTS[markedCount];
      document.getElementById('stave-counter-badge').textContent = `${markedCount} of 4 Marked`;
      document.getElementById('step-2-result').innerHTML = `
        <div class="space-y-1">
          <div class="flex items-center justify-center gap-2">
            <span class="font-mono text-xs px-2 py-0.5 rounded bg-gold/20 text-goldBright font-bold">${markedCount} Marked</span>
            <h3 class="font-display text-lg font-bold text-gold">${alignment.deity} — ${alignment.title}</h3>
          </div>
          <p class="text-sm sm:text-base text-parchment/90">${alignment.meaning}</p>
        </div>
      `;

      const btn2 = document.getElementById('btn-step-2');
      btn2.textContent = 'Staves Weighed ✓';
      btn2.disabled = true;
      btn2.classList.add('opacity-50', 'cursor-default');

      unlockStep(3);
      updateProgressUI();
    }

    // =========================================================================
    // STEP 3 & 4: THE TRIADIC DRAW & GEMATRIA REDUCTION
    // =========================================================================
    function performStep3() {
      if (oracleState.step < 2) return;

      // Fisher-Yates shuffle copy of HEBREW_LETTERS to draw 3 unique tokens
      const pool = [...HEBREW_LETTERS];
      for (let i = pool.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [pool[i], pool[j]] = [pool[j], pool[i]];
      }
      oracleState.letters = pool.slice(0, 3);
      oracleState.step = 4;

      renderStep3Tokens();
      computeAndRenderStep4();
      renderSynthesis();

      const btn3 = document.getElementById('btn-step-3');
      btn3.textContent = 'Triadic Tokens Drawn ✓';
      btn3.disabled = true;
      btn3.classList.add('opacity-50', 'cursor-default');

      unlockStep(4);
      updateProgressUI();
    }

    function renderStep3Tokens() {
      const positions = [
        { idx: 0, label: 'Right Position (1st)', role: 'The Root', sub: 'Past cause or foundational reality' },
        { idx: 1, label: 'Center Position (2nd)', role: 'The Fulcrum', sub: 'Present tension or active mechanism' },
        { idx: 2, label: 'Left Position (3rd)', role: 'The Fruit', sub: 'Trajectory if current pattern holds' }
      ];

      const isUrim = oracleState.stone === 'urim';

      positions.forEach((pos) => {
        const letter = oracleState.letters[pos.idx];
        const slotEl = document.getElementById(`token-slot-${pos.idx}`);
        slotEl.className = 'animate-token rounded-xl bg-gradient-to-b from-lapisLight/90 to-obsidian border border-gold/45 p-5 flex flex-col justify-between shadow-xl';
        slotEl.style.animationDelay = `${pos.idx * 140}ms`;

        let categoryBadgeColor = 'bg-turquoise/20 text-teal-300 border-turquoise/40';
        if (letter.category === 'Mother') categoryBadgeColor = 'bg-gold/20 text-goldBright border-gold/50';
        if (letter.category === 'Double') categoryBadgeColor = 'bg-purple-900/40 text-purple-200 border-purple-400/40';

        let interpretationHtml = '';
        if (letter.category === 'Double') {
          interpretationHtml = `
            <div class="mt-3 pt-3 border-t border-white/10 text-left space-y-2 text-xs sm:text-sm">
              <p class="font-mono text-[11px] text-limestone">${letter.elementOrFaculty}</p>
              <div class="p-2.5 rounded-lg ${isUrim ? 'bg-gold/15 border border-gold/50 text-parchment' : 'bg-white/5 border border-white/10 text-limestone/60'}">
                <span class="font-mono text-[10px] uppercase tracking-wider ${isUrim ? 'text-goldBright font-bold' : ''}">
                  ${isUrim ? '★ Active Light Pole (Urim):' : 'Light Pole:'}
                </span>
                <p class="mt-0.5 leading-snug">${letter.lightPole}</p>
              </div>
              <div class="p-2.5 rounded-lg ${!isUrim ? 'bg-crimson/20 border border-crimson/60 text-parchment' : 'bg-white/5 border border-white/10 text-limestone/60'}">
                <span class="font-mono text-[10px] uppercase tracking-wider ${!isUrim ? 'text-rose-300 font-bold' : ''}">
                  ${!isUrim ? '★ Active Shadow Pole (Thummim):' : 'Shadow Pole:'}
                </span>
                <p class="mt-0.5 leading-snug">${letter.shadowPole}</p>
              </div>
            </div>
          `;
        } else {
          interpretationHtml = `
            <div class="mt-3 pt-3 border-t border-white/10 text-left space-y-1.5">
              <p class="font-mono text-[11px] text-gold/90">${letter.elementOrFaculty}</p>
              <p class="text-sm sm:text-base text-parchment/90 leading-snug">${letter.meaning}</p>
            </div>
          `;
        }

        slotEl.innerHTML = `
          <div>
            <div class="flex items-center justify-between text-[11px] font-mono text-limestone/80 mb-2">
              <span>${pos.label}</span>
              <span class="text-gold font-semibold">Val: ${letter.value}</span>
            </div>
            <div class="text-center pb-2">
              <span class="font-display text-xs uppercase tracking-widest text-gold">${pos.role}</span>
              <p class="text-xs text-limestone/70 italic">${pos.sub}</p>
            </div>

            <!-- Hebrew Glyph Medallion -->
            <div class="my-3 mx-auto w-20 h-20 rounded-2xl bg-obsidian border border-gold/40 flex flex-col items-center justify-center shadow-inner">
              <span class="font-hebrew text-4xl font-bold text-goldBright leading-none">${letter.glyph}</span>
              <span class="font-display text-xs text-parchment mt-1">${letter.name}</span>
            </div>

            <div class="flex justify-center">
              <span class="font-mono text-[11px] px-2.5 py-0.5 rounded-full border ${categoryBadgeColor}">
                ${letter.category} Letter
              </span>
            </div>
          </div>
          ${interpretationHtml}
        `;
      });
    }

    function computeAndRenderStep4() {
      const [rootL, fulcrumL, fruitL] = oracleState.letters;
      const rawSum = rootL.value + fulcrumL.value + fruitL.value;

      // Recursive addition reduction (1-9)
      const reductionSteps = [];
      let current = rawSum;
      while (current > 9) {
        const digits = String(current).split('').map(Number);
        const nextSum = digits.reduce((a, b) => a + b, 0);
        reductionSteps.push(`${digits.join(' + ')} = ${nextSum}`);
        current = nextSum;
      }

      oracleState.gematria = {
        rawSum,
        steps: reductionSteps,
        rootDigit: current
      };

      const freq = ROOT_FREQUENCIES[current];
      const chainText = reductionSteps.length > 0
        ? `${rawSum} → ${reductionSteps.join(' → ')}`
        : `${rawSum} (Already a single root digit)`;

      document.getElementById('step-4-content').innerHTML = `
        <div class="flex flex-col md:flex-row items-center justify-between gap-6 text-left">
          <div class="space-y-2 flex-1">
            <div class="font-mono text-xs sm:text-sm text-limestone">
              <span class="text-parchment">${rootL.name} (${rootL.value})</span> +
              <span class="text-parchment">${fulcrumL.name} (${fulcrumL.value})</span> +
              <span class="text-parchment">${fruitL.name} (${fruitL.value})</span> =
              <strong class="text-goldBright">${rawSum}</strong>
            </div>
            <div class="inline-block px-3.5 py-2 rounded-lg bg-lapis border border-gold/30 font-mono text-xs sm:text-sm text-gold">
              Reduction Path: ${chainText}
            </div>
            <div class="pt-2">
              <h3 class="font-display text-xl font-bold text-parchment">
                Root Frequency ${current}: <span class="text-gold">${freq.title}</span>
              </h3>
              <p class="text-base sm:text-lg text-limestone mt-1">${freq.desc}</p>
            </div>
          </div>

          <!-- Large Root Digit Seal -->
          <div class="w-24 h-24 rounded-2xl bg-gradient-to-br from-gold/25 to-obsidian border-2 border-gold flex flex-col items-center justify-center shrink-0 shadow-[0_0_25px_rgba(212,175,55,0.2)]">
            <span class="font-mono text-[10px] uppercase tracking-widest text-gold">Frequency</span>
            <span class="font-display text-4xl font-bold text-goldBright">${current}</span>
          </div>
        </div>
      `;
    }

    // =========================================================================
    // SYNTHESIS & READING LOG
    // =========================================================================
    function renderSynthesis() {
      const section = document.getElementById('synthesis-section');
      const body = document.getElementById('synthesis-body');
      section.classList.remove('hidden');

      const queryText = document.getElementById('query-input').value.trim();
      const isUrim = oracleState.stone === 'urim';
      const alignment = EGYPTIAN_ALIGNMENTS[oracleState.markedCount];
      const [rootL, fulcrumL, fruitL] = oracleState.letters;
      const { rawSum, steps, rootDigit } = oracleState.gematria;
      const freq = ROOT_FREQUENCIES[rootDigit];

      const formatLetterSummary = (l) => {
        if (l.category === 'Double') {
          const activeText = isUrim ? l.lightPole : l.shadowPole;
          return `<strong>${l.name} (${l.glyph}, ${l.value})</strong> [Double — ${isUrim ? 'Light/Urim' : 'Shadow/Thummim'} Pole active]: ${activeText}`;
        }
        return `<strong>${l.name} (${l.glyph}, ${l.value})</strong> [${l.category} — ${l.elementOrFaculty}]: ${l.meaning}`;
      };

      body.innerHTML = `
        ${queryText ? `
          <div class="p-4 rounded-xl bg-obsidian/80 border-l-4 border-gold">
            <span class="font-mono text-xs uppercase tracking-wider text-gold block mb-1">Inquired Matter</span>
            <p class="italic text-parchment text-lg">"${escapeHtml(queryText)}"</p>
          </div>
        ` : ''}

        <p>
          <strong class="text-gold">1. The Binary Gate (${isUrim ? 'Urim — White Stone' : 'Thummim — Black Stone'}):</strong>
          ${isUrim
            ? 'The vessel yielded the White Stone of <em>Urim</em> ("Lights"), signaling expansion, affirmation, and <em>Ma\'at</em>. Your query is active; read the following signs as guidance for how to move forward.'
            : 'The vessel yielded the Black Stone of <em>Thummim</em> ("Completions"), signaling contraction, boundary, and <em>Din</em>. Your query is currently bound or premature; read the following signs to uncover what is hidden or must be resolved before acting.'}
        </p>

        <p>
          <strong class="text-gold">2. The Quadrature Drop (${oracleState.markedCount}/4 Marked Staves — ${alignment.deity}):</strong>
          The casting sticks fell into the alignment of <strong>${alignment.deity} (${alignment.title})</strong>. ${alignment.meaning}
        </p>

        <div class="p-4 rounded-xl bg-obsidian/60 border border-gold/20 space-y-2.5">
          <strong class="text-gold block font-display text-sm uppercase tracking-wider">3. The Triadic Path (Read Right → Left)</strong>
          <ul class="space-y-2 text-base">
            <li><span class="font-mono text-xs text-gold uppercase">[Right • The Root]</span> ${formatLetterSummary(rootL)}</li>
            <li><span class="font-mono text-xs text-gold uppercase">[Center • The Fulcrum]</span> ${formatLetterSummary(fulcrumL)}</li>
            <li><span class="font-mono text-xs text-gold uppercase">[Left • The Fruit]</span> ${formatLetterSummary(fruitL)}</li>
          </ul>
        </div>

        <p>
          <strong class="text-gold">4. Gematria Root Frequency (${rawSum}${steps.length ? ' → ' + rootDigit : ''} — ${freq.title}):</strong>
          The combined numerical weight of ${rootL.name} (${rootL.value}) + ${fulcrumL.name} (${fulcrumL.value}) + ${fruitL.name} (${fruitL.value}) equals <strong>${rawSum}</strong>, reducing to Root Frequency <strong>${rootDigit} (${freq.title})</strong>: ${freq.desc}
        </p>
      `;
    }

    function copyReadingToClipboard() {
      const queryText = document.getElementById('query-input').value.trim();
      const isUrim = oracleState.stone === 'urim';
      const alignment = EGYPTIAN_ALIGNMENTS[oracleState.markedCount];
      const [rootL, fulcrumL, fruitL] = oracleState.letters;
      const { rawSum, steps, rootDigit } = oracleState.gematria;
      const freq = ROOT_FREQUENCIES[rootDigit];

      const lines = [
        '=== MA\'AT-GORAL — THE BALANCE OF THE LOT ===',
        queryText ? `Query: "${queryText}"` : 'Query: (Unspoken / General Alignment)',
        '',
        `1. BINARY GATE: ${isUrim ? 'White Stone — Urim ("Lights" / Expansion / Ma\'at)' : 'Black Stone — Thummim ("Completions" / Contraction / Din)'}`,
        `2. QUADRATURE DROP: ${oracleState.markedCount}/4 Marked Staves — ${alignment.deity} (${alignment.title}): ${alignment.meaning}`,
        '3. TRIADIC DRAW (Right -> Left):',
        `   - [Right / Root]: ${rootL.name} (${rootL.glyph}, ${rootL.value}) [${rootL.category}] — ${rootL.category === 'Double' ? (isUrim ? rootL.lightPole : rootL.shadowPole) : rootL.meaning}`,
        `   - [Center / Fulcrum]: ${fulcrumL.name} (${fulcrumL.glyph}, ${fulcrumL.value}) [${fulcrumL.category}] — ${fulcrumL.category === 'Double' ? (isUrim ? fulcrumL.lightPole : fulcrumL.shadowPole) : fulcrumL.meaning}`,
        `   - [Left / Fruit]: ${fruitL.name} (${fruitL.glyph}, ${fruitL.value}) [${fruitL.category}] — ${fruitL.category === 'Double' ? (isUrim ? fruitL.lightPole : fruitL.shadowPole) : fruitL.meaning}`,
        `4. GEMATRIA REDUCTION: ${rawSum}${steps.length ? ' -> ' + steps.join(' -> ') : ''} -> Root Frequency ${rootDigit} (${freq.title}): ${freq.desc}`
      ];

      const textToCopy = lines.join('\n');
      const tempArea = document.createElement('textarea');
      tempArea.value = textToCopy;
      tempArea.style.position = 'fixed';
      tempArea.style.left = '-9999px';
      document.body.appendChild(tempArea);
      tempArea.select();
      try {
        document.execCommand('copy');
        showToast('Ma\'at-Goral reading copied to clipboard.');
      } catch (err) {
        showToast('Unable to copy reading.');
      }
      document.body.removeChild(tempArea);
    }

    // =========================================================================
    // MASTER CONTROLS: CAST ALL & RESET
    // =========================================================================
    function castAllSteps() {
      resetCast(true);
      performStep1();
      setTimeout(() => {
        performStep2();
        setTimeout(() => {
          performStep3();
          showToast('Complete 4-step Ma\'at-Goral cast completed.');
        }, 180);
      }, 180);
    }

    function resetCast(silent = false) {
      oracleState.step = 0;
      oracleState.stone = null;
      oracleState.staves = [];
      oracleState.markedCount = 0;
      oracleState.letters = [];
      oracleState.gematria = null;

      // Reset Step 1
      document.getElementById('step-1-uncast').classList.remove('hidden');
      const res1 = document.getElementById('step-1-result');
      res1.classList.add('hidden');
      res1.innerHTML = '';
      const btn1 = document.getElementById('btn-step-1');
      btn1.textContent = 'Draw Anchor Stone from Vessel';
      btn1.disabled = false;
      btn1.classList.remove('opacity-50', 'cursor-default');

      // Reset Step 2
      const card2 = document.getElementById('card-step-2');
      card2.classList.add('opacity-75', 'border-white/10');
      card2.classList.remove('border-gold/30', 'gold-border-glow');
      document.getElementById('stave-counter-badge').textContent = '4 Staves • 0–4 Scale';
      document.getElementById('staves-container').innerHTML = ['I', 'II', 'III', 'IV'].map(num => `
        <div class="h-28 rounded-lg border border-dashed border-gold/25 bg-lapis/40 flex flex-col items-center justify-center text-limestone/40 font-mono text-xs">
          <span>STAVE ${num}</span>
        </div>
      `).join('');
      document.getElementById('step-2-result').innerHTML = `
        <p class="text-limestone/70 text-base italic">
          Complete Step I first, then cast the four two-sided staves to weigh the energetic momentum.
        </p>
      `;
      const btn2 = document.getElementById('btn-step-2');
      btn2.textContent = 'Cast Four Egyptian Staves';
      btn2.disabled = true;
      btn2.classList.remove('opacity-50', 'cursor-default');

      // Reset Step 3
      const card3 = document.getElementById('card-step-3');
      card3.classList.add('opacity-75', 'border-white/10');
      card3.classList.remove('border-gold/30', 'gold-border-glow');
      const defaultSlots = [
        { id: 2, label: 'Left Position (3rd Drawn)', title: 'The Fruit', desc: 'Trajectory & outcome if the current pattern holds.' },
        { id: 1, label: 'Center Position (2nd Drawn)', title: 'The Fulcrum', desc: 'Present tension, active mechanism, or pivot point.' },
        { id: 0, label: 'Right Position (1st Drawn)', title: 'The Root', desc: 'Past cause, origin, or foundational reality.' }
      ];
      defaultSlots.forEach(s => {
        const el = document.getElementById(`token-slot-${s.id}`);
        el.className = 'rounded-xl bg-obsidian/70 border border-dashed border-gold/25 p-5 min-h-[260px] flex flex-col items-center justify-center text-center';
        el.innerHTML = `
          <span class="font-mono text-[11px] uppercase tracking-widest text-limestone/60 mb-1">${s.label}</span>
          <h3 class="font-display text-base text-gold/80 mb-2">${s.title}</h3>
          <p class="text-sm text-limestone/60 max-w-[220px]">${s.desc}</p>
        `;
      });
      const btn3 = document.getElementById('btn-step-3');
      btn3.textContent = 'Draw 3 Letter Tokens (Right → Left)';
      btn3.disabled = true;
      btn3.classList.remove('opacity-50', 'cursor-default');

      // Reset Step 4 & Synthesis
      const card4 = document.getElementById('card-step-4');
      card4.classList.add('opacity-75', 'border-white/10');
      card4.classList.remove('border-gold/30', 'gold-border-glow');
      document.getElementById('step-4-content').innerHTML = `
        <p class="text-limestone/70 text-base italic">
          Automatically calculates once the three Hebrew Letter Tokens are drawn in Step III.
        </p>
      `;
      document.getElementById('synthesis-section').classList.add('hidden');

      updateProgressUI();
      if (!silent) showToast('Vessel cleared for a new cast.');
    }

    function unlockStep(stepNum) {
      const card = document.getElementById(`card-step-${stepNum}`);
      if (card) {
        card.classList.remove('opacity-75', 'border-white/10');
        card.classList.add('border-gold/30', 'gold-border-glow');
      }
      const btn = document.getElementById(`btn-step-${stepNum}`);
      if (btn) {
        btn.disabled = false;
      }
    }

    function updateProgressUI() {
      for (let i = 1; i <= 4; i++) {
        const el = document.getElementById(`prog-${i}`);
        const isActive = oracleState.step >= i - 1;
        const isDone = oracleState.step >= i;
        if (isDone) {
          el.className = 'flex items-center gap-2 px-3 py-1.5 rounded-lg bg-gold/15 border border-gold/50 text-goldBright';
        } else if (isActive) {
          el.className = 'flex items-center gap-2 px-3 py-1.5 rounded-lg bg-obsidian/80 border border-gold/30 text-gold';
        } else {
          el.className = 'flex items-center gap-2 px-3 py-1.5 rounded-lg bg-obsidian/40 border border-white/10 text-limestone/50';
        }
      }
    }

    // =========================================================================
    // REFERENCE MODAL & HELPERS
    // =========================================================================
    function toggleReferenceModal(show) {
      const modal = document.getElementById('reference-modal');
      if (show) {
        modal.classList.remove('hidden');
      } else {
        modal.classList.add('hidden');
      }
    }

    function switchCodexTab(tabName) {
      ['letters', 'rules', 'history'].forEach(t => {
        document.getElementById(`codex-${t}`).classList.toggle('hidden', t !== tabName);
        const btn = document.getElementById(`tab-${t}`);
        if (t === tabName) {
          btn.classList.add('border-gold', 'text-gold');
          btn.classList.remove('border-transparent', 'text-limestone');
        } else {
          btn.classList.remove('border-gold', 'text-gold');
          btn.classList.add('border-transparent', 'text-limestone');
        }
      });
    }

    function populateCodexModal() {
      const lettersGrid = document.getElementById('codex-letters-grid');
      lettersGrid.innerHTML = HEBREW_LETTERS.map(l => `
        <div class="p-3 rounded-xl bg-obsidian border border-gold/20 flex items-start gap-3">
          <div class="w-11 h-11 rounded-lg bg-lapis border border-gold/30 flex items-center justify-center shrink-0">
            <span class="font-hebrew text-2xl font-bold text-goldBright">${l.glyph}</span>
          </div>
          <div class="min-w-0 flex-1">
            <div class="flex items-center justify-between">
              <span class="font-display text-sm font-bold text-parchment">${l.name}</span>
              <span class="font-mono text-xs text-gold">${l.value}</span>
            </div>
            <span class="font-mono text-[10px] uppercase tracking-wider text-limestone/80 block">${l.category} • ${l.elementOrFaculty}</span>
            <p class="text-xs text-limestone mt-1 leading-snug">
              ${l.category === 'Double' ? `${l.lightPole} / ${l.shadowPole}` : l.meaning}
            </p>
          </div>
        </div>
      `).join('');

      const freqGrid = document.getElementById('codex-frequencies-grid');
      freqGrid.innerHTML = Object.entries(ROOT_FREQUENCIES).map(([num, data]) => `
        <div class="p-3 rounded-xl bg-obsidian border border-gold/20">
          <span class="font-mono text-xs text-gold font-bold">${num} — ${data.title}</span>
          <p class="text-xs text-limestone mt-1">${data.desc}</p>
        </div>
      `).join('');
    }

    function escapeHtml(str) {
      return str.replace(/[&<>"']/g, m => ({
        '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;'
      }[m]));
    }
  </script>
</body>
</html>
