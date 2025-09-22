<script setup>
import { motion } from "motion-v"

import SpriteLogo from "../assets/images/sprite-logo-white.png"
import WakandaLogo from "../assets/images/wakanda-forever-logo.png"
</script>

<template>
  <div class="flex items-center justify-center gap-6">
    <motion.img
      :src="SpriteLogo"
      alt="Sprite Logo"
      class="h-14 sm:h-24 w-24 sm:w-32"
      :initial="{ opacity: 0, x: -40 }"
      :animate="{ opacity: 1, x: 0 }"
      :transition="{ duration: 0.8, ease: 'easeOut' }"
    />
    <span class="text-gray-400">
      <i class="pi pi-times text-xl sm:text-xl mx-auto"></i>
    </span>
    <motion.img
      :src="WakandaLogo"
      alt="Wakanda Forever Logo"
      class="h-14 sm:h-24 w-24 sm:w-32"
      :initial="{ opacity: 0, x: 40 }"
      :animate="{ opacity: 1, x: 0 }"
      :transition="{ duration: 0.8, ease: 'easeOut' }"
    />
  </div>
</template>
