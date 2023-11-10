<template>
  <div class="parallax-container">
    <ParallaxComponent />
  </div>
  <div class="intro-container">
    <q-img :src="'http://localhost:1337' + introsData[0].image" alt="Description de l'image" class="image-container"/>
    <p class="text-container">{{ introsData[0].text }}</p>
  </div>
  <div class="caroussel-container">
    <carousselHome
      v-for="carousselData in carousselsData"
      :key="carousselData.id"
      :datasImg="carousselData"
    />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import ParallaxComponent from '../components/ParallaxComponent.vue';
import carousselHome from '../components/CarousselHome.vue';

const introsData = ref([{}]);
const carousselsData = ref([{}]);

async function getIntroData() {
  const response = await axios.get('http://localhost:1337/api/intros?populate=*');
  const textIntro = response.data.data.map((introData) => ({
    text: introData.attributes.text,
    image: introData.attributes.logo.data.attributes.url,
  }));
  // console.log('test', textIntro);
  introsData.value = textIntro;
  // console.log('intro', introsData.value);
}

async function getCaroussel() {
  const response = await axios.get('http://localhost:1337/api/caroussels?populate=*');
  const datas = response.data.data.map((data) => ({
    caroussel: data.attributes.caroussel,
  }));
  console.log('caroussel', datas);
  carousselsData.value = datas;
  console.log(carousselsData.value);
}

onMounted(() => {
  getIntroData();
  getCaroussel();
});

</script>

<style scoped>
.parallax-container {
  margin-top: 70px;
}
.intro-container {
  padding-left: 4rem;
  margin-top: 50px;
  display: flex;
  align-items: center;
  gap: 2rem;
}
p {
  font-size: 24px;
}
.image-container {
  width: 35rem;
  padding: 10%;
}
.text-container {
  padding: 0 15% 0 2%;
}
.caroussel-container {
  height: 300px;
}
</style>
