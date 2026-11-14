<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="theme-color" content="#050810">
  <title>VYOMA — Experience Beyond Boundaries</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,opsz,wght@0,9..40,400;0,9..40,500;0,9..40,600;0,9..40,700;1,9..40,400&family=Space+Grotesk:wght@400;500;600;700&display=swap" rel="stylesheet">
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            void: '#050810',
            midnight: '#070a12',
            navy: '#0c1524',
            graphite: '#111b2e',
            cyan: {
              electric: '#73e3ed',
              ice: '#a5e6ff',
              deep: '#1b4965'
            }
          },
          fontFamily: {
            sans: ['"DM Sans"', 'sans-serif'],
            display: ['"Space Grotesk"', 'sans-serif']
          }
        }
      }
    }
  </script>
  <style>
    :root {
      --bg-void: #050810;
      --bg-midnight: #070a12;
      --bg-navy: #0c1524;
      --cyan-electric: #73e3ed;
      --cyan-ice: #a5e6ff;
      --border-subtle: rgba(255, 255, 255, 0.1);
    }

    * {
      box-sizing: border-box;
    }

    html {
      scroll-padding-top: 84px;
      background-color: var(--bg-void);
      color: #f4f7fb;
    }

    body {
      background:
        radial-gradient(ellipse 80% 50% at 75% -10%, rgba(27, 73, 101, 0.35), transparent 65%),
        radial-gradient(ellipse 60% 40% at 10% 35%, rgba(115, 227, 237, 0.06), transparent 60%),
        var(--bg-void);
      overflow-x: hidden;
    }

    /* Architectural grid overlay */
    .arch-grid {
      background-image:
        linear-gradient(to right, rgba(165, 230, 255, 0.04) 1px, transparent 1px),
        linear-gradient(to bottom, rgba(165, 230, 255, 0.04) 1px, transparent 1px);
      background-size: 48px 48px;
    }

    /* Selective glassmorphism */
    .glass-panel {
      background: rgba(12, 21, 36, 0.68);
      backdrop-filter: blur(18px);
      -webkit-backdrop-filter: blur(18px);
      border: 1px solid rgba(255, 255, 255, 0.11);
    }

    .glass-card {
      background: linear-gradient(145deg, rgba(17, 27, 46, 0.85), rgba(9, 15, 26, 0.92));
      border: 1px solid rgba(255, 255, 255, 0.09);
      transition: transform 0.35s cubic-bezier(0.22, 1, 0.36, 1), border-color 0.35s ease, box-shadow 0.35s ease;
    }

    .glass-card:hover {
      border-color: rgba(115, 227, 237, 0.4);
      transform: translateY(-4px);
      box-shadow: 0 20px 45px -15px rgba(0, 0, 0, 0.7), 0 0 25px -10px rgba(115, 227, 237, 0.18);
    }

    .text-gradient {
      background: linear-gradient(115deg, #ffffff 10%, #a5e6ff 55%, #73e3ed 95%);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
    }

    /* Scroll reveal animations */
    .reveal {
      opacity: 0;
      transform: translateY(22px);
      transition: opacity 0.75s cubic-bezier(0.22, 1, 0.36, 1), transform 0.75s cubic-bezier(0.22, 1, 0.36, 1);
    }

    .reveal.visible {
      opacity: 1;
      transform: translateY(0);
    }

    /* Custom range slider */
    input[type="range"].vyoma-slider {
      -webkit-appearance: none;
      appearance: none;
      background: rgba(255, 255, 255, 0.14);
      height: 4px;
      border-radius: 999px;
    }

    input[type="range"].vyoma-slider::-webkit-slider-thumb {
      -webkit-appearance: none;
      appearance: none;
      width: 18px;
      height: 18px;
      border-radius: 50%;
      background: #73e3ed;
      cursor: pointer;
      box-shadow: 0 0 12px rgba(115, 227, 237, 0.65);
      border: 2px solid #050810;
    }

    /* 360 Panorama Viewport drag cursor */
    .pano-stage {
      cursor: grab;
      user-select: none;
      touch-action: pan-y;
    }
    .pano-stage:active {
      cursor: grabbing;
    }

    /* Subtle pulse for spatial hotspots */
    @keyframes hotspotPulse {
      0%, 100% { box-shadow: 0 0 0 0 rgba(115, 227, 237, 0.6); }
      50% { box-shadow: 0 0 0 10px rgba(115, 227, 237, 0); }
    }
    .hotspot-dot {
      animation: hotspotPulse 2.6s infinite;
    }

    /* Pipeline animated flow line */
    @keyframes flowDash {
      to { stroke-dashoffset: -24; }
    }
    .pipeline-flow {
      stroke-dasharray: 6 6;
      animation: flowDash 1.4s linear infinite;
    }

    /* 3D Projected CAD Callout Pins */
    .cad-pin {
      position: absolute;
      transform: translate(-50%, -50%);
      pointer-events: none;
      transition: opacity 0.2s ease;
      z-index: 15;
    }

    /* Split Curtain Handle */
    .curtain-handle {
      cursor: ew-resize;
      touch-action: none;
      user-select: none;
    }

    /* Print Stylesheet for Project Brief Card */
    @media print {
      body * {
        visibility: hidden;
      }
      #briefPreviewBox, #briefPreviewBox * {
        visibility: visible;
      }
      #briefPreviewBox {
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
        background: #ffffff !important;
        color: #050810 !important;
        border: 2px solid #050810 !important;
        padding: 24px !important;
      }
    }

    @media (prefers-reduced-motion: reduce) {
      html { scroll-behavior: auto !important; }
      .reveal { opacity: 1 !important; transform: none !important; transition: none !important; }
      .hotspot-dot, .pipeline-flow { animation: none !important; }
      .glass-card { transition: none !important; }
    }
  </style>
