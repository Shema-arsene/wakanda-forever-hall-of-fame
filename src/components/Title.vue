<script setup>
import { motion } from "motion-v"
</script>

<template>
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
</template>
