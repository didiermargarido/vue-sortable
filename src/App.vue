<template>
  <div
    id="app"
    class="app"
  >
    <h1>VueJs Sortable</h1>
    <a
      href="https://github.com/didiermargarido/vue-sortable"
      target="_blank"
    >
      View on GitHub
    </a> |
    <a
      href="https://github.com/SortableJS/Sortable"
      target="_blank"
    >
      View SortableJs library
    </a>
    <Sortable />
  </div>
</template>

<script>
import Sortable from '@/components/Sortable';

export default {
  name: 'App',
  components: {
    Sortable
  }
};
</script>

<style lang="scss" src="./app.scss" />
