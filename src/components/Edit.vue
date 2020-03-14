<template>
  <div class="edit container">
    <Alert v-if="alert" v-bind:message="alert"></Alert>
    <h1 class="page-header">编辑用户：</h1>
    <form @submit="updateCustomers">
      <div class="well">
        <h4>用户信息</h4>
        <div class="form-group">
          <label for>姓名</label>
          <input type="text" class="form-control" placeholder="name" v-model="customer.name" />
        </div>
        <div class="form-group">
          <label for>电话</label>
          <input type="phone" class="form-control" placeholder="phone" v-model="customer.phone" />
        </div>
        <div class="form-group">
          <label for>邮箱</label>
          <input type="email" class="form-control" placeholder="email" v-model="customer.email" />
        </div>
        <div class="form-group">
          <label for>学历</label>
          <input type="text" class="form-control" placeholder="edu" v-model="customer.edu" />
        </div>
        <div class="form-group">
          <label for>毕业学校</label>
          <input
            type="text"
            class="form-control"
            placeholder="graduationSchool"
            v-model="customer.graduationSchool"
          />
        </div>
        <div class="form-group">
          <label for>职业</label>
          <input
            type="text"
            class="form-control"
            placeholder="profession"
            v-model="customer.profession"
          />
        </div>
        <div class="form-group">
          <label for>个人简介</label>
          <textarea
            type="text"
            rows="10"
            class="form-control"
            placeholder="profile"
            v-model="customer.profile"
          ></textarea>
        </div>
        <button type="submit" class="btn btn-primary">确认</button>
      </div>
    </form>
  </div>
</template>

<script>
import Alert from "./Alert";
export default {
  name: "edit",
  data() {
    return {
      customer: {},
      alert: "",
      jsonServer: "http://localhost:3000/customers/"
    };
  },
  components: {
    Alert
  },
  methods: {
    fetchCustomer(id) {
      this.$http.get(this.jsonServer + id).then(function(response) {
        //   console.log(response);
        this.customer = response.body;
      });
    },
    updateCustomers(e) {
      //   console.log(123);
      if (!this.customer.name || !this.customer.phone || !this.customer.email) {
        // console.log("请填写对应信息！");
        this.alert = "请填写对应信息！";
      } else {
        let updateCustomer = {
          name: this.customer.name,
          phone: this.customer.phone,
          email: this.customer.email,
          edu: this.customer.edu,
          graduationSchool: this.customer.graduationSchool,
          profession: this.customer.profession,
          profile: this.customer.profile
        };
        this.$http
          .put(this.jsonServer + this.$route.params.id, updateCustomer)
          .then(function(response) {
            // console.log(response);
            this.$router.push({
              path: "/",
              query: { alert: "用户信息更新成功！" }
            });
          });
      }
      e.preventDefault();
    }
  },
  created() {
    this.fetchCustomer(this.$route.params.id);
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
