<template>
  <q-layout view="hHh lpR fFf">

    <q-header elevated class="bg-primary text-white">
      <q-toolbar>

        <q-btn v-model="toolbarBtnMenu" v-if="toolbarBtnMenu" dense flat round icon="menu" @click="drawerLeftState = !drawerLeftState" />

        <q-toolbar-title>
          <q-avatar>
            <img src="https://cdn.quasar.dev/logo/svg/quasar-logo.svg">
          </q-avatar>
          Guacamolas 
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer  v-model="drawerLeftState" side="left" bordered>
      <!-- drawer content -->
      <q-scroll-area class="fit">
          <q-list v-for="(menuItem, index) in menuList" :key="index">

            <q-item :to="menuItem.route" clickable :active="menuItem.label === 'Outbox'" v-ripple>
              <q-item-section avatar>
                <q-icon :name="menuItem.icon" />
              </q-item-section>
              <q-item-section>
                {{ menuItem.label }}
              </q-item-section>
            </q-item>

           <q-separator v-if="menuItem.separator" />

          </q-list>
        </q-scroll-area>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>

  </q-layout>
</template>

<script>
const menuList = [
  {
    icon: 'inbox',
    label: 'Sign-In',
    separator: false,
    route: '/signin'
  },
  {
    icon: 'send',
    label: 'Sign-Up',
    separator: false,
    route: '/signup'
  }
];
export default {
  name:'Layout',
  data () {
    return {
      menuList
    }
  },
  computed: {
    drawerLeftState: {
      get () {
        return this.$store.state.layout.drawerLeftState
      },
      set (val) {
        this.$store.commit('layout/updateDrawerLeftState', val)
      }
    },
    toolbarBtnMenu: {
      get () {
        return this.$store.state.layout.toolbarBtnMenu
      },
      set (val) {
        this.$store.commit('layout/updateToolbarBtnMenu', val)
      }
    }
  }
}
</script>