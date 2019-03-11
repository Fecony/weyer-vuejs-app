<template>
  <div class="main">
    <h1 class="title">Search</h1>
    <form @submit.prevent="sendForm">
      <div class="search">
        <input v-model="text" type="text" placeholder="Search for song...">
        <a @click="changeType" class="icon">
          <i :class="type"></i>
        </a>
      </div>
      <input :disabled="disabled" type="submit" class="search-btn" value="Search"/>
    </form>
  </div>
</template>

<script>
export default {
  name: "MainView",
  data() {
    return {
      type: "track",
      text: null,
      disabled: true
    };
  },
  watch: {
    text: function(val) {
      if (this.text && this.text.length > 0) {
        this.disabled = false;
      } else {
        this.disabled = true;
      }
    }
  },
  methods: {
    changeType() {
      this.type = this.type === "track" ? "album" : "track";
    },
    sendForm() {
      // console.log(this.text + " | " + this.type);
      this.text = null;
    }
  }
};
</script>

<style scoped lang="less">
.main {
  .title {
    font-size: 60px;
    font-family: "Roboto", sans-serif;
    color: #2a3757;
  }
  .search {
    width: 506px;
    margin: auto;
    position: relative;
    display: flex;
    margin-top: 152px;
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
      padding: 21px 20px 21px 28px;
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
      min-width: 60px;
      width: 60px;
      height: 60px;
      background: #f5f6f8;
      margin-left: 20px;
      border: none;
      cursor: pointer;
      box-shadow: 2px 3px 5px 0px rgba(0, 0, 0, 0.16);
      outline: none;
      i {
        position: absolute;
        top: 50%;
        transform: translate(-50%) translateY(-50%);
      }
      .track {
        background: url("../assets/icons/track-icon.svg") no-repeat;
        cursor: pointer;
        width: 19px;
        height: 21px;
        display: inline-block;
      }
      .album {
        background: url("../assets/icons/album-icon.svg") no-repeat;
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
  .search-btn {
    border: none;
    outline: none;
    cursor: pointer;
    font-size: 22px;
    font-weight: 500;
    height: 50px;
    background: #49c77a;
    color: #f5f6f8;
    width: 146px;
    margin-top: 238px;
    font-family: "Roboto", sans-serif;
    &:active {
      background: rgb(66, 182, 111);
    }
    &:disabled {
      background: gray;
      cursor: default; 
    }
  }
  @media (max-width: 320px) {
    .search-btn {
      margin-top: 150px;
    }
    .search {
      margin-top: 0;
    }
  }
  @media (max-width: 480px) {
    .search {
      width: 100%;
      margin-top: 0;
    }
  }
}
</style>
