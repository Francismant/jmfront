<template>
    <div>
        <q-carousel
      animated
      v-model="slide"
      arrows
      navigation
      infinite
    >
      <q-carousel-slide
      v-for="dataImg in datasImg.caroussel"
      :key="dataImg.id"
      :img-src="dataImg.attributes"
      @click="test(dataImg)"
      />
    </q-carousel>
    </div>
</template>

<script setup>
import { ref, defineProps } from 'vue';

const test = (dataImg) => {
  console.log(dataImg);
};

const slide = ref(1);

defineProps({
  datasImg: Object,
});
</script>
