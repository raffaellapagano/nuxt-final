<template>
  <div>
    <div class="card bg-light p-3">
      <p class="text-center">{{ user.name | uppercaseName }}</p>
      <button
        class="btn btn-primary"
        @click="
          Show(user.id);
          SetConsulted(user.name);
        "
      >
        Info
      </button>
    </div>
  </div>
</template>

<script>
import Vuex from 'vuex'

export default {
  props: {
    user: Object
  },
  methods: {
    Anterior () {
      this.$router.push('/')
    },
    Show (proId) {
      this.$router.push({
        name: 'ShowClient',
        params: {
          Pid: proId
        }
      })
    },
    ...Vuex.mapMutations(['ShowClients', 'SetConsulted', 'Prueba'])
  },
  computed: {
    ...Vuex.mapState(['showClient', 'users', 'consultedUsers'])
  },
  filters: {
    uppercaseName (value) {
      return value.toString().toUpperCase()
    }
  }
}
</script>

<style>
p {
  text-align: left;
}
</style>
