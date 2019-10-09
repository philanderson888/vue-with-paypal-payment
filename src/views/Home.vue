<template>
  <div class="home">
    <main-shop msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
// @ is an alias to /src
import MainShop from "@/components/MainShop.vue";

export default {
  name: "home",
  components: {
    MainShop
  }
};
</script>
