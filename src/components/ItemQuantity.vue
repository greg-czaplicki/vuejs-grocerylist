<template>
<div>
  <div class="field">
    <label class="label is-medium">Quantity</label>
    <div class="field is-grouped">
      
      <div class="control">
        <button v-on:click.prevent="increaseQuantity" class="button is-primary quantity"><span class="buttonplusminus">+</span></button>
      </div>
      <div class="control">
        <h2 id="quantNumber">{{ item.quantity }}</h2>
      </div>
      <div class="control">
        <button v-on:click.prevent="decreaseQuantity" v-if="item.quantity > 1" class="button is-danger quantity"><span class="buttonplusminus">-</span></button>
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
  props: {
    item: Object
  },
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
.quantity {
  width: 143px;
  height: 40px;
}

#quantNumber {
  font-size: 22px;
  margin: 5px 26px;
}

.buttonplusminus {
  font-size: 30px;
  line-height: 0;
}

button {
  align-content: center;
}

.is-link {
  margin: 15px 0;
  width: 100%;
  height: 45px;
  font-size: 20px;
}
</style>
