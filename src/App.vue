<template>
  <div id="app">
    <router-view />
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>
<style>
  .main-body{
    margin: 15px;
    height: calc(100vh - 80px);
    background-color: #ffffff;
    overflow-y: auto;
    border-radius: 2px;
  }
  .container{
    margin: 15px;
  }
  .page{
    margin: 10px 0;
    text-align: right;
  }
  .form-container{
    width: 65%;
    margin: auto;
  }
</style>
