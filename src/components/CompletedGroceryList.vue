<template>
  <div>
    <h2 id="catTitleCompleted" v-if="items.length > 0">{{ items[0].category }}</h2>
    <ul v-for="item in items">
      <li v-on:click="toggleCompleted(item, item.isCompleted)" :class="{completed: item.isCompleted}" class="is-capitalized">
        • {{ item.name }}<span v-if="item.quantity > 1"> - {{ item.quantity }}</span></li>
    </ul>
  </div>
</template>


<script>
export default {
  props: {
    items: Array,
    toggleCompleted: Function
  },
  data () {
    return {}
  }
}
</script>

<style lang="scss">
.completed {
  text-decoration-line: line-through;
  -webkit-text-decoration-line: line-through;
  font-style: italic;
  color: rgb(182, 182, 182);
}

li {
  font-size: 25px;
}

#catTitleCompleted {
  font-size: 30px;
  color: rgb(182, 182, 182);
  text-decoration-line: underline;
  -webkit-text-decoration-line: underline;
}
</style>
