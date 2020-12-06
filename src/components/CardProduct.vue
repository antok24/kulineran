<template>
  <div>
    <div class="card shadow card-product">
      <img src="../assets/images/nasigoreng.jpg" class="card-img-top" alt="Nasi Goreng" />
      <div class="card-body">
        <h5 class="card-title">{{product.nama}}</h5>
        <p class="card-text">
          <strong> {{ product.harga }} </strong>
        </p>
        <router-link :to="'/foods/'+product.id" class="btn btn-primary"><b-icon-cart></b-icon-cart> Pesan</router-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardProduct",
  props: ['product']
};
</script>

<style>
</style>