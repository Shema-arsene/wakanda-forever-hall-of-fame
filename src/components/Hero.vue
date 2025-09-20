<!-- <script>
import { ref, onMounted, onUnmounted } from "vue"
import { gsap } from "gsap"
import { ScrollTrigger } from "gsap/ScrollTrigger"

gsap.registerPlugin(ScrollTrigger)

export default {
  name: "WakandaHero",
  setup() {
    // Refs
    const bgRef = ref(null)
    const bgVideo = ref(null)
    const heroImage = ref(null)
    const spriteCircle = ref(null)
    const wakandaLogo = ref(null)
    const titleContainer = ref(null)
    const hallText = ref(null)
    const ofText = ref(null)
    const zeroLimitsText = ref(null)
    const theaterText = ref(null)
    const ctaText = ref(null)
    const enterButton = ref(null)
    const accessibleLink = ref(null)
    const plantLeft = ref(null)
    const plantRight = ref(null)
    const urnCenter = ref(null)

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

      // Logo parallax
      gsap.to(spriteCircle.value, {
        x: (relativeX - 0.5) * 20,
        y: (relativeY - 0.5) * 20,
        rotation: (relativeX - 0.5) * 360,
        duration: 1,
        ease: "power2.out",
      })

      gsap.to(wakandaLogo.value, {
        x: (relativeX - 0.5) * 15,
        y: (relativeY - 0.5) * 15,
        rotationY: (relativeX - 0.5) * 5,
        duration: 1.2,
        ease: "power2.out",
      })

      // Title parallax
      gsap.to(titleContainer.value, {
        x: (relativeX - 0.5) * 10,
        y: (relativeY - 0.5) * 10,
        rotationY: (relativeX - 0.5) * 3,
        duration: 1.3,
        ease: "power2.out",
      })

      // Individual text elements
      gsap.to(hallText.value, {
        x: (relativeX - 0.5) * 8,
        y: (relativeY - 0.5) * 8,
        rotationY: (relativeX - 0.5) * 2,
        duration: 1.1,
        ease: "power2.out",
      })

      gsap.to(zeroLimitsText.value, {
        x: (relativeX - 0.5) * 12,
        y: (relativeY - 0.5) * 12,
        rotationY: (relativeX - 0.5) * 4,
        duration: 1.4,
        ease: "power2.out",
      })

      // CTA parallax
      gsap.to(ctaText.value, {
        x: (relativeX - 0.5) * 6,
        y: (relativeY - 0.5) * 6,
        rotationY: (relativeX - 0.5) * 1,
        duration: 0.8,
        ease: "power2.out",
      })

      gsap.to(enterButton.value, {
        x: (relativeX - 0.5) * 8,
        y: (relativeY - 0.5) * 8,
        scale: 1 + Math.abs(relativeX - 0.5) * 0.1,
        duration: 0.6,
        ease: "power2.out",
      })

      // Decorative elements
      gsap.to(plantLeft.value, {
        x: (relativeX - 0.5) * 30,
        y: (relativeY - 0.5) * 30,
        rotation: (relativeX - 0.5) * 180,
        duration: 2,
        ease: "power2.out",
      })

      gsap.to(plantRight.value, {
        x: -(relativeX - 0.5) * 25,
        y: (relativeY - 0.5) * 25,
        rotation: -(relativeX - 0.5) * 180,
        duration: 1.8,
        ease: "power2.out",
      })

      gsap.to(urnCenter.value, {
        y: (relativeY - 0.5) * 15,
        rotationY: (relativeX - 0.5) * 8,
        duration: 1.6,
        ease: "power2.out",
      })
    }

    // Mouse leave handler
    const handleMouseLeave = () => {
      gsap.to(
        [
          bgRef.value,
          spriteCircle.value,
          wakandaLogo.value,
          titleContainer.value,
          hallText.value,
          zeroLimitsText.value,
          ctaText.value,
          enterButton.value,
          plantLeft.value,
          plantRight.value,
          urnCenter.value,
        ],
        {
          x: 0,
          y: 0,
          rotation: 0,
          rotationY: 0,
          rotationX: 0,
          scale: 1,
          duration: 1.5,
          ease: "power2.out",
        }
      )
    }

    // Entrance animation
    const initEntranceAnimation = () => {
      tl = gsap.timeline()

      // Stagger logo elements
      tl.from([spriteCircle.value, wakandaLogo.value], {
        opacity: 0,
        y: 50,
        duration: 1,
        ease: "power3.out",
        stagger: 0.2,
      })

      // Title entrance
      tl.from(
        hallText.value,
        {
          opacity: 0,
          y: 60,
          scale: 0.8,
          duration: 1.2,
          ease: "back.out(1.7)",
        },
        "-=0.5"
      )

      tl.from(
        ofText.value,
        {
          opacity: 0,
          y: 40,
          duration: 0.8,
          ease: "power2.out",
        },
        "-=0.8"
      )

      tl.from(
        zeroLimitsText.value,
        {
          opacity: 0,
          y: 80,
          scale: 0.9,
          duration: 1.5,
          ease: "back.out(1.7)",
        },
        "-=0.6"
      )

      // Theater text
      tl.from(
        theaterText.value,
        {
          opacity: 0,
          x: -30,
          duration: 0.6,
          ease: "power2.out",
        },
        "-=0.4"
      )

      // CTA entrance
      tl.from(
        ctaText.value,
        {
          opacity: 0,
          y: 30,
          duration: 0.8,
          ease: "power2.out",
        },
        "-=0.3"
      )

      tl.from(
        enterButton.value,
        {
          opacity: 0,
          scale: 0.5,
          y: 20,
          duration: 0.6,
          ease: "back.out(1.7)",
        },
        "-=0.2"
      )

      // Decorative elements
      tl.from(
        [plantLeft.value, plantRight.value, urnCenter.value],
        {
          opacity: 0,
          y: 100,
          duration: 1.2,
          ease: "power2.out",
          stagger: 0.1,
        },
        "-=0.5"
      )
    }

    // Button hover effects
    const initButtonEffects = () => {
      gsap.to(enterButton.value, {
        scale: 1.05,
        duration: 0.3,
        ease: "power2.out",
        paused: true,
        onComplete: () => {
          gsap.to(enterButton.value, {
            scale: 1,
            duration: 0.2,
            ease: "power2.out",
          })
        },
      })

      enterButton.value.addEventListener("mouseenter", () => {
        gsap.to(enterButton.value, {
          scale: 1.05,
          duration: 0.3,
          ease: "power2.out",
        })
        gsap.to(enterButton.value.querySelector(".arrow-icon"), {
          x: 5,
          duration: 0.3,
          ease: "power2.out",
        })
      })

      enterButton.value.addEventListener("mouseleave", () => {
        gsap.to(enterButton.value, {
          scale: 1,
          duration: 0.2,
          ease: "power2.out",
        })
        gsap.to(enterButton.value.querySelector(".arrow-icon"), {
          x: 0,
          duration: 0.2,
          ease: "power2.out",
        })
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
      // Initialize video
      if (bgVideo.value) {
        bgVideo.value.play().catch((e) => console.log("Video play failed:", e))
      }

      // Get container bounds
      const updateContainerRect = () => {
        if (bgRef.value) {
          containerRect = bgRef.value.getBoundingClientRect()
        }
      }
      updateContainerRect()
      window.addEventListener("resize", updateContainerRect)

      // Add event listeners
      window.addEventListener("mousemove", handleMouseMove)
      window.addEventListener("mouseleave", handleMouseLeave)

      // Initialize animations
      setTimeout(() => {
        initEntranceAnimation()
        initButtonEffects()
        initScrollAnimations()
      }, 100)

      // Initial glow effects
      gsap.to(".sprite-circle", {
        boxShadow: "0 0 30px rgba(0, 255, 65, 0.8)",
        duration: 2,
        repeat: -1,
        yoyo: true,
        ease: "power2.inOut",
      })

      gsap.to(".zero-limits-text", {
        textShadow: "0 0 40px rgba(0, 255, 65, 1)",
        duration: 3,
        repeat: -1,
        yoyo: true,
        ease: "power2.inOut",
      })
    })

    onUnmounted(() => {
      window.removeEventListener("mousemove", handleMouseMove)
      window.removeEventListener("mouseleave", handleMouseLeave)
      window.removeEventListener("resize", updateContainerRect)

      if (tl) {
        tl.kill()
      }
      ScrollTrigger.getAll().forEach((trigger) => trigger.kill())
    })

    return {
      bgRef,
      bgVideo,
      heroImage,
      spriteCircle,
      wakandaLogo,
      titleContainer,
      hallText,
      ofText,
      zeroLimitsText,
      theaterText,
      ctaText,
      enterButton,
      accessibleLink,
      plantLeft,
      plantRight,
      urnCenter,
    }
  },
}
</script> -->

