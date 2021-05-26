<template>
  <q-layout view="hHh lpR fFf" class="WAL__layout">
    <q-header reveal class="bg-grey-9 text-white">
      <q-toolbar class="shadow-2">
        <q-toolbar-title>
          ITSU
          &nbsp;&nbsp;
          <span>
            Connecting people
          </span>
          &nbsp;&nbsp;
        </q-toolbar-title>

        <q-space />
      <!--
        notice shrink property since we are placing it
        as child of QToolbar
      -->
      <q-tabs shrink>
        <q-route-tab name="tab2" label="Логин" to="login"></q-route-tab>
        <q-route-tab name="tab3" label="Регистрация" to="register"></q-route-tab>
      </q-tabs>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />

    </q-page-container>
  </q-layout>
</template>

<script>
import Corps from 'components/Corps.vue';

export default {
  name: 'MainLayout',
  components: { Corps },
  data() {
    return {
      leftDrawerOpen: false,
      // essentialLinks: linksData,
    };
  },
};
</script>
