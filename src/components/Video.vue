<template>
  <div>
    <VideoBackground
      ref="videobackground"
      :src="this.video"
      id="video-player"
      style="max-height: 400px; height: 100vh;"
    >
      <h1 style="color: white;">WilTubby.com</h1>
    </VideoBackground>
  </div>
</template>

<script>
import VideoBackground from "vue-responsive-video-background-player";

export default {
  name: "HelloWorld",
  data() {
    return {
      video: require("@/assets/vidtest.mp4"),
      videoMoon: require("@/assets/vid.mp4"),
    };
  },
  components: { VideoBackground },
  props: {
    msg: String,
  },

  methods: {},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#video-player {
}
</style>
