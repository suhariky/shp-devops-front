<script setup>
import { ref, watchEffect } from 'vue'

const number = ref(null)
const API_URL = import.meta.env.VITE_API_URL
watchEffect(async () => {
  console.log(import.meta.env.VITE_API_URL)
  // this effect will run immediately and then
  // re-run whenever currentBranch.value changes
  const url = `${API_URL}/api/random`
  let a = await fetch(url,{
    mode: 'cors',
  })

  console.log(a)
  number.value = await a.json()

})
</script>



<template>
  <label :for="number">{{ number }}</label>

</template>
