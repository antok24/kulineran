<template>
  <div class="container">
    <nav class="navbar navbar-expand-lg navbar-light">
      <a class="navbar-brand" href="#">Kulineran</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item">
            <router-link class="nav-link" to="/">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/foods">Foods</router-link>
          </li>
        </ul>

        <ul class="navbar-nav ml-auto">
          <li class="nav-item">
            <router-link class="nav-link" to="/keranjang"
              >Keranjang
              <b-icon-bag></b-icon-bag>
              <span class="badge badge-success ml-2">{{ jumlah_pesanan.length}}</span>
              </router-link>
          </li>
        </ul>
      </div>
    </nav>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Navbar",

  data() {
    return {
      jumlah_pesanan:[]
    };
  },
  methods: {
    setJumlah(data){
      this.jumlah_pesanan = data
    }  
  },
  mounted() {
    axios
      .get("http://127.0.0.1:8001/api/keranjang")
      .then((response) =>
        this.setJumlah(response.data.data))

      .catch((error) =>
        console.log(error))
  },

};
</script>

<style>
</style>