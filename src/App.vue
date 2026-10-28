<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue';
import { 
  Sun, Moon, Github, Linkedin, Mail, Code2, 
  Briefcase, User, Cpu, Sparkles, ChevronRight, Menu, X, 
  Download, Send, CheckCircle2, ArrowUpRight, FolderGit2,
  Terminal, Layers, Globe, GraduationCap, Heart, Gamepad2, 
  BookOpen, Music, Dumbbell, FileText, Instagram, Brain, Users, Target, Workflow, Database
} from 'lucide-vue-next';

// Map Ikon untuk Tech Stack pada Tag Proyek
const TECH_ICONS = {
  "Vue.js": "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vuejs/vuejs-original.svg",
  "Vue.js 3": "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vuejs/vuejs-original.svg",
  "Tailwind CSS": "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/tailwindcss/tailwindcss-original.svg",
  "Tailwind": "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/tailwindcss/tailwindcss-original.svg",
  "Vite": "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vite/vite-original.svg",
  "JavaScript": "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/javascript/javascript-original.svg",
  "React": "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/react/react-original.svg",
  "Chart.js": "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/chartjs/chartjs-color.svg",
  "REST API": "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/fastapi/fastapi-original.svg",
  "LocalStorage": "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/html5/html5-original.svg"
};

