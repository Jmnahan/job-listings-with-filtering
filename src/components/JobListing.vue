<template>
  <!-- <input type="text" v-model="search" /> -->
  <div v-if="show">
    <input v-model="inputValue" />
  </div>
  <section v-for="data in filteredData" :key="data.id" class="border border-danger d-flex w-75">
    <img :src="data.logo" alt="SVG logo" class="h-50 my-auto" />
    <article class="mx-2">
      <div class="d-flex">
        <p class="mx-2">{{ data.company }}</p>
        <p v-if="data.new == true" class="mx-2">New!</p>
        <p v-if="data.featured == true">Featured!</p>
      </div>
      <h5>{{ data.position }}</h5>
      <ul class="list-unstyled d-flex">
        <li>{{ data.postedAt }}</li>
        <span class="mx-2">·</span>
        <li>{{ data.contract }}</li>
        <span class="mx-2">·</span>
        <li>{{ data.location }}</li>
      </ul>
    </article>
    <aside class="ms-auto my-auto">
      <button class="mx-2">{{ data.role }}</button>
      <button>{{ data.level }}</button>
      <button v-for="languages in data.languages" :key="languages" class="mx-2">
        {{ languages }}
      </button>
    </aside>
  </section>

  <template v-for="dataJson in dataJson" :key="dataJson.id">
    <section v-if="search === ''" class="border border-danger d-flex w-75">
      <img :src="dataJson.logo" alt="SVG logo" class="h-50 my-auto" />
      <article class="mx-2">
        <div class="d-flex">
          <p class="mx-2">{{ dataJson.company }}</p>
          <p v-if="dataJson.new == true" class="mx-2">New!</p>
          <p v-if="dataJson.featured == true">Featured!</p>
        </div>
        <h5>{{ dataJson.position }}</h5>
        <ul class="list-unstyled d-flex">
          <li>{{ dataJson.postedAt }}</li>
          <span class="mx-2">·</span>
          <li>{{ dataJson.contract }}</li>
          <span class="mx-2">·</span>
          <li>{{ dataJson.location }}</li>
        </ul>
      </article>
      <aside class="ms-auto my-auto d-flex">
        <button class="mx-2" @click="showInput(dataJson.role)">{{ dataJson.role }}</button>
        <button class="mx-2" @click="showInput(dataJson.level)">{{ dataJson.level }}</button>
        <ul v-for="language in dataJson.languages" :key="language">
          <button @click="showInput(language)">
            {{ language }}
          </button>
        </ul>
      </aside>
    </section>
  </template>
</template>
<script>
export default {
  data() {
    return {
      search: '',
      dataJson: [],
      buttons: [],
      show: false,
      inputValue: ''
    }
  },
  mounted() {
    fetch('./json/data.json')
      .then((response) => response.json())
      .then((data) => {
        this.dataJson = data
      })
      .catch((error) => console.error(error))
  },
  computed: {
    filteredData() {
      return this.dataJson.filter((data) => data.languages.includes(this.search))
    }
  },
  methods: {
    showInput(value) {
      this.show = true
      this.inputValue = value
    }
  }
}
</script>
