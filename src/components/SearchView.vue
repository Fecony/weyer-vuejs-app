<template>
  <div class="main" v-if="items.data.length > 0">
    <router-link class="back" tag="a" to="/">
      <i class="arrow-icon"></i>
    </router-link>
    <h1 class="title">{{ items.type | capitalize}}</h1>
    <div v-if="items.type == 'albums'" class="album-search-result">
      <a class="item" href="#" v-for="item in items.data" :key="item.id">
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
        v-for="item in items.data"
        :key="item.id"
        :to="{ name: 'playTrack', params: { id: item.id } }"
      >{{ item.name }} - {{ item.artists[0].name }}
      </router-link>
    </div>
  </div>
  <div class="main" v-else>
    <router-link class="back" tag="a" to="/">
      <i class="arrow-icon"></i>
    </router-link>
    <h1>Sorry nothing found</h1>
    <h1 style="transform: rotate(90deg)">:(</h1>
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
  .back {
    display: block;
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
    margin: 0 15%;
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
      width: 150px;
      height: 150px;
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
        content: '\27A4';
        color: #263759;
        position: absolute;
        width: 12px;
        height: 12px;
        left: .5em;
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
  @media (max-width: 320px) {
  }
  @media (max-width: 480px) {
  }
}
</style>
