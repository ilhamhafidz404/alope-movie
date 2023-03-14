<template>
  <navbar></navbar>
  <router-view></router-view>
  <foot></foot>
</template>

<script>
import navbar from "./components/navbar.vue";
import foot from "./components/footer.vue";
export default {
  components: {
    navbar,
    foot,
  },
};
</script>

<style>
</style>