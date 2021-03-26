<template>
  <div class="container-fluid">
    <h1>Table Users</h1>
    <div class="show__data">
      <label for="data-record">Show data: </label>
      <select v-model="dataRecord" name="data-record" id="data-record">
        <option value="all">All</option>
        <option value="3">3</option>
        <option value="5">5</option>
        <option value="10">10</option>
      </select>
    </div>
    <table class="table__container">
      <thead>
        <tr class="table__row">
          <th class="table__col__id" @click="sort('id')">
            ID <i :class="{'fas fa-sort':'id' == currentSort}"></i>
          </th>
          <th class="table__col__fname" @click="sort('first_name')">
            First Name <i :class="{'fas fa-sort':'first_name' == currentSort}"></i>
          </th>
          <th class="table__col__lname" @click="sort('last_name')">
            Last Name <i :class="{'fas fa-sort':'last_name' == currentSort}"></i>
          </th>
          <th class="table__col__email" @click="sort('email')">
            Email <i :class="{'fas fa-sort':'email' == currentSort}"></i>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr class="table__row" v-for="user in usersShow" :key="user.id">
          <UserList :user="user"/>
        </tr>
      </tbody>
    </table>
    <div class="table__pages">
      <button v-if="page > 1" @click="changePage(-1)">Prev</button>
      <h4>Page {{ page }} / {{total_pages}}</h4>
      <button v-if="page < total_pages" @click="changePage(1)">Next</button>
    </div>
  </div>
</template>

<script>
  import UserList from "../components/UserList"
  import axios from "axios";

  export default {
    name: 'Table',
    components: {
      UserList
    },
    data: () => {
      return{
        users_api: 'https://reqres.in/api/users',
        page: 1,
        total_pages: 1,
        users: [],
        usersShow: [],
        currentSort: 'id',
        ascending: false,
        dataRecord: 'all',
        numRecord: -1,
      }
    },
    watch: {
      dataRecord: function() {
        if (this.dataRecord.length > 0) {
          let temp = this.dataRecord == "all" ? true : false;
          this.numRecord = this.dataRecord != "all" ? parseInt(this.dataRecord) : -1;
          if (temp) {
            this.total_pages = 1;
            this.usersShow = this.users;
          }
          else {
            this.total_pages = Math.floor((this.users.length - 1) / this.numRecord) + 1;
            this.usersShow = [];
            for (let i = 0; i < this.numRecord; i++){
              this.usersShow.push(this.users[i]);
            }
          }
          this.page = 1;
        }
      }
    },
    methods: {
      getUsers(data) {
        for (let user in data){
          this.users.push(data[user]);
        }
      },
      getData(dataTotalPages) {
        for (let i = 1; i <= dataTotalPages; i++){
          let get_api = this.users_api + "?page=" + i;
          axios.get(get_api)
          .then((response) =>
            this.getUsers(response.data.data)
          )
        }
      },
      changePage: function(n) {
        this.page += n;
        let end = (this.page * this.numRecord) > this.users.length ?
        this.users.length : (this.page * this.numRecord);
        let start = (this.page - 1) * this.numRecord;
        this.usersShow = [];
        for (let i = start; i < end; i++){
          this.usersShow.push(this.users[i]);
        }
      },
      sort: function(value) {
        this.ascending = value === this.currentSort ? !this.ascending : this.ascending;
        this.currentSort = value;

        var asc = this.ascending;
        this.usersShow.sort(function(a, b) {
          if (a[value] < b[value]) return asc ? 1 : -1;
          if (a[value] > b[value]) return asc ? -1 : 1;
          return 0;
        })
        this.users.sort(function(a, b) {
          if (a[value] < b[value]) return asc ? 1 : -1;
          if (a[value] > b[value]) return asc ? -1 : 1;
          return 0;
        })
      }
    },
    mounted() {
      axios.get(this.users_api)
      .then((response) =>
        this.getData(response.data.total_pages)
      )
      .catch((error) =>
        console.log(error)
      );
      this.usersShow = this.users;
    }
  }
</script>

<style>
  @import '../assets/style/table.css'
</style>
