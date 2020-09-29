<template>
 
 


  <div
    v-for="product in products"
    :key="product.id"
    class="product-card"
     @click="openmodal(product)"


  >
    <div class="product-card-overlay" >
      <i class="fas fa-search-plus"></i> Details
    </div>
    <img :src="`${product.image}`"    />
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

    <p-modal :pid="this.productid" v-if="this.$store.state.productmodal"></p-modal>
  <skeleton v-if="loading"> </skeleton>
</template>

<script>
import axios from "axios";
import skeleton from "./skeleton"
import pModal from "./p-modal"

export default {
  data() {
    return {
      products: '',
      loading: true,
      colorfilter:'olive',
    productid:'',
    };
  },
  mounted() {
this.getProduct();


  },



  methods:{
                async getProduct() {
      const productsres = await axios.get(
       `https://5f7301beb63868001615f226.mockapi.io/api/products`
      )
          this.products = productsres.data;
          this.loading = false;
    },

openmodal(product) {
  this.$store.state.productmodal = true;
  this.productid = product.id
 console.log(this.productid)
},
  
  },
  

  components: {
    skeleton,
    pModal
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
    z-index:600;  
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
    z-index:500;
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
