<template>
  <div class="containner">
<input type="text" v-model="keyword">
  <button @click="searchData()">Search</button>
  <!--{{List}}-->
  
  <div>
 <!-- id = {{data.mal_id}}
  ชื่อ = {{data.title}}
  รายละเอียด = {{data.synopsis}}
  รูป = {{data.image_url}}<img src="data.image_url">-->
  <b-card-group columns>
   <b-card v-for="data in List" :key="data.trackId"
    :title="data.trackName"
    :img-src="data.artworkUrl100"
    img-alt="Image"
    img-top
    tag="article"
    style="max-width: 20rem;"
    class="mb-auto"
  >
    <b-card-text>
      {{data.synopsis}}
    </b-card-text>

    <b-button :href="data.trackViewUrl" variant="primary">Go somewhere</b-button>
  </b-card>
  </b-card-group>
  </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      List: null,
      keyword:''
    };
  },
  methods: {
    searchData() {
      axios
        .get("https://itunes.apple.com/search?term="+this.keyword)
        .then((response) => {
          this.List = response.data.results;
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>
<style>
</style>