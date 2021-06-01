<template>
  <div class="row">
    <div class="col-md-12">
      <h1>Borrowed Books Record</h1>
      <div class="titles">
          <ul class="list-group">
          <li class="list-group-item">
            <a href="#" class="list-group-item-action"
                @click.prevent="selectBorrow(list)">
            <table class="table">
              <thead class="thead-dark">
                <tr>
                  <th scope="col">Student ID</th>
                  <th scope="col">Book ID</th>
                  <th scope="col">Date Borrowed</th>
                  <th scope="col">Date Returned</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="borrow in borrows" :key="borrow.id">
                  <td>{{borrow.books_id}}</td>
                  <td>{{borrow.students_id}}</td>
                  <td>{{borrow.date_borrowed}}</td>
                  <td>{{borrow.date_returned}}</td>
                </tr>
              </tbody>
            </table>
            </a>
          </li>
        </ul>
      </div>
    </div>
    <div class="col-md-8">
      <Borrow :borrow="selectedBorrow" v-if="selectedBorrow!=null" />
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Borrow from './components/Borrow.vue'
// import HelloWorld from './components/HelloWorld.vue'
export default {
  name: 'App',
  components: {
    Borrow
  },
  data() {
    return {
      borrows: [],
      selectedBorrow: null
    }
  },
  methods: {
    async getBorrows() {
      axios.get('https://laravel-apiproj.herokuapp.com/api/borrows')
      .then(response => {
        if(response.status==200) {
          this.borrows = response.data;
        }
      })
    },
    selectBorrow(borrow) {
      this.selectedBorrow = borrow
    }
  },
  created() {
    this.getBorrows()
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width: 10000px;
  margin:30px;
}

</style>
