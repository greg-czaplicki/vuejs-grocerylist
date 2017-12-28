<template>
  <div id="app">
    <h1 id="title">Grocery List</h1>

    <form v-on:submit.prevent="addItem">
      <div class="field">
        <label class="label">Item Name:</label>
        <div class="control">
          <input v-model="item.name" class="input" type="text" placeholder="Parsley">
        </div>
      </div>

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
  </form>

    <Item v-if="sorted_produce" :toggleCompleted="toggleCompleted" :items="sorted_produce"></Item>
    <!-- <Item v-if="sorted_dairy" v-bind:items="sorted_dairy"></Item>  -->

</div>
</template>

<script>
import Firebase from 'firebase'
import Item from './components/Item'

const config = {
  apiKey: 'AIzaSyAifz-Sm1RBPfnq-xLAeWT5H5XrBuZCW0A',
  authDomain: 'vuejsgrocery.firebaseapp.com',
  databaseURL: 'https://vuejsgrocery.firebaseio.com',
  projectId: 'vuejsgrocery',
  storageBucket: 'vuejsgrocery.appspot.com',
  messagingSenderId: '986128402964'
}
const app = Firebase.initializeApp(config)
const db = app.database()
const itemsRef = db.ref('items')
const produceRef = db.ref('produce')

export default {
  components: {
    Item: Item
  },
  firebase: {
    items: itemsRef,
    produce: produceRef
  },
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
      myName: 'Greg',
      item: {
        quantity: 1,
        name: '',
        category: 'Produce',
        isCompleted: false
      }
    }
  },
  methods: {
    increaseQuantity: function () {
      this.item.quantity += 1
    },
    decreaseQuantity: function () {
      this.item.quantity -= 1
    },
    addItem: function () {
      if (this.item.category === 'Produce') {
        produceRef.push(this.item)
      } else {
        itemsRef.push(this.item)
      }
      this.item.name = ''
      this.item.category = 'Produce'
      this.item.quantity = 1
    },
    toggleCompleted: function (item, isCompleted) {
      produceRef.child(item['.key']).child('isCompleted').set(!isCompleted)
    }
  },
  computed: {
    sorted_produce: function () {
      return this.produce.sort((a, b) => a.name > b.name)
    },
    sorted_dairy: function () {
      return this.items.sort((a, b) => a.name > b.name)
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

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

#title {
  text-align: center;
}

.quantity {
  width: 40px;
  height: 40px;
}
</style>
