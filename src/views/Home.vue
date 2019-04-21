<template>
  <div class="home">
    <MainView></MainView>
  </div>
</template>

<script>
// @ is an alias to /src
import MainView from "@/components/MainView.vue";

export default {
  name: "home",
  components: {
    MainView
  }
};
</script>
