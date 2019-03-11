<template>
  <div class="time">
    <h1>{{datenow}}</h1>
  </div>
</template>

<script>
export default {
  name: 'CurrentTime',
  data() {
    return {
      datenow: '...'
    }
  },
  methods: {
    time() {
      this.datenow = moment().format('HH:mm')
    }
  },
  mounted() {
    this.interval = setInterval(this.time, 1000)
  },
  beforeDestroy() {
    clearInterval(this.interval)
  }
}
</script>

<style lang="less" scoped>
.time {
  h1 {
    font-size: 40px;
    color: #000;
  }
}
</style>
