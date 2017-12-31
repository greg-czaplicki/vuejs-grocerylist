<template>
  <div id="app">

    <!-- Title -->
    <h1 id="title">Grocery List</h1>

    <!-- Form -->
    <form v-on:submit.prevent="addItem">
      <ItemName v-bind:item="item"></ItemName>
      <ItemCategory v-bind:categories="categories" v-bind:item="item"></ItemCategory>
      <ItemQuantity v-bind:item="item"></ItemQuantity>
    </form>

    <!-- Grocery List -->
    <div v-for="category in categories">
      <GroceryList :toggleCompleted="toggleCompleted" :items="filterItems(category)"></GroceryList>
    </div>

    <!-- Completed List -->
  <hr>
  <h2 id="completedTitle">Completed <i class="fa fa-shopping-cart" aria-hidden="true"></i></h2>
    <div v-for="category in categories">
      <GroceryList :toggleCompleted="toggleCompleted" :items="filterCompleted(category)"></GroceryList>
    </div>

    <button v-on:click="clearDb" v-if="items.length > 0" class="button is-warning">Clear</button>

  </div>
</template>

<script>
// ---------------
// FirebaseConfig
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
// ---------------------------
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
      },
      completeHeader: false
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
      return this.items
        .filter(item => item.category === cat)
        .sort((a, b) => a.name > b.name)
        .filter(item => item.isCompleted === false)
    },
    toggleCompleted: function (item, isCompleted) {
      itemsRef
        .child(item['.key'])
        .child('isCompleted')
        .set(!isCompleted)
    },
    filterCompleted: function (cat) {
      return this.items
        .filter(item => item.category === cat)
        .sort((a, b) => a.name > b.name)
        .filter(item => item.isCompleted === true)
    },
    clearDb: function () {
      const answer = window.prompt('Enter the passcode to clear the grocery list.')
      if (answer === '1029') {
        itemsRef.remove()
      } else {
        alert('You entered the wrong passcode!')
      }
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
  max-width: 90%;
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

#completedTitle {
  font-size: 30px;
  color: rgb(182, 182, 182);
  font-style: italic;
}

button {
  align-content: center;
}

.is-warning {
  margin: 15px 0;
  width: 100%;
  height: 45px;
  font-size: 20px;
  margin-top: 40px;
}

/* Desktops and laptops ----------- */
@media only screen and (min-width: 1224px) {
  /* Styles */
  #app {
    margin: 60px auto;
    max-width: 40%;
  }
}
</style>
