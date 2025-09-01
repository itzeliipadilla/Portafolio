<template>
  <nav
    class="fixed top-0 left-0 w-full flex justify-between items-center px-10 py-4 z-50 transition-all duration-300"
    :class="[
      scrolled ? 'backdrop-blur-md bg-black/30' : 'bg-transparent',
      'md:bg-transparent bg-[#030014]'
    ]"
  >
    <h1 class="text-2xl md:ml-32 font-bold bg-gradient-to-r from-purple-500 to-blue-500 text-transparent bg-clip-text">
      Itzel LP
    </h1>

    <!-- Menú escritorio -->
    <ul class="hidden md:flex gap-8 text-base font-medium mr-32">
      <li
        v-for="item in menuItems"
        :key="item"
        @click="scrollToSection(item)"
        class="relative cursor-pointer transition-all"
      >
        <span
          :class="[
            active === item
              ? 'bg-gradient-to-r from-purple-500 to-blue-500 text-transparent bg-clip-text'
              : 'text-white'
          ]"
        >
          {{ item }}
        </span>
        <span
          class="absolute left-0 -bottom-1 h-[3px] w-full bg-gradient-to-r from-purple-500 to-blue-500 rounded-full transition-all scale-x-0 origin-left"
          :class="{ 'scale-x-100': active === item }"
        ></span>
      </li>
    </ul>
  </nav>
</template>

<script setup>
import { ref, watch, onMounted, onUnmounted } from "vue";

// Props
const props = defineProps({
  activeSection: String,
});

// Estado sección activa
const active = ref("Inicio");
watch(() => props.activeSection, val => active.value = val);

// Menú
const menuItems = ["Inicio", "Sobre mí", "Proyectos", "Certificados"];

// Scroll
const scrolled = ref(false);

const handleScroll = () => {
  scrolled.value = window.scrollY > 0;
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
});

const scrollToSection = (id) => {
  const el = document.getElementById(id);
  if (el) {
    const top = el.offsetTop - 64;
    window.scrollTo({ top, behavior: "smooth" });
    active.value = id;
  }
};
</script>

<style scoped>
li:hover span:last-child {
  transform: scaleX(1);
}
</style>
