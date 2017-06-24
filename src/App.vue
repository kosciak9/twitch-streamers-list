<template>
  <div class="app">
    <twitch-title></twitch-title>
    <streamers-list></streamers-list>
  </div>
</template>

<script>
import StreamersList from './components/StreamersList/Container.vue'
import TwitchTitle from './components/TwitchTitle/View.vue'

export default {
  name: 'app',
  components: {
    StreamersList,
    TwitchTitle
  },
  data () {
    return {
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Poppins');

html {
  width: 100%;
}
body {
  background-color: #4B367C;
  color: white;
  width: 100%;
  font-family: 'Poppins', sans-serif;
}
a {
  color: white;
  text-decoration: none;
}
.app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
</style>
