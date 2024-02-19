<script setup>
import { ref , onMounted} from 'vue';

const imageData = ref([])

const fetchData = async () => {
  try {
    const response = await fetch('https://www.reddit.com/r/aww/top/.json?t=all')
    const jsonResponse = await response.json()
    const data = jsonResponse.data.children.map(item => item.data)
   
    imageData.value = data
  } catch (error) {
    console.error('Error catching data: ', error)
  }
}

onMounted(() => {
  fetchData()
})
</script>


<template>
  <div>
    Image Carousel
    <div>
      <div 
        v-for="(item, index) in imageData"
        :key="index"
      >
        <img :src="item.url" />
      </div>
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
