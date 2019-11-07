<template>

  <div>
    <nav class="navbar navbar-expand-lg navbar-light bg-dark">
        <img style="cursor: pointer; width : 50px" :src="logoHome" alt="">
        <a class="navbar-brand" href="#">Nama Web</a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav mr-auto">
            <li class="nav-item active">
              <a class="nav-link" href="" @click="home" >Home <span class="sr-only">(current)</span></a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">Link</a>
            </li>                    
          </ul>
          <form class="form-inline my-2 my-lg-0">
            <button class="btn btn-outline-success my-2 my-sm-0" type="submit" @click.prevent="logout" >Logout</button>
          </form>
        </div>
      </nav>
  </div>
  <!-- <nav>
      <!-- logo dari parent -->
      <!-- :src ini akan diisi dengan props yang didapat dari home  -->
      <!-- <a href=""> <img :src="logoHome" alt="" @click="home" ></a>
      <ul>Makan</ul> -->
  <!-- </nav>  -->
</template>

<script>
export default {
    props : ['logoHome'], // props menerima data dari parent
    methods: {
      home() {        
      },
      logout() {
        localStorage.removeItem('token')
      }
    }
}
</script>

<style>

</style>