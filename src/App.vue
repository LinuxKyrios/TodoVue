<template>
  <div id="app">
    <h4 class="bg-primary text-white text-center p-2">
      Task List of the user {{name}}
    </h4>
  </div>
</template>

<script>

export default {
  name: 'App',
    data() {
      return {
        name: "Linux Kyrios"
      }
    }
}
</script>

