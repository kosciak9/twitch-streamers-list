<template>
  <streamers-list :streamList="streamList"></streamers-list>
</template>

<script>
import StreamersList from './View.vue'

export default {
  name: 'StreamersListContainer',
  components: {
    StreamersList
  },
  methods: {
    refresh: function () {
      const api = 'https://api.twitch.tv/kraken/'
      const clientId = '?client_id=ws1jkkl2igiymv87pspxh9y4vh4cex'
      for (let i = 0; i < this.streamers.length; i++) {
        this.$http.get(api + 'channels/' + this.streamers[i] + clientId)
          .then((response) => {
            return response.data
          })
          .then((data) => {
            this.$http.get(api + 'streams/' + this.streamers[i] + clientId)
              .then((response) => {
                if (!response.data.stream) {
                  this.streamList.push(
                    {
                      name: data.name,
                      desc: 'Channel is offline',
                      logo: data.logo,
                      url: data.url,
                      online: false,
                      preview: '//origen.gg/assets/plugins/origen-streams/public/img/offline.png'
                    }
                  )
                } else {
                  this.streamList.push(
                    {
                      name: data.display_name,
                      desc: `Streaming ${response.data.stream.game}`,
                      url: data.url,
                      logo: data.logo,
                      preview: response.data.stream.preview.medium,
                      online: true
                    }
                  )
                }
              })
              .catch((err) => console.log(err))
          })
          .catch((err) => {
            if (err) {
              this.streamList.push(
                {
                  name: this.streamers[i],
                  desc: 'User does not exist',
                  logo: 'https://www.socialtalent.co/wp-content/uploads/2015/08/question-mark-512.gif',
                  preview: '//origen.gg/assets/plugins/origen-streams/public/img/offline.png',
                  online: false
                }
              )
            }
          })
      }
    }
  },
  data () {
    return {
      streamList: [],
      streamers: [
        'imaqtpie',
        'ESL_SC2',
        'freecodecamp',
        'taketv',
        'comster404'
      ]
    }
  },
  mounted () {
    this.refresh()
  }
}
</script>
