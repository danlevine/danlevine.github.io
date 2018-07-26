<template>
  <section class="container">
    <app-header />
    <about-me />
  </section>
</template>

<script>
import AppHeader from '~/components/AppHeader.vue'
import AboutMe from '~/components/AboutMe.vue'

export default {
  components: {
    AppHeader,
    AboutMe
  }
}
</script>