</head>
<body class="font-sans antialiased text-slate-100 selection:bg-cyan-electric selection:text-void">

  <!-- Global ARIA Live Region for Screen Reader Announcements -->
  <div id="vyomaAriaLive" class="sr-only" aria-live="polite" aria-atomic="true"></div>

  <!-- 1. STICKY GLASSMORPHIC NAVIGATION -->
  <header class="fixed top-0 inset-x-0 z-50 glass-panel border-b border-white/10">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
      <a href="#hero" class="flex items-center gap-3 group focus:outline-none focus-visible:ring-2 focus-visible:ring-cyan-electric rounded-lg px-1">
        <span class="w-8 h-8 rounded-lg border border-cyan-electric/40 bg-cyan-electric/10 flex items-center justify-center text-cyan-electric font-display font-bold text-sm group-hover:bg-cyan-electric group-hover:text-void transition-colors">V</span>
        <span class="font-display font-bold text-xl tracking-[0.22em] text-white">VY<span class="text-cyan-electric">O</span>MA</span>
      </a>

      <!-- Desktop Navigation -->
      <nav aria-label="Primary Navigation" class="hidden lg:flex items-center gap-7 text-xs font-medium tracking-wider uppercase text-slate-300">
        <a href="#transformation" class="hover:text-cyan-electric transition-colors">Transformation</a>
        <a href="#explorer-3d" class="hover:text-cyan-electric transition-colors">3D Residence</a>
        <a href="#experience-levels" class="hover:text-cyan-electric transition-colors">4 Levels</a>
        <a href="#industries" class="hover:text-cyan-electric transition-colors">Industries</a>
        <a href="#showroom" class="hover:text-cyan-electric transition-colors">Showroom</a>
        <a href="#studio" class="hover:text-cyan-electric transition-colors">Studio</a>
        <a href="#pipeline" class="hover:text-cyan-electric transition-colors">Pipeline</a>
        <a href="#commercial" class="hover:text-cyan-electric transition-colors">Model</a>
      </nav>

      <div class="hidden sm:flex items-center gap-3">
        <a href="#explorer-3d" class="px-4 py-2.5 rounded-full text-xs font-semibold tracking-wider uppercase border border-cyan-electric/40 text-cyan-ice hover:bg-cyan-electric/10 transition-colors">
          Launch 3D Space
        </a>
        <a href="#enquiry" class="px-5 py-2.5 rounded-full text-xs font-bold tracking-wider uppercase bg-gradient-to-r from-cyan-electric to-cyan-ice text-void hover:opacity-95 transition-opacity">
          Project Brief
        </a>
      </div>

      <!-- Mobile Menu Trigger -->
      <button id="mobileMenuBtn" type="button" aria-expanded="false" aria-controls="mobileDrawer" aria-label="Toggle Navigation Menu" class="lg:hidden p-2.5 rounded-xl border border-white/15 text-slate-200 hover:border-cyan-electric/50">
        <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24">
          <path id="menuIconOpen" stroke-linecap="round" stroke-linejoin="round" d="M4 7h16M4 12h16M4 17h16"/>
          <path id="menuIconClose" class="hidden" stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12"/>
        </svg>
      </button>
    </div>

    <!-- Mobile Navigation Drawer -->
    <div id="mobileDrawer" class="hidden lg:hidden glass-panel border-t border-white/10 px-6 py-6 space-y-4">
      <div class="grid grid-cols-2 gap-3 text-xs font-semibold tracking-wider uppercase text-slate-300">
        <a href="#transformation" class="py-2 hover:text-cyan-electric mobile-nav-link">Transformation</a>
        <a href="#explorer-3d" class="py-2 hover:text-cyan-electric mobile-nav-link">3D Residence</a>
        <a href="#experience-levels" class="py-2 hover:text-cyan-electric mobile-nav-link">4 Experience Levels</a>
        <a href="#industries" class="py-2 hover:text-cyan-electric mobile-nav-link">12 Industries</a>
        <a href="#solutions" class="py-2 hover:text-cyan-electric mobile-nav-link">Solutions</a>
        <a href="#showroom" class="py-2 hover:text-cyan-electric mobile-nav-link">Virtual Showroom</a>
        <a href="#studio" class="py-2 hover:text-cyan-electric mobile-nav-link">Design Studio</a>
        <a href="#pipeline" class="py-2 hover:text-cyan-electric mobile-nav-link">Tech Pipeline</a>
        <a href="#commercial" class="py-2 hover:text-cyan-electric mobile-nav-link">Commercial Model</a>
        <a href="#roadmap" class="py-2 hover:text-cyan-electric mobile-nav-link">Roadmap</a>
      </div>
      <div class="pt-3 border-t border-white/10 flex flex-col sm:flex-row gap-3">
        <a href="#explorer-3d" class="mobile-nav-link text-center py-3 rounded-full text-xs font-semibold uppercase tracking-wider border border-cyan-electric/40 text-cyan-ice">Explore 3D Residence</a>
        <a href="#enquiry" class="mobile-nav-link text-center py-3 rounded-full text-xs font-bold uppercase tracking-wider bg-cyan-electric text-void">Configure Project Brief</a>
      </div>
    </div>
  </header>

  <main>
    <!-- 2. HERO SECTION — THE FIRST IMPRESSION -->
    <section id="hero" class="relative min-h-screen pt-28 pb-16 flex items-center arch-grid overflow-hidden">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 w-full">
        <div class="grid lg:grid-cols-12 gap-10 lg:gap-8 items-center">
          <!-- Left Editorial Column -->
          <div class="lg:col-span-6 space-y-7 z-10">
            <div class="inline-flex items-center gap-2.5 px-3.5 py-1.5 rounded-full border border-cyan-electric/30 bg-cyan-electric/10 text-cyan-ice text-[11px] font-semibold tracking-[0.2em] uppercase">
              <span class="w-2 h-2 rounded-full bg-cyan-electric"></span>
              Spatial Visualisation Venture • Experience Beyond Boundaries
            </div>

            <h1 class="font-display font-bold text-4xl sm:text-5xl xl:text-[3.75rem] leading-[1.03] tracking-tight text-white">
              WHAT IF YOU COULD <span class="text-gradient block mt-1">WALK INTO A HOME</span> BEFORE IT EXISTS?
            </h1>

            <p class="text-lg sm:text-xl text-slate-300 font-normal leading-relaxed max-w-xl">
              Turning architectural imagination into immersive reality. Don't just show the space—let clients, buyers, and stakeholders experience its true scale, light, and flow before a single brick is laid.
            </p>

            <div class="flex flex-wrap items-center gap-4 pt-1">
              <a href="#explorer-3d" class="px-7 py-4 rounded-full bg-gradient-to-r from-cyan-electric to-cyan-ice text-void font-display font-bold text-xs tracking-[0.16em] uppercase shadow-lg shadow-cyan-electric/20 hover:scale-[1.02] transition-transform">
                EXPERIENCE VYOMA →
              </a>
              <a href="#transformation" class="px-7 py-4 rounded-full border border-white/20 bg-white/5 hover:border-cyan-electric/60 text-white font-display font-semibold text-xs tracking-[0.16em] uppercase transition-colors">
                EXPLORE OUR TECHNOLOGY
              </a>
            </div>

            <!-- Credible Architectural Value Pillars (No fake stats) -->
            <div class="grid grid-cols-3 gap-4 pt-6 border-t border-white/10 max-w-lg">
              <div>
                <div class="font-display font-bold text-xl sm:text-2xl text-white">1:1 Scale</div>
                <div class="text-xs text-slate-400 mt-0.5">True human proportion</div>
              </div>
              <div>
                <div class="font-display font-bold text-xl sm:text-2xl text-cyan-electric">Levels 01–04</div>
                <div class="text-xs text-slate-400 mt-0.5">360° to Mixed Reality</div>
              </div>
              <div>
                <div class="font-display font-bold text-xl sm:text-2xl text-white">CAD → VR</div>
                <div class="text-xs text-slate-400 mt-0.5">Plan-to-space pipeline</div>
              </div>
            </div>
          </div>

          <!-- Right Interactive 3D Architectural Stage -->
          <div class="lg:col-span-6 relative" id="heroParallaxWrapper">
            <div class="relative h-[430px] sm:h-[510px] rounded-3xl overflow-hidden border border-cyan-electric/25 bg-navy/80 shadow-2xl shadow-black/70">
              <canvas id="heroCanvas" class="w-full h-full block" aria-label="Interactive 3D architectural residence preview transitioning between wireframe blueprint and furnished model"></canvas>

              <!-- Floating Architectural Dimension Callouts -->
              <div class="pointer-events-none absolute top-4 left-4 flex flex-wrap gap-2">
                <span class="px-3 py-1 rounded-full glass-panel text-[11px] font-mono text-cyan-ice border border-cyan-electric/30">
                  AREA: 145 m² / 1,560 sq.ft
                </span>
                <span class="px-3 py-1 rounded-full glass-panel text-[11px] font-mono text-slate-300">
                  CLEAR HEIGHT: 3.20 m
                </span>
              </div>

              <!-- Interactive Hero Stage Controls -->
              <div class="absolute top-4 right-4 flex items-center gap-2 z-10">
                <button id="heroWireframeBtn" type="button" class="px-3.5 py-1.5 rounded-full glass-panel text-[11px] font-semibold tracking-wider uppercase text-cyan-electric border border-cyan-electric/40 hover:bg-cyan-electric hover:text-void transition-colors">
                  Wireframe Blueprint
                </button>
                <button id="heroLightBtn" type="button" class="px-3.5 py-1.5 rounded-full glass-panel text-[11px] font-semibold tracking-wider uppercase text-slate-200 border border-white/15 hover:border-cyan-electric/40 transition-colors">
                  Evening Light
                </button>
              </div>

              <!-- Bottom VR Spatial HUD -->
              <div class="absolute inset-x-4 bottom-4 glass-panel rounded-2xl p-3.5 flex flex-wrap items-center justify-between gap-3">
                <div class="flex items-center gap-3">
                  <div class="w-9 h-9 rounded-xl bg-cyan-electric/15 border border-cyan-electric/30 flex items-center justify-center text-cyan-electric" aria-hidden="true">
                    <!-- VR Headset SVG Icon -->
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" stroke-width="1.7" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" d="M3 9.5A2.5 2.5 0 015.5 7h13A2.5 2.5 0 0121 9.5v5a2.5 2.5 0 01-2.5 2.5h-3.38a1.5 1.5 0 01-1.34-.83l-.88-1.76a1 1 0 00-1.8 0l-.88 1.76a1.5 1.5 0 01-1.34.83H5.5A2.5 2.5 0 013 14.5v-5z"/>
                    </svg>
                  </div>
                  <div>
                    <div class="text-[11px] font-bold tracking-widest uppercase text-cyan-electric">CONCEPTUAL RESIDENCE MODEL</div>
                    <div class="text-xs text-slate-300">Drag to orbit • Toggle Wireframe/Furnished • Scroll down for full cutaway</div>
                  </div>
                </div>
                <a href="#explorer-3d" class="text-xs font-semibold text-cyan-ice hover:underline">Open Full 3D Explorer ↓</a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 3. THE TRANSFORMATION — BEFORE AND AFTER VR (6 STAGES) -->
    <section id="transformation" class="py-24 bg-midnight/90 border-y border-white/10">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="max-w-3xl reveal">
          <div class="text-xs font-bold tracking-[0.22em] uppercase text-cyan-electric mb-3">01 / The Paradigm Shift</div>
          <h2 class="font-display font-bold text-3xl sm:text-5xl tracking-tight text-white">
            From interpreting lines to <span class="text-gradient">inhabiting the architecture.</span>
          </h2>
          <p class="text-slate-400 mt-4 text-base sm:text-lg leading-relaxed">
            Most buyers struggle to translate 2D CAD drawings into real spatial volume. Explore how the exact same 3-bedroom residence evolves across six progressive visualisation stages.
          </p>
        </div>

        <!-- 6-Stage Selector Pills -->
        <div class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-6 gap-2.5 mt-10 reveal" role="tablist" aria-label="Six stages of architectural visualisation">
          <button type="button" role="tab" aria-selected="true" data-stage="0" class="stage-tab active text-left p-3.5 rounded-2xl border border-cyan-electric bg-cyan-electric/15 transition-all">
            <span class="block font-mono text-[10px] text-cyan-electric">STAGE 01</span>
            <span class="block font-display font-semibold text-xs sm:text-sm text-white mt-0.5">2D Floor Plan</span>
          </button>
          <button type="button" role="tab" aria-selected="false" data-stage="1" class="stage-tab text-left p-3.5 rounded-2xl border border-white/10 bg-navy/50 hover:border-white/25 transition-all">
            <span class="block font-mono text-[10px] text-slate-400">STAGE 02</span>
            <span class="block font-display font-semibold text-xs sm:text-sm text-slate-200 mt-0.5">Static Render</span>
          </button>
          <button type="button" role="tab" aria-selected="false" data-stage="2" class="stage-tab text-left p-3.5 rounded-2xl border border-white/10 bg-navy/50 hover:border-white/25 transition-all">
            <span class="block font-mono text-[10px] text-slate-400">STAGE 03</span>
            <span class="block font-display font-semibold text-xs sm:text-sm text-slate-200 mt-0.5">360° Panorama</span>
          </button>
          <button type="button" role="tab" aria-selected="false" data-stage="3" class="stage-tab text-left p-3.5 rounded-2xl border border-white/10 bg-navy/50 hover:border-white/25 transition-all">
            <span class="block font-mono text-[10px] text-slate-400">STAGE 04</span>
            <span class="block font-display font-semibold text-xs sm:text-sm text-slate-200 mt-0.5">Navigable 3D</span>
          </button>
          <button type="button" role="tab" aria-selected="false" data-stage="4" class="stage-tab text-left p-3.5 rounded-2xl border border-white/10 bg-navy/50 hover:border-white/25 transition-all">
            <span class="block font-mono text-[10px] text-slate-400">STAGE 05</span>
            <span class="block font-display font-semibold text-xs sm:text-sm text-slate-200 mt-0.5">Configurable VR</span>
          </button>
          <button type="button" role="tab" aria-selected="false" data-stage="5" class="stage-tab text-left p-3.5 rounded-2xl border border-white/10 bg-navy/50 hover:border-white/25 transition-all">
            <span class="block font-mono text-[10px] text-slate-400">STAGE 06</span>
            <span class="block font-display font-semibold text-xs sm:text-sm text-slate-200 mt-0.5">Mixed Reality</span>
          </button>
        </div>

        <!-- Interactive Stage Comparison Display -->
        <div class="mt-6 grid lg:grid-cols-12 gap-6 items-stretch reveal">
          <!-- Architectural Stage Canvas (7 Cols) -->
          <div class="lg:col-span-7 glass-card rounded-3xl p-4 sm:p-6 flex flex-col justify-between">
            <div class="flex flex-wrap items-center justify-between gap-2 pb-3 border-b border-white/10">
              <div>
                <span id="stageBadge" class="text-xs font-mono uppercase tracking-wider text-cyan-electric block">STAGE 01 / ORTHOGRAPHIC CAD DRAWING</span>
                <span id="stageScaleTag" class="text-[11px] font-mono text-slate-400">1:100 Flat Projection</span>
              </div>
              <button id="toggleSplitCurtainBtn" type="button" aria-pressed="false" class="px-3.5 py-1.5 rounded-full text-xs font-semibold border border-cyan-electric/40 bg-cyan-electric/10 text-cyan-ice hover:bg-cyan-electric hover:text-void transition-colors">
                ⇄ Split-Screen CAD vs. Spatial Curtain
              </button>
            </div>

            <!-- Dynamic Architectural SVG Visualization OR Split Curtain -->
            <div class="relative my-4 h-[300px] sm:h-[360px] rounded-2xl bg-[#060c17] border border-white/10 overflow-hidden">
              <!-- Standard 6-Stage View -->
              <div id="stageVisualContainer" class="w-full h-full flex items-center justify-center">
                <!-- Populated dynamically by JS for crisp architectural diagrams per stage -->
              </div>

              <!-- Interactive Split-Screen Before/After Curtain Overlay -->
              <div id="splitCurtainWrapper" class="hidden absolute inset-0 select-none">
                <!-- Right / Full Spatial Lit Layer (Base) -->
                <div class="absolute inset-0 bg-[#081222] flex items-center justify-center">
                  <svg viewBox="0 0 640 340" class="w-full h-full">
                    <defs>
                      <linearGradient id="curtainFloor" x1="0" y1="0" x2="1" y2="1"><stop offset="0%" stop-color="#9c7a54"/><stop offset="100%" stop-color="#5c4228"/></linearGradient>
                      <linearGradient id="curtainWall" x1="0" y1="0" x2="0" y2="1"><stop offset="0%" stop-color="#334155"/><stop offset="100%" stop-color="#1e293b"/></linearGradient>
                      <radialGradient id="curtainSun" cx="75%" cy="25%" r="60%"><stop offset="0%" stop-color="#fde68a" stop-opacity="0.45"/><stop offset="100%" stop-color="#73e3ed" stop-opacity="0"/></radialGradient>
                    </defs>
                    <rect x="0" y="0" width="640" height="340" fill="#07101e"/>
                    <!-- 3D Perspective Lit Room -->
                    <polygon points="90,265 320,150 550,265 320,330" fill="url(#curtainFloor)" stroke="#e2e8f0" stroke-width="1.5"/>
                    <polygon points="90,265 90,75 320,20 320,150" fill="url(#curtainWall)" stroke="#94a3b8"/>
                    <polygon points="320,150 320,20 550,75 550,265" fill="#253549" stroke="#94a3b8"/>
                    <!-- Glazing & Daylight -->
                    <polygon points="355,58 515,96 515,212 355,172" fill="#0d2a42" stroke="#73e3ed" stroke-width="2.5"/>
                    <polygon points="355,58 515,96 320,325 140,265" fill="url(#curtainSun)"/>
                    <!-- Furnished Sofa & Island -->
                    <polygon points="150,248 255,198 318,228 215,278" fill="#4b6b82" stroke="#a5e6ff" stroke-width="1"/>
                    <polygon points="335,235 415,196 475,226 395,265" fill="#6e4e37" stroke="#e2e8f0" stroke-width="1"/>
                    <text x="415" y="36" fill="#73e3ed" font-family="monospace" font-size="11" font-weight="bold">SPATIAL 3D ENVIRONMENT (1:1)</text>
                  </svg>
                </div>

                <!-- Left / 2D CAD Blueprint Clipped Layer -->
                <div id="splitCurtainLeftClip" class="absolute inset-0 bg-[#050a14] overflow-hidden" style="clip-path: inset(0 50% 0 0);">
                  <svg viewBox="0 0 640 340" class="w-full h-full">
                    <g stroke="#1e293b" stroke-width="1"><line x1="0" y1="60" x2="640" y2="60"/><line x1="0" y1="280" x2="640" y2="280"/><line x1="100" y1="0" x2="100" y2="340"/><line x1="540" y1="0" x2="540" y2="340"/></g>
                    <rect x="110" y="55" width="420" height="230" fill="none" stroke="#e2e8f0" stroke-width="4"/>
                    <line x1="320" y1="55" x2="320" y2="285" stroke="#e2e8f0" stroke-width="3"/>
                    <line x1="110" y1="170" x2="530" y2="170" stroke="#e2e8f0" stroke-width="3"/>
                    <g stroke="#73e3ed" stroke-width="1.5" fill="none" stroke-dasharray="5 3">
                      <rect x="130" y="75" width="170" height="75"/>
                      <rect x="340" y="75" width="170" height="75"/>
                      <rect x="130" y="190" width="170" height="75"/>
                      <rect x="340" y="190" width="170" height="75"/>
                    </g>
                    <g fill="#94a3b8" font-family="monospace" font-size="11">
                      <text x="150" y="116">MASTER SUITE 4.5×3.8m</text>
                      <text x="360" y="116">LIVING LOUNGE 5.4×4.2m</text>
                      <text x="150" y="232">MODULAR KITCHEN</text>
                      <text x="360" y="232">DINING & TERRACE</text>
                      <text x="25" y="36" fill="#a5e6ff" font-weight="bold">RAW 2D CAD BLUEPRINT</text>
                    </g>
                  </svg>
                </div>

                <!-- Vertical Draggable Divider Line & Handle -->
                <div id="splitCurtainDivider" class="curtain-handle absolute top-0 bottom-0 w-1 bg-cyan-electric shadow-[0_0_15px_#73e3ed]" style="left: 50%;">
                  <div class="absolute top-1/2 -translate-y-1/2 -translate-x-1/2 w-9 h-9 rounded-full bg-void border-2 border-cyan-electric text-cyan-electric flex items-center justify-center shadow-lg font-mono text-xs">
                    ⇄
                  </div>
                </div>
              </div>
            </div>

            <!-- Quick Stage Scrubber -->
            <div class="flex items-center gap-4 pt-2">
              <span class="text-xs text-slate-400 whitespace-nowrap" id="scrubberLeftLabel">2D Plan</span>
              <input id="stageScrubber" type="range" min="0" max="5" step="1" value="0" aria-label="Scrub through the 6 visualisation stages" class="vyoma-slider w-full">
              <span class="text-xs text-cyan-electric whitespace-nowrap" id="scrubberRightLabel">Mixed Reality</span>
            </div>
          </div>

          <!-- Spatial Comprehension Breakdown (5 Cols) -->
          <div class="lg:col-span-5 glass-card rounded-3xl p-6 sm:p-8 flex flex-col justify-between">
            <div>
              <div class="text-xs font-bold tracking-[0.2em] uppercase text-cyan-ice" id="stageSubtitle">TRADITIONAL COMMUNICATION</div>
              <h3 class="font-display font-bold text-2xl sm:text-3xl text-white mt-2" id="stageTitle">2D Architectural Floor Plan</h3>
              <p class="text-slate-300 text-sm leading-relaxed mt-3" id="stageDesc">
                Shows wall thicknesses, room labels, and linear dimensions. Accurate for engineers, yet forces buyers to mentally guess ceiling height, natural daylight, and furniture clearance.
              </p>

              <!-- 6 Key Architectural Parameters Evaluated at Each Stage -->
              <div class="mt-6 space-y-3 border-t border-white/10 pt-5">
                <div class="text-[11px] font-bold tracking-widest uppercase text-slate-400">Spatial Clarity Breakdown</div>
                <div class="grid grid-cols-2 gap-3 text-xs">
                  <div class="p-3 rounded-xl bg-void/70 border border-white/5">
                    <span class="text-slate-400 block">Dimensions & Proportions</span>
                    <strong id="paramDimensions" class="text-white font-medium mt-0.5 block">2D width × length only</strong>
                  </div>
                  <div class="p-3 rounded-xl bg-void/70 border border-white/5">
                    <span class="text-slate-400 block">Furniture Placement</span>
                    <strong id="paramFurniture" class="text-white font-medium mt-0.5 block">Flat symbolic outlines</strong>
                  </div>
                  <div class="p-3 rounded-xl bg-void/70 border border-white/5">
                    <span class="text-slate-400 block">Walking Paths</span>
                    <strong id="paramPaths" class="text-white font-medium mt-0.5 block">Inferred from door arcs</strong>
                  </div>
                  <div class="p-3 rounded-xl bg-void/70 border border-white/5">
                    <span class="text-slate-400 block">Windows & Natural Light</span>
                    <strong id="paramLight" class="text-white font-medium mt-0.5 block">Not visually represented</strong>
                  </div>
                  <div class="p-3 rounded-xl bg-void/70 border border-white/5">
                    <span class="text-slate-400 block">Interior Finishes</span>
                    <strong id="paramFinishes" class="text-white font-medium mt-0.5 block">Text notes / schedules</strong>
                  </div>
                  <div class="p-3 rounded-xl bg-void/70 border border-white/5">
                    <span class="text-slate-400 block">Exterior Appearance</span>
                    <strong id="paramExterior" class="text-white font-medium mt-0.5 block">Requires separate elevation</strong>
                  </div>
                </div>
              </div>
            </div>

            <div class="mt-6 pt-4 border-t border-white/10 flex items-center justify-between">
              <button id="prevStageBtn" type="button" class="px-4 py-2 rounded-xl border border-white/15 text-xs font-semibold hover:border-cyan-electric/50 disabled:opacity-40">← Previous</button>
              <span id="stageStepCounter" class="text-xs font-mono text-slate-400">01 / 06</span>
              <button id="nextStageBtn" type="button" class="px-4 py-2 rounded-xl bg-cyan-electric/15 border border-cyan-electric/40 text-cyan-ice text-xs font-semibold hover:bg-cyan-electric hover:text-void transition-colors">Next Stage →</button>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 4. REALISTIC 3D PROPERTY EXPERIENCE (INTERACTIVE ARCHITECTURAL CUTAWAY) -->
    <section id="explorer-3d" class="py-24 relative">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex flex-col lg:flex-row lg:items-end justify-between gap-6 mb-10 reveal">
          <div class="max-w-2xl">
            <div class="text-xs font-bold tracking-[0.22em] uppercase text-cyan-electric mb-3">02 / Interactive 3D Property Prototype</div>
            <h2 class="font-display font-bold text-3xl sm:text-5xl tracking-tight text-white">
              Explore a modern villa <span class="text-gradient">room by room.</span>
            </h2>
            <p class="text-slate-400 mt-3 text-base">
              Inspect our conceptual 145 m² Courtyard Residence in real-time 3D. Select individual rooms, toggle furniture, lift walls for an exploded view, or launch a guided walkthrough.
            </p>
          </div>
          <div class="text-xs text-slate-400 glass-panel px-4 py-2.5 rounded-xl border border-cyan-electric/20">
            <strong class="text-cyan-ice">Interactive Browser Demonstration:</strong> Built in Three.js to preview spatial scale & layout.
          </div>
        </div>

        <!-- 3D Viewport & Architectural Controls -->
        <div class="grid lg:grid-cols-12 gap-6 items-start reveal">
          <!-- Main 3D Canvas Stage (8 Cols) -->
          <div class="lg:col-span-8 relative rounded-3xl overflow-hidden border border-white/15 bg-[#080f1c] shadow-2xl">
            <div id="villaViewportContainer" class="relative h-[480px] sm:h-[600px] w-full overflow-hidden">
              <canvas id="villaCanvas" class="w-full h-full block cursor-grab active:cursor-grabbing" aria-label="Interactive 3D architectural cutaway model of a multi-room modern residence"></canvas>

              <!-- 3D-Projected CAD Dimension Callout Overlay Container -->
              <div id="cadDimensionsOverlay" class="hidden absolute inset-0 pointer-events-none overflow-hidden">
                <div class="cad-pin px-2 py-0.5 rounded bg-void/90 border border-cyan-electric/60 text-[10px] font-mono text-cyan-ice shadow" data-world="-3.2,1.6,0.4">
                  LIVING SPAN: 5.40m × 4.20m
                </div>
                <div class="cad-pin px-2 py-0.5 rounded bg-void/90 border border-cyan-electric/60 text-[10px] font-mono text-cyan-ice shadow" data-world="3.8,1.6,0.8">
                  KITCHEN ISLAND: 2.10m × 0.85m
                </div>
                <div class="cad-pin px-2 py-0.5 rounded bg-void/90 border border-cyan-electric/60 text-[10px] font-mono text-cyan-ice shadow" data-world="-3.4,1.6,-2.6">
                  MASTER SUITE: 19.5 m²
                </div>
                <div class="cad-pin px-2 py-0.5 rounded bg-void/90 border border-amber-300/60 text-[10px] font-mono text-amber-200 shadow" data-world="0,2.85,-3.9">
                  CLEAR CEILING: 3.20 m
                </div>
                <div class="cad-pin px-2 py-0.5 rounded bg-void/90 border border-emerald-300/60 text-[10px] font-mono text-emerald-200 shadow" data-world="-1.8,1.4,2.05">
                  LOW-E GLAZING RATIO: 68%
                </div>
              </div>

              <!-- Top Camera Perspective & Mode Bar -->
              <div class="absolute top-4 left-4 right-4 flex flex-wrap items-center justify-between gap-2 pointer-events-none z-20">
                <div class="flex flex-wrap gap-1.5 pointer-events-auto">
                  <button type="button" data-cam="dollhouse" class="cam-preset-btn px-3 py-1.5 rounded-full text-xs font-semibold bg-cyan-electric text-void shadow">Dollhouse Orbit</button>
                  <button type="button" data-cam="exterior" class="cam-preset-btn px-3 py-1.5 rounded-full text-xs font-semibold glass-panel text-slate-200 hover:border-cyan-electric/50">Exterior & Deck</button>
                  <button type="button" data-cam="walkthrough" id="walkthroughBtn" class="cam-preset-btn px-3 py-1.5 rounded-full text-xs font-semibold glass-panel text-cyan-ice border border-cyan-electric/40 hover:bg-cyan-electric/20">▶ Guided Tour</button>
                  <button type="button" data-cam="firstperson" id="firstPersonBtn" class="cam-preset-btn px-3 py-1.5 rounded-full text-xs font-semibold glass-panel text-emerald-300 border border-emerald-400/40 hover:bg-emerald-400/20">🚶 First-Person Walk (1.65m)</button>
                </div>
                <span id="walkthroughStatus" class="hidden px-3 py-1 rounded-full bg-cyan-electric/20 border border-cyan-electric text-cyan-ice text-[11px] font-mono">
                  WALKTHROUGH TOUR ACTIVE
                </span>
              </div>

              <!-- Synchronized 2D Architectural Mini-Map (HUD Top-Right) -->
              <div id="miniMapHud" class="absolute top-16 right-4 z-20 glass-panel rounded-2xl p-2.5 border border-cyan-electric/30 w-44 sm:w-52 shadow-xl">
                <div class="flex items-center justify-between text-[10px] font-mono text-cyan-electric mb-1.5 px-1">
                  <span>2D CAD RADAR</span>
                  <button id="toggleMiniMapBtn" type="button" class="text-slate-400 hover:text-white">Hide</button>
                </div>
                <div id="miniMapBody">
                  <svg id="miniMapSvg" viewBox="-6.5 -4.8 13 9.2" class="w-full h-28 rounded-xl bg-[#050a14] border border-white/10 cursor-pointer" aria-label="Interactive 2D floor plan radar. Click any room to teleport camera.">
                    <!-- Clickable Room Zones in World Coordinates -->
                    <rect data-map-room="master" x="-5.4" y="-3.9" width="4.0" height="2.6" fill="rgba(115,227,237,0.08)" stroke="#475569" stroke-width="0.12"/>
                    <rect data-map-room="bedroom2" x="-1.4" y="-3.9" width="3.4" height="2.6" fill="rgba(115,227,237,0.08)" stroke="#475569" stroke-width="0.12"/>
                    <rect data-map-room="bathroom" x="2.0" y="-3.9" width="3.4" height="2.6" fill="rgba(115,227,237,0.08)" stroke="#475569" stroke-width="0.12"/>
                    <rect data-map-room="living" x="-5.4" y="-1.3" width="4.4" height="3.4" fill="rgba(115,227,237,0.16)" stroke="#73e3ed" stroke-width="0.14"/>
                    <rect data-map-room="dining" x="-1.0" y="-1.3" width="3.2" height="3.4" fill="rgba(115,227,237,0.08)" stroke="#475569" stroke-width="0.12"/>
                    <rect data-map-room="kitchen" x="2.2" y="-1.3" width="3.2" height="3.4" fill="rgba(115,227,237,0.08)" stroke="#475569" stroke-width="0.12"/>
                    <!-- Terrace & Pool -->
                    <rect x="-5.4" y="2.1" width="10.8" height="1.8" fill="rgba(156,123,86,0.2)" stroke="#334155" stroke-width="0.1"/>
                    <rect x="0.4" y="2.4" width="4.4" height="1.2" fill="rgba(36,142,166,0.45)"/>
                    <!-- Labels -->
                    <g fill="#94a3b8" font-family="monospace" font-size="0.55" pointer-events="none" text-anchor="middle">
                      <text x="-3.4" y="-2.5">M.BED</text>
                      <text x="0.3" y="-2.5">GUEST</text>
                      <text x="3.7" y="-2.5">BATH</text>
                      <text x="-3.2" y="0.5" fill="#e2e8f0">LIVING</text>
                      <text x="0.6" y="0.5">DINING</text>
                      <text x="3.8" y="0.5">KITCH</text>
                    </g>
                    <!-- Live Camera Cone & Position Node -->
                    <g id="miniMapCamGroup" transform="translate(0,0) rotate(0)" pointer-events="none">
                      <polygon points="0,0 -1.35,-2.4 1.35,-2.4" fill="rgba(115,227,237,0.28)" stroke="#73e3ed" stroke-width="0.08"/>
                      <circle cx="0" cy="0" r="0.35" fill="#73e3ed" stroke="#050810" stroke-width="0.12"/>
                    </g>
                  </svg>
                  <div class="text-[9px] text-slate-400 mt-1 text-center">Click any room on radar to focus</div>
                </div>
              </div>

              <!-- On-Screen Touch / First-Person Navigation Pad (Shown in First-Person Mode) -->
              <div id="fpTouchControls" class="hidden absolute bottom-24 right-4 z-20 glass-panel rounded-2xl p-2.5 border border-emerald-400/40">
                <div class="text-[9px] font-mono text-emerald-300 text-center mb-1.5">WASD / STEP PAD</div>
                <div class="grid grid-cols-3 gap-1 w-28">
                  <div></div>
                  <button type="button" data-fp-move="fwd" class="fp-pad-btn py-2 rounded-lg bg-void/80 border border-white/15 text-xs font-bold text-white active:bg-emerald-400 active:text-void">▲</button>
                  <div></div>
                  <button type="button" data-fp-move="left" class="fp-pad-btn py-2 rounded-lg bg-void/80 border border-white/15 text-xs font-bold text-white active:bg-emerald-400 active:text-void">◀</button>
                  <button type="button" data-fp-move="back" class="fp-pad-btn py-2 rounded-lg bg-void/80 border border-white/15 text-xs font-bold text-white active:bg-emerald-400 active:text-void">▼</button>
                  <button type="button" data-fp-move="right" class="fp-pad-btn py-2 rounded-lg bg-void/80 border border-white/15 text-xs font-bold text-white active:bg-emerald-400 active:text-void">▶</button>
                </div>
              </div>

              <!-- Selected Room Floating Dimension Card -->
              <div id="roomHudCard" class="absolute bottom-4 left-4 right-4 sm:right-auto sm:w-80 glass-panel rounded-2xl p-4 border border-cyan-electric/30 z-20">
                <div class="flex items-center justify-between">
                  <span class="text-[10px] font-mono uppercase tracking-widest text-cyan-electric" id="hudRoomZone">SELECTED SPACE</span>
                  <span class="text-[11px] font-mono text-slate-300" id="hudRoomDims">5.4m × 4.2m (22.7 m²)</span>
                </div>
                <h3 class="font-display font-bold text-lg text-white mt-1" id="hudRoomName">Living Lounge & Glazing</h3>
                <p class="text-xs text-slate-300 mt-1 leading-relaxed" id="hudRoomDesc">
                  Double-aspect living space opening onto the timber terrace with floor-to-ceiling low-E glazing and sectional seating.
                </p>
              </div>
            </div>
          </div>

          <!-- Architectural Control Panel (4 Cols) -->
          <div class="lg:col-span-4 space-y-4">
            <!-- Room Selector -->
            <div class="glass-card rounded-3xl p-5">
              <div class="text-xs font-bold tracking-[0.18em] uppercase text-cyan-electric mb-3">1. Inspect Individual Rooms</div>
              <div class="grid grid-cols-2 gap-2" id="roomButtonsGrid">
                <button type="button" data-room="living" class="room-select-btn active text-left p-3 rounded-xl border border-cyan-electric bg-cyan-electric/15 text-xs font-semibold text-white">
                  Living Lounge
                  <span class="block text-[10px] font-mono text-cyan-ice mt-0.5">22.7 m²</span>
                </button>
                <button type="button" data-room="kitchen" class="room-select-btn text-left p-3 rounded-xl border border-white/10 bg-void/60 hover:border-white/30 text-xs font-semibold text-slate-200">
                  Kitchen & Island
                  <span class="block text-[10px] font-mono text-slate-400 mt-0.5">14.8 m²</span>
                </button>
                <button type="button" data-room="dining" class="room-select-btn text-left p-3 rounded-xl border border-white/10 bg-void/60 hover:border-white/30 text-xs font-semibold text-slate-200">
                  Dining Area
                  <span class="block text-[10px] font-mono text-slate-400 mt-0.5">13.2 m²</span>
                </button>
                <button type="button" data-room="master" class="room-select-btn text-left p-3 rounded-xl border border-white/10 bg-void/60 hover:border-white/30 text-xs font-semibold text-slate-200">
                  Master Bedroom
                  <span class="block text-[10px] font-mono text-slate-400 mt-0.5">19.5 m²</span>
                </button>
                <button type="button" data-room="bedroom2" class="room-select-btn text-left p-3 rounded-xl border border-white/10 bg-void/60 hover:border-white/30 text-xs font-semibold text-slate-200">
                  Guest Bedroom
                  <span class="block text-[10px] font-mono text-slate-400 mt-0.5">14.0 m²</span>
                </button>
                <button type="button" data-room="bathroom" class="room-select-btn text-left p-3 rounded-xl border border-white/10 bg-void/60 hover:border-white/30 text-xs font-semibold text-slate-200">
                  Spa Bathroom
                  <span class="block text-[10px] font-mono text-slate-400 mt-0.5">7.8 m²</span>
                </button>
              </div>
            </div>

            <!-- Architectural Toggles & Sliders -->
            <div class="glass-card rounded-3xl p-5 space-y-3.5">
              <div class="text-xs font-bold tracking-[0.18em] uppercase text-cyan-electric">2. Spatial & Solar Controls</div>

              <!-- Continuous Solar Sun-Path & Time-of-Day Scrubber -->
              <div class="p-3.5 rounded-xl bg-void/60 border border-white/10 space-y-2">
                <div class="flex items-center justify-between">
                  <span class="text-xs font-semibold text-white">Solar Azimuth & Time</span>
                  <span id="solarTimeReadout" class="text-[11px] font-mono text-amber-300">10:30 AM • Morning Sun</span>
                </div>
                <input id="solarTimeSlider" type="range" min="6" max="21" step="0.25" value="10.5" aria-label="Solar Azimuth and Time of Day" class="vyoma-slider w-full">
                <div class="flex justify-between text-[10px] font-mono text-slate-400">
                  <span>06:00 Sunrise</span>
                  <span>12:30 Zenith</span>
                  <span>17:45 Golden</span>
                  <span>21:00 Night</span>
                </div>
              </div>

              <!-- Exploded Axonometric Layer View Slider -->
              <div class="p-3.5 rounded-xl bg-void/60 border border-white/10 space-y-2">
                <div class="flex items-center justify-between">
                  <span class="text-xs font-semibold text-white">Exploded Axonometric Layers</span>
                  <span id="explodedReadout" class="text-[11px] font-mono text-cyan-electric">0% Assembled</span>
                </div>
                <input id="explodedViewSlider" type="range" min="0" max="100" step="1" value="0" aria-label="Exploded Axonometric Layer Separation" class="vyoma-slider w-full">
                <div class="text-[10px] text-slate-400">Separates Slab → Finishes → Furniture → Walls → Roof Pergola</div>
              </div>

              <div class="flex items-center justify-between p-3 rounded-xl bg-void/60 border border-white/10">
                <div>
                  <div class="text-xs font-semibold text-white">Interior Furnishing</div>
                  <div class="text-[11px] text-slate-400">Compare bare shell vs. furnished scale</div>
                </div>
                <button id="toggleFurnitureBtn" type="button" aria-pressed="true" class="px-3.5 py-1.5 rounded-lg bg-cyan-electric text-void text-xs font-bold">
                  Furnished
                </button>
              </div>

              <div class="flex items-center justify-between p-3 rounded-xl bg-void/60 border border-white/10">
                <div>
                  <div class="text-xs font-semibold text-white">Wall Cutaway</div>
                  <div class="text-[11px] text-slate-400">Lower partitions for clear sightlines</div>
                </div>
                <button id="toggleWallsBtn" type="button" aria-pressed="false" class="px-3.5 py-1.5 rounded-lg border border-white/20 text-slate-200 text-xs font-semibold hover:border-cyan-electric">
                  Standard
                </button>
              </div>

              <div class="flex items-center justify-between p-3 rounded-xl bg-void/60 border border-white/10">
                <div>
                  <div class="text-xs font-semibold text-white">CAD Dimensions Overlay</div>
                  <div class="text-[11px] text-slate-400">Pin 3D span, height & glazing callouts</div>
                </div>
                <button id="toggleCadOverlayBtn" type="button" aria-pressed="false" class="px-3.5 py-1.5 rounded-lg border border-white/20 text-slate-200 text-xs font-semibold hover:border-cyan-electric">
                  Hidden
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 5. THE FOUR VYOMA EXPERIENCE LEVELS -->
    <section id="experience-levels" class="py-24 bg-midnight/90 border-y border-white/10">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="max-w-3xl reveal">
          <div class="text-xs font-bold tracking-[0.22em] uppercase text-cyan-electric mb-3">03 / The Experience Spectrum</div>
          <h2 class="font-display font-bold text-3xl sm:text-5xl tracking-tight text-white">
            Four distinct levels of <span class="text-gradient">spatial immersion.</span>
          </h2>
          <p class="text-slate-400 mt-4 text-base sm:text-lg">
            Every project has different goals, budgets, and hardware needs. VYOMA structures its capabilities into four transparent, well-defined tiers.
          </p>
        </div>

        <!-- Level Selector Tabs -->
        <div class="grid sm:grid-cols-2 lg:grid-cols-4 gap-3 mt-10 reveal" role="tablist" aria-label="VYOMA Experience Levels">
          <button type="button" role="tab" aria-selected="true" data-exp="0" class="exp-tab active text-left p-5 rounded-2xl border border-cyan-electric bg-cyan-electric/15 transition-all">
            <span class="font-mono text-xs text-cyan-electric">LEVEL 01</span>
            <h3 class="font-display font-bold text-lg text-white mt-1">VYOMA VIEW</h3>
            <p class="text-xs text-slate-300 mt-1">360° Panoramic Visualisation</p>
          </button>
          <button type="button" role="tab" aria-selected="false" data-exp="1" class="exp-tab text-left p-5 rounded-2xl border border-white/10 bg-navy/50 hover:border-white/30 transition-all">
            <span class="font-mono text-xs text-slate-400">LEVEL 02 • FLAGSHIP</span>
            <h3 class="font-display font-bold text-lg text-white mt-1">VYOMA IMMERSION</h3>
            <p class="text-xs text-slate-400 mt-1">Real-Time Navigable 3D Walkthrough</p>
          </button>
          <button type="button" role="tab" aria-selected="false" data-exp="2" class="exp-tab text-left p-5 rounded-2xl border border-white/10 bg-navy/50 hover:border-white/30 transition-all">
            <span class="font-mono text-xs text-slate-400">LEVEL 03</span>
            <h3 class="font-display font-bold text-lg text-white mt-1">VYOMA INTERACTIVE</h3>
            <p class="text-xs text-slate-400 mt-1">Configurable Environments</p>
          </button>
          <button type="button" role="tab" aria-selected="false" data-exp="3" class="exp-tab text-left p-5 rounded-2xl border border-white/10 bg-navy/50 hover:border-white/30 transition-all">
            <span class="font-mono text-xs text-slate-400">LEVEL 04</span>
            <h3 class="font-display font-bold text-lg text-white mt-1">VYOMA REALITY</h3>
            <p class="text-xs text-slate-400 mt-1">Mixed Reality & Site Context</p>
          </button>
        </div>

        <!-- Level Detail & Interactive Mini-Demo Panel -->
        <div class="mt-6 glass-card rounded-3xl p-6 sm:p-10 reveal">
          <div class="grid lg:grid-cols-12 gap-8 items-center">
            <!-- Interactive Demonstration Box (6 Cols) -->
            <div class="lg:col-span-6">
              <div id="expDemoContainer" class="relative h-[320px] sm:h-[370px] rounded-2xl bg-void border border-white/15 overflow-hidden">
                <!-- Interactive mini-demo rendered per level -->
              </div>
              <p id="expDemoCaption" class="text-xs text-slate-400 mt-3">
                Interactive Demo: Drag horizontally inside the panorama viewport to look around 360°, or click a hotspot node to jump viewpoints.
              </p>
            </div>

            <!-- Explanation, Target Customers & Applications (6 Cols) -->
            <div class="lg:col-span-6 space-y-5">
              <div>
                <span id="expBadge" class="inline-block px-3 py-1 rounded-full bg-cyan-electric/15 border border-cyan-electric/30 text-cyan-electric font-mono text-xs">
                  LEVEL 01 — STATIONARY 360° PANORAMAS
                </span>
                <h3 id="expTitle" class="font-display font-bold text-2xl sm:text-3xl text-white mt-3">
                  VYOMA VIEW — Look Around Every Room Remotely
                </h3>
                <p id="expSummary" class="text-slate-300 text-sm sm:text-base leading-relaxed mt-3">
                  A curated series of high-resolution 360-degree viewpoints connected via intuitive spatial hotspots. Visitors can look in every direction from fixed camera nodes—ideal for fast web sharing, mobile viewing, and remote NRI property previews.
                </p>
              </div>

              <!-- Honest Technical Distinction Note -->
              <div id="expDistinction" class="p-3.5 rounded-xl bg-navy/80 border border-cyan-electric/25 text-xs text-cyan-ice">
                <strong>Scope Note:</strong> VYOMA VIEW provides stationary panoramic viewpoints with hotspot transitions rather than unrestricted free-roaming 3D movement.
              </div>

              <div class="grid sm:grid-cols-2 gap-4 pt-2">
                <div class="p-4 rounded-2xl bg-void/70 border border-white/10">
                  <div class="text-[11px] font-bold tracking-widest uppercase text-cyan-electric mb-2">Target Customers</div>
                  <ul id="expCustomers" class="text-xs text-slate-300 space-y-1.5 list-disc list-inside">
                    <li>Real estate brokers & resale agents</li>
                    <li>Residential apartment listings</li>
                    <li>Remote & NRI property buyers</li>
                  </ul>
                </div>
                <div class="p-4 rounded-2xl bg-void/70 border border-white/10">
                  <div class="text-[11px] font-bold tracking-widest uppercase text-cyan-electric mb-2">Practical Applications</div>
                  <ul id="expApplications" class="text-xs text-slate-300 space-y-1.5 list-disc list-inside">
                    <li>WhatsApp / web shareable tour links</li>
                    <li>Pre-visit property shortlisting</li>
                    <li>Hospitality suite & venue previews</li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 6. COMPLETE RANGE OF 12 INDUSTRIES -->
    <section id="industries" class="py-24">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex flex-col md:flex-row md:items-end justify-between gap-6 mb-12 reveal">
          <div class="max-w-2xl">
            <div class="text-xs font-bold tracking-[0.22em] uppercase text-cyan-electric mb-3">04 / Multi-Sector Applications</div>
            <h2 class="font-display font-bold text-3xl sm:text-5xl tracking-tight text-white">
              One spatial engine. <span class="text-gradient">Twelve industries.</span>
            </h2>
            <p class="text-slate-400 mt-3 text-base">
              Wherever physical space requires planning, approval, training, or presentation, VYOMA bridges imagination and reality.
            </p>
          </div>
          <!-- Category Filter -->
          <div class="flex flex-wrap gap-2" role="group" aria-label="Filter industries">
            <button type="button" data-ind-filter="all" class="ind-filter-btn active px-3.5 py-1.5 rounded-full text-xs font-semibold bg-cyan-electric text-void">All 12 Sectors</button>
            <button type="button" data-ind-filter="property" class="ind-filter-btn px-3.5 py-1.5 rounded-full text-xs font-semibold glass-panel text-slate-300 hover:border-cyan-electric/40">Real Estate & Living</button>
            <button type="button" data-ind-filter="design" class="ind-filter-btn px-3.5 py-1.5 rounded-full text-xs font-semibold glass-panel text-slate-300 hover:border-cyan-electric/40">Design & Retail</button>
            <button type="button" data-ind-filter="enterprise" class="ind-filter-btn px-3.5 py-1.5 rounded-full text-xs font-semibold glass-panel text-slate-300 hover:border-cyan-electric/40">Civic & Industrial</button>
          </div>
        </div>

        <div id="industriesGrid" class="grid sm:grid-cols-2 lg:grid-cols-4 gap-5 reveal">
          <!-- Populated cleanly via JS with custom architectural SVG emblems -->
        </div>
      </div>
    </section>

    <!-- 7. CUSTOMER-SPECIFIC SOLUTIONS -->
    <section id="solutions" class="py-24 bg-midnight/90 border-y border-white/10">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="max-w-3xl reveal">
          <div class="text-xs font-bold tracking-[0.22em] uppercase text-cyan-electric mb-3">05 / Tailored Value</div>
          <h2 class="font-display font-bold text-3xl sm:text-5xl tracking-tight text-white">
            Built for everyone who <span class="text-gradient">designs, builds, or buys.</span>
          </h2>
          <p class="text-slate-400 mt-4 text-base">
            Select a stakeholder profile below to examine the core challenge they face, how VYOMA resolves it, and a practical conceptual scenario.
          </p>
        </div>

        <!-- 4 Stakeholder Tabs -->
        <div class="grid sm:grid-cols-2 lg:grid-cols-4 gap-3 mt-10 reveal" role="tablist" aria-label="Customer segments">
          <button type="button" role="tab" aria-selected="true" data-cust="0" class="cust-tab active text-left p-5 rounded-2xl border border-cyan-electric bg-cyan-electric/15">
            <span class="font-mono text-[11px] text-cyan-electric">01 / INDIVIDUALS</span>
            <h3 class="font-display font-bold text-lg text-white mt-1">Homeowners</h3>
            <p class="text-xs text-slate-300 mt-1">Experience your future home before construction.</p>
          </button>
          <button type="button" role="tab" aria-selected="false" data-cust="1" class="cust-tab text-left p-5 rounded-2xl border border-white/10 bg-navy/50 hover:border-white/30">
            <span class="font-mono text-[11px] text-slate-400">02 / DEVELOPERS</span>
            <h3 class="font-display font-bold text-lg text-white mt-1">Builders & Developers</h3>
            <p class="text-xs text-slate-400 mt-1">Present properties before physical completion.</p>
          </button>
          <button type="button" role="tab" aria-selected="false" data-cust="2" class="cust-tab text-left p-5 rounded-2xl border border-white/10 bg-navy/50 hover:border-white/30">
            <span class="font-mono text-[11px] text-slate-400">03 / BROKERAGE</span>
            <h3 class="font-display font-bold text-lg text-white mt-1">Real Estate Agents</h3>
            <p class="text-xs text-slate-400 mt-1">Showcase existing spaces remotely & effectively.</p>
          </button>
          <button type="button" role="tab" aria-selected="false" data-cust="3" class="cust-tab text-left p-5 rounded-2xl border border-white/10 bg-navy/50 hover:border-white/30">
            <span class="font-mono text-[11px] text-slate-400">04 / STUDIOS</span>
            <h3 class="font-display font-bold text-lg text-white mt-1">Architects & Designers</h3>
            <p class="text-xs text-slate-400 mt-1">Help clients evaluate designs before execution.</p>
          </button>
        </div>

        <!-- Stakeholder Problem / Solution / Benefit / Example Card -->
        <div id="customerDetailPanel" class="mt-6 glass-card rounded-3xl p-6 sm:p-10 reveal">
          <!-- Populated dynamically via JS -->
        </div>
      </div>
    </section>

    <!-- 8. VIRTUAL PROPERTY SHOWROOM -->
    <section id="showroom" class="py-24">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex flex-col md:flex-row md:items-end justify-between gap-6 mb-12 reveal">
          <div class="max-w-2xl">
            <div class="text-xs font-bold tracking-[0.22em] uppercase text-cyan-electric mb-3">06 / Virtual Property Gallery</div>
            <h2 class="font-display font-bold text-3xl sm:text-5xl tracking-tight text-white">
              Step into a <span class="text-gradient">digital property showroom.</span>
            </h2>
            <p class="text-slate-400 mt-3 text-base">
              Developers and agencies can present an entire portfolio inside one unified spatial gallery. Select any conceptual property below to launch a guided inspection brief.
            </p>
          </div>
          <span class="px-3.5 py-2 rounded-xl border border-amber-400/30 bg-amber-400/10 text-amber-200 text-xs font-medium">
            Note: All properties below are conceptual architectural demonstrations.
          </span>
        </div>

        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-6 reveal" id="showroomGrid">
          <!-- Rendered via JS -->
        </div>

        <!-- Guided Property Inspection Drawer/Panel -->
        <div id="showroomInspector" class="mt-8 glass-panel rounded-3xl p-6 sm:p-8 border border-cyan-electric/35 reveal">
          <!-- Populated with selected property details -->
        </div>
      </div>
    </section>

    <!-- 9. INTERIOR CUSTOMISATION STUDIO -->
    <section id="studio" class="py-24 bg-midnight/90 border-y border-white/10">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="max-w-3xl mb-10 reveal">
          <div class="text-xs font-bold tracking-[0.22em] uppercase text-cyan-electric mb-3">07 / VYOMA Interactive Preview</div>
          <h2 class="font-display font-bold text-3xl sm:text-5xl tracking-tight text-white">
            Interior <span class="text-gradient">Customisation Studio.</span>
          </h2>
          <p class="text-slate-400 mt-3 text-base">
            Eliminate material guesswork before procurement. Switch room presets, wall finishes, flooring planks, furniture layouts, and lighting moods in real time.
          </p>
        </div>

        <div class="grid lg:grid-cols-12 gap-8 items-start reveal">
          <!-- Interactive Architectural Room Illustration (7 Cols) -->
          <div class="lg:col-span-7 glass-card rounded-3xl p-4 sm:p-6">
            <div class="flex flex-wrap items-center justify-between gap-2 pb-4 border-b border-white/10">
              <div class="flex gap-2">
                <button type="button" data-studio-room="lounge" class="studio-room-btn active px-3.5 py-1.5 rounded-full text-xs font-semibold bg-cyan-electric text-void">Living Lounge</button>
                <button type="button" data-studio-room="suite" class="studio-room-btn px-3.5 py-1.5 rounded-full text-xs font-semibold border border-white/15 text-slate-300 hover:border-cyan-electric/40">Master Suite</button>
              </div>
              <span id="studioThemeLabel" class="text-xs font-mono text-cyan-ice">THEME: SCANDINAVIAN WARMTH</span>
            </div>

            <!-- Live Layered SVG Architectural Perspective -->
            <div class="relative my-4 h-[320px] sm:h-[390px] rounded-2xl overflow-hidden border border-white/10 bg-[#080e1a]">
              <svg id="studioSvg" viewBox="0 0 800 450" class="w-full h-full" role="img" aria-label="Interactive interior room customisation preview">
                <defs>
                  <linearGradient id="studioSkyGrad" x1="0" y1="0" x2="0" y2="1">
                    <stop id="skyStop1" offset="0%" stop-color="#7ec8e3"/>
                    <stop id="skyStop2" offset="100%" stop-color="#d8f3ff"/>
                  </linearGradient>
                  <radialGradient id="studioLampGlow" cx="50%" cy="30%" r="55%">
                    <stop id="lampStop1" offset="0%" stop-color="#ffd280" stop-opacity="0.32"/>
                    <stop offset="100%" stop-color="#ffd280" stop-opacity="0"/>
                  </radialGradient>
                </defs>

                <!-- Exterior Window Backdrop -->
                <rect x="460" y="55" width="250" height="215" fill="url(#studioSkyGrad)"/>
                <!-- Architectural Horizon Trees -->
                <circle cx="520" cy="235" r="45" fill="#2b594b" opacity="0.75"/>
                <circle cx="575" cy="225" r="55" fill="#1f473b" opacity="0.85"/>
                <circle cx="655" cy="240" r="40" fill="#2b594b" opacity="0.7"/>

                <!-- Ceiling -->
                <polygon points="0,0 800,0 710,55 130,55" fill="#162030"/>
                <!-- Back Wall -->
                <polygon id="studioBackWall" points="130,55 710,55 710,310 130,310" fill="#d8d3c8"/>
                <!-- Left Perspective Wall -->
                <polygon id="studioLeftWall" points="0,0 130,55 130,310 0,410" fill="#bfb9ad"/>
                <!-- Right Perspective Wall -->
                <polygon id="studioRightWall" points="710,55 800,0 800,410 710,310" fill="#b4aea2"/>

                <!-- Window Frame Cutout & Mullions -->
                <rect x="460" y="55" width="250" height="215" fill="url(#studioSkyGrad)"/>
                <g stroke="#1e293b" stroke-width="5" fill="none">
                  <rect x="460" y="55" width="250" height="215"/>
                  <line x1="543" y1="55" x2="543" y2="270"/>
                  <line x1="626" y1="55" x2="626" y2="270"/>
                </g>

                <!-- Floor Plane -->
                <polygon id="studioFloor" points="0,410 130,310 710,310 800,410 800,450 0,450" fill="#9c7a54"/>
                <!-- Floor Plank / Tile Perspective Lines -->
                <g id="studioFloorLines" stroke="#000000" stroke-opacity="0.16" stroke-width="1.5">
                  <line x1="130" y1="310" x2="40" y2="450"/>
                  <line x1="245" y1="310" x2="205" y2="450"/>
                  <line x1="360" y1="310" x2="360" y2="450"/>
                  <line x1="475" y1="310" x2="515" y2="450"/>
                  <line x1="590" y1="310" x2="670" y2="450"/>
                  <line x1="710" y1="310" x2="785" y2="450"/>
                  <line x1="75" y1="350" x2="745" y2="350"/>
                  <line x1="30" y1="395" x2="780" y2="395"/>
                </g>

                <!-- Wall Art / Architectural Niche on Back Wall -->
                <g id="studioWallArt">
                  <rect x="200" y="105" width="145" height="105" rx="3" fill="#182232" stroke="#475569" stroke-width="3"/>
                  <circle cx="255" cy="155" r="26" fill="#73e3ed" opacity="0.55"/>
                  <polygon points="235,195 275,140 315,195" fill="#94a3b8" opacity="0.6"/>
                </g>

                <!-- Furniture Layer (Updates by Room & Arrangement) -->
                <g id="studioFurnitureGroup"></g>

                <!-- Pendant Light Fixture -->
                <line x1="395" y1="0" x2="395" y2="85" stroke="#1e293b" stroke-width="3"/>
                <path d="M365,85 Q395,62 425,85 Z" fill="#1e293b"/>
                <ellipse cx="395" cy="87" rx="22" ry="4" fill="#fde68a"/>

                <!-- Ambient Lighting Overlay -->
                <rect id="studioAmbientOverlay" x="0" y="0" width="800" height="450" fill="url(#studioLampGlow)" pointer-events="none"/>
              </svg>
            </div>

            <!-- Active Specification Strip -->
            <div class="grid grid-cols-2 sm:grid-cols-4 gap-2 text-[11px]">
              <div class="p-2.5 rounded-xl bg-void/70 border border-white/10">
                <span class="text-slate-400 block">Wall Finish</span>
                <strong id="specWall" class="text-white">Warm Alabaster</strong>
              </div>
              <div class="p-2.5 rounded-xl bg-void/70 border border-white/10">
                <span class="text-slate-400 block">Flooring</span>
                <strong id="specFloor" class="text-white">Natural Oak</strong>
              </div>
              <div class="p-2.5 rounded-xl bg-void/70 border border-white/10">
                <span class="text-slate-400 block">Layout</span>
                <strong id="specLayout" class="text-white">Modern Lounge</strong>
              </div>
              <div class="p-2.5 rounded-xl bg-void/70 border border-white/10">
                <span class="text-slate-400 block">Lighting</span>
                <strong id="specLight" class="text-white">Morning Daylight</strong>
              </div>
            </div>
          </div>

          <!-- Customisation Controls (5 Cols) -->
          <div class="lg:col-span-5 glass-card rounded-3xl p-6 space-y-5">
            <!-- Wall Colour -->
            <div>
              <label class="block text-xs font-bold tracking-wider uppercase text-cyan-electric mb-2.5">1. Wall Colour & Plaster</label>
              <div class="grid grid-cols-2 gap-2">
                <button type="button" data-wall="#d8d3c8|#bfb9ad|#b4aea2|Warm Alabaster" class="studio-wall-btn active flex items-center gap-2.5 p-2.5 rounded-xl border border-cyan-electric bg-cyan-electric/10 text-xs font-medium text-white">
                  <span class="w-5 h-5 rounded-full border border-white/30" style="background:#d8d3c8"></span> Warm Alabaster
                </button>
                <button type="button" data-wall="#334155|#263244|#1e293b|Slate Graphite" class="studio-wall-btn flex items-center gap-2.5 p-2.5 rounded-xl border border-white/10 bg-void/60 text-xs font-medium text-slate-300">
                  <span class="w-5 h-5 rounded-full border border-white/30" style="background:#334155"></span> Slate Graphite
                </button>
                <button type="button" data-wall="#9ab0a6|#82998e|#748a80|Sage Mist" class="studio-wall-btn flex items-center gap-2.5 p-2.5 rounded-xl border border-white/10 bg-void/60 text-xs font-medium text-slate-300">
                  <span class="w-5 h-5 rounded-full border border-white/30" style="background:#9ab0a6"></span> Sage Mist
                </button>
                <button type="button" data-wall="#b87d65|#9e6650|#8c5844|Terracotta Clay" class="studio-wall-btn flex items-center gap-2.5 p-2.5 rounded-xl border border-white/10 bg-void/60 text-xs font-medium text-slate-300">
                  <span class="w-5 h-5 rounded-full border border-white/30" style="background:#b87d65"></span> Terracotta Clay
                </button>
              </div>
            </div>

            <!-- Flooring Type -->
            <div>
              <label class="block text-xs font-bold tracking-wider uppercase text-cyan-electric mb-2.5">2. Flooring Material</label>
              <div class="grid grid-cols-2 gap-2">
                <button type="button" data-floor="#9c7a54|Natural Oak" class="studio-floor-btn active flex items-center gap-2.5 p-2.5 rounded-xl border border-cyan-electric bg-cyan-electric/10 text-xs font-medium text-white">
                  <span class="w-5 h-5 rounded-md border border-white/30" style="background:#9c7a54"></span> Natural Oak
                </button>
                <button type="button" data-floor="#cbd5e1|Polished Terrazzo" class="studio-floor-btn flex items-center gap-2.5 p-2.5 rounded-xl border border-white/10 bg-void/60 text-xs font-medium text-slate-300">
                  <span class="w-5 h-5 rounded-md border border-white/30" style="background:#cbd5e1"></span> Polished Terrazzo
                </button>
                <button type="button" data-floor="#64748b|Matte Concrete" class="studio-floor-btn flex items-center gap-2.5 p-2.5 rounded-xl border border-white/10 bg-void/60 text-xs font-medium text-slate-300">
                  <span class="w-5 h-5 rounded-md border border-white/30" style="background:#64748b"></span> Matte Concrete
                </button>
                <button type="button" data-floor="#5c3d28|Smoked Walnut" class="studio-floor-btn flex items-center gap-2.5 p-2.5 rounded-xl border border-white/10 bg-void/60 text-xs font-medium text-slate-300">
                  <span class="w-5 h-5 rounded-md border border-white/30" style="background:#5c3d28"></span> Smoked Walnut
                </button>
              </div>
            </div>

            <!-- Furniture Arrangement -->
            <div>
              <label class="block text-xs font-bold tracking-wider uppercase text-cyan-electric mb-2.5">3. Furniture Arrangement</label>
              <div class="grid grid-cols-3 gap-2">
                <button type="button" data-layout="modern" class="studio-layout-btn active p-2.5 rounded-xl border border-cyan-electric bg-cyan-electric/10 text-xs font-semibold text-white">Modern</button>
                <button type="button" data-layout="family" class="studio-layout-btn p-2.5 rounded-xl border border-white/10 bg-void/60 text-xs font-semibold text-slate-300">Family</button>
                <button type="button" data-layout="minimal" class="studio-layout-btn p-2.5 rounded-xl border border-white/10 bg-void/60 text-xs font-semibold text-slate-300">Minimalist</button>
              </div>
            </div>

            <!-- Lighting Style -->
            <div>
              <label class="block text-xs font-bold tracking-wider uppercase text-cyan-electric mb-2.5">4. Lighting Mood</label>
              <div class="grid grid-cols-3 gap-2">
                <button type="button" data-light="daylight" class="studio-light-btn active p-2.5 rounded-xl border border-cyan-electric bg-cyan-electric/10 text-xs font-semibold text-white">Daylight</button>
                <button type="button" data-light="sunset" class="studio-light-btn p-2.5 rounded-xl border border-white/10 bg-void/60 text-xs font-semibold text-slate-300">Golden Hour</button>
                <button type="button" data-light="evening" class="studio-light-btn p-2.5 rounded-xl border border-white/10 bg-void/60 text-xs font-semibold text-slate-300">Warm Night</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 10. ARCHITECTURAL TECHNOLOGY PIPELINE -->
    <section id="pipeline" class="py-24">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="max-w-3xl reveal">
          <div class="text-xs font-bold tracking-[0.22em] uppercase text-cyan-electric mb-3">08 / Technical Architecture</div>
          <h2 class="font-display font-bold text-3xl sm:text-5xl tracking-tight text-white">
            From CAD blueprints to <span class="text-gradient">real-time spatial worlds.</span>
          </h2>
          <p class="text-slate-400 mt-4 text-base">
            A structured production pipeline ensures dimensional fidelity, physically based lighting, and smooth frame rates across VR headsets, desktop browsers, and mobile presentations.
          </p>
        </div>

        <!-- 7-Stage Pipeline Flow Diagram -->
        <div class="mt-12 grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-7 gap-3 reveal">
          <div class="glass-card rounded-2xl p-4 relative">
            <span class="font-mono text-[10px] text-cyan-electric">STEP 01</span>
            <h3 class="font-display font-bold text-sm text-white mt-1">CLIENT DRAWINGS</h3>
            <p class="text-xs text-slate-400 mt-1.5">2D plans, elevations, site photos & material moodboards.</p>
          </div>
          <div class="glass-card rounded-2xl p-4 relative">
            <span class="font-mono text-[10px] text-cyan-electric">STEP 02</span>
            <h3 class="font-display font-bold text-sm text-white mt-1">CAD / BIM INTERPRETATION</h3>
            <p class="text-xs text-slate-400 mt-1.5">Structural grid verification, wall heights & MEP clearance checks.</p>
          </div>
          <div class="glass-card rounded-2xl p-4 relative">
            <span class="font-mono text-[10px] text-cyan-electric">STEP 03</span>
            <h3 class="font-display font-bold text-sm text-white mt-1">3D RECONSTRUCTION</h3>
            <p class="text-xs text-slate-400 mt-1.5">Clean architectural topology, joinery & bespoke furniture assets.</p>
          </div>
          <div class="glass-card rounded-2xl p-4 relative">
            <span class="font-mono text-[10px] text-cyan-electric">STEP 04</span>
            <h3 class="font-display font-bold text-sm text-white mt-1">MATERIALS & LIGHTING</h3>
            <p class="text-xs text-slate-400 mt-1.5">PBR surface shaders, solar path simulation & interior luminaires.</p>
          </div>
          <div class="glass-card rounded-2xl p-4 relative">
            <span class="font-mono text-[10px] text-cyan-electric">STEP 05</span>
            <h3 class="font-display font-bold text-sm text-white mt-1">REAL-TIME VISUALISATION</h3>
            <p class="text-xs text-slate-400 mt-1.5">Baked global illumination, collision bounds & interactive logic.</p>
          </div>
          <div class="glass-card rounded-2xl p-4 relative">
            <span class="font-mono text-[10px] text-cyan-electric">STEP 06</span>
            <h3 class="font-display font-bold text-sm text-white mt-1">VR / MR EXPERIENCE</h3>
            <p class="text-xs text-slate-400 mt-1.5">Packaging for standalone headsets, PCVR, WebXR, or 360° web.</p>
          </div>
          <div class="glass-card rounded-2xl p-4 border-cyan-electric/40 bg-cyan-electric/10 relative">
            <span class="font-mono text-[10px] text-cyan-ice">STEP 07</span>
            <h3 class="font-display font-bold text-sm text-white mt-1">CLIENT PRESENTATION</h3>
            <p class="text-xs text-slate-300 mt-1.5">Guided walkthroughs, design sign-offs & buyer sales sessions.</p>
          </div>
        </div>

        <!-- Ecosystem Software & Hardware Toolchain -->
        <div class="mt-8 glass-panel rounded-3xl p-6 sm:p-8 reveal">
          <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 pb-5 border-b border-white/10">
            <div>
              <h3 class="font-display font-bold text-lg text-white">Supported Industry Toolchain & Spatial Platforms</h3>
              <p class="text-xs text-slate-400 mt-1">The exact software stack is selected per project based on source file format, visual fidelity target, and delivery device.</p>
            </div>
            <span class="text-xs font-mono text-cyan-electric">FLEXIBLE INTEROPERABLE STACK</span>
          </div>
          <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-5 gap-3 mt-5 text-xs">
            <div class="p-3 rounded-xl bg-void/70 border border-white/10"><strong class="text-white block">AutoCAD</strong><span class="text-slate-400">2D DWG drafting</span></div>
            <div class="p-3 rounded-xl bg-void/70 border border-white/10"><strong class="text-white block">Autodesk Revit</strong><span class="text-slate-400">BIM & parametric data</span></div>
            <div class="p-3 rounded-xl bg-void/70 border border-white/10"><strong class="text-white block">SketchUp</strong><span class="text-slate-400">Rapid massing & interiors</span></div>
            <div class="p-3 rounded-xl bg-void/70 border border-white/10"><strong class="text-white block">Blender</strong><span class="text-slate-400">Mesh optimisation & UV</span></div>
            <div class="p-3 rounded-xl bg-void/70 border border-white/10"><strong class="text-white block">Twinmotion</strong><span class="text-slate-400">Fast architectural RT</span></div>
            <div class="p-3 rounded-xl bg-void/70 border border-white/10"><strong class="text-white block">Unreal Engine</strong><span class="text-slate-400">Photorealistic VR & logic</span></div>
            <div class="p-3 rounded-xl bg-void/70 border border-white/10"><strong class="text-white block">Matterport</strong><span class="text-slate-400">Reality capture scanning</span></div>
            <div class="p-3 rounded-xl bg-void/70 border border-white/10"><strong class="text-white block">3DVista</strong><span class="text-slate-400">Interactive 360° tours</span></div>
            <div class="p-3 rounded-xl bg-void/70 border border-white/10"><strong class="text-white block">Navisworks</strong><span class="text-slate-400">BIM clash & coordination</span></div>
            <div class="p-3 rounded-xl bg-void/70 border border-white/10"><strong class="text-white block">OpenXR / WebXR</strong><span class="text-slate-400">Cross-headset & MR SDKs</span></div>
          </div>
        </div>
      </div>
    </section>

    <!-- 11. COMMERCIAL MODEL AND SERVICE CATALOGUE -->
    <section id="commercial" class="py-24 bg-midnight/90 border-y border-white/10">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex flex-col lg:flex-row lg:items-end justify-between gap-6 mb-12 reveal">
          <div class="max-w-2xl">
            <div class="text-xs font-bold tracking-[0.22em] uppercase text-cyan-electric mb-3">09 / Commercial Framework</div>
            <h2 class="font-display font-bold text-3xl sm:text-5xl tracking-tight text-white">
              Proposed Service Catalogue & <span class="text-gradient">Pricing Structure.</span>
            </h2>
            <p class="text-slate-400 mt-3 text-base">
              Structured to scale from single residential apartments to multi-tower developer showrooms.
            </p>
          </div>
          <div class="px-4 py-2.5 rounded-xl border border-cyan-electric/30 bg-cyan-electric/10 text-xs text-cyan-ice max-w-md">
            <strong>Transparency Notice:</strong> Figures below represent preliminary proposed pricing ranges for concept planning, not confirmed formal quotations. Final quotes depend on floor area and detail level.
          </div>
        </div>

        <!-- 4 Indicative Pricing Tiers -->
        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-5 reveal">
          <div class="glass-card rounded-3xl p-6 flex flex-col justify-between">
            <div>
              <span class="font-mono text-xs text-cyan-electric">LEVEL 01</span>
              <h3 class="font-display font-bold text-xl text-white mt-1">VYOMA VIEW</h3>
              <div class="font-display font-bold text-2xl sm:text-3xl text-white mt-4">₹8,000 – ₹15,000</div>
              <span class="text-[11px] text-slate-400 block mt-1">Indicative per-property range</span>
              <ul class="mt-5 space-y-2.5 text-xs text-slate-300 border-t border-white/10 pt-4">
                <li>• 360° panoramic room viewpoints</li>
                <li>• Hotspot room-to-room navigation</li>
                <li>• Web & mobile browser link</li>
                <li>• Ideal for resale & rental listings</li>
              </ul>
            </div>
            <a href="#enquiry" data-preset-level="VYOMA VIEW (₹8,000–₹15,000)" class="preset-enquiry-btn mt-6 block text-center py-2.5 rounded-xl border border-white/20 text-xs font-semibold hover:border-cyan-electric hover:text-cyan-electric transition-colors">Select in Project Brief</a>
          </div>

          <div class="glass-card rounded-3xl p-6 border-cyan-electric/50 bg-cyan-electric/[0.06] flex flex-col justify-between relative">
            <div>
              <div class="flex items-center justify-between">
                <span class="font-mono text-xs text-cyan-electric">LEVEL 02 • FLAGSHIP</span>
                <span class="px-2 py-0.5 rounded-full bg-cyan-electric text-void text-[10px] font-bold">CORE</span>
              </div>
              <h3 class="font-display font-bold text-xl text-white mt-1">VYOMA IMMERSION</h3>
              <div class="font-display font-bold text-2xl sm:text-3xl text-white mt-4">₹25,000 – ₹45,000</div>
              <span class="text-[11px] text-slate-400 block mt-1">Indicative per-unit range</span>
              <ul class="mt-5 space-y-2.5 text-xs text-slate-200 border-t border-white/10 pt-4">
                <li>• Full 1:1 scale navigable 3D interior</li>
                <li>• Free movement across all rooms</li>
                <li>• Realistic daylight & material shaders</li>
                <li>• VR headset & desktop ready</li>
              </ul>
            </div>
            <a href="#enquiry" data-preset-level="VYOMA IMMERSION (₹25,000–₹45,000)" class="preset-enquiry-btn mt-6 block text-center py-2.5 rounded-xl bg-cyan-electric text-void text-xs font-bold hover:opacity-95 transition-opacity">Select in Project Brief</a>
          </div>

          <div class="glass-card rounded-3xl p-6 flex flex-col justify-between">
            <div>
              <span class="font-mono text-xs text-cyan-electric">LEVEL 03</span>
              <h3 class="font-display font-bold text-xl text-white mt-1">VYOMA INTERACTIVE</h3>
              <div class="font-display font-bold text-2xl sm:text-3xl text-white mt-4">₹45,000 – ₹85,000</div>
              <span class="text-[11px] text-slate-400 block mt-1">Indicative per-project range</span>
              <ul class="mt-5 space-y-2.5 text-xs text-slate-300 border-t border-white/10 pt-4">
                <li>• Everything in VYOMA IMMERSION</li>
                <li>• Live wall, floor & finish switching</li>
                <li>• Alternate furniture & lighting sets</li>
                <li>• Built for bespoke homes & studios</li>
              </ul>
            </div>
            <a href="#enquiry" data-preset-level="VYOMA INTERACTIVE (₹45,000–₹85,000)" class="preset-enquiry-btn mt-6 block text-center py-2.5 rounded-xl border border-white/20 text-xs font-semibold hover:border-cyan-electric hover:text-cyan-electric transition-colors">Select in Project Brief</a>
          </div>

          <div class="glass-card rounded-3xl p-6 flex flex-col justify-between">
            <div>
              <span class="font-mono text-xs text-cyan-electric">LEVEL 04</span>
              <h3 class="font-display font-bold text-xl text-white mt-1">VYOMA REALITY</h3>
              <div class="font-display font-bold text-2xl sm:text-3xl text-white mt-4">₹75,000 – ₹1,50,000+</div>
              <span class="text-[11px] text-slate-400 block mt-1">Indicative custom scope range</span>
              <ul class="mt-5 space-y-2.5 text-xs text-slate-300 border-t border-white/10 pt-4">
                <li>• Mixed reality site & plot overlays</li>
                <li>• Exterior massing in real context</li>
                <li>• Selected BIM comparison workflows</li>
                <li>• Developer & enterprise presentations</li>
              </ul>
            </div>
            <a href="#enquiry" data-preset-level="VYOMA REALITY (₹75,000–₹1,50,000+)" class="preset-enquiry-btn mt-6 block text-center py-2.5 rounded-xl border border-white/20 text-xs font-semibold hover:border-cyan-electric hover:text-cyan-electric transition-colors">Select in Project Brief</a>
          </div>
        </div>

        <!-- 7 Revenue & Engagement Models -->
        <div class="mt-10 glass-panel rounded-3xl p-6 sm:p-8 reveal">
          <h3 class="font-display font-bold text-lg text-white mb-4">Commercial Engagement & Revenue Pathways</h3>
          <div class="grid sm:grid-cols-2 lg:grid-cols-4 gap-3 text-xs">
            <div class="p-3.5 rounded-xl bg-void/70 border border-white/10">
              <strong class="text-cyan-ice block mb-1">1. Individual Property Projects</strong>
              <span class="text-slate-400">One-time turnkey 3D/VR build for private homeowners or single villas.</span>
            </div>
            <div class="p-3.5 rounded-xl bg-void/70 border border-white/10">
              <strong class="text-cyan-ice block mb-1">2. Builder & Developer Contracts</strong>
              <span class="text-slate-400">Multi-unit packages covering 2BHK/3BHK/Penthouse typologies per project.</span>
            </div>
            <div class="p-3.5 rounded-xl bg-void/70 border border-white/10">
              <strong class="text-cyan-ice block mb-1">3. Agency Subscriptions</strong>
              <span class="text-slate-400">Monthly recurring quota of 360° panoramic tours for active real estate brokers.</span>
            </div>
            <div class="p-3.5 rounded-xl bg-void/70 border border-white/10">
              <strong class="text-cyan-ice block mb-1">4. Virtual Showroom Setups</strong>
              <span class="text-slate-400">On-site experience center kiosks & headset stations at developer sales offices.</span>
            </div>
            <div class="p-3.5 rounded-xl bg-void/70 border border-white/10">
              <strong class="text-cyan-ice block mb-1">5. Design Add-On Packs</strong>
              <span class="text-slate-400">Additional interior themes, modular kitchen variants & lighting scenarios.</span>
            </div>
            <div class="p-3.5 rounded-xl bg-void/70 border border-white/10">
              <strong class="text-cyan-ice block mb-1">6. Cloud Hosting & Maintenance</strong>
              <span class="text-slate-400">Annual web streaming, analytics, and model updates for active sales portals.</span>
            </div>
            <div class="p-3.5 rounded-xl bg-void/70 border border-white/10 sm:col-span-2">
              <strong class="text-cyan-ice block mb-1">7. Enterprise & Infrastructure Visualisation</strong>
              <span class="text-slate-400">Bespoke township, campus, industrial facility, and mixed-reality stakeholder briefings.</span>
            </div>
          </div>
        </div>

        <!-- Interactive Rework & Pre-Build ROI Calculator -->
        <div class="mt-8 glass-card rounded-3xl p-6 sm:p-8 border border-cyan-electric/35 reveal">
          <div class="grid lg:grid-cols-12 gap-8 items-center">
            <div class="lg:col-span-7 space-y-5">
              <div>
                <span class="font-mono text-xs text-cyan-electric">COMMERCIAL VALUE ESTIMATOR</span>
                <h3 class="font-display font-bold text-2xl text-white mt-1">Cost of Physical Rework vs. VYOMA Pre-Build Validation</h3>
                <p class="text-xs sm:text-sm text-slate-300 mt-1">
                  Modifying a wall partition, electrical point, or flooring tile inside VYOMA costs ₹0 in physical material waste. Estimate how much post-construction demolition rework is avoided by validating spaces before execution.
                </p>
              </div>

              <div class="space-y-4">
                <div>
                  <div class="flex justify-between text-xs mb-1.5">
                    <label for="roiAreaInput" class="text-slate-300 font-semibold">1. Property / Project Built-up Area</label>
                    <span id="roiAreaLabel" class="font-mono text-cyan-electric">2,200 sq.ft</span>
                  </div>
                  <input id="roiAreaInput" type="range" min="600" max="10000" step="100" value="2200" class="vyoma-slider w-full">
                </div>

                <div class="grid sm:grid-cols-2 gap-4">
                  <div>
                    <label for="roiFinishTier" class="block text-xs font-semibold text-slate-300 mb-1.5">2. Interior Specification Tier</label>
                    <select id="roiFinishTier" class="w-full px-3.5 py-2.5 rounded-xl bg-void border border-white/15 text-xs text-white focus:outline-none focus:border-cyan-electric">
                      <option value="1800">Standard Residential (₹1,800/sq.ft interior)</option>
                      <option value="2800" selected>Premium Villa / 3BHK (₹2,800/sq.ft interior)</option>
                      <option value="4500">Luxury Bespoke / Commercial (₹4,500/sq.ft interior)</option>
                    </select>
                  </div>
                  <div>
                    <div class="flex justify-between text-xs mb-1.5">
                      <label for="roiChangesInput" class="text-slate-300 font-semibold">3. Revisions Caught Pre-Build</label>
                      <span id="roiChangesLabel" class="font-mono text-cyan-electric">4 changes</span>
                    </div>
                    <input id="roiChangesInput" type="range" min="1" max="12" step="1" value="4" class="vyoma-slider w-full mt-2">
                  </div>
                </div>
              </div>
            </div>

            <div class="lg:col-span-5 glass-panel rounded-2xl p-6 border border-cyan-electric/30 space-y-4">
              <div class="text-[11px] font-mono uppercase tracking-widest text-cyan-electric">INDICATIVE PRE-BUILD SAVINGS</div>
              <div class="grid grid-cols-2 gap-3">
                <div class="p-3.5 rounded-xl bg-void/80 border border-white/10">
                  <span class="text-[11px] text-slate-400 block">Avoided Site Rework</span>
                  <strong id="roiSavingsOutput" class="font-display font-bold text-xl sm:text-2xl text-emerald-300 mt-1 block">₹3,42,000</strong>
                </div>
                <div class="p-3.5 rounded-xl bg-void/80 border border-white/10">
                  <span class="text-[11px] text-slate-400 block">Recommended VYOMA Tier</span>
                  <strong id="roiTierOutput" class="font-display font-bold text-sm sm:text-base text-cyan-ice mt-1.5 block">VYOMA IMMERSION</strong>
                </div>
              </div>
              <div class="p-3.5 rounded-xl bg-void/80 border border-white/10 text-xs text-slate-300 flex items-center justify-between">
                <span>Estimated Schedule Delay Saved:</span>
                <strong id="roiTimeSaved" class="font-mono text-white">~3.5 Weeks</strong>
              </div>
              <p class="text-[11px] text-slate-400 leading-relaxed">
                *Conceptual estimation based on typical 5%–9% on-site layout, tile, joinery, and electrical alteration costs during residential/commercial fit-outs.
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 12. PROJECT ROADMAP (6 PHASES) -->
    <section id="roadmap" class="py-24">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="max-w-3xl mb-12 reveal">
          <div class="text-xs font-bold tracking-[0.22em] uppercase text-cyan-electric mb-3">10 / Venture Development Roadmap</div>
          <h2 class="font-display font-bold text-3xl sm:text-5xl tracking-tight text-white">
            A disciplined path from <span class="text-gradient">prototype to ecosystem.</span>
          </h2>
          <p class="text-slate-400 mt-3 text-base">
            This roadmap outlines VYOMA's phased product and engineering vision—validating each capability through real-world architectural pilots before scaling.
          </p>
        </div>

        <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-5 reveal">
          <div class="glass-card rounded-3xl p-6 border-cyan-electric/40">
            <div class="flex items-center justify-between">
              <span class="font-mono text-xs font-bold text-cyan-electric">PHASE 01</span>
              <span class="px-2.5 py-0.5 rounded-full bg-cyan-electric/15 text-cyan-ice text-[10px] font-mono">INITIAL FOCUS</span>
            </div>
            <h3 class="font-display font-bold text-xl text-white mt-3">Foundation</h3>
            <p class="text-sm text-slate-300 mt-2 leading-relaxed">
              Develop a realistic residential prototype and establish the initial CAD-to-3D architectural workflow, lighting standards, and browser/VR testbeds.
            </p>
          </div>

          <div class="glass-card rounded-3xl p-6">
            <span class="font-mono text-xs font-bold text-cyan-electric">PHASE 02</span>
            <h3 class="font-display font-bold text-xl text-white mt-3">Immersive Experience</h3>
            <p class="text-sm text-slate-300 mt-2 leading-relaxed">
              Launch VYOMA VIEW panoramic visualisation and VYOMA IMMERSION navigable 3D walkthroughs for early homeowner, architect, and builder pilots.
            </p>
          </div>

          <div class="glass-card rounded-3xl p-6">
            <span class="font-mono text-xs font-bold text-cyan-electric">PHASE 03</span>
            <h3 class="font-display font-bold text-xl text-white mt-3">Interactive Environments</h3>
            <p class="text-sm text-slate-300 mt-2 leading-relaxed">
              Introduce real-time configurable materials, wall finishes, modular furniture sets, and lighting mood switching inside walkthroughs.
            </p>
          </div>

          <div class="glass-card rounded-3xl p-6">
            <span class="font-mono text-xs font-bold text-cyan-electric">PHASE 04</span>
            <h3 class="font-display font-bold text-xl text-white mt-3">Business Expansion</h3>
            <p class="text-sm text-slate-300 mt-2 leading-relaxed">
              Deploy multi-property virtual showrooms for developers, agency subscription workflows, and dedicated sales-gallery VR stations.
            </p>
          </div>

          <div class="glass-card rounded-3xl p-6">
            <span class="font-mono text-xs font-bold text-cyan-electric">PHASE 05</span>
            <h3 class="font-display font-bold text-xl text-white mt-3">Mixed Reality</h3>
            <p class="text-sm text-slate-300 mt-2 leading-relaxed">
              Explore on-site mixed reality architectural overlays, exterior plot massing previews, and selected BIM model comparison workflows.
            </p>
          </div>

          <div class="glass-card rounded-3xl p-6">
            <span class="font-mono text-xs font-bold text-cyan-electric">PHASE 06</span>
            <h3 class="font-display font-bold text-xl text-white mt-3">Spatial Ecosystem</h3>
            <p class="text-sm text-slate-300 mt-2 leading-relaxed">
              Expand toward connected digital twins, collaborative multi-user design reviews, and broader spatial computing applications.
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- 13. FUTURE POSSIBILITIES — BEYOND THE INITIAL PROJECT -->
    <section id="future" class="py-24 bg-gradient-to-b from-midnight via-navy/70 to-void border-t border-white/10">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="grid lg:grid-cols-12 gap-10 items-center reveal">
          <div class="lg:col-span-5 space-y-5">
            <div class="text-xs font-bold tracking-[0.22em] uppercase text-cyan-electric">11 / Long-Term Horizon</div>
            <h2 class="font-display font-bold text-3xl sm:text-5xl tracking-tight text-white leading-[1.08]">
              Beyond individual buildings: <span class="text-gradient">the spatial future.</span>
            </h2>
            <p class="text-slate-300 text-base leading-relaxed">
              As spatial computing hardware matures, VYOMA's core 3D reconstruction and real-time visualisation pipeline can extend into city-scale planning, industrial operations, and connected digital twins.
            </p>

            <!-- Custom Architectural Future Vision SVG Diagram -->
            <div class="rounded-2xl border border-cyan-electric/25 bg-void/80 p-4">
              <svg viewBox="0 0 460 200" class="w-full h-auto" role="img" aria-label="Wireframe spatial city and digital twin telemetry diagram">
                <g stroke="#73e3ed" stroke-opacity="0.25" stroke-width="1" fill="none">
                  <path d="M20 160 L230 95 L440 160 L230 195 Z"/>
                  <path d="M90 148 L230 105 L370 148"/>
                  <path d="M230 95 L230 195"/>
                </g>
                <!-- Stylized High-Rise Spatial Volumes -->
                <g stroke="#a5e6ff" stroke-width="1.3" fill="rgba(115,227,237,0.08)">
                  <polygon points="195,125 230,112 265,125 230,138"/>
                  <polygon points="195,125 195,45 230,32 230,112"/>
                  <polygon points="230,112 230,32 265,45 265,125"/>
                  <polygon points="130,138 155,128 180,138 155,148"/>
                  <polygon points="130,138 130,82 155,72 155,128"/>
                  <polygon points="155,128 155,72 180,82 180,138"/>
                  <polygon points="285,136 310,126 335,136 310,146"/>
                  <polygon points="285,136 285,74 310,64 310,126"/>
                  <polygon points="310,126 310,64 335,74 335,136"/>
                </g>
                <circle cx="230" cy="32" r="4" fill="#73e3ed"/>
                <line x1="230" y1="32" x2="315" y2="20" stroke="#73e3ed" stroke-dasharray="3 3"/>
                <text x="320" y="23" fill="#a5e6ff" font-family="monospace" font-size="10">DIGITAL TWIN NODE</text>
              </svg>
            </div>
          </div>

          <div class="lg:col-span-7 grid sm:grid-cols-2 gap-3.5">
            <div class="glass-card rounded-2xl p-4">
              <h3 class="font-display font-bold text-sm text-white">Virtual Architecture Exhibitions</h3>
              <p class="text-xs text-slate-400 mt-1">Global design biennales and student/studio showcases accessible from any headset.</p>
            </div>
            <div class="glass-card rounded-2xl p-4">
              <h3 class="font-display font-bold text-sm text-white">Smart-City Visualisation</h3>
              <p class="text-xs text-slate-400 mt-1">Transit corridors, zoning density, and environmental shadow studies at urban scale.</p>
            </div>
            <div class="glass-card rounded-2xl p-4">
              <h3 class="font-display font-bold text-sm text-white">Construction Progress Comparison</h3>
              <p class="text-xs text-slate-400 mt-1">Comparing approved 3D BIM models against periodic site captures over time.</p>
            </div>
            <div class="glass-card rounded-2xl p-4">
              <h3 class="font-display font-bold text-sm text-white">Infrastructure Planning</h3>
              <p class="text-xs text-slate-400 mt-1">Public stakeholder walkthroughs for stations, bridges, and civic campuses.</p>
            </div>
            <div class="glass-card rounded-2xl p-4">
              <h3 class="font-display font-bold text-sm text-white">Industrial Facility Training</h3>
              <p class="text-xs text-slate-400 mt-1">Virtual safety orientation and plant layout familiarisation before commissioning.</p>
            </div>
            <div class="glass-card rounded-2xl p-4">
              <h3 class="font-display font-bold text-sm text-white">Virtual Property Marketplaces</h3>
              <p class="text-xs text-slate-400 mt-1">Curated spatial portals where verified developments can be toured side by side.</p>
            </div>
            <div class="glass-card rounded-2xl p-4">
              <h3 class="font-display font-bold text-sm text-white">Remote Property Inspections</h3>
              <p class="text-xs text-slate-400 mt-1">Guided live co-browsing sessions for overseas investors and family decision-makers.</p>
            </div>
            <div class="glass-card rounded-2xl p-4">
              <h3 class="font-display font-bold text-sm text-white">Connected Digital Twins</h3>
              <p class="text-xs text-slate-400 mt-1">Linking spatial building geometry with energy, occupancy, and asset documentation.</p>
            </div>
            <div class="glass-card rounded-2xl p-4">
              <h3 class="font-display font-bold text-sm text-white">Collaborative Design Environments</h3>
              <p class="text-xs text-slate-400 mt-1">Architects, structural engineers, and clients reviewing 1:1 spaces together remotely.</p>
            </div>
            <div class="glass-card rounded-2xl p-4">
              <h3 class="font-display font-bold text-sm text-white">Spatial Computing Applications</h3>
              <p class="text-xs text-slate-400 mt-1">Next-generation mixed-reality interfaces for architecture and interior retail.</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 15. CONTACT AND PROJECT ENQUIRY (INTERACTIVE DEMONSTRATION) -->
    <section id="enquiry" class="py-24 border-t border-white/10">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="grid lg:grid-cols-12 gap-10 items-start reveal">
          <!-- Left Pitch Summary (5 Cols) -->
          <div class="lg:col-span-5 space-y-6">
            <div class="text-xs font-bold tracking-[0.22em] uppercase text-cyan-electric">12 / Initiate a Spatial Project</div>
            <h2 class="font-display font-bold text-3xl sm:text-5xl tracking-tight text-white leading-[1.06]">
              Don't just show the space. <span class="text-gradient">Let them experience it.</span>
            </h2>
            <p class="text-slate-300 text-base leading-relaxed">
              Use the interactive Project Brief Builder to structure your spatial visualisation requirements—whether for a pre-construction residence, developer showroom, or architectural review.
            </p>

            <div class="p-4 rounded-2xl border border-amber-400/30 bg-amber-400/10 text-xs text-amber-200 leading-relaxed">
              <strong>Demonstration Form Notice:</strong> This interactive brief builder operates locally in your browser to preview how VYOMA structures client enquiries. No external transmission occurs until connected to a live backend service.
            </div>

            <div class="glass-panel rounded-2xl p-5 space-y-3 text-xs text-slate-300">
              <div class="font-display font-bold text-sm text-white">What happens in a real VYOMA engagement?</div>
              <p>1. Share CAD floor plans (.DWG / .PDF), Revit/SketchUp models, or site photos.</p>
              <p>2. Confirm desired Experience Level (01 View to 04 Reality) and target delivery devices.</p>
              <p>3. Receive a scoped production timeline and formal quotation based on area and complexity.</p>
            </div>
          </div>

          <!-- Right Interactive Project Brief Form (7 Cols) -->
          <div class="lg:col-span-7 glass-card rounded-3xl p-6 sm:p-8">
            <form id="vyomaEnquiryForm" class="space-y-4">
              <div class="grid sm:grid-cols-2 gap-4">
                <div>
                  <label for="custName" class="block text-xs font-semibold text-slate-300 mb-1.5">Customer / Organisation Name *</label>
                  <input id="custName" name="custName" type="text" required placeholder="e.g., Aarav Mehta / Studio Axis" class="w-full px-4 py-3 rounded-xl bg-void border border-white/15 text-sm text-white placeholder-slate-500 focus:outline-none focus:border-cyan-electric">
                </div>
                <div>
                  <label for="custCategory" class="block text-xs font-semibold text-slate-300 mb-1.5">Customer Category *</label>
                  <select id="custCategory" name="custCategory" class="w-full px-4 py-3 rounded-xl bg-void border border-white/15 text-sm text-white focus:outline-none focus:border-cyan-electric">
                    <option value="Homeowner">Homeowner</option>
                    <option value="Builder / Real Estate Developer">Builder / Real Estate Developer</option>
                    <option value="Real Estate Agent / Reseller">Real Estate Agent / Reseller</option>
                    <option value="Architect / Interior Designer">Architect / Interior Designer</option>
                    <option value="Commercial / Hospitality / Enterprise">Commercial / Hospitality / Enterprise</option>
                  </select>
                </div>
              </div>

              <div class="grid sm:grid-cols-3 gap-4">
                <div>
                  <label for="projectType" class="block text-xs font-semibold text-slate-300 mb-1.5">Project Stage</label>
                  <select id="projectType" name="projectType" class="w-full px-4 py-3 rounded-xl bg-void border border-white/15 text-sm text-white focus:outline-none focus:border-cyan-electric">
                    <option value="Pre-Construction (From Plans)">Pre-Construction (From Plans)</option>
                    <option value="Under Construction">Under Construction</option>
                    <option value="Completed / Existing Space">Completed / Existing Space</option>
                    <option value="Renovation / Remodelling">Renovation / Remodelling</option>
                  </select>
                </div>
                <div>
                  <label for="propertyType" class="block text-xs font-semibold text-slate-300 mb-1.5">Property / Space Type</label>
                  <select id="propertyType" name="propertyType" class="w-full px-4 py-3 rounded-xl bg-void border border-white/15 text-sm text-white focus:outline-none focus:border-cyan-electric">
                    <option value="Residential Villa / Bungalow">Residential Villa / Bungalow</option>
                    <option value="Apartment / Penthouse">Apartment / Penthouse</option>
                    <option value="Commercial Office / Retail">Commercial Office / Retail</option>
                    <option value="Hospitality / Resort">Hospitality / Resort</option>
                    <option value="Industrial / Campus / Civic">Industrial / Campus / Civic</option>
                  </select>
                </div>
                <div>
                  <label for="projectSize" class="block text-xs font-semibold text-slate-300 mb-1.5">Approx. Project Size</label>
                  <input id="projectSize" name="projectSize" type="text" placeholder="e.g., 2,400 sq.ft / 3BHK" class="w-full px-4 py-3 rounded-xl bg-void border border-white/15 text-sm text-white placeholder-slate-500 focus:outline-none focus:border-cyan-electric">
                </div>
              </div>

              <div class="grid sm:grid-cols-2 gap-4">
                <div>
                  <label for="experienceLevelSelect" class="block text-xs font-semibold text-slate-300 mb-1.5">Desired VYOMA Experience Level</label>
                  <select id="experienceLevelSelect" name="experienceLevelSelect" class="w-full px-4 py-3 rounded-xl bg-void border border-white/15 text-sm text-white focus:outline-none focus:border-cyan-electric">
                    <option value="VYOMA VIEW (₹8,000–₹15,000)">Level 01 — VYOMA VIEW (360° Panorama)</option>
                    <option value="VYOMA IMMERSION (₹25,000–₹45,000)" selected>Level 02 — VYOMA IMMERSION (Navigable 3D)</option>
                    <option value="VYOMA INTERACTIVE (₹45,000–₹85,000)">Level 03 — VYOMA INTERACTIVE (Configurable)</option>
                    <option value="VYOMA REALITY (₹75,000–₹1,50,000+)">Level 04 — VYOMA REALITY (Mixed Reality)</option>
                  </select>
                </div>
                <div>
                  <label for="contactDetails" class="block text-xs font-semibold text-slate-300 mb-1.5">Preferred Contact (Email or Phone) *</label>
                  <input id="contactDetails" name="contactDetails" type="text" required placeholder="name@domain.com or +91 ..." class="w-full px-4 py-3 rounded-xl bg-void border border-white/15 text-sm text-white placeholder-slate-500 focus:outline-none focus:border-cyan-electric">
                </div>
              </div>

              <div>
                <label for="projectDesc" class="block text-xs font-semibold text-slate-300 mb-1.5">Project Description & Available Inputs</label>
                <textarea id="projectDesc" name="projectDesc" rows="3" placeholder="Mention available CAD drawings, SketchUp/Revit files, number of rooms, or presentation goals..." class="w-full px-4 py-3 rounded-xl bg-void border border-white/15 text-sm text-white placeholder-slate-500 focus:outline-none focus:border-cyan-electric"></textarea>
              </div>

              <div class="flex flex-wrap items-center justify-between gap-4 pt-2">
                <span class="text-[11px] text-slate-400">Generates an instant local project brief summary.</span>
                <button type="submit" class="px-7 py-3.5 rounded-full bg-gradient-to-r from-cyan-electric to-cyan-ice text-void font-display font-bold text-xs tracking-[0.16em] uppercase hover:opacity-95 transition-opacity">
                  Preview Project Brief →
                </button>
              </div>
            </form>

            <!-- Interactive Brief Preview Output (Replaces any alert() or fake submission) -->
            <div id="briefPreviewBox" class="hidden mt-6 p-6 rounded-2xl bg-void border border-cyan-electric/60 space-y-4 shadow-2xl">
              <div class="flex flex-wrap items-center justify-between gap-2 pb-3 border-b border-white/10">
                <div>
                  <span class="text-xs font-mono font-bold text-cyan-electric block">VYOMA SPATIAL PROJECT BRIEF & SCOPE CARD</span>
                  <span id="briefRefId" class="text-[11px] font-mono text-slate-400">REF: VYM-2026-8410</span>
                </div>
                <button id="closeBriefBtn" type="button" class="text-xs text-slate-400 hover:text-white px-2.5 py-1 rounded border border-white/10">Reset Form</button>
              </div>
              <div id="briefPreviewContent" class="text-xs text-slate-200 grid sm:grid-cols-2 gap-3 leading-relaxed"></div>
              <div class="pt-3 border-t border-white/10 flex flex-wrap items-center justify-between gap-3">
                <span class="text-[11px] text-amber-300">Demonstration Mode: Generated locally in browser.</span>
                <div class="flex flex-wrap gap-2">
                  <button id="printBriefBtn" type="button" class="px-3.5 py-2 rounded-xl border border-white/20 text-white text-xs font-semibold hover:border-cyan-electric transition-colors">
                    ⎙ Print / Save PDF Brief
                  </button>
                  <button id="copyBriefBtn" type="button" class="px-4 py-2 rounded-xl bg-cyan-electric text-void text-xs font-bold hover:opacity-95 transition-opacity">
                    Copy Brief to Clipboard
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>

  <!-- FOOTER -->
  <footer class="bg-void border-t border-white/10 py-12">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex flex-col md:flex-row items-start md:items-center justify-between gap-6">
      <div>
        <div class="font-display font-bold text-xl tracking-[0.22em] text-white">VY<span class="text-cyan-electric">O</span>MA</div>
        <p class="text-xs text-cyan-ice mt-1 tracking-wider uppercase">SEE THE UNBUILT. EXPERIENCE THE UNIMAGINED.</p>
        <p class="text-xs text-slate-500 mt-2">Spatial Visualisation Concept Platform • Experience Beyond Boundaries.</p>
      </div>
      <div class="text-xs text-slate-400 md:text-right space-y-1">
        <p>Architectural visualisations, property cards, and pricing ranges shown are conceptual demonstrations.</p>
        <p class="text-slate-500">© 2026 VYOMA Spatial Visualisation Venture Concept.</p>
      </div>
    </div>
  </footer>

  <!-- JAVASCRIPT APPLICATION LOGIC & THREE.JS SCENES -->
  <script type="module">
    // Helper for ARIA Live announcements
    function announceAria(msg) {
      const region = document.getElementById('vyomaAriaLive');
      if (region) region.textContent = msg;
    }

    // Helper for Keyboard Left/Right Arrow Navigation on Tablists
    function enableTablistKeyboardNav(selector, activateCallback) {
      const tabs = Array.from(document.querySelectorAll(selector));
      tabs.forEach((tab, idx) => {
        tab.addEventListener('keydown', (e) => {
          if (e.key === 'ArrowRight' || e.key === 'ArrowDown') {
            e.preventDefault();
            const next = (idx + 1) % tabs.length;
            tabs[next].focus();
            activateCallback(next);
          } else if (e.key === 'ArrowLeft' || e.key === 'ArrowUp') {
            e.preventDefault();
            const prev = (idx - 1 + tabs.length) % tabs.length;
            tabs[prev].focus();
            activateCallback(prev);
          }
        });
      });
    }

    // =========================================================================
    // 1. MOBILE NAVIGATION & SCROLL REVEAL
    // =========================================================================
    const mobileMenuBtn = document.getElementById('mobileMenuBtn');
    const mobileDrawer = document.getElementById('mobileDrawer');
    const menuIconOpen = document.getElementById('menuIconOpen');
    const menuIconClose = document.getElementById('menuIconClose');

    function setMobileMenu(open) {
      mobileDrawer.classList.toggle('hidden', !open);
      menuIconOpen.classList.toggle('hidden', open);
      menuIconClose.classList.toggle('hidden', !open);
      mobileMenuBtn.setAttribute('aria-expanded', String(open));
    }

    mobileMenuBtn.addEventListener('click', () => {
      const isOpen = mobileMenuBtn.getAttribute('aria-expanded') === 'true';
      setMobileMenu(!isOpen);
    });

    document.querySelectorAll('.mobile-nav-link').forEach(link => {
      link.addEventListener('click', () => setMobileMenu(false));
    });

    const revealObserver = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('visible');
          revealObserver.unobserve(entry.target);
        }
      });
    }, { threshold: 0.08 });

    document.querySelectorAll('.reveal').forEach(el => revealObserver.observe(el));

    // =========================================================================
    // 2. THE TRANSFORMATION — 6-STAGE INTERACTIVE ARCHITECTURAL COMPARISON
    // =========================================================================
    const stagesData = [
      {
        badge: 'STAGE 01 / ORTHOGRAPHIC CAD DRAWING',
        scale: '1:100 Flat Projection',
        subtitle: 'TRADITIONAL COMMUNICATION',
        title: '2D Architectural Floor Plan',
        desc: 'Communicates structural wall thicknesses, room labels, and linear dimensions. Accurate for engineers, yet forces buyers to mentally guess ceiling heights, daylight quality, and real furniture clearance.',
        params: ['2D width × length only', 'Flat symbolic outlines', 'Inferred from door arcs', 'Not visually represented', 'Text notes / schedules', 'Requires separate elevation'],
        svg: `
          <svg viewBox="0 0 640 340" class="w-full h-full">
            <g stroke="#1e293b" stroke-width="1"><line x1="0" y1="60" x2="640" y2="60"/><line x1="0" y1="280" x2="640" y2="280"/><line x1="100" y1="0" x2="100" y2="340"/><line x1="540" y1="0" x2="540" y2="340"/></g>
            <rect x="120" y="60" width="400" height="220" fill="none" stroke="#e2e8f0" stroke-width="5"/>
            <line x1="310" y1="60" x2="310" y2="280" stroke="#e2e8f0" stroke-width="4"/>
            <line x1="120" y1="170" x2="520" y2="170" stroke="#e2e8f0" stroke-width="4"/>
            <g stroke="#73e3ed" stroke-width="1.5" fill="none" stroke-dasharray="4 3">
              <rect x="140" y="80" width="150" height="70"/>
              <rect x="330" y="80" width="170" height="70"/>
              <rect x="140" y="190" width="150" height="70"/>
              <rect x="330" y="190" width="170" height="70"/>
            </g>
            <g fill="#94a3b8" font-family="monospace" font-size="11">
              <text x="165" y="118">MASTER BED 4.5×3.8m</text>
              <text x="360" y="118">LIVING 5.4×4.2m</text>
              <text x="165" y="228">KITCHEN 3.8×3.4m</text>
              <text x="360" y="228">DINING & TERRACE</text>
              <text x="275" y="45" fill="#73e3ed">← 14.50 m EXTERIOR SPAN →</text>
            </g>
          </svg>`
      },
      {
        badge: 'STAGE 02 / PERSPECTIVE STILL IMAGE',
        scale: 'Fixed Camera Angle',
        subtitle: 'VISUAL APPEARANCE ONLY',
        title: 'Static Architectural Render',
        desc: 'Introduces perspective depth, textures, and shadows from one chosen camera corner. Visually appealing for brochures, but blind spots remain hidden and viewers cannot test circulation paths.',
        params: ['Single-angle visual depth', 'Rendered fixed furniture', 'Hidden behind camera frame', 'Fixed sun angle snapshot', 'Photorealistic fixed palette', 'Single facade angle'],
        svg: `
          <svg viewBox="0 0 640 340" class="w-full h-full">
            <defs>
              <linearGradient id="st2Wall" x1="0" y1="0" x2="1" y2="1"><stop offset="0%" stop-color="#334155"/><stop offset="100%" stop-color="#1e293b"/></linearGradient>
              <linearGradient id="st2Light" x1="1" y1="0" x2="0" y2="1"><stop offset="0%" stop-color="#fde68a" stop-opacity="0.35"/><stop offset="100%" stop-color="#fde68a" stop-opacity="0"/></linearGradient>
            </defs>
            <polygon points="80,270 320,175 560,270 320,330" fill="#475569"/>
            <polygon points="80,270 80,85 320,25 320,175" fill="url(#st2Wall)"/>
            <polygon points="320,175 320,25 560,85 560,270" fill="#273549"/>
            <polygon points="365,65 510,98 510,205 365,172" fill="#0f2942" stroke="#73e3ed" stroke-width="2"/>
            <polygon points="365,65 510,98 310,320 120,265" fill="url(#st2Light)"/>
            <polygon points="145,250 245,210 315,238 215,278" fill="#64748b"/>
            <rect x="495" y="18" width="125" height="24" rx="12" fill="rgba(15,23,42,0.85)" stroke="#73e3ed"/>
            <text x="512" y="34" fill="#73e3ed" font-family="monospace" font-size="10">FIXED VIEWPOINT</text>
          </svg>`
      },
      {
        badge: 'STAGE 03 / VYOMA VIEW',
        scale: '360° Spherical Node',
        subtitle: 'STATIONARY PANORAMIC EXPLORATION',
        title: '360-Degree Panoramic Experience',
        desc: 'Places the viewer at the center of a room with full 360° rotational freedom. Linked hotspots allow jumping from Living to Kitchen to Bedroom—ideal for remote buyers on mobile or web.',
        params: ['Full 360° rotational context', 'Seen in true room context', 'Hotspot-to-hotspot jumps', 'Full window-to-room relationship', 'Realistic surface reflections', 'Balcony & facade nodes'],
        svg: `
          <svg viewBox="0 0 640 340" class="w-full h-full">
            <ellipse cx="320" cy="170" rx="260" ry="125" fill="none" stroke="#73e3ed" stroke-width="1.5" stroke-dasharray="6 4"/>
            <ellipse cx="320" cy="170" rx="170" ry="70" fill="rgba(115,227,237,0.06)" stroke="#a5e6ff" stroke-width="1"/>
            <path d="M120 225 L320 135 L520 225 L320 295 Z" fill="#1e293b" stroke="#64748b"/>
            <circle cx="320" cy="185" r="10" fill="#73e3ed"/>
            <circle cx="320" cy="185" r="22" fill="none" stroke="#73e3ed" stroke-width="1.5"/>
            <circle cx="205" cy="165" r="7" fill="#a5e6ff"/>
            <circle cx="435" cy="165" r="7" fill="#a5e6ff"/>
            <line x1="205" y1="165" x2="320" y2="185" stroke="#73e3ed" stroke-dasharray="3 3"/>
            <line x1="435" y1="165" x2="320" y2="185" stroke="#73e3ed" stroke-dasharray="3 3"/>
            <text x="255" y="34" fill="#73e3ed" font-family="monospace" font-size="11">360° LOOK-AROUND + HOTSPOTS</text>
          </svg>`
      },
      {
        badge: 'STAGE 04 / VYOMA IMMERSION',
        scale: '1:1 Real-Time 3D Scale',
        subtitle: 'FLAGSHIP WALKTHROUGH EXPERIENCE',
        title: 'Fully Navigable 3D Environment',
        desc: 'Unlocks unrestricted human-scale movement throughout the residence. Walk through doorways, feel corridor widths, check kitchen counter reach, and observe natural daylight from every angle.',
        params: ['1:1 true human eye-level scale', 'Physical clearance & reach tested', 'Continuous real-time walking', 'Dynamic glazing & sun angles', 'Full room-to-room continuity', 'Complete exterior + garden walk'],
        svg: `
          <svg viewBox="0 0 640 340" class="w-full h-full">
            <polygon points="90,260 320,145 550,260 320,325" fill="#1e293b" stroke="#94a3b8" stroke-width="1.5"/>
            <polygon points="90,260 90,75 320,15 320,145" fill="#28384f" stroke="#94a3b8"/>
            <polygon points="320,145 320,15 550,75 550,260" fill="#1b283b" stroke="#94a3b8"/>
            <path d="M185,265 Q280,235 320,205 T445,235" fill="none" stroke="#73e3ed" stroke-width="3" stroke-dasharray="8 5"/>
            <polygon points="440,228 456,236 442,244" fill="#73e3ed"/>
            <circle cx="185" cy="265" r="7" fill="#73e3ed"/>
            <text x="145" y="292" fill="#a5e6ff" font-family="monospace" font-size="10">FREE WALKING PATH (1:1 SCALE)</text>
          </svg>`
      },
      {
        badge: 'STAGE 05 / VYOMA INTERACTIVE',
        scale: 'Live Configurable 3D',
        subtitle: 'REAL-TIME DESIGN DECISIONS',
        title: 'Interactive Configurable Environment',
        desc: 'Transforms passive viewing into active co-design. Swap wall palettes, flooring materials, modular kitchen finishes, furniture layouts, and day/night lighting scenarios while standing inside the room.',
        params: ['Compare ceiling & volume options', 'Test multiple sofa & bed layouts', 'Evaluate flow per layout variant', 'Compare daylight vs. evening mood', 'Live swap tiles, wood & paint', 'Compare facade cladding options'],
        svg: `
          <svg viewBox="0 0 640 340" class="w-full h-full">
            <polygon points="100,255 320,145 540,255 320,320" fill="#6b533b" stroke="#e2e8f0"/>
            <polygon points="320,145 540,255 320,320" fill="#475569" opacity="0.85"/>
            <polygon points="100,255 100,75 320,15 320,145" fill="#9ab0a6"/>
            <polygon points="320,145 320,15 540,75 540,255" fill="#334155"/>
            <g transform="translate(45, 30)">
              <rect x="0" y="0" width="135" height="92" rx="10" fill="rgba(5,8,16,0.88)" stroke="#73e3ed"/>
              <text x="12" y="22" fill="#73e3ed" font-family="monospace" font-size="10">LIVE FINISHES</text>
              <circle cx="24" cy="45" r="9" fill="#9ab0a6"/><text x="42" y="49" fill="#fff" font-size="10">Sage Wall</text>
              <circle cx="24" cy="70" r="9" fill="#9c7a54"/><text x="42" y="74" fill="#fff" font-size="10">Oak Floor</text>
            </g>
          </svg>`
      },
      {
        badge: 'STAGE 06 / VYOMA REALITY',
        scale: 'Spatial Mixed Reality',
        subtitle: 'DIGITAL ARCHITECTURE ON REAL SITES',
        title: 'Mixed Reality Representation',
        desc: 'Anchors proposed 3D building massing and structural BIM elements directly onto a physical plot or real-world surroundings—bridging unbuilt architectural plans with actual site views and context.',
        params: ['True physical site alignment', 'Contextual scale on real land', 'Site access & setback verification', 'Real sun path & view corridors', 'Interior-to-real-view alignment', 'Proposed building on real plot'],
        svg: `
          <svg viewBox="0 0 640 340" class="w-full h-full">
            <!-- Real Plot Terrain Grid -->
            <polygon points="40,260 320,180 600,260 320,330" fill="#132a24" stroke="#2dd4bf" stroke-opacity="0.4"/>
            <line x1="160" y1="225" x2="480" y2="295" stroke="#2dd4bf" stroke-opacity="0.25"/>
            <line x1="480" y1="225" x2="160" y2="295" stroke="#2dd4bf" stroke-opacity="0.25"/>
            <!-- Anchored Proposed Architectural Massing -->
            <polygon points="210,225 320,180 430,225 320,265" fill="rgba(115,227,237,0.22)" stroke="#73e3ed" stroke-width="2"/>
            <polygon points="210,225 210,120 320,78 320,180" fill="rgba(115,227,237,0.14)" stroke="#73e3ed" stroke-width="2"/>
            <polygon points="320,180 320,78 430,120 430,225" fill="rgba(165,230,255,0.18)" stroke="#a5e6ff" stroke-width="2"/>
            <text x="195" y="45" fill="#73e3ed" font-family="monospace" font-size="11">PROPOSED BIM MASSING OVERLAID ON REAL PLOT</text>
          </svg>`
      }
    ];

    let currentStage = 0;
    const stageTabs = document.querySelectorAll('.stage-tab');
    const stageScrubber = document.getElementById('stageScrubber');

    function renderStage(idx) {
      currentStage = Math.max(0, Math.min(stagesData.length - 1, idx));
      const s = stagesData[currentStage];
      stageTabs.forEach((btn, i) => {
        const active = i === currentStage;
        btn.setAttribute('aria-selected', String(active));
        btn.className = active
          ? 'stage-tab active text-left p-3.5 rounded-2xl border border-cyan-electric bg-cyan-electric/15 transition-all'
          : 'stage-tab text-left p-3.5 rounded-2xl border border-white/10 bg-navy/50 hover:border-white/25 transition-all';
        btn.querySelector('span:first-child').className = active ? 'block font-mono text-[10px] text-cyan-electric' : 'block font-mono text-[10px] text-slate-400';
      });

      stageScrubber.value = String(currentStage);
      document.getElementById('stageBadge').textContent = s.badge;
      document.getElementById('stageScaleTag').textContent = s.scale;
      document.getElementById('stageSubtitle').textContent = s.subtitle;
      document.getElementById('stageTitle').textContent = s.title;
      document.getElementById('stageDesc').textContent = s.desc;
      document.getElementById('stageVisualContainer').innerHTML = s.svg;

      document.getElementById('paramDimensions').textContent = s.params[0];
      document.getElementById('paramFurniture').textContent = s.params[1];
      document.getElementById('paramPaths').textContent = s.params[2];
      document.getElementById('paramLight').textContent = s.params[3];
      document.getElementById('paramFinishes').textContent = s.params[4];
      document.getElementById('paramExterior').textContent = s.params[5];
      document.getElementById('stageStepCounter').textContent = `0${currentStage + 1} / 06`;
      document.getElementById('prevStageBtn').disabled = currentStage === 0;
      document.getElementById('nextStageBtn').disabled = currentStage === stagesData.length - 1;
      announceAria(`Transformation Stage ${currentStage + 1}: ${s.title}`);
    }

    stageTabs.forEach(btn => btn.addEventListener('click', () => {
      if (splitCurtainActive) toggleSplitCurtain(false);
      renderStage(Number(btn.dataset.stage));
    }));
    enableTablistKeyboardNav('.stage-tab', (idx) => {
      if (splitCurtainActive) toggleSplitCurtain(false);
      renderStage(idx);
    });
    stageScrubber.addEventListener('input', (e) => {
      if (splitCurtainActive) toggleSplitCurtain(false);
      renderStage(Number(e.target.value));
    });
    document.getElementById('prevStageBtn').addEventListener('click', () => renderStage(currentStage - 1));
    document.getElementById('nextStageBtn').addEventListener('click', () => renderStage(currentStage + 1));

    // Split-Screen CAD vs. Spatial Curtain Logic
    let splitCurtainActive = false;
    let splitPercent = 50;
    const splitBtn = document.getElementById('toggleSplitCurtainBtn');
    const splitWrapper = document.getElementById('splitCurtainWrapper');
    const splitLeftClip = document.getElementById('splitCurtainLeftClip');
    const splitDivider = document.getElementById('splitCurtainDivider');

    function updateSplitPosition(pct) {
      splitPercent = Math.max(5, Math.min(95, pct));
      splitLeftClip.style.clipPath = `inset(0 ${100 - splitPercent}% 0 0)`;
      splitDivider.style.left = `${splitPercent}%`;
    }

    function toggleSplitCurtain(forceState) {
      splitCurtainActive = typeof forceState === 'boolean' ? forceState : !splitCurtainActive;
      splitBtn.setAttribute('aria-pressed', String(splitCurtainActive));
      splitWrapper.classList.toggle('hidden', !splitCurtainActive);
      splitBtn.textContent = splitCurtainActive ? '✕ Exit Split Curtain' : '⇄ Split-Screen CAD vs. Spatial Curtain';
      if (splitCurtainActive) {
        document.getElementById('stageBadge').textContent = 'INTERACTIVE SPLIT CURTAIN / 2D CAD VS. 3D SPATIAL';
        announceAria('Split-screen CAD versus Spatial comparison curtain activated. Drag divider left or right.');
      } else {
        renderStage(currentStage);
      }
    }

    splitBtn.addEventListener('click', () => toggleSplitCurtain());

    let curtainDragging = false;
    splitWrapper.addEventListener('pointerdown', (e) => {
      curtainDragging = true;
      const rect = splitWrapper.getBoundingClientRect();
      updateSplitPosition(((e.clientX - rect.left) / rect.width) * 100);
      splitWrapper.setPointerCapture(e.pointerId);
    });
    splitWrapper.addEventListener('pointermove', (e) => {
      if (!curtainDragging) return;
      const rect = splitWrapper.getBoundingClientRect();
      updateSplitPosition(((e.clientX - rect.left) / rect.width) * 100);
    });
    splitWrapper.addEventListener('pointerup', () => { curtainDragging = false; });

    renderStage(0);

    // =========================================================================
    // 3. THE FOUR VYOMA EXPERIENCE LEVELS (INTERACTIVE MINI-DEMOS)
    // =========================================================================
    const expLevelsData = [
      {
        badge: 'LEVEL 01 — STATIONARY 360° PANORAMAS',
        title: 'VYOMA VIEW — Look Around Every Room Remotely',
        summary: 'A curated series of high-resolution 360-degree viewpoints connected via intuitive spatial hotspots. Visitors can look in every direction from fixed camera nodes—ideal for fast web sharing, mobile viewing, and remote NRI property previews.',
        distinction: 'Scope Note: VYOMA VIEW provides stationary panoramic viewpoints with hotspot transitions rather than unrestricted free-roaming 3D movement.',
        customers: ['Real estate brokers & resale agents', 'Residential apartment listings', 'Remote & NRI property buyers'],
        applications: ['Web & WhatsApp shareable tour links', 'Pre-visit property shortlisting', 'Hospitality suite & venue previews'],
        caption: 'Interactive Demo: Drag horizontally inside the panorama viewport to pan 360°, or click a room hotspot to switch viewpoints.'
      },
      {
        badge: 'LEVEL 02 — FLAGSHIP 1:1 REAL-TIME WALKTHROUGH',
        title: 'VYOMA IMMERSION — Step Inside at True Human Scale',
        summary: 'Enter a real-time 3D architectural environment built at 1:1 scale. Walk freely between rooms, experience ceiling heights, test corridor flow, and understand spatial volume naturally on VR headsets or desktop.',
        distinction: 'Flagship Capability: Full spatial freedom and human-perspective navigation across the entire unbuilt property.',
        customers: ['Homeowners building custom residences', 'Builders & developers launching pre-sales', 'Architects presenting spatial concepts'],
        applications: ['Pre-construction villa & apartment walkthroughs', 'Developer experience-center VR sessions', 'Spatial proportion & circulation validation'],
        caption: 'Interactive Demo: Click "Launch 3D Walkthrough" below to experience the guided human-scale camera tour in the 3D Residence above.'
      },
      {
        badge: 'LEVEL 03 — CONFIGURABLE IMMERSIVE SPACES',
        title: 'VYOMA INTERACTIVE — Customise Materials & Layouts Live',
        summary: 'Go beyond exploring a single fixed design. Switch wall colours, flooring planks, furniture configurations, and lighting moods in real time to compare design options inside the 3D environment.',
        distinction: 'Decision Accelerator: Eliminates costly post-construction changes by validating finishes before procurement.',
        customers: ['Bespoke homeowners & luxury buyers', 'Interior design & modular kitchen studios', 'Developers offering upgrade packages'],
        applications: ['Live finish & colour palette comparison', 'Modular kitchen & wardrobe configuration', 'Daylight vs. evening lighting evaluation'],
        caption: 'Interactive Demo: Toggle live wall and lighting presets below, or explore the full Interior Customisation Studio.'
      },
      {
        badge: 'LEVEL 04 — MIXED REALITY & SITE CONTEXT',
        title: 'VYOMA REALITY — Anchor Digital Architecture in the Real World',
        summary: 'Overlay proposed building exteriors, structural volumes, and selected BIM models onto physical plots and real-world surroundings—bridging digital design with real site context.',
        distinction: 'Mixed Reality vs. VR: Unlike conventional VR which replaces your surroundings completely, Mixed Reality blends virtual architecture onto real physical environments.',
        customers: ['Landowners & villa plot buyers', 'Urban planners & infrastructure teams', 'Architects & BIM project coordinators'],
        applications: ['Proposed building overlaid on an empty plot', 'Site setback, view-corridor & sun verification', 'Selected BIM & structural context reviews'],
        caption: 'Interactive Demo: Slide between the Existing Physical Plot and Proposed Mixed Reality Overlay.'
      }
    ];

    let panoOffset = 0;
    let panoRoom = 'Living Lounge';
    let lvl3Palette = 0;
    let mrBlend = 65;

    function renderExpDemo(idx) {
      const box = document.getElementById('expDemoContainer');
      if (idx === 0) {
        box.innerHTML = `
          <div id="panoViewport" class="pano-stage w-full h-full relative overflow-hidden bg-[#081220]">
            <svg id="panoSvg" viewBox="0 0 1200 370" preserveAspectRatio="xMidYMid slice" class="h-full w-[220%] max-w-none transition-transform duration-75" style="transform: translateX(${panoOffset}px)">
              <rect x="0" y="0" width="1200" height="210" fill="#16263d"/>
              <rect x="0" y="210" width="1200" height="160" fill="#3a2f26"/>
              <line x1="0" y1="210" x2="1200" y2="210" stroke="#73e3ed" stroke-opacity="0.35"/>
              <!-- Panoramic Architectural Glazing & Furniture -->
              <rect x="140" y="45" width="280" height="145" fill="#0d2b45" stroke="#73e3ed" stroke-width="2"/>
              <rect x="680" y="45" width="320" height="145" fill="#0d2b45" stroke="#73e3ed" stroke-width="2"/>
              <rect x="210" y="195" width="190" height="55" rx="8" fill="#52728a"/>
              <rect x="750" y="190" width="170" height="65" rx="6" fill="#7c5d41"/>
              <text x="230" y="115" fill="#a5e6ff" font-family="monospace" font-size="14">PANORAMIC VIEW: ${panoRoom.toUpperCase()}</text>
              <text x="765" y="115" fill="#a5e6ff" font-family="monospace" font-size="14">360° HORIZON</text>
            </svg>
            <!-- Hotspot Nodes -->
            <button type="button" data-pano-target="Living Lounge" class="pano-hotspot hotspot-dot absolute top-1/2 left-1/4 -translate-y-1/2 px-3 py-1.5 rounded-full bg-void/85 border border-cyan-electric text-[11px] font-semibold text-cyan-ice">
              ◉ Living Node
            </button>
            <button type="button" data-pano-target="Dining & Kitchen" class="pano-hotspot hotspot-dot absolute top-1/2 right-1/4 -translate-y-1/2 px-3 py-1.5 rounded-full bg-void/85 border border-cyan-electric text-[11px] font-semibold text-cyan-ice">
              ◉ Kitchen Node
            </button>
            <div class="absolute top-3 left-3 px-3 py-1 rounded-full glass-panel text-[11px] font-mono text-cyan-electric">
              360° VIEWPOINT: ${panoRoom} • DRAG TO PAN
            </div>
          </div>`;

        const vp = document.getElementById('panoViewport');
        const svg = document.getElementById('panoSvg');
        let dragging = false, startX = 0;
        vp.addEventListener('pointerdown', (e) => {
          if (e.target.closest('.pano-hotspot')) return;
          dragging = true;
          startX = e.clientX - panoOffset;
          vp.setPointerCapture(e.pointerId);
        });
        vp.addEventListener('pointermove', (e) => {
          if (!dragging) return;
          panoOffset = Math.max(-420, Math.min(0, e.clientX - startX));
          svg.style.transform = `translateX(${panoOffset}px)`;
        });
        vp.addEventListener('pointerup', () => { dragging = false; });
        vp.querySelectorAll('.pano-hotspot').forEach(btn => {
          btn.addEventListener('click', () => {
            panoRoom = btn.dataset.panoTarget;
            panoOffset = panoRoom === 'Living Lounge' ? 0 : -260;
            renderExpDemo(0);
          });
        });
      } else if (idx === 1) {
        box.innerHTML = `
          <div class="w-full h-full flex flex-col justify-between p-6 bg-gradient-to-br from-[#0c1a2e] to-[#060b14]">
            <div class="flex items-center justify-between">
              <span class="text-xs font-mono text-cyan-electric">1:1 HUMAN-SCALE WALKTHROUGH</span>
              <span class="text-xs font-mono text-slate-400">EYE HEIGHT: 1.65 m</span>
            </div>
            <svg viewBox="0 0 460 190" class="w-full h-44 my-auto">
              <polygon points="40,165 230,85 420,165 230,185" fill="#1b2d45" stroke="#73e3ed" stroke-opacity="0.5"/>
              <path d="M110,160 C175,145 215,125 265,128 C310,130 340,145 375,152" fill="none" stroke="#73e3ed" stroke-width="3" stroke-dasharray="6 4"/>
              <circle cx="110" cy="160" r="6" fill="#73e3ed"/>
              <circle cx="265" cy="128" r="6" fill="#a5e6ff"/>
              <circle cx="375" cy="152" r="6" fill="#73e3ed"/>
              <text x="85" y="180" fill="#cbd5e1" font-family="monospace" font-size="9">ENTRY</text>
              <text x="242" y="116" fill="#73e3ed" font-family="monospace" font-size="9">LIVING → DINING</text>
              <text x="350" y="170" fill="#cbd5e1" font-family="monospace" font-size="9">SUITE</text>
            </svg>
            <div class="flex items-center justify-between gap-3 pt-3 border-t border-white/10">
              <span class="text-xs text-slate-300">Experience continuous room-to-room flow</span>
              <a href="#explorer-3d" id="jumpWalkthroughBtn" class="px-4 py-2 rounded-full bg-cyan-electric text-void text-xs font-bold uppercase tracking-wider">Launch 3D Tour ↑</a>
            </div>
          </div>`;
        document.getElementById('jumpWalkthroughBtn').addEventListener('click', () => {
          setTimeout(() => document.getElementById('walkthroughBtn')?.click(), 650);
        });
      } else if (idx === 2) {
        const palettes = [
          { name: 'Nordic Oak & Alabaster', wall: '#d8d3c8', floor: '#9c7a54', light: 'Daylight' },
          { name: 'Graphite & Smoked Walnut', wall: '#334155', floor: '#5c3d28', light: 'Evening Warm' },
          { name: 'Sage Mist & Terrazzo', wall: '#9ab0a6', floor: '#cbd5e1', light: 'Soft Morning' }
        ];
        const p = palettes[lvl3Palette];
        box.innerHTML = `
          <div class="w-full h-full flex flex-col justify-between p-5 bg-[#080f1c]">
            <div class="flex items-center justify-between text-xs">
              <span class="font-mono text-cyan-electric">LIVE MATERIAL SWITCHER</span>
              <span class="text-slate-300">${p.name}</span>
            </div>
            <svg viewBox="0 0 460 200" class="w-full h-44 rounded-xl overflow-hidden border border-white/10">
              <polygon points="0,0 460,0 400,35 60,35" fill="#1e293b"/>
              <rect x="60" y="35" width="340" height="115" fill="${p.wall}"/>
              <polygon points="0,0 60,35 60,150 0,185" fill="${p.wall}" opacity="0.85"/>
              <polygon points="400,35 460,0 460,185 400,150" fill="${p.wall}" opacity="0.8"/>
              <polygon points="0,185 60,150 400,150 460,185 460,200 0,200" fill="${p.floor}"/>
              <rect x="135" y="112" width="190" height="42" rx="6" fill="#1e293b"/>
            </svg>
            <div class="grid grid-cols-3 gap-2">
              ${palettes.map((item, i) => `
                <button type="button" data-pal="${i}" class="lvl3-pal-btn py-2 px-2.5 rounded-xl text-[11px] font-semibold border ${i === lvl3Palette ? 'border-cyan-electric bg-cyan-electric/20 text-white' : 'border-white/10 bg-void text-slate-400'}">
                  Option 0${i + 1}
                </button>`).join('')}
            </div>
          </div>`;
        box.querySelectorAll('.lvl3-pal-btn').forEach(b => {
          b.addEventListener('click', () => {
            lvl3Palette = Number(b.dataset.pal);
            renderExpDemo(2);
          });
        });
      } else {
        box.innerHTML = `
          <div class="w-full h-full flex flex-col justify-between p-5 bg-[#07111a]">
            <div class="flex items-center justify-between text-xs">
              <span class="font-mono text-cyan-electric">MIXED REALITY PLOT OVERLAY</span>
              <span class="font-mono text-cyan-ice">OVERLAY OPACITY: ${mrBlend}%</span>
            </div>
            <svg viewBox="0 0 460 200" class="w-full h-44 rounded-xl border border-white/10 bg-[#0d1f1c]">
              <!-- Existing Physical Site Terrain & Trees -->
              <rect x="0" y="0" width="460" height="95" fill="#102538"/>
              <polygon points="0,95 460,95 460,200 0,200" fill="#19332b"/>
              <circle cx="65" cy="92" r="24" fill="#234d3e"/>
              <circle cx="395" cy="90" r="28" fill="#234d3e"/>
              <text x="20" y="185" fill="#6ee7b7" font-family="monospace" font-size="10">EXISTING PHYSICAL SITE CONTEXT</text>
              <!-- Proposed Architectural Massing Overlay -->
              <g opacity="${mrBlend / 100}">
                <polygon points="145,145 230,112 315,145 230,175" fill="#73e3ed" fill-opacity="0.3" stroke="#73e3ed" stroke-width="2"/>
                <polygon points="145,145 145,72 230,42 230,112" fill="#73e3ed" fill-opacity="0.22" stroke="#73e3ed" stroke-width="2"/>
                <polygon points="230,112 230,42 315,72 315,145" fill="#a5e6ff" fill-opacity="0.26" stroke="#a5e6ff" stroke-width="2"/>
                <text x="165" y="30" fill="#73e3ed" font-family="monospace" font-size="10">PROPOSED VILLA BIM VOLUME</text>
              </g>
            </svg>
            <div class="flex items-center gap-3 text-xs text-slate-400">
              <span>Empty Plot</span>
              <input id="mrSlider" type="range" min="0" max="100" value="${mrBlend}" aria-label="Adjust mixed reality building overlay opacity" class="vyoma-slider w-full">
              <span class="text-cyan-electric">MR Overlay</span>
            </div>
          </div>`;
        document.getElementById('mrSlider').addEventListener('input', (e) => {
          mrBlend = Number(e.target.value);
          renderExpDemo(3);
        });
      }
    }

    function selectExpLevel(idx) {
      const item = expLevelsData[idx];
      document.querySelectorAll('.exp-tab').forEach((btn, i) => {
        const active = i === idx;
        btn.setAttribute('aria-selected', String(active));
        btn.className = active
          ? 'exp-tab active text-left p-5 rounded-2xl border border-cyan-electric bg-cyan-electric/15 transition-all'
          : 'exp-tab text-left p-5 rounded-2xl border border-white/10 bg-navy/50 hover:border-white/30 transition-all';
      });
      document.getElementById('expBadge').textContent = item.badge;
      document.getElementById('expTitle').textContent = item.title;
      document.getElementById('expSummary').textContent = item.summary;
      document.getElementById('expDistinction').textContent = item.distinction;
      document.getElementById('expDemoCaption').textContent = item.caption;
      document.getElementById('expCustomers').innerHTML = item.customers.map(c => `<li>${c}</li>`).join('');
      document.getElementById('expApplications').innerHTML = item.applications.map(a => `<li>${a}</li>`).join('');
      renderExpDemo(idx);
    }

    document.querySelectorAll('.exp-tab').forEach(btn => {
      btn.addEventListener('click', () => {
        const idx = Number(btn.dataset.exp);
        selectExpLevel(idx);
        announceAria(`Selected ${expLevelsData[idx].title}`);
      });
    });
    enableTablistKeyboardNav('.exp-tab', (idx) => selectExpLevel(idx));
    selectExpLevel(0);

    // =========================================================================
    // 4. COMPLETE RANGE OF 12 INDUSTRIES
    // =========================================================================
    const industriesList = [
      { id: '01', cat: 'property', name: 'Residential Properties', desc: 'Walk through unbuilt apartments, villas, and plotted homes at 1:1 scale before foundation work.' },
      { id: '02', cat: 'enterprise', name: 'Commercial Buildings', desc: 'Leasing walkthroughs for corporate office floors, retail showrooms, and co-working hubs.' },
      { id: '03', cat: 'design', name: 'Architecture & Interior Design', desc: 'Collaborative spatial reviews of proportions, daylighting, joinery, and material palettes.' },
      { id: '04', cat: 'property', name: 'Hotels & Resorts', desc: 'Preview luxury suites, banquet halls, and destination masterplans for investors and guests.' },
      { id: '05', cat: 'enterprise', name: 'Industrial Facilities', desc: 'Visualise factory floor layouts, warehouse logistics paths, and safety zones pre-commissioning.' },
      { id: '06', cat: 'enterprise', name: 'Infrastructure', desc: 'Communicate bridges, transit hubs, and civic engineering proposals clearly to stakeholders.' },
      { id: '07', cat: 'enterprise', name: 'Educational Institutions', desc: 'Explore proposed university campuses, laboratories, auditoriums, and learning spaces.' },
      { id: '08', cat: 'property', name: 'Real Estate Exhibitions', desc: 'Showcase entire multi-project portfolios inside compact VR booths at property expos.' },
      { id: '09', cat: 'design', name: 'Renovation & Remodelling', desc: 'Compare existing room conditions side-by-side against proposed structural & interior upgrades.' },
      { id: '10', cat: 'design', name: 'Furniture & Modular Kitchens', desc: 'Test ergonomic counter heights, cabinet finishes, and bespoke furniture scale in context.' },
      { id: '11', cat: 'enterprise', name: 'Urban Planning & Public Spaces', desc: 'Evaluate streetscapes, public plazas, shadow corridors, and township walkability.' },
      { id: '12', cat: 'property', name: 'NRI Property Viewing', desc: 'Enable overseas buyers to inspect floor layouts, views, and finishes remotely with confidence.' }
    ];

    function renderIndustries(filter = 'all') {
      const grid = document.getElementById('industriesGrid');
      const filtered = filter === 'all' ? industriesList : industriesList.filter(i => i.cat === filter);
      grid.innerHTML = filtered.map(ind => `
        <article class="glass-card rounded-2xl p-5 flex flex-col justify-between">
          <div>
            <div class="flex items-center justify-between mb-3">
              <span class="font-mono text-xs text-cyan-electric">${ind.id}</span>
              <svg class="w-5 h-5 text-cyan-ice/70" fill="none" stroke="currentColor" stroke-width="1.6" viewBox="0 0 24 24" aria-hidden="true">
                <path stroke-linecap="round" stroke-linejoin="round" d="M3 21h18M5 21V7l7-4 7 4v14M9 21v-6h6v6"/>
              </svg>
            </div>
            <h3 class="font-display font-bold text-base text-white">${ind.name}</h3>
            <p class="text-xs text-slate-400 mt-2 leading-relaxed">${ind.desc}</p>
          </div>
          <div class="mt-4 pt-3 border-t border-white/10 text-[10px] font-mono uppercase tracking-wider text-slate-400">
            VYOMA Spatial Workflow
          </div>
        </article>
      `).join('');
    }

    document.querySelectorAll('.ind-filter-btn').forEach(btn => {
      btn.addEventListener('click', () => {
        document.querySelectorAll('.ind-filter-btn').forEach(b => {
          b.className = 'ind-filter-btn px-3.5 py-1.5 rounded-full text-xs font-semibold glass-panel text-slate-300 hover:border-cyan-electric/40';
        });
        btn.className = 'ind-filter-btn active px-3.5 py-1.5 rounded-full text-xs font-semibold bg-cyan-electric text-void';
        renderIndustries(btn.dataset.indFilter);
      });
    });
    renderIndustries('all');

    // =========================================================================
    // 5. CUSTOMER-SPECIFIC SOLUTIONS
    // =========================================================================
    const customerSolutions = [
      {
        segment: 'HOMEOWNERS & PRIVATE FAMILIES',
        headline: 'Eliminate guesswork before investing life savings into construction.',
        problem: 'Families struggle to judge room proportions, natural light, and kitchen/wardrobe ergonomics from flat 2D blueprints—leading to expensive mid-construction rework.',
        solution: 'VYOMA converts approved architectural plans into a 1:1 navigable 3D residence where families can walk every room and compare finish options early.',
        benefit: 'Confident design sign-off, fewer on-site modifications, and peace of mind for every family member.',
        example: 'Conceptual Example: A family planning a 3BHK duplex previews master bedroom wardrobe clearances and living room daylight before slab casting begins.'
      },
      {
        segment: 'BUILDERS & REAL ESTATE DEVELOPERS',
        headline: 'Sell upcoming inventory long before the sample flat is physically built.',
        problem: 'Physical sample apartments require high capital expenditure, take months to construct, and can only display one fixed interior layout.',
        solution: 'VYOMA creates a branded Virtual Property Showroom featuring navigable 3D walkthroughs of every unit typology (2BHK, 3BHK, Penthouse) at one experience center.',
        benefit: 'Earlier pre-launch buyer engagement, reduced physical mock-up overhead, and consistent presentations across sales teams.',
        example: 'Conceptual Example: A residential developer presents three apartment layouts and balcony views via VR headsets at their site office during pre-launch.'
      },
      {
        segment: 'REAL ESTATE AGENTS & RESELLERS',
        headline: 'Conduct high-clarity property tours for remote and NRI buyers.',
        problem: 'Coordinating physical site visits across busy schedules—or presenting properties to out-of-city and NRI buyers—slows down shortlisting.',
        solution: 'VYOMA VIEW 360° panoramic tours allow buyers to inspect room flow, dimensions, and condition remotely on any phone or laptop prior to an in-person visit.',
        benefit: 'More qualified physical visits, faster decision cycles, and stronger differentiation for exclusive listings.',
        example: 'Conceptual Example: An agency shares an interactive 360° hotspot tour of a resale villa with an overseas buyer, narrowing down final choices in a single call.'
      },
      {
        segment: 'ARCHITECTS & INTERIOR DESIGNERS',
        headline: 'Communicate spatial intent and secure faster client approvals.',
        problem: 'Clients often misread orthographic drawings or hesitate on bold material and lighting proposals until late in the execution phase.',
        solution: 'VYOMA transforms CAD, SketchUp, or Revit models into immersive design-review environments with switchable finishes and lighting moods.',
        benefit: 'Clearer client alignment, fewer revision bottlenecks, and elevated studio presentation quality.',
        example: 'Conceptual Example: An interior studio compares matte concrete vs. warm oak flooring live with a client during a 30-minute VR review session.'
      }
    ];

    function renderCustomerSolution(idx) {
      const c = customerSolutions[idx];
      document.querySelectorAll('.cust-tab').forEach((btn, i) => {
        const active = i === idx;
        btn.setAttribute('aria-selected', String(active));
        btn.className = active
          ? 'cust-tab active text-left p-5 rounded-2xl border border-cyan-electric bg-cyan-electric/15'
          : 'cust-tab text-left p-5 rounded-2xl border border-white/10 bg-navy/50 hover:border-white/30';
      });

      document.getElementById('customerDetailPanel').innerHTML = `
        <div class="space-y-6">
          <div>
            <span class="font-mono text-xs text-cyan-electric">${c.segment}</span>
            <h3 class="font-display font-bold text-2xl sm:text-3xl text-white mt-1.5">${c.headline}</h3>
          </div>
          <div class="grid md:grid-cols-3 gap-5">
            <div class="p-5 rounded-2xl bg-void/70 border border-white/10">
              <div class="text-[11px] font-bold tracking-widest uppercase text-rose-300 mb-2">The Existing Problem</div>
              <p class="text-xs sm:text-sm text-slate-300 leading-relaxed">${c.problem}</p>
            </div>
            <div class="p-5 rounded-2xl bg-void/70 border border-cyan-electric/30">
              <div class="text-[11px] font-bold tracking-widest uppercase text-cyan-electric mb-2">The VYOMA Solution</div>
              <p class="text-xs sm:text-sm text-slate-200 leading-relaxed">${c.solution}</p>
            </div>
            <div class="p-5 rounded-2xl bg-void/70 border border-white/10">
              <div class="text-[11px] font-bold tracking-widest uppercase text-emerald-300 mb-2">Practical Benefit</div>
              <p class="text-xs sm:text-sm text-slate-300 leading-relaxed">${c.benefit}</p>
            </div>
          </div>
          <div class="p-4 rounded-2xl bg-navy/70 border border-white/10 text-xs text-cyan-ice">
            ${c.example}
          </div>
        </div>`;
    }

    document.querySelectorAll('.cust-tab').forEach(btn => {
      btn.addEventListener('click', () => renderCustomerSolution(Number(btn.dataset.cust)));
    });
    enableTablistKeyboardNav('.cust-tab', (idx) => renderCustomerSolution(idx));
    renderCustomerSolution(0);

    // =========================================================================
    // 6. VIRTUAL PROPERTY SHOWROOM (CONCEPTUAL DEMONSTRATIONS)
    // =========================================================================
    const showroomProperties = [
      {
        id: 'prop-villa',
        tag: 'CONCEPTUAL VILLA',
        name: 'The Courtyard Pavilion',
        type: '3BHK Single-Level Villa',
        area: '2,450 sq.ft (228 m²)',
        style: 'Tropical Modernism',
        recommendedLevel: 'VYOMA IMMERSION + INTERACTIVE',
        highlights: ['Central landscaped courtyard with cross-ventilation', 'Open-plan living, dining & island kitchen', 'Covered timber pool deck and shaded verandah'],
        accent: '#73e3ed'
      },
      {
        id: 'prop-sky',
        tag: 'CONCEPTUAL APARTMENT',
        name: 'Aether Sky-Deck Residence',
        type: '2.5BHK High-Rise Unit',
        area: '1,480 sq.ft (137 m²)',
        style: 'Contemporary Urban Minimal',
        recommendedLevel: 'VYOMA IMMERSION',
        highlights: ['270-degree corner glazing with horizon sightlines', 'Convertible study / guest bedroom partition', 'Acoustic-insulated master suite with walk-in wardrobe'],
        accent: '#a5e6ff'
      },
      {
        id: 'prop-coastal',
        tag: 'CONCEPTUAL RETREAT',
        name: 'Horizon Slope House',
        type: '2BHK Contoured Weekend Home',
        area: '1,820 sq.ft (169 m²)',
        style: 'Warm Timber & Stone',
        recommendedLevel: 'VYOMA REALITY (PLOT OVERLAY)',
        highlights: ['Cantilevered living deck adapted to sloped terrain', 'Mixed reality site alignment for view-corridor check', 'Natural stone feature wall and clerestory daylighting'],
        accent: '#6ee7b7'
      },
      {
        id: 'prop-loft',
        tag: 'CONCEPTUAL STUDIO',
        name: 'Atelier Double-Height Loft',
        type: '1BHK Mezzanine Residence',
        area: '960 sq.ft (89 m²)',
        style: 'Architectural Graphite',
        recommendedLevel: 'VYOMA VIEW (360° TOUR)',
        highlights: ['5.2m double-height living volume', 'Floating steel staircase to mezzanine sleeping deck', 'Compact modular kitchen & integrated workspace'],
        accent: '#93c5fd'
      }
    ];

    let activeShowroomIdx = 0;

    function renderShowroom() {
      const grid = document.getElementById('showroomGrid');
      grid.innerHTML = showroomProperties.map((p, idx) => `
        <article class="glass-card rounded-3xl p-5 flex flex-col justify-between cursor-pointer ${idx === activeShowroomIdx ? 'border-cyan-electric bg-cyan-electric/10' : ''}" data-showroom-idx="${idx}">
          <div>
            <!-- Architectural Isometric Thumbnail SVG -->
            <div class="h-36 rounded-2xl bg-[#070f1d] border border-white/10 mb-4 flex items-center justify-center overflow-hidden">
              <svg viewBox="0 0 260 130" class="w-full h-full">
                <polygon points="40,95 130,52 220,95 130,122" fill="#172840" stroke="${p.accent}" stroke-width="1.5"/>
                <polygon points="40,95 40,48 130,14 130,52" fill="#1e3554" stroke="${p.accent}" stroke-opacity="0.7"/>
                <polygon points="130,52 130,14 220,48 220,95" fill="#132338" stroke="${p.accent}" stroke-opacity="0.7"/>
                <text x="16" y="20" fill="${p.accent}" font-family="monospace" font-size="9">${p.tag}</text>
              </svg>
            </div>
            <div class="text-[10px] font-mono text-cyan-electric">${p.type}</div>
            <h3 class="font-display font-bold text-lg text-white mt-0.5">${p.name}</h3>
            <div class="text-xs text-slate-400 mt-1">${p.area} • ${p.style}</div>
          </div>
          <button type="button" class="mt-4 w-full py-2.5 rounded-xl border ${idx === activeShowroomIdx ? 'border-cyan-electric bg-cyan-electric text-void font-bold' : 'border-white/15 text-slate-200 font-semibold'} text-xs">
            ${idx === activeShowroomIdx ? 'Inspecting Concept' : 'Inspect Layout'}
          </button>
        </article>
      `).join('');

      grid.querySelectorAll('[data-showroom-idx]').forEach(card => {
        card.addEventListener('click', () => {
          activeShowroomIdx = Number(card.dataset.showroomIdx);
          renderShowroom();
        });
      });

      const sel = showroomProperties[activeShowroomIdx];
      document.getElementById('showroomInspector').innerHTML = `
        <div class="grid lg:grid-cols-12 gap-6 items-center">
          <div class="lg:col-span-8 space-y-3">
            <div class="flex flex-wrap items-center gap-2">
              <span class="px-2.5 py-1 rounded-full bg-cyan-electric/15 border border-cyan-electric/30 text-cyan-electric font-mono text-[11px]">${sel.tag}</span>
              <span class="text-xs font-mono text-slate-400">RECOMMENDED TIER: ${sel.recommendedLevel}</span>
            </div>
            <h3 class="font-display font-bold text-2xl text-white">${sel.name} — ${sel.type}</h3>
            <p class="text-xs sm:text-sm text-slate-300">Floor Area: <strong class="text-white">${sel.area}</strong> • Interior Direction: <strong class="text-white">${sel.style}</strong></p>
            <ul class="grid sm:grid-cols-3 gap-3 pt-2">
              ${sel.highlights.map(h => `<li class="p-3 rounded-xl bg-void/70 border border-white/10 text-xs text-slate-300">• ${h}</li>`).join('')}
            </ul>
          </div>
          <div class="lg:col-span-4 flex flex-col gap-3">
            <a href="#explorer-3d" class="text-center py-3.5 px-5 rounded-full bg-gradient-to-r from-cyan-electric to-cyan-ice text-void font-display font-bold text-xs tracking-wider uppercase">
              Explore 3D Residence Prototype ↑
            </a>
            <a href="#enquiry" class="text-center py-3 px-5 rounded-full border border-white/20 text-xs font-semibold text-white hover:border-cyan-electric">
              Request Similar Concept Brief
            </a>
          </div>
        </div>`;
    }
    renderShowroom();

    // =========================================================================
    // 8. ENQUIRY PROJECT BRIEF DEMONSTRATION FORM + ROI CALCULATOR
    // =========================================================================
    // Pre-Build ROI & Rework Savings Calculator
    const roiAreaInput = document.getElementById('roiAreaInput');
    const roiFinishTier = document.getElementById('roiFinishTier');
    const roiChangesInput = document.getElementById('roiChangesInput');

    function updateRoiCalculator() {
      const area = Number(roiAreaInput.value);
      const rate = Number(roiFinishTier.value);
      const changes = Number(roiChangesInput.value);

      document.getElementById('roiAreaLabel').textContent = `${area.toLocaleString('en-IN')} sq.ft`;
      document.getElementById('roiChangesLabel').textContent = `${changes} ${changes === 1 ? 'change' : 'changes'}`;

      const baseInteriorValue = area * rate;
      const estimatedReworkSaved = Math.round((baseInteriorValue * 0.014 * changes) / 1000) * 1000;
      const weeksSaved = (changes * 0.85).toFixed(1);

      document.getElementById('roiSavingsOutput').textContent = `₹${estimatedReworkSaved.toLocaleString('en-IN')}`;
      document.getElementById('roiTimeSaved').textContent = `~${weeksSaved} Weeks`;

      let recTier = 'VYOMA IMMERSION';
      if (area > 4000 || rate >= 4500) recTier = 'VYOMA INTERACTIVE + REALITY';
      else if (changes >= 4 || rate >= 2800) recTier = 'VYOMA INTERACTIVE';
      document.getElementById('roiTierOutput').textContent = recTier;
    }

    [roiAreaInput, roiFinishTier, roiChangesInput].forEach(el => {
      el?.addEventListener('input', updateRoiCalculator);
    });
    updateRoiCalculator();

    document.querySelectorAll('.preset-enquiry-btn').forEach(btn => {
      btn.addEventListener('click', () => {
        const levelVal = btn.dataset.presetLevel;
        const select = document.getElementById('experienceLevelSelect');
        if (select) select.value = levelVal;
      });
    });

    const enquiryForm = document.getElementById('vyomaEnquiryForm');
    const briefBox = document.getElementById('briefPreviewBox');
    const briefContent = document.getElementById('briefPreviewContent');

    enquiryForm.addEventListener('submit', (e) => {
      e.preventDefault();
      const data = new FormData(enquiryForm);
      const refNum = `VYM-2026-${Math.floor(1000 + Math.random() * 9000)}`;
      document.getElementById('briefRefId').textContent = `REF: ${refNum}`;

      const tier = String(data.get('experienceLevelSelect'));
      let toolchain = 'AutoCAD → SketchUp/Blender → Unreal Engine 5 (1:1 VR/Desktop)';
      let timeline = '7–12 Working Days';
      if (tier.includes('VIEW')) {
        toolchain = 'CAD/3D Render → 360° Equirectangular Nodes → 3DVista / WebXR';
        timeline = '3–5 Working Days';
      } else if (tier.includes('INTERACTIVE')) {
        toolchain = 'Revit/CAD → Blender PBR → Unreal Engine Live Configurator';
        timeline = '12–18 Working Days';
      } else if (tier.includes('REALITY')) {
        toolchain = 'Revit/Navisworks BIM → Spatial Anchoring → OpenXR Mixed Reality';
        timeline = '15–25 Working Days';
      }

      const cards = [
        `<div class="p-3 rounded-xl bg-navy/60 border border-white/10"><span class="text-slate-400 block text-[10px]">CLIENT / ENTITY</span><strong class="text-white">${escapeHtml(data.get('custName'))} (${escapeHtml(data.get('custCategory'))})</strong></div>`,
        `<div class="p-3 rounded-xl bg-navy/60 border border-white/10"><span class="text-slate-400 block text-[10px]">PROPERTY & STAGE</span><strong class="text-white">${escapeHtml(data.get('propertyType'))} • ${escapeHtml(data.get('projectType'))}</strong></div>`,
        `<div class="p-3 rounded-xl bg-navy/60 border border-white/10"><span class="text-slate-400 block text-[10px]">SELECTED TIER & BAND</span><strong class="text-cyan-electric">${escapeHtml(tier)}</strong></div>`,
        `<div class="p-3 rounded-xl bg-navy/60 border border-white/10"><span class="text-slate-400 block text-[10px]">ESTIMATED DELIVERY</span><strong class="text-emerald-300">${timeline} (${escapeHtml(data.get('projectSize') || 'Standard Area')})</strong></div>`,
        `<div class="p-3 rounded-xl bg-navy/60 border border-white/10 sm:col-span-2"><span class="text-slate-400 block text-[10px]">RECOMMENDED TECHNICAL PIPELINE</span><strong class="text-cyan-ice">${toolchain}</strong></div>`,
        `<div class="p-3 rounded-xl bg-navy/60 border border-white/10 sm:col-span-2"><span class="text-slate-400 block text-[10px]">CONTACT & BRIEF NOTES</span><span class="text-slate-200">${escapeHtml(data.get('contactDetails'))} — ${escapeHtml(data.get('projectDesc') || 'Standard architectural CAD-to-VR spatial workflow.')}</span></div>`
      ];
      briefContent.innerHTML = cards.join('');
      briefBox.classList.remove('hidden');
      announceAria(`Project brief ${refNum} generated.`);
    });

    document.getElementById('closeBriefBtn').addEventListener('click', () => {
      briefBox.classList.add('hidden');
      enquiryForm.reset();
    });

    document.getElementById('printBriefBtn').addEventListener('click', () => {
      window.print();
    });

    document.getElementById('copyBriefBtn').addEventListener('click', () => {
      const refText = document.getElementById('briefRefId').textContent;
      const plainText = briefContent.innerText;
      const tempArea = document.createElement('textarea');
      tempArea.value = `VYOMA SPATIAL PROJECT BRIEF (${refText})\n${plainText}`;
      document.body.appendChild(tempArea);
      tempArea.select();
      document.execCommand('copy');
      document.body.removeChild(tempArea);
      const btn = document.getElementById('copyBriefBtn');
      btn.textContent = 'Copied to Clipboard ✓';
      setTimeout(() => { btn.textContent = 'Copy Brief to Clipboard'; }, 2200);
    });

    function escapeHtml(str) {
      return String(str || '').replace(/[&<>"']/g, m => ({
        '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;'
      })[m]);
    }

    // =========================================================================
    // 9. THREE.JS REALISTIC ARCHITECTURAL 3D SCENES (HERO + FULL CUTAWAY VILLA)
    // =========================================================================
    const prefersReducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

    try {
      const THREE = await import('https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.module.js');

      // -----------------------------------------------------------------------
      // PROCEDURAL HTML5 CANVAS PBR TEXTURE GENERATOR
      // -----------------------------------------------------------------------
      function createProceduralTexture(type) {
        const c = document.createElement('canvas');
        c.width = 256;
        c.height = 256;
        const ctx = c.getContext('2d');

        if (type === 'wood') {
          ctx.fillStyle = '#8b6846';
          ctx.fillRect(0, 0, 256, 256);
          for (let i = 0; i < 64; i++) {
            ctx.fillStyle = i % 2 === 0 ? 'rgba(60,38,18,0.14)' : 'rgba(210,175,135,0.08)';
            ctx.fillRect(0, i * 4, 256, 2);
          }
          ctx.strokeStyle = 'rgba(30,18,8,0.35)';
          ctx.lineWidth = 2;
          for (let p = 0; p < 256; p += 32) {
            ctx.beginPath(); ctx.moveTo(0, p); ctx.lineTo(256, p); ctx.stroke();
          }
        } else if (type === 'marble') {
          ctx.fillStyle = '#e5ebf0';
          ctx.fillRect(0, 0, 256, 256);
          ctx.strokeStyle = 'rgba(100,116,139,0.28)';
          ctx.lineWidth = 2;
          for (let v = 0; v < 8; v++) {
            ctx.beginPath();
            ctx.moveTo(0, v * 36);
            ctx.bezierCurveTo(85, v * 36 + 24, 170, v * 36 - 20, 256, v * 36 + 12);
            ctx.stroke();
          }
        } else if (type === 'fabric') {
          ctx.fillStyle = '#4b6b82';
          ctx.fillRect(0, 0, 256, 256);
          ctx.fillStyle = 'rgba(255,255,255,0.06)';
          for (let x = 0; x < 256; x += 4) {
            ctx.fillRect(x, 0, 1, 256);
            ctx.fillRect(0, x, 256, 1);
          }
        } else if (type === 'concrete') {
          ctx.fillStyle = '#cfd8e2';
          ctx.fillRect(0, 0, 256, 256);
          for (let i = 0; i < 600; i++) {
            ctx.fillStyle = i % 2 === 0 ? 'rgba(30,41,59,0.06)' : 'rgba(255,255,255,0.08)';
            ctx.fillRect((i * 73) % 256, (i * 41) % 256, 3, 3);
          }
        }

        const tex = new THREE.CanvasTexture(c);
        tex.wrapS = THREE.RepeatWrapping;
        tex.wrapT = THREE.RepeatWrapping;
        tex.repeat.set(2, 2);
        return tex;
      }

      const woodTex = createProceduralTexture('wood');
      const marbleTex = createProceduralTexture('marble');
      const fabricTex = createProceduralTexture('fabric');
      const concreteTex = createProceduralTexture('concrete');

      // Viewport Visibility Flags (Pauses off-screen WebGL rendering)
      let heroCanvasVisible = true;
      let villaCanvasVisible = true;

      // -----------------------------------------------------------------------
      // A) HERO ARCHITECTURAL STAGE (WIREFRAME TO FURNISHED + LIGHTING)
      // -----------------------------------------------------------------------
      const heroCanvas = document.getElementById('heroCanvas');
      const heroScene = new THREE.Scene();
      heroScene.background = new THREE.Color(0x070e1b);
      heroScene.fog = new THREE.FogExp2(0x070e1b, 0.032);

      const heroCamera = new THREE.PerspectiveCamera(36, 1, 0.1, 100);
      const heroRenderer = new THREE.WebGLRenderer({ canvas: heroCanvas, antialias: true });
      heroRenderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
      heroRenderer.shadowMap.enabled = true;
      heroRenderer.shadowMap.type = THREE.PCFSoftShadowMap;
      heroRenderer.toneMapping = THREE.ACESFilmicToneMapping;
      heroRenderer.toneMappingExposure = 1.2;

      const heroHemi = new THREE.HemisphereLight(0xd8f1ff, 0x1b283b, 1.9);
      heroScene.add(heroHemi);

      const heroSun = new THREE.DirectionalLight(0xfff1d6, 3.0);
      heroSun.position.set(7, 11, 8);
      heroSun.castShadow = true;
      heroScene.add(heroSun);

      const heroAccentLight = new THREE.PointLight(0x73e3ed, 18, 20);
      heroAccentLight.position.set(-4, 3.5, 3);
      heroScene.add(heroAccentLight);

      const heroGroup = new THREE.Group();
      heroScene.add(heroGroup);

      const solidMeshes = [];
      const wireframeLines = [];

      function addHeroBlock(w, h, d, color, x, y, z, opts = {}) {
        const geo = new THREE.BoxGeometry(w, h, d);
        const mat = opts.glass
          ? new THREE.MeshPhysicalMaterial({ color: 0x73e3ed, transparent: true, opacity: 0.32, roughness: 0.1 })
          : new THREE.MeshStandardMaterial({ color, map: opts.tex || null, roughness: opts.rough ?? 0.65, metalness: opts.metal ?? 0.05 });
        const mesh = new THREE.Mesh(geo, mat);
        mesh.position.set(x, y, z);
        mesh.castShadow = !opts.glass;
        mesh.receiveShadow = true;
        heroGroup.add(mesh);
        solidMeshes.push(mesh);

        const edges = new THREE.EdgesGeometry(geo);
        const line = new THREE.LineSegments(edges, new THREE.LineBasicMaterial({ color: 0x73e3ed, transparent: true, opacity: 0.18 }));
        line.position.copy(mesh.position);
        heroGroup.add(line);
        wireframeLines.push(line);
        return mesh;
      }

      // Base Plinth & Terrace Deck
      addHeroBlock(9.2, 0.24, 6.8, 0x263547, 0, 0.12, 0);
      addHeroBlock(8.4, 0.1, 6.0, 0xffffff, 0, 0.28, 0, { tex: woodTex });
      // Pool strip
      addHeroBlock(2.4, 0.12, 4.4, 0x2b9eb3, 3.1, 0.26, 0.4, { glass: true });
      // Exterior Walls & Floating Roof Canopy
      addHeroBlock(6.2, 2.5, 0.18, 0xffffff, -1.0, 1.55, -2.6, { tex: concreteTex });
      addHeroBlock(0.18, 2.5, 5.2, 0xffffff, -4.0, 1.55, 0, { tex: concreteTex });
      addHeroBlock(6.6, 0.22, 5.6, 0x1e293b, -0.9, 2.9, 0);
      // Glazed Corner Window
      addHeroBlock(4.2, 2.2, 0.06, 0x73e3ed, 0.1, 1.45, 2.5, { glass: true });
      // Interior Living Furniture
      addHeroBlock(2.1, 0.48, 0.85, 0xffffff, -1.8, 0.56, 0.8, { tex: fabricTex });
      addHeroBlock(1.1, 0.22, 0.65, 0xffffff, -1.8, 0.43, -0.3, { tex: woodTex });
      addHeroBlock(1.8, 0.85, 0.7, 0xffffff, -2.5, 0.75, -1.8, { tex: marbleTex });

      const heroGrid = new THREE.GridHelper(26, 26, 0x2b4c66, 0x132234);
      heroScene.add(heroGrid);

      let heroWireframeMode = false;
      let heroEveningMode = false;

      document.getElementById('heroWireframeBtn').addEventListener('click', (e) => {
        heroWireframeMode = !heroWireframeMode;
        e.target.textContent = heroWireframeMode ? 'Furnished View' : 'Wireframe Blueprint';
        solidMeshes.forEach(m => { m.visible = !heroWireframeMode; });
        wireframeLines.forEach(l => { l.material.opacity = heroWireframeMode ? 0.9 : 0.18; });
      });

      document.getElementById('heroLightBtn').addEventListener('click', (e) => {
        heroEveningMode = !heroEveningMode;
        e.target.textContent = heroEveningMode ? 'Morning Sun' : 'Evening Light';
        heroSun.intensity = heroEveningMode ? 0.55 : 3.0;
        heroAccentLight.color.setHex(heroEveningMode ? 0xffb76b : 0x73e3ed);
        heroAccentLight.intensity = heroEveningMode ? 32 : 18;
      });

      let hDragging = false, hPrevX = 0, hPrevY = 0, hTheta = 0.65, hPhi = 1.05, hRadius = 13.2;
      let pointerTiltX = 0, pointerTiltY = 0;

      heroCanvas.addEventListener('pointerdown', (e) => {
        hDragging = true;
        hPrevX = e.clientX;
        hPrevY = e.clientY;
        heroCanvas.setPointerCapture(e.pointerId);
      });
      heroCanvas.addEventListener('pointermove', (e) => {
        const rect = heroCanvas.getBoundingClientRect();
        pointerTiltX = ((e.clientX - rect.left) / rect.width - 0.5) * 0.18;
        pointerTiltY = ((e.clientY - rect.top) / rect.height - 0.5) * 0.12;
        if (!hDragging) return;
        hTheta -= (e.clientX - hPrevX) * 0.008;
        hPhi = Math.max(0.45, Math.min(1.42, hPhi + (e.clientY - hPrevY) * 0.006));
        hPrevX = e.clientX;
        hPrevY = e.clientY;
      });
      heroCanvas.addEventListener('pointerup', () => { hDragging = false; });

      function resizeHero() {
        const w = heroCanvas.clientWidth;
        const h = heroCanvas.clientHeight;
        if (w && h) {
          heroCamera.aspect = w / h;
          heroCamera.updateProjectionMatrix();
          heroRenderer.setSize(w, h, false);
        }
      }
      new ResizeObserver(resizeHero).observe(heroCanvas);
      resizeHero();

      // -----------------------------------------------------------------------
      // B) REALISTIC MULTI-ROOM 3D PROPERTY EXPLORER (SECTION 4)
      // -----------------------------------------------------------------------
      const villaCanvas = document.getElementById('villaCanvas');
      const villaScene = new THREE.Scene();
      villaScene.background = new THREE.Color(0x091322);

      const villaCamera = new THREE.PerspectiveCamera(42, 1, 0.1, 120);
      const villaRenderer = new THREE.WebGLRenderer({ canvas: villaCanvas, antialias: true });
      villaRenderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
      villaRenderer.shadowMap.enabled = true;
      villaRenderer.shadowMap.type = THREE.PCFSoftShadowMap;
      villaRenderer.toneMapping = THREE.ACESFilmicToneMapping;
      villaRenderer.toneMappingExposure = 1.25;

      // Pause off-screen WebGL canvases using IntersectionObserver
      const webglVisibilityObserver = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.target === heroCanvas) heroCanvasVisible = entry.isIntersecting;
          if (entry.target === villaCanvas) villaCanvasVisible = entry.isIntersecting;
        });
      }, { threshold: 0.02 });
      webglVisibilityObserver.observe(heroCanvas);
      webglVisibilityObserver.observe(villaCanvas);

      // Lighting Rig (Controlled by Solar Azimuth & Time-of-Day Scrubber)
      const vHemi = new THREE.HemisphereLight(0xd9f0ff, 0x243247, 2.0);
      villaScene.add(vHemi);

      const vSun = new THREE.DirectionalLight(0xfff0d4, 3.1);
      vSun.position.set(9, 14, 10);
      vSun.castShadow = true;
      vSun.shadow.mapSize.set(1024, 1024);
      villaScene.add(vSun);

      const vWarmInterior = new THREE.PointLight(0xffb86c, 0, 22);
      vWarmInterior.position.set(0, 2.8, 0);
      villaScene.add(vWarmInterior);

      // Procedural PBR Materials Library
      const mOakFloor = new THREE.MeshStandardMaterial({ color: 0xffffff, map: woodTex, roughness: 0.58 });
      const mTileFloor = new THREE.MeshStandardMaterial({ color: 0xdbe4ec, map: marbleTex, roughness: 0.3 });
      const mExtWall = new THREE.MeshStandardMaterial({ color: 0xf1f5f9, map: concreteTex, roughness: 0.72 });
      const mIntWall = new THREE.MeshStandardMaterial({ color: 0xd5e0ea, map: concreteTex, roughness: 0.75 });
      const mDarkTrim = new THREE.MeshStandardMaterial({ color: 0x1e293b, roughness: 0.45, metalness: 0.25 });
      const mWood = new THREE.MeshStandardMaterial({ color: 0x8b6244, map: woodTex, roughness: 0.55 });
      const mFabric = new THREE.MeshStandardMaterial({ color: 0xffffff, map: fabricTex, roughness: 0.85 });
      const mLinen = new THREE.MeshStandardMaterial({ color: 0xf1f5f9, roughness: 0.8 });
      const mMarble = new THREE.MeshStandardMaterial({ color: 0xffffff, map: marbleTex, roughness: 0.22 });
      const mGlass = new THREE.MeshPhysicalMaterial({ color: 0x73e3ed, transparent: true, opacity: 0.34, roughness: 0.1 });
      const mGrass = new THREE.MeshStandardMaterial({ color: 0x1e4035, roughness: 0.9 });
      const mWater = new THREE.MeshPhysicalMaterial({ color: 0x248ea6, transparent: true, opacity: 0.78, roughness: 0.12 });
      const mShadowPlane = new THREE.MeshBasicMaterial({ color: 0x030712, transparent: true, opacity: 0.38 });

      // 5 Vertical Architectural Layers for Exploded Axonometric Slider
      const layer0Site = new THREE.Group();      // Layer 0: Site & Plinth
      const layer1Floors = new THREE.Group();    // Layer 1: Floor Finishes & Pool
      const layer2Furniture = new THREE.Group(); // Layer 2: Interior Furniture & Contact Shadows
      const layer3Walls = new THREE.Group();     // Layer 3: Structural Walls & Glazing
      const layer4Roof = new THREE.Group();      // Layer 4: Architectural Roof Pergola & Lighting Grid
      villaScene.add(layer0Site, layer1Floors, layer2Furniture, layer3Walls, layer4Roof);

      const wallMeshes = [];

      function makeBox(parent, w, h, d, mat, x, y, z, isWall = false) {
        const mesh = new THREE.Mesh(new THREE.BoxGeometry(w, h, d), mat);
        mesh.position.set(x, y, z);
        mesh.castShadow = mat !== mGlass && mat !== mShadowPlane;
        mesh.receiveShadow = true;
        parent.add(mesh);
        if (isWall) wallMeshes.push({ mesh, fullH: h, fullY: y });
        return mesh;
      }

      function addContactShadow(w, d, x, z) {
        const plane = new THREE.Mesh(new THREE.PlaneGeometry(w, d), mShadowPlane);
        plane.rotation.x = -Math.PI / 2;
        plane.position.set(x, 0.33, z);
        layer2Furniture.add(plane);
      }

      // LAYER 0: Exterior Landscaping Plot & Foundation Slab
      makeBox(layer0Site, 18, 0.14, 15, mGrass, 0, -0.07, 0);
      makeBox(layer0Site, 11.4, 0.26, 8.8, mDarkTrim, 0, 0.13, 0);

      // LAYER 1: Timber Terrace, Lap Pool & Room Floor Zones
      makeBox(layer1Floors, 11.0, 0.08, 2.2, mWood, 0, 0.28, 3.2);
      makeBox(layer1Floors, 4.4, 0.14, 1.4, mWater, 2.6, 0.26, 3.2);
      makeBox(layer1Floors, 4.4, 0.08, 3.4, mOakFloor, -3.2, 0.28, 0.4);   // Living Lounge
      makeBox(layer1Floors, 3.2, 0.08, 3.4, mOakFloor, 0.6, 0.28, 0.4);    // Dining Area
      makeBox(layer1Floors, 3.2, 0.08, 2.6, mTileFloor, 3.8, 0.28, 0.8);   // Kitchen
      makeBox(layer1Floors, 4.0, 0.08, 2.6, mOakFloor, -3.4, 0.28, -2.6);  // Master Bedroom
      makeBox(layer1Floors, 3.4, 0.08, 2.6, mOakFloor, 0.3, 0.28, -2.6);   // Guest Bedroom
      makeBox(layer1Floors, 3.4, 0.08, 2.6, mTileFloor, 3.7, 0.28, -2.6);  // Spa Bathroom

      // LAYER 3: Exterior Perimeter & Internal Partition Walls
      makeBox(layer3Walls, 11.0, 2.65, 0.18, mExtWall, 0, 1.6, -3.9, true);   // North Back Wall
      makeBox(layer3Walls, 0.18, 2.65, 6.0, mExtWall, -5.4, 1.6, -0.9, true); // West Wall
      makeBox(layer3Walls, 0.18, 2.65, 6.0, mExtWall, 5.4, 1.6, -0.9, true);  // East Wall
      makeBox(layer3Walls, 9.2, 2.45, 0.14, mIntWall, -0.8, 1.5, -1.3, true); // Corridor spine wall
      makeBox(layer3Walls, 0.14, 2.45, 2.6, mIntWall, -1.4, 1.5, -2.6, true); // Master / Guest divider
      makeBox(layer3Walls, 0.14, 2.45, 2.6, mIntWall, 2.0, 1.5, -2.6, true);  // Guest / Bath divider
      makeBox(layer3Walls, 0.14, 2.2, 1.8, mIntWall, 2.2, 1.38, 1.2, true);   // Kitchen partial screen

      // Front Terrace Glazing & Architectural Mullions
      makeBox(layer3Walls, 6.8, 2.2, 0.06, mGlass, -1.8, 1.4, 2.05, true);
      [-5.2, -2.9, -0.6, 1.6].forEach(mx => {
        makeBox(layer3Walls, 0.07, 2.25, 0.1, mDarkTrim, mx, 1.42, 2.05, true);
      });

      // LAYER 4: Architectural Roof Pergola Frame & Louvers
      makeBox(layer4Roof, 11.2, 0.12, 0.22, mDarkTrim, 0, 2.98, -3.9);
      makeBox(layer4Roof, 11.2, 0.12, 0.22, mDarkTrim, 0, 2.98, 2.05);
      makeBox(layer4Roof, 0.22, 0.12, 6.1, mDarkTrim, -5.4, 2.98, -0.9);
      makeBox(layer4Roof, 0.22, 0.12, 6.1, mDarkTrim, 5.4, 2.98, -0.9);
      for (let lx = -4.5; lx <= 4.5; lx += 1.5) {
        makeBox(layer4Roof, 0.08, 0.08, 5.9, mWood, lx, 2.96, -0.9);
      }

      // LAYER 2: Furniture Assets + Contact Shadows
      // 1. Living Lounge (-3.2, 0.4)
      addContactShadow(2.6, 1.2, -3.5, 1.15);
      makeBox(layer2Furniture, 2.3, 0.45, 0.85, mFabric, -3.5, 0.54, 1.15);
      makeBox(layer2Furniture, 2.3, 0.72, 0.18, mFabric, -3.5, 0.72, 1.5);
      makeBox(layer2Furniture, 0.85, 0.45, 1.15, mFabric, -4.4, 0.54, 0.25);
      addContactShadow(1.35, 0.85, -3.3, -0.05);
      makeBox(layer2Furniture, 1.15, 0.18, 0.65, mWood, -3.3, 0.42, -0.05);
      makeBox(layer2Furniture, 1.8, 0.42, 0.4, mDarkTrim, -3.3, 0.52, -1.05);

      // 2. Dining Area (0.6, 0.4)
      addContactShadow(2.1, 1.6, 0.6, 0.35);
      makeBox(layer2Furniture, 1.65, 0.1, 0.95, mWood, 0.6, 0.82, 0.35);
      makeBox(layer2Furniture, 0.1, 0.52, 0.1, mDarkTrim, 0.0, 0.56, 0.35);
      makeBox(layer2Furniture, 0.1, 0.52, 0.1, mDarkTrim, 1.2, 0.56, 0.35);
      [-0.1, 0.6, 1.3].forEach(cx => {
        makeBox(layer2Furniture, 0.42, 0.42, 0.42, mFabric, cx, 0.52, -0.35);
        makeBox(layer2Furniture, 0.42, 0.42, 0.42, mFabric, cx, 0.52, 1.05);
      });

      // 3. Kitchen & Island (3.8, 0.8)
      addContactShadow(2.4, 1.0, 3.8, 0.65);
      makeBox(layer2Furniture, 2.7, 0.88, 0.65, mLinen, 3.85, 0.76, -0.85);
      makeBox(layer2Furniture, 2.74, 0.08, 0.68, mMarble, 3.85, 1.22, -0.85);
      makeBox(layer2Furniture, 2.1, 0.86, 0.78, mDarkTrim, 3.8, 0.75, 0.65);
      makeBox(layer2Furniture, 2.16, 0.08, 0.84, mMarble, 3.8, 1.2, 0.65);
      [3.1, 3.8, 4.5].forEach(sx => makeBox(layer2Furniture, 0.34, 0.62, 0.34, mWood, sx, 0.62, 1.25));

      // 4. Master Bedroom (-3.4, -2.6)
      addContactShadow(2.2, 2.3, -3.5, -2.65);
      makeBox(layer2Furniture, 1.95, 0.38, 2.1, mWood, -3.5, 0.5, -2.65);
      makeBox(layer2Furniture, 1.85, 0.26, 1.98, mLinen, -3.5, 0.74, -2.62);
      makeBox(layer2Furniture, 2.05, 0.95, 0.14, mWood, -3.5, 0.82, -3.7);
      makeBox(layer2Furniture, 0.62, 0.12, 0.42, mFabric, -3.95, 0.92, -3.35);
      makeBox(layer2Furniture, 0.62, 0.12, 0.42, mFabric, -3.05, 0.92, -3.35);
      makeBox(layer2Furniture, 0.55, 2.1, 1.8, mWood, -5.0, 1.35, -2.6); // Wardrobe

      // 5. Guest Bedroom (0.3, -2.6)
      addContactShadow(1.9, 2.1, 0.3, -2.7);
      makeBox(layer2Furniture, 1.65, 0.36, 1.95, mWood, 0.3, 0.48, -2.7);
      makeBox(layer2Furniture, 1.58, 0.24, 1.85, mLinen, 0.3, 0.7, -2.68);
      makeBox(layer2Furniture, 0.55, 2.0, 1.4, mLinen, 1.6, 1.3, -2.7);

      // 6. Spa Bathroom (3.7, -2.6)
      addContactShadow(1.8, 0.9, 4.35, -3.35);
      makeBox(layer2Furniture, 1.65, 0.55, 0.78, mLinen, 4.35, 0.58, -3.35); // Freestanding Tub
      makeBox(layer2Furniture, 1.3, 0.78, 0.52, mWood, 2.85, 0.7, -3.5);     // Double Vanity
      makeBox(layer2Furniture, 1.34, 0.06, 0.55, mMarble, 2.85, 1.1, -3.5);
      makeBox(layer2Furniture, 0.06, 2.0, 1.1, mGlass, 3.45, 1.3, -2.1);     // Glass Shower Screen

      // Landscaping Trees
      function addTree(x, z) {
        const trunk = new THREE.Mesh(new THREE.CylinderGeometry(0.1, 0.14, 1.1, 10), mWood);
        trunk.position.set(x, 0.55, z);
        layer0Site.add(trunk);
        const crown = new THREE.Mesh(new THREE.SphereGeometry(0.68, 14, 12), mGrass);
        crown.position.set(x, 1.45, z);
        crown.castShadow = true;
        layer0Site.add(crown);
      }
      addTree(-6.8, -3.5);
      addTree(-6.6, 2.8);
      addTree(6.8, -2.8);
      addTree(6.7, 3.2);

      // Room Highlight Zone Plane
      const highlightPlane = new THREE.Mesh(
        new THREE.PlaneGeometry(4.2, 3.2),
        new THREE.MeshBasicMaterial({ color: 0x73e3ed, transparent: true, opacity: 0.22, side: THREE.DoubleSide })
      );
      highlightPlane.rotation.x = -Math.PI / 2;
      highlightPlane.position.set(-3.2, 0.34, 0.4);
      layer1Floors.add(highlightPlane);

      const roomCatalog = {
        living: {
          name: 'Living Lounge & Glazing',
          dims: '5.4m × 4.2m (22.7 m²)',
          desc: 'Double-aspect living space opening onto the timber terrace with floor-to-ceiling low-E glazing and sectional seating.',
          pos: new THREE.Vector3(-3.2, 0.8, 0.4),
          size: [4.2, 3.2],
          camTheta: -0.45,
          camPhi: 0.92,
          camRadius: 11.5
        },
        kitchen: {
          name: 'Modular Kitchen & Island',
          dims: '4.1m × 3.6m (14.8 m²)',
          desc: 'Ergonomic parallel work counter with central breakfast island, bar seating, and direct dining service axis.',
          pos: new THREE.Vector3(3.8, 0.8, 0.8),
          size: [3.1, 2.5],
          camTheta: 0.65,
          camPhi: 0.92,
          camRadius: 11.0
        },
        dining: {
          name: 'Central Dining Pavilion',
          dims: '3.8m × 3.5m (13.2 m²)',
          desc: 'Six-seater dining zone positioned between the living lounge and kitchen with unobstructed garden sightlines.',
          pos: new THREE.Vector3(0.6, 0.8, 0.4),
          size: [3.1, 3.2],
          camTheta: 0.15,
          camPhi: 0.95,
          camRadius: 11.0
        },
        master: {
          name: 'Master Bedroom Suite',
          dims: '5.0m × 3.9m (19.5 m²)',
          desc: 'Private suite with king bed orientation, full-height built-in wardrobe wall, and acoustic separation from living zones.',
          pos: new THREE.Vector3(-3.4, 0.8, -2.6),
          size: [3.9, 2.5],
          camTheta: -0.75,
          camPhi: 0.88,
          camRadius: 11.2
        },
        bedroom2: {
          name: 'Guest / Family Bedroom',
          dims: '4.0m × 3.5m (14.0 m²)',
          desc: 'Quiet secondary bedroom with queen bed clearance, integrated wardrobe storage, and north-facing daylight.',
          pos: new THREE.Vector3(0.3, 0.8, -2.6),
          size: [3.3, 2.5],
          camTheta: 0.05,
          camPhi: 0.88,
          camRadius: 11.2
        },
        bathroom: {
          name: 'Spa Bathroom & Vanity',
          dims: '3.1m × 2.5m (7.8 m²)',
          desc: 'Wet-and-dry zoned bathroom featuring a freestanding soaking tub, frameless glass shower enclosure, and double vanity.',
          pos: new THREE.Vector3(3.7, 0.8, -2.6),
          size: [3.3, 2.5],
          camTheta: 0.85,
          camPhi: 0.88,
          camRadius: 11.2
        }
      };

      // Camera Orbit, First-Person & Smooth Interpolation State
      let vDragging = false, vPrevX = 0, vPrevY = 0;
      let vTheta = 0.55, vPhi = 0.96, vRadius = 15.8;
      let targetTheta = vTheta, targetPhi = vPhi, targetRadius = vRadius;
      const vLookTarget = new THREE.Vector3(0, 1.0, -0.3);
      const desiredLookTarget = new THREE.Vector3(0, 1.0, -0.3);
      let walkthroughActive = false;
      let walkthroughClock = 0;

      // First-Person Mode State (1.65m eye height)
      let firstPersonActive = false;
      const fpPos = new THREE.Vector3(-3.2, 1.65, 1.6);
      let fpYaw = 0;
      let fpPitch = -0.05;
      const fpKeys = { fwd: false, back: false, left: false, right: false };

      function stopSpecialModes() {
        walkthroughActive = false;
        firstPersonActive = false;
        document.getElementById('walkthroughStatus').classList.add('hidden');
        document.getElementById('fpTouchControls').classList.add('hidden');
      }

      function selectRoomByKey(roomKey) {
        const r = roomCatalog[roomKey];
        if (!r) return;
        document.querySelectorAll('.room-select-btn').forEach(b => {
          const isMatch = b.dataset.room === roomKey;
          b.className = isMatch
            ? 'room-select-btn active text-left p-3 rounded-xl border border-cyan-electric bg-cyan-electric/15 text-xs font-semibold text-white'
            : 'room-select-btn text-left p-3 rounded-xl border border-white/10 bg-void/60 hover:border-white/30 text-xs font-semibold text-slate-200';
        });

        document.getElementById('hudRoomName').textContent = r.name;
        document.getElementById('hudRoomDims').textContent = r.dims;
        document.getElementById('hudRoomDesc').textContent = r.desc;

        highlightPlane.position.set(r.pos.x, 0.34, r.pos.z);
        highlightPlane.scale.set(r.size[0] / 4.2, r.size[1] / 3.2, 1);

        if (firstPersonActive) {
          fpPos.set(r.pos.x, 1.65, r.pos.z + 0.8);
        } else {
          stopSpecialModes();
          desiredLookTarget.copy(r.pos);
          targetTheta = r.camTheta;
          targetPhi = r.camPhi;
          targetRadius = r.camRadius;
        }
        announceAria(`Focused on ${r.name}, dimensions ${r.dims}`);
      }

      document.querySelectorAll('.room-select-btn').forEach(btn => {
        btn.addEventListener('click', () => selectRoomByKey(btn.dataset.room));
      });

      // Clickable 2D Mini-Map Radar Teleport
      document.querySelectorAll('[data-map-room]').forEach(rect => {
        rect.addEventListener('click', (e) => {
          e.stopPropagation();
          selectRoomByKey(rect.dataset.mapRoom);
        });
      });

      document.getElementById('toggleMiniMapBtn').addEventListener('click', (e) => {
        const body = document.getElementById('miniMapBody');
        const hidden = body.classList.toggle('hidden');
        e.target.textContent = hidden ? 'Show' : 'Hide';
      });

      // Camera Perspective & First-Person Presets
      document.querySelectorAll('.cam-preset-btn').forEach(btn => {
        btn.addEventListener('click', () => {
          const mode = btn.dataset.cam;
          document.querySelectorAll('.cam-preset-btn').forEach(b => {
            b.className = 'cam-preset-btn px-3 py-1.5 rounded-full text-xs font-semibold glass-panel text-slate-200 hover:border-cyan-electric/50';
          });
          btn.className = 'cam-preset-btn px-3 py-1.5 rounded-full text-xs font-semibold bg-cyan-electric text-void shadow';

          if (mode === 'walkthrough') {
            firstPersonActive = false;
            document.getElementById('fpTouchControls').classList.add('hidden');
            walkthroughActive = !walkthroughActive;
            walkthroughClock = 0;
            const statusEl = document.getElementById('walkthroughStatus');
            statusEl.textContent = 'WALKTHROUGH TOUR ACTIVE';
            statusEl.classList.toggle('hidden', !walkthroughActive);
          } else if (mode === 'firstperson') {
            walkthroughActive = false;
            firstPersonActive = true;
            fpPos.set(desiredLookTarget.x, 1.65, desiredLookTarget.z + 1.1);
            fpYaw = 0;
            fpPitch = -0.05;
            const statusEl = document.getElementById('walkthroughStatus');
            statusEl.textContent = 'FIRST-PERSON 1.65m WALK (WASD / ARROWS)';
            statusEl.classList.remove('hidden');
            document.getElementById('fpTouchControls').classList.remove('hidden');
            announceAria('First-person 1.65 meter walk mode active. Use W A S D, arrow keys, or on-screen step buttons.');
          } else {
            stopSpecialModes();
            desiredLookTarget.set(0, 1.0, -0.3);
            if (mode === 'dollhouse') {
              targetTheta = 0.55; targetPhi = 0.96; targetRadius = 15.8;
            } else if (mode === 'exterior') {
              targetTheta = 0.85; targetPhi = 1.24; targetRadius = 16.8;
            }
          }
        });
      });

      // WASD / Arrow Keys & On-Screen Touch Pad for First-Person Mode
      window.addEventListener('keydown', (e) => {
        if (!firstPersonActive) return;
        if (['INPUT', 'TEXTAREA', 'SELECT'].includes(document.activeElement?.tagName)) return;
        if (e.key === 'w' || e.key === 'W' || e.key === 'ArrowUp') { fpKeys.fwd = true; e.preventDefault(); }
        if (e.key === 's' || e.key === 'S' || e.key === 'ArrowDown') { fpKeys.back = true; e.preventDefault(); }
        if (e.key === 'a' || e.key === 'A' || e.key === 'ArrowLeft') { fpKeys.left = true; e.preventDefault(); }
        if (e.key === 'd' || e.key === 'D' || e.key === 'ArrowRight') { fpKeys.right = true; e.preventDefault(); }
      });
      window.addEventListener('keyup', (e) => {
        if (e.key === 'w' || e.key === 'W' || e.key === 'ArrowUp') fpKeys.fwd = false;
        if (e.key === 's' || e.key === 'S' || e.key === 'ArrowDown') fpKeys.back = false;
        if (e.key === 'a' || e.key === 'A' || e.key === 'ArrowLeft') fpKeys.left = false;
        if (e.key === 'd' || e.key === 'D' || e.key === 'ArrowRight') fpKeys.right = false;
      });

      document.querySelectorAll('.fp-pad-btn').forEach(btn => {
        const dir = btn.dataset.fpMove;
        btn.addEventListener('pointerdown', (e) => { e.preventDefault(); fpKeys[dir] = true; });
        btn.addEventListener('pointerup', () => { fpKeys[dir] = false; });
        btn.addEventListener('pointerleave', () => { fpKeys[dir] = false; });
      });

      // Continuous Solar Azimuth & Time-of-Day Scrubber
      const solarSlider = document.getElementById('solarTimeSlider');
      const solarReadout = document.getElementById('solarTimeReadout');

      function updateSolarLighting(hourVal) {
        const hrs = Math.floor(hourVal);
        const mins = Math.round((hourVal - hrs) * 60);
        const ampm = hrs >= 12 ? 'PM' : 'AM';
        const dispHr = hrs > 12 ? hrs - 12 : (hrs === 0 ? 12 : hrs);
        const timeStr = `${String(dispHr).padStart(2, '0')}:${String(mins).padStart(2, '0')} ${ampm}`;

        // Normalize 6:00 -> 18:00 sun arc
        const sunProgress = Math.max(0, Math.min(1, (hourVal - 6) / 12.5));
        const angle = sunProgress * Math.PI;
        const sunX = -14 * Math.cos(angle);
        const sunY = Math.max(1.2, 15 * Math.sin(angle));
        const sunZ = 8 + 4 * Math.sin(angle);
        vSun.position.set(sunX, sunY, sunZ);

        let phaseLabel = 'Daylight';
        if (hourVal < 8) {
          phaseLabel = 'Sunrise Glow';
          vSun.color.setHex(0xffb36b);
          vSun.intensity = 2.1;
          vHemi.intensity = 1.4;
          vWarmInterior.intensity = 12;
          villaScene.background.setHex(0x0d1b2e);
        } else if (hourVal <= 15.5) {
          phaseLabel = 'Zenith Daylight';
          vSun.color.setHex(0xfff5e4);
          vSun.intensity = 3.2;
          vHemi.intensity = 2.1;
          vWarmInterior.intensity = 0;
          villaScene.background.setHex(0x0a1628);
        } else if (hourVal <= 18.5) {
          phaseLabel = 'Golden Hour';
          vSun.color.setHex(0xff9e44);
          vSun.intensity = 2.3;
          vHemi.intensity = 1.3;
          vWarmInterior.intensity = 24;
          villaScene.background.setHex(0x121829);
        } else {
          phaseLabel = 'Night Cove Light';
          vSun.color.setHex(0x3b82f6);
          vSun.intensity = 0.35;
          vHemi.intensity = 0.65;
          vWarmInterior.intensity = 42;
          villaScene.background.setHex(0x050912);
        }
        solarReadout.textContent = `${timeStr} • ${phaseLabel}`;
      }
      solarSlider.addEventListener('input', (e) => updateSolarLighting(Number(e.target.value)));
      updateSolarLighting(10.5);

      // Exploded Axonometric Layer View Slider
      const explodedSlider = document.getElementById('explodedViewSlider');
      const explodedReadout = document.getElementById('explodedReadout');
      explodedSlider.addEventListener('input', (e) => {
        const pct = Number(e.target.value);
        const t = pct / 100;
        explodedReadout.textContent = pct === 0 ? '0% Assembled' : `${pct}% Exploded`;
        layer0Site.position.y = 0;
        layer1Floors.position.y = t * 0.7;
        layer2Furniture.position.y = t * 1.8;
        layer3Walls.position.y = t * 3.2;
        layer4Roof.position.y = t * 4.8;
      });

      // Architectural Toggles
      let furnitureVisible = true;
      document.getElementById('toggleFurnitureBtn').addEventListener('click', (e) => {
        furnitureVisible = !furnitureVisible;
        layer2Furniture.visible = furnitureVisible;
        e.target.textContent = furnitureVisible ? 'Furnished' : 'Unfurnished Shell';
        e.target.setAttribute('aria-pressed', String(furnitureVisible));
      });

      let cutawayLowered = false;
      document.getElementById('toggleWallsBtn').addEventListener('click', (e) => {
        cutawayLowered = !cutawayLowered;
        wallMeshes.forEach(w => {
          w.mesh.scale.y = cutawayLowered ? 0.32 : 1.0;
          w.mesh.position.y = cutawayLowered ? 0.28 + (w.fullH * 0.32) / 2 : w.fullY;
        });
        e.target.textContent = cutawayLowered ? 'Cutaway Low' : 'Standard';
        e.target.setAttribute('aria-pressed', String(cutawayLowered));
      });

      let cadOverlayVisible = false;
      const cadOverlayEl = document.getElementById('cadDimensionsOverlay');
      const cadPins = Array.from(document.querySelectorAll('.cad-pin'));
      document.getElementById('toggleCadOverlayBtn').addEventListener('click', (e) => {
        cadOverlayVisible = !cadOverlayVisible;
        cadOverlayEl.classList.toggle('hidden', !cadOverlayVisible);
        e.target.textContent = cadOverlayVisible ? 'Visible (5 Pins)' : 'Hidden';
        e.target.setAttribute('aria-pressed', String(cadOverlayVisible));
      });

      // Pointer & Wheel Orbit / First-Person Look Controls on Villa Canvas
      villaCanvas.addEventListener('pointerdown', (e) => {
        if (walkthroughActive) stopSpecialModes();
        vDragging = true;
        vPrevX = e.clientX;
        vPrevY = e.clientY;
        villaCanvas.setPointerCapture(e.pointerId);
      });
      villaCanvas.addEventListener('pointermove', (e) => {
        if (!vDragging) return;
        const dx = e.clientX - vPrevX;
        const dy = e.clientY - vPrevY;
        if (firstPersonActive) {
          fpYaw -= dx * 0.006;
          fpPitch = Math.max(-0.6, Math.min(0.6, fpPitch - dy * 0.005));
        } else {
          targetTheta -= dx * 0.008;
          targetPhi = Math.max(0.35, Math.min(1.44, targetPhi + dy * 0.006));
        }
        vPrevX = e.clientX;
        vPrevY = e.clientY;
      });
      villaCanvas.addEventListener('pointerup', () => { vDragging = false; });
      villaCanvas.addEventListener('wheel', (e) => {
        e.preventDefault();
        if (firstPersonActive) return;
        if (walkthroughActive) stopSpecialModes();
        targetRadius = Math.max(6.8, Math.min(22, targetRadius + e.deltaY * 0.012));
      }, { passive: false });

      function resizeVilla() {
        const w = villaCanvas.clientWidth;
        const h = villaCanvas.clientHeight;
        if (w && h) {
          villaCamera.aspect = w / h;
          villaCamera.updateProjectionMatrix();
          villaRenderer.setSize(w, h, false);
        }
      }
      new ResizeObserver(resizeVilla).observe(villaCanvas);
      resizeVilla();

      const miniMapCamGroup = document.getElementById('miniMapCamGroup');
      const tempProjVec = new THREE.Vector3();

      // Main Unified Animation Loop (Respects Viewport Visibility)
      function animateScenes() {
        requestAnimationFrame(animateScenes);

        // 1. Hero Scene Update (Only when visible in viewport)
        if (heroCanvasVisible) {
          if (!hDragging && !prefersReducedMotion) {
            hTheta += 0.0018;
          }
          heroCamera.position.set(
            hRadius * Math.sin(hPhi) * Math.sin(hTheta) + pointerTiltX * 4,
            1.2 + hRadius * Math.cos(hPhi) - pointerTiltY * 3,
            hRadius * Math.sin(hPhi) * Math.cos(hTheta)
          );
          heroCamera.lookAt(-0.4, 1.2, 0);
          heroRenderer.render(heroScene, heroCamera);
        }

        // 2. Villa Explorer Update (Only when visible in viewport)
        if (!villaCanvasVisible) return;

        if (firstPersonActive) {
          const speed = 0.075;
          const forwardX = -Math.sin(fpYaw);
          const forwardZ = -Math.cos(fpYaw);
          const rightX = Math.cos(fpYaw);
          const rightZ = -Math.sin(fpYaw);

          if (fpKeys.fwd) { fpPos.x += forwardX * speed; fpPos.z += forwardZ * speed; }
          if (fpKeys.back) { fpPos.x -= forwardX * speed; fpPos.z -= forwardZ * speed; }
          if (fpKeys.left) { fpPos.x -= rightX * speed; fpPos.z -= rightZ * speed; }
          if (fpKeys.right) { fpPos.x += rightX * speed; fpPos.z += rightZ * speed; }

          // Bounding-box plot collision clamp
          fpPos.x = Math.max(-5.1, Math.min(5.1, fpPos.x));
          fpPos.z = Math.max(-3.6, Math.min(3.5, fpPos.z));

          villaCamera.position.copy(fpPos);
          vLookTarget.set(
            fpPos.x + forwardX * 4,
            fpPos.y + Math.sin(fpPitch) * 4,
            fpPos.z + forwardZ * 4
          );
          villaCamera.lookAt(vLookTarget);
        } else if (walkthroughActive) {
          walkthroughClock += 0.008;
          const waypoints = [
            { pos: new THREE.Vector3(-3.2, 1.35, 1.4), look: new THREE.Vector3(-3.2, 1.15, -0.6), label: 'Living Lounge' },
            { pos: new THREE.Vector3(0.4, 1.35, 1.2), look: new THREE.Vector3(0.8, 1.1, -0.4), label: 'Dining Area' },
            { pos: new THREE.Vector3(3.4, 1.35, 1.3), look: new THREE.Vector3(3.8, 1.1, -0.7), label: 'Kitchen & Island' },
            { pos: new THREE.Vector3(-2.6, 1.35, -1.8), look: new THREE.Vector3(-3.6, 1.0, -3.1), label: 'Master Suite' }
          ];
          const seg = Math.floor(walkthroughClock) % waypoints.length;
          const nextSeg = (seg + 1) % waypoints.length;
          const alpha = walkthroughClock % 1;
          const smoothAlpha = alpha * alpha * (3 - 2 * alpha);

          villaCamera.position.lerpVectors(waypoints[seg].pos, waypoints[nextSeg].pos, smoothAlpha);
          vLookTarget.lerpVectors(waypoints[seg].look, waypoints[nextSeg].look, smoothAlpha);
          villaCamera.lookAt(vLookTarget);
          document.getElementById('hudRoomName').textContent = `Walkthrough: ${waypoints[seg].label}`;
        } else {
          vTheta += (targetTheta - vTheta) * 0.08;
          vPhi += (targetPhi - vPhi) * 0.08;
          vRadius += (targetRadius - vRadius) * 0.08;
          vLookTarget.lerp(desiredLookTarget, 0.08);

          villaCamera.position.set(
            vLookTarget.x + vRadius * Math.sin(vPhi) * Math.sin(vTheta),
            vLookTarget.y + vRadius * Math.cos(vPhi),
            vLookTarget.z + vRadius * Math.sin(vPhi) * Math.cos(vTheta)
          );
          villaCamera.lookAt(vLookTarget);
        }

        // Update 2D Mini-Map Camera Radar Position & Cone Angle
        if (miniMapCamGroup) {
          const cx = Math.max(-6.0, Math.min(6.0, villaCamera.position.x));
          const cz = Math.max(-4.3, Math.min(4.0, villaCamera.position.z));
          const dx = vLookTarget.x - villaCamera.position.x;
          const dz = vLookTarget.z - villaCamera.position.z;
          const deg = (Math.atan2(dx, -dz) * 180) / Math.PI;
          miniMapCamGroup.setAttribute('transform', `translate(${cx.toFixed(2)}, ${cz.toFixed(2)}) rotate(${deg.toFixed(1)})`);
        }

        // Update 3D Projected CAD Dimension Overlay Pins
        if (cadOverlayVisible) {
          const cw = villaCanvas.clientWidth;
          const ch = villaCanvas.clientHeight;
          cadPins.forEach(pin => {
            const [wx, wy, wz] = pin.dataset.world.split(',').map(Number);
            tempProjVec.set(wx, wy + layer3Walls.position.y * 0.5, wz);
            tempProjVec.project(villaCamera);
            if (tempProjVec.z > 1) {
              pin.style.opacity = '0';
            } else {
              const px = (tempProjVec.x * 0.5 + 0.5) * cw;
              const py = (-tempProjVec.y * 0.5 + 0.5) * ch;
              pin.style.opacity = '1';
              pin.style.left = `${px}px`;
              pin.style.top = `${py}px`;
            }
          });
        }

        villaRenderer.render(villaScene, villaCamera);
      }
      animateScenes();

    } catch (err) {
      // Graceful fallback if Three.js CDN or WebGL is unavailable
      const fallbackHtml = `
        <div class="w-full h-full flex flex-col items-center justify-center p-8 text-center bg-navy/90">
          <div class="w-12 h-12 rounded-2xl bg-cyan-electric/15 border border-cyan-electric/40 flex items-center justify-center text-cyan-electric font-display font-bold mb-3">3D</div>
          <div class="font-display font-bold text-lg text-white">VYOMA Spatial Viewport</div>
          <p class="text-xs text-slate-300 max-w-md mt-2">Interactive WebGL 3D preview requires a WebGL-compatible browser and active network connection for the 3D engine.</p>
        </div>`;
      if (document.getElementById('heroCanvas')) document.getElementById('heroCanvas').outerHTML = fallbackHtml;
      if (document.getElementById('villaCanvas')) document.getElementById('villaCanvas').outerHTML = fallbackHtml;
    }
  </script>
</body>
</html>
