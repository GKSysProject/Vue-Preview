<template>
  <div id="app">
    <Header />
    <Main />
    <SchoolList />
  </div>
</template>

<script>
import Header from "./components/AppHeader.vue";
import Main from "./components/AppMain.vue";
import SchoolList from "./components/SchoolList.vue";

export default {
  name: "App",
  components: {
    Header,
    Main,
    SchoolList,
  },
};
</script>

<style>
/* Add your global styles here */
</style>