<script setup>
import { ref, onMounted, onUnmounted } from "vue"
import { gsap } from "gsap"
import { ScrollTrigger } from "gsap/ScrollTrigger"

import HeroImg from "../assets/images/hero-background.png"

gsap.registerPlugin(ScrollTrigger)

// Refs
const bgRef = ref(null)
const bgVideo = ref(null)
const heroImage = ref(null)
const spriteCircle = ref(null)
const wakandaLogo = ref(null)
const titleContainer = ref(null)
const hallText = ref(null)
const ofText = ref(null)
const zeroLimitsText = ref(null)
const theaterText = ref(null)
const ctaText = ref(null)
const enterButton = ref(null)
const accessibleLink = ref(null)
const plantLeft = ref(null)
const plantRight = ref(null)
const urnCenter = ref(null)

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

  // Logo parallax
  gsap.to(spriteCircle.value, {
    x: (relativeX - 0.5) * 20,
    y: (relativeY - 0.5) * 20,
    rotation: (relativeX - 0.5) * 360,
    duration: 1,
    ease: "power2.out",
  })

  gsap.to(wakandaLogo.value, {
    x: (relativeX - 0.5) * 15,
    y: (relativeY - 0.5) * 15,
    rotationY: (relativeX - 0.5) * 5,
    duration: 1.2,
    ease: "power2.out",
  })

  // Title parallax
  gsap.to(titleContainer.value, {
    x: (relativeX - 0.5) * 10,
    y: (relativeY - 0.5) * 10,
    rotationY: (relativeX - 0.5) * 3,
    duration: 1.3,
    ease: "power2.out",
  })

  // Individual text elements
  gsap.to(hallText.value, {
    x: (relativeX - 0.5) * 8,
    y: (relativeY - 0.5) * 8,
    rotationY: (relativeX - 0.5) * 2,
    duration: 1.1,
    ease: "power2.out",
  })

  gsap.to(zeroLimitsText.value, {
    x: (relativeX - 0.5) * 12,
    y: (relativeY - 0.5) * 12,
    rotationY: (relativeX - 0.5) * 4,
    duration: 1.4,
    ease: "power2.out",
  })

  // CTA parallax
  gsap.to(ctaText.value, {
    x: (relativeX - 0.5) * 6,
    y: (relativeY - 0.5) * 6,
    rotationY: (relativeX - 0.5) * 1,
    duration: 0.8,
    ease: "power2.out",
  })

  gsap.to(enterButton.value, {
    x: (relativeX - 0.5) * 8,
    y: (relativeY - 0.5) * 8,
    scale: 1 + Math.abs(relativeX - 0.5) * 0.1,
    duration: 0.6,
    ease: "power2.out",
  })

  // Decorative elements
  gsap.to(plantLeft.value, {
    x: (relativeX - 0.5) * 30,
    y: (relativeY - 0.5) * 30,
    rotation: (relativeX - 0.5) * 180,
    duration: 2,
    ease: "power2.out",
  })

  gsap.to(plantRight.value, {
    x: -(relativeX - 0.5) * 25,
    y: (relativeY - 0.5) * 25,
    rotation: -(relativeX - 0.5) * 180,
    duration: 1.8,
    ease: "power2.out",
  })

  gsap.to(urnCenter.value, {
    y: (relativeY - 0.5) * 15,
    rotationY: (relativeX - 0.5) * 8,
    duration: 1.6,
    ease: "power2.out",
  })
}

