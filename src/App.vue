<template>
  <div>
    <!-- panggil komponennya disini -->
    <navBar :logo-home="logoHome" @isLogin="logOut" :isLogin="isLogin"></navBar>
    <!-- Login -->
    <div class="container mt-5" >
      <div class="row" >
        <div v-if="isLogin==false" class="form-group col-sm-8 offset-sm-2 border rounded py-3"  >
          <div >
            <h2 class="text-center" >Login Form</h2>
            <form v-on:submit.prevent="login" >
              <div class="form-group" >
                <label>Email address</label>
                <input type="email" class="form-control" placeholder="Enter email" v-model="email" />
              </div>
              <div class="form-group">
                <label>Password</label>
                <input type="password" class="form-control" placeholder="Password" v-model="password" />
              </div>
              <input class="btn btn-secondary" type="submit" name="Login" />
            </form>
          </div>
        </div>
      </div>
    </div>
    
    <!-- Register -->
    <div class="container mt-5">
      <div class="row">
        <div v-if="isRegister" class="form-group col-sm-8 offset-sm-2 border rounded py-3">
          <div >
            <h2 class="text-center">Register Form</h2>
            <form v-on:submit.prevent="register">
              <div class="form-group">
                <label>Email address</label>
                <input type="email" class="form-control" placeholder="Enter email" v-model="email_register" />
                <small
                  id="emailHelp"
                  class="form-text text-muted"
                >We'll never share your email with anyone else.</small>
              </div>
              <div class="form-group">
                <label>Username</label>
                <input type="text" class="form-control" placeholder="Enter username" v-model="username_register" />
              </div>
              <div class="form-group">
                <label>Password</label>
                <input type="password" class="form-control" placeholder="Password" v-model="password_register" />
              </div>
              <input type="submit" name="submit"  class="btn "/>
            </form>
          </div>
      </div>
      </div>
    </div>

    <formImage @getPicture="getPictures" v-if="isLogin"></formImage>
    <profilePic :pic="pic"></profilePic>
    <profile v-if="showProfile" :pictures="pictures" :user="user" @getPicture="getPictures"></profile>
    <footerItem></footerItem>
  </div>
</template>

<script>
import axios from "axios";
// bagian ini berisi component mana saja yang ingin kita pakai
import navBar from "./components/navBar";
import srcLogo from "../assets/logo.png";
import formImage from "./components/formImage";
import profilePic from "./components/profilePic";
import profile from "./components/profile";
//import formRegister from './components/formRegister';
//import formLogin from './components/formLogin';
import footerItem from "./components/footerItem";

export default {
  created() {
    if (localStorage.getItem("token")) {
      this.isLogin = true;
      this.isRegister = false;
      this.getPictures();
    } else {
      this.isLogin = false;
      this.isRegister = true;
    }
  },
  data() {
    return {
      // data yang ada di sini akan dipakai oleh setiap komponen
      isLogin: false,
      isRegister: true,
      showProfile: false,
      user: "",
      username: "",
      email: "",
      password: "",
      pictures: [],
      logoHome: srcLogo,
      pic: "",
      email_register: "",
      password_register: "",
      username_register: ""
    };
  },
  watch: {
    isLogin: function(val) {
      if (val) {
        this.getPic();
      } else {
        this.pictures = [];
      }
    }
  },
  methods: {
    register() {
      console.log(this.email, this.password, this.username);
      axios({
        method: "POST",
        url: "http://localhost:3000/users/signup",
        data: {
          username: this.username_register,
          email: this.email_register,
          password: this.password_register
        }
      })
        .then(({ data }) => {
          Swal.fire({
            position: "center",
            icon: "success",
            title: "Successfully Registered",
            showConfirmButton: false,
            timer: 1500
          });
          console.log("Successfully registering new user");
          console.log(data);
          this.isRegister = false;
        })
        .catch(err => {
          console.log("error while registering new user", err);
        });
    },
    login() {
      axios({
        method: "POST",
        url: "http://localhost:3000/users/signin",
        data: {
          email: this.email,
          password: this.password
        }
      })
        .then(({ data }) => {
          Swal.fire({
            position: "center",
            icon: "success",
            title: "Successfully Login",
            showConfirmButton: false,
            timer: 1500
          });
          console.log("data => ", data);
          localStorage.setItem("token", data.access_token);
          this.showProfile = true;
          this.isRegister = false;
          this.user = data.username;
          this.isLogin = true;
          (this.email = ""), (this.password = "");
          this.getPictures();
        })
        .catch(err => {
          console.log("error while registering new user", err);
        });
    },
    getPictures() {
      console.log("148");
      axios({
        method: "get",
        url: "http://localhost:3000/files/all",
        headers: {
          token: localStorage.getItem("token")
        }
      })
        .then(response => {
          console.log("response => ", response);
          this.pictures = response.data;
          this.showProfile = true;
        })
        .catch(err => {
          console.log(err);
        });
    },
    logOut() {
      localStorage.removeItem("token");
      this.isLogin = false;
    }
  },
  components: {
    navBar,
    formImage,
    profile,
    profilePic,
    footerItem
  }
};
</script>

<style scoped>
</style>