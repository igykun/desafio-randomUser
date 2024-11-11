<script>
import Mensajes from './components/Mensajes.vue';
export default {
    name: "App",
    components: {
      Mensajes,
    },
};
</script>

<template>
    <div class="container">
      <Mensajes />
    </div>
</template>

<style scoped>
.container {
  max-width: 1280px;
  margin: auto;
}
</style>