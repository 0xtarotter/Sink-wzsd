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
          正在 - <span class="text-primary">重定向</span>
        </h1>
        <p class="text-muted-foreground">
         请稍候...
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
// 1. 设置页面标题 (回答你上一个关于标题的问题)
useHead({
  title: 'IURL.CC'
})

// 2. 定义倒计时变量 (修改这里可以调整秒数)
const countdown = ref(18) // 初始显示的数字
const totalTime = 18      // 总时长，用于圆环进度计算
const targetUrl = 'https://tarotter.com'

// 3. 计算圆环进度条的偏移量
const dashOffset = computed(() => {
  return 283 * (1 - countdown.value / totalTime)
})

// 4. 落地执行倒计时逻辑
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
/* 入场动画：让内容稍微往上浮动出现 */
.relative {
  animation: fadeIn 0.8s ease-out;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(10px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>
