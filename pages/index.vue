<template>
  <main>
    <b-carousel
      id="indexcarousel"
      v-model="carousel.slide"
      :interval="carousel.interval"
      controls
      indicators
      background="#ababab"
      img-width="1024"
      img-height="480"
      style="text-shadow: 1px 1px 2px #333;"
    >
      <b-carousel-slide
        caption="PvE & Survival"
        img-src="https://wallup.net/wp-content/uploads/2016/01/265248-Minecraft-shaders-video_games.jpg"
      />
      <b-carousel-slide
        caption="Customized Bedrock Edition Server"
        img-src="https://wallpapertag.com/wallpaper/full/2/1/2/487284-popular-minecraft-wallpaper-1080p-1920x1080-for-retina.jpg"
      />
    </b-carousel>

    <b-container class="mt-5">
      <b-row>
        <b-col v-for="action in actions" :key="action.id" class="text-center">
          <b-img
            width="140"
            height="140"
            rounded="circle"
            thumbnail
            :alt="action.image.alt"
            :src="require(`~/assets/img/${action.image.src}.png`)"
          />
          <h2>{{ action.title }}</h2>
          <p>{{ action.body }}</p>
          <p>
            <b-button size="sm" class="my-2 my-sm-0" type="button" @click="action.button.click">
              {{ action.button.text }}
            </b-button>
          </p>
        </b-col>
      </b-row>

      <hr class="big-note-divider"/>
      <b-row class="big-note-row">
        <b-col md="7">
          <h2>Jsme teprve na začátku!</h2>
          <p class="lead">
            Rozbíháme první funkcionality nad jádrem NukkitX, buďte součástí prvních testů a pomocte stvořit hezké místo!
          </p>
        </b-col>
        <b-col md="5">
          <b-img fluid-grow thumbnail src="https://wallpapercave.com/wp/wp2652291.jpg"/>
        </b-col>
      </b-row>

      <hr class="big-note-divider"/>
      <b-row class="big-note-row">
        <b-col md="7">
          <h2>Jsme teprve na začátku!</h2>
          <p class="lead">
            Rozbíháme první funkcionality nad jádrem NukkitX, buďte součástí prvních testů a pomocte stvořit hezké místo!
          </p>
        </b-col>
        <b-col md="5">
          <b-img fluid-grow thumbnail src="https://wallpapercave.com/wp/b6zzVDW.jpg"/>
        </b-col>
      </b-row>

      <hr class="big-note-divider"/>
    </b-container>
  </main>
</template>

<script>
export default {
  data () {
    return {
      carousel: {
        slide: 0,
        interval: 4000
      },

      actions: [],
      lastActionId: 0
    }
  },

  mounted () {
    this.addAction({
      imgsrcname: 'swords',
      imgalt: 'No PVP',
      title: 'PvE',
      body: 'Primární důraz je kladen na PvE a Survival!',
      btnclick: () => {
        console.log('PvE informace')
      }
    })
    this.addAction({
      imgsrcname: 'diamond',
      imgalt: 'Diamond',
      title: 'Mining',
      body: 'Kdo chce přežít musí těžit. A nebo handlovat s ostatními!',
      btnclick: () => {
        console.log('Mining informace')
      }
    })
    this.addAction({
      btnclick: () => {
        console.log('Obchody informace')
      }
    })
  },

  methods: {
    addAction (action) {
      const {
        imgsrcname = 'chest',
        imgalt = 'Chest',
        title = 'Obchody',
        body = 'Na serveru je možné využívat chest obchody, k zakoupení hůř dostupných itemů, cena bude ale samozřejmě úměrná!',
        btntext = 'Více informací',
        btnclick = () => {}
      } = action
      this.actions.push({
        image: {
          src: imgsrcname,
          alt: imgalt
        },
        title,
        body,
        button: {
          text: btntext,
          click: btnclick
        },
        id: this.lastActionId++
      })
    }
  }
}
</script>

<style scoped>
</style>
