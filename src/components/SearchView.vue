<template>
  <div class="main" v-if="items">
    <h1 class="title">{{ items.type | capitalize}}</h1>
    <div>
      <ul>
        <li
          v-for="item in items.data"
          :key="item.id"
        >{{ item }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
import router from "../router";

export default {
  name: "SearchView",
  props: {
    items: {
      required: true
    }
  },
  created() {
    if (this.items === undefined) {
      router.push({
        name: "home"
      });
    };
  },
  filters: {
    capitalize: function(value) {
      if (!value) return "";
      value = value.toString();
      return value.charAt(0).toUpperCase() + value.slice(1);
    }
  }
};
</script>