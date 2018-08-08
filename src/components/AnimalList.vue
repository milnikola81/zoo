<template>
  <div>
      <h1>Animal List</h1>
      <form @submit.prevent>
          <label>Species</label><br>
          <input v-model="newAnimal.species" type="text" placeholder="species..."> <br><br>
          <label>Name</label><br>
          <input v-model="newAnimal.name" type="text" placeholder="name..."> <br><br>
          <label>Birth date</label><br>
          <input v-model="newAnimal.birth_date" type="text" placeholder="birth date..."> <br><br>

          <select v-model="newAnimal.sector">
            <option disabled value="">Please select sector</option>
            <option v-for="(sector, index) in sectors" :key='index' v-bind:value="sector">{{ sector.name }}</option>
          </select>
          <br><br>
          <button @click="addAnimal()" type="submit">Add animal</button>
      </form><br><br><br>
      <table>
          <thead>
              <th>Species</th>
              <th>Name</th>
              <th>Birth Date</th>
              <th>Sector</th>
          </thead>
          <tbody>
              <tr v-for="(animal, index) in animals" :key="index" v-bind:class="{ green: animal.background }">
                  <td>{{animal.species}}</td>
                  <td>{{animal.name}}</td>
                  <td v-if="typeof animal.birth_date === 'undefined' || animal.birth_date === ''">unknown</td>
                  <td v-else>{{animal.birth_date}}</td>
                  <td>{{animal.sector.name}}</td>
                  <td style="border: none"><button @click="removeAnimal(animal)" type="submit">Remove</button></td>
                  <td style="border: none"><button @click="moveToTop(animal)" type="submit">Move to top</button></td>
                  <td style="border: none"><button @click="toggleBackground(animal)" type="submit">Toggle</button></td>
              </tr>
          </tbody>
      </table>

      <table>
          <thead>
              <th>No.</th>
              <th>Sector</th>
          </thead>
          <tbody>
              <tr v-for="(sector, index) in sectors" :key="index">
                  <td>{{index+1}}</td>
                  <td>{{sector.name}}</td>
                  <td style="border: none"><button @click="showAnimals(sector)" type="submit">Show animals</button></td>
              </tr>
          </tbody>
      </table>  
      
  </div>
</template>

<script>
const sectors = [
    {name: "North"},
    {name: "South"},
    {name: "West"},
    {name: "East"}
];
export default {
  name: 'AnimalList',
  data() {
      return {
          sectors: sectors,
          animals: [
              {species: "Elephant", name: "John", birth_date: "2012-05-05", sector: sectors[0], background: false},
              {species: "Parrot", name: "Jack", birth_date: "2017-06-06", sector: sectors[1], background: true},
              {species: "Lion", name: "Bob", birth_date: "2002-07-08", sector: sectors[2], background: false},
              {species: "Tiger", name: "Bill", sector: sectors[3], background: true},
              {species: "Bear", name: "Joe", birth_date: "2014-02-25", sector: sectors[1], background: false}
          ],
          newAnimal: {
              species: '',
              name: '',
              birth_date: '',
              sector: '',
              background: false
          },
      }
  },
  methods: {
      addAnimal() {
            this.animals.push(this.newAnimal);
            console.log(this.newAnimal.sector.name)
        },
      removeAnimal(animal) {
            let index = this.animals.indexOf(animal);
            this.animals.splice(index, 1);
      },
      moveToTop(animal) {
            let index = this.animals.indexOf(animal);
            this.animals.splice(index, 1);
            this.animals.unshift(animal);
      },
      showAnimals(sector) {
          let sectorAnimals = [];
          for(var i=0; i<this.animals.length; i++) {
              if (this.animals[i].sector === sector) {
                  sectorAnimals.push(this.animals[i].species);
              }
          }
          alert("In this sector we have: "+sectorAnimals);
      },
      toggleBackground(animal) {
          let index = this.animals.indexOf(animal);
          if(this.animals[index].background) {
              this.animals[index].background = false;
          }
          else {
              this.animals[index].background = true;
          }
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
form {
    text-align: left;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
table {
    text-align: left;
    margin-bottom: 1rem;
}
td {
    border: 1px solid gray;
    padding: 0.5rem;
}
a {
  color: #42b983;
}
.green {
    background: green;
}
a {
  color: #42b983;
}
</style>
