<template>
  <div>
    <h1 v-if="items.length > 0">{{ items[0].category }}</h1>
    <ul v-for="item in items">
      <li v-on:click="toggleCompleted(item, item.isCompleted)" :class="{completed: item.isCompleted}">
        {{ item.name }}<span v-if="item.quantity > 1"> - {{ item.quantity }}</span></li>
    </ul>
  </div>
</template>


<script>
export default {
  props: ['items', 'toggleCompleted'],
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
  color: rgb(155, 155, 155);
}
</style>
