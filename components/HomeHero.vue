<template>
  <section class="hero">
    <small>Hi, I'm</small>
    <h1 class="page-title">Daniel Levine</h1>
    <div>and I build user interfaces for the web</div>
    <div class="subtext">(for example, I built this simple/minimal static site using VueJS/Nuxt. Expect more to come!)</div>
  </section>
</template>

<style scoped>
.hero {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 40px;
  text-align: center;
}

@media (min-width: 500px) {
  .hero {
    padding: 80px;
  } 
}

small {
  font-size: 12px;
}

.page-title {
  font-size: 70px;
}

.subtext {
  font-size:10px;
  margin-top: 80px;
}
</style>
