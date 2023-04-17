<script>
      import json from '../json/data.json'
      export default{
          data(){
              return{
                  myJson: json
              }
          }
      }
</script>

<template>
  <h1>JOBLISTING</h1>
  <p>data{{ myJson[1] }}</p>
</template>