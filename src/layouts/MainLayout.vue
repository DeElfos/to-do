<template>
  <q-layout view="lhh lpR lff">
    <q-header class="transparent">
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above bordered id="header">
      <MenuProfile />
      <EssentialLink />

      <div id="header-content" class="full-width">
        <MenuBottom />
      </div>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>

    <q-footer align="center" class="transparent q-py-lg">
      <p> Feito por Marcos Filho / DeElfos</p>
      <p>Todos os direitos reservados</p>
      <p>Em caso de reprodução, atribua os créditos!</p>
      
    </q-footer>

  </q-layout>
</template>

<script>
import EssentialLink from "components/EssentialLink.vue";
import MenuProfile from "components/MenuProfile.vue";
import MenuBottom from "components/MenuBottom.vue";

import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "MainLayout",

  components: {
    EssentialLink,
    MenuProfile,
    MenuBottom,
  },

  setup() {
    const leftDrawerOpen = ref(false);

    return {
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
});
</script>

<style lang="scss">
#header {
  position: relative;
  min-height: 150px;
}

#header-content {
  position: absolute;
  bottom: 0;
  left: 0;
}
</style>
