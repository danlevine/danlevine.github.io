<template>
  <header>
    <div class="logo">DL</div>
    <ul class="link-list">
      <li
        class="link-item"
        v-for="link in links"
        :key="link.title"
      >
        <nuxt-link :to="link.url" class="link">
          {{ link.title }}
        </nuxt-link>
      </li>
    </ul>
  </header>
</template>

<script>
export default {
  props: {
    currentPage: {
      type: String
    }
  },
  data() {
    return {
      links: [
        {
          title: 'Home',
          url: '/',
        },
        {
          title: 'About',
          url: '/about',
        },
        {
          title: 'Links',
          url: '/links',
        },
      ]
    }
  }
}
</script>

<style>

header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  padding: 40px 40px 0;
}

@media (min-width: 500px) {
  header {
    padding: 40px 80px 0;
  } 
}

.logo {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  font-size: 18px;
  font-weight: 600;
  padding: 4px 16px 18px 6px;
  border-radius: 3px;
  background: #373737;
  color: #f4f4f4;
}

.link-list {
  display: flex;
  list-style: none;
  padding: 0;
}

.link-item {
  margin-left: 15px;
}

@media (min-width: 500px) {
  .link-item {
    margin-left: 40px;
  } 
}

.link {
  text-decoration: none;
  color: #888;
  font-weight: 600;
}

.link:hover,
.link:focus {
  padding-bottom: 10px;
  border-bottom: 5px solid #888;
  outline: none;
}

.link.nuxt-link-exact-active {
  color: #c0b283;
  border-bottom: none;
}
</style>
