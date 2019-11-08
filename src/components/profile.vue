<template>
  <div class="card-columns">
    <div v-for="pic in pictures" v-bind:key="pic.id">
      <div class="card" v-bind:picUrl="pic.id">
        <img :src="pic.url" class="card-img-top" alt="image" />
        <div class="card-body">
          <div class="row">
            <div class="col" id="pic-age">
              <strong>Detected age: {{ age }}</strong>
            </div>

            <div class="col" id="pic-keywords">
              <strong>Detected keywords:</strong>
              <ul>
                <div v-for="keyword in keywords" v-bind:key="keyword.id">
                  <li>
                    <strong>{{ keyword }}</strong>
                  </li>
                </div>
              </ul>
            </div>

            <div class="col" id="pic-quality">
              <strong>Picture quality: {{ (Number(quality)*100).toFixed() }}</strong>
            </div>
          </div>

          <div class="col">
            <button class="btn btn-info" @click="getAge(pic._id)">
              <span class="fa fa-plus-circle"></span>Get Age
            </button>

            <button class="btn btn-info" @click="getKeywords(pic._id)">
              <span class="fa fa-user"></span>Get Keywords
            </button>

            <button class="btn btn-info" @click="getQuality(pic._id)">
              <span class="fa fa-user"></span>Get quality
            </button>

            <button class="btn btn-danger" @click="deletePic(pic._id)">
              <span class="fa fa-user"></span>Delete
            </button>

            <button class="btn btn-info">
              <a :href="'https://twitter.com/intent/tweet?text=checkout+my+pic ' + pic.url" onclick="javascript:window.open(this.href, '', 'menubar=no,toolbar=no,resizable=yes,scrollbars=yes,height=600,width=600');return false;">Tweet</a>
            </button>

          </div>

        </div>
      </div>
    </div>
  </div>

</template>

<script>
import axios from "axios";

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
    }
  }
};
</script>

<style scoped>
button:hover {
  color: aliceblue;
}

button {
  margin: 2px;
}

a {
  color: white;
}

</style>