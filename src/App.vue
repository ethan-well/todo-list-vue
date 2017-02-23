<template>
  <div id="app">
    <div>
      <h1>{{ title }}</h1>
    </div>
    <div class="contenor-left"></div>
    <div class="contenor">
      <input v-model="newItem" v-on:keyup.enter="AddItem">
      <ul>
        <li v-for="item in items" v-bind:class="{ 'is-finished': item.is_finished }"
          v-on:click="make_finished(item)" >
          {{ item.message }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import Store from './store'
export default {
  data: function() {
    return {
      title: "My Todo List",
      items: Store.fetch(),
      newItem: ''
    }
  },
  methods: {
    make_finished: function(item){
      item.is_finished = !item.is_finished
    },
    AddItem: function(){
      console.log(this.newItem);
      this.items.push({
        message: this.newItem,
        is_finished: false
      });
      this.newItem = "";
    }
  },
  watch: {
    items: {
      handler: function(items){
        Store.save(items);
        console.log(items)
      },
      deep: true
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.is-finished{
  color: red;
  text-decoration: line-through;
}

.contenor-left{
  float:left;
  width:40%;
  height: 2px;
}

.contenor{
  float: left;
  width:20%;
  text-align:center;
}

li{
  text-align: left;
}
</style>
