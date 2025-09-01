<template>
  <section class="flex flex-col justify-start items-center px-8 md:px-32 space-y-12 mt-8 md:mt-0">

    <!-- Título -->
    <div ref="titleRef" :class="{ 'animate-zoom-in': titleVisible }" class="text-center opacity-0">
      <h2 class="text-4xl md:text-6xl font-medium text-purple-500 mb-4">Sobre mí</h2>
      <p class="text-gray-300 text-lg md:text-xl animate-zoom-in-delay">
        Transformando ideas en experiencias digitales
      </p>
    </div>

    <div class="flex flex-col md:flex-row items-center md:items-start md:space-x-12 w-full -mt-8 md:mt-8">
      
      <!-- Foto -->
      <div ref="photoRef" :class="{ 'animate-slide-in-left': photoVisible }"
        class="rounded-lg overflow-hidden shadow-[0_0_25px_rgba(100,150,255,0.5)] flex-shrink-0 mt-8 md:mt-0 ml-0 md:ml-12 opacity-0 w-[300px] h-[200px] md:w-[550px] md:h-[280px]"
      >
        <img :src="photo.src" alt="Foto" class="w-full h-full object-cover" />
      </div>

      <!-- Descripción -->
      <div ref="textRef" :class="{ 'animate-slide-in-right': textVisible }"
        class="flex flex-col space-y-4 text-gray-300 w-full md:w-[46%] mt-12 md:mt-0"
      >
        <p v-for="(line, index) in description" :key="index" class="text-lg text-justify">{{ line }}</p>

        <!-- Botones -->
        <div class="flex flex-row flex-wrap justify-center md:justify-start gap-4 mt-4">
          <a v-for="(btn, index) in buttons" :key="index" :href="btn.link" target="_blank"
            class="px-6 py-3 rounded-xl bg-black flex items-center justify-center shadow-[0_0_15px_rgba(100,150,255,0.6)] hover:shadow-[0_0_25px_rgba(100,150,255,0.8)] transition-all"
          >
            <span v-html="btn.icon" class="mr-2"></span>
            {{ btn.text }}
          </a>
        </div>
      </div>
    </div>

    <!-- Tecnologías -->
    <div ref="techTitleRef" :class="{ 'animate-zoom-in': techTitleVisible }" class="w-full mt-8 md:mt-12 opacity-0">
      <div class="flex items-center space-x-4 ml-2 sm:ml-10 justify-center sm:justify-start">
        <h2 class="text-3xl md:text-4xl font-medium text-purple-500">
          Tecnologías
        </h2>
        <div class="hidden sm:flex flex-1 max-w-236 h-[2px] bg-gradient-to-r from-blue-500 to-purple-500"></div>
      </div>
    </div>

    <!-- Tarjetas -->
    <div ref="techGridRef" :class="{ 'animate-slide-in': techGridVisible }"
      class="grid grid-cols-2 sm:grid-cols-2 md:grid-cols-5 gap-x-12 gap-y-10 mt-6 md:mt-10 opacity-0 justify-items-center md:justify-items-start"
    >
      <div v-for="(tech, index) in technologies" :key="index"
        class="bg-white/10 backdrop-blur-md rounded-xl p-4 flex flex-col items-center justify-center transition-all duration-300 border border-transparent hover:border-purple-500 hover:scale-105 transform w-[120px] h-[150px] md:w-[198px] md:h-auto md:flex-row md:space-x-6"
      >
        <img :src="tech.img"  :alt="tech.name" class="w-14 h-14 object-contain rounded-md mb-2 md:mb-0 md:mr-2"/>
        <span class="text-white font-normal text-lg text-center md:text-left">{{tech.name}}</span>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from "vue";
import Aboutme from "../assets/profile/Aboutme.jpg";
import HTMLImg from "../assets/skills/HTML.png";
import CSSImg from "../assets/skills/CSS.png";
import JSImg from "../assets/skills/JavaScript.png";
import VueImg from "../assets/skills/Vue.png";
import TailwindImg from "../assets/skills/Tailwind.png";
import BootstrapImg from "../assets/skills/Bootstrap.png";
import FigmaImg from "../assets/skills/Figma.png";
import ReactImg from "../assets/skills/React.png";
import SQLImg from "../assets/skills/SQL.png";

const titleRef = ref(null);
const photoRef = ref(null);
const textRef = ref(null);
const techTitleRef = ref(null);
const techGridRef = ref(null);

const titleVisible = ref(false);
const photoVisible = ref(false);
const textVisible = ref(false);
const techTitleVisible = ref(false);
const techGridVisible = ref(false);

const photo = { src: Aboutme };

// Descripción
const description = [
  "Egresada de Ingeniería en Sistemas Computacionales con gran interés en el desarrollo web. Me enfoco en crear experiencias digitales atractivas y funcionales, siempre buscando aportar soluciones efectivas en cada proyecto.",
  "Curiosa, colaborativa y adaptable, con facilidad para trabajar en equipo y enfrentar retos con creatividad."
];

