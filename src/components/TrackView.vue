<template>
  <div class="main">
    <router-link class="back" tag="a" to="/">
      <i class="arrow-icon"></i>
    </router-link>
    <h1 class="title">Track</h1>
    {{trackData.name}}
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
  props: ["track"],
  created() {
    if (this.track === undefined) {
      router.push({
        name: "home"
      });
    }
    this.fetchTrack();
  },
  data() {
    return {
      trackData: []
    };
  },
  methods: {
    fetchTrack() {
      axios.get(`https://api.spotify.com/v1/tracks/${this.track}`, 
      {
        headers: {
          Authorization: `Bearer ${this.$root.TOKEN}`
        }
      })
      .then(response => {
        console.log(response);
        this.trackData = response.data;
      });
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
  @media (max-width: 320px) {
  }
  @media (max-width: 480px) {
  }
}
</style>
