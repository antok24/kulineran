<template>
  <div>
    <Navbar />
    <div class="container">
      <div class="row mt-4">
        <div class="col">
          <h2>Daftar <strong>Makanan</strong></h2>
        </div>
      </div>

      <div class="row mt-3">
        <div class="col">
          <div class="input-group mb-3">
            <input
            v-model="search"
              type="text"
              class="form-control"
              placeholder="mau makan apa hari ini ?"
              aria-label="Cari Makanan"
              aria-describedby="basic-addon1"
              @keyup="searchFood"
            />
            <div class="input-group-prepend">
              <span class="input-group-text" id="basic-addon1"
                ><b-icon-search></b-icon-search
              ></span>
            </div>
          </div>
        </div>
      </div>

      <div class="row mb-4">
        <div
          class="col-md-3 mt-4"
          v-for="product in products"
          :key="product.id"
        >
          <CardProduct :product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import CardProduct from "@/components/CardProduct.vue";
import axios from "axios";

export default {
  name: "Foods",
  components: {
    Navbar,
    CardProduct,
  },
  data() {
    return {
      products: [],
      search: "",
    };
  },
  methods: {
    setProduct(data) {
      this.products = data;
    },
    searchFood() {
      axios
        .get("http://127.0.0.1:8001/api/products?q="+this.search)
        .then((
          response // console.log(response.data))
        ) => this.setProduct(response.data.data))

        .catch((error) => console.log(error));
    },
  },
  mounted() {
    axios
      .get("http://127.0.0.1:8001/api/products")
      .then((
        response // console.log(response.data))
      ) => this.setProduct(response.data.data))

      .catch((error) => console.log(error));
  },
};
</script> 

<style>
</style>