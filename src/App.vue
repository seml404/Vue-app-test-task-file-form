<template>
  <div class="container">
    <h2>File uploading form</h2>
    <uploading-section />
  </div>
</template>

<script>
import UploadingSection from "./components/UploadingSection.vue";
export default {
  name: "App",
  components: { UploadingSection },
};
</script>

<style>
button {
  border: none;
  border-radius: 10px;
  padding: 5px;
  cursor: pointer;
}

.container {
  width: 600px;
  height: 600px;
  margin: 0 auto;
  border-radius: 10%;
  border: 1px solid grey;
  box-shadow: 2px 2px 2px 2px grey;
  padding: 20px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
