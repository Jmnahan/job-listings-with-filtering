<script>
  import json from '../json/data.json'
  export default{
    data(){
      return{
        search: '',
        dataJson: json
      }
    },
    computed: {
      filteredData() {
        return this.dataJson.filter(data => data.languages.includes(this.search))
      }
    }
  }
</script>

<template>
  <h1>JOBLISTING</h1>
  <input type="text" v-model="search"/>
  <div v-for="data in filteredData" :key="data.id">
    <ul class="list-unstyled">
      <li class="border border-danger mb-2">
        <div class="d-flex">
          <img :src="data.logo" alt="SVG logo">
          <p>{{ data.company }}</p>
          <p v-if="data.new == true">New!</p>
          <p v-if="data.featured == true">Featured!</p>
        </div>
        <p>{{ data.position }}</p>
        <div>{{ data.postedAt }} · {{ data.contract }} · {{ data.location }}</div>
        <span v-for="languages in data.languages" :key="languages" class="mx-2">
          {{ languages }}
        </span>
      </li>
    </ul>  
  </div>

  <ul v-if="search === ''" class="list-unstyled">
    <li v-for="dataJson in dataJson" :key="dataJson.id" class="border border-danger mb-2">
      <div class="d-flex">
        <img :src="dataJson.logo" alt="SVG logo">
        <p>{{ dataJson.company }}</p>
        <p v-if="dataJson.new == true">New!</p>
        <p v-if="dataJson.featured == true">Featured!</p>
      </div>
        <p>{{ dataJson.position }}</p>
      <div>{{ dataJson.postedAt }} · {{ dataJson.contract }} · {{ dataJson.location }}</div>
      <span v-for="languages in dataJson.languages" :key="languages" class="mx-2">
        {{ languages }}
      </span>
    </li>
  </ul>
</template>