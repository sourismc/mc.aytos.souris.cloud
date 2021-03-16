<template>
  <b-container>
    <b-row
      v-for="player in players"
      :key="player._id"
    >
      <b-col>
        <h3>{{ player.name }}</h3>
      </b-col>
      <b-col>
        Money: {{ player.money }}
      </b-col>
      <b-col>
        Group: {{ player.group }}
      </b-col>
      <b-col>
        UUID: {{ player.uuid }}
      </b-col>
      <b-col>
        ONLINE: {{ player.onlineStatus ? 'Ano' : 'Ne' }}
      </b-col>
    </b-row>
  </b-container>
</template>

<script>

export default {
  name: 'PlayersList',

  data () {
    return {
      players: [],
      refreshTimer: null
    }
  },

  async fetch () {
    console.log('fetching mcquery players')
    const players = await fetch('http://localhost:19199/players').then(res => res.json())

    if (players.status === 'ok') {
      this.players = players
    } else {
      throw players.error
    }
  },

  beforeMount () {
    const vm = this
    this.refreshTimer = setInterval(() => {
      vm.$fetch()
    }, 1000)
  },

  beforeDestroy () {
    if (this.refreshTimer) {
      clearInterval(this.refreshTimer)
    }
  }
}
</script>

<style scoped>

</style>
