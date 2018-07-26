<template>
  <section class="container">
    <app-header />
    <links />
  </section>
</template>

<script>
import AppHeader from '~/components/AppHeader.vue'
import Links from '~/components/Links.vue'

export default {
  components: {
    AppHeader,
    Links
  }
}
</script>
