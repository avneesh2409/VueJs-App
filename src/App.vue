<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <div class="jumbotron text-center">
      <div class="row">
        <div class="col-md-12">
          <form>
            <strong>Hello We are Here</strong>
            <div class="form-control">
              <label >username :</label>
              <input type="text" v-model="username" />
            </div>
            <div class="form-control">
              <label>password :</label>

              <input type="password" v-model="password" />
            </div>
            <div class="form-control">
              <label>Age :</label>

              <input type="number" v-model="age" />
            </div>

            <div class="form-control">
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
import HelloWorld from "./components/HelloWorld.vue";
export default {
  name: "app",
  components: {
    HelloWorld
  },
  data: () => {
    return {
      username: "",
      email: "",
      age: 21,
      password: "",
      load: false,
      employees: []
    };
  },
  methods: {
    Submitted() {
      this.$http
        .get("https://vue-http-86b74.firebaseio.com/userData.json")
        .then(response => {
          return response;
        })
        .then(response => {
          this.employees = response.body;
          this.load = true;
          console.log(response);
        });
      let senddata = {
        username:this.username,
        password:this.password,
        email:this.email,
        age:this.age
      }
      this.$http.post("https://vue-http-86b74.firebaseio.com/userData.json",senddata)
      .then(response => {
        return response.json()
      }).then(response =>{
          console.log(response)
      })

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
</style>
