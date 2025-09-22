<script setup>
import { ref, onMounted, onUnmounted } from "vue"
import { gsap } from "gsap"
import { ScrollTrigger } from "gsap/ScrollTrigger"

import HeroVid from "../assets/Videos/wakanda.mp4"
import PartnersLogo from "./PartnersLogo.vue"
import Title from "./Title.vue"

gsap.registerPlugin(ScrollTrigger)

// Refs
const bgRef = ref(null)
const bgVideo = ref(null)

// Mouse tracking
let mouseX = ref(0)
let mouseY = ref(0)
let containerRect = null

// GSAP Timeline
let tl = null

// Mouse move handler
const handleMouseMove = (e) => {
  mouseX.value = e.clientX
  mouseY.value = e.clientY

  if (!containerRect) return

  const relativeX = (e.clientX - containerRect.left) / containerRect.width
  const relativeY = (e.clientY - containerRect.top) / containerRect.height

  // Parallax background
  gsap.to(bgRef.value, {
    x: (relativeX - 0.5) * 50,
    y: (relativeY - 0.5) * 50,
    rotationY: (relativeX - 0.5) * 10,
    rotationX: (relativeY - 0.5) * -10,
    duration: 1.5,
    ease: "power2.out",
  })

  gsap.to(bgVideo.value, {
    x: (relativeX - 0.5) * 40,
    y: (relativeY - 0.5) * 40,
    rotationY: (relativeX - 0.5) * 8,
    rotationX: (relativeY - 0.5) * -8,
    scale: 1.05,
    duration: 1.5,
    ease: "power2.out",
  })
}

// Mouse leave handler
const handleMouseLeave = () => {
  gsap.to([bgRef.value, bgVideo.value], {
    x: 0,
    y: 0,
    rotation: 0,
    rotationY: 0,
    rotationX: 0,
    scale: 1,
    duration: 1.5,
    ease: "power2.out",
  })
}

// Scroll-triggered animations
const initScrollAnimations = () => {
  ScrollTrigger.create({
    trigger: ".hero-section",
    start: "top top",
    end: "bottom top",
    onEnter: () => {
      gsap.to(".geometric-overlay", {
        opacity: 0.7,
        duration: 1,
        ease: "power2.out",
      })
    },
    onLeave: () => {
      gsap.to(".geometric-overlay", {
        opacity: 0.3,
        duration: 0.8,
        ease: "power2.out",
      })
    },
    onEnterBack: () => {
      gsap.to(".geometric-overlay", {
        opacity: 0.7,
        duration: 1,
        ease: "power2.out",
      })
    },
  })
}

onMounted(() => {
  if (bgVideo.value) {
    bgVideo.value.play().catch((e) => console.log("Video play failed:", e))
  }

  const updateContainerRect = () => {
    if (bgRef.value) {
      containerRect = bgRef.value.getBoundingClientRect()
    }
  }
  updateContainerRect()
  window.addEventListener("resize", updateContainerRect)

  window.addEventListener("mousemove", handleMouseMove)
  window.addEventListener("mouseleave", handleMouseLeave)

  setTimeout(() => {
    initScrollAnimations()
  }, 100)
})

onUnmounted(() => {
  window.removeEventListener("mousemove", handleMouseMove)
  window.removeEventListener("mouseleave", handleMouseLeave)
  window.removeEventListener("resize", () => (containerRect = null))

  if (tl) {
    tl.kill()
  }
  ScrollTrigger.getAll().forEach((trigger) => trigger.kill())
})
</script>

