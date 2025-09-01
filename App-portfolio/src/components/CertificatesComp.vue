<template>
  <section class="flex flex-col justify-start items-center px-4 sm:px-8 md:px-32 mt-20 md:-mt-11 space-y-12">
    
    <!-- Título -->
    <div ref="titleRef"
      :class="{
        'animate-zoom-in opacity-100': titleVisible,
        'opacity-0': !titleVisible,
      }"
      class="text-center transition-opacity duration-700"
    >

      <h2 class="text-3xl sm:text-4xl md:text-6xl font-medium text-purple-500 mb-4">
        Certificados
      </h2>

      <p class="text-gray-300 text-base sm:text-lg md:text-xl animate-zoom-in-delay">
        Mis logros y reconocimientos
      </p>
    </div>

    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6 sm:gap-8 md:gap-12">
      <div
        v-for="(cert, index) in certificates"
        :key="index"
        class="w-[290px] md:w-[364px] aspect-video bg-black rounded-xl shadow-lg shadow-blue-500/50 cursor-pointer overflow-hidden transform transition duration-300 hover:-translate-y-2 mx-auto animate-slide-in-left"
        @click="openModal(cert.image)"
      >
        <img
          :src="cert.image"
          alt="Certificado"
          class="w-full h-full object-cover object-[50%_30%]"
        />
      </div>
    </div>

    <div v-if="selectedImage" class="fixed inset-0 bg-black/80 flex items-center justify-center z-50">
      <div class="relative">
        <button @click="closeModal"
          class="absolute top-2 right-2 text-white bg-black/60 rounded-full p-2 hover:bg-black/80 transition"
        >
          ✕
        </button>
        <img
          :src="selectedImage"
          alt="Certificado ampliado"
          class="max-w-[90vw] max-h-[80vh] rounded-lg shadow-lg"
        />
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from "vue";
import FormacionJS from "../assets/certificates/Formación  JavaScript .jpg";
import CSS from "../assets/certificates/Curso CSS.jpg";
import Git from "../assets/certificates/Curso Git y GitHub.jpg";
import DOM from "../assets/certificates/Curso JavaScript DOM.jpg";
import JS from "../assets/certificates/Curso Javascript.jpg";
import Formacion from "../assets/certificates/Formación.jpg";

function useIntersectionObserver(
  targetRef,
  callback,
  options = { threshold: 0.2 }
) {
  onMounted(() => {
    if (!targetRef.value) return;
    const observer = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) callback(entry);
      });
    }, options);
    observer.observe(targetRef.value);
  });
}

const titleRef = ref(null);
const titleVisible = ref(false);
useIntersectionObserver(titleRef, () => (titleVisible.value = true));

const certificates = ref([
  { image: FormacionJS },
  { image: CSS },
  { image: Git },
  { image: DOM },
  { image: JS },
  { image: Formacion },
]);

const selectedImage = ref(null);
const openModal = (image) => (selectedImage.value = image);
const closeModal = () => (selectedImage.value = null);
</script>