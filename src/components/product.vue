<template>
  <pfilter class="filter-sticky" @clicked="onClickChild"></pfilter>

  <div class="grid grid-cols-1 md:grid-cols-4">
    <div
      v-for="product in products"
      :key="product.id"
      class="product-card"
      @click="openmodal(product)"
    >
      <div class="product-card-overlay">
        <i class="fas fa-search-plus"></i> Details
      </div>
      <img :src="`${product.image}`" />

      <div
        class="product-card-color ml-auto"
        :style="` background-color:${product.color} `"
      ></div>

      <div class="p-3 h-full flex flex-col">
        <span class="product-card-name flex items-center">
          {{ product.name }}
        </span>
        <span class="product-card-price">{{ product.price }} $</span>

        <div class="product-card-footer">
          <div class="product-card-time">
            {{ product.createdAt.slice(8, 10) }}.{{
              product.createdAt.slice(5, 7)
            }}.{{ product.createdAt.slice(0, 4) }}
          </div>
        </div>
      </div>
    </div>
    <skeleton v-if="loading"> </skeleton>
  </div>

  <p-modal
    :pid="this.productid"
    v-if="this.$store.state.productmodal"
  ></p-modal>
</template>

<script>
import axios from "axios";
import skeleton from "./skeleton";
import pModal from "./p-modal";
import pfilter from "./p-filter";

export default {
  data() {
    return {
      products: "",
      loading: true,
      isFirst: true,
      productid: "",
    };
  },
  mounted() {
    this.onClickChild();
  },

  methods: {
    async onClickChild(value) {
      let url = "";
      if (this.isFirst) {
        url = `https://5f7301beb63868001615f226.mockapi.io/api/products`;
      } else {
        url = `https://5f7301beb63868001615f226.mockapi.io/api/products?color=${value.selectedcolor}&sortBy=${value.sortby}&order=${value.orderby}`;
      }
      const productsres = await axios.get(url);
      this.products = productsres.data;
      this.loading = false;
      this.isFirst = false;
    },

    openmodal(product) {
      this.$store.state.productmodal = true;
      this.productid = product.id;
    },
  },

  components: {
    skeleton,
    pModal,
    pfilter,
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

.filter-sticky {
  position: sticky;
  top: 0;
  left: 0;
  z-index: 601;
}

.product-card {
  display: flex;
  flex-direction: column;
  width: 75%;
  margin: 15px auto;
  position: relative;
  border-radius: $radius;
  box-shadow: 0 0 3px 1px rgba(1, 1, 1, 0.1);
  height: 275px;
  cursor: pointer;

  .product-card-overlay {
    background-color: rgba(255, 255, 255, 0.5);
    border-radius: $radius;
    position: absolute;
    width: 100%;
    height: 100%;
    display: none;
    justify-content: center;
    align-items: center;
    color: $cyan-normal;
    font-size: 40px;
    text-shadow: 1px 1px 3px rgba(1, 1, 1, 0.5);
    font-weight: 600;
    flex-direction: column;
    z-index: 600;
  }

  .product-card-name {
    font-size: 18px;
    letter-spacing: 0.3px;
    color: $cyan-normal;
    font-weight: 500;
  }

  .product-card-price {
    font-size: 16px;
    margin: 5px 8px;
    letter-spacing: 0.3px;
    color: $cyan-darker;
  }

  img {
    height: 150px;
    border-radius: 10px 10px 0 0;
    width: 100%;
    object-fit: cover;
  }

  .product-card-color {
    width: 12px;
    height: 12px;
    white-space: nowrap;
    border-radius: 50%;
    color: white;
    text-shadow: 1px 1px black;
    // box-shadow: 0 0 0 1px rgb(255, 255, 255), 0 0 3px 1px rgba(0, 0, 0, 0.302);;
    position: absolute;
    top: 15px;
    right: 15px;
    z-index: 500;
  }

  .product-card-footer {
    margin-top: auto;
    margin-left: 3px;
    margin-right: 3px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
  }

  .product-card-time {
    font-size: 12px;
    color: gray;
  }
}

.product-card:hover {
  .product-card-overlay {
    display: flex;
  }
}
</style>
