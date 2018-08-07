<template>
  <div>
      <h1>Animal List</h1>
      <table>
          <thead>
              <th>Species</th>
              <th>Name</th>
              <th>Birth Date</th>
          </thead>
          <tbody>
              <tr v-for="(animal, key) in animals" :key="key">
                  <td>{{animal.species}}</td>
                  <td>{{animal.name}}</td>
                  <td v-if="typeof animal.birth_date === 'undefined' || animal.birth_date === ''">unknown</td>
                  <td v-else>{{animal.birth_date}}</td>
              </tr>
          </tbody>
      </table>  
      
  </div>
</template>

<script>
export default {
  name: 'AnimalList',
  data() {
      return {
          animals: [
              {species: "Elephant", name: "John", birth_date: "2012-05-05"},
              {species: "Parrot", name: "Jack", birth_date: "2017-06-06"},
              {species: "Lion", name: "Bob", birth_date: "2002-07-08"},
              {species: "Tiger", name: "Bill"},
              {species: "Bear", name: "Joe", birth_date: "2014-02-25"}
          ],
      }
  },
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
