<template>

    <div>
        <div class="col-sm-10 offset-sm-1 pt-5">
            <div class="row">
                <div class="col-sm-6">
                    
                    <div class="card">
                        <img src="https://media1.giphy.com/media/jwY3FBoIyb4Kx80FMS/giphy.gif" class="card-img-top" alt="...">                      
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
                                            <div class="col-3 float-left px-1"><a href=""><img class="img-fluid" src="https://labs.everypixel.com/api/static/i/estest_sample1.jpg"></a></div>
                                            <div class="col-3 float-left px-1"><a href=""><img class="img-fluid" src="https://labs.everypixel.com/api/static/i/estest_sample2.jpg"></a></div>
                                            <div class="col-3 float-left px-1"><a href=""><img class="img-fluid" src="https://labs.everypixel.com/api/static/i/estest_sample3.jpg"></a></div>
                                            <div class="col-3 float-left px-1"><a href=""><img class="img-fluid" src="https://labs.everypixel.com/api/static/i/estest_sample4.jpg"></a></div>
                                        </div>
                                        <div class="carousel-item row no-gutters ">
                                            <div class="col-3 float-left px-1"><a href=""><img class="img-fluid" src="https://labs.everypixel.com/api/static/i/estest_sample5.jpg"></a></div>
                                            <div class="col-3 float-left px-1"><a href=""><img class="img-fluid" src="https://labs.everypixel.com/api/static/i/estest_sample3.jpg"></a></div>
                                            <div class="col-3 float-left px-1"><a href=""><img class="img-fluid" src="https://labs.everypixel.com/api/static/i/estest_sample4.jpg"></a></div>
                                            <div class="col-3 float-left px-1"><a href=""><img class="img-fluid" src="https://labs.everypixel.com/api/static/i/estest_sample5.jpg"></a></div>
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

                            
                        <div class="card-footer">       
                                <label>Choose one image file to upload</label>
                                <div class="form-group">
                                    <div class="custom-file">
                                        <input type="file" class="custom-file-input" id="customFile" v-on:change="postFile($event)">
                                        <label class="custom-file-label" for="customFile">Choose file</label>
                                    </div>
                                    <a href="" class="btn btn-primary mt-2" @submit.prevent="sendFile" >Upload Image</a>
                                </div>
                        </div>
                    </div>
                </div>
            </div>
      </div>
    </div>
  <!-- <form @submit.prevent="sendFile">
      <label>Choose one image file to upload</label>
      <input type="file" v-on:change="postFile($event)" >
      <button type="submit">Upload</button>
  </form> -->
</template>

<script>
export default {
    data() {
        fileToUpload: null;
        isSuccess: false;
    },
    methods: {
        sendFile() {
            console.log('sendFile invoked')
            let bodyFromData = new FormData();
            bodyFromData.set('image', this.fileToUpload);
            axios({
                method: "POST",
                url: "",

            })
            .then(( response ) => {
                this.isSuccess = true;
            
            })
            .catch(( err ) => {
                console.log(err.response)
            })
        },
        postFile(event) {
             console.log('postFile invoked')
            this.fileToUpload = event.target.files[0]
        }
    }
}
</script>

<style>

</style>