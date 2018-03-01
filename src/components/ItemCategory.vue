<template>
  <div class="field">
    <label class="label is-medium">Category:</label>
    <div class="control">
      <div class="select is-medium">
        <select v-model="item.category">
          <option v-for="category in categories" :key="category">{{ category }}</option>
        </select>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    categories: Array,
    item: Object
  },
  data () {
    return {}
  }
}
</script>

<style lang="scss">
.select {
  width: 100%;
}

select {
  width: 100%;
}
</style>
