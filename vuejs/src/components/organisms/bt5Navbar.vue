<template>
  <div>
    <nav class="navbar navbar-expand-lg bg-light">
      <div class="container-fluid">
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarTogglerDemo03"
          aria-controls="navbarTogglerDemo03"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <a class="navbar-brand" href="#">
          <router-link to="/" class="nav-link">Fluchtachterl</router-link>
          </a>
        <div class="collapse navbar-collapse" id="navbarTogglerDemo03">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">

            <li class="nav-item">
              <router-link to="/products" class="nav-link">
                Products
              </router-link>
            </li>
            <li class="nav-item">
              <router-link to="/auctions" class="nav-link">
                Auctions
              </router-link>
            </li>
            <li class="nav-item">
              <router-link to="/imprint" class="nav-link">Imprint</router-link>
            </li>
            <li class="nav-item">
              <router-link to="/help" class="nav-link">Help</router-link>
            </li>
            <li class="nav-item" v-if="permission == 'Admin'">
              <router-link to="/usermoderation" class="nav-link">User Moderation</router-link>
            </li>
            <!--
            <li class="nav-item dropdown">
              <a
                class="nav-link dropdown-toggle"
                href="#"
                role="button"
                data-bs-toggle="dropdown"
                aria-expanded="false"
              >
                Dropdown
              </a>
              <ul class="dropdown-menu">
                <li><a class="dropdown-item" href="#">Action</a></li>
                <li><a class="dropdown-item" href="#">Another action</a></li>
                <li>
                  <hr class="dropdown-divider" />
                </li>
                <li>
                  <a class="dropdown-item" href="#">Something else here</a>
                </li>
              </ul>
            </li>
            <li class="nav-item">
              <a class="nav-link disabled">Disabled</a>
            </li>
            -->
          </ul>
          <div class="d-flex" v-if="!permission">
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
              <li class="nav-item">
                <router-link to="/login" class="nav-link">Login</router-link>
              </li>
              <li class="nav-item">
                <router-link to="/register" class="nav-link">
                  Register
                </router-link>
              </li>
            </ul>
          </div>

          <div class="d-flex" v-if="permission">
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
              <li class="nav-item">
                <router-link to="/user" class="nav-link">User</router-link>
              </li>
              <li class="nav-item nav-link" @click="logoutUser">
<!--                <router-link to="/" class="nav-link">-->
                  Logout
<!--                </router-link>-->
              </li>
            </ul>
          </div>
          <!--
          <form class="d-flex" role="search">
            <input
              class="form-control me-2"
              type="search"
              placeholder="Search"
              aria-label="Search"
            />
            <button class="btn btn-outline-success" type="submit">
              Search
            </button>
          </form>
          -->
        </div>
      </div>
    </nav>
  </div>
</template>

<script>
import jwt_decode from "jwt-decode";
import {watch} from "vue";
import { useRouter, useRoute } from 'vue-router'

export default {
  name: "bt5Navbar",
  data() {
    return {
      permission: null
    }
  },
  methods: {
    logoutUser() {
      localStorage.clear()
      // this.$forceUpdate()
      window.location.reload()

    }
  },
  created() {
    // get the username from local storage
    let tkn = localStorage.getItem('accessToken');
    if (tkn) {
      let decoded_token = jwt_decode(tkn)
      // set the username data property
      this.permission = decoded_token.permissions;
      console.log(this.permission)
      // window.location.reload()
    } else {
      this.$router.push({ path: '/' })
    }

  },



};
</script>

<style>

  #nav .active-link-nav {
    color: #42b983;
    border-bottom: 2px solid blue;
  }

</style>
