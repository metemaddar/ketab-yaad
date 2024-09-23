<template>
  <q-layout view="hHh lpr lFf">

    <q-header elevated class="bg-primary text-white" height-hint="98">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />

        <q-toolbar-title>
          <q-avatar>
            <q-icon name="auto_stories" />
          </q-avatar>
          Ketab Yaad
          <CurrentDate />
        </q-toolbar-title>

        <q-btn dense flat round icon="menu" @click="toggleRightDrawer" />
      </q-toolbar>

      <q-tabs align="left">
        <q-route-tab to="/page1" label="Page One" />
        <q-route-tab to="/page2" label="Page Two" />
        <q-route-tab to="/page3" label="Page Three" />
      </q-tabs>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" side="left" overlay bordered>
      <!-- drawer content -->
    </q-drawer>

    <q-drawer show-if-above v-model="rightDrawerOpen" side="right" bordered>
      <!-- drawer content -->
    </q-drawer>

    <q-page-container>
      <router-view />
      <AddBookPopup v-model:dialog="dialog" @book-added="handleBookAdded" />
    </q-page-container>



    <q-footer elevated class="bg-grey-8 text-white">
      <q-toolbar>
        <q-toolbar-title>
          <q-avatar>
            <img src="https://cdn.quasar.dev/logo-v2/svg/logo-mono-white.svg">
          </q-avatar>
          <div>Title</div>
          <div class="fixed-bottom-right q-mr-lg q-mb-lg">
            <q-btn round color="secondary" icon="library_add" class="q-mr-sm" @click="showDialog" />
            <q-btn round color="primary" icon="add_circle" />
          </div>
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>

  </q-layout>
</template>

<script>
import { ref } from 'vue'
import DateComponent from 'src/components/DateComponent.vue';
import AddBookPopup from 'src/components/AddBookPopup.vue';

export default {
  setup() {
    const leftDrawerOpen = ref(false)
    const rightDrawerOpen = ref(false)

    const dialog = ref(false);

    const showDialog = () => {
      dialog.value = true;
    };

    const handleBookAdded = (book) => {
      console.log('Book added:', book);
      // Handle the book data as needed
    };

    return {
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value
      },

      rightDrawerOpen,
      toggleRightDrawer() {
        rightDrawerOpen.value = !rightDrawerOpen.value
      },
      dialog,
      showDialog,
      handleBookAdded
    }
  },
  components: {
    CurrentDate: DateComponent,
    AddBookPopup,
  },

}
</script>