<template>
  <section
    class="hero-section relative w-full min-h-screen overflow-hidden bg-black"
  >
    <!-- Background Video with Parallax -->
    <div class="absolute inset-0" ref="bgRef">
      <video
        ref="bgVideo"
        :src="HeroVid"
        loop
        muted
        alt="Wakanda Forever"
        class="absolute inset-0 w-full h-full object-cover -z-10"
      ></video>

      <!-- Geometric Overlay Pattern -->
      <div class="geometric-overlay absolute inset-0 opacity-30 z-10"></div>
    </div>

    <!-- Main Content -->
    <div
      class="hero-content relative z-10 flex flex-col items-center justify-evenly h-screen px-8 py-12 max-w-7xl mx-auto"
    >
      <!-- Version button -->
      <button
        class="lg:absolute top-20 right-20 md:mb-10 w-fit mx-auto flex items-center justify-center px-9 py-5 text-white font-extrabold border-2 border-yellow-100 rounded-tl-md rounded-tr-3xl rounded-bl-3xl rounded-br-md bg-green-900/20 cursor-pointer"
      >
        Accessible Version
        <i class="pi pi-chevron-right text-sm font-extrabold"></i>
        <i class="pi pi-chevron-right text-xl -ml-1 font-extrabold"></i>
      </button>

      <!-- Logo Section -->
      <PartnersLogo />

      <!-- Title Section -->
      <div class="w-fit mx-auto">
        <Title :isHeroSection="true" />
      </div>

      <!-- CTA Section -->
      <div
        class="relative w-fit px-24 bg-green-700/20 [mask-image:linear-gradient(to_right,transparent,black_20%,black_80%,transparent)] [mask-repeat:no-repeat] [mask-size:100%_100%]"
      >
        <!-- Content -->
        <div
          class="relative z-10 text-white flex items-center justify-center h-full"
        >
          <div
            class="cta-text flex flex-col items-center gap-1 uppercase md:tracking-widest whitespace-nowrap"
          >
            <p class="text-xl sm:text-2xl font-bold text-yellow-100">
              Explore your new paths.
            </p>
            <p class="text-xl sm:text-2xl font-bold text-yellow-100">
              Find your gift.
            </p>
          </div>
        </div>
      </div>

      <!-- CTA Button -->
      <button
        class="relative w-fit mx-auto flex items-center justify-center px-9 py-5 text-white font-extrabold tracking-[0.3em] border-2 border-green-400 rounded-tl-md rounded-tr-3xl rounded-bl-3xl rounded-br-md bg-green-500/20 hover:bg-green-500/50 transition duration-300 before:content-[''] before:absolute before:inset-0 before:rounded-md before:border-2 before:border-green-500 before:opacity-70 before:blur-md shadow-[0_0_15px_rgba(34,197,94,0.8),inset_0_0_10px_rgba(34,197,94,0.6)] cursor-pointer"
      >
        ENTER
        <i
          class="pi pi-arrow-right text-green-500 text-lg font-extrabold drop-shadow-[0_0_15px_#ffc55eCC]"
        ></i>
        <i
          class="pi pi-arrow-right text-green-500 text-lg -ml-2 font-extrabold drop-shadow-[0_0_15px_#22c55eCC]"
        ></i>
      </button>

      <!-- Sponsors -->
      <div
        class="fixed flex items-center justify-between border border-white p-0 text-white text-xs md:text-sm w-[90%] max-w-[350px] md:w-auto"
        :class="[
          'left-1/2 -translate-x-1/2 bottom-4',
          'md:left-auto md:translate-x-0 md:right-4 md:bottom-4',
        ]"
      >
        <!-- Left logo -->
        <div
          class="flex flex-col items-center px-4 py-2 m-0 text-center leading-tight border-r border-white"
        >
          <img
            src="../assets/images/sprite-logo-white.png"
            alt="Sprite Logo"
            class="h-8 object-contain"
          />
        </div>

        <!-- Center logo -->
        <div
          class="flex flex-col items-center px-4 py-2 m-0 text-center leading-tight border-r border-white"
        >
          <img
            src="../assets/images/wakanda-forever-logo.png"
            alt="Wakanda Forever"
            class="h-8 object-contain"
          />
        </div>

        <!-- Right text -->
        <span class="whitespace-nowrap text-xs font-bold text-gray-300 px-1">
          Sprite Zero Sugar® | &copy; MARVEL
        </span>
      </div>
    </div>
  </section>
</template>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Alegreya:ital,wght@0,400..900;1,400..900&family=Roboto:ital,wght@0,100..900;1,100..900&display=swap");

.cta-text {
  font-family: "Alegreya", serif;
}
</style>
