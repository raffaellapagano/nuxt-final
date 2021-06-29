<template>
  <div class="home">
    <div class="d-flex row justify-content-center">
      <Consulted
        :title="'Users'"
        :arrayConsulted="consultedUsers"
        class="col-lg-4"
      ></Consulted>
      <Consulted
        :title="'Pictures'"
        :arrayConsulted="consultedAlbums"
        class="col-lg-4"
      ></Consulted>
    </div>
  </div>
</template>

<script>
import Vuex from 'vuex'
import Consulted from '.././components/ConsultedComponent'

export default {
  name: 'Home',
  components: {
    Consulted
  },
  data () {
    return {
      numberShow: 0
    }
  },
  methods: {
    ...Vuex.mapMutations(['SetConsulted'])
  },
  computed: {
    ...Vuex.mapState([
      'albums',
      'users',
      'consultedUsers',
      'consultedAlbums',
      'modal'
    ])
  }
}
</script>
