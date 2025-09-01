<template>
  <NavbarComp :active-section="activeSection" />

  <main class="w-full overflow-x-hidden -mb-5">
    <section id="Inicio" class="min-h-screen mt-2">
      <HomeComp />
    </section>

    <section id="Sobre mí" class="mb-10 md:mb-15">
      <AboutmeComp />
    </section>

    <section id="Proyectos" class="min-h-screen md:mb-14">
      <ProjectsComp />
    </section>

    <section id="Certificados" class="min-h-screen mb-20 md:mb-0">
      <CertificatesComp />
    </section>
  </main>

  <!-- Footer -->
  <footer class="bg-[#030014] text-gray-400 py-6 text-center border-t border-gray-700">
    <p class="text-sm">
      Creado por <span class="text-purple-400 font-semibold">Itzel Larraga Padilla</span> © 2025
    </p>
    <p class="text-xs mt-1">
      Todos los derechos reservados | 
      <a href="https://github.com/itzeliipadilla" target="_blank" class="hover:text-purple-400 transition">
        GitHub
      </a>
      ·
      <a href="https://www.linkedin.com/in/itzel-padilla-4a1473349/" target="_blank" class="hover:text-purple-400 transition">
        LinkedIn
      </a>
    </p>
  </footer>
</template>


<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import NavbarComp from "./components/NavbarComp.vue";
import HomeComp from "./components/HomeComp.vue";
import AboutmeComp from "./components/AboutmeComp.vue";
import ProjectsComp from "./components/ProjectsComp.vue";
import CertificatesComp from "./components/CertificatesComp.vue";

const activeSection = ref("Inicio");

const sections = ["Inicio", "Sobre mí", "Proyectos", "Certificados"];

// Detecta la sección visible según scroll
const updateActiveSection = () => {
  const scrollPos = window.scrollY + 200; // Ajuste navbar fija
  for (const id of sections) {
    const el = document.getElementById(id);
    if (
      el &&
      scrollPos >= el.offsetTop &&
      scrollPos < el.offsetTop + el.offsetHeight
    ) {
      activeSection.value = id;
      break;
    }
  }
};

// Listener de scroll
onMounted(() => window.addEventListener("scroll", updateActiveSection));
onUnmounted(() => window.removeEventListener("scroll", updateActiveSection));
</script>

