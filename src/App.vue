<template>
  <div id="app">
    <HomeView />
    <!-- <Header />
    <RankingView />
    <SchoolList /> -->
  </div>
</template>

<script>
import HomeView from './components/HomeView.vue'

export default {
  name: "App",
  components: {
    HomeView
    // Header,
    // RankingView,
    // SchoolList,
  },
};
</script>

<style>
/* Add your global styles here */
</style>
