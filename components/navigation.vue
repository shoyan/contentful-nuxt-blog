<template>
  <nav role="navigation">
    <ul class="navigation">
      <li class="navigationItem">
        <nuxt-link to="/">Home</nuxt-link>
      </li>
      <li class="navigationItem">
        <nuxt-link to="/blog/">Blog</nuxt-link>
      </li>
    </ul>
  </nav>
</template>

<style scoped>
.navigation {
  display: flex;
  justify-content: center;
  list-style: none;
  padding: 0;
  margin: 0;
  height: 20vh;
  max-height: 100px;
  font-size: 1.25em;
}

.navigationItem {
  display: inline-flex;
  align-items: center;
  margin: 0 1em;
}

.navigationItem a {
  color: currentColor;
}
</style>
