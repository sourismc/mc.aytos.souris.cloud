<template>
  <b-container>
    <b-row>
      <b-col md="4">
        MOTD:
      </b-col>
      <b-col md="8">
        {{ status.motd[0] }}
      </b-col>
    </b-row>
    <b-row>
      <b-col md="4">
        Verze:
      </b-col>
      <b-col md="8">
        {{ status.version }}
      </b-col>
    </b-row>
    <b-row>
      <b-col md="4">
        Edice:
      </b-col>
      <b-col md="8">
        {{ status.edition }}
      </b-col>
    </b-row>
    <b-row>
      <b-col md="4">
        Game Mode:
      </b-col>
      <b-col md="8">
        {{ status.gameMode }}
      </b-col>
    </b-row>
    <b-row>
      <b-col md="4">
        Maximální počet hráčů:
      </b-col>
      <b-col md="8">
        {{ status.maxPlayers }}
      </b-col>
    </b-row>
    <b-row>
      <b-col md="4">
        Hráčů online:
      </b-col>
      <b-col md="8">
        {{ status.onlinePlayers }}
      </b-col>
    </b-row>
  </b-container>
</template>

<script>

export default {
  name: 'ServerStatus',

  data () {
    return {
      status: {
        host: '',
        port: 19132,
        edition: '',
        motd: ['', ''],
        version: '',
        maxPlayers: 32,
        onlinePlayers: 0,
        gameMode: 'Survival',
        serverID: ''
      },
      refreshTimer: null
    }
  },

  async fetch () {
    console.log('fetching mcquery server status')
    const status = await fetch('http://localhost:19199/status').then(res => res.json())

    if (status.requestStatus === 'ok') {
      this.status = status
    } else {
      throw status.error
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
