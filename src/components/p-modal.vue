<template>
  <div class="mloading" v-if="mloading">
    <div></div>
  </div>

  <div class="p-modal">
    <div
      @click="this.$store.state.productmodal = false"
      class="p-modal-overlay"
    ></div>

    <div
      v-for="productdet in productdetails"
      :key="productdet"
      class="p-modal-card"
    >
      <div class="flex flex-col md:flex-row">
        <div class="p-modal-image w-1/1 md:w-5/12">
          <img :src="`${product.image}`" />
        </div>
        <div class="p-modal-info">
          <span class="p-modal-name">{{ product.name }}</span>

          <span class="p-modal-seller">Seller: {{ productdet.seller }}</span>
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
      product: "",
      productdetails: "",
      mloading: true,
    };
  },

  props: ["pid"],

  mounted() {
    this.getProduct();
    this.getProductDetails();
  },

  methods: {
    async getProduct() {
      const productres = await axios.get(
        `https://5f7301beb63868001615f226.mockapi.io/api/products/${this.pid}`
      );
      this.product = productres.data;
      this.mloading = false;
    },

    async getProductDetails() {
      const productdetres = await axios.get(
        `https://5f7301beb63868001615f226.mockapi.io/api/products/${this.pid}/product-details`
      );
      this.productdetails = productdetres.data;
      this.mloading = false;
    },
  },
};
</script>

<style lang="scss">
$radius: 10px;
$dark: rgb(65, 65, 65);

$cyan-lighter: #48fcfe;
$cyan-light: #54dbfd;
$cyan-normal: #3fffca;
$cyan-dark: #2a96b5;
$cyan-darker: #1d817f;

.mloading {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background-color: #1d817f6e;
  z-index: 1001;
  display: flex;
  justify-content: center;
  align-items: center;

  div {
    border: 3px dashed $cyan-normal;
    text-shadow: 1px 1px 0 $cyan-light, 1px 1px 10px $cyan-lighter;
    animation: mloading 2s infinite;

    width: 50px;
    height: 50px;
    border-radius: 50%;
  }
}

.p-modal {
  overflow: auto;
  position: fixed;
  display: flex;
  width: 100%;
  top: 0;
  left: 0;
  justify-content: center;
  z-index: 999;
  min-height: 100vh;
}

.p-modal-overlay {
  position: fixed;
  display: flex;
  width: 100%;
  top: 0;
  left: 0;
  z-index: 999;
  background-color: rgba(1, 1, 1, 0.9);
  min-height: 100vh;
}

.p-modal-card {
  width: 1000px;
  max-width: 95%;
  background-color: white;
  border-radius: $radius;
  display: flex;
  flex-direction: column;
  position: absolute;
  top: 5%;
  z-index: 1000;
  padding: 15px;

  .p-modal-image {
    max-width: 100%;

    img {
      border-radius: $radius;
      object-fit: contain;
    }
  }
}

.p-modal-info {
  display: flex;
  flex-direction: column;
  padding: 15px;
}

@keyframes mloading {
  0% {
    transform: scale(0.5) rotate(-360deg);
  }
  50% {
    transform: scale(2) rotate(0deg);
  }

  100% {
    transform: scale(0.5) rotate(360deg);
  }
}
</style>