// Mouse leave handler
const handleMouseLeave = () => {
  gsap.to(
    [
      bgRef.value,
      spriteCircle.value,
      wakandaLogo.value,
      titleContainer.value,
      hallText.value,
      zeroLimitsText.value,
      ctaText.value,
      enterButton.value,
      plantLeft.value,
      plantRight.value,
      urnCenter.value,
    ],
    {
      x: 0,
      y: 0,
      rotation: 0,
      rotationY: 0,
      rotationX: 0,
      scale: 1,
      duration: 1.5,
      ease: "power2.out",
    }
  )
}

// Entrance animation
const initEntranceAnimation = () => {
  tl = gsap.timeline()

  // Stagger logo elements
  tl.from([spriteCircle.value, wakandaLogo.value], {
    opacity: 0,
    y: 50,
    duration: 1,
    ease: "power3.out",
    stagger: 0.2,
  })

  // Title entrance
  tl.from(
    hallText.value,
    {
      opacity: 0,
      y: 60,
      scale: 0.8,
      duration: 1.2,
      ease: "back.out(1.7)",
    },
    "-=0.5"
  )

  tl.from(
    ofText.value,
    {
      opacity: 0,
      y: 40,
      duration: 0.8,
      ease: "power2.out",
    },
    "-=0.8"
  )

  tl.from(
    zeroLimitsText.value,
    {
      opacity: 0,
      y: 80,
      scale: 0.9,
      duration: 1.5,
      ease: "back.out(1.7)",
    },
    "-=0.6"
  )

  // Theater text
  tl.from(
    theaterText.value,
    {
      opacity: 0,
      x: -30,
      duration: 0.6,
      ease: "power2.out",
    },
    "-=0.4"
  )

  // CTA entrance
  tl.from(
    ctaText.value,
    {
      opacity: 0,
      y: 30,
      duration: 0.8,
      ease: "power2.out",
    },
    "-=0.3"
  )

  tl.from(
    enterButton.value,
    {
      opacity: 0,
      scale: 0.5,
      y: 20,
      duration: 0.6,
      ease: "back.out(1.7)",
    },
    "-=0.2"
  )

  // Decorative elements
  tl.from(
    [plantLeft.value, plantRight.value, urnCenter.value],
    {
      opacity: 0,
      y: 100,
      duration: 1.2,
      ease: "power2.out",
      stagger: 0.1,
    },
    "-=0.5"
  )
}

