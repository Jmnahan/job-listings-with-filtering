<script>
      import json from '../json/data.json'
      export default{
          data(){
              return{
                  dataJson: json
              }
          }
      }
</script>

<template>
  <h1>JOBLISTING</h1>
  <ul class="list-unstyled">
    <li v-for="dataJson in dataJson" :key="dataJson.id" class="border border-danger mb-2">
      <div class="d-flex">
        <img :src="dataJson.logo" alt="SVG logo">
        {{ dataJson.company }}
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