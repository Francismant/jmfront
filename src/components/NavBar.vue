<template>
    <div class="container">
        <div class="navbar">
            <q-img
                src="../assets/nav-logo.png"
                alt="logo avec inscription JM Construction et rénovation"
                width="250px"
            />
            <div class="buttonNavbar">
                <q-btn outline style="color: black;" label="Projets" />
                <q-btn outline style="color: black;" label="Faq" />
                <q-btn outline style="color: black;" label="Contact" />
                <q-btn style="color: black;" label="Devis" />
            </div>
        </div>
    </div>
</template>
<script>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'NavBar',
});
</script>
<script setup>
</script>
<style>
.container {
    height: 70px;
    width: 100%;
}
.navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.buttonNavbar {
    display: flex;
    margin-right: 30px;
    gap: 2rem;
}
</style>
