<template>
  <div id="app">
    <CurrentTime></CurrentTime>
    <transition name="moveIn">
      <router-view/>
    </transition>
  </div>
</template>

<script>
import CurrentTime from '@/components/CurrentTime.vue'

export default {
  components: {
    CurrentTime
  }
}
</script>

<style lang="less">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
.moveIn-enter-active{
  animation: fadeIn 1s ease-in;
}
@keyframes fadeIn{
  0%{
    opacity: 0;
  }
  100%{
    opacity: 1;
  }
}
</style>
