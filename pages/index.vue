<template>
  <section class="container">
    <app-header />
    <home-hero />
  </section>
</template>

<script>
import AppHeader from '~/components/AppHeader.vue'
import HomeHero from '~/components/HomeHero.vue'

export default {
  components: {
    AppHeader,
    HomeHero
  }
}
</script>
