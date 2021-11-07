<template>
    <div>
        <div class="sidebar"> 
            <center><i class="fa fa-building" aria-hidden="true"></i>
            <h1 class="text-center"><b>Room Service</b></h1></center>
            <a><router-link :to="{name: 'blogs'}"><i class="fa fa-calendar-check-o" aria-hidden="true"></i><b> Room Service</b></router-link></a>
            <a><router-link :to="{name: 'comments'}"><i class="fa fa-pencil-square-o" aria-hidden="true"></i><b> Notify Repair</b></router-link></a>
            <a><router-link :to="{name: 'users'}"><i class="fa fa-address-card" aria-hidden="true"></i><b> User Account</b></router-link></a> 
            <a><router-link :to="{name: 'login'}"><i class="fa fa-user" aria-hidden="true"></i><b> Login</b></router-link></a>
            <a><a v-on:click.prevent="logout" v-on:click="navigateTo('/login')"><i class="fa fa-sign-out" aria-hidden="true"></i><b> Logout</b></a></a>
        </div>
    </div>
</template>

<script>
import AuthenService from "@/services/AuthenService";

export default {
  data() {
    return {
      email: "",
      password: "",
      error: null
    };
  },
  methods: {
    async onLogin() {
      try {
        const response = await AuthenService.login({
          email: this.email,
          password: this.password
        });

        this.$store.dispatch("setToken", response.data.token);
        this.$store.dispatch("setUser", response.data.user);

        this.$router.push({
          name: "users"
        });
      } catch (error) {
        console.log(error);
        this.error = error.response.data.error; //ฟ้อง error ถ้าใส่รหัสผิด หรือรหัสไม่มีอยู่ในคลัง
        this.email = "";
        this.password = "";
      }
    },
    navigateTo(route) {
      this.$router.push(route);
    },
    logout() {
      this.$store.dispatch("setToken", null);
      this.$store.dispatch("setUser", null);

      this.$router.push({
        name: "login",
      });
    },
  }
};
</script>

<style scoped>
    /* The side navigation menu */
.sidebar {
  margin: 0;
  padding: 0;
  width: 230px;
  background-color: #7dcbf0; /*444*/ 
  position: fixed;
  height: 100%;
  overflow: auto;
  font-size: 17px;
  border-radius: 0px 0px 0px 0px;

}

.sidebar center {
  font-size: 70px;
  display: block;
  color: #006696;
  padding: 9px; /* ห่างจากตัวออกไป */
  text-decoration: none;
  background-color: #FCE205;
}

.sidebar center h1 {
  font-size: 30px;
}

/* Sidebar links */
.sidebar a {
  display: block;
  color: black;
  padding: 9px; /* ห่างจากตัวออกไป */
  text-decoration: none;
  text-align: center;
}

/* Active/current link */
.sidebar a.active {
  background-color: #FCE205 ;
  color: #7dcbf0;
}

/* Links on mouse-over */
.sidebar a:hover:not(.active) {
  background-color: #FCE205 ;
  border-radius: 10px 10px 10px 10px;
  color: #005780;
}

/* Page content. The value of the margin-left property should match the value of the sidebar's width property */
div.content {
  margin-left: 200px;
  padding: 1px 16px;
  height: 1000px;
}

/* On screens that are less than 700px wide, make the sidebar into a topbar */
@media screen and (max-width: 700px) {
  .sidebar {
    width: 100%;
    height: auto;
    position: relative;
  }
  .sidebar a {float: left;}
  div.content {margin-left: 0;}
}

/* On screens that are less than 400px, display the bar vertically, instead of horizontally */
@media screen and (max-width: 400px) {
  .sidebar a {
    text-align: center;
    float: none;
  }
}

.sidebar a.router-link-active{
    color: black;
    background-color: #FCE205 ;
     border-radius: 5px 5px 5px 5px;

}

</style>