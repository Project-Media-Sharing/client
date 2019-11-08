<template>
  <div class="card-columns">
    <div v-for="pic in pictures" v-bind:key="pic.id">

      <cardImage :pic="pic" @getPicture="getPicture"></cardImage>

      </div>
    </div>
  </div>

</template>

<script>
import axios from "axios";
import cardImage from './cardImage.vue'

export default {
  data() {
    return {
      age: "",
      keywords: "",
      quality: "",
      picUrl: "",
      hrefTwitter: "https://twitter.com/intent/tweet?text=checkout+my+pic+$" + this.picUrl
    };
  },
  props: ["pictures", "user"],
  methods: {
    getAge(id) {
      console.log("ini id", id);
      
      axios({
        method: "get",
        url: `http://localhost:3000/files/${id}/image-age`,
        headers: {
          token: localStorage.getItem("token")
        }
      })
        .then(response => {
          this.age = response.data.faces[0].age.toFixed();
        })
        .catch(err => {
          console.log(err);
        });
    },
    getKeywords(id) {
      axios({
        method: "get",
        url: `http://localhost:3000/files/${id}/image-keywords`,
        headers: {
          token: localStorage.getItem("token")
        }
      })
        .then(response => {
          let arr = [];
          let keywords = response.data.keywords;
          for (let i = 0; i < 5; i++) {
            arr.push(keywords[i].keyword);
          } 
          this.keywords = arr;
        })
        .catch(err => {
          console.log(err);
        });
    },
    getQuality(id) {
      axios({
        method: "get",
        url: `http://localhost:3000/files/${id}/image-quality`,
        headers: {
          token: localStorage.getItem("token")
        }
      })
        .then(response => {
          this.quality = response.data.quality.score;
        })
        .catch(err => {
          console.log(err);
        });
    },
    deletePic(id) {
      axios({
        method: "delete",
        url: `http://localhost:3000/files/${id}/delete`,
        headers: {
          token: localStorage.getItem("token")
        }
      })
        .then(response => {
          this.$emit("getPicture");
          Swal.fire({
            position: "center",
            icon: "success",
            title: "Successfully Delete Picture",
            showConfirmButton: false,
            timer: 1500
          });
        })
        .catch(err => {
          console.log(err);
        });
    },
    getPicture() {
      this.$emit("getPicture")
    }
  },
  components: {
    cardImage
  }
};
</script>

<style scoped>

</style>