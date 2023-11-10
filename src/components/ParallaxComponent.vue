<template>
  <div>
    <q-parallax :height="400" :speed="0.5">
      <template v-slot:media>
        <img :src="'http://localhost:1337' + parallaxsImage[0].image" class="custom-parallax">
      </template>
    </q-parallax>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

const parallaxsImage = ref([{ image: '' }]);

// async function getParallaxsImage() {
//   const response = await axios.get('http://localhost:1337/api/parallaxes?populate=*');
//   const imagesParallax = response.data.data.map((imageParallax) => ({
//     image: imageParallax.attributes.parallaxImage.data.attributes.url,
//   }));
//   // console.log('testParallax', imagesParallax);
//   ParallaxsImage.value = imagesParallax;
//   console.log('Parallax', ParallaxsImage.value);
// }

async function getParallaxsImage() {
  try {
    const response = await axios.get('http://localhost:1337/api/parallaxes?populate=*');
    const imagesParallax = response.data.data.map((imageParallax) => ({
      image: imageParallax.attributes.parallaxImage.data.attributes.url,
    }));
    parallaxsImage.value = imagesParallax;
    console.log('Parallax', parallaxsImage.value[0].image);
  } catch (error) {
    console.error('Error fetching parallax images:', error);
  }
}

// async function fetchActivities() {
//   const url = 'http://localhost:1337/api/parallaxes?populate=*';
//   const { data } = await axios.get(url);
//   parallaxsImage.value = data.map((imageParallax) => ({
//     ...imageParallax,
//     image: imageParallax.attributes.parallaxImage.data.attributes.url,
//   }));
//   console.log('parallax', parallaxsImage.value);
// }

onMounted(async () => {
  await getParallaxsImage();
  // await fetchActivities();
});

</script>

<style scoped>
.custom-parallax img {
  width: 100vw;  /* Ajustez la taille selon vos besoins */
  height: auto; /* Garantit que l'aspect ratio de l'image est préservé */
}
</style>
