<template>
  <main id="grid" class="grid" :class="{ 'grid-ready': gridIsReady }">
    <card-news />
    <card-add />
    <card
      v-for="(entry, i) in startups"
      :key="i"
      v-bind="entry"
      :card-id="idFromTitle(entry.title)"
      @click="$router.push({ path: `#${idFromTitle(entry.title)}` })"
    />
  </main>
</template>

<script>
import MagicGrid from 'magic-grid'
import Card from '@/components/Card'
import CardAdd from '@/components/CardAdd'
import CardNews from '@/components/CardNews'
// import { getYposition } from '@/utils'

export default {
  components: {
    Card,
    CardAdd,
    CardNews
  },
  props: {
    startups: {
      type: Array,
      default: () => []
    }
  },
  data: function() {
    return {
      magicGrid: null
    }
  },
  computed: {
    gridIsReady() {
      return this.magicGrid ? this.magicGrid.ready() : false
    }
  },
  watch: {
    startups() {
      this.$nextTick(() => {
        this.initGrid()
      })
    }
  },
  mounted() {
    this.initGrid()
  },
  methods: {
    initGrid() {
      this.magicGrid = new MagicGrid({
        container: this.$el,
        items: this.startups.length + 2,
        animate: true,
        gutter: 20
        // useMin: true
        // maxColumns: 5
      })
      this.magicGrid.listen()
      if (this.$route.hash) {
        this.$nextTick(() => {
          setTimeout(() => {
            const y = this.getYposition(this.$route)
            window.scrollTo(0, y)
          }, 500)
        })
      }
    },
    idFromTitle(title) {
      const slug = title.toLowerCase().replace(' ', '-')
      const cardId = `card-${slug}`
      return cardId
    },
    getYposition(to) {
      const target = document.querySelector(to.hash)
      return target.getBoundingClientRect().top - 50
    }
  }
}
</script>

<style lang="scss">
.grid {
  transition: opacity 200ms ease-in;
  opacity: 0;
  &.grid-ready {
    opacity: 1;
  }
}
</style>
