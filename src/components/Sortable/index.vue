<template>
  <div class="sort-component">
    <ul
      v-sortable="options"
      class="list-group"
    >
      <li
        v-for="i in items"
        :key="i.id"
        class="list-group-item"
      >
        <div class="sort-field">
          ID: {{ i.id }} <i class="ep-sortable-handle"></i>
        </div>
      </li>
    </ul>
    {{ items }}
  </div>
</template>

<script>
import SortableJs from 'sortablejs';

export default {
  name: 'SortComponent',
  directives: {
    sortable: {
      inserted: (el, binding) => {
        new SortableJs(el, binding.value || {})
      }
    }
  },
  data() {
    return {
      items: [{id: 1},{id: 2},{id: 3},{id: 4},{id: 5}],
      options: {
        animation: 150,
        forceFallback: true,
        handle: '.ep-sortable-handle',
        ghostClass: 'ep-sortable-ghost',
        dragClass: 'ep-sortable-drag',
        onEnd: this.reOrder
      }
    }
  },
  methods: {
    reOrder({oldIndex, newIndex}) {
      const movedItem = this.items.splice(oldIndex, 1)[0]
      this.items.splice(newIndex, 0, movedItem)
    }
  }
}
</script>

<style lang="scss" src="./index.scss" />

