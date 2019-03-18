<template>
  <div class="track">
    <TrackView :track="id"></TrackView>
  </div>
</template>

<script>
import TrackView from "@/components/TrackView.vue";

export default {
  name: "playTrack",
  components: {
    TrackView
  },
  props: ["id"]
};
</script>
