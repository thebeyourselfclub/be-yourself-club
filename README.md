<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>The Be Yourself Club — Quotes, Gratitude & Ambient Sounds</title>
  
  <!-- Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Caveat:wght@600;700&family=Fira+Code:wght@400;500&family=Outfit:wght@300;400;500;600;700&family=Playfair+Display:ital,wght@0,600;0,700;1,400&display=swap" rel="stylesheet">
  
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  
  <!-- Canvas Confetti CDN -->
  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>

  <!-- Lucide Icons -->
  <script src="https://unpkg.com/lucide@latest"></script>

  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          colors: {
            babyblue: {
              50: '#f0f8ff',
              100: '#e0f2fe',
              200: '#bae6fd',
              300: '#7dd3fc',
              400: '#38bdf8',
              500: '#0284c7',
              900: '#0c4a6e',
            },
            sunny: {
              50: '#fffbeb',
              100: '#fef3c7',
              200: '#fde68a',
              300: '#fcd34d',
              400: '#fbbf24',
              500: '#f59e0b',
            },
            sunset: {
              bg: '#0b0f19',
              card: 'rgba(23, 28, 44, 0.75)',
              border: 'rgba(245, 158, 11, 0.2)',
              amber: '#fbbf24',
              navy: '#1e1b4b',
              purple: '#2e1065',
              glow: 'rgba(245, 158, 11, 0.15)'
            }
          },
          fontFamily: {
            sans: ['Outfit', 'sans-serif'],
            serif: ['Playfair Display', 'serif'],
            handwriting: ['Caveat', 'cursive'],
            mono: ['Fira Code', 'monospace']
          },
          keyframes: {
            float: {
              '0%, 100%': { transform: 'translateY(0px)' },
              '50%': { transform: 'translateY(-8px)' },
            },
            fadeIn: {
              '0%': { opacity: '0', transform: 'translateY(12px)' },
              '100%': { opacity: '1', transform: 'translateY(0)' },
            },
            pulseSlow: {
              '0%, 100%': { opacity: '1' },
              '50%': { opacity: '0.6' }
            }
          },
          animation: {
            float: 'float 5s ease-in-out infinite',
            fadeIn: 'fadeIn 0.4s cubic-bezier(0.16, 1, 0.3, 1) forwards',
            pulseSlow: 'pulseSlow 3s ease-in-out infinite',
          }
        }
      }
    }
  </script>

  <style>
    /* Custom scrollbars */
    ::-webkit-scrollbar {
      width: 8px;
      height: 8px;
    }
    ::-webkit-scrollbar-track {
      background: rgba(240, 248, 255, 0.5);
    }
    .dark ::-webkit-scrollbar-track {
      background: #0b0f19;
    }
    ::-webkit-scrollbar-thumb {
      background: #bae6fd;
      border-radius: 4px;
    }
    .dark ::-webkit-scrollbar-thumb {
      background: #312e81;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: #7dd3fc;
    }

    /* Glassmorphism Styles */
    .glass-card {
      background: rgba(255, 255, 255, 0.85);
      backdrop-filter: blur(12px);
      border: 1px solid rgba(255, 255, 255, 0.6);
    }
    .dark .glass-card {
      background: rgba(23, 28, 44, 0.8);
      backdrop-filter: blur(14px);
      border: 1px solid rgba(245, 158, 11, 0.18);
    }

    .glass-nav {
      background: rgba(255, 255, 255, 0.88);
      backdrop-filter: blur(16px);
    }
    .dark .glass-nav {
      background: rgba(11, 15, 25, 0.88);
    }

    /* Toast Animation */
    .toast-slide {
      animation: toastIn 0.3s cubic-bezier(0.16, 1, 0.3, 1) forwards;
    }
    @keyframes toastIn {
      from { transform: translateY(100%) scale(0.9); opacity: 0; }
      to { transform: translateY(0) scale(1); opacity: 1; }
    }

    /* Range Slider Styling */
    input[type=range] {
      accent-color: #f59e0b;
    }

    /* Smooth theme transitions */
    body, header, main, footer, div, card, button, input, textarea {
      transition: background-color 0.3s ease, border-color 0.3s ease, color 0.3s ease;
    }
  </style>
