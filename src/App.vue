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
export default {
  data: function() {
    return {
      title: "My Todo List",
      items: [ ],
    newItem: '',
    is_finished: 'is-finished'
    }
  },
  methods: {
    make_finished: function(item){
      item.is_finished = !item.is_finished
      console.log('xxxxx')
    },
    AddItem: function(){
      console.log(this.newItem);
      this.items.push({
        message: this.newItem,
        is_finished: false
      });
      this.newItem = "";
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
