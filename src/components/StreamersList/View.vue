<template>
  <div class="streamers-list">
    <button class="toggle-button"
      v-on:click="toggleOffline">
      Toggle offline and non-existent streamers
    </button>
    <template v-if="!showOnlineOnly">
      <div class="stream-container" v-for="streamer in streamList">
        <img class="logo" :src="streamer.logo">
        <a class="description" :href="streamer.url">
          <span class="name">{{ streamer.name }}</span>
          <span class="game">{{ streamer.desc }}</span>
        </a>
        <img class="preview" :src="streamer.preview">
      </div>
    </template>
    <template v-else>
      <div class="stream-container" v-for="streamer in streamListOnline">
        <img class="logo" :src="streamer.logo">
        <a class="description" :href="streamer.url">
          <span class="name">{{ streamer.name }}</span>
          <span class="game">{{ streamer.desc }}</span>
        </a>
        <img class="preview" :src="streamer.preview">
      </div>
    </template>
  </div>
</template>

<script>
export default {
  props: [
    'streamList'
  ],
  name: 'StreamersListView',
  data () {
    return {
      showOnlineOnly: false
    }
  },
  methods: {
    toggleOffline: function () {
      this.showOnlineOnly = !this.showOnlineOnly
    }
  },
  computed: {
    streamListOnline: function () {
      return this.streamList.filter((el) => {
        return el.online
      })
    }
  }
}
</script>

<style>
  .toggle-button {
    width: 80%;
    margin-left: 10%;
    margin-top: 20px;
    margin-bottom: 20px;
    padding: 10px;
    border: 1px solid black;
    background-color: #4a67b1;
    color: white;
  }
  .streamers-list {
    width: 100%;
  }
  .stream-container:nth-of-type(2n) {
    background-color: #694ab1;
  }
  .stream-container:nth-of-type(2n+1) {
    background-color: #422f6c;
  }
  .stream-container {
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-left: 10px;
    box-sizing: border-box;
  }
  .stream-container > .logo {
    height: 40px;
    width: auto;
  }
  .stream-container > .description {
    width: 40%;
  }
  .stream-container > .description > .name {
    font-weight: bold;
    text-transform: uppercase;
    margin: 5px;
  }
  @media only screen and (max-width: 900px) {
    .stream-container > .description > .name {
      display: block;
    }
    .stream-container > .description > .game {
      display: block;
    }
  }
  .stream-container > .description > .game {
    margin: 5px;
  }
  .stream-container > .preview {
    height: 80px;
    width: auto;
  }
  @media only screen and (max-width: 400px) {
    .stream-container > .logo {
      height: 30px;
      width: auto;
    }
    .stream-container > .preview {
      height: 40px;
      width: auto;
    }
  }
</style>
