<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <q-toolbar>
        <q-btn
          flat
          dense
          @click="leftDrawerOpen = !leftDrawerOpen"
          round
          icon="menu"
          aria-label="Menu"
           />

      </q-toolbar>
      <div class="q-px-lg q-pt-xl q-mb-md">
        <div class="text-h3">ToDo</div>
        <div class="class">{{ todaysDate }}</div>
      </div>
      <q-img
          src="https://cdn.pixabay.com/photo/2017/07/10/23/35/globe-2491989_960_720.jpg"
          :ratio="16/9"
          class="header-image absolute-top"
        />
    </q-header>

    <q-drawer
        v-model="leftDrawerOpen"
        show-if-above
        :width="250"
        :breakpoint="600"
      >
        <q-scroll-area style="height: calc(100% - 192px); margin-top: 192px; border-right: 1px solid #ddd">
          <q-list padding>
            <q-item
                to="/"
                clickable v-ripple>
              <q-item-section avatar>
                <q-icon name="list" />
              </q-item-section>

              <q-item-section>
                ToDo
              </q-item-section>
            </q-item>

            <q-item
                to="/Help"
                clickable v-ripple>
              <q-item-section avatar>
                <q-icon name="help" />
              </q-item-section>

              <q-item-section>
                Help
              </q-item-section>
            </q-item>

          </q-list>
        </q-scroll-area>

        <q-img class="absolute-top" src="https://cdn.pixabay.com/photo/2017/07/10/23/35/globe-2491989_960_720.jpg"
        :ratio="16/9" style="height: 192px">
          <div class="absolute-bottom bg-transparent">
            <q-avatar size="56px" class="q-mb-sm">
              <img src="https://media.licdn.com/dms/image/C4E03AQHBZ_j0w_YnWg/profile-displayphoto-shrink_100_100/0/1623167098109?e=1680739200&v=beta&t=_ByEFAMnWQSNQ3MV3pqCrgEvcu3XDEMjTWjMDTnXoD0">
            </q-avatar>
            <div class="text-weight-bold">Maurice Cune</div>
            <div>@mauircecune</div>
          </div>
        </q-img>
      </q-drawer>

    <q-page-container>
      <keep-alive>
        <router-view />
      </keep-alive>

    </q-page-container>
  </q-layout>
</template>

<script>
import { date } from 'quasar'

export default {
  name: 'MainLayout',

  data () {
    return {
      leftDrawerOpen: false
    }
  },
  computed: {
    todaysDate () {
      const timeStamp = Date.now()
      return date.formatDate(timeStamp, 'dddd D MMMM')
    }
  }
}
</script>

<style lang="scss">
  .header-image{
    height: 100%;
    z-index: -1;
    opacity: 0.2;
    filter: grayscale(100%);
  }
</style>
