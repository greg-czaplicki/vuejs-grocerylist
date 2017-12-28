<template>
  <div class="field">
    <label class="label">Item Name:</label>
      <div class="control">
        <input v-model="item.name" class="input" type="text" placeholder="Parsley">
      </div>
    </div>
</template>

<script>
export default {
  props: ['item'],
  data () {
    return {}
  }
}
</script>

<style lang="scss">

</style>
