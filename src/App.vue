<script setup>
import { ref, onMounted } from 'vue';

const imageUrls = ref([])


const fetchData = async () => {
  const response = await fetch(`https://www.reddit.com/r/aww/top/.json?t=all`)
  const jsonResponse = await response.json()
  const data = jsonResponse.data.children

  data.map((item) => {
    imageUrls.value.push(item.data.url)
  })

  console.log(imageUrls.value)
}




onMounted(() => {
  fetchData()
})

</script>


<template>
  <div>
    Image Carousel
    <div 
      class="border-2 border-teal-600 w-full h-[550px]"
      style="background-image: url('https://th.bing.com/th/id/R.76312dfb95d1c1bdb1dec80fd71fa45f?rik=u9WkKnH%2bZTi%2fpg&riu=http%3a%2f%2fwww.pixelstalk.net%2fwp-content%2fuploads%2f2016%2f07%2fHD-Peaceful-Backgrounds.jpg&ehk=VI7X2ZKR%2bgNtV0t5oSJfEcz%2fLs7ugAhZZDw5il%2fOg3I%3d&risl=&pid=ImgRaw&r=0')"
    >
    </div>
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
