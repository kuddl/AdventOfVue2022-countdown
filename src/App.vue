<script setup>
import CountdownHeader from '@/components/CountdownHeader.vue'
import CountdownSegment from './components/CountdownSegment.vue'
import { useNow } from '@vueuse/core'
import { computed } from 'vue'

const now = useNow()
const christmas = new Date('12/25/2022 00:00:00')

const result = computed(() => {
  // https://stackoverflow.com/a/32514236
  var d = Math.abs(christmas.getTime() - now.value.getTime()) / 1000 // delta
  var r = {} // result
  var s = {
    // structure
    // year: 31536000,
    // month: 2592000,
    // week: 604800, // uncomment row to ignore
    day: 86400, // feel free to add your own row
    hour: 3600,
    minute: 60,
    second: 1,
  }

  Object.keys(s).forEach(function (key) {
    r[key] = Math.floor(d / s[key])
    d -= r[key] * s[key]
  })
  return r
})
</script>
<template>
  <div class="w-full h-full flex justify-center items-center p-10">
    <div>
      <div class="shadow-md relative bg-white p-5 rounded-lg border-gray-100 border-[1px]">
        <CountdownHeader />
        <main class="flex justify-center">
          <CountdownSegment label="days" :number="result.day" />
          <CountdownSegment label="hours" :number="result.hour" />
          <CountdownSegment label="minutes" :number="result.minute" />
          <CountdownSegment label="seconds" :number="result.second" />
        </main>
      </div>
      <h4 class="mt-10 text-gray-400 text-center text-sm">
        This challenge brought to you by <a href="https://vueschool.io/" class="underline">Vue School</a>
      </h4>
    </div>
  </div>
</template>

<style>
div {
  display: block;
}

body {
  @apply bg-gray-100;
}
</style>
