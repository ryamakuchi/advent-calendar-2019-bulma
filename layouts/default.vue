<template>
  <div>
    <nav
      class="bd-navbar navbar has-shadow is-spaced"
      role="navigation"
      aria-label="main navigation"
    >
      <div class="navbar-brand">
        <logo class="level-item" />

        <a
          href="https://qiita.com/advent-calendar/2019/nuxt-js"
          target="_blank"
          rel="noopener noreferrer"
          class="level-item has-text-weight-bold has-text-primary"
        >
          Nuxt.js Advent Calendar 2019 for Qiita
        </a>
      </div>

      <div class="navbar-menu">
        <div class="navbar-end">
          <a
            href="https://bulma.io/"
            target="_blank"
            rel="noopener noreferrer"
            class="navbar-item button is-primary"
          >
            Made with Bulma
          </a>
        </div>
      </div>
    </nav>

    <nuxt />
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  }
}
</script>

<style>
html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}
</style>
