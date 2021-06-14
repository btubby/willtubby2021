<template>
  <div id="app" class="toplevel">
    <Video />
    <vue-waterfall-easy
      ref="waterfall"
      :imgsArr="flickrItems"
      @scrollReachBottom="getData"
      @click="clickFn"
      @imgError="imgErrorFn"
    ></vue-waterfall-easy>
    enf
  </div>
</template>

<script>
import axios from "axios";
import Video from "./components/Video.vue";
import vueWaterfallEasy from "vue-waterfall-easy";

export default {
  name: "App",
  components: {
    Video,
    vueWaterfallEasy,
  },
  data() {
    return {
      flickrItems: [],
    };
  },

  methods: {
    clickFn(event, { index, value }) {
      // event.preventDefault()
      if (event.target.tagName.toLowerCase() == "img") {
        console.log("img clicked", index, value);
      }
    },
    imgErrorFn(imgItem) {
      console.log(`imgErrorFn ${imgItem}`);
    },
    getData() {
      console.log("getData");
    },
    processFickrImagesOrVideo(entry) {
      return {
        media: entry.media,
        id: entry.id,
        src: entry.url_z,
        hires: entry.url_l,
        height: parseInt(entry.height_z),
        width: parseInt(entry.width_z),
      };
    },
  },
  mounted() {
    let url =
      "https://api.flickr.com/services/rest/?method=flickr.photos.search&" +
      "&api_key=52f7e77ccc225a2c6cda920bb6173fb5" +
      "&user_id=tubbycreative" +
      "&sort=date-taken-desc" +
      "&tag_mode=all" +
      "&extras=tags,date_upload,date_taken,media,url_n,url_l,url_z,url_o&per_page=300&page=1" +
      "&format=json" +
      "&nojsoncallback=1";
    console.log(url);
    axios
      .get(url)
      .then((response) => {
        console.log(response);
        this.flickrItems = response.data.photos.photo.map(
          this.processFickrImagesOrVideo
        );
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>

<style>
.toplevel {
  /* background-color: black; */
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  min-height: 100%;
}
#vid {
  display: flex;
}

* {
  margin: 0;
  padding: 0;
}

html,
body,
#app {
  height: 100%;
}
.vue-waterfall-easy-container {
  background-color: black;
}
</style>
