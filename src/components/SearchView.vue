<template>
  <div class="main" v-if="items.length > 0 && !loading">
    <router-link class="back" tag="a" to="/">
      <i class="arrow-icon"></i>
    </router-link>
    <h1 class="title">{{ type | capitalize}}</h1>
    <div class="alert alert-danger" v-if="error">{{ error }}</div>
    <div class="alert alert-loading" v-if="loading">Fetching data...</div>
    <div v-if="type == 'album'" class="album-search-result">
      <a class="item" href="#" v-for="item in items" :key="item.id">
        <span>
          <img :src="item.images[0].url">
          <span class="info">
            <p class="name">{{ item.name }}</p>
            <p class="artist">{{ item.artists[0].name }}</p>
          </span>
        </span>
      </a>
    </div>
    <div v-else class="track-search-result">
      <router-link
        class="item"
        tag="a"
        v-for="item in items"
        :key="item.id"
        :to="{ name: 'playTrack', params: { id: item.id } }"
      >{{ item.name }} - {{ item.artists[0].name }}</router-link>
    </div>
  </div>
  <div class="main" v-else>
    <router-link class="back" tag="a" to="/">
      <i class="arrow-icon"></i>
    </router-link>
    <h1>Sorry nothing found</h1>
    <h1>😔</h1>
  </div>
</template>

<script>
import axios from "axios";
import router from "../router";

export default {
  name: "SearchView",
  data() {
    return {
      loading: true,
      error: null,
      items: [],
      query: "",
      type: "",
      baseURL: process.env.VUE_APP_BASE_URL || "http://localhost:8888"
    };
  },
  created() {
    this.query = this.$route.query.query;
    this.type = this.$route.query.type;
    this.fetchData();
  },
  methods: {
    fetchData() {
      axios
        .get(`${this.baseURL}/tracks?query=${this.query}&type=${this.type}`)
        .then(response => {
          this.items = response.data;
          this.error = null;
        })
        .finally(() => {
          this.loading = false;
        });
    }
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

<style scoped lang="less">
.main {
  .title {
    font-size: 60px;
    font-family: "Roboto", sans-serif;
    color: #2a3757;
    margin-bottom: 55px;
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
    &-danger {
      background: rgb(220, 21, 21);
      position: absolute;
      left: 50%;
      transform: translate(-50%);
      &:before {
        content: "\26A0";
        position: absolute;
        left: 15px;
        top: 50%;
        transform: translateY(-50%);
      }
    }
    &-loading {
      position: absolute;
      left: 50%;
      transform: translate(-50%);
      &:before {
        content: "\21BB";
        position: absolute;
        left: 15px;
        transform: translateY(-50%);
        animation: spin 4s linear infinite;
        @keyframes spin {
          0% {
            transform: rotate(0deg);
          }
          100% {
            transform: rotate(360deg);
          }
        }
      }
    }
  }
  .back {
    display: block;
    cursor: pointer;
    i.arrow-icon {
      background: url("../assets/icons/arrow_icon.svg") no-repeat top left;
      width: 40px;
      background-size: 40px 70px;
      height: 70px;
      left: 10%;
      top: 15%;
      position: absolute;
    }
  }
  .album-search-result {
    margin: 0 auto;
    max-width: 70%;
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
    a:link,
    a:visited,
    a:active {
      text-decoration: none;
    }
    .item {
      width: 13%;
      height: 13%;
      margin: 0 19px 19px 0;
      position: relative;
      img {
        width: 100%;
        height: 100%;
      }
      .info {
        opacity: 0;
        display: flex;
        left: 0;
        top: 0;
        position: absolute;
        background: rgba(23, 60, 66, 0.7);
        height: 100%;
        width: 100%;
        color: white;
        flex-wrap: wrap;
        transition: 0.3s;
        .name,
        .artist {
          margin: auto;
          text-align: center;
        }
        .name {
          width: 150px;
          font-weight: 600;
          font-size: 15px;
        }
        .artist {
          width: 150px;
          font-weight: 900;
          font-size: 15px;
        }
        &:hover {
          opacity: 1;
        }
      }
      &:nth-child(6n) {
        margin-right: 0;
      }
    }
  }
  .track-search-result {
    .item {
      display: block;
      text-align: left;
      border-radius: 4px;
      border: 1px solid;
      margin: 5px 250px;
      padding: 5px 5px 5px 30px;
      color: #263759;
      position: relative;
      text-decoration: none;
      &:before {
        content: "\27A4";
        color: #263759;
        position: absolute;
        width: 12px;
        height: 12px;
        left: 0.5em;
      }
      &:hover {
        background: #263759;
        color: white;
        font-weight: bold;
        &:before {
          color: white;
        }
      }
    }
  }
}
@media (min-width: 1025px) and (max-width: 1280px) {
  .main {
    .album-search-result {
      max-width: 80%;
    }
    .track-search-result {
      .item {
        margin: 5px 150px;
      }
    }
  }
}

@media (min-width: 768px) and (max-width: 1024px) {
  .main {
    .album-search-result {
      .item {
        width: 30%;
        height: 30%;
        &:nth-child(6n) {
          margin-right: 19px;
        }
        &:nth-child(3n) {
          margin-right: 0;
        }
      }
    }
    .track-search-result {
      .item {
        margin: 5px 100px;
      }
    }
  }
}

@media (min-width: 481px) and (max-width: 767px) {
  .main {
    .album-search-result {
      max-width: 100%;
      .item {
        width: 30%;
        &:nth-child(6n) {
          margin-right: 19px;
        }
        &:nth-child(3n) {
          margin-right: 0;
        }
      }
    }
    .track-search-result {
      .item {
        margin: 5px 20px;
      }
    }
  }
}
@media (min-width: 320px) and (max-width: 480px) {
  .main {
    .album-search-result {
      max-width: 100%;
      .item {
        width: 100%;
        margin: 10px 20px;
      }
    }
    .track-search-result {
      .item {
        margin: 5px auto;
      }
    }
  }
}
</style>
