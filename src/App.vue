<template>
  <div id="app">
    <navbar />
    <div>
      <router-view />
    </div>
  </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";

export default {
  components: {
    Navbar
  }
};
</script>

Navbar
