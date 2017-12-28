<template>
  <div class="field">
    <label class="label">Category:</label>
    <div class="control">
      <div class="select">
        <select v-model="item.category">
          <option v-for="category in categories">{{ category }}</option>
        </select>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['categories', 'item'],
  data () {
    return {}
  }
}
</script>

<style lang="scss">

</style>
