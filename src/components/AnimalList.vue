<template>
  <div>
      <h1>Animal List</h1>
      <form @submit.prevent>
          <label>Species</label>
          <input v-model="newAnimal.species" type="text" placeholder="species"> <br>
          <label>Name</label>
          <input v-model="newAnimal.name" type="text" placeholder="name"> <br>
          <label>Birth date</label>
          <input v-model="newAnimal.birth_date" type="text" placeholder="birth date"> <br>
          <button @click="addAnimal()" type="submit">Add animal</button>
      </form>
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
                  <td><button @click="removeAnimal(animal)" type="submit">Remove</button></td>
                  <td><button @click="moveToTop(animal)" type="submit">Move to top</button></td>
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
          newAnimal: {
              species: '',
              name: '',
              birth_date: ''
          }
      }
  },
  methods: {
      addAnimal() {
            this.animals.push(this.newAnimal);
        },
      removeAnimal(animal) {
            let index = this.animals.indexOf(animal);
            this.animals.splice(index, 1);
      },
      moveToTop(animal) {
            let index = this.animals.indexOf(animal);
            let animalToMove = animal;
            this.animals.splice(index, 1);
            this.animals.unshift(animalToMove);
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
