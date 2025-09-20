<script setup>
import { ref, onMounted } from "vue"
import { motion } from "motion-v"
import PartnersLogo from "./components/PartnersLogo.vue"
import Hero from "./components/Hero.vue"

const progress = ref(0)

onMounted(() => {
  const interval = setInterval(() => {
    if (progress.value < 100) {
      progress.value += 1
    } else {
      clearInterval(interval)
    }
  }, 100)
})
</script>

<template>
  <!-- Preloader overlay -->
  <motion.main
    class="absolute inset-0 flex items-center justify-center bg-black text-white p-10 z-50"
    :initial="{ opacity: 1, y: '0%' }"
    :animate="progress === 100 ? { y: '-100%' } : {}"
    :transition="{ duration: 1, ease: 'easeOut' }"
  >
    <!-- Background image -->
    <div
      class="absolute inset-0 bg-[url('https://www.transparenttextures.com/patterns/dark-mosaic.png')]"
    ></div>

    <div class="relative z-10 flex flex-col items-center space-y-8 text-center">
      <!-- Logos -->
      <PartnersLogo />

      <!-- Title -->
      <motion.div
        class="uppercase"
        :initial="{ opacity: 0, y: 40 }"
        :animate="{ opacity: 1, y: 0 }"
        :transition="{ duration: 0.8, delay: 0.3, ease: 'easeOut' }"
      >
        <p
          class="font-panthera tracking-[0.3em] flex items-start justify-between text-yellow-100 drop-shadow-[0_0_15px_rgba(34,197,94,0.8)]"
        >
          <span class="text-1xl drop-shadow-[0_0_15px_rgba(34,197,94,0.8)]"
            >The</span
          >
          <span
            class="text-3xl font-extrabold drop-shadow-[0_0_15px_rgba(34,197,94,0.8)]"
            >Hall</span
          >
          <span
            class="text-1xl mb-0 mt-auto drop-shadow-[0_0_15px_rgba(34,197,94,0.8)]"
            >of</span
          >
        </p>
        <h1
          class="text-3xl sm:text-4xl font-extrabold text-yellow-100 drop-shadow-[0_0_15px_rgba(34,197,94,0.8)]"
        >
          Zero Limits
        </h1>
      </motion.div>

      <!-- Progress Bar -->
      <motion.div
        class="relative w-72 bg-gray-800 rounded-full h-1 shadow-inner mt-5"
        :initial="{ opacity: 0.5 }"
        :animate="{ opacity: 1 }"
        :transition="{ duration: 1 }"
      >
        <!-- Progress -->
        <motion.div
          class="h-1 bg-green-300 drop-shadow-[0_0_15px_rgba(34,197,94,0.8)]"
          :initial="{ opacity: 0.5, width: '0%' }"
          :animate="{ width: progress + '%' }"
          :transition="{ duration: 0.25, ease: 'easeOut' }"
        ></motion.div>

        <!-- Percentage -->
        <motion.p
          class="absolute top-3 text-yellow-100 font-medium text-lg drop-shadow-[0_0_15px_rgba(34,197,94,0.8)]"
          :animate="{ left: progress - 2 + '%' }"
          :transition="{ duration: 0.25, ease: 'easeOut' }"
        >
          {{ progress }}%
        </motion.p>
      </motion.div>
    </div>
  </motion.main>

  <!-- Hero underneath -->
  <section class="relative z-0">
    <Hero />
  </section>
</template>
