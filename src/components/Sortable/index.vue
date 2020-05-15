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
            <span data-rank>{{ i.rank }}</span>
            ) {{ i.name }}
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
          rank: 1,
          name: 'Foobar'
        },
        {
          id: 2,
          rank: 2,
          name: 'Foo'
        },
        {
          id: 3,
          rank: 3,
          name: 'Bar'
        },
        {
          id: 4,
          rank: 4,
          name: 'Baz'
        },
        {
          id: 5,
          rank: 5,
          name: 'Qux'
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
        onEnd: this.onEnd
      }
    }
  },
  methods: {
    onChange({ newIndex }) {
      document.querySelector(`.${this.options.fallbackClass} [data-rank]`).innerHTML = ++newIndex;
    },
    onEnd({ oldIndex, newIndex }) {
      const movedItem = this.items.splice(oldIndex, 1)[0];
      this.items.splice(newIndex, 0, movedItem);
      this.items.forEach((key, i) => {
        this.items[i].rank = ++i;
      });
    }
  }
}
</script>

<style lang="scss" src="./index.scss" />

