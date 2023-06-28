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
          <img :src="mediaURL + item.poster_path" :alt="item.name" />
        </div>
        <div class="card__info">
          <h3>{{ item.name }}</h3>
          <span>{{ item.first_air_date }}</span>
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
  name: string
  first_air_date: string
  overview: string
  poster_path: string
}
export default {
  data() {
    return {
      contentType: 'tv',
      categories: ['popular', 'airing today', 'on the air', 'top rated'],
      currentCat: 'popular',
      originCountry: ['US'], // add more
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
        new RegExp(' ', 'g'),
        '_'
      )}/?with_origin_country=${this.originCountry}&page=1&api_key=${TMDB_API_KEY}`
      const response = await axios.get(url)
      console.log(response.data.results)
      this.itemList = response.data.results
    }
  }
}
</script>

<style lang="scss"></style>
