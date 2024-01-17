<script setup>
import { ref, watchEffect } from 'vue'

const number = ref(null)
const err = ref(null)
const API_URL = import.meta.env.VITE_API_URL
watchEffect(async () => {
  console.log(import.meta.env.VITE_API_URL)
  // this effect will run immediately and then
  // re-run whenever currentBranch.value changes
  const url = `${API_URL}/api/random`

  try {
    let a = await fetch(url,{
      mode: 'cors',
    })
    console.log(a)
    let val = await a.json()
    number.value = val.number
  } catch (error) {
    // TypeError: Failed to fetch
    console.log('There was an error', error);
    err.value = error
  }

})
</script>



<template>
  <label :for="number">{{ number }}</label>
  <label class="red" :for="err">{{ err }}</label>

</template>
