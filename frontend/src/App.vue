<template>
  <body>
    <Header />
    <div class="content">
      <Main />
    </div>
    <Footer />
  </body>
</template>

<script setup lang="ts">
import Header from './blocks/header/Header.vue';
import Footer from './blocks/footer/Footer.vue';
import Main from './blocks/main/Main.vue';


</script>

<style scoped>
  .content {
    display: flex;
    flex-direction: row;
  }
</style>
