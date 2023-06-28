<template lang="">
  <div class="hero">
    <div class="hero__inner">
      <!-- TODO: Add typewriter effect? -->
      <h1 class="h1">What are you looking for?</h1>
      <div class="input__wrapper">
        <input class="input__field" type="text" placeholder="Brian De Palma" />
        <button><box-icon name="search" color="white"></box-icon></button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import 'boxicons'
export default {}
</script>

<style lang="scss">
.hero {
  @apply mt-32;
  &__inner {
    @apply flex flex-col items-center;
    h1 {
      @apply text-4xl;
    }
    .input {
      &__wrapper {
        @apply relative;
        width: 60%;
        box-icon {
          @apply absolute right-6 transition;
          top: 55%;
          opacity: 0.3;
        }
      }
      &__field {
        @apply mt-8 bg-slate-600 rounded-full px-8 text-lg w-full transition;
        height: 3rem;
        &:focus {
          outline: 1px solid rgba(white, $alpha: 0.5);
          & + button {
            box-icon {
              opacity: 0.6;
            }
          }
        }
      }
    }
  }
}
</style>
