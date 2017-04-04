<template>
  <div class="hello">
    <h1>AJAX test</h1>
    <button v-if="nb < 10" v-on:click="addPerson">Add people</button>
    <ul>
        <li v-for="person in people">
          <h2>{{person.name}}</h2>
          <p>{{person.email}}</p>
        </li>
    </ul>
  </div>
</template>

<script>

var $ = require('jquery')
window.jQuery = $

export default {
  name: 'hello',
  data () {
    return {
      people: [],
      nb: 1
    }
  },
  methods: {
    fetchData: function(){
      var root = 'https://jsonplaceholder.typicode.com';
      self = this;
      jQuery.get(root + "/users/" + this.nb, function(data){
        self.people = [...self.people,data];
        console.log(data);
      })
    },
    addPerson: function(){
      if(this.nb !=10){
        this.nb +=1;
        this.fetchData();
      }
    }
  },
  mounted(){
    this.fetchData();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}

li {
  margin: 10px 10px;
  border: 1px solid lightgray;
  width: 30%;
}

li:hover{
  color: blue;
  border: 1px solid green;
}

a {
  color: #42b983;
}
</style>
