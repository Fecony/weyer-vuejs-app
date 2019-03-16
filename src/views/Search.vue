<template>
  <div class="search">
    <SearchView :items="results"></SearchView>
  </div>
</template>

<script>
import SearchView from '@/components/SearchView.vue'

export default {
  name: 'search',
  components: {
    SearchView
  },
  props: ['results']
}
</script>
