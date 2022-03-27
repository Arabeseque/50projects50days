/* eslint-disable @typescript-eslint/ban-ts-comment */
<script setup lang="ts">
import TypeIt from 'typeit'

const block = ref<HTMLPreElement>()

onMounted(() => {
  // eslint-disable-next-line @typescript-eslint/ban-ts-comment
  // @ts-expect-error
  new TypeIt(block.value, {
    speed: 50,
    startDelay: 900,
  })
    .type('the mot versti', { delay: 100 })
    .move(-8, { delay: 100 })
    .type('s', { delay: 400 })
    .move(null, { to: 'START', instant: true, delay: 300 })
    .move(1, { delay: 200 })
    .delete(1)
    .type('T', { delay: 225 })
    .pause(200)
    .move(2, { instant: true })
    .pause(200)
    .move(5, { instant: true })
    .move(5, { delay: 200 })
    .type('a', { delay: 350 })
    .move(null, { to: 'END' })
    .type('le', { delay: 350 })
    .break()
    .type('typing utlity')
    .move(-4, { delay: 150 })
    .type('i')
    .move(null, { to: 'END' })
    .type(' on the ', { delay: 250 })
    .break()
    .type(' <span class="place">internet</span>', { delay: 400 })

    .delete('.place', { delay: 800, instant: true })
    .type('<em><strong class="font-semibold">planet.</strong></em>', { speed: 100 })
    .go()
})
</script>

<template>
  <div outline-none>
    <nav sticky top-0 h-24 flex justify-between px-5 py-5 z-20 w-full bg-white>
      <span class="flex-initial text-5xl font-extralight logo">
        <a href="/" font-extralight text-gray-700>Expired</a>
      </span>
      <div
        class="
        flex
        justify-end
        relative
        top-0
        left-[0]
        h-full
        w-full
        bg-white
        translate-left
        lg:translate-none
        overflow-scroll
        lg:overflow-visible
        pt-8
        lg:p-0
        mr-6"
      >
        <ul class=" mx-auto lg:-mx-3 lg:mt-0  lg:flex mb-8 lg:mb-0 fw200 text-xl pt-3.25">
          <li class="siteNavListItem flex px-5 flex-col lg:flex-row ld:items-center font-extralight mb-5 lg:mb-0 relative">
            <a href="" class="siteNavLink">Pricing</a>
          </li>
          <li class="siteNavListItem flex px-5 flex-col lg:flex-row ld:items-center font-extralight mb-5 lg:mb-0 relative">
            <a href="" class="siteNavLink">Demos</a>
          </li>
          <li class="siteNavListItem flex px-5 flex-col lg:flex-row ld:items-center font-extralight mb-5 lg:mb-0 relative">
            <a href="" class="siteNavLink">Flavors</a>
          </li>
          <li class="siteNavListItem flex px-5 flex-col lg:flex-row ld:items-center font-extralight mb-5 lg:mb-0 relative">
            <a href="" class="siteNavLink">Documentation</a>
          </li>
          <li class="siteNavListItem" px-5>
            <button flex items-center>
              <div i-ri:search-line />
            </button>
          </li>
          <div class="siteNavListItem justify-center siteNavListItem md:mt--2.5">
            <el-button color="#626aef" style="color: #ffffff" py-5 px-3 text-xl>
              Purchase a License
            </el-button>
          </div>
        </ul>
      </div>
    </nav>
    <div relative max-w-3xl mx-auto pt-0 md:pt-20 px-3 z-10>
      <pre
        ref="block"
        class="hero-animation"
        leading-tight
        text-center
        mt-12
        md:mt-0
        mb-20
        text-4xl
        md:text-6xl
        font-extralight
        max-w-xl
        mx-auto
        font-sans
        style="opacity: 1;"
      />
    </div>
  </div>
</template>

<style>
* {
  font-family: Heebo,sans-serif;
}
.hero-animation .place {
  font-weight: lighter;
}

.button {

    --tw-ring-opacity: 1;
    --tw-ring-color: rgb(147 51 234/var(--tw-ring-opacity));
    background-image: linear-gradient(to bottom right,#a855f7,#9333ea);
    border-radius: .25rem;

    color: rgb(255 255 255/var(--tw-text-opacity));
    cursor: pointer;
    font-size: 1.125rem;
}

.button.slim {
    --tw-ring-offset-shadow: var(--tw-ring-inset) 0 0 0 var(--tw-ring-offset-width) var(--tw-ring-offset-color);
    --tw-ring-shadow: var(--tw-ring-inset) 0 0 0 calc(2px + var(--tw-ring-offset-width)) var(--tw-ring-color);
    font-weight: 300;
    padding: .25rem .75rem;
}
.button, .button.slim {
    box-shadow: var(--tw-ring-offset-shadow),var(--tw-ring-shadow),var(--tw-shadow,0 0 #0000);
}
</style>
