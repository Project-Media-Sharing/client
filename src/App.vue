<template>
  <div>
    <!-- Login -->
    <div v-if="isLogin==false">
      <form v-on:submit.prevent="login">
          <div class="form-group">
              <label>Email address</label>
              <input type="email" class="form-control" placeholder="Enter email" v-model="email">
          </div>
          <div class="form-group">
              <label>Password</label>
              <input type="password" class="form-control" placeholder="Password" v-model="password">
          </div>
          <input type="submit" name="submit">
      </form>
    </div>

    <!-- Register -->
    <div v-if="isRegister">
      <form v-on:submit.prevent="register">
          <div class="form-group">
              <label>Email address</label>
              <input type="email" class="form-control" placeholder="Enter email" v-model="email">
              <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
          </div>
          <div class="form-group">
              <label>Username</label>
              <input type="text" class="form-control" placeholder="Enter username" v-model="username">
          </div>
          <div class="form-group">
              <label>Password</label>
              <input type="password" class="form-control" placeholder="Password" v-model="password">
          </div>
          <input type="submit" name="submit">
      </form>
    </div>

      <!-- panggil komponenya disini -->
      <navBar :logo-home='logoHome' > </navBar>
      <formImage></formImage>
      <profilePic :pic="pic"></profilePic>
      <profile v-if="showProfile" :pictures="pictures" :user="user"></profile>
      <footerItem> </footerItem>
  </div>
</template>

<script>

import axios from 'axios';
// bagian ini berisi component mana saja yang ingin kita pakai
import navBar from './components/navBar'; 
import srcLogo from '../assets/logo.png';
import formImage from './components/formImage';
import profilePic from './components/profilePic';
import profile from './components/profile';
//import formRegister from './components/formRegister';
//import formLogin from './components/formLogin';
import footerItem from './components/footerItem';

export default {
  created() {
    if(localStorage.getItem("token")) {
      this.isLogin= true
      this.isRegister= false;
      this.getPictures();
    } else {
      this.isLogin=false
      this.isRegister=true
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
      logoHome : srcLogo,
      pic: "",
    };
  },
  watch: {
    isLogin: function(val) {
      if( val ) {
        this.getPic();
      } else {
        this.pictures = [];
      }
    }
  },
  methods: {
    register() {
      console.log(this.email, this.password,this.username)
      axios({
        method:"POST",
        url: "http://localhost:3000/users/signup",
        data: {
          username: this.username,
          email: this.email,
          password: this.password
        }
      })
        .then(({ data }) => {
          Swal.fire({
            position: 'center',
            icon: 'success',
            title: 'Successfully Registered',
            showConfirmButton: false,
            timer: 1500
          })
          console.log('Successfully registering new user');
          console.log(data);
          this.isRegister = false;
        })
        .catch(( err ) => {
          console.log('error while registering new user', err);
        })
    },
    login() {
      axios({
        method:"POST",
        url: "http://localhost:3000/users/signin",
        data: {
          email: this.email,
          password: this.password
        }
      })
        .then(({ data }) => {
          Swal.fire({
            position: 'center',
            icon: 'success',
            title: 'Successfully Login',
            showConfirmButton: false,
            timer: 1500
          })
          console.log('data => ',data);
          localStorage.setItem("token", data.access_token);
          this.showProfile = true;
          this.isRegister = false;
          this.user = data.username;
          this.isLogin= true;
          this.email="",
          this.password=""
          this.getPictures();
        })
        .catch(( err ) => {
          console.log('error while registering new user', err);
        })
    },
    getPictures() {
      console.log('148')
      axios({
          method: 'get',              
          url : 'http://localhost:3000/files/all',
          headers: {
            token: localStorage.getItem("token")
          }
      })
         .then(response => {
            console.log('response => ',response);
            this.pictures = response.data;
            this.showProfile = true;
        })
        .catch(err => {
            console.log(err);
        })
    },
    logout() {
      localStorage.removeItem("token");
      this.isLogin = false;
    }
  },
  components : {
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