<script setup>
import { ref , onMounted} from 'vue';

const imageUrls = ref([])
const currentIndex = ref(0)

const fetchData = async () => {
  try {
    const response = await fetch('https://www.reddit.com/r/aww/top/.json?t=all')
    const jsonResponse = await response.json()
    const data = jsonResponse.data.children.map(item => item.data.thumbnail)
   
    imageUrls.value = data
  } catch (error) {
    console.error('Error catching data: ', error)
  }
}

onMounted(() => {
  fetchData()
})

const goToNextSlide = () => {
  currentIndex.value = (currentIndex.value + 1) % imageUrls.value.length;
}

const goToPreviousSlide = () => {
  currentIndex.value = (currentIndex.value - 1 + imageUrls.value.length) % imageUrls.value.length;
}
</script>

<template>
  <div>
    <h1 class="mb-8">Image Carousel</h1>
    <div class="relative w-[35rem] m-auto">
      <div 
        v-for="(item, index) in imageUrls"
        :key="index"
        :class="[
          'm-auto w-[9rem] relative',
          {'invisible': index !== currentIndex},
          {'visible': index === currentIndex}
        ]"
      >
        <img 
          :src="item" 
          class="absolute"
        />
      </div>
      <button
        @click="goToPreviousSlide"
        class="absolute left-[5rem] top-[3rem]"
      >
        Previous</button>
      <button 
        @click="goToNextSlide"
        class="absolute right-[5rem] top-[3rem]"
      >
        Next</button>
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
