<template>
  <v-app id="inspire">
    <!-- Left Bar -->
    <v-navigation-drawer
      v-model="drawer"
      app
    >
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="text-h6">
            Application
          </v-list-item-title>
          <v-list-item-subtitle>
            subtext
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list
        dense
        nav
      >
        <v-list-item
          v-for="item in items"
          :key="item.title"
          link
          :to="item.link"
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <!-- Top Bar -->
    <v-app-bar app>
      <v-app-bar-nav-icon @click="toogleDrawer"></v-app-bar-nav-icon>
      <v-toolbar-title>Application</v-toolbar-title>
    </v-app-bar>

    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
  export default {
    data() {
      return {
        drawer: Object,
        items: [
          { title: 'Countries', icon: 'mdi-earth', link: '/' },
          { title: 'Photos', icon: 'mdi-image', link: '/about' },
          { title: 'About', icon: 'mdi-help-box' },
        ],
        right: null,
      }
    },
    methods: {
      toogleDrawer() {
        this.drawer = !this.drawer
        localStorage.setItem('_drawer', this.drawer ? 'even' : 'odd')
      }
    },
    created () {
      const _drawer = localStorage.getItem('_drawer')
      if (['odd', 'even'].indexOf(_drawer) === -1) {
        this.drawer = true
      } else {
        this.drawer = _drawer === 'even'
      }
      localStorage.setItem('_drawer', this.drawer ? 'even' : 'odd')
    },
  }
</script>