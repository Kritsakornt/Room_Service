<template>
<div>
    <body>
        <section class="login">
            <div class="login_box">
                <div class="left">
                <div class="top_link"><a href="http://localhost:8080/users"><img src="https://drive.google.com/u/0/uc?id=16U__U5dJdaTfNGobB_OpwAJ73vM50rPV&export=download" alt="">Back</a></div>
                    <div class="contact">
                        <form v-on:submit.prevent = "createUser">
                            <h3>REGISTER USER</h3>
                                <input type="text" v-model="user.name" placeholder="NAME">
                                <input type="text" v-model="user.lastname" placeholder="LASTNAME">
                                <input type="text" v-model="user.email" placeholder="USERNAME">
                                <input type="text" v-model="user.password" placeholder="PASSWORD">
                                <button class="submit">SUBMIT</button>
                        </form>
                    </div>
                </div>
                <div class="right">
                    <div class="right-text">
                        <h5><p><b>REGISTER</b></p>
                            <p>Name : {{user.name}}</p>
                            <p>Lastname : {{user.lastname}}</p>
                            <p>Username : {{user.email}}</p>
                            <p>Password : {{user.password}}</p>
                        </h5>
                    </div>
                </div>
            </div>
        </section>
    </body>
</div>
</template>
<script>
import UsersService from '@/services/UsersService'
export default {
    data() {
        return {
            user: {
                name: '',
                lastname: '',
                email: '',
                password: '',
                status: 'active'
            }
        }
    },
    methods: {
        async createUser() {
            try {
                await UsersService.post(this.user)
                this.$router.push({
                    name: 'users'
                })
            } catch (error) {
                console.log(error)
            }
        }
    }
}
</script>
<style scoped>
img{
	width: 100%;
}

.login_box {
    width: 920px;
    height: 500px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);
    background: #fff;
    border-radius: 10px;
    box-shadow: 1px 4px 22px -8px #0004;
    display: flex;
    overflow: hidden;
    margin-left: 120px;
}
.login_box .left{
  width: 41%;
  height: 100%;
  padding: 25px 25px;
}
.login_box .right{
  width: 59%;
  height: 100%  
}
.left .top_link a {
    color: #6d6d6d;
    font-weight: 400;
}
.left .top_link{
  height: 20px;
}

.left .top_link a:hover {
  color: rgb(0, 102, 150);
}

.left .contact{
	display: flex;
    align-items: center;
    justify-content: center;
    align-self: center;
    height: 100%;
    width: 73%;
    margin: auto;
}
.left h3{
  text-align: center;
  margin-bottom: 25px;
}
.left input {
    border: none;
    width: 80%;
    margin: 15px 0px;
    border-bottom: 1px solid #3067417d;
    padding: 7px 9px;
    width: 100%;
    overflow: hidden;
    background: transparent;
    font-weight: 600;
    font-size: 14px;
}
.left{
	background: linear-gradient(-45deg, #dcd7e0, #fff);
}
.submit {
    border: none;
    padding: 15px 70px;
    border-radius: 8px;
    display: block;
    margin: auto;
    margin-top: 20px;
    background: #FCE205;
    color: rgb(0, 0, 0);
    font-weight: bold;
    -webkit-box-shadow: 0px 9px 15px -11px rgb(71, 114, 54);
    -moz-box-shadow: 0px 9px 15px -11px rgb(54, 114, 79);
    box-shadow: 0px 9px 15px -11px rgb(54, 114, 72);
}

.right {
	background: linear-gradient(212.38deg, rgba(252, 226, 5, 0.212) 0%, rgba(125, 203, 240, 0.377) 100%),url(https://static.seattletimes.com/wp-content/uploads/2019/01/web-typing-ergonomics-1020x680.jpg);
	color: rgb(0, 0, 0);
	position: relative;
}

.right .right-text{
  height: 100%;
  position: relative;
  transform: translate(0%, 26%);
}
.right-text h2{
  display: block;
  width: 100%;
  text-align: center;
  font-size: 50px;
  font-weight: 500;
}
.right-text h5{
  display: block;
  width: 100%;
  text-align: center;
  font-size: 25px;
  font-weight: 400;
}

.right .right-inductor{
  position: absolute;
  width: 70px;
  height: 7px;
  background: #fff0;
  left: 50%;
  bottom: 70px;
  transform: translate(-50%, 0%);
}
.top_link img {
    width: 18px;
    padding-right: 7px;
    margin-top: -3px;
    color: #000000;
}
</style>