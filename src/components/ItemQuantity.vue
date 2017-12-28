<template>
<div>
  <div class="field">
    <label class="label">Quantity</label>
    <div class="field is-grouped">
      <div class="control">
        <h2>{{ item.quantity }}</h2>
      </div>
      <div class="control">
        <button v-on:click.prevent="increaseQuantity" class="button is-primary quantity">+</button>
        </div>
      <div class="control">
        <button v-on:click.prevent="decreaseQuantity" v-if="item.quantity > 1" class="button is-danger quantity">-</button>
      </div>
    </div>
  </div>
  <div class="field">
    <div class="control">
      <input v-if="item.name" type="submit" value="Add Item" class="button is-link">
    </div>
  </div>
</div>
</template>

<script>
export default {
  props: ['item'],
  data () {
    return {}
  },
  methods: {
    increaseQuantity: function () {
      this.item.quantity += 1
    },
    decreaseQuantity: function () {
      this.item.quantity -= 1
    }
  }
}
</script>

<style lang="scss">

</style>
