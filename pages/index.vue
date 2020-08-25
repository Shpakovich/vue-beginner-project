<template>
  <section class="container">
    <AppLogo></AppLogo>
    <h1>My Vue project in progress</h1>
    <nuxt-link to="/counter">
      link counter project
    </nuxt-link>
    <nuxt-link to="/stopwatch">
      link stopwatch project
    </nuxt-link>
  </section>
</template>

<script>
import AppLogo from '../components/AppLogo';

  export default {
    components: {
      AppLogo
    }
  }
</script>

<style>
.container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}

</style>