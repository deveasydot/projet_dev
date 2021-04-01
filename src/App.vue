<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import axios from 'axios'
import Airtable from 'airtable'
export default {
  name: 'App',
  components: {
    HelloWorld
  },
  mounted () {
    axios.get('https://api64.ipify.org?format=json').then((res) => {
      const ip = res.data.ip
      let base = new Airtable({apiKey: 'keyIAotyly94UhxKo'}).base('appGQaW9NULfpN9BR')
      base('Table 1').create([
        {
          "fields": {
            ip: ip
          }
        }
      ], function(err, records) {
        if (err) {
          console.error(err);
          return;
        }
        records.forEach(function (record) {
          console.log(record.getId());
        });
      });
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
