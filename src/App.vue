<template>
  <div id="app">

    <h1 id="title">Grocery List</h1>

    <form v-on:submit.prevent="addItem(item)">
      <ItemName v-bind:item="item"></ItemName>
      <ItemCategory v-bind:categories="categories" v-bind:item="item"></ItemCategory>
      <ItemQuantity v-bind:item="item"></ItemQuantity>
    </form>

    <GroceryList :toggleCompleted="toggleCompleted" :items="filterItems('Produce')"></GroceryList>
    <GroceryList :toggleCompleted="toggleCompleted" :items="filterItems('Deli')"></GroceryList>

  </div>
</template>

<script>
import Firebase from 'firebase'
import GroceryList from './components/GroceryList'
import ItemName from './components/ItemName'
import ItemCategory from './components/ItemCategory'
import ItemQuantity from './components/ItemQuantity'

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

export default {
  components: {
    GroceryList: GroceryList,
    ItemName: ItemName,
    ItemCategory: ItemCategory,
    ItemQuantity: ItemQuantity
  },
  firebase: {
    items: itemsRef
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
      item: {
        quantity: 1,
        name: '',
        category: 'Produce',
        isCompleted: false
      }
    }
  },
  methods: {
    addItem: function () {
      itemsRef.push(this.item)
      this.item.name = ''
      this.item.category = 'Produce'
      this.item.quantity = 1
    },
    filterItems: function (cat) {
      return this.items.filter(item => item.category === cat)
    },
    toggleCompleted: function (item, isCompleted) {
      itemsRef
        .child(item['.key'])
        .child('isCompleted')
        .set(!isCompleted)
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
