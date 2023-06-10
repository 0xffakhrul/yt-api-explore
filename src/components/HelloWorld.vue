
<template>
  <div>
    <h1>{{ msg }}</h1>
    <h2>{{ quote }}</h2>

    <ul>
      <li v-for="video in videos" :key="video.id.videoId" class="box">
        {{ video.snippet.title }}
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from "vue";
import axios from "axios";

export default {
  setup() {
    const videos = ref([]);

    const loadQuote = async () => {
      try {
        const response = await axios.get(
          "https://youtube.googleapis.com/youtube/v3/search?part=snippet&channelId=UCbJM_Y06iuUOl3hVPqYcvng&maxResults=10&order=viewCount&key=AIzaSyBMS5znSwBJoWxJIsItuVawq7TPDjvs2Hw"
        );
        videos.value = response.data.items;
      } catch (err) {
        console.log(err);
      }
    };

    loadQuote();

    return {
      videos,
    };
  },
};

// defineProps({
//   msg: String,
// });
</script>

<style scoped>
.box {
  background: black;
  width: 20rem;
  height: 10rem;
}
</style>
