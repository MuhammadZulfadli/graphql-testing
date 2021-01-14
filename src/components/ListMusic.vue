<template>
  <div class="mx-auto px-5 py-24 ">
    <div class="flex flex-wrap m-4 gap-4">
      <!-- component -->
      <div
        class="mx-auto bg-white overflow-hidden border-b-4 border-red-400 w-1/3"
        v-for="musics in music"
        :key="musics.id"
      >
        <img
          :src="musics.artist.image"
          alt="People"
          class="w-full object-cover h-32 sm:h-48 md:h-64"
        />
        <div class="p-4 md:p-6">
          <h3 class="text-green-500 font-semibold text-base mb-1 leading-none">
            {{ musics.title }}
          </h3>
          <h4
            class="font-semibold mb-2 text-xl leading-tight sm:leading-normal"
          >
            {{ musics.artist.name }}
          </h4>
          <div class="text-sm flex items-center">
            <span class="leading-none">{{
              musics.artist.biography.publishDate
            }}</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "ListMusic",
  data() {
    return {
      music: []
    };
  },

  methods: {
    async GetList() {
      const response = await axios({
        method: "POST",
        url: "https://graphbrainz.herokuapp.com/?",
        data: {
          query: `
                {
                 lastFM{
                    chart{
                        topTracks{
                                nodes{
                                title
                                    artist {
                                        name
                                        image
                                        url
                                        biography{
                                            publishDate
                                            }
                                    }
                                }
                            }
                        }
                    }
                }
            `
        }
      });
      this.music = response.data.data.lastFM.chart.topTracks.nodes;
      console.log(this.music);
    }
  },
  mounted() {
    this.GetList();
  }
};
</script>

<style></style>
