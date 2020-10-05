<template>
  <v-container>
    <h1>選択</h1>
    <v-btn dark @click="selectView"> 切替 </v-btn>
    <div id="app">
      <RotateBox v-if="view" />
      <Sphere v-else />
    </div>
  </v-container>
</template>

<script>
import RotateBox from '~/components/RotateBox'
import Sphere from '~/components/Sphere'

export default {
  name: 'App',
  components: {
    RotateBox,
    Sphere,
  },
  data() {
    const view = false
    return {
      view,
    }
  },
  methods: {
    selectView() {
      this.view = !this.view
    },
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
