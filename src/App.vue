<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <div class="jumbotron">
      <div class="row">
        <div class="col-md-12 col-sm-6 col-xs-3">
          <form>
            <strong>Hello We are Here</strong>
            <div class="form-control padding">
              <label>username :</label>
              <input type="text" v-model="username" />
            </div>
            <div class="form-control padding">
              <label>password :</label>
              <input type="password" v-model="password" />
            </div>
            <div class="form-control padding">
              <label>Age :</label>
              <input type="number" v-model="age" />
            </div>

            <div class="form-control padding">
              <label>Email :</label>
              <input type="email" v-model="email" />
            </div>
            <div class="form-control">
              <button @click.prevent="Submitted" class="btn btn-primary">Submit</button>
            </div>
          </form>
        </div>
      </div>
      <div class="container" v-if="load">
        <HelloWorld :employees="employees"></HelloWorld>
      </div>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
export default {
  name: 'app',
  components: {
    HelloWorld
  },
  data: () => {
    return {
      username: '',
      email: '',
      age: 21,
      password: '',
      load: false,
      employees: []
    };
  },
  methods: {
    Submitted() {
      this.$http
        .get('https://vue-http-86b74.firebaseio.com/userData.json')
        .then(response => {
          return response.json();
        })
        .then(response => {
          let dataArray = [];
          response.forEach(element => {
            this.employees.push(element);
          });
          this.employees = dataArray;
          this.load = true;
          console.log(response);
        });
      // axios
      //   .get('http://dummy.restapiexample.com/api/v1/employees')
      //   .then(response => {
      //     console.log(response.data)
      //     this.employee = response.data
      //   })
      //   .catch(err => {
      //     console.log(err)
      //   });
    }
  }
};
</script>

<style scoped>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.form-control {
  margin-top: 20px;
  padding: 10px;
}
</style>
