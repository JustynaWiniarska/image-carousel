# Image Carousel in Vue3

#### Requirements
- Images are fetched from an endpoint.
- The slideshow wraps around - after the last image the first one is shown.
- The carousel cycles through images displaying a new image every 3 seconds.

```<script setup>
import { ref , onMounted, onBeforeUnmount} from 'vue';

const imageUrls = ref([]);
const currentIndex = ref(0);
let intervalId = null;

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
  fetchData();
  startInterval();
})

const startInterval = () => {
  intervalId = setInterval(() => {
    goToNextSlide()
  }, 3000)
}

const goToNextSlide = () => {
  currentIndex.value = (currentIndex.value + 1) % imageUrls.value.length;
}

const goToPreviousSlide = () => {
  currentIndex.value = (currentIndex.value - 1 + imageUrls.value.length) % imageUrls.value.length;
}

onBeforeUnmount(() => {
  clearInterval(intervalId)
})
</script>