// Botones
const buttons = [
  {
    text: "GitHub",
    link: "https://github.com/itzeliipadilla",
    icon: '<svg class="w-6 h-6 text-gray-800 dark:text-white" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" viewBox="0 0 24 24"><path fill-rule="evenodd" d="M12.006 2a9.847 9.847 0 0 0-6.484 2.44 10.32 10.32 0 0 0-3.393 6.17 10.48 10.48 0 0 0 1.317 6.955 10.045 10.045 0 0 0 5.4 4.418c.504.095.683-.223.683-.494 0-.245-.01-1.052-.014-1.908-2.78.62-3.366-1.21-3.366-1.21a2.711 2.711 0 0 0-1.11-1.5c-.907-.637.07-.621.07-.621.317.044.62.163.885.346.266.183.487.426.647.71.135.253.318.476.538.655a2.079 2.079 0 0 0 2.37.196c.045-.52.27-1.006.635-1.37-2.219-.259-4.554-1.138-4.554-5.07a4.022 4.022 0 0 1 1.031-2.75 3.77 3.77 0 0 1 .096-2.713s.839-.275 2.749 1.05a9.26 9.26 0 0 1 5.004 0c1.906-1.325 2.74-1.05 2.74-1.05.37.858.406 1.828.101 2.713a4.017 4.017 0 0 1 1.029 2.75c0 3.939-2.339 4.805-4.564 5.058a2.471 2.471 0 0 1 .679 1.897c0 1.372-.012 2.477-.012 2.814 0 .272.18.592.687.492a10.05 10.05 0 0 0 5.388-4.421 10.473 10.473 0 0 0 1.313-6.948 10.32 10.32 0 0 0-3.39-6.165A9.847 9.847 0 0 0 12.007 2Z" clip-rule="evenodd"/></svg>',
    classes:"px-6 py-3 rounded-xl bg-black flex items-center justify-center shadow-[0_0_15px_rgba(100,150,255,0.6)] hover:shadow-[0_0_25px_rgba(100,150,255,0.8)] transition-all",
  },
  {
    text: "LinkedIn",
    link: "https://www.linkedin.com/in/itzel-padilla-4a1473349/",
    icon: '<svg class="w-6 h-6 text-gray-800 dark:text-white" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" viewBox="0 0 24 24"><path fill-rule="evenodd" d="M12.51 8.796v1.697a3.738 3.738 0 0 1 3.288-1.684c3.455 0 4.202 2.16 4.202 4.97V19.5h-3.2v-5.072c0-1.21-.244-2.766-2.128-2.766-1.827 0-2.139 1.317-2.139 2.676V19.5h-3.19V8.796h3.168ZM7.2 6.106a1.61 1.61 0 0 1-.988 1.483 1.595 1.595 0 0 1-1.743-.348A1.607 1.607 0 0 1 5.6 4.5a1.601 1.601 0 0 1 1.6 1.606Z" clip-rule="evenodd"/><path d="M7.2 8.809H4V19.5h3.2V8.809Z"/></svg>',
    classes:"px-6 py-3 rounded-xl bg-black flex items-center justify-center shadow-[0_0_15px_rgba(100,150,255,0.6)] hover:shadow-[0_0_25px_rgba(100,150,255,0.8)] transition-all",
  },
  {
    text: "WhatsApp",
    link: "https://wa.me/4811027300",
    icon: '<svg class="w-6 h-6 text-gray-800 dark:text-white" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24"><path fill="currentColor" fill-rule="evenodd" d="M12 4a8 8 0 0 0-6.895 12.06l.569.718-.697 2.359 2.32-.648.379.243A8 8 0 1 0 12 4ZM2 12C2 6.477 6.477 2 12 2s10 4.477 10 10-4.477 10-10 10a9.96 9.96 0 0 1-5.016-1.347l-4.948 1.382 1.426-4.829-.006-.007-.033-.055A9.958 9.958 0 0 1 2 12Z" clip-rule="evenodd"/><path fill="currentColor" d="M16.735 13.492c-.038-.018-1.497-.736-1.756-.83a1.008 1.008 0 0 0-.34-.075c-.196 0-.362.098-.49.291-.146.217-.587.732-.723.886-.018.02-.042.045-.057.045-.013 0-.239-.093-.307-.123-1.564-.68-2.751-2.313-2.914-2.589-.023-.04-.024-.057-.024-.057.005-.021.058-.074.085-.101.08-.079.166-.182.249-.283l.117-.14c.121-.14.175-.25.237-.375l.033-.066a.68.68 0 0 0-.02-.64c-.034-.069-.65-1.555-.715-1.711-.158-.377-.366-.552-.655-.552-.027 0 0 0-.112.005-.137.005-.883.104-1.213.311-.35.22-.94.924-.94 2.16 0 1.112.705 2.162 1.008 2.561l.041.06c1.161 1.695 2.608 2.951 4.074 3.537 1.412.564 2.081.63 2.461.63.16 0 .288-.013.4-.024l.072-.007c.488-.043 1.56-.599 1.804-1.276.192-.534.243-1.117.115-1.329-.088-.144-.239-.216-.43-.308Z"/></svg>',
    classes:"px-6 py-3 rounded-xl bg-black flex items-center justify-center shadow-[0_0_15px_rgba(100,150,255,0.6)] hover:shadow-[0_0_25px_rgba(100,150,255,0.8)] transition-all",
  },
];

// Tecnologías
const technologies = [
  { name: "HTML", img: HTMLImg },
  { name: "CSS", img: CSSImg },
  { name: "JavaScript", img: JSImg },
  { name: "Vue", img: VueImg },
  { name: "Tailwind CSS", img: TailwindImg },
  { name: "Bootstrap", img: BootstrapImg },
  { name: "Figma", img: FigmaImg },
  { name: "React", img: ReactImg },
  { name: "Sql", img: SQLImg },
];

onMounted(() => {
  const elements = [
    { ref: titleRef, visible: titleVisible },
    { ref: photoRef, visible: photoVisible },
    { ref: textRef, visible: textVisible },
    { ref: techTitleRef, visible: techTitleVisible },
    { ref: techGridRef, visible: techGridVisible },
  ];

  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          const el = elements.find((e) => e.ref.value === entry.target);
          if (el) el.visible.value = true;
        }
      });
    },
    { threshold: 0.2 }
  );

  elements.forEach((e) => observer.observe(e.ref.value));
});
</script>
