<template>
  <div class="food-detail">
    <Navbar />
    <div class="container">
      <div class="row mt-5">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/" class="text-dark">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link to="/foods" class="text-dark">Foods</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">
                Foods Order
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row">
        <div class="col-md-6">
          <img src="../assets/images/nasigoreng.jpg"  class="img-fluid img-fooddetail shadow" width="100%" /> 
        </div>
        <div class="col-md-6">
          <h2>
            <strong>{{ product.nama }}</strong>
            <hr>
            <h4>Harga : <strong>Rp. {{product.harga}}</strong></h4>

            
          </h2>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";

export default {
  name: "FoodDetail",
  components: {
    Navbar,
  },
  data() {
    return {
      product: {}
    }
  },

  methods: {
    setProducts(data) {
      this.product = data
    }
  },

  mounted() {
    axios
      .get("http://127.0.0.1:8001/api/products/" + this.$route.params.id)
      .then((response) => this.setProducts(response.data.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style>
</style>