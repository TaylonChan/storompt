<template>
  <menu 
    id="sidemenu" 
    ref="sidemenu" 
    class="absolute z-30 max-w-[--menu] overflow-y-scroll w-full h-full pb-[--header] border-r border-theme-grid bg-white duration-300 [&>*]:select-none"
    :class="store.sidemenuStatus ? 'left-0' : 'left-[calc(var(--menu)*-1)]'"
  >
    <section id="menu-header" class="fixed w-[--menu] h-[--header] border-b border-r border-theme-grid bg-white z-10">
      <div class="absolute flex w-full h-full px-7 justify-between items-center">
        <button>
          <img src="@/src/assets/logo/storompt_logo_dark_only.svg" class="w-10" alt="storompt logo">
        </button>
        <img 
          @click="closeSidemenu"
          src="@/src/assets/icon/close_square.svg" 
          class="w-6 h-6 cursor-pointer duration-200 hover:scale-125" 
          alt="close button"
        >
      </div>
    </section>
    <section id="navigation" class="mt-[--header] p-7 pb-0">
      <div class="flex flex-col pb-2">
        <button class="flex items-center py-2 px-3 mb-2 rounded-lg border-x-theme-gridlight border duration-200 hover:bg-theme-light active:bg-theme-grid">
          <img src="@/src/assets/icon/discovery.svg" class="mr-8" alt="explore">
          <span class="mb-[0.125rem] font-medium text-sm">Explore</span>
        </button>
        <button class="flex items-center py-2 px-3 mb-2 rounded-lg border-x-theme-gridlight border duration-200 hover:bg-theme-light active:bg-theme-grid">
          <img src="@/src/assets/icon/heart.svg" class="mr-8" alt="liked story">
          <span class="mb-[0.125rem] font-medium text-sm">Liked Story</span>
        </button>
        <button class="flex items-center py-2 px-3 mb-2 rounded-lg border-x-theme-gridlight border duration-200 hover:bg-theme-light active:bg-theme-grid">
          <img src="@/src/assets/icon/setting.svg" class="mr-8" alt="setting">
          <span class="mb-[0.125rem] font-medium text-sm">Setting</span>
        </button>
      </div>
    </section>
    <section id="journey" class="flex flex-col">
      <div class="flex justify-between items-center pt-4 ">
        <h5 class="pl-7 text-sm text-theme-darklight font-semibold">YOUR JOURNEY</h5>
        <button @click="$router.push('/demo')" class="group flex items-center pr-7 opacity-90 hover:opacity-100">
          <img src="@/src/assets/icon/plus.svg" class="w-5 mr-1.5 group-hover:scale-110 duration-200" alt="add button">
          <span class="mt-[0.125rem] text-xs font-semibold">NEW</span>
        </button>
      </div>
      
      <div class="my-4 border-y border-y-theme-gridlight">
        <button @click="$router.push('/demo/ee28faa9-c4b5-4972-b516-66d985b8030e')" class="group relative flex flex-col justify-center w-full h-20 px-10 border-b border-b-theme-gridlight first:bg-theme-pale hover:bg-theme-light last:border-0 
        [&>*]:max-w-[200px] [&>*]:whitespace-nowrap [&>*]:overflow-hidden [&>*]:text-ellipsis">
          <h6 class="pb-1.5 text-xs opacity-50">Fantasy</h6>
          <h3 class="pb-0.5 text-sm font-semibold">Harry Potter</h3>
          <p class="text-xs opacity-70">Harry Potter is a magical story about a young boy named Harry who discovers he has special powers.</p>
          <img src="@/src/assets/icon/more_square.svg" class="hidden absolute right-2 top-2 w-5 rounded-full group-hover:block hover:bg-[#0001] active:bg-theme-darklight" alt="more">
        </button>
        <button @click="$router.push('/demo/cd64e696-5b61-4c77-bc7d-88ae6c2e3826')" class="group relative flex flex-col justify-center w-full h-20 px-10 border-b border-b-theme-gridlight first:bg-theme-pale hover:bg-theme-light last:border-0 
        [&>*]:max-w-[200px] [&>*]:whitespace-nowrap [&>*]:overflow-hidden [&>*]:text-ellipsis">
          <h6 class="pb-1.5 text-xs opacity-50">Science Fiction</h6>
          <h3 class="pb-0.5 text-sm font-semibold">Star Wars</h3>
          <p class="text-xs opacity-70">In a galaxy far, far away, there's a hero who's about to rise</p>
          <img src="@/src/assets/icon/more_square.svg" class="hidden absolute right-2 top-2 w-5 rounded-full group-hover:block hover:bg-[#0001] active:bg-theme-darklight" alt="more">
        </button>
        <button @click="$router.push('/demo/a4148169-6e94-4f89-b500-6632e1ac7aef')" class="group relative flex flex-col justify-center w-full h-20 px-10 border-b border-b-theme-gridlight first:bg-theme-pale hover:bg-theme-light last:border-0 
        [&>*]:max-w-[200px] [&>*]:whitespace-nowrap [&>*]:overflow-hidden [&>*]:text-ellipsis">
          <h6 class="pb-1.5 text-xs opacity-50">Advanture</h6>
          <h3 class="pb-0.5 text-sm font-semibold">The Lord of The Rings</h3>
          <p class="text-xs opacity-70">In the realm of Middle-earth, where elves, dwarves, and humans coexist, a tale of epic proportions unfolds</p>
          <img src="@/src/assets/icon/more_square.svg" class="hidden absolute right-2 top-2 w-5 rounded-full group-hover:block hover:bg-[#0001] active:bg-theme-darklight" alt="more">
        </button>
        <button @click="$router.push('/demo/03ec8f1b-e679-4dd0-90d8-c86b92acb33e')" class="group relative flex flex-col justify-center w-full h-20 px-10 border-b border-b-theme-gridlight first:bg-theme-pale hover:bg-theme-light last:border-0 
        [&>*]:max-w-[200px] [&>*]:whitespace-nowrap [&>*]:overflow-hidden [&>*]:text-ellipsis">
          <h6 class="pb-1.5 text-xs opacity-50">Mystery</h6>
          <h3 class="pb-0.5 text-sm font-semibold">Stranger Things</h3>
          <p class="text-xs opacity-70">In the small town of Hawkins, something strange is happening</p>
          <img src="@/src/assets/icon/more_square.svg" class="hidden absolute right-2 top-2 w-5 rounded-full group-hover:block hover:bg-[#0001] active:bg-theme-darklight" alt="more">
        </button>
      </div>
      <button class="text-theme-dark text-xs text-center font-semibold hover:underline">Show More</button>
    </section>
    <section id="internal-link" class="flex flex-wrap justify-center mx-7 pt-7 pb-3 text-xs border-b border-theme-darklight
    [&>a]:opacity-75 [&>a]:text-theme-black [&>a]:mx-1.5 [&>a]:my-0.5 hover:[&>a]:underline hover:[&>a]:opacity-100">
      <router-link to="/about">About</router-link>
      <router-link to="/privacy-policy">Privacy Policy</router-link>
      <router-link to="/terms-of-use">Terms of Use</router-link>
      <router-link to="/contact-us">Contact Us</router-link>
      <router-link to="/feedback">Feedback</router-link>
    </section>
    <section id="external-link" class="flex justify-evenly p-4 [&>*>img]:w-6">
      <a href="https://github.com/TaylonChan/storompt" target="_blank">
        <img src="@/src/assets/logo/github.svg" alt="github logo">
      </a>
      <div class="-mx-7 my-1 border"></div>
      <a href="" target="_blank">
        <img src="@/src/assets/logo/dev.svg" alt="dev logo">
      </a>
      <div class="-mx-7 my-1 border"></div>
      <a href="" target="_blank">
        <img src="@/src/assets/logo/threads.svg" alt="threads logo">
      </a>
    </section>
    <section id="profile-panel" class="fixed bottom-0 w-[--menu] h-[--header] border-t border-r bg-white z-10">
      <div class="flex justify-between items-center h-full w-full px-7">
        <button class="-mr-4">
          <img src="@/src/assets/avatar/Shape=10, Color=Pedigrey.svg" class="w-10" alt="">
        </button>
        <div class="">
          <h3 class="text-sm font-semibold">Taylon Chan</h3>
          <h5 class="text-xs opacity-75">Free Plan - <span class="text-theme-dark font-semibold">Upgrade</span></h5>
        </div>
        <button class="">
          <img src="@/src/assets/icon/logout.svg" class="w-6" alt="">
        </button>
      </div>
    </section>
  </menu>
</template>

<script>
import { useStatusStore } from '@/src/store/useStatusStore'

export default {
    name: 'Sidemenu',
    components: {
    },
    props: [
      'openSidemenu'
    ],
    data() {
      return {
        store: useStatusStore(),
      }
    },
    computed: {
    },
    created() {
      this.$watch(
        () => this.$route.params,
        (toParams, previousParams) => {
          window.location.reload()
        }
      )
    },
    methods: {
      closeSidemenu() {
        this.store.sidemenuStatus = false
      }
    }
}
</script>

<style>

</style>