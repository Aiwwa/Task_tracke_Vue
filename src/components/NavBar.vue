<template>
  <nav class="navbar">
    <router-link :to="{name: 'Home'}">Projects</router-link>
    <router-link :to="{name: 'AddProject'}">Add a new project</router-link>
  </nav>
</template>

<script>
export default {

}
</script>

<style>
  .navbar {
    text-align: center;
    margin: 40px auto;
  }
  .navbar a{
    display: inline-block;
    text-decoration: none;
    margin: 0 10px;
    color: #999;
    font-size: 18px;
  }
  a.router-link-active {
    border-bottom: 2px solid rgb(191, 255, 0);
    padding-bottom: 4px;
  }
</style>