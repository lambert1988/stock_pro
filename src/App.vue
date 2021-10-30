<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
* {
  margin: 0px;
  padding: 0px;
  color:#ccc !important;
  background-color: #000 !important;
}
html, body, #app{ 
  height: 100%; 
  margin: 0; 
  padding: 0;
  background-color: #000;
}
</style>
