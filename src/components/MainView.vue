<template>
  <div class="main">
    <h1>Search</h1>
    <div class="search">
      <input type="text" placeholder="Search for song...">
      <button @click="changeType" class="icon">
        <i :class=type></i>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "MainView",
  data() {
    return {
      type: 'track'
    }
  },
  methods: {
    changeType() {
      this.type = this.type === 'track' ? 'album' : 'track'
    }
  }
};
</script>

<style scoped lang="less">
.search {
  width: 506px;
  margin: auto;
  position: relative;
  display: flex;
  &:before {
    content: "";
    height: 22px;
    width: 3px;
    background: #5856d6;
    position: absolute;
    top: 50%;
    left: 18px;
    transform: translateY(-50%);
  }
  input {
    padding: 21px 20px;
    padding-left: 28px;
    width: 378px;
    font-size: 16px;
    background: #f5f6f8;
    border: none;
    box-shadow: 2px 3px 5px 0px rgba(0, 0, 0, 0.16);
    &:focus {
      outline: none;
    }
  }
  .icon {
    width: 60px;
    height: 60px;
    background: #f5f6f8;
    margin-left: 20px;
    border: none;
    cursor: pointer;
    box-shadow: 2px 3px 5px 0px rgba(0, 0, 0, 0.16);
    outline: none;
    .track {
      background: url('../assets/icons/track-icon.svg') no-repeat;
      cursor: pointer;
      width: 19px;
      height: 21px;
      display: inline-block;
    }
    .album {
      background: url('../assets/icons/album-icon.svg') no-repeat;
      cursor: pointer;
      width: 39px;
      height: 27px;
      display: inline-block;
    }
    &:active {
      background: #e6e6e6;
    }
  }
}
</style>
