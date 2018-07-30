<template>
  <section>
    <h1 class="page-title">Witness me</h1>
    <div class="links">
      <a class="link--linkedin" href="https://www.linkedin.com/in/iamdanlevine/" >
        <img src="@/assets/icons/linkedin.svg" alt="Linkedin icon"/>
      </a>
      <a class="link--github" href="https://github.com/danlevine" >
        <img src="@/assets/icons/github.svg" alt="Github icon"/>
      </a>
    </div>
  </section>
</template>

<style scoped>
section {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 80px 20px;
}

.links {
  display: flex;
  flex-direction: column;
}

a {
  border: 8px solid transparent;
  border-radius: 50px;
}

a.link--linkedin:hover,
a.link--linkedin:focus {
  border-color: #0077B5;
  outline: none;
}

a.link--github:hover,
a.link--github:focus {
  border-color: #4078c0;
  outline: none;
}

img {
  max-width: 100%;
}

@media (min-width: 500px) {
  .links {
    flex-direction: row;
  }

  a {
    margin: 0 20px;
  }
}
</style>
