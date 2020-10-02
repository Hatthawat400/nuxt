<template>
  <div>
    <v-row no-gutters>
      <nuxt-link to="/">
        หน้าแรก
      </nuxt-link>/{{ Name }}
    </v-row>
    <v-row nogutters>
      <v-col cols="2">
        <v-img :src="img" />
      </v-col>
      <v-col cols="8">
        <v-list-item-title class="headline mb-1">
          {{ Name }}
        </v-list-item-title>
        <a :href="collectionViewUrl" target="_blank">
          <span>{{ artistName }}</span></a>
        <v-list-item>Gene : {{ Gene }}</v-list-item>
        <v-list-item>Collection : {{ Collection }}</v-list-item>
      </v-col>
    </v-row>

    <v-row>
      <v-col cols="2" />
      <v-col cols="12">
        <audio-player :sources="previewUrl" :loop="true" />
      </v-col>
    </v-row>

    <v-divider />
    <v-row>
      <v-col cols="12">
        <v-card>
          <v-list-item-group>
            <v-list-item
              v-for="list in Datalist"
              :key="list.trackId"
            >
              <v-img
                :src="list.artworkUrl100"
                max-width="50"
              />
              <p>{{ list.trackName }}</p>
            </v-list-item>
          </v-list-item-group>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<style >
</style>

<script>
export default {
  data () {
    return {
      Datalist: null,
      Name: this.$route.params.id.trackName,
      Gene: this.$route.params.id.primaryGenreName,
      Collection: this.$route.params.id.collectionName,
      collectionViewUrl: this.$route.params.id.collectionViewUrl,
      img: this.$route.params.id.artworkUrl100,
      artistName: this.$route.params.id.artistName,
      previewUrl: this.$route.params.id.previewUrl
    }
  }
}
</script>
