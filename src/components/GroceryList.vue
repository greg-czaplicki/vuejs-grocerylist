<template>
  <div>
    <h2 id="catTitle" v-if="items.length > 0">{{ items[0].category }}</h2>
    <ul v-for="item in items" :key="item+1">
      <li v-on:click="toggleCompleted(item, item.isCompleted)" :class="{completed: item.isCompleted}" class="is-capitalized">
       <span style="color: #00c6a7">•</span> {{ item.name }}<span v-if="item.quantity > 1"> - {{ item.quantity }}</span></li>
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

#catTitle {
  font-size: 30px;
  color: #00c6a7;
  text-decoration-line: underline;
  -webkit-text-decoration-line: underline;
}
</style>
