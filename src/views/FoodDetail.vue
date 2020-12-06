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
          <img
            src="../assets/images/nasigoreng.jpg"
            class="img-fluid img-fooddetail shadow"
            width="100%"
          />
        </div>
        <div class="col-md-6">
          <h2>
            <strong>{{ product.nama }}</strong>
            <hr />
            <h4>
              Harga : <strong>Rp. {{ product.harga }}</strong>
            </h4>
            <form class="mt-4" v-on:submit.prevent>
              <div class="form-group">
                <input
                  type="number"
                  class="form-control"
                  placeholder="Jumlah Pesan"
                  v-model="keranjang.jumlah_pesan"
                />
              </div>
              <div class="form-group">
                <input
                  type="text"
                  class="form-control"
                  placeholder="keterangan : pedes, nasi setengah"
                  v-model="keranjang.keterangan"
                />
              </div>
              <div class="form-group">
                <input
                  type="text"
                  class="form-control"
                  placeholder="product ID"
                  v-model="keranjang.id_product"
                />
              </div>
              <button type="submit" class="btn btn-success" @click="pemesanan">
                <b-icon-cart></b-icon-cart> Pesan
              </button>
            </form>
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
      product: {},
      keranjang: {},
    };
  },

  methods: {
    setProducts(data) {
      this.product = data;
    },
    pemesanan() {
      if (this.keranjang.jumlah_pesan) {
        axios
          .post("http://127.0.0.1:8001/api/keranjang/store", this.keranjang)
          .then(() => {
            this.$router.push({ path: "/keranjang"})
            this.$toast.success("Sukses Masuk keranjang", {
              type: "success",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((err) => console.log(err));
      } else {
        this.$toast.error("Jumlah Pesan harus diisi", {
          type: "error",
          position: "top-right",
          duration: 3000,
          dismissible: true,
        });
      }
    },
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