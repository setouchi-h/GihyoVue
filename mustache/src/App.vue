<script setup lang="ts">
import { ref } from 'vue'

const name = ref('田中太郎')

const now = new Date()
const nowStr = now.toLocaleTimeString()
let timeStr = nowStr
const timeStrRef = ref(nowStr)

// 新しい時刻に変更する関数
function changeTime(): void {
  const newTime = new Date()
  const newTimeStr = newTime.toLocaleTimeString()
  timeStr = newTimeStr
  timeStrRef.value = newTimeStr
}

setInterval(changeTime, 1000)
</script>

<template>
  <h1>こんにちは！{{ name }}さん！</h1>
  <p>現在時刻：{{ timeStr }}</p>
  <p>現在時刻(ref)：{{ timeStrRef }}</p>
</template>
