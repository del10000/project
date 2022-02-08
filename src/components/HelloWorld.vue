<template>
  <div class="">
    <div class="row">
      <div class="col-3" :key="index" v-for="(tshirts, index) in tshirt">
        <span style="position: relative; top: 25px; z-index:1;" class="badge badge-danger"> {{tshirts.flag}}</span>
        <div class="card my-3" style="min-height: 25rem">
          <img class="card-img-top" :src="tshirts.imageURL" alt="Card image cap">
            <div class="card-body">
            <h5 class="card-title">{{ tshirts.name }}</h5>
            <button v-on:click="getProduct(tshirts.id)" class="btn btn-primary">See tshirt</button>
          </div>
        </div>
      </div>
    </div>

    <nav aria-label="Page navigation example">
      <ul class="pagination d-flex justify-content-center">
        <!-- <li class="page-item"><button class="page-link" v-on:click="previousPage">Previous</button></li> -->
        <li class="page-item"><button class="page-link" v-on:click="getPage(1)">1</button></li>
        <li class="page-item"><button class="page-link" v-on:click="getPage(2)">2</button></li>
        <li class="page-item"><button class="page-link" v-on:click="getPage(3)">3</button></li>
        <li class="page-item"><button class="page-link" v-on:click="getPage(4)">4</button></li>
        <li class="page-item"><button class="page-link" v-on:click="getPage(5)">5</button></li>
        <!-- <li class="page-item"><button class="page-link" v-on:click="nextPage">Next</button></li> -->
      </ul>
    </nav>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HelloWorld',
  data(){
    return{
      tshirt: null,
      page: 1
    }
  },

  mounted(){
    axios
    .get('http://vps-a47222b1.vps.ovh.net/TShirt/page/1')
    .then(response => {
      this.tshirt = response.data
    console.log(this.tshirt)
    });
  },

  methods: {
    getPage(page){
      axios.get('http://vps-a47222b1.vps.ovh.net/TShirt/page/' + page)
      .then(response => {
        this.tshirt = response.data
      console.log(this.tshirt)
      });
    },

    previousPage(){
      if (this.page > 1) {
      this.page--
      axios.get('http://vps-a47222b1.vps.ovh.net/TShirt/page/' + this.page)
      .then(response => {
        this.tshirt = response.data
      console.log(this.tshirt)
      });
        console.log(this.page)
      }
    },

    nextPage(){
      if (this.page <= 5) {
        this.page++
      axios.get('http://vps-a47222b1.vps.ovh.net/TShirt/page/' + this.page)
      .then(response => {
        this.tshirt = response.data
      console.log(this.tshirt)
      });
        console.log(this.page)
      }
    },

    getProduct(id){
      axios.get('http://vps-a47222b1.vps.ovh.net/TShirt/' + id)
      .then(response => {
        this.tshirt = response.data
      console.log(this.tshirt)
      });
    }


  },

  created() {
    fetch('http://vps-a47222b1.vps.ovh.net/TShirt/${this.$route.id}')
  }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