// Data Portofolio Ahdam Ashari
const PORTFOLIO_DATA = {
  personal: {
    name: "AHDAM ASHARI",
    firstName: "AHDAM",
    lastName: "ASHARI",
    role: "Junior Frontend & Backend Developer",
    bio: "Saya membangun pengalaman web yang responsif, cepat, dan berfokus pada pengguna dengan teknologi JavaScript modern serta backend development. Mengintegrasikan antarmuka interaktif dengan arsitektur sistem yang andal.",
    location: "Bontang, Kalimantan Timur, Indonesia",
    email: "ahdamashari12@gmail.com",
    github: "https://github.com/4hdm",
    linkedin: "https://linkedin.com",
    instagram: "https://instagram.com",
    avatar: "foto profil.png",
    stats: [
      { label: "Tahun Pengalaman", value: "2+" },
      { label: "Proyek Selesai", value: "8+" },
      { label: "Klien / Tugas Puas", value: "10+" },
      { label: "Komit / Kontribusi", value: "150+" }
    ]
  },
  skills: {
    softwareEngineer: [
      { name: "Python", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/python/python-original.svg" },
      { name: "C++", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/cplusplus/cplusplus-original.svg" },
      { name: "Vue.js", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vuejs/vuejs-original.svg" },
      { name: "React.js", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/react/react-original.svg" },
      { name: "JavaScript", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/javascript/javascript-original.svg" },
      { name: "TypeScript", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/typescript/typescript-original.svg" },
      { name: "Tailwind CSS", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/tailwindcss/tailwindcss-original.svg" },
      { name: "Next.js", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nextjs/nextjs-original.svg" },
      { name: "Node.js", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nodejs/nodejs-original.svg" },
      { name: "MySQL", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/mysql/mysql-original.svg" }
    ],
    toolsServer: [
      { name: "Git", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/git/git-original.svg" },
      { name: "GitHub", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/github/github-original.svg" },
      { name: "Figma", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/figma/figma-original.svg" },
      { name: "Vite", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vite/vite-original.svg" },
      { name: "Webpack", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/webpack/webpack-original.svg" }
    ],
    softSkills: [
      { name: "Problem Solving", icon: Brain },
      { name: "Team Collaboration", icon: Users },
      { name: "Critical Thinking", icon: Target },
      { name: "Adaptability", icon: Workflow }
    ]
  },
  education: [
    {
      degree: "S1 Teknik Informatika",
      institution: "Sekolah Tinggi Teknologi Bontang (STITEK)",
      period: "2024 - Sekarang",
      description: "Fokus pada pengembangan perangkat lunak, struktur data, basis data, dan kecerdasan buatan."
    },
    { 
      degree: "SMA Jurusan IPA",
      institution: "SEKOLAH MENENGAH ATAS NEGERI 2 BONTANG",
      period: "2019 - 2022",
      description: "Fokus pada pengembangan diri baik soft dan hardskill, berfokus dalam bidang menghitung atau matematika."
    }
  ],
  publications: [
    {
      title: "Analisis Perbandingan Kinerja Algoritma KNN dengan Resampling ADASYN untuk Deteksi Intrusi",
      category: "Jurnal Penelitian",
      period: "2026",
      description: "Penelitian mengenai peningkatan akurasi sistem deteksi intrusi jaringan menggunakan pendekatan machine learning dan penanganan data tidak seimbang.",
      link: "URL_MENUJU_JURNAL_ANDA"
    }
  ],
  projects: [
    {
      id: 1,
      title: "Portfolio Website",
      category: "Web App",
      description: "Tampilan antarmuka mode gelap (dark mode) pada website portofolio personal yang interaktif dan responsif.",
      image: "Cuplikan layar 2026-10-20 124542.png",
      tags: ["Vue.js", "Tailwind CSS", "Vite", "JavaScript"],
      liveLink: "https://4hdm.github.io",
      githubLink: "https://github.com/4hdm/fortopolio-vue.js-"
    },
    {
      id: 2,
      title: "VueShop List",
      category: "Web App",
      description: "Aplikasi manajemen daftar belanja harian yang interaktif dan responsif untuk mencatat, memfilter, serta memantau progres belanja secara real-time.",
      image: "Cuplikan layar 2026-10-20 153809.png",
      tags: ["Vue.js 3", "Tailwind CSS", "LocalStorage"],
      liveLink: "https://example.com",
      githubLink: "https://github.com/4hdm/vue-shoplist"
    },
    {
      id: 3,
      title: "VueCalc Pro",
      category: "Web App",
      description: "Aplikasi kalkulator saintifik modern berbasis Vue 3 dan Tailwind CSS yang mendukung fungsi matematika dasar hingga tingkat lanjut.",
      image: "Cuplikan layar 2026-10-20 164839.png",
      tags: ["Vue.js 3", "Tailwind CSS", "JavaScript"],
      liveLink: "https://4hdm.github.io/vue-calc",
      githubLink: "https://github.com/4hdm/vue-calc"
    },
    {
      id: 4,
      title: "Mahasiswa)",
      category: "Web App",
      description: "Aplikasi Manajemen Data Mahasiswa & Program Studi modern dengan sentuhan estetika Crimson Luxury & Adaptive Dark Mode.",
      image: "Cuplikan layar 2026-10-24 002216.png",
      tags: ["Laravel 10/11", "Bootstrap 5.3", "JavaScript", "MySQL", "PHP", "DomPDF"],
      liveLink: "https://github.com/4hdm/Sim-mahasiswa",
      githubLink: "https://github.com/4hdm/Sim-mahasiswa"
    }
  ]
};

// Reactive State
const darkMode = ref(true);
const mobileMenuOpen = ref(false);
const activeSection = ref('hero');
const projectCategory = ref('All');
const selectedProject = ref(null);
const formSubmitted = ref(false);
const isHovered = ref(false);

const navItems = [
  { id: 'hero', label: 'HOME' },
  { id: 'about', label: 'ABOUT' },
  { id: 'projects', label: 'PROJECT' },
  { id: 'publications', label: 'PUBLICATIONS' },
  { id: 'contact', label: 'CONTACT' }
];

const filteredProjects = computed(() => {
  if (projectCategory.value === 'All') return PORTFOLIO_DATA.projects;
  return PORTFOLIO_DATA.projects.filter(p => p.category === projectCategory.value);
});

const toggleDarkMode = () => {
  darkMode.value = !darkMode.value;
  if (darkMode.value) {
    document.documentElement.classList.add('dark');
  } else {
    document.documentElement.classList.remove('dark');
  }
};

const handleScroll = () => {
  const sections = ['hero', 'about', 'projects', 'publications', 'contact'];
  const scrollPosition = window.scrollY + 200;

  for (const section of sections) {
    const el = document.getElementById(section);
    if (el) {
      const top = el.offsetTop;
      const height = el.offsetHeight;
      if (scrollPosition >= top && scrollPosition < top + height) {
        activeSection.value = section;
        break;
      }
    }
  }
};

const handleFormSubmit = () => {
  formSubmitted.value = true;
  setTimeout(() => {
    formSubmitted.value = false;
  }, 4000);
};

onMounted(() => {
  if (darkMode.value) {
    document.documentElement.classList.add('dark');
  }
  window.addEventListener('scroll', handleScroll);
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
});
</script>

<template>
  <div :class="['min-h-screen transition-colors duration-300 font-sans selection:bg-red-600 selection:text-white', darkMode ? 'bg-black text-slate-100' : 'bg-slate-50 text-slate-900']">
    
    <!-- HEADER -->
    <header :class="['fixed top-0 left-0 right-0 z-50 backdrop-blur-md border-b transition-colors duration-300', darkMode ? 'bg-black/80 border-zinc-900' : 'bg-white/90 border-slate-200 shadow-sm']">
      <div class="max-w-7xl mx-auto px-6 h-20 flex items-center justify-between">
        
        <a href="#hero" :class="['text-2xl font-black tracking-tighter transition uppercase', darkMode ? 'text-white' : 'text-slate-900']">
          AHDAM<span class="text-red-600">.</span>
        </a>

        <!-- Desktop Navigation -->
        <nav class="hidden md:flex items-center gap-8 text-xs font-bold tracking-widest">
          <a
            v-for="item in navItems"
            :key="item.id"
            :href="`#${item.id}`"
            :class="[
              'transition-colors uppercase hover:text-red-600',
              activeSection === item.id 
                ? 'text-red-600 border-b-2 border-red-600 pb-0.5' 
                : darkMode ? 'text-zinc-400' : 'text-slate-600'
            ]"
          >
            {{ item.label }}
          </a>
        </nav>

        <!-- Right Controls -->
        <div class="flex items-center gap-4">
          <button
            @click="toggleDarkMode"
            :class="[
              'p-2.5 rounded-xl transition-all border',
              darkMode 
                ? 'bg-zinc-900 text-amber-400 border-zinc-800 hover:bg-zinc-800' 
                : 'bg-slate-100 text-slate-700 border-slate-200 hover:bg-slate-200'
            ]"
            aria-label="Toggle Theme"
          >
            <Sun v-if="darkMode" class="w-4 h-4" />
            <Moon v-else class="w-4 h-4" />
          </button>

          <a 
            href="#contact" 
            class="hidden sm:inline-flex px-5 py-2.5 rounded-full bg-red-600 hover:bg-red-700 text-white text-xs font-black tracking-wider uppercase transition-all shadow-md shadow-red-600/30"
          >
            CONTACT ME
          </a>

          <button @click="mobileMenuOpen = !mobileMenuOpen" class="md:hidden p-2 text-slate-500 hover:text-slate-900">
            <X v-if="mobileMenuOpen" class="w-6 h-6" />
            <Menu v-else class="w-6 h-6" />
          </button>
        </div>
      </div>

      <!-- Mobile Menu -->
      <div v-if="mobileMenuOpen" :class="['md:hidden border-b px-6 py-4 space-y-3', darkMode ? 'bg-zinc-950 border-zinc-900' : 'bg-white border-slate-200']">
        <a
          v-for="item in navItems"
          :key="item.id"
          :href="`#${item.id}`"
          @click="mobileMenuOpen = false"
          :class="['block py-2 uppercase font-bold text-sm tracking-wider', activeSection === item.id ? 'text-red-600 font-extrabold' : darkMode ? 'text-zinc-300' : 'text-slate-700']"
        >
          {{ item.label }}
        </a>
      </div>
    </header>

    <!-- SIDE SOCIAL BAR -->
    <aside :class="['fixed left-6 top-1/2 -translate-y-1/2 z-40 hidden xl:flex flex-col gap-6', darkMode ? 'text-zinc-400' : 'text-slate-500']">
      <a :href="PORTFOLIO_DATA.personal.instagram" target="_blank" class="hover:text-red-600 transition-colors p-1.5 rounded-lg hover:bg-slate-200/50 dark:hover:bg-zinc-900">
        <Instagram class="w-5 h-5" />
      </a>
      <a :href="PORTFOLIO_DATA.personal.linkedin" target="_blank" class="hover:text-red-600 transition-colors p-1.5 rounded-lg hover:bg-slate-200/50 dark:hover:bg-zinc-900">
        <Linkedin class="w-5 h-5" />
      </a>
      <a :href="PORTFOLIO_DATA.personal.github" target="_blank" class="hover:text-red-600 transition-colors p-1.5 rounded-lg hover:bg-slate-200/50 dark:hover:bg-zinc-900">
        <Github class="w-5 h-5" />
      </a>
    </aside>

    <main class="pt-20">
      
      <!-- HERO SECTION -->
      <section id="hero" class="relative min-h-[90vh] flex flex-col justify-center items-center overflow-hidden px-4">
        
        <!-- Glow Merah di Latar Belakang -->
        <div class="absolute inset-0 flex items-center justify-center pointer-events-none">
          <div class="w-[500px] h-[500px] bg-red-600/20 rounded-full blur-[150px] animate-pulse"></div>
        </div>

        <div 
          class="relative w-full max-w-6xl mx-auto flex flex-col items-center justify-center text-center cursor-pointer"
          @mouseenter="isHovered = true"
          @mouseleave="isHovered = false"
        >
          
          <!-- Teks Nama AHDAM -->
          <div 
            :class="[
              'select-none text-[12vw] lg:text-[11vw] font-black tracking-tighter leading-none uppercase transition-all duration-700 ease-out',
              isHovered 
                ? 'text-white opacity-100 drop-shadow-[0_10px_35px_rgba(255,255,255,0.25)]' 
                : 'text-zinc-800 opacity-40'
            ]"
          >
            {{ PORTFOLIO_DATA.personal.firstName }}
          </div>

          <!-- Teks Nama ASHARI -->
          <div 
            :class="[
              'select-none text-[12vw] lg:text-[11vw] font-black tracking-tighter leading-none uppercase -mt-4 md:-mt-12 transition-all duration-700 ease-out',
              isHovered 
                ? 'text-red-600 opacity-100 drop-shadow-[0_10px_45px_rgba(229,9,20,0.6)]' 
                : 'text-red-950/40 opacity-30'
            ]"
          >
            {{ PORTFOLIO_DATA.personal.lastName }}
          </div>

          <!-- Foto Profil (Diatur Jarak Gesernya Lebih Jauh ke Kanan + Responsif) -->
          <div class="absolute inset-0 flex items-center justify-center pointer-events-none z-10">
            <div 
              :class="[
                'hero-photo-container pointer-events-auto transition-all duration-700 cubic-bezier(0.34, 1.56, 0.64, 1)',
                isHovered 
                  ? 'translate-x-[42vw] md:translate-x-[36vw] lg:translate-x-[420px] scale-90' 
                  : 'translate-x-0 scale-100'
              ]"
            >
              <div class="relative w-48 sm:w-56 md:w-64 h-60 sm:h-72 md:h-[380px] rounded-2xl overflow-hidden shadow-[0_25px_60px_rgba(0,0,0,0.9)] border border-zinc-800/80">
                <img 
                  :src="PORTFOLIO_DATA.personal.avatar" 
                  :alt="PORTFOLIO_DATA.personal.name"
                  class="w-full h-full object-cover object-top transition-transform duration-500 hover:scale-105"
                />
                <div class="absolute inset-0 bg-gradient-to-t from-black/80 via-transparent to-transparent"></div>
              </div>
            </div>
          </div>

        </div>
      </section>

      <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 space-y-24 py-12">
        
        <!-- ABOUT ME & SKILLS COMBINED SECTION -->
        <section id="about" class="scroll-mt-24">
          <div :class="['border rounded-[2.5rem] p-8 md:p-12 shadow-lg space-y-10 transition-colors', darkMode ? 'bg-zinc-900/40 border-zinc-800' : 'bg-white border-slate-200/90 shadow-slate-200/50']">
            
            <div class="grid md:grid-cols-12 gap-8 items-start">
              <div class="md:col-span-5 space-y-4">
                <span class="text-xs font-black tracking-widest text-red-600 uppercase">[ 01 . PROFILE ]</span>
                <h2 :class="['text-4xl md:text-5xl font-black tracking-tight uppercase', darkMode ? 'text-white' : 'text-slate-900']">ABOUT <span class="text-red-600">ME</span></h2>
                
                <div :class="['text-xs font-bold space-y-2 uppercase pt-2', darkMode ? 'text-zinc-400' : 'text-slate-600']">
                  <p>NAME: <span :class="darkMode ? 'text-white' : 'text-slate-900'">{{ PORTFOLIO_DATA.personal.name }}</span></p>
                  <p>LOCATION: <span :class="darkMode ? 'text-white' : 'text-slate-900'">{{ PORTFOLIO_DATA.personal.location }}</span></p>
                  <p>STATUS: <span :class="darkMode ? 'text-white' : 'text-slate-900'">STUDENT / DEVELOPER</span></p>
                </div>

                <div class="pt-2">
                  <a href="#contact" class="inline-flex items-center gap-2 px-5 py-3 rounded-xl bg-red-600 hover:bg-red-700 text-white text-xs font-black tracking-wider uppercase transition shadow-md shadow-red-600/20">
                    <Download class="w-4 h-4" /> DOWNLOAD CV
                  </a>
                </div>
              </div>

              <div class="md:col-span-7 space-y-4">
                <p :class="['text-sm md:text-base leading-relaxed font-medium', darkMode ? 'text-zinc-300' : 'text-slate-700']">
                  {{ PORTFOLIO_DATA.personal.bio }}
                </p>

                <div class="grid grid-cols-2 gap-4 pt-4">
                  <div 
                    v-for="(stat, idx) in PORTFOLIO_DATA.personal.stats" 
                    :key="idx" 
                    :class="['p-4 rounded-2xl border text-center transition-colors', darkMode ? 'bg-black/50 border-zinc-800' : 'bg-slate-50 border-slate-200']"
                  >
                    <div class="text-2xl font-black text-red-600">{{ stat.value }}</div>
                    <div :class="['text-[10px] uppercase font-bold mt-1', darkMode ? 'text-zinc-400' : 'text-slate-500']">{{ stat.label }}</div>
                  </div>
                </div>
              </div>
            </div>

            <!-- SKILLS & TOOLS CARDS WITH LOGOS/ICONS -->
            <div :class="['grid md:grid-cols-3 gap-6 pt-8 border-t', darkMode ? 'border-zinc-800' : 'border-slate-200']">
              
              <!-- Software Engineer Card -->
              <div :class="['border p-6 rounded-2xl space-y-4 transition-colors', darkMode ? 'bg-black/60 border-zinc-800/80' : 'bg-slate-50 border-slate-200']">
                <h3 class="text-xs font-black tracking-widest text-red-600 uppercase">SOFTWARE ENGINEER</h3>
                <div class="flex flex-wrap gap-2">
                  <div 
                    v-for="(skill, idx) in PORTFOLIO_DATA.skills.softwareEngineer" 
                    :key="idx" 
                    :class="[
                      'flex items-center gap-2 text-xs px-3 py-2 rounded-xl border font-bold transition-all hover:border-red-600/50',
                      darkMode ? 'bg-zinc-900 border-zinc-800 text-zinc-200' : 'bg-white border-slate-200 text-slate-800 shadow-sm'
                    ]"
                  >
                    <img :src="skill.icon" :alt="skill.name" class="w-4 h-4 object-contain" />
                    <span>{{ skill.name }}</span>
                  </div>
                </div>
              </div>

              <!-- Tools & Server Card -->
              <div :class="['border p-6 rounded-2xl space-y-4 transition-colors', darkMode ? 'bg-black/60 border-zinc-800/80' : 'bg-slate-50 border-slate-200']">
                <h3 class="text-xs font-black tracking-widest text-red-600 uppercase">TOOLS & SERVER</h3>
                <div class="flex flex-wrap gap-2">
                  <div 
                    v-for="(tool, idx) in PORTFOLIO_DATA.skills.toolsServer" 
                    :key="idx" 
                    :class="[
                      'flex items-center gap-2 text-xs px-3 py-2 rounded-xl border font-bold transition-all hover:border-red-600/50',
                      darkMode ? 'bg-zinc-900 border-zinc-800 text-zinc-200' : 'bg-white border-slate-200 text-slate-800 shadow-sm'
                    ]"
                  >
                    <img :src="tool.icon" :alt="tool.name" class="w-4 h-4 object-contain" />
                    <span>{{ tool.name }}</span>
                  </div>
                </div>
              </div>

              <!-- Soft Skills Card -->
              <div :class="['border p-6 rounded-2xl space-y-4 transition-colors', darkMode ? 'bg-black/60 border-zinc-800/80' : 'bg-slate-50 border-slate-200']">
                <h3 class="text-xs font-black tracking-widest text-red-600 uppercase">SOFT SKILLS</h3>
                <div class="flex flex-wrap gap-2">
                  <div 
                    v-for="(soft, idx) in PORTFOLIO_DATA.skills.softSkills" 
                    :key="idx" 
                    :class="[
                      'flex items-center gap-2 text-xs px-3 py-2 rounded-xl border font-bold transition-all hover:border-red-600/50',
                      darkMode ? 'bg-zinc-900 border-zinc-800 text-zinc-200' : 'bg-white border-slate-200 text-slate-800 shadow-sm'
                    ]"
                  >
                    <component :is="soft.icon" class="w-4 h-4 text-red-600" />
                    <span>{{ soft.name }}</span>
                  </div>
                </div>
              </div>

            </div>

          </div>
        </section>

      </div>

      <!-- TICKER MARQUEE BANNER -->
      <div :class="['my-16 py-5 border-y overflow-hidden select-none transition-colors', darkMode ? 'bg-black border-zinc-900 text-zinc-400' : 'bg-white border-slate-200 text-slate-700 shadow-sm']">
        <div class="flex whitespace-nowrap gap-8 text-sm md:text-base font-black tracking-widest uppercase animate-marquee">
          <span>SCALABLE SYSTEM</span>
          <span class="text-red-600">•</span>
          <span>CLEAN CODE</span>
          <span class="text-red-600">•</span>
          <span>HIGH PERFORMANCE</span>
          <span class="text-red-600">•</span>
          <span>FULL-STACK DEVELOPMENT</span>
          <span class="text-red-600">•</span>
          <span>RESPONSIVE UI</span>
          <span class="text-red-600">•</span>
          <span>SCALABLE SYSTEM</span>
          <span class="text-red-600">•</span>
          <span>CLEAN CODE</span>
          <span class="text-red-600">•</span>
          <span>HIGH PERFORMANCE</span>
        </div>
      </div>

      <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 space-y-24">

        <!-- PROJECTS SECTION (DENGAN LOGO DI TAG TECH STACK) -->
        <section id="projects" class="scroll-mt-24">
          <div class="flex items-center gap-3 mb-6">
            <FolderGit2 class="w-6 h-6 text-red-600" />
            <h2 :class="['text-2xl sm:text-3xl font-black tracking-tight', darkMode ? 'text-white' : 'text-slate-900']">Proyek Portofolio</h2>
          </div>

          <div class="flex flex-wrap gap-2 mb-8">
            <button
              v-for="cat in ['All', 'Web App']"
              :key="cat"
              @click="projectCategory = cat"
              :class="[
                'px-4 py-1.5 rounded-lg text-xs font-bold transition',
                projectCategory === cat 
                  ? 'bg-red-600 text-white' 
                  : darkMode ? 'bg-zinc-900 text-slate-400 hover:bg-zinc-800' : 'bg-white border border-slate-200 text-slate-700 hover:bg-slate-100'
              ]"
            >
              {{ cat }}
            </button>
          </div>

          <div class="grid md:grid-cols-2 gap-8">
            <div 
              v-for="project in filteredProjects" 
              :key="project.id" 
              :class="[
                'group rounded-3xl overflow-hidden border transition-all duration-300 flex flex-col justify-between',
                darkMode ? 'bg-zinc-900/40 border-zinc-800 hover:border-red-600/50' : 'bg-white border-slate-200 shadow-md hover:border-red-600/50'
              ]"
            >
              <div>
                <div class="relative overflow-hidden aspect-video bg-zinc-900">
                  <img :src="project.image" :alt="project.title" class="w-full h-full object-cover group-hover:scale-105 transition duration-500" />
                  <div class="absolute top-3 right-3 bg-black/80 backdrop-blur-md px-2.5 py-1 rounded-md text-[10px] font-bold text-red-500 border border-zinc-700">
                    {{ project.category }}
                  </div>
                </div>

                <div class="p-6">
                  <h3 :class="['text-xl font-black mb-2 transition group-hover:text-red-600', darkMode ? 'text-white' : 'text-slate-900']">{{ project.title }}</h3>
                  <p :class="['text-sm line-clamp-2 mb-4 font-medium', darkMode ? 'text-slate-400' : 'text-slate-600']">{{ project.description }}</p>
                  
                  <!-- TAGS DENGAN LOGO MASING-MASING TEKNOLOGI -->
                  <div class="flex flex-wrap gap-2 mb-4">
                    <span 
                      v-for="(tag, tIdx) in project.tags" 
                      :key="tIdx" 
                      :class="[
                        'inline-flex items-center gap-1.5 text-[11px] px-2.5 py-1 rounded-lg font-bold border transition-colors', 
                        darkMode ? 'bg-zinc-900/80 border-zinc-800 text-zinc-300' : 'bg-slate-100 border-slate-200 text-slate-700'
                      ]"
                    >
                      <img 
                        v-if="TECH_ICONS[tag]" 
                        :src="TECH_ICONS[tag]" 
                        :alt="tag" 
                        class="w-3.5 h-3.5 object-contain" 
                      />
                      <span>{{ tag }}</span>
                    </span>
                  </div>
                </div>
              </div>

              <div :class="['p-5 border-t flex items-center justify-between text-xs font-bold', darkMode ? 'border-zinc-800' : 'border-slate-100']">
                <button @click="selectedProject = project" class="text-red-600 hover:underline inline-flex items-center gap-1 uppercase">
                  Detail Proyek
                </button>
                <div class="flex items-center gap-4">
                  <a :href="project.githubLink" target="_blank" rel="noreferrer" :class="darkMode ? 'text-slate-400 hover:text-white' : 'text-slate-500 hover:text-slate-900'">
                    <Github class="w-4 h-4" />
                  </a>
                  <a :href="project.liveLink" target="_blank" rel="noreferrer" class="text-red-600 hover:text-red-700 flex items-center gap-0.5">
                    Demo <ArrowUpRight class="w-3.5 h-3.5" />
                  </a>
                </div>
              </div>
            </div>
          </div>
        </section>

        <!-- PUBLICATIONS SECTION -->
        <section id="publications" class="scroll-mt-24">
          <div class="flex items-center gap-3 mb-8">
            <FileText class="w-6 h-6 text-red-600" />
            <h2 :class="['text-2xl sm:text-3xl font-black tracking-tight', darkMode ? 'text-white' : 'text-slate-900']">Publikasi Jurnal</h2>
          </div>

          <div class="grid gap-4">
            <div 
              v-for="(pub, idx) in PORTFOLIO_DATA.publications" 
              :key="idx" 
              :class="[
                'p-6 rounded-2xl border flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 transition-colors', 
                darkMode ? 'bg-zinc-900/40 border-zinc-800' : 'bg-white border-slate-200 shadow-sm'
              ]"
            >
              <div class="space-y-2">
                <div class="flex items-center gap-2">
                  <span class="text-xs px-2.5 py-0.5 rounded-full bg-red-600/10 text-red-600 font-bold border border-red-600/20">
                    {{ pub.category }}
                  </span>
                  <span :class="['text-xs font-bold', darkMode ? 'text-slate-400' : 'text-slate-500']">{{ pub.period }}</span>
                </div>
                <h3 :class="['text-lg font-bold transition hover:text-red-600', darkMode ? 'text-white' : 'text-slate-900']">{{ pub.title }}</h3>
                <p :class="['text-xs max-w-2xl leading-relaxed font-medium', darkMode ? 'text-slate-400' : 'text-slate-600']">{{ pub.description }}</p>
              </div>
              
              <a :href="pub.link" target="_blank" rel="noreferrer" class="inline-flex items-center gap-1.5 px-4 py-2 rounded-xl bg-red-600/10 hover:bg-red-600/20 text-red-600 text-xs font-black border border-red-600/20 whitespace-nowrap transition">
                Baca Jurnal <ArrowUpRight class="w-3.5 h-3.5" />
              </a>
            </div>
          </div>
        </section>

        <!-- CONTACT SECTION -->
        <section id="contact" class="scroll-mt-24">
          <div class="flex items-center gap-3 mb-8">
            <Mail class="w-6 h-6 text-red-600" />
            <h2 :class="['text-2xl sm:text-3xl font-black tracking-tight', darkMode ? 'text-white' : 'text-slate-900']">Hubungi Saya</h2>
          </div>

          <div class="grid md:grid-cols-2 gap-8">
            <div class="space-y-4">
              <h3 :class="['text-xl font-bold', darkMode ? 'text-white' : 'text-slate-900']">Mari Berdiskusi Proyek Selanjutnya!</h3>
              <p :class="['text-sm leading-relaxed font-medium', darkMode ? 'text-slate-400' : 'text-slate-600']">
                Apakah Anda memiliki ide proyek, tawaran pekerjaan, atau sekadar ingin bertanya? Silakan kirim pesan melalui formulir atau kontak sosial media saya.
              </p>
              
              <div class="space-y-3 pt-4">
                <div :class="['flex items-center gap-3 text-sm font-bold', darkMode ? 'text-slate-300' : 'text-slate-700']">
                  <Mail class="w-4 h-4 text-red-600" />
                  <span>{{ PORTFOLIO_DATA.personal.email }}</span>
                </div>
                <div :class="['flex items-center gap-3 text-sm font-bold', darkMode ? 'text-slate-300' : 'text-slate-700']">
                  <Globe class="w-4 h-4 text-red-600" />
                  <span>{{ PORTFOLIO_DATA.personal.location }}</span>
                </div>
              </div>
            </div>

            <!-- Contact Form -->
            <form 
              @submit.prevent="handleFormSubmit" 
              :class="['p-6 rounded-2xl border space-y-4 transition-colors', darkMode ? 'bg-zinc-900/50 border-zinc-800' : 'bg-white border-slate-200 shadow-md']"
            >
              <div v-if="formSubmitted" class="p-3 bg-emerald-500/10 border border-emerald-500/30 text-emerald-600 rounded-lg text-xs font-bold flex items-center gap-2">
                <CheckCircle2 class="w-4 h-4" /> Pesan berhasil dikirim! Saya akan membalas secepatnya.
              </div>

              <div>
                <label :class="['block text-xs font-bold uppercase mb-1', darkMode ? 'text-slate-400' : 'text-slate-600']">Nama</label>
                <input 
                  type="text" 
                  required 
                  placeholder="Nama Lengkap Anda" 
                  :class="[
                    'w-full px-3 py-2.5 rounded-lg text-sm border outline-none focus:border-red-600 transition font-medium',
                    darkMode ? 'bg-black border-zinc-800 text-slate-100' : 'bg-slate-50 border-slate-300 text-slate-900'
                  ]" 
                />
              </div>

              <div>
                <label :class="['block text-xs font-bold uppercase mb-1', darkMode ? 'text-slate-400' : 'text-slate-600']">Email</label>
                <input 
                  type="email" 
                  required 
                  placeholder="email@example.com" 
                  :class="[
                    'w-full px-3 py-2.5 rounded-lg text-sm border outline-none focus:border-red-600 transition font-medium',
                    darkMode ? 'bg-black border-zinc-800 text-slate-100' : 'bg-slate-50 border-slate-300 text-slate-900'
                  ]" 
                />
              </div>

              <div>
                <label :class="['block text-xs font-bold uppercase mb-1', darkMode ? 'text-slate-400' : 'text-slate-600']">Pesan</label>
                <textarea 
                  :rows="4" 
                  required 
                  placeholder="Tuliskan pesan atau detail proyek Anda..." 
                  :class="[
                    'w-full px-3 py-2.5 rounded-lg text-sm border outline-none focus:border-red-600 transition font-medium',
                    darkMode ? 'bg-black border-zinc-800 text-slate-100' : 'bg-slate-50 border-slate-300 text-slate-900'
                  ]" 
                />
              </div>

              <button type="submit" class="w-full py-3 rounded-xl bg-red-600 hover:bg-red-700 text-white font-black text-xs tracking-wider uppercase transition flex items-center justify-center gap-2 shadow-md shadow-red-600/20">
                <Send class="w-4 h-4" /> Kirim Pesan
              </button>
            </form>
          </div>
        </section>

      </div>
    </main>

    <!-- MODAL DETAIL PROYEK -->
    <div v-if="selectedProject" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/80 backdrop-blur-sm">
      <div :class="['max-w-lg w-full rounded-3xl border p-6 space-y-4 shadow-2xl', darkMode ? 'bg-zinc-900 border-zinc-800 text-white' : 'bg-white border-slate-200 text-slate-900']">
        <div class="flex justify-between items-start">
          <h3 class="text-xl font-black uppercase">{{ selectedProject.title }}</h3>
          <button @click="selectedProject = null" class="text-slate-400 hover:text-slate-600 dark:hover:text-white">
            <X class="w-5 h-5" />
          </button>
        </div>

        <img :src="selectedProject.image" :alt="selectedProject.title" class="w-full h-48 object-cover rounded-2xl border border-slate-200 dark:border-zinc-800" />
        <p :class="['text-xs leading-relaxed font-medium', darkMode ? 'text-slate-400' : 'text-slate-600']">{{ selectedProject.description }}</p>

        <!-- TAGS MODAL DENGAN LOGO -->
        <div class="flex flex-wrap gap-2">
          <span 
            v-for="(t, idx) in selectedProject.tags" 
            :key="idx" 
            class="inline-flex items-center gap-1.5 text-xs px-2.5 py-1 rounded-md bg-red-600/10 text-red-600 font-bold"
          >
            <img 
              v-if="TECH_ICONS[t]" 
              :src="TECH_ICONS[t]" 
              :alt="t" 
              class="w-3.5 h-3.5 object-contain" 
            />
            <span>{{ t }}</span>
          </span>
        </div>

        <div class="flex justify-end gap-3 pt-2 border-t border-slate-200 dark:border-zinc-800">
          <a :href="selectedProject.githubLink" target="_blank" rel="noreferrer" :class="['px-4 py-2 rounded-xl border text-xs font-bold uppercase transition', darkMode ? 'border-zinc-700 hover:bg-zinc-800' : 'border-slate-300 hover:bg-slate-100']">
            GitHub Repo
          </a>
          <a :href="selectedProject.liveLink" target="_blank" rel="noreferrer" class="px-4 py-2 rounded-xl bg-red-600 text-white text-xs font-bold uppercase hover:bg-red-700 shadow-md shadow-red-600/30">
            Buka Live Demo
          </a>
        </div>
      </div>
    </div>

    <!-- FOOTER -->
    <footer :class="['border-t py-8 mt-20 text-center text-xs font-bold tracking-wider uppercase transition-colors', darkMode ? 'border-zinc-900 bg-black text-slate-500' : 'border-slate-200 bg-white text-slate-500']">
      <p>© {{ new Date().getFullYear() }} {{ PORTFOLIO_DATA.personal.name }}. Dibuat dengan Vue 3 & Tailwind CSS.</p>
    </footer>

  </div>
</template>

<style scoped>
/* Animasi Turun Foto Utama */
.hero-photo-container {
  animation: photoSlideDownLong 1.8s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

@keyframes photoSlideDownLong {
  0% {
    opacity: 0;
    transform: translateY(-160px) scale(0.85);
  }
  100% {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

/* Animasi Marquee Running Text */
@keyframes marquee {
  0% { transform: translateX(0%); }
  100% { transform: translateX(-50%); }
}

.animate-marquee {
  display: flex;
  width: 200%;
  animation: marquee 20s linear infinite;
}

.animate-marquee:hover {
  animation-play-state: paused;
}
</style>