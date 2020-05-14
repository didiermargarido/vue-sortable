<template>
  <div
    id="app"
    class="app"
  >
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
