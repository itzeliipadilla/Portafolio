<template>
  <section id="projects" class="lg:pt-8">

    <!-- Título -->
    <div class="text-center mb-12 px-4 sm:px-6 mt-6 md:mt-8">
      <h2 ref="projectsTitleRef"
        class="text-4xl sm:text-5xl lg:text-6xl font-medium text-purple-500 mb-4 opacity-0"
        :class="{ 'animate-zoom-in': projectsTitleVisible }"
      >
        Proyectos
      </h2>
      <p ref="projectsSubtitleRef" class="text-base sm:text-lg lg:text-xl text-gray-300 opacity-0" :class="{ 'animate-zoom-in-delay': projectsSubtitleVisible }">
        Algunos de mis trabajos recientes
      </p>
    </div>
    <div ref="projectsCardsTrigger" class="h-1"></div>

    <!-- Cards -->
    <div ref="projectsCardsRef"
      class="flex flex-wrap justify-center gap-8 sm:gap-16 px-2 sm:px-4 opacity-0"
      :class="{ 'animate-slide-in-opposite': projectsCardsVisible }"
    >
      <div v-for="(project, index) in projects" :key="index"
        class="backdrop-blur-md bg-white/10 p-4 sm:p-6 rounded-2xl shadow-lg flex flex-col justify-between w-[290px] sm:w-[300px] lg:w-[350px] h-[320px] sm:h-[390px] border border-white/20 transition-all duration-700 ease-out"
      >
        <div class="h-32 sm:h-40 bg-blue-300 rounded-xl flex items-center justify-center overflow-hidden">
          <img
            :src="project.image"
            :alt="project.title"
            class="w-full h-full object-cover"
          />
        </div>

        <h3 class="md:mt-2 text-lg sm:text-xl font-semibold bg-gradient-to-r from-blue-300 to-pink-200 text-transparent bg-clip-text">
          {{ project.title }}
        </h3>

        <p class="text-sm sm:text-base text-gray-300 line-clamp-2 mb-2">
          {{ project.description }}
        </p>

        <button @click="openFullScreen(project)"
          class="group flex items-center justify-center gap-2 px-4 sm:px-6 py-2 border border-purple-500 bg-[#030014] font-medium rounded-lg cursor-pointer transition-all duration-300 hover:shadow-[0_0_8px_3px_rgba(147,51,234,0.6)]"
        >
          <span class="bg-clip-text text-transparent bg-gradient-to-r from-purple-400 to-blue-400 font-medium text-xs sm:text-sm">
            Detalles
          </span>
          <svg class="w-4 sm:w-5 h-4 sm:h-5 text-purple-400" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M19 12H5m14 0-4 4m4-4-4-4" />
          </svg>
        </button>
      </div>
    </div>

    <!-- Vista proyecto -->
    <transition name="fade-slide">
      <div v-if="selectedProject"
        class="fixed inset-0 bg-[#030014] flex flex-col z-50 p-4 sm:p-8 overflow-y-auto no-scrollbar"
      >
        <div class="flex flex-col lg:flex-row gap-6 lg:gap-12 mb-4 mb:mb-0 h-full mt-5 md:mt-0">
          <div class="flex-1 animate-slide-in-left md:ml-38">
            <button @click="closeFullScreen" class="mb-6 sm:mb-8 px-4 sm:px-5 py-2 rounded-lg border border-white/20 bg-white/10 backdrop-blur-md text-gray-200 hover:bg-white/20 transition shadow-md flex items-center gap-2">
              <svg class="w-4 sm:w-5 h-4 sm:h-5 text-gray-200" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 12h14M5 12l4-4m-4 4 4 4"/>
              </svg>
              <span class="text-sm sm:text-base">Atrás</span>
            </button>

            <h2 class="text-2xl md:h-20 sm:text-3xl lg:text-4xl font-bold bg-gradient-to-r from-blue-200 to-pink-200 text-transparent bg-clip-text mb-4 sm:mb-6">
              {{ selectedProject.title }}
            </h2>

            <div class="h-[3px] w-24 sm:w-32 bg-gradient-to-r from-purple-500 to-blue-500 rounded-full shadow-lg mb-4"></div>
            <p class="text-gray-300 mb-6 sm:mb-8">
              {{ selectedProject.description }}
            </p>

            <a v-if="selectedProject.github" :href="selectedProject.github" target="_blank"
              class="inline-flex items-center gap-2 text-sm sm:text-base px-4 sm:px-6 py-2 rounded-lg font-medium border border-purple-500 text-white hover:bg-purple-500/20 transition mb-6 sm:mb-8"
            >
              <svg class="w-4 sm:w-5 h-4 sm:h-5 text-white" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 24 24">
                <path fill-rule="evenodd" d="M12.006 2a9.847 9.847 0 0 0-6.484 2.44 10.32 10.32 0 0 0-3.393 6.17 10.48 10.48 0 0 0 1.317 6.955 10.045 10.045 0 0 0 5.4 4.418c.504.095.683-.223.683-.494 0-.245-.01-1.052-.014-1.908-2.78.62-3.366-1.21-3.366-1.21a2.711 2.711 0 0 0-1.11-1.5c-.907-.637.07-.621.07-.621.317.044.62.163.885.346.266.183.487.426.647.71.135.253.318.476.538.655a2.079 2.079 0 0 0 2.37.196c.045-.52.27-1.006.635-1.37-2.219-.259-4.554-1.138-4.554-5.07a4.022 4.022 0 0 1 1.031-2.75 3.77 3.77 0 0 1 .096-2.713s.839-.275 2.749 1.05a9.26 9.26 0 0 1 5.004 0c1.906-1.325 2.74-1.05 2.74-1.05.37.858.406 1.828.101 2.713a4.017 4.017 0 0 1 1.029 2.75c0 3.939-2.339 4.805-4.564 5.058a2.471 2.471 0 0 1 .679 1.897c0 1.372-.012 2.477-.012 2.814 0 .272.18.592.687.492a10.05 10.05 0 0 0 5.388-4.421 10.473 10.473 0 0 0 1.313-6.948 10.32 10.32 0 0 0-3.39-6.165A9.847 9.847 0 0 0 12.007 2Z" clip-rule="evenodd"/>
              </svg>
              GitHub
            </a>

            <div class="sm:mt-8 flex items-center gap-2 mb-4 sm:mb-8">
              <span class="text-blue-400 font-bold">&lt;/&gt;</span>
              <h3 class="text-base sm:text-lg text-gray-200 font-semibold">
                Tecnologías usadas
              </h3>
            </div>

            <div class="flex flex-wrap gap-2 sm:gap-3 mt-2 sm:mt-4">
              <span v-for="(tech, i) in selectedProject.technologies" :key="i"
                class="px-2 sm:px-4 py-1 sm:py-2 rounded-lg text-sm sm:text-base font-medium text-blue-300 border border-blue-500 backdrop-blur-md bg-white/5 hover:bg-blue-500/20 transition"
              >
                {{ tech }}
              </span>
            </div>
          </div>

          <!-- Imagen -->
          <div class="flex-1 flex items-center justify-center animate-slide-in-right mt-4 lg:mt-0 md:mr-21">
            <div class="w-full sm:w-130 h-40 sm:h-80 rounded-xl flex items-center justify-center overflow-hidden">
              <img
                :src="selectedProject.image"
                :alt="selectedProject.title"
                class="w-full h-full object-cover"
              />
            </div>
          </div>
        </div>

        <!-- Video -->
        <div class="mt-6 sm:mt-15 rounded-xl overflow-hidden relative pb-[40%] w-full h-[100%] sm:w-[81.5%] md:ml-38 animate-zoom-in-delay">
          <iframe
            v-if="selectedProject.video"
            class="absolute top-0 left-0 w-full md:h-full rounded-xl"
            :src="selectedProject.video"
            frameborder="0"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
            allowfullscreen
          ></iframe>
        </div>
      </div>
    </transition>
  </section>
