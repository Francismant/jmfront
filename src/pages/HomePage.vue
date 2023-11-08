<template>
  <div class="parallax-container">
    <ParallaxComponent />
  </div>
  <div class="intro-container">
    <q-img :src="urlImg" alt="Description de l'image" class="image-container"/>
    <p class="text-container" v-if="introsData.length > 0">{{ introsData[0].text }}</p>
    <!-- <p>{{ introsData.text }}</p> -->
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import ParallaxComponent from '../components/ParallaxComponent.vue';

const introsData = ref([]);

// async function getIntroData() {
//   const data = await axios.get('http://localhost:1337/api/intros?populate=*');
//   introsData.value = data.data.map((introData) => ({
//     ...introData,
//     text: introData.attributes.text,
//   }));
//   // introsData.value = data.data;
//   // console.log(introsData.value.data);
// }

async function getIntroData() {
  const response = await axios.get('http://localhost:1337/api/intros?populate=*');
  if (response.data && Array.isArray(response.data.data)) {
    introsData.value = response.data.data.map((introData) => ({
      text: introData.attributes.text,
    }));
    console.log(introsData.value[0].text);
  } else {
    console.error('Data structure is not as expected:', response.data);
  }
}

const urlImg = ref('http://localhost:1337/uploads/small_LOGOJ_8f37b3c4f3.jpg');

onMounted(() => {
  getIntroData();
});
</script>

<style>
.parallax-container {
  margin-top: 70px;
}
.intro-container {
  display: flex;
  align-items: center;
  gap: 2rem;
}
.image-container {
  width: 50%;
}
.text-container {
  width: 50%;
}
</style>
