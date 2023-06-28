<script setup lang="ts">
import { RouterLink } from 'vue-router'
import IconLogo from './icons/IconLogo.vue'
</script>

<template>
  <div class="header">
    <div class="header__inner">
      <div class="header__logo">
        <router-link to="/">
          <IconLogo />
        </router-link>
      </div>
      <div class="header__navigation">
        <router-link to="/movies">Movies</router-link>
        <router-link to="/shows">TV Shows</router-link>
        <router-link to="/anime">Anime</router-link>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
.header {
  &__inner {
    @apply flex justify-between items-center my-4;
  }
  &__logo {
    width: 200px;
    svg {
      fill: white;
    }
  }
  &__navigation {
    @apply space-x-12;
  }
}
</style>
