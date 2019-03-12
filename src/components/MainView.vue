<template>
  <div class="main">
    <h1 class="title">Search</h1>
    <div class="alert alert-danger" v-if="error">{{ error }}</div>
    <div class="alert" v-if="loading">Loading...</div>
    <form @submit.prevent="sendForm">
      <div class="search">
        <input v-model="text" type="text" placeholder="Search for song...">
        <a @click="changeType" class="icon">
          <i :class="type"></i>
        </a>
      </div>
      <input :disabled="textIsEmpty" type="submit" class="search-btn" value="Search">
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "MainView",
  data() {
    return {
      type: "track",
      text: "",
      disabled: true,
      loading: false,
      error: false
    };
  },
  created() {
    this.fetch();
  },
  computed: {
    textIsEmpty: function() {
      return this.text.length == 0;
    }
  },
  methods: {
    changeType() {
      this.type = this.type === "track" ? "album" : "track";
    },
    async fetch() {
      this.loading = true;
      await axios
        .get("http://localhost:8888/")
        .then(response => {
          this.$root.TOKEN = response.data;
          this.text = "";
          this.error = false;
        })
        .catch(e => {
          this.error = e;
          console.log(e);
        })
        .finally(() => {
          this.loading = false;
        });
    },
    sendForm() {
      // console.log(this.text + " | " + this.type);
      this.text = "";
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
  .alert {
    border-radius: 5px;
    width: 40%;
    margin: 0 auto;
    text-align: left;
    position: relative;
    padding: 10px 10px 10px 40px;
    color: white;
    font-weight: 600;
    background: #2a3757;
    opacity: 0.8;
    position: relative;
    &-danger {
      background: rgb(220, 21, 21);
      &:before {
        content: "\26A0";
        position: absolute;
        left: 15px;
        top: 50%;
        transform: translateY(-50%);
      }
    }
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
      opacity: 0.5;
      cursor: not-allowed;
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
    .alert {
      margin-bottom: 20px;
      width: 85%;
    }
  }
}
</style>
