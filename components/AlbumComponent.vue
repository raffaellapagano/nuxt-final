<template>
  <div>
    <img
      class="imgAlbum"
      :src="album.url"
      alt=""
      @click="
        Show(album.id);
        SetConsultedPictures(album.title);"/>
  </div>
</template>

<script>
import Vuex from 'vuex'

export default {
  name: 'Album',
  props: {
    album: Object
  },
  components: {
  },
  methods: {
    Anterior () {
      this.$router.push('/')
    },
    Show (proId) {
      this.$router.push({
        name: 'ShowAlbum',
        params: {
          Pid: proId
        }
      })
    },
    ...Vuex.mapMutations(['SetConsultedPictures'])
  },
  computed: {
    ...Vuex.mapState(['showClient', 'albums'])
  }
}
</script>

<style scoped>
p {
  text-align: center;
}

.imgAlbum {
  height: 100%;
  width: 100%;
  cursor: pointer;
}
</style>
