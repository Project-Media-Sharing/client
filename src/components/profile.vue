<template>
	<div class="row">
		<div class="col-md-offset-2 col-md-8 col-lg-offset-3 col-lg-6">
    	 <div class="well profile">
            <div class="col-sm-12">
                <div class="col-xs-12 col-sm-8">
                    <h2>{{ user }}</h2>
                </div>             
            </div>            
            <div class="col-xs-12 divider text-center">
            	<div class="col-xs-12 col-sm-4 text-center" v-for="pic in pictures"> <!-- looping v-for setiap procpic dari user -->
                    <figure>
                        <img :src="pic.url" alt="" class="img-circle img-responsive">
                    </figure>
                    <div class="col-xs-12 col-sm-4 emphasis">
                    	<button class="btn btn-success btn-block" @click="getAge(pic._id)"><span class="fa fa-plus-circle"></span>Get Age</button>
                    	<h2><strong>{{ age }}</strong></h2>
                	</div>
                	<div class="col-xs-12 col-sm-4 emphasis">
                    	<button class="btn btn-info btn-block" @click="getKeywords(pic._id)"><span class="fa fa-user"></span>Get Keywords</button>
                    	<div v-for="keyword in keywords">
                    		<h2><strong>{{ keyword }}</strong></h2>
                    	</div>
                	</div>
                	<div class="col-xs-12 col-sm-4 emphasis">
                    	<button class="btn btn-info btn-block" @click="getQuality(pic._id)"><span class="fa fa-user"></span>Get quality</button>
                    	<h2><strong>{{ (Number(quality)*100).toFixed() }}%</strong></h2>
                	</div>
                	<div class="col-xs-12 col-sm-4 emphasis">
                    	<button class="btn btn-info btn-block" @click="deletePic(pic._id)"><span class="fa fa-user"></span>Delete</button>
                	</div>
                </div>
            </div>
    	 </div>                 
		</div>
	</div>
</template>

<script>

import axios from 'axios';

export default {
	data() {
		return {
			age: "",
			keywords: "",
			quality: ""
		}
	},
	props: ['pictures', 'user'],
	methods: {
		getAge(id) {
			axios({
	          method: 'get',							
	          url : `http://localhost:3000/files/${id}/image-age`,
	          headers: {
	          	token: localStorage.getItem("token")
	          }
	      	})
	      	.then(response => {
	        	this.age = response.data.faces[0].age.toFixed();
	    	})
	      	.catch(err => {
	      		console.log(err);
  			})
		},
		getKeywords(id) {
			axios({
	          method: 'get',						
	          url : `http://localhost:3000/files/${id}/image-keywords`,
	          headers: {
	          	token: localStorage.getItem("token")
	          }
	      	})
	      	.then(response => {
	      		let arr = [];
	      		let keywords = response.data.keywords;
	      		for(let i=0; i<5; i++) {
	      			arr.push(keywords[i].keyword)
	      		}
	        	this.keywords = arr;
	    	})
	      	.catch(err => {
	      		console.log(err);
  			})
		},
		getQuality(id) {
			axios({
	          method: 'get',						
	          url : `http://localhost:3000/files/${id}/image-quality`,
	          headers: {
	          	token: localStorage.getItem("token")
	          }
	      	})
	      	.then(response => {
	        	this.quality = response.data.quality.score;
	    	})
	      	.catch(err => {
	      		console.log(err);
  			})
		},
		deletePic(id) {
			axios({
	          method: 'delete',						
	          url : `http://localhost:3000/files/${id}/delete`,
	          headers: {
	          	token: localStorage.getItem("token")
	          }
	      	})
	      	.then(response => {
	        	Swal.fire({
		            position: 'center',
		            icon: 'success',
		            title: 'Successfully Delete Picture',
		            showConfirmButton: false,
		            timer: 1500
		        })
	    	})
	      	.catch(err => {
	      		console.log(err);
  			})
		}
	}
}
</script>

<style>
</style>