</head>
<body class="bg-gradient-to-br from-babyblue-50 via-white to-sunny-50 text-slate-800 dark:from-slate-950 dark:via-indigo-950 dark:to-slate-900 dark:text-slate-100 min-h-screen flex flex-col font-sans selection:bg-sunny-200 selection:text-slate-900">

  <!-- Toast Notification Container -->
  <div id="toastContainer" class="fixed bottom-6 right-6 z-50 flex flex-col gap-2 pointer-events-none"></div>

  <!-- Header & Navigation -->
  <header class="sticky top-0 z-40 glass-nav shadow-sm border-b border-babyblue-100 dark:border-amber-900/30">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-3.5">
      <div class="flex flex-col md:flex-row md:items-center md:justify-between gap-4">
        
        <!-- Logo / Title -->
        <div class="flex items-center justify-between">
          <div class="flex items-center gap-3">
            <div class="w-11 h-11 rounded-2xl bg-gradient-to-tr from-sunny-300 via-amber-400 to-babyblue-300 dark:from-amber-500 dark:to-indigo-600 flex items-center justify-center shadow-md shadow-sunny-200/50 dark:shadow-amber-900/30 animate-float">
              <i data-lucide="sun" class="w-6 h-6 text-slate-900 dark:text-amber-100"></i>
            </div>
            <div>
              <h1 class="text-xl sm:text-2xl font-bold font-serif tracking-tight text-slate-900 dark:text-amber-100">The Be Yourself Club</h1>
              <p class="text-xs text-slate-500 dark:text-amber-200/70 font-medium">Embrace your uniqueness & celebrate daily growth.</p>
            </div>
          </div>

          <!-- Mobile Dark Toggle & Quick Sound trigger -->
          <div class="flex items-center gap-2 md:hidden">
            <button id="sunsetToggleMobile" class="p-2 rounded-xl bg-slate-100 dark:bg-slate-800 text-slate-700 dark:text-amber-300" title="Toggle Sunset Night Mode">
              <i data-lucide="moon" class="w-5 h-5 dark:hidden"></i>
              <i data-lucide="sun" class="w-5 h-5 hidden dark:block text-amber-300"></i>
            </button>
          </div>
        </div>

        <!-- Header Actions & Navigation Switcher -->
        <div class="flex items-center justify-between md:justify-end gap-2 sm:gap-3 flex-wrap">
          
          <!-- Section Switcher Tabs -->
          <div class="flex items-center bg-slate-100 dark:bg-slate-800/80 p-1 rounded-2xl border border-slate-200 dark:border-slate-700/60">
            <button id="navQuotesBtn" class="px-3.5 py-1.5 rounded-xl text-xs sm:text-sm font-semibold transition-all bg-white dark:bg-amber-500 text-slate-900 dark:text-slate-950 shadow-sm flex items-center gap-1.5">
              <i data-lucide="quote" class="w-3.5 h-3.5"></i>
              <span>Quotes</span>
            </button>
            <button id="navJournalBtn" class="px-3.5 py-1.5 rounded-xl text-xs sm:text-sm font-semibold transition-all text-slate-600 dark:text-slate-300 hover:text-slate-900 dark:hover:text-white flex items-center gap-1.5">
              <i data-lucide="book-open" class="w-3.5 h-3.5"></i>
              <span>Journal</span>
            </button>
          </div>

          <!-- Ambient Audio Widget Trigger -->
          <button id="ambientAudioBtn" class="relative flex items-center gap-2 px-3.5 py-2 rounded-2xl bg-amber-100 dark:bg-amber-950/80 hover:bg-amber-200 text-amber-900 dark:text-amber-200 font-medium text-xs sm:text-sm border border-amber-300/60 dark:border-amber-700/50 transition-all">
            <i data-lucide="waves" class="w-4 h-4 text-amber-600 dark:text-amber-400"></i>
            <span class="hidden sm:inline">Sounds</span>
            <span id="audioPlayingDot" class="hidden absolute -top-1 -right-1 w-3 h-3 bg-emerald-500 rounded-full animate-ping"></span>
            <span id="audioPlayingDotStatic" class="hidden absolute -top-1 -right-1 w-3 h-3 bg-emerald-500 rounded-full border-2 border-white dark:border-slate-900"></span>
          </button>

          <!-- Surprise Encouragement -->
          <button id="surpriseBtn" class="flex items-center gap-1.5 px-3.5 py-2 rounded-2xl bg-gradient-to-r from-sunny-300 to-sunny-400 hover:from-sunny-400 hover:to-sunny-500 dark:from-amber-500 dark:to-amber-600 text-slate-900 font-bold text-xs sm:text-sm shadow-sm transition-all transform hover:-translate-y-0.5 active:translate-y-0">
            <i data-lucide="sparkles" class="w-4 h-4"></i>
            <span class="hidden sm:inline">Boost</span>
          </button>

          <!-- Add Quote Modal -->
          <button id="openSubmitModalBtn" class="flex items-center gap-1.5 px-3.5 py-2 rounded-2xl bg-babyblue-100 dark:bg-indigo-900/60 hover:bg-babyblue-200 dark:hover:bg-indigo-800 text-slate-800 dark:text-indigo-200 font-semibold text-xs sm:text-sm transition-all border border-babyblue-200 dark:border-indigo-700/50">
            <i data-lucide="plus-circle" class="w-4 h-4 text-babyblue-600 dark:text-indigo-300"></i>
            <span class="hidden sm:inline">Add</span>
          </button>

          <!-- Sunset Night Mode Toggle (Desktop) -->
          <button id="sunsetToggle" class="hidden md:flex items-center justify-center p-2.5 rounded-2xl bg-slate-100 dark:bg-slate-800 text-slate-700 dark:text-amber-300 border border-slate-200 dark:border-slate-700 hover:scale-105 transition-all" title="Toggle Sunset Night Mode">
            <i data-lucide="moon" class="w-4 h-4 dark:hidden"></i>
            <i data-lucide="sun" class="w-4 h-4 hidden dark:block text-amber-300"></i>
          </button>

        </div>
      </div>

    </div>
  </header>

  <!-- Ambient Audio Floating Controls Drawer -->
  <div id="ambientDrawer" class="hidden fixed top-20 right-4 z-50 w-80 glass-card rounded-3xl p-5 shadow-2xl border border-amber-300/50 dark:border-amber-700/50 transition-all animate-fadeIn">
    <div class="flex items-center justify-between pb-3 border-b border-slate-200/80 dark:border-slate-700/60">
      <div class="flex items-center gap-2">
        <i data-lucide="headphones" class="w-4 h-4 text-amber-500"></i>
        <h3 class="font-bold text-sm text-slate-900 dark:text-amber-100">Ambient Nature Sounds</h3>
      </div>
      <button id="closeAmbientDrawer" class="p-1 rounded-lg text-slate-400 hover:text-slate-600 dark:hover:text-slate-200">
        <i data-lucide="x" class="w-4 h-4"></i>
      </button>
    </div>

    <div class="space-y-4 pt-4">
      <!-- Rain Control -->
      <div class="space-y-1.5">
        <div class="flex items-center justify-between text-xs font-semibold">
          <span class="flex items-center gap-2 text-slate-700 dark:text-slate-300">
            <i data-lucide="cloud-rain" class="w-4 h-4 text-blue-400"></i> Soft Rain
          </span>
          <button id="toggleRain" class="px-2.5 py-1 rounded-lg bg-slate-200 dark:bg-slate-700 text-[11px] font-bold text-slate-700 dark:text-slate-200 transition-colors">Play</button>
        </div>
        <input type="range" id="volumeRain" min="0" max="1" step="0.05" value="0.5" class="w-full h-1.5 bg-slate-200 dark:bg-slate-700 rounded-lg appearance-none cursor-pointer">
      </div>

      <!-- Waves Control -->
      <div class="space-y-1.5">
        <div class="flex items-center justify-between text-xs font-semibold">
          <span class="flex items-center gap-2 text-slate-700 dark:text-slate-300">
            <i data-lucide="waves" class="w-4 h-4 text-cyan-400"></i> Ocean Waves
          </span>
          <button id="toggleWaves" class="px-2.5 py-1 rounded-lg bg-slate-200 dark:bg-slate-700 text-[11px] font-bold text-slate-700 dark:text-slate-200 transition-colors">Play</button>
        </div>
        <input type="range" id="volumeWaves" min="0" max="1" step="0.05" value="0.5" class="w-full h-1.5 bg-slate-200 dark:bg-slate-700 rounded-lg appearance-none cursor-pointer">
      </div>

      <!-- Ambient Pad Control -->
      <div class="space-y-1.5">
        <div class="flex items-center justify-between text-xs font-semibold">
          <span class="flex items-center gap-2 text-slate-700 dark:text-slate-300">
            <i data-lucide="music" class="w-4 h-4 text-amber-400"></i> Warm Synth Pad
          </span>
          <button id="togglePad" class="px-2.5 py-1 rounded-lg bg-slate-200 dark:bg-slate-700 text-[11px] font-bold text-slate-700 dark:text-slate-200 transition-colors">Play</button>
        </div>
        <input type="range" id="volumePad" min="0" max="1" step="0.05" value="0.4" class="w-full h-1.5 bg-slate-200 dark:bg-slate-700 rounded-lg appearance-none cursor-pointer">
      </div>

      <!-- Master Volume & Timer -->
      <div class="pt-3 border-t border-slate-200/80 dark:border-slate-700/60 space-y-3">
        <div class="flex items-center justify-between">
          <span class="text-xs font-medium text-slate-500 dark:text-slate-400">Master Volume</span>
          <input type="range" id="masterVolume" min="0" max="1" step="0.05" value="0.8" class="w-32 h-1.5 bg-slate-200 dark:bg-slate-700 rounded-lg appearance-none cursor-pointer">
        </div>

        <div class="flex items-center justify-between gap-2 text-xs">
          <span class="font-medium text-slate-500 dark:text-slate-400 flex items-center gap-1">
            <i data-lucide="timer" class="w-3.5 h-3.5"></i> Sleep Timer
          </span>
          <select id="sleepTimerSelect" class="bg-slate-100 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-lg px-2 py-1 text-xs text-slate-700 dark:text-slate-200 focus:outline-none">
            <option value="off">Off</option>
            <option value="15">15 Mins</option>
            <option value="30">30 Mins</option>
            <option value="60">60 Mins</option>
          </select>
        </div>
        <div id="timerCountdown" class="hidden text-center text-[11px] text-amber-600 dark:text-amber-400 font-mono"></div>
      </div>
    </div>
  </div>

  <!-- Main Content Container -->
  <main class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-6 flex-grow w-full space-y-8">

    <!-- VIEW 1: QUOTES FEED & DAILY SPARK -->
    <div id="quotesView" class="space-y-8">
      
      <!-- Filters & Search Bar -->
      <div class="flex flex-col lg:flex-row lg:items-center justify-between gap-4 pb-2">
        <!-- Filter Tabs -->
        <div class="flex items-center gap-1.5 overflow-x-auto pb-2 lg:pb-0 scrollbar-none" id="filterTabs">
          <button data-category="all" class="filter-tab active px-4 py-2 rounded-xl text-xs sm:text-sm font-semibold whitespace-nowrap transition-all bg-slate-900 dark:bg-amber-500 text-white dark:text-slate-950 shadow-sm">
            All Quotes
          </button>
          <button data-category="being-yourself" class="filter-tab px-4 py-2 rounded-xl text-xs sm:text-sm font-medium whitespace-nowrap transition-all text-slate-600 dark:text-slate-300 hover:bg-babyblue-100/60 dark:hover:bg-slate-800 hover:text-slate-900 dark:hover:text-white">
            Being Yourself
          </button>
          <button data-category="life-inspiration" class="filter-tab px-4 py-2 rounded-xl text-xs sm:text-sm font-medium whitespace-nowrap transition-all text-slate-600 dark:text-slate-300 hover:bg-babyblue-100/60 dark:hover:bg-slate-800 hover:text-slate-900 dark:hover:text-white">
            Life & Inspiration
          </button>
          <button data-category="encouragement" class="filter-tab px-4 py-2 rounded-xl text-xs sm:text-sm font-medium whitespace-nowrap transition-all text-slate-600 dark:text-slate-300 hover:bg-babyblue-100/60 dark:hover:bg-slate-800 hover:text-slate-900 dark:hover:text-white">
            Encouragement
          </button>
          <button data-category="favorites" class="filter-tab px-4 py-2 rounded-xl text-xs sm:text-sm font-medium whitespace-nowrap transition-all text-slate-600 dark:text-slate-300 hover:bg-sunny-100 dark:hover:bg-slate-800 hover:text-amber-800 dark:hover:text-amber-300 flex items-center gap-1.5">
            <i data-lucide="heart" class="w-3.5 h-3.5 text-rose-500 fill-rose-500"></i>
            Favorites (<span id="favCount">0</span>)
          </button>
        </div>

        <!-- Search input -->
        <div class="relative min-w-[240px]">
          <i data-lucide="search" class="w-4 h-4 absolute left-3.5 top-1/2 -translate-y-1/2 text-slate-400"></i>
          <input type="text" id="searchInput" placeholder="Search quotes or authors..." class="w-full pl-10 pr-4 py-2 bg-white/80 dark:bg-slate-800/80 border border-slate-200 dark:border-slate-700/70 rounded-xl text-xs sm:text-sm focus:outline-none focus:ring-2 focus:ring-amber-400 transition-all dark:text-slate-100 dark:placeholder-slate-500">
        </div>
      </div>

      <!-- Daily Spark / Hero Banner -->
      <section id="dailySparkSection" class="relative overflow-hidden rounded-3xl bg-gradient-to-br from-sunny-100 via-white to-babyblue-100 dark:from-slate-900 dark:via-indigo-950/80 dark:to-slate-900 border border-sunny-200/80 dark:border-amber-500/20 p-6 sm:p-8 shadow-lg shadow-sunny-100/40 dark:shadow-indigo-950/50">
        
        <!-- Decorative Backdrop Elements -->
        <div class="absolute -top-12 -right-12 w-48 h-48 bg-sunny-300/30 dark:bg-amber-500/10 rounded-full blur-2xl pointer-events-none"></div>
        <div class="absolute -bottom-12 -left-12 w-48 h-48 bg-babyblue-300/30 dark:bg-indigo-500/10 rounded-full blur-2xl pointer-events-none"></div>

        <div class="relative z-10 flex flex-col md:flex-row items-start md:items-center justify-between gap-6">
          <div class="space-y-3 max-w-3xl">
            <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-sunny-200 dark:bg-amber-500/20 text-amber-900 dark:text-amber-300 text-xs font-semibold uppercase tracking-wider">
              <i data-lucide="zap" class="w-3.5 h-3.5 fill-amber-900 dark:fill-amber-300"></i>
              Daily Spark
            </div>
            
            <blockquote class="text-xl sm:text-2xl md:text-3xl font-serif font-semibold text-slate-900 dark:text-amber-50 leading-relaxed italic">
              "<span id="dailyQuoteText">To be yourself in a world that is constantly trying to make you something else is the greatest accomplishment.</span>"
            </blockquote>

            <p class="text-sm sm:text-base font-medium text-slate-600 dark:text-slate-300 flex items-center gap-2">
              <span class="w-6 h-0.5 bg-sunny-400 dark:bg-amber-400 inline-block"></span>
              <span id="dailyQuoteAuthor">Ralph Waldo Emerson</span>
            </p>
          </div>

          <!-- Banner Actions -->
          <div class="flex md:flex-col items-center gap-2 w-full md:w-auto shrink-0 pt-2 md:pt-0">
            <button id="dailyCardBtn" class="flex-1 md:flex-none w-full flex items-center justify-center gap-2 px-4 py-2.5 rounded-xl bg-slate-900 dark:bg-amber-500 text-white dark:text-slate-950 font-semibold text-xs sm:text-sm hover:bg-slate-800 dark:hover:bg-amber-400 transition-all shadow-sm">
              <i data-lucide="image" class="w-4 h-4"></i>
              <span>Create Card</span>
            </button>
            <div class="flex items-center gap-2 w-full">
              <button id="dailyFavBtn" class="flex-1 flex items-center justify-center gap-1.5 px-3 py-2 rounded-xl bg-white/90 dark:bg-slate-800/90 hover:bg-white dark:hover:bg-slate-800 text-slate-700 dark:text-slate-200 border border-slate-200 dark:border-slate-700 text-xs font-medium transition-all shadow-sm">
                <i data-lucide="heart" id="dailyFavIcon" class="w-3.5 h-3.5"></i>
                <span id="dailyFavLabel">Favorite</span>
              </button>
              <button id="dailyCopyBtn" class="flex-1 flex items-center justify-center gap-1.5 px-3 py-2 rounded-xl bg-white/90 dark:bg-slate-800/90 hover:bg-white dark:hover:bg-slate-800 text-slate-700 dark:text-slate-200 border border-slate-200 dark:border-slate-700 text-xs font-medium transition-all shadow-sm">
                <i data-lucide="copy" class="w-3.5 h-3.5"></i>
                <span>Copy</span>
              </button>
            </div>
          </div>
        </div>
      </section>

      <!-- Quotes Grid Section -->
      <section class="space-y-4">
        <div class="flex items-center justify-between">
          <h2 id="sectionTitle" class="text-base sm:text-lg font-bold text-slate-800 dark:text-slate-100 tracking-tight flex items-center gap-2">
            <span>All Quotes</span>
            <span id="resultsBadge" class="text-xs font-normal px-2.5 py-0.5 rounded-full bg-babyblue-100 dark:bg-indigo-900/60 text-slate-600 dark:text-indigo-200">18 quotes</span>
          </h2>
        </div>

        <!-- Quote Cards Grid -->
        <div id="quotesGrid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          <!-- Dynamic Cards rendered via JavaScript -->
        </div>

        <!-- Empty State -->
        <div id="emptyState" class="hidden text-center py-16 space-y-3 bg-white/50 dark:bg-slate-900/50 rounded-3xl border border-dashed border-slate-200 dark:border-slate-800">
          <div class="w-12 h-12 rounded-full bg-slate-100 dark:bg-slate-800 flex items-center justify-center mx-auto text-slate-400">
            <i data-lucide="search-x" class="w-6 h-6"></i>
          </div>
          <h3 class="text-base font-semibold text-slate-800 dark:text-slate-200">No quotes found</h3>
          <p class="text-xs sm:text-sm text-slate-500 dark:text-slate-400 max-w-sm mx-auto">Try adjusting your search terms or filter selections to find what you are looking for.</p>
          <button id="resetFiltersBtn" class="px-4 py-2 bg-slate-900 dark:bg-amber-500 text-white dark:text-slate-950 rounded-xl text-xs font-semibold hover:bg-slate-800 transition-all">Reset Filters</button>
        </div>
      </section>
    </div>

    <!-- VIEW 2: GRATITUDE & REFLECTION JOURNAL -->
    <div id="journalView" class="hidden space-y-8 animate-fadeIn">
      
      <!-- Journal Intro & Stats Header -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
        
        <!-- Welcome Card -->
        <div class="md:col-span-2 glass-card rounded-3xl p-6 sm:p-8 space-y-3 border border-amber-200/60 dark:border-amber-700/30">
          <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-emerald-100 dark:bg-emerald-950 text-emerald-800 dark:text-emerald-300 text-xs font-semibold uppercase tracking-wider">
            <i data-lucide="book-heart" class="w-3.5 h-3.5"></i>
            Private & Sanctuary
          </div>
          <h2 class="text-2xl sm:text-3xl font-serif font-bold text-slate-900 dark:text-amber-100">Daily Reflection Journal</h2>
          <p class="text-xs sm:text-sm text-slate-600 dark:text-slate-300 leading-relaxed">
            Take a moment to slow down. Write down today's wins, moments of joy, and kind thoughts about yourself. All reflections are saved locally in your browser.
          </p>
        </div>

        <!-- Stats / Streaks Box -->
        <div class="glass-card rounded-3xl p-6 flex flex-col justify-between border border-amber-200/60 dark:border-amber-700/30">
          <div class="space-y-1">
            <span class="text-xs font-semibold text-slate-500 dark:text-slate-400 uppercase tracking-wider">Reflection Streak</span>
            <div class="flex items-baseline gap-2">
              <span id="reflectionCount" class="text-4xl font-extrabold text-amber-500">0</span>
              <span class="text-sm font-semibold text-slate-600 dark:text-slate-300">Days Logged</span>
            </div>
          </div>
          <div class="pt-4 border-t border-slate-200 dark:border-slate-800 flex items-center justify-between text-xs text-slate-500 dark:text-slate-400">
            <span>Last Entry:</span>
            <span id="lastEntryDate" class="font-medium text-slate-700 dark:text-slate-200">Never</span>
          </div>
        </div>
      </div>

      <!-- New Reflection Form -->
      <div class="glass-card rounded-3xl p-6 sm:p-8 space-y-6 border border-slate-200 dark:border-slate-800 shadow-lg">
        <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-3 pb-4 border-b border-slate-200 dark:border-slate-800">
          <div>
            <h3 class="text-lg font-bold font-serif text-slate-900 dark:text-amber-100">New Journal Entry</h3>
            <p class="text-xs text-slate-500 dark:text-slate-400">Reflect on today's positives and appreciate yourself.</p>
          </div>
          <button id="generatePromptBtn" class="inline-flex items-center gap-1.5 px-3 py-1.5 rounded-xl bg-sunny-100 dark:bg-amber-950/80 text-amber-900 dark:text-amber-300 hover:bg-sunny-200 text-xs font-semibold transition-all">
            <i data-lucide="help-circle" class="w-3.5 h-3.5"></i>
            <span>Get Prompt</span>
          </button>
        </div>

        <form id="journalForm" class="space-y-5">
          <!-- Active Prompt Display -->
          <div id="promptDisplay" class="hidden p-3.5 rounded-2xl bg-amber-50 dark:bg-slate-800/80 border border-amber-200 dark:border-amber-700/40 text-xs text-amber-900 dark:text-amber-200 font-medium flex items-center justify-between">
            <span id="promptText">"What made you feel grateful or peaceful today?"</span>
            <button type="button" id="clearPromptBtn" class="text-slate-400 hover:text-slate-600 dark:hover:text-slate-200"><i data-lucide="x" class="w-3.5 h-3.5"></i></button>
          </div>

          <!-- Mood Selector -->
          <div class="space-y-2">
            <label class="block text-xs font-semibold text-slate-700 dark:text-slate-300">How are you feeling today?</label>
            <div class="flex items-center gap-2 flex-wrap" id="moodSelector">
              <button type="button" data-mood="😊 Joyful" class="mood-btn active px-3.5 py-2 rounded-2xl border border-slate-200 dark:border-slate-700 text-xs font-semibold bg-slate-900 dark:bg-amber-500 text-white dark:text-slate-950 transition-all flex items-center gap-1.5">
                <span>😊</span> <span>Joyful</span>
              </button>
              <button type="button" data-mood="🌿 Calm" class="mood-btn px-3.5 py-2 rounded-2xl border border-slate-200 dark:border-slate-700 text-xs font-semibold text-slate-700 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-800 transition-all flex items-center gap-1.5">
                <span>🌿</span> <span>Calm</span>
              </button>
              <button type="button" data-mood="✨ Inspired" class="mood-btn px-3.5 py-2 rounded-2xl border border-slate-200 dark:border-slate-700 text-xs font-semibold text-slate-700 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-800 transition-all flex items-center gap-1.5">
                <span>✨</span> <span>Inspired</span>
              </button>
              <button type="button" data-mood="💪 Strong" class="mood-btn px-3.5 py-2 rounded-2xl border border-slate-200 dark:border-slate-700 text-xs font-semibold text-slate-700 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-800 transition-all flex items-center gap-1.5">
                <span>💪</span> <span>Strong</span>
              </button>
              <button type="button" data-mood="🧘 Reflective" class="mood-btn px-3.5 py-2 rounded-2xl border border-slate-200 dark:border-slate-700 text-xs font-semibold text-slate-700 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-800 transition-all flex items-center gap-1.5">
                <span>🧘</span> <span>Reflective</span>
              </button>
            </div>
          </div>

          <!-- Wins Input -->
          <div class="space-y-1.5">
            <label for="journalWins" class="block text-xs font-semibold text-slate-700 dark:text-slate-300">Today's Wins & Daily Gratitude *</label>
            <textarea id="journalWins" rows="3" required placeholder="Name 1-3 things that went well or made you smile today..." class="w-full p-3.5 bg-white/80 dark:bg-slate-800/80 border border-slate-200 dark:border-slate-700/80 rounded-2xl text-xs sm:text-sm focus:outline-none focus:ring-2 focus:ring-amber-400 dark:text-slate-100 transition-all"></textarea>
          </div>

          <!-- Self Appreciation Input -->
          <div class="space-y-1.5">
            <label for="journalSelfLove" class="block text-xs font-semibold text-slate-700 dark:text-slate-300">Self-Appreciation Note</label>
            <input type="text" id="journalSelfLove" placeholder="What is something you appreciate or admire about yourself today?" class="w-full p-3.5 bg-white/80 dark:bg-slate-800/80 border border-slate-200 dark:border-slate-700/80 rounded-2xl text-xs sm:text-sm focus:outline-none focus:ring-2 focus:ring-amber-400 dark:text-slate-100 transition-all">
          </div>

          <div class="flex justify-end pt-2">
            <button type="submit" class="px-6 py-3 rounded-2xl bg-slate-900 dark:bg-amber-500 text-white dark:text-slate-950 font-bold text-xs sm:text-sm shadow-md hover:bg-slate-800 dark:hover:bg-amber-400 transition-all flex items-center gap-2">
              <i data-lucide="save" class="w-4 h-4"></i>
              <span>Save Private Log</span>
            </button>
          </div>
        </form>
      </div>

      <!-- Log Timeline -->
      <div class="space-y-4">
        <div class="flex items-center justify-between">
          <h3 class="text-lg font-bold font-serif text-slate-900 dark:text-slate-100">Past Journal Logs</h3>
          <span id="journalCountBadge" class="text-xs text-slate-500 dark:text-slate-400 font-medium">0 entries</span>
        </div>

        <div id="journalEntriesList" class="space-y-4">
          <!-- Dynamic Journal Entries -->
        </div>

        <div id="journalEmptyState" class="text-center py-12 glass-card rounded-3xl border border-dashed border-slate-200 dark:border-slate-800 space-y-2">
          <p class="text-xs sm:text-sm text-slate-500 dark:text-slate-400">No journal logs saved yet. Fill out the form above to record your first moment of reflection!</p>
        </div>
      </div>

    </div>

  </main>

  <!-- Footer -->
  <footer class="mt-auto border-t border-babyblue-100 dark:border-slate-800 bg-white/60 dark:bg-slate-950/60 py-8 text-center text-xs sm:text-sm text-slate-500 dark:text-slate-400">
    <div class="max-w-6xl mx-auto px-4 space-y-2">
      <p class="font-medium text-slate-700 dark:text-slate-300">The Be Yourself Club &copy; <span id="year"></span></p>
      <p class="text-xs text-slate-400 dark:text-slate-500">Designed to spread sunshine, mindfulness, authenticity, and gentle encouragement.</p>
    </div>
  </footer>

  <!-- MODAL 1: SHAREABLE QUOTE CARD GENERATOR -->
  <div id="quoteCardModal" class="fixed inset-0 z-50 flex items-center justify-center bg-slate-950/60 backdrop-blur-md p-4 hidden opacity-0 transition-opacity duration-300 overflow-y-auto">
    <div class="glass-card bg-white dark:bg-slate-900 w-full max-w-4xl rounded-3xl shadow-2xl p-6 sm:p-8 space-y-6 relative border border-amber-300/50 dark:border-amber-700/50 my-auto transform scale-95 transition-transform duration-300" id="quoteCardModalCard">
      <button id="closeQuoteCardBtn" class="absolute top-4 right-4 p-2 text-slate-400 hover:text-slate-600 dark:hover:text-slate-200 rounded-full hover:bg-slate-100 dark:hover:bg-slate-800 transition-all">
        <i data-lucide="x" class="w-5 h-5"></i>
      </button>

      <div class="space-y-1">
        <h3 class="text-xl font-bold font-serif text-slate-900 dark:text-amber-100 flex items-center gap-2">
          <i data-lucide="palette" class="w-5 h-5 text-amber-500"></i>
          <span>Shareable Quote Card Generator</span>
        </h3>
        <p class="text-xs text-slate-500 dark:text-slate-400">Customize aesthetics, text fonts, and download as a high-res image card for Instagram, Stories, or Twitter.</p>
      </div>

      <div class="grid grid-cols-1 lg:grid-cols-12 gap-6 items-start">
        
        <!-- Controls Column -->
        <div class="lg:col-span-5 space-y-4">
          
          <!-- Theme Palette Selector -->
          <div class="space-y-2">
            <label class="block text-xs font-semibold text-slate-700 dark:text-slate-300">Theme Background</label>
            <div class="grid grid-cols-2 gap-2" id="cardThemeOptions">
              <button data-theme="sunset" class="card-theme-btn active p-2.5 rounded-xl border-2 border-amber-500 bg-gradient-to-br from-amber-400 via-orange-500 to-purple-900 text-white text-xs font-semibold shadow-sm flex items-center gap-2">
                <span class="w-3 h-3 rounded-full bg-amber-300"></span> Sunset Amber
              </button>
              <button data-theme="ocean" class="card-theme-btn p-2.5 rounded-xl border border-slate-200 dark:border-slate-700 bg-gradient-to-br from-cyan-500 via-blue-600 to-indigo-900 text-white text-xs font-semibold shadow-sm flex items-center gap-2">
                <span class="w-3 h-3 rounded-full bg-cyan-300"></span> Ocean Breeze
              </button>
              <button data-theme="midnight" class="card-theme-btn p-2.5 rounded-xl border border-slate-200 dark:border-slate-700 bg-gradient-to-br from-slate-900 via-purple-950 to-slate-950 text-white text-xs font-semibold shadow-sm flex items-center gap-2">
                <span class="w-3 h-3 rounded-full bg-indigo-400"></span> Midnight Star
              </button>
              <button data-theme="lavender" class="card-theme-btn p-2.5 rounded-xl border border-slate-200 dark:border-slate-700 bg-gradient-to-br from-pink-200 via-purple-200 to-indigo-300 text-slate-800 text-xs font-semibold shadow-sm flex items-center gap-2">
                <span class="w-3 h-3 rounded-full bg-purple-400"></span> Soft Lavender
              </button>
              <button data-theme="minimal" class="card-theme-btn p-2.5 rounded-xl border border-slate-200 dark:border-slate-700 bg-amber-50 text-slate-900 text-xs font-semibold shadow-sm flex items-center gap-2 col-span-2">
                <span class="w-3 h-3 rounded-full bg-amber-200"></span> Minimalist Cream
              </button>
            </div>
          </div>

          <!-- Font Style Selector -->
          <div class="space-y-2">
            <label class="block text-xs font-semibold text-slate-700 dark:text-slate-300">Typography Font</label>
            <div class="grid grid-cols-2 gap-2" id="cardFontOptions">
              <button data-font="serif" class="card-font-btn active p-2 rounded-xl border-2 border-amber-500 bg-slate-100 dark:bg-slate-800 text-xs font-serif text-slate-800 dark:text-slate-200 font-semibold">Playfair Serif</button>
              <button data-font="sans" class="card-font-btn p-2 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-100 dark:bg-slate-800 text-xs font-sans text-slate-800 dark:text-slate-200">Outfit Sans</button>
              <button data-font="handwriting" class="card-font-btn p-2 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-100 dark:bg-slate-800 text-xs font-handwriting text-slate-800 dark:text-slate-200 font-bold">Caveat Script</button>
              <button data-font="mono" class="card-font-btn p-2 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-100 dark:bg-slate-800 text-xs font-mono text-slate-800 dark:text-slate-200">Fira Mono</button>
            </div>
          </div>

          <!-- Aspect Ratio Options -->
          <div class="space-y-2">
            <label class="block text-xs font-semibold text-slate-700 dark:text-slate-300">Aspect Ratio</label>
            <div class="flex items-center gap-2" id="cardRatioOptions">
              <button data-ratio="1:1" class="card-ratio-btn active flex-1 p-2 rounded-xl border-2 border-amber-500 bg-slate-100 dark:bg-slate-800 text-xs font-semibold text-slate-800 dark:text-slate-200">1:1 Square</button>
              <button data-ratio="9:16" class="card-ratio-btn flex-1 p-2 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-100 dark:bg-slate-800 text-xs font-semibold text-slate-800 dark:text-slate-200">9:16 Story</button>
              <button data-ratio="16:9" class="card-ratio-btn flex-1 p-2 rounded-xl border border-slate-200 dark:border-slate-700 bg-slate-100 dark:bg-slate-800 text-xs font-semibold text-slate-800 dark:text-slate-200">16:9 Banner</button>
            </div>
          </div>

          <!-- Watermark & Author Toggles -->
          <div class="pt-2 space-y-2 border-t border-slate-200 dark:border-slate-800">
            <label class="flex items-center justify-between text-xs text-slate-700 dark:text-slate-300 font-medium cursor-pointer">
              <span>Show Watermark</span>
              <input type="checkbox" id="cardShowWatermark" checked class="w-4 h-4 rounded text-amber-500 focus:ring-amber-400">
            </label>
            <label class="flex items-center justify-between text-xs text-slate-700 dark:text-slate-300 font-medium cursor-pointer">
              <span>Show Author</span>
              <input type="checkbox" id="cardShowAuthor" checked class="w-4 h-4 rounded text-amber-500 focus:ring-amber-400">
            </label>
          </div>

          <!-- Download Action -->
          <button id="downloadCardBtn" class="w-full py-3.5 rounded-2xl bg-slate-900 dark:bg-amber-500 text-white dark:text-slate-950 font-bold text-xs sm:text-sm shadow-lg hover:bg-slate-800 dark:hover:bg-amber-400 transition-all flex items-center justify-center gap-2">
            <i data-lucide="download" class="w-4 h-4"></i>
            <span>Download High-Res Card PNG</span>
          </button>
        </div>

        <!-- Preview Canvas Container Column -->
        <div class="lg:col-span-7 flex flex-col items-center justify-center bg-slate-100 dark:bg-slate-950 rounded-2xl p-4 border border-slate-200 dark:border-slate-800 min-h-[360px]">
          <span class="text-[11px] font-semibold text-slate-400 uppercase tracking-wider mb-2">Live Canvas Preview</span>
          
          <!-- Rendered Output Canvas -->
          <canvas id="quoteCardCanvas" class="max-w-full h-auto rounded-2xl shadow-xl transition-all border border-slate-300/40 dark:border-slate-700/40"></canvas>
        </div>

      </div>
    </div>
  </div>

  <!-- MODAL 2: ENCOURAGEMENT GENERATOR / BOOST -->
  <div id="encouragementModal" class="fixed inset-0 z-50 flex items-center justify-center bg-slate-950/60 backdrop-blur-sm p-4 hidden opacity-0 transition-opacity duration-300">
    <div class="glass-card bg-white dark:bg-slate-900 w-full max-w-lg rounded-3xl shadow-2xl p-6 sm:p-8 space-y-6 relative border border-sunny-200 dark:border-amber-700/50 transform scale-95 transition-transform duration-300" id="encouragementModalCard">
      <button id="closeEncouragementBtn" class="absolute top-4 right-4 p-2 text-slate-400 hover:text-slate-600 dark:hover:text-slate-200 rounded-full hover:bg-slate-100 dark:hover:bg-slate-800 transition-all">
        <i data-lucide="x" class="w-5 h-5"></i>
      </button>

      <div class="text-center space-y-3">
        <div class="w-14 h-14 rounded-2xl bg-sunny-100 dark:bg-amber-950/80 text-amber-600 dark:text-amber-300 flex items-center justify-center mx-auto shadow-inner">
          <i data-lucide="sparkles" class="w-7 h-7"></i>
        </div>
        <span class="text-xs font-bold uppercase tracking-widest text-amber-600 dark:text-amber-400">Your Special Encouragement</span>
        <h3 id="encouragementText" class="text-xl sm:text-2xl font-serif font-bold text-slate-900 dark:text-amber-100 leading-snug pt-2">
          "You are capable of far more than you realize. Keep shining your light!"
        </h3>
      </div>

      <div class="flex items-center gap-3 pt-2">
        <button id="nextEncouragementBtn" class="flex-1 py-3 px-4 rounded-2xl bg-gradient-to-r from-sunny-300 to-sunny-400 dark:from-amber-500 dark:to-amber-600 text-slate-900 font-bold text-xs sm:text-sm shadow-sm transition-all flex items-center justify-center gap-2">
          <i data-lucide="refresh-cw" class="w-4 h-4"></i>
          <span>Another Boost</span>
        </button>
        <button id="copyEncouragementBtn" class="py-3 px-4 rounded-2xl bg-babyblue-100 dark:bg-slate-800 text-slate-700 dark:text-slate-200 font-semibold text-xs sm:text-sm transition-all flex items-center justify-center gap-2">
          <i data-lucide="copy" class="w-4 h-4"></i>
          <span>Copy</span>
        </button>
      </div>
    </div>
  </div>

  <!-- MODAL 3: SUBMIT YOUR OWN SPARK -->
  <div id="submitModal" class="fixed inset-0 z-50 flex items-center justify-center bg-slate-950/60 backdrop-blur-sm p-4 hidden opacity-0 transition-opacity duration-300">
    <div class="glass-card bg-white dark:bg-slate-900 w-full max-w-lg rounded-3xl shadow-2xl p-6 sm:p-8 space-y-6 relative border border-babyblue-200 dark:border-indigo-800/50 transform scale-95 transition-transform duration-300" id="submitModalCard">
      <button id="closeSubmitBtn" class="absolute top-4 right-4 p-2 text-slate-400 hover:text-slate-600 dark:hover:text-slate-200 rounded-full hover:bg-slate-100 dark:hover:bg-slate-800 transition-all">
        <i data-lucide="x" class="w-5 h-5"></i>
      </button>

      <div class="space-y-1">
        <h3 class="text-xl font-bold font-serif text-slate-900 dark:text-amber-100">Submit Your Spark</h3>
        <p class="text-xs text-slate-500 dark:text-slate-400">Share your words of wisdom, positive encouragement, or favorite quote.</p>
      </div>

      <form id="submitQuoteForm" class="space-y-4">
        <div>
          <label for="inputQuote" class="block text-xs font-semibold text-slate-700 dark:text-slate-300 mb-1">Quote or Words of Encouragement *</label>
          <textarea id="inputQuote" rows="3" required placeholder="Write something inspiring..." class="w-full p-3 bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-xl text-xs sm:text-sm focus:outline-none focus:ring-2 focus:ring-amber-400 dark:text-slate-100 transition-all"></textarea>
        </div>

        <div>
          <label for="inputAuthor" class="block text-xs font-semibold text-slate-700 dark:text-slate-300 mb-1">Author / Credit</label>
          <input type="text" id="inputAuthor" placeholder="e.g., Yourself, Maya Angelou, Anonymous" class="w-full p-3 bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-xl text-xs sm:text-sm focus:outline-none focus:ring-2 focus:ring-amber-400 dark:text-slate-100 transition-all">
        </div>

        <div>
          <label for="inputCategory" class="block text-xs font-semibold text-slate-700 dark:text-slate-300 mb-1">Category</label>
          <select id="inputCategory" class="w-full p-3 bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-xl text-xs sm:text-sm focus:outline-none focus:ring-2 focus:ring-amber-400 dark:text-slate-100 transition-all">
            <option value="being-yourself">Being Yourself</option>
            <option value="life-inspiration">Life & Inspiration</option>
            <option value="encouragement">Words of Encouragement</option>
          </select>
        </div>

        <button type="submit" class="w-full py-3.5 rounded-2xl bg-slate-900 dark:bg-amber-500 text-white dark:text-slate-950 font-bold text-xs sm:text-sm transition-all shadow-md mt-2">
          Add to Feed
        </button>
      </form>
    </div>
  </div>

  <!-- JavaScript Application Logic -->
  <script>
    // Initial Seed Quotes Dataset
    const initialQuotes = [
      {
        id: 'q1',
        text: 'To be yourself in a world that is constantly trying to make you something else is the greatest accomplishment.',
        author: 'Ralph Waldo Emerson',
        category: 'being-yourself'
      },
      {
        id: 'q2',
        text: 'Act as if what you do makes a difference. It does.',
        author: 'William James',
        category: 'life-inspiration'
      },
      {
        id: 'q3',
        text: 'You are capable of amazing things, just take it one step at a time.',
        author: 'Encouragement',
        category: 'encouragement'
      },
      {
        id: 'q4',
        text: 'Be yourself; everyone else is already taken.',
        author: 'Oscar Wilde',
        category: 'being-yourself'
      },
      {
        id: 'q5',
        text: 'Always be a first-rate version of yourself, instead of a second-rate version of somebody else.',
        author: 'Judy Garland',
        category: 'being-yourself'
      },
      {
        id: 'q6',
        text: 'No one can make you feel inferior without your consent.',
        author: 'Eleanor Roosevelt',
        category: 'being-yourself'
      },
      {
        id: 'q7',
        text: 'The only person you are destined to become is the person you decide to be.',
        author: 'Ralph Waldo Emerson',
        category: 'life-inspiration'
      },
      {
        id: 'q8',
        text: 'Believe you can and you\'re halfway there.',
        author: 'Theodore Roosevelt',
        category: 'encouragement'
      },
      {
        id: 'q9',
        text: 'You don\'t have to be great to start, but you have to start to be great.',
        author: 'Zig Ziglar',
        category: 'life-inspiration'
      },
      {
        id: 'q10',
        text: 'Keep your face always toward the sunshine—and shadows will fall behind you.',
        author: 'Walt Whitman',
        category: 'life-inspiration'
      },
      {
        id: 'q11',
        text: 'You are enough just as you are. Your voice, your story, your mind matter.',
        author: 'Word of Encouragement',
        category: 'encouragement'
      },
      {
        id: 'q12',
        text: 'Don\'t compromise yourself. You\'re all you\'ve got.',
        author: 'Janis Joplin',
        category: 'being-yourself'
      },
      {
        id: 'q13',
        text: 'Tough times never last, but tough people do.',
        author: 'Robert H. Schuller',
        category: 'encouragement'
      },
      {
        id: 'q14',
        text: 'Wherever you go, go with all your heart.',
        author: 'Confucius',
        category: 'life-inspiration'
      },
      {
        id: 'q15',
        text: 'Your time is limited, so don\'t waste it living someone else\'s life.',
        author: 'Steve Jobs',
        category: 'being-yourself'
      },
      {
        id: 'q16',
        text: 'Small steps every day add up to big results. Give yourself credit for how far you\'ve come.',
        author: 'Daily Encouragement',
        category: 'encouragement'
      },
      {
        id: 'q17',
        text: 'Light tomorrow with today!',
        author: 'Elizabeth Barrett Browning',
        category: 'life-inspiration'
      },
      {
        id: 'q18',
        text: 'Embrace the glorious mess that you are.',
        author: 'Elizabeth Gilbert',
        category: 'being-yourself'
      }
    ];

    // High energy encouragement boosts
    const encouragementBoosts = [
      "You are capable of far more than you realize. Keep shining your light!",
      "Don't forget to take a deep breath. You are doing much better than you think.",
      "Your uniqueness is your superpower. Never dim your shine for anyone!",
      "Every small step counts. Celebrate your progress today!",
      "You bring something special into this world that nobody else can duplicate.",
      "Trust your process. Great things take time, and you are right on track.",
      "Be gentle with yourself. You are growing every single day.",
      "You are strong, resilient, and completely worthy of happiness."
    ];

    // Reflection Prompts Dataset
    const reflectionPrompts = [
      "What made you feel grateful or peaceful today?",
      "What is something kind you did for yourself or someone else today?",
      "What is a recent hurdle you handled better than you used to?",
      "Name 3 things that brought a smile to your face today.",
      "What is a quality or skill about yourself you feel proud of right now?",
      "What lesson did today teach you about your inner strength?"
    ];

    // Category Styling Mappings
    const categoryDetails = {
      'being-yourself': {
        label: 'Being Yourself',
        badgeBg: 'bg-sunny-100 dark:bg-amber-950/80',
        badgeText: 'text-amber-900 dark:text-amber-300',
        borderHover: 'hover:border-sunny-300 dark:hover:border-amber-500/50'
      },
      'life-inspiration': {
        label: 'Life & Inspiration',
        badgeBg: 'bg-babyblue-100 dark:bg-indigo-950/80',
        badgeText: 'text-babyblue-800 dark:text-indigo-300',
        borderHover: 'hover:border-babyblue-300 dark:hover:border-indigo-500/50'
      },
      'encouragement': {
        label: 'Encouragement',
        badgeBg: 'bg-emerald-50 dark:bg-emerald-950/80',
        badgeText: 'text-emerald-800 dark:text-emerald-300',
        borderHover: 'hover:border-emerald-300 dark:hover:border-emerald-500/50'
      }
    };

    // Card Generator Preset Themes
    const cardThemes = {
      sunset: { bg1: '#f59e0b', bg2: '#d97706', bg3: '#4c1d95', text: '#ffffff', subtext: '#fde68a', font: 'serif' },
      ocean: { bg1: '#06b6d4', bg2: '#2563eb', bg3: '#1e1b4b', text: '#ffffff', subtext: '#bae6fd', font: 'sans' },
      midnight: { bg1: '#0f172a', bg2: '#311b92', bg3: '#020617', text: '#f1f5f9', subtext: '#fcd34d', font: 'serif' },
      lavender: { bg1: '#fbcfe8', bg2: '#e9d5ff', bg3: '#c7d2fe', text: '#1e1b4b', subtext: '#4338ca', font: 'handwriting' },
      minimal: { bg1: '#fffbeb', bg2: '#fef3c7', bg3: '#fde68a', text: '#0f172a', subtext: '#b45309', font: 'serif' }
    };

    // App State
    let quotes = [];
    let favorites = new Set();
    let journalEntries = [];
    let currentCategory = 'all';
    let searchQuery = '';
    let dailySparkQuote = null;
    let selectedJournalMood = '😊 Joyful';

    // Quote Card Generator State
    let cardState = {
      quote: null,
      theme: 'sunset',
      font: 'serif',
      ratio: '1:1',
      showWatermark: true,
      showAuthor: true
    };

    // Web Audio Synthesizer State
    let audioCtx = null;
    let rainNode = null, waveNode = null, padOscs = [];
    let rainGain = null, waveGain = null, padGain = null, masterGainNode = null;
    let isRainPlaying = false, isWavePlaying = false, isPadPlaying = false;
    let sleepTimerTimeout = null, sleepTimerInterval = null;

    // DOM References
    const quotesView = document.getElementById('quotesView');
    const journalView = document.getElementById('journalView');
    const navQuotesBtn = document.getElementById('navQuotesBtn');
    const navJournalBtn = document.getElementById('navJournalBtn');

    const quotesGrid = document.getElementById('quotesGrid');
    const emptyState = document.getElementById('emptyState');
    const filterTabs = document.getElementById('filterTabs');
    const searchInput = document.getElementById('searchInput');
    const favCountEl = document.getElementById('favCount');
    const sectionTitle = document.getElementById('sectionTitle');
    const resultsBadge = document.getElementById('resultsBadge');
    const resetFiltersBtn = document.getElementById('resetFiltersBtn');

    // Daily Spark Elements
    const dailyQuoteText = document.getElementById('dailyQuoteText');
    const dailyQuoteAuthor = document.getElementById('dailyQuoteAuthor');
    const dailyFavBtn = document.getElementById('dailyFavBtn');
    const dailyFavIcon = document.getElementById('dailyFavIcon');
    const dailyFavLabel = document.getElementById('dailyFavLabel');
    const dailyCopyBtn = document.getElementById('dailyCopyBtn');
    const dailyCardBtn = document.getElementById('dailyCardBtn');

    // Modals
    const surpriseBtn = document.getElementById('surpriseBtn');
    const encouragementModal = document.getElementById('encouragementModal');
    const encouragementModalCard = document.getElementById('encouragementModalCard');
    const closeEncouragementBtn = document.getElementById('closeEncouragementBtn');
    const encouragementText = document.getElementById('encouragementText');
    const nextEncouragementBtn = document.getElementById('nextEncouragementBtn');
    const copyEncouragementBtn = document.getElementById('copyEncouragementBtn');

    const openSubmitModalBtn = document.getElementById('openSubmitModalBtn');
    const submitModal = document.getElementById('submitModal');
    const submitModalCard = document.getElementById('submitModalCard');
    const closeSubmitBtn = document.getElementById('closeSubmitBtn');
    const submitQuoteForm = document.getElementById('submitQuoteForm');

    // Card Generator Modal Elements
    const quoteCardModal = document.getElementById('quoteCardModal');
    const quoteCardModalCard = document.getElementById('quoteCardModalCard');
    const closeQuoteCardBtn = document.getElementById('closeQuoteCardBtn');
    const quoteCardCanvas = document.getElementById('quoteCardCanvas');
    const downloadCardBtn = document.getElementById('downloadCardBtn');
    const cardShowWatermark = document.getElementById('cardShowWatermark');
    const cardShowAuthor = document.getElementById('cardShowAuthor');

    // Ambient Audio Drawer Elements
    const ambientAudioBtn = document.getElementById('ambientAudioBtn');
    const ambientDrawer = document.getElementById('ambientDrawer');
    const closeAmbientDrawer = document.getElementById('closeAmbientDrawer');
    const toggleRain = document.getElementById('toggleRain');
    const toggleWaves = document.getElementById('toggleWaves');
    const togglePad = document.getElementById('togglePad');
    const volumeRain = document.getElementById('volumeRain');
    const volumeWaves = document.getElementById('volumeWaves');
    const volumePad = document.getElementById('volumePad');
    const masterVolume = document.getElementById('masterVolume');
    const sleepTimerSelect = document.getElementById('sleepTimerSelect');
    const timerCountdown = document.getElementById('timerCountdown');

    // Journal Elements
    const journalForm = document.getElementById('journalForm');
    const journalWins = document.getElementById('journalWins');
    const journalSelfLove = document.getElementById('journalSelfLove');
    const moodSelector = document.getElementById('moodSelector');
    const journalEntriesList = document.getElementById('journalEntriesList');
    const journalEmptyState = document.getElementById('journalEmptyState');
    const journalCountBadge = document.getElementById('journalCountBadge');
    const reflectionCount = document.getElementById('reflectionCount');
    const lastEntryDate = document.getElementById('lastEntryDate');
    const generatePromptBtn = document.getElementById('generatePromptBtn');
    const promptDisplay = document.getElementById('promptDisplay');
    const promptText = document.getElementById('promptText');
    const clearPromptBtn = document.getElementById('clearPromptBtn');

    // Sunset Night Mode Toggles
    const sunsetToggle = document.getElementById('sunsetToggle');
    const sunsetToggleMobile = document.getElementById('sunsetToggleMobile');

    // Toast Container
    const toastContainer = document.getElementById('toastContainer');

    // --- INITIALIZATION ---
    function init() {
      document.getElementById('year').textContent = new Date().getFullYear();

      // Load Theme Preference
      initSunsetTheme();

      // Load Local Storage Data
      loadFavorites();
      loadCustomQuotes();
      loadJournal();

      // Set Daily Spark
      dailySparkQuote = quotes[0];
      updateDailySparkUI();

      // Render Views
      renderQuotes();
      updateFavCount();

      // Setup All Event Handlers
      setupEventListeners();

      lucide.createIcons();
    }

    // --- SUNSET NIGHT MODE TOGGLE ---
    function initSunsetTheme() {
      const storedTheme = localStorage.getItem('byc_theme');
      if (storedTheme === 'dark' || (!storedTheme && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
        document.documentElement.classList.add('dark');
      } else {
        document.documentElement.classList.remove('dark');
      }
    }

    function toggleSunsetTheme() {
      const isDark = document.documentElement.classList.toggle('dark');
      localStorage.setItem('byc_theme', isDark ? 'dark' : 'light');
      showToast(isDark ? 'Sunset Night Mode enabled 🌙' : 'Daylight Mode enabled ☀️');
    }

    // --- NAVIGATION VIEW SWITCHER ---
    function switchView(view) {
      if (view === 'quotes') {
        quotesView.classList.remove('hidden');
        journalView.classList.add('hidden');
        navQuotesBtn.className = "px-3.5 py-1.5 rounded-xl text-xs sm:text-sm font-semibold transition-all bg-white dark:bg-amber-500 text-slate-900 dark:text-slate-950 shadow-sm flex items-center gap-1.5";
        navJournalBtn.className = "px-3.5 py-1.5 rounded-xl text-xs sm:text-sm font-semibold transition-all text-slate-600 dark:text-slate-300 hover:text-slate-900 dark:hover:text-white flex items-center gap-1.5";
      } else {
        quotesView.classList.add('hidden');
        journalView.classList.remove('hidden');
        navJournalBtn.className = "px-3.5 py-1.5 rounded-xl text-xs sm:text-sm font-semibold transition-all bg-white dark:bg-amber-500 text-slate-900 dark:text-slate-950 shadow-sm flex items-center gap-1.5";
        navQuotesBtn.className = "px-3.5 py-1.5 rounded-xl text-xs sm:text-sm font-semibold transition-all text-slate-600 dark:text-slate-300 hover:text-slate-900 dark:hover:text-white flex items-center gap-1.5";
        renderJournal();
      }
    }

    // --- DATA MANAGEMENT ---
    function loadFavorites() {
      const stored = localStorage.getItem('byc_favorites');
      if (stored) {
        try { favorites = new Set(JSON.parse(stored)); } catch (e) { favorites = new Set(); }
      }
    }

    function saveFavorites() {
      localStorage.setItem('byc_favorites', JSON.stringify([...favorites]));
      updateFavCount();
    }

    function updateFavCount() {
      favCountEl.textContent = favorites.size;
    }

    function loadCustomQuotes() {
      const stored = localStorage.getItem('byc_custom_quotes');
      if (stored) {
        try {
          const parsed = JSON.parse(stored);
          quotes = [...initialQuotes, ...parsed];
        } catch (e) {
          quotes = [...initialQuotes];
        }
      } else {
        quotes = [...initialQuotes];
      }
    }

    // --- RENDER QUOTES GRID ---
    function renderQuotes() {
      quotesGrid.innerHTML = '';

      let filtered = quotes.filter(q => {
        if (currentCategory === 'favorites') {
          if (!favorites.has(q.id)) return false;
        } else if (currentCategory !== 'all' && q.category !== currentCategory) {
          return false;
        }

        if (searchQuery.trim() !== '') {
          const query = searchQuery.toLowerCase();
          const matchText = q.text.toLowerCase().includes(query);
          const matchAuthor = (q.author || '').toLowerCase().includes(query);
          return matchText || matchAuthor;
        }
        return true;
      });

      let categoryName = "All Quotes";
      if (currentCategory === 'being-yourself') categoryName = "Being Yourself";
      if (currentCategory === 'life-inspiration') categoryName = "Life & Inspiration";
      if (currentCategory === 'encouragement') categoryName = "Words of Encouragement";
      if (currentCategory === 'favorites') categoryName = "Your Favorite Quotes";

      sectionTitle.firstElementChild.textContent = categoryName;
      resultsBadge.textContent = `${filtered.length} quote${filtered.length === 1 ? '' : 's'}`;

      if (filtered.length === 0) {
        emptyState.classList.remove('hidden');
      } else {
        emptyState.classList.add('hidden');

        filtered.forEach((q, index) => {
          const isFav = favorites.has(q.id);
          const details = categoryDetails[q.category] || categoryDetails['being-yourself'];

          const card = document.createElement('div');
          card.className = `glass-card rounded-2xl p-5 sm:p-6 flex flex-col justify-between gap-4 border border-slate-200/80 dark:border-slate-800 transition-all duration-300 hover:shadow-lg hover:-translate-y-1 ${details.borderHover} animate-fadeIn`;
          card.style.animationDelay = `${index * 0.03}s`;

          card.innerHTML = `
            <div class="space-y-3">
              <div class="flex items-center justify-between">
                <span class="text-xs font-semibold px-2.5 py-1 rounded-full ${details.badgeBg} ${details.badgeText}">
                  ${details.label}
                </span>
                <button onclick="toggleFavorite('${q.id}')" class="p-2 text-slate-400 hover:text-rose-500 rounded-full hover:bg-rose-50 dark:hover:bg-rose-950/40 transition-colors" title="Save Favorite">
                  <i data-lucide="heart" class="w-4 h-4 ${isFav ? 'fill-rose-500 text-rose-500' : ''}"></i>
                </button>
              </div>
              <blockquote class="text-base sm:text-lg font-serif font-semibold text-slate-800 dark:text-slate-100 leading-snug">
                "${escapeHtml(q.text)}"
              </blockquote>
            </div>

            <div class="flex items-center justify-between pt-3 border-t border-slate-100/80 dark:border-slate-800">
              <p class="text-xs font-medium text-slate-500 dark:text-slate-400 truncate max-w-[130px] sm:max-w-[160px]">
                — ${escapeHtml(q.author || 'Anonymous')}
              </p>
              <div class="flex items-center gap-1">
                <button onclick="openCardGeneratorModal('${q.id}')" class="flex items-center gap-1 text-xs text-amber-600 dark:text-amber-400 font-semibold hover:bg-amber-50 dark:hover:bg-amber-950/50 px-2 py-1 rounded-lg transition-colors" title="Generate Image Card">
                  <i data-lucide="image" class="w-3.5 h-3.5"></i>
                  <span class="hidden sm:inline">Card</span>
                </button>
                <button onclick="copyToClipboard('${escapeJsString(q.text)} — ${escapeJsString(q.author)}')" class="flex items-center gap-1 text-xs text-slate-500 hover:text-babyblue-600 dark:hover:text-indigo-300 font-medium transition-colors px-2 py-1 rounded-lg hover:bg-babyblue-50 dark:hover:bg-indigo-950/50">
                  <i data-lucide="copy" class="w-3.5 h-3.5"></i>
                  <span class="hidden sm:inline">Copy</span>
                </button>
              </div>
            </div>
          `;

          quotesGrid.appendChild(card);
        });

        lucide.createIcons();
      }
    }

    function updateDailySparkUI() {
      if (!dailySparkQuote) return;
      dailyQuoteText.textContent = dailySparkQuote.text;
      dailyQuoteAuthor.textContent = dailySparkQuote.author || 'Anonymous';
      
      const isFav = favorites.has(dailySparkQuote.id);
      if (isFav) {
        dailyFavIcon.classList.add('fill-rose-500', 'text-rose-500');
        dailyFavLabel.textContent = 'Favorited';
      } else {
        dailyFavIcon.classList.remove('fill-rose-500', 'text-rose-500');
        dailyFavLabel.textContent = 'Favorite';
      }
    }

    window.toggleFavorite = function(id) {
      if (favorites.has(id)) {
        favorites.delete(id);
        showToast('Removed from favorites');
      } else {
        favorites.add(id);
        showToast('Saved to favorites! ❤️');
      }
      saveFavorites();
      renderQuotes();
      if (dailySparkQuote && dailySparkQuote.id === id) {
        updateDailySparkUI();
      }
    };

    // --- FEATURE 1: SHAREABLE QUOTE CARD GENERATOR (CANVAS) ---
    window.openCardGeneratorModal = function(quoteId) {
      const found = quotes.find(q => q.id === quoteId) || dailySparkQuote;
      if (!found) return;

      cardState.quote = found;
      openModal(quoteCardModal, quoteCardModalCard);
      renderCardCanvas();
    };

    function renderCardCanvas() {
      if (!cardState.quote) return;
      const ctx = quoteCardCanvas.getContext('2d');
      const theme = cardThemes[cardState.theme] || cardThemes.sunset;

      // Determine dimensions based on ratio
      let width = 1080;
      let height = 1080;
      if (cardState.ratio === '9:16') { width = 1080; height = 1920; }
      if (cardState.ratio === '16:9') { width = 1920; height = 1080; }

      quoteCardCanvas.width = width;
      quoteCardCanvas.height = height;

      // Draw Gradient Background
      const grad = ctx.createLinearGradient(0, 0, width, height);
      grad.addColorStop(0, theme.bg1);
      grad.addColorStop(0.5, theme.bg2);
      grad.addColorStop(1, theme.bg3);
      ctx.fillStyle = grad;
      ctx.fillRect(0, 0, width, height);

      // Draw Subtle Decorative Shapes
      ctx.fillStyle = 'rgba(255, 255, 255, 0.05)';
      ctx.beginPath();
      ctx.arc(width * 0.85, height * 0.15, width * 0.3, 0, Math.PI * 2);
      ctx.fill();

      ctx.beginPath();
      ctx.arc(width * 0.15, height * 0.85, width * 0.25, 0, Math.PI * 2);
      ctx.fill();

      // Configure Text Fonts
      let fontFamily = 'Playfair Display, serif';
      if (cardState.font === 'sans') fontFamily = 'Outfit, sans-serif';
      if (cardState.font === 'handwriting') fontFamily = 'Caveat, cursive';
      if (cardState.font === 'mono') fontFamily = 'Fira Code, monospace';

      const padding = width * 0.12;
      const maxTextWidth = width - (padding * 2);

      // Calculate Dynamic Text Font Size
      let fontSize = width * 0.055;
      if (cardState.font === 'handwriting') fontSize = width * 0.075;
      if (cardState.quote.text.length > 120) fontSize *= 0.85;

      ctx.fillStyle = theme.text;
      ctx.textAlign = 'center';
      ctx.textBaseline = 'middle';

      // Draw Big Quote Mark Accent
      ctx.font = `italic ${fontSize * 2}px Playfair Display, serif`;
      ctx.fillStyle = theme.subtext;
      ctx.globalAlpha = 0.35;
      ctx.fillText('“', width / 2, height * 0.32);
      ctx.globalAlpha = 1.0;

      // Wrap Text Lines
      ctx.font = `600 ${fontSize}px ${fontFamily}`;
      ctx.fillStyle = theme.text;

      const words = cardState.quote.text.split(' ');
      let lines = [];
      let currentLine = '';

      for (let n = 0; n < words.length; n++) {
        let testLine = currentLine + words[n] + ' ';
        let metrics = ctx.measureText(testLine);
        if (metrics.width > maxTextWidth && n > 0) {
          lines.push(currentLine.trim());
          currentLine = words[n] + ' ';
        } else {
          currentLine = testLine;
        }
      }
      lines.push(currentLine.trim());

      // Render Wrapped Quote
      const lineHeight = fontSize * 1.35;
      const totalTextHeight = lines.length * lineHeight;
      let startY = (height / 2) - (totalTextHeight / 2) + (fontSize * 0.2);

      lines.forEach((line, idx) => {
        ctx.fillText(line, width / 2, startY + (idx * lineHeight));
      });

      // Render Author Name
      if (cardState.showAuthor && cardState.quote.author) {
        ctx.font = `500 ${fontSize * 0.45}px Outfit, sans-serif`;
        ctx.fillStyle = theme.subtext;
        const authorY = startY + totalTextHeight + (fontSize * 0.8);
        ctx.fillText(`— ${cardState.quote.author}`, width / 2, authorY);
      }

      // Render Watermark Branding
      if (cardState.showWatermark) {
        ctx.font = `600 ${fontSize * 0.35}px Outfit, sans-serif`;
        ctx.fillStyle = theme.subtext;
        ctx.globalAlpha = 0.8;
        ctx.fillText('✨ The Be Yourself Club', width / 2, height - (padding * 0.6));
        ctx.globalAlpha = 1.0;
      }
    }

    function downloadQuoteCard() {
      const link = document.createElement('a');
      link.download = `BeYourselfQuote_${Date.now()}.png`;
      link.href = quoteCardCanvas.toDataURL('image/png');
      link.click();
      showToast('Quote Card Downloaded! 🎨');
    }

    // --- FEATURE 2: PRIVATE GRATITUDE & REFLECTION JOURNAL ---
    function loadJournal() {
      const stored = localStorage.getItem('byc_journal_entries');
      if (stored) {
        try { journalEntries = JSON.parse(stored); } catch (e) { journalEntries = []; }
      } else {
        journalEntries = [];
      }
    }

    function saveJournal() {
      localStorage.setItem('byc_journal_entries', JSON.stringify(journalEntries));
    }

    function renderJournal() {
      journalEntriesList.innerHTML = '';
      journalCountBadge.textContent = `${journalEntries.length} ${journalEntries.length === 1 ? 'entry' : 'entries'}`;
      reflectionCount.textContent = journalEntries.length;

      if (journalEntries.length > 0) {
        const lastDate = new Date(journalEntries[0].timestamp).toLocaleDateString(undefined, { month: 'short', day: 'numeric' });
        lastEntryDate.textContent = lastDate;
        journalEmptyState.classList.add('hidden');
      } else {
        lastEntryDate.textContent = 'Never';
        journalEmptyState.classList.remove('hidden');
        return;
      }

      journalEntries.forEach((entry, idx) => {
        const dateStr = new Date(entry.timestamp).toLocaleDateString(undefined, {
          weekday: 'short', month: 'short', day: 'numeric', year: 'numeric'
        });

        const item = document.createElement('div');
        item.className = "glass-card rounded-2xl p-5 space-y-3 border border-slate-200 dark:border-slate-800 animate-fadeIn";

        item.innerHTML = `
          <div class="flex items-center justify-between pb-2 border-b border-slate-100 dark:border-slate-800">
            <div class="flex items-center gap-2">
              <span class="text-xs px-2.5 py-1 rounded-full bg-amber-100 dark:bg-amber-950 text-amber-900 dark:text-amber-300 font-semibold">
                ${escapeHtml(entry.mood || '😊 Joyful')}
              </span>
              <span class="text-xs text-slate-400 font-medium">${dateStr}</span>
            </div>
            <button onclick="deleteJournalEntry(${entry.id})" class="text-slate-400 hover:text-rose-500 p-1 rounded-lg transition-colors" title="Delete Entry">
              <i data-lucide="trash-2" class="w-4 h-4"></i>
            </button>
          </div>

          ${entry.prompt ? `<p class="text-xs italic text-amber-800 dark:text-amber-300 bg-amber-50 dark:bg-amber-950/40 p-2 rounded-xl">Prompt: "${escapeHtml(entry.prompt)}"</p>` : ''}

          <div class="space-y-1">
            <h4 class="text-xs font-bold text-slate-500 uppercase tracking-wider">Today's Wins & Gratitude</h4>
            <p class="text-xs sm:text-sm text-slate-800 dark:text-slate-200 leading-relaxed whitespace-pre-line">${escapeHtml(entry.wins)}</p>
          </div>

          ${entry.selfLove ? `
            <div class="pt-2 border-t border-slate-100 dark:border-slate-800/60 space-y-0.5">
              <h5 class="text-[11px] font-bold text-emerald-600 dark:text-emerald-400 uppercase tracking-wider">Self-Appreciation</h5>
              <p class="text-xs text-slate-700 dark:text-slate-300 italic">"${escapeHtml(entry.selfLove)}"</p>
            </div>
          ` : ''}
        `;

        journalEntriesList.appendChild(item);
      });

      lucide.createIcons();
    }

    window.deleteJournalEntry = function(id) {
      journalEntries = journalEntries.filter(e => e.id !== id);
      saveJournal();
      renderJournal();
      showToast('Journal log deleted');
    };

    // --- FEATURE 3: SOFT AMBIENT MUSIC / NATURE SOUND PLAYER (WEB AUDIO API) ---
    function initAudioContext() {
      if (!audioCtx) {
        const AudioContext = window.AudioContext || window.webkitAudioContext;
        audioCtx = new AudioContext();

        masterGainNode = audioCtx.createGain();
        masterGainNode.gain.value = parseFloat(masterVolume.value);
        masterGainNode.connect(audioCtx.destination);
      }
      if (audioCtx.state === 'suspended') {
        audioCtx.resume();
      }
    }

    // Procedural Noise Generator (Rain / Waves)
    function createNoiseBuffer() {
      const bufferSize = audioCtx.sampleRate * 2;
      const buffer = audioCtx.createBuffer(1, bufferSize, audioCtx.sampleRate);
      const output = buffer.getChannelData(0);
      for (let i = 0; i < bufferSize; i++) {
        output[i] = Math.random() * 2 - 1;
      }
      return buffer;
    }

    function toggleRainSound() {
      initAudioContext();
      if (isRainPlaying) {
        if (rainNode) { rainNode.stop(); rainNode.disconnect(); }
        isRainPlaying = false;
        toggleRain.textContent = 'Play';
        toggleRain.className = 'px-2.5 py-1 rounded-lg bg-slate-200 dark:bg-slate-700 text-[11px] font-bold text-slate-700 dark:text-slate-200 transition-colors';
      } else {
        const noiseBuffer = createNoiseBuffer();
        const whiteNoise = audioCtx.createBufferSource();
        whiteNoise.buffer = noiseBuffer;
        whiteNoise.loop = true;

        // Filter for soft rain sound
        const filter = audioCtx.createBiquadFilter();
        filter.type = 'lowpass';
        filter.frequency.value = 800;

        rainGain = audioCtx.createGain();
        rainGain.gain.value = parseFloat(volumeRain.value) * 0.4;

        whiteNoise.connect(filter);
        filter.connect(rainGain);
        rainGain.connect(masterGainNode);

        whiteNoise.start();
        rainNode = whiteNoise;
        isRainPlaying = true;

        toggleRain.textContent = 'Stop';
        toggleRain.className = 'px-2.5 py-1 rounded-lg bg-amber-500 text-[11px] font-bold text-slate-950 transition-colors';
      }
      updateAudioIndicators();
    }

    function toggleWavesSound() {
      initAudioContext();
      if (isWavePlaying) {
        if (waveNode) { waveNode.stop(); waveNode.disconnect(); }
        isWavePlaying = false;
        toggleWaves.textContent = 'Play';
        toggleWaves.className = 'px-2.5 py-1 rounded-lg bg-slate-200 dark:bg-slate-700 text-[11px] font-bold text-slate-700 dark:text-slate-200 transition-colors';
      } else {
        const noiseBuffer = createNoiseBuffer();
        const whiteNoise = audioCtx.createBufferSource();
        whiteNoise.buffer = noiseBuffer;
        whiteNoise.loop = true;

        const filter = audioCtx.createBiquadFilter();
        filter.type = 'bandpass';
        filter.frequency.value = 400;

        // LFO to simulate ocean wave swells
        const lfo = audioCtx.createOscillator();
        lfo.frequency.value = 0.12; // wave frequency
        const lfoGain = audioCtx.createGain();
        lfoGain.gain.value = 300;
        lfo.connect(lfoGain);
        lfoGain.connect(filter.frequency);
        lfo.start();

        waveGain = audioCtx.createGain();
        waveGain.gain.value = parseFloat(volumeWaves.value) * 0.5;

        whiteNoise.connect(filter);
        filter.connect(waveGain);
        waveGain.connect(masterGainNode);

        whiteNoise.start();
        waveNode = whiteNoise;
        isWavePlaying = true;

        toggleWaves.textContent = 'Stop';
        toggleWaves.className = 'px-2.5 py-1 rounded-lg bg-amber-500 text-[11px] font-bold text-slate-950 transition-colors';
      }
      updateAudioIndicators();
    }

    function togglePadSound() {
      initAudioContext();
      if (isPadPlaying) {
        padOscs.forEach(osc => { try { osc.stop(); osc.disconnect(); } catch(e){} });
        padOscs = [];
        isPadPlaying = false;
        togglePad.textContent = 'Play';
        togglePad.className = 'px-2.5 py-1 rounded-lg bg-slate-200 dark:bg-slate-700 text-[11px] font-bold text-slate-700 dark:text-slate-200 transition-colors';
      } else {
        padGain = audioCtx.createGain();
        padGain.gain.value = parseFloat(volumePad.value) * 0.15;

        // Warm ambient synth chord frequencies (C major / A minor chords)
        const freqs = [130.81, 164.81, 196.00, 246.94]; // C3, E3, G3, B3
        padOscs = freqs.map(f => {
          const osc = audioCtx.createOscillator();
          osc.type = 'sine';
          osc.frequency.value = f;
          osc.connect(padGain);
          osc.start();
          return osc;
        });

        padGain.connect(masterGainNode);
        isPadPlaying = true;

        togglePad.textContent = 'Stop';
        togglePad.className = 'px-2.5 py-1 rounded-lg bg-amber-500 text-[11px] font-bold text-slate-950 transition-colors';
      }
      updateAudioIndicators();
    }

    function stopAllAudio() {
      if (isRainPlaying) toggleRainSound();
      if (isWavePlaying) toggleWavesSound();
      if (isPadPlaying) togglePadSound();
    }

    function updateAudioIndicators() {
      const playing = isRainPlaying || isWavePlaying || isPadPlaying;
      const dot1 = document.getElementById('audioPlayingDot');
      const dot2 = document.getElementById('audioPlayingDotStatic');
      if (playing) {
        dot1.classList.remove('hidden');
        dot2.classList.remove('hidden');
      } else {
        dot1.classList.add('hidden');
        dot2.classList.add('hidden');
      }
    }

    // --- SLEEP TIMER ---
    function setSleepTimer(minutes) {
      if (sleepTimerTimeout) clearTimeout(sleepTimerTimeout);
      if (sleepTimerInterval) clearInterval(sleepTimerInterval);
      timerCountdown.classList.add('hidden');

      if (minutes === 'off') return;

      let remainingMs = parseInt(minutes) * 60 * 1000;
      timerCountdown.classList.remove('hidden');

      function updateTimerDisplay() {
        let mins = Math.floor(remainingMs / 60000);
        let secs = Math.floor((remainingMs % 60000) / 1000);
        timerCountdown.textContent = `Auto stop in ${mins}m ${secs < 10 ? '0' : ''}${secs}s`;
      }

      updateTimerDisplay();

      sleepTimerInterval = setInterval(() => {
        remainingMs -= 1000;
        if (remainingMs <= 0) {
          clearInterval(sleepTimerInterval);
        } else {
          updateTimerDisplay();
        }
      }, 1000);

      sleepTimerTimeout = setTimeout(() => {
        stopAllAudio();
        showToast('Sleep timer finished — sounds paused 🌙');
        timerCountdown.classList.add('hidden');
        sleepTimerSelect.value = 'off';
      }, remainingMs);
    }

    // --- HELPER UTILITIES ---
    function escapeHtml(str) {
      return (str || '').replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;").replace(/"/g, "&quot;").replace(/'/g, "&#039;");
    }

    function escapeJsString(str) {
      return (str || '').replace(/\\/g, '\\\\').replace(/'/g, "\\'").replace(/"/g, '\\"');
    }

    window.copyToClipboard = function(text) {
      if (navigator.clipboard && window.isSecureContext) {
        navigator.clipboard.writeText(text).then(() => {
          showToast('Copied to clipboard! ✨');
        }).catch(() => fallbackCopy(text));
      } else {
        fallbackCopy(text);
      }
    };

    function fallbackCopy(text) {
      const area = document.createElement("textarea");
      area.value = text;
      area.style.position = "fixed";
      document.body.appendChild(area);
      area.focus();
      area.select();
      try {
        document.execCommand('copy');
        showToast('Copied to clipboard! ✨');
      } catch (err) {
        showToast('Copying failed');
      }
      document.body.removeChild(area);
    }

    function showToast(message) {
      const toast = document.createElement('div');
      toast.className = 'toast-slide bg-slate-900 dark:bg-amber-500 text-white dark:text-slate-950 px-4 py-3 rounded-2xl text-xs font-semibold shadow-lg flex items-center gap-2 pointer-events-auto border border-slate-700 dark:border-amber-400';
      toast.innerHTML = `<i data-lucide="check-circle" class="w-4 h-4 text-sunny-300 dark:text-slate-950"></i><span>${message}</span>`;
      toastContainer.appendChild(toast);
      lucide.createIcons();

      setTimeout(() => {
        toast.style.opacity = '0';
        toast.style.transition = 'opacity 0.3s ease';
        setTimeout(() => toast.remove(), 300);
      }, 2500);
    }

    function openModal(modal, card) {
      modal.classList.remove('hidden');
      setTimeout(() => {
        modal.classList.remove('opacity-0');
        card.classList.remove('scale-95');
        card.classList.add('scale-100');
      }, 10);
    }

    function closeModal(modal, card) {
      modal.classList.add('opacity-0');
      card.classList.remove('scale-100');
      card.classList.add('scale-95');
      setTimeout(() => { modal.classList.add('hidden'); }, 300);
    }

    function triggerConfetti() {
      if (typeof confetti === 'function') {
        confetti({
          particleCount: 60,
          spread: 70,
          origin: { y: 0.6 },
          colors: ['#bae6fd', '#fcd34d', '#38bdf8', '#fbbf24']
        });
      }
    }

    // --- EVENT LISTENERS SETUP ---
    function setupEventListeners() {
      // Navigation Tabs
      navQuotesBtn.addEventListener('click', () => switchView('quotes'));
      navJournalBtn.addEventListener('click', () => switchView('journal'));

      // Sunset Mode Toggles
      sunsetToggle.addEventListener('click', toggleSunsetTheme);
      sunsetToggleMobile.addEventListener('click', toggleSunsetTheme);

      // Category Filters
      filterTabs.querySelectorAll('.filter-tab').forEach(tab => {
        tab.addEventListener('click', () => {
          filterTabs.querySelectorAll('.filter-tab').forEach(t => {
            t.classList.remove('bg-slate-900', 'dark:bg-amber-500', 'text-white', 'dark:text-slate-950', 'shadow-sm');
            t.classList.add('text-slate-600', 'dark:text-slate-300');
          });

          tab.classList.remove('text-slate-600', 'dark:text-slate-300');
          tab.classList.add('bg-slate-900', 'dark:bg-amber-500', 'text-white', 'dark:text-slate-950', 'shadow-sm');

          currentCategory = tab.getAttribute('data-category');
          renderQuotes();
        });
      });

      // Search Filter Input
      searchInput.addEventListener('input', (e) => {
        searchQuery = e.target.value;
        renderQuotes();
      });

      resetFiltersBtn.addEventListener('click', () => {
        searchQuery = '';
        searchInput.value = '';
        currentCategory = 'all';
        renderQuotes();
      });

      // Daily Spark Actions
      dailyFavBtn.addEventListener('click', () => {
        if (dailySparkQuote) toggleFavorite(dailySparkQuote.id);
      });
      dailyCopyBtn.addEventListener('click', () => {
        if (dailySparkQuote) copyToClipboard(`"${dailySparkQuote.text}" — ${dailySparkQuote.author}`);
      });
      dailyCardBtn.addEventListener('click', () => {
        if (dailySparkQuote) openCardGeneratorModal(dailySparkQuote.id);
      });

      // Surprise Boost
      surpriseBtn.addEventListener('click', () => {
        const rand = encouragementBoosts[Math.floor(Math.random() * encouragementBoosts.length)];
        encouragementText.textContent = `"${rand}"`;
        openModal(encouragementModal, encouragementModalCard);
        triggerConfetti();
      });
      closeEncouragementBtn.addEventListener('click', () => closeModal(encouragementModal, encouragementModalCard));
      nextEncouragementBtn.addEventListener('click', () => {
        const rand = encouragementBoosts[Math.floor(Math.random() * encouragementBoosts.length)];
        encouragementText.textContent = `"${rand}"`;
        triggerConfetti();
      });
      copyEncouragementBtn.addEventListener('click', () => copyToClipboard(encouragementText.textContent));

      // Submit Quote Modal
      openSubmitModalBtn.addEventListener('click', () => openModal(submitModal, submitModalCard));
      closeSubmitBtn.addEventListener('click', () => closeModal(submitModal, submitModalCard));
      submitQuoteForm.addEventListener('submit', (e) => {
        e.preventDefault();
        const text = document.getElementById('inputQuote').value.trim();
        const author = document.getElementById('inputAuthor').value.trim() || 'Anonymous';
        const category = document.getElementById('inputCategory').value;

        if (text) {
          const newQuote = { id: 'custom_' + Date.now(), text, author, category };
          quotes.unshift(newQuote);
          const customOnly = quotes.filter(q => q.id.startsWith('custom_'));
          localStorage.setItem('byc_custom_quotes', JSON.stringify(customOnly));
          submitQuoteForm.reset();
          closeModal(submitModal, submitModalCard);
          renderQuotes();
          showToast('Quote added to feed! 🌟');
          triggerConfetti();
        }
      });

      // Quote Card Controls Listener
      closeQuoteCardBtn.addEventListener('click', () => closeModal(quoteCardModal, quoteCardModalCard));
      downloadCardBtn.addEventListener('click', downloadQuoteCard);

      document.querySelectorAll('#cardThemeOptions .card-theme-btn').forEach(btn => {
        btn.addEventListener('click', () => {
          document.querySelectorAll('#cardThemeOptions .card-theme-btn').forEach(b => {
            b.classList.remove('border-2', 'border-amber-500');
            b.classList.add('border', 'border-slate-200', 'dark:border-slate-700');
          });
          btn.classList.add('border-2', 'border-amber-500');
          cardState.theme = btn.getAttribute('data-theme');
          renderCardCanvas();
        });
      });

      document.querySelectorAll('#cardFontOptions .card-font-btn').forEach(btn => {
        btn.addEventListener('click', () => {
          document.querySelectorAll('#cardFontOptions .card-font-btn').forEach(b => {
            b.classList.remove('border-2', 'border-amber-500');
            b.classList.add('border', 'border-slate-200', 'dark:border-slate-700');
          });
          btn.classList.add('border-2', 'border-amber-500');
          cardState.font = btn.getAttribute('data-font');
          renderCardCanvas();
        });
      });

      document.querySelectorAll('#cardRatioOptions .card-ratio-btn').forEach(btn => {
        btn.addEventListener('click', () => {
          document.querySelectorAll('#cardRatioOptions .card-ratio-btn').forEach(b => {
            b.classList.remove('border-2', 'border-amber-500');
            b.classList.add('border', 'border-slate-200', 'dark:border-slate-700');
          });
          btn.classList.add('border-2', 'border-amber-500');
          cardState.ratio = btn.getAttribute('data-ratio');
          renderCardCanvas();
        });
      });

      cardShowWatermark.addEventListener('change', (e) => {
        cardState.showWatermark = e.target.checked;
        renderCardCanvas();
      });

      cardShowAuthor.addEventListener('change', (e) => {
        cardState.showAuthor = e.target.checked;
        renderCardCanvas();
      });

      // Ambient Audio Drawer Controls
      ambientAudioBtn.addEventListener('click', () => ambientDrawer.classList.toggle('hidden'));
      closeAmbientDrawer.addEventListener('click', () => ambientDrawer.classList.add('hidden'));

      toggleRain.addEventListener('click', toggleRainSound);
      toggleWaves.addEventListener('click', toggleWavesSound);
      togglePad.addEventListener('click', togglePadSound);

      volumeRain.addEventListener('input', (e) => { if (rainGain) rainGain.gain.value = parseFloat(e.target.value) * 0.4; });
      volumeWaves.addEventListener('input', (e) => { if (waveGain) waveGain.gain.value = parseFloat(e.target.value) * 0.5; });
      volumePad.addEventListener('input', (e) => { if (padGain) padGain.gain.value = parseFloat(e.target.value) * 0.15; });
      masterVolume.addEventListener('input', (e) => { if (masterGainNode) masterGainNode.gain.value = parseFloat(e.target.value); });
      sleepTimerSelect.addEventListener('change', (e) => setSleepTimer(e.target.value));

      // Journal Mood Selector Buttons
      moodSelector.querySelectorAll('.mood-btn').forEach(btn => {
        btn.addEventListener('click', () => {
          moodSelector.querySelectorAll('.mood-btn').forEach(b => {
            b.classList.remove('bg-slate-900', 'dark:bg-amber-500', 'text-white', 'dark:text-slate-950');
            b.classList.add('text-slate-700', 'dark:text-slate-300');
          });
          btn.classList.remove('text-slate-700', 'dark:text-slate-300');
          btn.classList.add('bg-slate-900', 'dark:bg-amber-500', 'text-white', 'dark:text-slate-950');
          selectedJournalMood = btn.getAttribute('data-mood');
        });
      });

      // Prompt Generator
      generatePromptBtn.addEventListener('click', () => {
        const rand = reflectionPrompts[Math.floor(Math.random() * reflectionPrompts.length)];
        promptText.textContent = `"${rand}"`;
        promptDisplay.classList.remove('hidden');
      });

      clearPromptBtn.addEventListener('click', () => {
        promptDisplay.classList.add('hidden');
      });

      // Journal Form Submission
      journalForm.addEventListener('submit', (e) => {
        e.preventDefault();
        const wins = journalWins.value.trim();
        const selfLove = journalSelfLove.value.trim();
        const activePrompt = !promptDisplay.classList.contains('hidden') ? promptText.textContent.replace(/^"|"$/g, '') : null;

        if (wins) {
          const entry = {
            id: Date.now(),
            timestamp: new Date().toISOString(),
            mood: selectedJournalMood,
            wins,
            selfLove,
            prompt: activePrompt
          };

          journalEntries.unshift(entry);
          saveJournal();
          journalForm.reset();
          promptDisplay.classList.add('hidden');
          renderJournal();
          showToast('Journal log saved privately! 📖');
          triggerConfetti();
        }
      });
    }

    // Run Initialization on Load
    window.onload = init;
  </script>
</body>
</html>


// A simple profanity & negativity keyword filter
const blockedKeywords = [
  "hate", "stupid", "ugly", "loser", "horrible", "awful", "terrible", "bad"
];

function validateSubmission(text) {
  const lowerText = text.toLowerCase();
  
  // Check against blocked words
  for (let keyword of blockedKeywords) {
    if (lowerText.includes(keyword)) {
      return {
        valid: false,
        message: "Please ensure your message is positive and encouraging before submitting!"
      };
    }
  }

  // Ensure minimum length
  if (text.trim().length < 5) {
    return {
      valid: false,
      message: "Please write a slightly longer note of encouragement!"
    };
  }

  return { valid: true };
}

// Example usage on form submit:
// const result = validateSubmission(userInput);
// if (!result.valid) { alert(result.message); }


Make this webpage code all together please
