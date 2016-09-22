<template>
<div id="app">
  <h1 v-html="title"></h1>
  <input v-on:keyup.enter="addNew" v-model="newItem" name="name" value="">
  <ul>
    <li v-for="item in items" v-bind:class="{fineshed: item.isFinished}" v-on:click="toggleFineshed(item)">
      {{item.label}}
    </li>
  </ul>
</div>
</template>

<script>
import Store from './store'
console.log(Store)
export default {
  data: function () {
    return {
      title: '<span>?</span>this is a todo list',
      items: Store.fetch(),
      newItem: ''
    }
  },
  methods: {
    toggleFineshed: function (item) {
      console.log(item.isFinished = !item.isFinished)
    },
    addNew: function () {
      this.items.push({
        label: this.newItem,
        isFinished: false
      })
      this.newItem = ''
    }
  },
  watch: {
    items: {
      handler: function (items) {
        Store.save(items)
      },
      deep: true
    }
  },
}
</script>

<style>
html {
  height: 100%;
}
.fineshed{
  text-decoration: line-through;
}
body {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
}

#app {
  color: #2c3e50;
  margin-top: -100px;
  max-width: 600px;
  font-family: Source Sans Pro, Helvetica, sans-serif;
  text-align: center;
}

#app a {
  color: #42b983;
  text-decoration: none;
}

.logo {
  width: 100px;
  height: 100px
}
</style>
