<script setup lang="ts">
import { onErrorCaptured, ref } from 'vue'
import { RouterLink, RouterView } from 'vue-router/auto'
const menuIsOpen = ref(false)

onErrorCaptured((err, instance, info) => {
  console.error('erreur : ', err, '\ninfo : ', info, '\ncomposant : ', instance)
  return true
})
</script>

<template>
  <header>
    <button
  aria-controls="mainNav"
  aria-expanded="true"
  class="rounded-full border-2 border-red-600 bg-red-300 px-2"
>
  menu
</button>
<!-- nav#mainNav>ul>li*3>a[href="#"]{item $} -->
<nav id="mainNav" v-show="menuIsOpen">
  <ul>
        <li>
          <RouterLink to="/" class="text-red-500 underline"> Accueil </RouterLink>
        </li>
        <li>
          <RouterLink to="accordeon" class="text-red-500 underline"> Accordeon </RouterLink>
        </li>
      </ul>
</nav>
  </header>
  <RouterView v-slot="{ Component }">
    <Suspense>
      <component :is="Component" />
    </Suspense>
  </RouterView>
</template>
