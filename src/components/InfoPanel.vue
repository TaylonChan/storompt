<template>
  <section 
    id="info-panel" 
    :class="store.infomenuStatus ? 'right-0' : 'right-[calc(var(--info)*-1)]'"
    class="absolute top-0 z-20 max-w-[--info] overflow-y-auto w-full h-full border-l border-theme-grid duration-300 bg-white xl:right-0"
  >
    <section id="panel-header" class="fixed w-[--info] h-[--header] border-b border-r border-theme-grid bg-white z-10 sm:w-full">
      <div class="absolute flex w-full h-full px-7 justify-between items-center">
        <img 
          @click="closeInfomenu"
          src="@/src/assets/icon/close_square.svg" 
          class="w-6 h-6 cursor-pointer duration-200 hover:scale-125 xl:hidden" 
          alt="close button"
        >
      </div>
    </section>
    <section id="panel-content" class="pt-[--header] pb-7">
      <div>
        <div class="h-10 items-center justify-center rounded-md bg-muted p-1 text-muted-foreground grid w-full grid-cols-2">
          <button 
            :data-state="tabState.charactor && 'active'"
            @click="changeTab('charactor')" 
            class="inline-flex items-center justify-center whitespace-nowrap rounded-sm px-3 py-1.5 text-sm font-medium ring-offset-background transition-all focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50 data-[state=active]:bg-background data-[state=active]:text-foreground data-[state=active]:shadow-sm"
          >
            Charactor
          </button>
          <button 
            :data-state="tabState.background && 'active'"
            @click="changeTab('background')"
            class="inline-flex items-center justify-center whitespace-nowrap rounded-sm px-3 py-1.5 text-sm font-medium ring-offset-background transition-all focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50 data-[state=active]:bg-background data-[state=active]:text-foreground data-[state=active]:shadow-sm"
          >
            Background
          </button>
        </div>
        <div v-if="tabState.charactor" value="charactor">
          <div v-if="chatItem['charactor']" class="p-7">
            <div 
              v-for="charactor in JSON.parse(chatItem['charactor'])"
              :key="charactor"
              class="flex items-center w-full mb-4 rounded-lg border border-theme-gray p-4 hover:bg-theme-light"
            >
              <div class="pr-4 border-r border-theme-gray">
                <img src="@/src/assets/avatar/Shape=10, Color=Fennel Flower.svg" class="w-8" alt="">
              </div>
              <div class="flex-1 pl-4 border-r border-theme-gray text-left">
                <h5 class="text-sm font-semibold">{{ charactor['name'] }}</h5>
                <span 
                  v-for="personality in charactor['personality'].replace(/\[|\]|\'/g,'').split(',')"
                  :key="personality"
                  class="text-xs opacity-70 mr-1 border-b border-theme-gray"
                >
                  {{ personality }}
                </span>
              </div>
              <div class="flex flex-col justify-center items-center pl-4">
                <button @click="chatTo(charactor['name'], charactor['personality'])" class="opacity-70 hover:opacity-100 pb-2">
                  <AtSign :size="18" :strokeWidth="1.5" />
                </button>
                <button @click="chatFrom(charactor['name'], charactor['personality'])" class="opacity-70 hover:opacity-100">
                  <MessageSquareText :size="18" :strokeWidth="1.5" />
                </button>
              </div>
            </div>
            <button 
              @click="openDialog()"
              class="flex justify-center items-center w-full mb-4 rounded-lg border border-theme-gray p-4 hover:bg-theme-light"
            >
              <div class="pr-4 border-r border-theme-gray">
                <UserRoundPlus :size="24" :strokeWidth="1" />
              </div>
              <div class="pl-4">
                <h5 class="text-xs font-semibold">Add New Charactor</h5>
              </div>
            </button>
          </div>
          <div v-else class="p-7">
            <Alert class="mb-8" variant="destructive">
              <AlertCircle class="w-4 h-4" />
              <AlertTitle>Loading Error</AlertTitle>
              <AlertDescription>
                <p>Failed To Receive Charactor Info</p>
              </AlertDescription>
            </Alert>
          </div>
        </div>
        <div v-if="tabState.background" id="background">
          <div class="p-7">
            <img src="@/src/assets/img/background_1.png" class="rounded-lg aspect-video object-cover object-center" alt="">
          </div>
          <div class="px-7">
            <h2 class="font-medium text-xl">{{ chatItem['title'] }}</h2>
            <p class="pt-2 text-sm opacity-70">{{ chatItem['title_description'] }}</p>
            <div class="flex my-7 py-7 border-y">
              <div class="flex-1 pr-2">
                <h5 class="pb-1 text-sm font-semibold text-theme-darklight">Genre</h5>
                <p class="text-sm leading-relaxed">{{ chatItem['genre'] }}</p>
              </div>
              <div class="flex-1 pr-2">
                <h5 class="pb-1 text-sm font-semibold text-theme-darklight">Classification</h5>
                <p class="text-sm leading-relaxed">{{ chatItem['classification'] }}</p>
              </div>
            </div>
            <div>
              <h5 class="pb-4 text-sm font-semibold text-theme-darklight">Background</h5>
              <p class="text-sm leading-relaxed">{{ chatItem['background'] }}</p>        
            </div>
          </div>
        </div>
      </div>
    </section>
  </section>
</template>

<script>
import { useStatusStore } from '@/src/store/useStatusStore'

import { Alert, AlertDescription, AlertTitle } from '@/src/components_shadcn/ui/alert'

import { 
  UserRoundPlus,
  AtSign,
  MessageSquareText,
  AlertCircle
} from 'lucide-vue-next';

export default {
    name: 'InfoPanel',
    components: {
      UserRoundPlus,
      AtSign,
      MessageSquareText,
      AlertCircle,
      Alert, 
      AlertDescription, 
      AlertTitle
    },
    props: [
      'chatItem'
    ],
    emits: ["changeTargetName", "receiveMessage"],
    data() {
      return {
        store: useStatusStore(),
        tabState: {
          charactor: false,
          background: true
        }
      }
    },
    computed: {
    },
    methods: {
      closeInfomenu() {
        this.store.infomenuStatus = false
      },
      changeTab(tabname) {
        Object.keys(this.tabState).map((item) => {
          if (item === tabname) {
            this.tabState[item] = true
          } else {
            this.tabState[item] = false
          }
        })
      },
      openDialog() {
        this.store.dialogStatus = true
      },
      chatTo(charname, personality) {
        this.$emit('changeTargetName', charname, personality)
      },
      chatFrom(charname, personality) {
        this.$emit('changeTargetName', charname, personality)
        this.$emit('receiveMessage', charname, personality)
      }
    }
}
</script>

<style>

</style>