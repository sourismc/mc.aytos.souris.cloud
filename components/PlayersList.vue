<template>
  <b-container>
    <b-row
      v-for="player in players"
      :key="player._id"
      align-content="center"
    >
      <b-col cols="1">
        <span :class="`dot-status dot-status--${player.onlineStatus ? 'online' : 'offline'}`"></span>
      </b-col>
      <b-col>
        <h4>{{ player.name }}</h4>
      </b-col>
      <b-col>
        Peníze: {{ player.money }}
      </b-col>
      <b-col>
        Skupina: {{ translateGroup(player.group) }}
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
    const players = await fetch('https://query.mc.aytos.souris.cloud/players').then(res => res.json())

    if (players.status === 'ok') {
      this.players = players.players
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
  },

  methods: {
    translateGroup (group) {
      switch (group) {
        case 'staff': return 'Admin'
        case 'player': return 'Hráč'
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.dot-status {
  height: 25px;
  width: 25px;
  border-radius: 50%;
  display: inline-block;

  &--offline {
    background-color: darkred;
  }

  &--online {
    background-color: darkgreen;
  }
}
</style>
