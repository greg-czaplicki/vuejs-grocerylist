<template>
  <div class="field">
    <label class="label is-medium">Item Name:</label>
      <div class="control">
        <input v-model="item.name" class="input is-medium" type="text" placeholder="i.e. Parsley">
      </div>
    </div>
</template>

<script>
export default {
  props: {
    item: Object
  },
  data () {
    return {}
  }
}
</script>

<style lang="scss">

</style>
