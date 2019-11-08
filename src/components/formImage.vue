<template>

    <div >
        <div class="col-sm-10 offset-sm-1 pt-5">
            <div class="row">
                <div class="col-sm-6">
                    
                    <div class="card">
                        <img :src="imageAddress" class="card-img-top" alt="...">                      
                    </div>
                    <div class="card-body">
                        
                    </div>
                </div>
                <div class="col-sm-6">
                    <div class="card">
                        <div class="card-body">
                            <h1 class="card-title">Try Out Our Web For Free</h1>
                            
                                <h4 class="py-3">You Can Try Our Web With The Sample Image</h4>
                            <div id="recipeCarousel" class="carousel slide w-100" data-ride="carousel">
                                <div class="carousel-inner w-100" role="listbox">
                                        <div class="carousel-item row no-gutters active">
                                            <div class="col-3 float-left px-1"><a href=""><img class="img-fluid" @click.prevent="sendFile('https://labs.everypixel.com/api/static/i/estest_sample1.jpg')" src="https://labs.everypixel.com/api/static/i/estest_sample1.jpg"></a></div>
                                            <div class="col-3 float-left px-1"><a href=""><img class="img-fluid" @click.prevent="sendFile('https://labs.everypixel.com/api/static/i/estest_sample2.jpg')" src="https://labs.everypixel.com/api/static/i/estest_sample2.jpg"></a></div>
                                            <div class="col-3 float-left px-1"><a href=""><img class="img-fluid" @click.prevent="sendFile('https://labs.everypixel.com/api/static/i/estest_sample3.jpg')" src="https://labs.everypixel.com/api/static/i/estest_sample3.jpg"></a></div>
                                            <div class="col-3 float-left px-1"><a href=""><img class="img-fluid" @click.prevent="sendFile('https://labs.everypixel.com/api/static/i/estest_sample4.jpg')" src="https://labs.everypixel.com/api/static/i/estest_sample4.jpg"></a></div>
                                        </div>
                                        <div class="carousel-item row no-gutters ">
                                            <div class="col-3 float-left px-1"><a href=""><img class="img-fluid" @click.prevent="sendFile('https://labs.everypixel.com/api/static/i/estest_sample5.jpg')" src="https://labs.everypixel.com/api/static/i/estest_sample5.jpg"></a></div>
                                            <div class="col-3 float-left px-1"><a href=""><img class="img-fluid" @click.prevent="sendFile('https://labs.everypixel.com/api/static/i/estest_sample3.jpg')" src="https://labs.everypixel.com/api/static/i/estest_sample3.jpg"></a></div>
                                            <div class="col-3 float-left px-1"><a href=""><img class="img-fluid" @click.prevent="sendFile('https://labs.everypixel.com/api/static/i/estest_sample4.jpg')" src="https://labs.everypixel.com/api/static/i/estest_sample4.jpg"></a></div>
                                            <div class="col-3 float-left px-1"><a href=""><img class="img-fluid" @click.prevent="sendFile('https://labs.everypixel.com/api/static/i/estest_sample5.jpg')" src="https://labs.everypixel.com/api/static/i/estest_sample5.jpg"></a></div>
                                        </div>
                                    </div>
                                    <a class="carousel-control-prev" href="#recipeCarousel" role="button" data-slide="prev">
                                        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                                        <span class="sr-only">Previous</span>
                                    </a>
                                    <a class="carousel-control-next" href="#recipeCarousel" role="button" data-slide="next">
                                        <span class="carousel-control-next-icon" aria-hidden="true"></span>
                                        <span class="sr-only">Next</span>
                                    </a>
                                </div>                                
                            </div>

                        <!-- INI FORM !!!!!!! -->    
                        <div class="card-footer">
                            <form @submit.prevent="upload">
                              <input type="file" name="file" @change="changeFile" ref="myFiles"/>
                              <input type="submit" val="test">
                            </form>
                        </div>
                    </div>
                </div>
            </div>
      </div> 
        <!-- Central Modal Warning Demo-->
            <div class="modal fade left" id="ModalWarning" tabindex="-1" role="dialog" aria-labelledby="myModalLabel"
            aria-hidden="true">
            <div class="modal-dialog modal-notify modal-warning modal-side modal-bottom-left" role="document">
                <!--Content-->
                <div class="modal-content">
                <!--Header-->
                <div class="modal-header">
                    <p class="heading">Modal Warning</p>

                    <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                    <span aria-hidden="true" class="white-text">&times;</span>
                    </button>
                </div>

                <!--Body-->
                <div class="modal-body">

                    <div class="row">
                    <div class="col-3 text-center">
                        <img src="https://mdbootstrap.com/img/Photos/Avatars/img%20(1).jpg" alt="IMG of Avatars"
                        class="img-fluid z-depth-1-half rounded-circle">
                        <div style="height: 10px"></div>
                        <p class="title mb-0">Jane</p>
                        <p class="text-muted " style="font-size: 13px">Consultant</p>
                    </div>

                    <div class="col-9">
                        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Fuga, molestiae provident temporibus
                        sunt earum.</p>
                        <p class="card-text"><strong>Lorem ipsum dolor sit amet, consectetur adipisicing elit.</strong></p>
                    </div>
                    </div>
                </div>

                <!--Footer-->
                <div class="modal-footer justify-content-center">
                    <a type="button" class="btn btn-warning">Get it now <i class="far fa-gem ml-1 white-text"></i></a>
                    <a type="button" class="btn btn-outline-warning waves-effect" data-dismiss="modal">No, thanks</a>
                </div>
                </div>
                <!--/.Content-->
            </div>
            </div>
            <!-- Central Modal Warning Demo-->

<div class="text-center">
  <a href="" class="btn btn-default btn-rounded" data-toggle="modal" data-target="#ModalWarning">Launch Modal
    Warning <i class="far fa-eye ml-1 text-white"></i></a>
</div>


    </div>
  <!-- <form @submit.prevent="sendFile">
      <label>Choose one image file to upload</label>
      <input type="file" v-on:change="postFile($event)" >
      <button type="submit">Upload</button>
  </form> -->
</template>

<script>
import axios from 'axios'

export default {
    data() {
        return {
            fileToUpload: null,
            isSuccess: false,
            imageAddress : 'https://media1.giphy.com/media/jwY3FBoIyb4Kx80FMS/giphy.gif'
        }        
    },
    methods: {
    upload: function () {
      console.log("ini file", this.fileToUpload);

      let data = new FormData()
      data.append("image", this.fileToUpload)

      axios({
        method: 'post',
        url: 'http://localhost:3000/files/upload-single',
        headers: {
            token: localStorage.getItem("token")
        },
        data
      })
        .then(result => {
            Swal.fire({
                position: 'center',
                icon: 'success',
                title: 'Successfully Upload Picture',
                showConfirmButton: false,
                timer: 1500
            })
            console.log(result);
        })
        .catch(( err ) => {
            Swal.fire({
              icon: 'error',
              title: 'Error while uploading pictures',
              text: 'Please upload again!'
            })
        })
    },
    changeFile() {
      this.fileToUpload = this.$refs.myFiles.files[0]
    }
  }
}
</script>

<style>
.btn {
  background-color : #392F5A;
  color : white;
}

.btn:hover {
    color: grey;
}
</style>