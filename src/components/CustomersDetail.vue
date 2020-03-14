<template>
  <div class="details container">
    <router-link to="/" class="btn btn-default">返回主页</router-link>
    <h1 class="page-header">
      {{customers.name}}
      <span class="pull-right">
        <router-link :to="'/edit/'+customers.id" class="btn btn-primary">编辑</router-link>
        <button class="btn btn-danger" v-on:click="delectCustomer(customers.id)">删除</button>
      </span>
    </h1>
    <ul class="list-group">
      <li class="list-group-item">
        <span class="glyphicon glyphicon-phone">：{{customers.phone}}</span>
      </li>
      <li class="list-group-item">
        <span class="glyphicon glyphicon-envelope">：{{customers.email}}</span>
      </li>
    </ul>
    <ul class="list-group">
      <li class="list-group-item">
        <span class="glyphicon glyphicon-phone">：{{customers.edu}}</span>
      </li>
      <li class="list-group-item">
        <span class="glyphicon glyphicon-envelope">：{{customers.graduationSchool}}</span>
      </li>

      <li class="list-group-item">
        <span class="glyphicon glyphicon-phone">：{{customers.profession}}</span>
      </li>
      <li class="list-group-item">
        <span class="glyphicon glyphicon-envelope">： {{customers.profile}}</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "customersdetails",
  data() {
    return {
      customers: ""
    };
  },
  methods: {
    fetchCustomers(id) {
      this.$http
        .get("http://localhost:3000/customers/" + id)
        .then(function(response) {
          // console.log(response.body);
          this.customers = response.body;
        });
    },
    delectCustomer(id) {
      this.$http
        .delete("http://localhost:3000/customers/" + id)
        .then(function(response) {
          this.$router.push({ path: "/", query: { alert: "用户删除成功！" } });
        });
      //   console.log(id);
    }
  },
  created() {
    this.fetchCustomers(this.$route.params.id);
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
