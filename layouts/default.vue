<template lang="pug">
  v-app(dark)
    v-navigation-drawer(:mini-variant.sync="miniVariant" :clipped="clipped" v-model="drawer" fixed app)
      v-list
        v-list-tile(router :to="item.to" :key="i" v-for="(item, i) in items" exact)
          v-list-tile-action
            v-icon(v-html="item.icon")
          v-list-tile-content
            v-list-tile-title(v-text="item.title")
    v-toolbar(fixed app :clipped-left="clipped")
      v-toolbar-side-icon(@click="drawer = !drawer")
      v-btn(icon @click.stop="miniVariant = !miniVariant")
        v-icon(v-html="miniVariant ? 'chevron_right' : 'chevron_left'")
      v-btn(icon @click.stop="clipped = !clipped")
        v-icon web
      v-btn(icon @click.stop="fixed = !fixed")
        v-icon remove
      v-toolbar-title(v-text="title")
      v-spacer
      v-btn(icon @click.stop="rightDrawer = !rightDrawer")
        v-icon menu
    v-content
      v-container
        nuxt
    v-navigation-drawer(temporary :right="right" v-model="rightDrawer" fixed)
      v-list
        v-list-tile(@click.native="right = !right")
          v-list-tile-action
            v-icon(light) compare_arrows
          v-list-tile-title Switch drawer (click me)
    v-footer(:fixed="fixed" app)
      span © \{{ new Date().getFullYear() }}
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator'

interface Item {
  icon: string
  title: string
  to: string
}

@Component
export default class DefaultLayout extends Vue {
  public title: string = 'Vuetify.js'
  public clipped: boolean = false
  public drawer: boolean = false
  public fixed: boolean = false
  public miniVariant: boolean = false
  public right: boolean = true
  public rightDrawer: boolean = false

  public items: Array<Item> = [
    {
      icon: 'apps',
      title: 'Welcome',
      to: '/'
    },
    {
      icon: 'bubble_chart',
      title: 'Inspire',
      to: '/inspire'
    }
  ]
}
</script>
