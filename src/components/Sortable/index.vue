<template>
  <div class="sortable">
    <ul
      v-sortable="options"
      class="sortable__group"
    >
      <li
        v-for="i in items"
        :key="i.id"
        class="sortable__item"
      >
        <div class="sortable__content">
          <span class="sortable__value">
            {{ i.name }}
          </span>
          <span class="sortable__handle">
            Drag
          </span>
        </div>
      </li>
    </ul>
    <h2>Result</h2>
    <div class="sortable__result">
      {{ items }}
    </div>
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
      items: [
        {
          id: 1,
          name: 'Foobar'
        },
        {
          id: 2,
          name: 'Foo'
        },
        {
          id: 3,
          name: 'Bar'
        },
        {
          id: 4,
          name: 'Baz'
        },
        {
          id: 5,
          name: 'Qux'
        }
      ],
      options: {
        animation: 150,
        forceFallback: true,
        handle: '.sortable__handle',
        ghostClass: 'sortable__ghost',
        dragClass: 'sortable__drag',
        onEnd: this.reOrder
      }
    }
  },
  methods: {
    reOrder({ oldIndex, newIndex }) {
      const movedItem = this.items.splice(oldIndex, 1)[0];
      this.items.splice(newIndex, 0, movedItem);
    }
  }
}
</script>

<style lang="scss" src="./index.scss" />

