<template>
  <div id="app">
    <MainContent />
  </div>
</template>

<script>
import MainContent from "@/components/MainContent";

export default {
  name: "app",
  components: {
    MainContent,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
