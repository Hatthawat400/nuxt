<template>
  <div>
    <v-row>
      <v-col cols="9">
        <v-text-field v-model="textsearch" label="" solo />
      </v-col>
      <v-col cols="3">
        <v-btn large @click="set()">
          <v-icon>mdi-magnify</v-icon>
        </v-btn>
      </v-col>
    </v-row>

    <v-row>
      <v-col
        v-for="list in Datalist"
        :key="list.trackId"
        class="d-flex child-flex"
        cols="4"
      >
        <nuxt-link :to="{ name: 'datas-id', params: { id: list } }">
          <v-hover v-slot:default="{ hover }">
            <v-card flat tile class="d-flex" :elevation="hover ? 12 : 2">
              <v-img
                :src="list.artworkUrl100"
                aspect-ratio="1"
              >
                <p>{{ list.trackName }}</p>
              </v-img>
            </v-card>
          </v-hover>
        </nuxt-link>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      Datalist: null,
      textsearch: ''
    }
  },
  methods: {
    set () {
      axios
        .get(
          'https://itunes.apple.com/search?term=$' + this.textsearch + '&limit=30'
        )
        .then((resp) => {
          this.Datalist = resp.data.results
          this.$emit('Datalist', Object(resp.data.results))
        })
        .catch((err) => {
          console.error(err)
        })
    }
  }
}
</script>

<style>
p {
  white-space: nowrap;
  width: 100px;
  overflow: hidden;
  text-overflow: clip;
}
</style>
