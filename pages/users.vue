<template>
  <div>
    <button
      class="btn btn-primary"
      @click="Anterior()"
    >
      Back
    </button>
    <h1
      class="font-weight-bold mt-3"
    >
      Users
    </h1>

    <div class="row p-3 d-flex justify-content-center">
      <ClienteComponent
        v-for="user in users"
        :key="user.id"
        :user="user"
        class="col-sm-3 mt-3"
      />
    </div>
  </div>
</template>

<script>
import Vuex from 'vuex'
import ClienteComponent from '../components/ClientComponent'

export default {
  components: {
    ClienteComponent
  },
  data () {
    return {
      clienteId: {
        type: Object,
        required: true
      }
    }
  },
  computed: {
    ...Vuex.mapState(['users', 'consulted', 'consultedUsers'])
  },
  methods: {
    Anterior () {
      this.$router.go(-1)
    }
    // ...Vuex.mapMutations(['ShowClients', 'SetConsulted'])
  }
}
</script>
