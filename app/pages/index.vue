<template>
  <div class="flex flex-1 flex-col items-center justify-center bg-background px-6">
    <div class="relative flex flex-col items-center space-y-8 text-center">
      
      <div class="relative flex items-center justify-center">
        <svg class="h-32 w-32 transform -rotate-90 sm:h-40 sm:w-40">
          <circle
            cx="50%"
            cy="50%"
            r="45%"
            stroke="currentColor"
            stroke-width="8"
            fill="transparent"
            class="text-muted/20"
          />
          <circle
            cx="50%"
            cy="50%"
            r="45%"
            stroke="currentColor"
            stroke-width="8"
            fill="transparent"
            stroke-dasharray="283"
            :stroke-dashoffset="dashOffset"
            stroke-linecap="round"
            class="text-primary transition-all duration-1000 ease-linear"
          />
        </svg>
        <span class="absolute text-4xl font-black sm:text-5xl">
          {{ countdown }}
        </span>
      </div>

      <div class="space-y-2">
        <h1 class="text-2xl font-bold tracking-tight sm:text-3xl">
          正在前往 <span class="text-primary">Tarotter</span>
        </h1>
        <p class="text-muted-foreground">
          即将为您开启全新体验，请稍候...
        </p>
      </div>

      <NuxtLink 
        to="https://tarotter.com" 
        class="text-sm text-muted-foreground underline underline-offset-4 hover:text-primary transition-colors"
      >
        如果没有自动跳转，请点击此处
      </NuxtLink>
    </div>
  </div>
</template>

<script setup lang="ts">
const countdown = ref(10)
const totalTime = 10
const targetUrl = 'https://tarotter.com'

// 计算圆环进度条的偏移量 (283 是周长近似值)
const dashOffset = computed(() => {
  return 283 * (1 - countdown.value / totalTime)
})

onMounted(() => {
  const timer = setInterval(() => {
    if (countdown.value > 1) {
      countdown.value--
    } else {
      clearInterval(timer)
      // 执行跳转
      window.location.href = targetUrl
    }
  }, 1000)
})
</script>

<style scoped>
/* 简单的入场动画 */
.relative {
  animation: fadeIn 0.8s ease-out;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(10px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>