// Button hover effects
const initButtonEffects = () => {
  enterButton.value.addEventListener("mouseenter", () => {
    gsap.to(enterButton.value, {
      scale: 1.05,
      duration: 0.3,
      ease: "power2.out",
    })
    gsap.to(enterButton.value.querySelector(".arrow-icon"), {
      x: 5,
      duration: 0.3,
      ease: "power2.out",
    })
  })

  enterButton.value.addEventListener("mouseleave", () => {
    gsap.to(enterButton.value, {
      scale: 1,
      duration: 0.2,
      ease: "power2.out",
    })
    gsap.to(enterButton.value.querySelector(".arrow-icon"), {
      x: 0,
      duration: 0.2,
      ease: "power2.out",
    })
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
  // Initialize video
  if (bgVideo.value) {
    bgVideo.value.play().catch((e) => console.log("Video play failed:", e))
  }

  // Get container bounds
  const updateContainerRect = () => {
    if (bgRef.value) {
      containerRect = bgRef.value.getBoundingClientRect()
    }
  }
  updateContainerRect()
  window.addEventListener("resize", updateContainerRect)

  // Add event listeners
  window.addEventListener("mousemove", handleMouseMove)
  window.addEventListener("mouseleave", handleMouseLeave)

  // Initialize animations
  setTimeout(() => {
    initEntranceAnimation()
    initButtonEffects()
    initScrollAnimations()
  }, 100)

  // Initial glow effects
  gsap.to(".sprite-circle", {
    boxShadow: "0 0 30px rgba(0, 255, 65, 0.8)",
    duration: 2,
    repeat: -1,
    yoyo: true,
    ease: "power2.inOut",
  })

  gsap.to(".zero-limits-text", {
    textShadow: "0 0 40px rgba(0, 255, 65, 1)",
    duration: 3,
    repeat: -1,
    yoyo: true,
    ease: "power2.inOut",
  })
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
    <!-- Background Image with Parallax -->
    <div class="absolute inset-0" ref="bgRef">
      <img
        :src="HeroImg"
        alt="Wakanda Forever Background"
        class="absolute inset-0 w-full h-full object-cover -z-10"
      />

      <!-- Geometric Overlay Pattern -->
      <div class="geometric-overlay absolute inset-0 opacity-30 z-10"></div>
    </div>

    <!-- Main Content -->
    <div
      class="hero-content relative z-10 flex flex-col justify-between h-screen px-8 py-12 max-w-7xl mx-auto"
    >
      <!-- Logo Section -->
      <div class="logo-container flex items-center gap-8">
        <div class="logo-item sprite-logo flex flex-col items-center">
          <div
            class="sprite-circle w-20 h-20 bg-green-400 rounded-full shadow-[0_0_20px_rgba(0,255,65,0.6)] relative"
            ref="spriteCircle"
          ></div>
          <div
            class="sprite-text mt-3 text-green-400 text-sm font-bold tracking-widest uppercase; text-shadow: 0 0 10px rgba(0, 255, 65, 0.8)"
          >
            SPRITE
          </div>
        </div>

        <div class="logo-item wakanda-logo" ref="wakandaLogo">
          <div
            class="wakanda-logo-inner bg-black/50 backdrop-blur-sm p-4 border-2 border-green-400/50 rounded-lg"
          >
            <div
              class="black-panther-text text-green-400 text-xs font-bold tracking-wide uppercase mb-1"
            >
              BLACK PANTHER
            </div>
            <div
              class="wakanda-forever-text text-white text-lg font-bold tracking-wide mb-1"
            >
              WAKANDA
            </div>
            <div
              class="forever-text text-green-400 text-xs font-bold tracking-wide uppercase"
            >
              FOREVER
            </div>
          </div>
        </div>
      </div>

      <!-- Title Section -->
      <div class="title-container text-center" ref="titleContainer">
        <div class="title-text space-y-2">
          <h1
            class="hall-text text-7xl text-green-400 font-black tracking-[0.2em] uppercase leading-tight; text-shadow: 0 0 20px rgba(0, 255, 65, 0.8)"
            ref="hallText"
          >
            <span class="the-text text-green-400">THE</span>
            <span class="hall-text-inner block">HALL</span>
          </h1>
          <h2
            class="of-text text-white text-4xl font-black tracking-[0.3em] uppercase; text-shadow: 0 0 15px rgba(0, 255, 65, 0.5)"
            ref="ofText"
          >
            OF
          </h2>
          <h1
            class="zero-limits-text text-8xl font-black tracking-[0.25em] uppercase relative"
            ref="zeroLimitsText"
          >
            <span class="zero-text block">ZERO</span>
            <span class="limits-text text-6xl -mt-4 block">LIMITS</span>
          </h1>
        </div>
        <p
          class="theater-text text-gray-400 text-lg tracking-[0.15em] uppercase mt-8"
          ref="theaterText"
        >
          ONLY IN THEATERS
        </p>
      </div>

      <!-- CTA Section -->
      <div class="cta-section flex flex-col items-center gap-6 mt-16">
        <div
          class="cta-text text-white text-xl text-center leading-relaxed tracking-wide"
          ref="ctaText"
        >
          EXPLORE YOUR NEW PATHS.
          <br />
          <span class="cta-highlight block text-green-400 font-bold"
            >FIND YOUR GIFT.</span
          >
        </div>

        <button
          class="enter-button relative inline-flex items-center gap-2 px-8 py-4 bg-green-400/20 border-2 border-green-400/50 backdrop-blur-sm rounded-full text-white font-bold text-lg uppercase tracking-wide hover:bg-green-400/30 hover:border-green-400"
          ref="enterButton"
        >
          <span>ENTER</span>
          <svg
            class="arrow-icon w-5 h-5 transition-transform duration-300"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
          >
            <polyline points="9,18 15,12 9,6"></polyline>
          </svg>
        </button>

        <a
          href="#"
          class="accessible-link text-green-400 text-sm font-bold tracking-wide hover:text-green-300 transition-colors"
          ref="accessibleLink"
        >
          Accessible version →
        </a>
      </div>
    </div>

    <!-- Foreground Decorative Elements -->
    <div class="decorative-elements absolute inset-0 pointer-events-none">
      <div
        class="plant-left absolute w-32 h-32 bg-green-400/20 rounded-full blur-xl top-[20%] -right-[10%]"
        ref="plantLeft"
      ></div>
      <div
        class="plant-right absolute w-32 h-32 bg-green-400/20 rounded-full blur-xl top-[60%] -right-[10%]"
        ref="plantRight"
      ></div>
      <div
        class="urn-center absolute w-24 h-24 bg-black/80 rounded-full bottom-20 left-1/2 -translate-x-1/2"
        ref="urnCenter"
      ></div>
    </div>
  </section>
</template>

<!-- <style scoped>
.hero-section {
  @apply relative w-full min-h-screen overflow-hidden bg-black;
  font-family: "Arial Black", Arial, sans-serif;
  font-weight: 900;
}

/* Background */
.hero-bg {
  @apply absolute inset-0;
  perspective: 1000px;
  transform-style: preserve-3d;
}

.hero-video,
.hero-image {
  @apply absolute inset-0 w-full h-full object-cover;
  filter: brightness(0.6) contrast(1.2);
}

.hero-video {
  z-index: -2;
}

.hero-image {
  z-index: -1;
}

/* Geometric Overlay */
.geometric-overlay {
  @apply absolute inset-0;
  background-image: repeating-linear-gradient(
      45deg,
      transparent,
      transparent 10px,
      rgba(0, 255, 65, 0.03) 10px,
      rgba(0, 255, 65, 0.03) 20px
    ),
    repeating-linear-gradient(
      -45deg,
      transparent,
      transparent 10px,
      rgba(0, 255, 65, 0.03) 10px,
      rgba(0, 255, 65, 0.03) 20px
    );
  opacity: 0.3;
  z-index: 1;
}

/* Content Container */
.hero-content {
  @apply relative z-10 flex flex-col justify-between h-screen px-8 py-12 max-w-7xl mx-auto;
}

/* Logo Section */
.logo-container {
  @apply flex items-center gap-8;
}

.sprite-logo {
  @apply flex flex-col items-center;
}

.sprite-circle {
  @apply w-20 h-20 bg-green-400 rounded-full shadow-[0_0_20px_rgba(0,255,65,0.6)] relative;
}

---- Add the ::before css code and the content: ""

.sprite-circle::before {
  content: "";
  @apply absolute inset-0 rounded-full bg-green-400/30 opacity-0 animate-ping;
}

.sprite-text {
  @apply mt-3 text-green-400 text-sm font-bold tracking-widest uppercase;
  text-shadow: 0 0 10px rgba(0, 255, 65, 0.8);
}

.wakanda-logo-inner {
  @apply bg-black/50 backdrop-blur-sm p-4 border-2 border-green-400/50 rounded-lg;
}

.black-panther-text {
  @apply text-green-400 text-xs font-bold tracking-wide uppercase mb-1;
}

.wakanda-forever-text {
  @apply text-white text-lg font-bold tracking-wide mb-1;
}

.forever-text {
  @apply text-green-400 text-xs font-bold tracking-wide uppercase;
}

/* Title Section */
.title-container {
  @apply text-center;
}

.title-text {
  @apply space-y-2;
}

.hall-text {
  @apply text-7xl text-green-400 font-black tracking-[0.2em] uppercase leading-tight;
  text-shadow: 0 0 20px rgba(0, 255, 65, 0.8);
}

.the-text {
  @apply text-green-400;
}

.hall-text-inner {
  @apply block;
}

.of-text {
  @apply text-white text-4xl font-black tracking-[0.3em] uppercase;
  text-shadow: 0 0 15px rgba(0, 255, 65, 0.5);
}

----- Apply the -webkit-background-clip styles ----- (An option is to keep the <style> and link the class name)

.zero-limits-text {
  @apply text-8xl font-black tracking-[0.25em] uppercase relative;
  background: linear-gradient(135deg, #00ff41 0%, #00cc33 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  text-shadow: 0 0 30px rgba(0, 255, 65, 0.9);
}

.zero-text {
  @apply block;
}

----- Apply the -webkit-background-clip styles ----- (An option is to keep the <style> and link the class name)

.limits-text {
  @apply text-6xl -mt-4 block;
  background: linear-gradient(135deg, #00ff41 0%, #00cc33 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.theater-text {
  @apply text-gray-400 text-lg tracking-[0.15em] uppercase mt-8;
  text-shadow: 0 0 10px rgba(0, 255, 65, 0.3);
}

/* CTA Section */
.cta-section {
  @apply flex flex-col items-center gap-6 mt-16;
}

.cta-text {
  @apply text-white text-xl text-center leading-relaxed tracking-wide;
  text-shadow: 0 0 10px rgba(0, 255, 65, 0.5);
}

.cta-highlight {
  @apply block text-green-400 font-bold;
}

.enter-button {
  @apply relative inline-flex items-center gap-2 px-8 py-4 bg-green-400/20 border-2 border-green-400/50 backdrop-blur-sm rounded-full text-white font-bold text-lg uppercase tracking-wide;
  transition: all 0.3s ease;
  cursor: pointer;
}

.enter-button:hover {
  @apply bg-green-400/30 border-green-400;
}

.arrow-icon {
  @apply w-5 h-5 transition-transform duration-300;
}

.accessible-link {
  @apply text-green-400 text-sm font-bold tracking-wide hover:text-green-300 transition-colors;
}

/* Decorative Elements */
.decorative-elements {
  @apply absolute inset-0 pointer-events-none;
}

.plant-left,
.plant-right {
  @apply absolute w-32 h-32 bg-green-400/20 rounded-full blur-xl;
}

.plant-left {
  top: 20%;
  left: -10%;
}

.plant-right {
  top: 60%;
  right: -10%;
}

.urn-center {
  @apply absolute w-24 h-24 bg-black/80 rounded-full bottom-20 left-1/2 -translate-x-1/2;
  border: 2px solid rgba(0, 255, 65, 0.3);
}

/* Responsive */
@media (max-width: 768px) {
  .logo-container {
    @apply flex-col gap-4;
  }

  .hall-text {
    @apply text-5xl tracking-[0.15em];
  }

  .of-text {
    @apply text-2xl tracking-[0.2em];
  }

  .zero-limits-text {
    @apply text-6xl tracking-[0.2em];
  }

  .limits-text {
    @apply text-4xl;
  }

  .cta-section {
    @apply mt-8 gap-4;
  }

  .cta-text {
    @apply text-base;
  }

  .enter-button {
    @apply px-6 py-3 text-base;
  }
}

/* Custom Animations */
@keyframes glowPulse {
  0%,
  100% {
    box-shadow: 0 0 20px rgba(0, 255, 65, 0.6);
  }
  50% {
    box-shadow: 0 0 40px rgba(0, 255, 65, 1);
  }
}

.sprite-circle {
  animation: glowPulse 3s ease-in-out infinite;
}
</style> -->
