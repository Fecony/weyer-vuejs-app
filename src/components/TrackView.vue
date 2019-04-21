<template>
  <div class="main" v-if="trackData">
    <a class="back" @click="goBack">
      <i class="arrow-icon"></i>
    </a>
    <h1 class="title">Track</h1>
    <div class="alert alert-danger" v-if="error">{{ error }}</div>
    <div class="alert alert-loading" v-if="loading">Fetching data...</div>
    {{trackData.name}}
    <img :src="trackData.album.images[0].url" width="100px">
    <audio controls>
      <source :src="trackData.preview_url">
      <p>Your browser doesn't support audio</p>
    </audio>
  </div>
</template>

<script>
import axios from "axios";
import router from "../router";

export default {
  name: "TrackView",
  data() {
    return {
      id: "",
      loading: true,
      error: null,
      trackData: null
    };
  },
  created() {
    this.id = this.$route.params.id;
    this.fetchTrack();
  },
  methods: {
    fetchTrack() {
      axios
        .get(`https://api.spotify.com/v1/tracks/${this.id}`, {
          headers: {
            Authorization: `Bearer ${this.$root.TOKEN}`
          }
        })
        .then(response => {
          this.trackData = response.data;
          this.error = null;
        })
        .catch(e => {
          this.error = e.response.data.error.message;
          if (e.response.data.error.status == 401) {
            this.refreshToken();
          }
        })
        .finally(() => {
          this.loading = false;
        });
    },
    refreshToken() {
      axios
        .get(
          process.env.VUE_APP_REFRESH_URL ||
            "http://localhost:8888/refreshToken"
        )
        .then(response => {
          this.$root.TOKEN = response.data;
          this.fetchTrack();
        })
        .catch(e => {
          this.error = e.response.data.error.message;
        });
    },
    goBack() {
      this.$router.go(-1);
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
  @media (max-width: 320px) {
  }
  @media (max-width: 480px) {
  }
}
</style>
