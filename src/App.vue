<template>
  <div id="app">
    <nav-bar></nav-bar>
    <hr>
    <h1>지금 코드 바꿉니다. 배포까지 해주세요</h1>
    <router-view></router-view>
  </div>
</template>

<script>
import NavBar from '@/components/NavBar.vue'

import { mapActions } from 'vuex'

export default {
  name: 'App',
  components: { NavBar },
  methods: {
    ...mapActions(['fetchCurrentUser'])
  },
  created() {
    this.fetchCurrentUser()
  }
}
</script>


<style>

</style>
