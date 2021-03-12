<template>
  <header>
    <b-navbar toggleable="lg" type="dark" variant="success" sticky>
      <b-navbar-brand router-component-name="nuxt-link" to="/">
        SourisMC @ Aytos.Souris.CLOUD
      </b-navbar-brand>

      <b-navbar-toggle target="nav-collapse" />

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item v-for="navItem in navigationItems" :key="navItem.id" router-component-name="nuxt-link" :to="navItem.to" :disabled="navItem.disabled">
            {{ navItem.text }}
          </b-nav-item>
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-form>
            <b-form-input disabled size="sm" class="mr-sm-2" placeholder="mc.aytos.souris.cloud" />
            <b-button size="sm" class="my-2 my-sm-0" type="button" href="minecraft://aytos.souris.cloud">
              Připojit
            </b-button>
          </b-nav-form>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </header>
</template>

<script>
export default {
  name: 'Navigation',

  data () {
    return {
      navigationItems: [],
      lastNavigationItemId: 0
    }
  },

  mounted () {
    this.addNavigationItem('Crew', '/staff')
    this.addNavigationItem('FAQ', '/faq')
    this.addNavigationItem('Server Info', '/server-info')
  },

  methods: {
    addNavigationItem (text, to = '/', disabled = false) {
      this.navigationItems.push({
        id: this.lastNavigationItemId++,
        text,
        disabled,
        to
      })
    }
  }
}
</script>

<style scoped>

</style>
