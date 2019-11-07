<template>
  <div>
      <section class="fdb-block py-0">
            <div class="container py-5 my-5" >
                <div class=" row justify-content-end">
                <div class="col-12 col-md-8 col-lg-6 col-xl-5 text-left">
                    <div class="fdb-box">
                    <div class="row">
                        <div class="col">
                        <h1>Register Page</h1>
                        <p class="lead">Right at the coast of the Semantics, a large language ocean. A small river named Duden.</p>
                        </div>
                    </div>
                    <div class="row">
                        <div class="col mt-4">
                        <input type="text" class="form-control" placeholder="Username" v-model="username">
                        </div>
                    </div>
                    <div class="row mt-4">
                        <div class="col">
                        <input type="password" class="form-control" placeholder="Password" v-model="password">
                        </div>
                    </div>
                    <div class="row mt-4">
                        <div class="col">
                        <button class="btn btn-secondary" type="button" @click.prevent="sendRegister()" >Submit</button>
                        </div>
                    </div>
                    </div>
                </div>
                </div>
            </div>
        </section>
  </div>
</template>

<script>
export default {
    data() {
        email : '';
        username : '';
        password : '';
    },
    methods : {
        sendRegister() {
            axios.post({
                url : 'http://localhost/3000/register',
                data : {
                    email : this.email,
                    password : this.password,
                    username : this.user
                }
            })
            then(({data}) => {
                
            })
        }
    }
}
</script>

<style>

</style>