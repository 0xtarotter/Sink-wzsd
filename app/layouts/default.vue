<template>
  <div class="min-h-screen flex flex-col items-center justify-center bg-black text-white">
    <div class="text-center space-y-6 px-6">
      <h1 class="text-5xl font-bold tracking-tight">
        Sink
      </h1>
      <p class="text-lg text-gray-400 max-w-xl mx-auto">
        A minimal, fast, and elegant short link service.
        Built for speed. Designed for clarity.
      </p>

      <div class="flex gap-4 justify-center">
        <button
          class="px-6 py-3 bg-white text-black rounded-2xl hover:scale-105 transition"
          @click="goDashboard"
        >
          Dashboard
        </button>

        <button
          class="px-6 py-3 border border-gray-600 rounded-2xl hover:bg-gray-800 transition"
          @click="goMain"
        >
          Main Site
        </button>
      </div>
    </div>

    <div class="absolute bottom-6 text-sm text-gray-500">
      © {{ new Date().getFullYear() }} Sink
    </div>
  </div>
</template>

<script setup>
const goDashboard = () => {
  window.location.href = '/dashboard'
}

const goMain = () => {
  window.location.href = 'https://tarotter.com'
}
</script>

<script setup>
import { useRoute } from 'vue-router'

const route = useRoute()

const goDashboard = () => {
  window.location.href = '/dashboard'
}

const goMain = () => {
  window.location.href = 'https://tarotter.com'
}

// ✅ 只在首页才执行（如果你有自动逻辑的话）
if (route.path !== '/') {
  // 非首页，不做任何事（避免影响 dashboard）
}
</script>
