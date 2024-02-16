<script setup>
import { onMounted } from 'vue';


const fetchImages = async () => {
  const response = await fetch(`https://www.reddit.com/r/aww/top/.json?t=all`)
  const jsonResponse = await response.json()
  const data = jsonResponse.data.children
  console.log(data)
}

onMounted(() => {
  fetchImages()
})

</script>


<template>
  <div>
    Image Carousel
    <div class="border-2 border-teal-600 w-full h-full"></div>
  </div>
</template>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
