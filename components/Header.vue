<template>
  <div id="nav">
    <nav
      class="navbar navbar-expand-lg navbar-dark bg-dark p-3"
    >
      <a
        class="navbar-brand"
        href="#"
      >
        <img
          src="../assets/IT logo.png"
          width="150"
          alt=""
        ></img
        ></a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span
          class="navbar-toggler-icon"
        />
      </button>

      <div
        id="navbarSupportedContent"
        class="collapse navbar-collapse d-flex justify-content-center"
      >
        <nuxt-link
          class="nav-link"
          to="/"
        >
          Home
        </nuxt-link>
        <nuxt-link
          class="nav-link"
          to="/users"
        >
          Users
        </nuxt-link>
        <nuxt-link
          class="nav-link"
          to="/pictures"
        >
          Picture
        </nuxt-link>
      </div>

      <div
        class="
          col-12 col-lg-4
          d-flex
          align-items-center
          row
          justify-content-center
        "
      >
        <form
          class="
            form-inline
            my-2
            d-flex
            justify-content-center
            flex-nowrap
            align-items-center
          "
        >
          <div id="search" class="bg-white rounded-lg">
            <ejs-autocomplete
              id="inputSearch"
              v-model="search"
              type="input"
              :data-source="userArray"
              :fields="dataFields"
              :highlight="true"
              placeholder="Select user"
            />
          </div>
          <div class="input-group-append">
            <button
              id="buttonSearch"
              class="btn btn-secondary"
              type="button"
              @click="
                Show(SearchIdUser(search));
                if (verify) {
                  SetConsulted(search);
                };
                search = '';
              "
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="16"
                height="16"
                fill="currentColor"
                class="bi bi-search"
                viewBox="0 0 16 16"
              >
                <path
                  d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"
                />
              </svg>
            </button>
          </div>
        </form>
      </div>
    </nav>
  </div>
</template>

<script>
import Vue from 'vue'
import Vuex from 'vuex'
import { AutoCompletePlugin } from '@syncfusion/ej2-vue-dropdowns'
import userSearch from '../assets/users.json'
Vue.use(AutoCompletePlugin)

export default {
  data () {
    return {
      search: '',
      verify: false,
      dataFields: { value: 'name' },
      userArray: userSearch
    }
  },
  computed: {
    ...Vuex.mapState(['users'])
  },
  methods: {
    SearchIdUser (nameUser) {
      for (let i = 0; i < this.userArray.length; i++) {
        if (nameUser === this.userArray[i].name) {
          return this.userArray[i].id
        }
      }
    },
    Show (proId) {
      for (let index = 0; index < this.userArray.length; index++) {
        if (this.search === this.userArray[index].name) {
          this.verify = true
          this.$router.push({
            name: 'ShowClient',
            params: {
              Pid: proId
            }
          })
        }
        if (this.verify === false) {
          alert('No users')
          this.$router.push('/')
        }
      }
    },
    StringInput () {
      this.search = this.search.$data.search
    },
    ...Vuex.mapMutations(['SetConsulted'])
  }
}
</script>

<style lang="scss">

@import url(https://cdn.syncfusion.com/ej2/material.css);

#nav{
  padding: 30px;

  a {
    font-weight: bold;
    color: #f9fbfc;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}

#inputSearch{
  width: 200px;
  height: 20px;
  margin: 2px;
  background: white;
  border-radius: 5px;
}

#buttonSearch{
  height: 40px;
}

#buttonSearch {
  height: 40px;
}
</style>
