<template>
  <section ref="mainSection" class="flex flex-col md:flex-row justify-between items-center px-6 sm:px-12 md:px-32 py-12 md:py-0 min-h-screen md:h-screen">
    
    <!-- Texto principal -->
    <div ref="textRef"
      :class="['flex flex-col space-y-4 transition-opacity duration-700 text-center md:text-left mt-3 md:mt-0 md:ml-10',
        textVisible ? 'animate-slide-in opacity-100' : 'opacity-0',
      ]"
    >
      <p class="text-purple-500 text-lg sm:text-xl font-semibold">{{ introText }}</p>

      <h1 class="text-5xl sm:text-6xl md:text-8xl font-semibold text-white drop-shadow-[0_0_15px_rgba(168,85,247,0.8)]">
        {{ firstName }}
      </h1>

      <h1 class="text-5xl sm:text-6xl md:text-8xl font-semibold">
        <span class="bg-gradient-to-r from-purple-500 to-blue-500 bg-clip-text text-transparent drop-shadow-[0_0_25px_rgba(168,85,247,0.8)]">
          {{ lastName }}
        </span>
      </h1>

      <!-- Typewriter -->
      <p class="mt-2 md:mt-4 text-lg sm:text-xl md:text-2xl text-gray-300 font-light h-8 flex items-center justify-center md:justify-start">
        {{ typeWriterText }}
        <span class="w-1 h-6 bg-purple-500 ml-1"></span>
      </p>

      <!-- Descripción -->
      <div class="text-gray-300 text-base sm:text-lg md:text-xl mt-2 md:mt-0">
        <p v-for="(line, index) in description" :key="index">{{ line }}</p>
      </div>

      <!-- Botones -->
      <div class="flex flex-row flex-nowrap justify-center md:justify-start gap-4 sm:gap-8 mt-4 md:mt-6">
        <a
          v-for="(btn, index) in buttons"
          :key="index"
          :href="btn.link"
          :download="btn.download || null"
          :class="`${btn.classes} flex items-center gap-2 text-[13px] sm:text-sm md:text-base`"
        >
          <span>{{ btn.text }}</span>
          <span v-html="btn.icon"></span>
        </a>
      </div>
    </div>

    <!-- Foto -->
    <div ref="photoRef"
      :class="['rounded-full overflow-hidden shadow-[0_0_25px_rgba(168,85,247,0.8)] mt-11 md:mt-0 md:mr-19 transition-opacity duration-700',
        photoVisible
          ? 'animate-slide-in-right-bounce opacity-100'
          : 'opacity-0',
      ]"
    >
      <img :src="photo.src" alt="Itzel" class="w-52 h-52 sm:w-64 sm:h-64 md:w-80 md:h-80 object-cover"/>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from "vue";
import ItzelImg from "../assets/profile/Itzel.jpg";

// Datos
const introText = "Hola mundo, soy";
const firstName = "Itzel";
const lastName = "Padilla";

const textsTypeWriter = [
  "Desarrolladora Frontend Junior",
  "Ingeniera en Sistemas Computacionales",
];

const typeWriterText = ref("");
const photo = { src: ItzelImg };

const description = [
  "Enfocada en el desarrollo web, con más de 2 años de experiencia",
  "construyendo aplicaciones enfocadas en la experiencia del usuario.",
];

// Botones
const buttons = [
  {
    text: "Proyectos",
    link: "#Proyectos",
    classes:"px-4 py-3 sm:px-6 sm:py-3 bg-gradient-to-r from-purple-500 to-blue-500 text-white font-medium rounded-lg transition-all hover:scale-105",
    icon: `<svg class="w-5 h-5 sm:w-6 sm:h-6 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"><path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M18 14v4.833A1.166 1.166 0 0 1 16.833 20H5.167A1.167 1.167 0 0 1 4 18.833V7.167A1.166 1.166 0 0 1 5.167 6h4.618m4.447-2H20v5.768m-7.889 2.121 7.778-7.778"/></svg>`,
  },
  {
    text: "Descargar CV",
    link: "/CV_ItzelLarragaPadilla.pdf",
    download: "CV_ItzelLarragaPadilla.pdf",
    classes:"px-4 py-3 sm:px-6 sm:py-3 border border-purple-500 text-white font-medium rounded-lg transition-transform transform hover:scale-105",
    icon: `<svg class="w-5 h-5 sm:w-6 sm:h-6 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"><path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 15v2a3 3 0 0 0 3 3h10a3 3 0 0 0 3-3v-2m-8 1V4m0 12-4-4m4 4 4-4"/></svg>`,
  },
];

// Utilidad sleep
const sleep = (ms) => new Promise((res) => setTimeout(res, ms));

// Efecto Typewriter
const typeWriterEffect = async () => {
  let current = 0;
  while (true) {
    const text = textsTypeWriter[current];
    for (let i = 0; i <= text.length; i++) {
      typeWriterText.value = text.slice(0, i);
      await sleep(100);
    }
    await sleep(1000);
    for (let i = text.length; i >= 0; i--) {
      typeWriterText.value = text.slice(0, i);
      await sleep(50);
    }
    current = (current + 1) % textsTypeWriter.length;
  }
};

// IntersectionObserver
const textRef = ref(null);
const photoRef = ref(null);
const textVisible = ref(false);
const photoVisible = ref(false);

onMounted(() => {
  typeWriterEffect();

  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (!entry.isIntersecting) return;
        if (entry.target === textRef.value) textVisible.value = true;
        if (entry.target === photoRef.value) photoVisible.value = true;
      });
    },
    { threshold: 0.2 }
  );

  [textRef, photoRef].forEach((el) => observer.observe(el.value));
});
</script>