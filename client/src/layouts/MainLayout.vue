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
          <small>{{account}}</small>
        </q-toolbar-title>

        <q-space />
      <!--
        notice shrink property since we are placing it
        as child of QToolbar
      -->
      <q-tabs v-model="tab" shrink>
        <q-tab name="tab2" label="Логин" @click="showSettingsDialog"/>
        <q-tab name="tab3" label="Регистрация" @click="openSupportURL" />
        <q-tab name="tab4" :label="username"></q-tab>
      </q-tabs>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <q-page>
        <div class="row q-pa-none">
          <div class="col-5">
          <!-- <Groups :groups="groups" /> -->
          </div>
          <div class="col-7 q-pa-sm">
          </div>
        </div>
      </q-page>
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