</template>

<script setup>
import { ref, onMounted } from "vue";
import CatalogoImg from "../assets/projects/Catalogo.png";
import SICIImg from "../assets/projects/SICI.png";
import DashboardImg from "../assets/projects/Dashboard.png";

const projects = ref([
  {
    title: "Catálogo Digital",
    description: "Aplicación web de catálogo digital que ofrece una interfaz pública para la consulta de productos y un panel administrativo para la gestión de inventario. El sistema permite al administrador registrar, actualizar y organizar los productos, así como generar catálogos en formato PDF por categorías. La plataforma es totalmente responsive, asegurando una visualización óptima y accesible en distintos dispositivos.",
    github: "https://github.com/itzeliipadilla/Catalogo-digital",
    technologies: ["Vue", "Tailwind", "Node.js", "Laravel", "Figma"],
    image: CatalogoImg,
    video: "https://www.youtube.com/embed/mlAGP8VsKxE",
  },
  {
    title: "Sistema integral de control de inventario",
    description: "Aplicación web enfocada en la gestión administrativa de inventarios, diseñada para optimizar el control de productos. Comparte la misma API que el Catálogo Digital, lo que asegura coherencia en la información. Desde este panel el administrador puede: registrar unidades de carga, asignar productos a dichas unidades, así como dar de alta a los operadores encargados de manejarlas. El sistema está orientado exclusivamente al entorno administrativo, ya que el módulo de operadores se desarrolló de manera independiente en una aplicación móvil con Flutter.",
    github: "https://github.com/itzeliipadilla/SICI",
    technologies: ["Vue", "Tailwind", "Node.js", "PHP", "Figma"],
    image: SICIImg,
    video: "https://www.youtube.com/embed/pj6VgNpYpok",
  },
  {
    title: "Sistema de registro de pacientes",
    description: "Aplicación web diseñada para optimizar el proceso de registro en las recepciones de un hospital. Cuenta con dos roles principales: administrador y recepcionista. Las recepcionistas pueden registrar a los pacientes atendidos, asociarlos con el doctor correspondiente y especificar el motivo de la atención. El administrador tiene la posibilidad de gestionar recepciones y doctores, además de generar informes generales o específicos por recepción. Todos los reportes pueden exportarse a Excel para un mejor análisis. La plataforma es totalmente responsive, asegurando un uso óptimo en distintos dispositivos.",
    github: "",
    technologies: ["Vue", "Tailwind", "Laravel", "Figma"],
    image: DashboardImg,
    video: "https://www.youtube.com/embed/EkvEe9FZwxU",
  },
]);

const selectedProject = ref(null);

function openFullScreen(project) {
  selectedProject.value = project;
  document.body.style.overflow = "hidden";
}
function closeFullScreen() {
  selectedProject.value = null;
  document.body.style.overflow = "";
}

// Refs y visibilidad
const refsArray = [
  { ref: ref(null), visible: ref(false) }, // Title
  { ref: ref(null), visible: ref(false) }, // Subtitle
  { ref: ref(null), visible: ref(false) }, // Cards Trigger
];

const [projectsTitleRef, projectsSubtitleRef, projectsCardsTrigger] =
  refsArray.map((r) => r.ref);
const [projectsTitleVisible, projectsSubtitleVisible, projectsCardsVisible] =
  refsArray.map((r) => r.visible);

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        const found = refsArray.find((r) => r.ref.value === entry.target);
        if (entry.isIntersecting && found) found.visible.value = true;
      });
    },
    { threshold: 0.2 }
  );

  refsArray.forEach((r) => r.ref.value && observer.observe(r.ref.value));
});
</script>