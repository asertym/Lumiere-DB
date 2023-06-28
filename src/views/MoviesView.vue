<template>
  <div class="filter-pills">
    <div class="pill-group">
      <div class="pill" v-for="(category, key) in categories" :key="key">
        <input v-model="currentCat" :id="category" :value="category" type="radio" class="pill" />
        <label :for="category">
          {{ category }}
        </label>
      </div>
    </div>
  </div>
  <div class="main-view mt-10">
    <!-- filter section -->
    <div class="side-filter"></div>
    <!-- List section -->
    <div class="item-list">
      <div class="card" v-for="(item, key) in itemList" :key="key">
        <div class="card__img">
          <img :src="mediaURL + item.poster_path" alt="{{ item.title }}" />
        </div>
        <div class="card__info">
          <h3>{{ item.title }}</h3>
          <span>{{ item.release_date }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import axios from 'axios'
const TMDB_API_URL = import.meta.env.VITE_API_URL
const TMDB_API_KEY = import.meta.env.VITE_API_KEY
const TMDB_MEDIA_URL = import.meta.env.VITE_MEDIA_URL

interface ResponseItems {
  id: number
  adult: boolean
  title: string
  release_date: string
  overview: string
  poster_path: string
}
export default {
  data() {
    return {
      contentType: 'movie',
      categories: ['popular', 'upcoming', 'now playing', 'top rated'],
      currentCat: 'popular',
      mediaURL: TMDB_MEDIA_URL,
      itemList: [] as ResponseItems[]
    }
  },
  created() {
    this.fetchData()
  },
  watch: {
    currentCat: 'fetchData'
  },
  methods: {
    async fetchData() {
      const url = `${TMDB_API_URL}/${this.contentType}/${this.currentCat.replace(
        ' ',
        '_'
      )}/?&api_key=${TMDB_API_KEY}`
      const response = await axios.get(url)
      this.itemList = response.data.results
    }
  }
}
</script>

<style lang="scss">
.filter-pills {
}
.pill-group {
  @apply flex justify-center;
  .pill {
    @apply overflow-hidden;
    &:not(:last-of-type) {
      border-right: 1px solid black;
    }
    &:first-of-type {
      border-radius: 10px 0 0 10px;
    }
    &:last-of-type {
      border-radius: 0 10px 10px 0;
    }
    input {
      display: none;
      &:checked + label {
        @apply bg-slate-500;
      }
    }
    label {
      @apply block py-3 px-6 bg-slate-600 capitalize cursor-pointer transition-all;
      &:hover {
        @apply bg-slate-600;
      }
    }
  }
}
.main-view {
  .item-list {
    @apply grid grid-cols-8 gap-4;
    .card {
      @apply flex flex-col rounded-xl overflow-hidden cursor-pointer;
      &:hover {
        .card__img {
          scale: 1.1;
        }
      }
      &__img {
        @apply transition-all;
      }
      &__info {
        @apply p-2 bg-slate-800 h-full flex flex-col justify-between relative z-20;
        span {
          @apply text-sm opacity-50;
        }
      }
    }
  }
}
</style>
