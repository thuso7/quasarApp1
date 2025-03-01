<template>
  <q-layout view="lHh Lpr lFf">
    <q-header 
     :class="state"
     bordered>
      <q-toolbar>
        <q-btn
          flat          
          round
          class="q-ml-sm"
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title class="text-center">
          OnChat
        </q-toolbar-title>

        <q-btn
          flat          
          round          
          icon="eva-search"
          class="q-mr-sm"          
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />
      </q-toolbar>
    </q-header>

    <q-footer 
     :class="state"
     bordered>
        <q-tabs
         no-caps
         indicator-color="transparent"
         v-model="tab">

        <q-tab name="mails" icon="mdi-chat-outline" label="Chats" />
        <q-tab name="alarms" icon="explore" label="Discover" />
        <q-tab name="movies" icon="mdi-account-multiple-outline" label="People" />
        <q-tab name="movies" icon="mdi-phone-outline" label="Calls" />
        
      </q-tabs>
    </q-footer>

    <q-drawer
      v-model="leftDrawerOpen"
      :class="state"
      show-if-above
    >
      <q-list>
        <q-avatar
        class="q-ml-md q-mt-md q-mb-sm" 
        size="36px">
          <img src="1.jpg">
        </q-avatar>

        <q-item clickable v-ripple>
          <q-item-section>
           <q-item-label>
             <strong>
               Fred Jumbe
             </strong>
           </q-item-label>
           <q-item-label caption>
            0998422412
           </q-item-label>
         </q-item-section>
        </q-item>

        <q-separator class="q-mt-md q-mb-md" inset />

        <EssentialLink
          v-for="link in linksList"
          :key="link.title"
          v-bind="link"
        />

       <q-separator class="q-mt-md q-mb-md" inset />

       <q-expansion-item        
        icon="mdi-settings"
        label="Account settings"
        caption="John Doe"
      >
        <q-item clickable v-ripple>
        <q-item-section avatar>
          <q-icon color="primary" name="bluetooth" />
        </q-item-section>

        <q-item-section>Icon as avatar</q-item-section>
      </q-item>

      <q-item clickable v-ripple>
        <q-item-section avatar>
          <q-icon color="primary" name="bluetooth" />
        </q-item-section>

        <q-item-section>Icon as avatar</q-item-section>
      </q-item>
      </q-expansion-item>


      </q-list>

      <q-btn
          flat          
          round
          class="q-ml-sm q-mb-md absolute-bottom"
          icon="eva-moon-outline"
          aria-label="Menu" 
          @click="toggleBottomSheet"         
        />
    </q-drawer>

    <q-dialog    
    v-model="dialog" 
    position="bottom">

      <q-card 
      class="touch-draggabel"
      style="width: 350px; border-top-left-radius: 28px; border-top-right-radius: 28px">
         <div class="text-weight-bold q-ml-lg q-mt-lg">
           Dark Mode
         </div>
         
         <q-item 
         @click="dark"
         class="q-px-lg"
         tag="label" v-ripple>        
        <q-item-section>
          <strong>
              On
            </strong>
        </q-item-section>

        <q-item-section avatar>
          <q-radio v-model="color" val="opt1" color="teal" />
        </q-item-section>
      </q-item>  

      <q-item 
          @click="light"
         class="q-px-lg"
         tag="label" v-ripple>        
        <q-item-section>
          <strong>
              Off
            </strong>
        </q-item-section>

        <q-item-section avatar>
          <q-radio v-model="color" val="opt2" color="teal" />
        </q-item-section>
      </q-item>  

      <q-item 
          @click="auto"
         class="q-px-lg"
         tag="label" v-ripple>        
        <q-item-section>
          <strong>
              Default system
            </strong>
        </q-item-section>

        <q-item-section avatar>
          <q-radio v-model="color" val="opt3" color="teal" />
        </q-item-section>
      </q-item>  
      
      </q-card>
    </q-dialog>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref, computed } from 'vue'
import { useQuasar } from 'quasar'
import EssentialLink from 'components/EssentialLink.vue'

const linksList = [
  {
    title: 'Contacts',
    caption: 'quasar.dev',
    icon: 'school',
    link: 'https://quasar.dev'
  },
  {
    title: 'Channels',
    caption: 'github.com/quasarframework',
    icon: 'code',
    link: 'https://github.com/quasarframework'
  },
  {
    title: 'Discord Chat Channel',
    caption: 'chat.quasar.dev',
    icon: 'chat',
    link: 'https://chat.quasar.dev'
  },
  {
    title: 'Calls',    
    icon: 'mdi-phone'    
  },
  {
    title: 'Twitter',
    caption: '@quasarframework',
    icon: 'rss_feed',
    link: 'https://twitter.quasar.dev'
  }
]

const dialog = ref(false)

const toggleBottomSheet = () => {
  dialog.value = true
}

 const $q = useQuasar()

const leftDrawerOpen = ref(false)

const color = ref("opt1")

function toggleLeftDrawer () {
  leftDrawerOpen.value = !leftDrawerOpen.value
}

function dark () {
  $q.dark.set(true) 

}

function light () {
  $q.dark.set(false)
}

function auto () {
  $q.dark.set("auto")
 
}

const state = computed(() => {
  if ($q.dark.isActive) {
    return 'body--dark'
  }
  else return 'body--light'
})
</script>
