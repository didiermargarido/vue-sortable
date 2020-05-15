<template>
  <div class="sortable">
    <button
      @click="onAdd"
      class="sortable__add"
    >
      Add Item
    </button>
    <ul
      v-sortable="options"
      class="sortable__group"
    >
      <li
        v-for="item in items"
        :key="item.id"
        class="sortable__item"
      >
        <div class="sortable__content">
          <span class="sortable__value">
            <span data-rank>{{ item.rank }}</span>
            ) {{ item.name }}
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
          name: 'Foobar',
          rank: 1
        },
        {
          id: 2,
          name: 'Foo',
          rank: 2
        },
        {
          id: 3,
          name: 'Bar',
          rank: 3
        },
        {
          id: 4,
          name: 'Baz',
          rank: 4
        },
        {
          id: 5,
          name: 'Qux',
          rank: 5
        }
      ],
      options: {
        animation: 150,
        forceFallback: true,
        fallbackClass: 'sortable__clone',
        handle: '.sortable__handle',
        ghostClass: 'sortable__ghost',
        dragClass: 'sortable__drag',
        onChange: this.onChange,
        onEnd: this.onEnd,
        onAdd: this.onAdd
      }
    }
  },
  methods: {
    onChange({ newIndex }) {
      document.querySelector(`.${this.options.fallbackClass} [data-rank]`).innerHTML = ++newIndex;
    },
    onEnd({ oldIndex, newIndex }) {
      const movedItem = this.items.splice(oldIndex, 1)[0]
      this.items.splice(newIndex, 0, movedItem)

      let order = 0;
      this.items.forEach((item) => {
        item.rank = ++order;
      });
    },
    onAdd() {
      const i = this.items[this.items.length - 1].rank + 1;
      this.items.push({
        id: i,
        name: `New Item ${i}`,
        rank: i
      });
    }
  }
}
</script>

<style lang="scss" src="./index.scss" />

