<template>
  <div>
    <Home class="home"></Home>
  </div>
</template>

<script>
import Home from '~/components/HomeComponent.vue'

export default {
  components: { Home },
  mounted () {
    this.$store.dispatch('loadUsers')
    this.$store.dispatch('loadAlbums')
  }
}
</script>
