<script setup>
import { motion } from "motion-v"
import { defineProps } from "vue"

defineProps({
  isHeroSection: {
    type: Boolean,
    default: false,
  },
})
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
      :class="isHeroSection === true && 'text-4xl justify-center'"
    >
      <span class="text-1xl drop-shadow-[0_0_15px_rgba(34,197,94,0.8)]"
        >The</span
      >
      <span
        class="hall-text text-3xl font-extrabold drop-shadow-[0_0_15px_rgba(34,197,94,0.8)]"
        :class="isHeroSection === true && 'text-9xl'"
        >Hall</span
      >
      <span
        class="text-1xl mb-0 mt-auto drop-shadow-[0_0_15px_rgba(34,197,94,0.8)]"
        >of</span
      >
    </p>
    <h1
      class="zero-limit-text text-3xl sm:text-4xl font-extrabold text-yellow-100 drop-shadow-[0_0_15px_rgba(34,197,94,0.8)]"
      :class="
        isHeroSection === true && 'zero-limit-text-hero tracking-[1.5rem]'
      "
    >
      Zero Limits
    </h1>
  </motion.div>
</template>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Oswald:wght@200..700&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Alegreya:ital,wght@0,400..900;1,400..900&display=swap");

.zero-limit-text {
  font-family: "Oswald", sans-serif;
  font-weight: 900;
}

.zero-limit-text-hero {
  font-size: 5rem;
}

.hall-text {
  font-family: "Alegreya", serif;
  font-weight: 900;
}
</style>
