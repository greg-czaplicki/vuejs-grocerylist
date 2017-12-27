<template>
  <div id="app">
    <h1>Grocery List</h1>

    <div class="field">
      <label class="label">Item Name:</label>
      <div class="control">
        <input v-model="itemName" class="input" type="text" placeholder="Parsley">
      </div>
    </div>
    <div class="field">
      <label class="label">Category:</label>
      <div class="control">
        <div class="select">
          <select v-model="itemCategory">
            <option v-for="category in categories">{{ category }}</option>
          </select>
        </div>
      </div>
    </div>
    <div class="field">
      <label class="label">Quantity</label>
      <div class="field is-grouped">
        <div class="control">
          <h2>{{ quantity }}</h2>
        </div>
        <div class="control">
          <button v-on:click="increaseQuantity" class="button is-primary">+</button>
          </div>
        <div class="control">
          <button v-on:click="decreaseQuantity" v-if="quantity > 1" class="button is-danger">-</button>
          </div>
      </div>
    </div>
    <div class="field is-grouped">
    <div class="control">
      <button v-if="itemName" class="button is-link">Submit</button>
    </div>
  </div>

  <h1 v-if="sorted_produce.length > 0">Produce</h1>
  <p v-for="x in sorted_produce">{{ x.name }}</p>

  </div>
</template>

<script>
export default {
  data () {
    return {
      categories: [
        'Produce',
        'Deli',
        'Breads/Pasta',
        'Snacks',
        'Baking/Condiments',
        'Canned Goods',
        'Breakfast',
        'Beverages',
        'Meat/Seafood',
        'Dairy',
        'Cleaning Products',
        'Paper/Plastics',
        'Toiletries',
        'Frozen Foods',
        'Miscellaneous'
      ],
      quantity: 1,
      itemName: '',
      itemCategory: 'Produce',
      groceryList: [{ name: 'Parsley', cat: 'Produce', quant: 2 }, { name: 'Apple', cat: 'Produce', quant: 1 }]
    }
  },
  methods: {
    increaseQuantity: function () {
      this.quantity += 1
    },
    decreaseQuantity: function () {
      this.quantity -= 1
    }
  },
  computed: {
    sorted_produce () {
      const result = this.groceryList.filter(ct => ct.cat === 'Produce')
      return result.sort((a, b) => a.name > b.name)
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px auto;
  max-width: 50%;
}

h1,
h2 {
  font-weight: normal;
}

h1 {
  font-size: 3rem;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
