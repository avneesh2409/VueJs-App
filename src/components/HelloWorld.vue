<template>
  <div class="row">
    <div class="col-md-12">
      <div>
        <div class="jumbotron">
         <table class="table table-striped">
           <tr v-for="employee in employees" :key="employee.id">
             <td>{{ employee.username }}</td>
             <td>{{ employee.password }}</td>
             <td>{{ employee.email }}</td>
             <td>{{ employee.age }}</td>
           </tr>
         </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import "../assets/static/js/index";
export default {
  name: "HelloWorld",
  props: ["employees"]
};
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
