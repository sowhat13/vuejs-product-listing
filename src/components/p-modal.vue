<template>
  <div class="mloading" v-if="mloading">
    <div class="spinner"></div>
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
        <div class="p-modal-info w-1/1 md:w-5/12">
          <span class="p-modal-name">{{ product.name }}</span>

          <span class="p-modal-seller ">by {{ productdet.seller }}</span>



          <span class="p-modal-price">{{ product.price }} $</span>

          <span class="p-modal-attr">
            <i class="fas fa-check-double"></i>
             {{ productdet.attribute }}</span>

          <span class="p-modal-desc">
            <p>Description</p>
            
          <span> {{ productdet.productdesc }}</span>  </span>

<div class="p-modal-buy">
<button class="addtocart"><i class="fas fa-shopping-cart"></i> Add To Cart</button>  

<button class="buynow">
  <i class="fas fa-money-check"></i>
  Buy Now</button>  


</div>
        </div>
        <div class=" p-modal-info2 w-1/1 md:w-2/12">

        <span class="p-modal-time mt-auto ml-auto">
          {{ product.createdAt.slice(8, 10) }}.{{
            product.createdAt.slice(5, 7)
          }}.{{ product.createdAt.slice(0, 4) }}</span
        >
      </div>
      </div>
<span class="close-modal">
        <i
           @click="this.$store.state.productmodal = false"
         class="fas fa-times"></i></span>
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
$redish:rgb(255, 141, 141);
$redish-dark:rgb(245, 124, 124);
$shadow:0 0 5px 1px rgba(0, 0, 0, 0.234);

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

  .spinner {
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
  margin: 5%;
  z-index: 1000;
  padding: 15px;

.close-modal{
  position:absolute;
  right:1%;
  top:1%;
  font-size:18px;
  background-color:gray;
  width:24px;
  height:24px;
  border-radius:50%;
  color:white;
  display:flex;
  justify-content: center;
  align-items: center;
  cursor:pointer;
}

  .p-modal-image {
    max-width: 100%;

    img {
      border-radius: $radius;
      object-fit: contain;
    }
  }

  .p-modal-name {
    font-size: 24px;
    letter-spacing: 0.3px;
    color: $cyan-normal;
    font-weight: 500;
  }
  .p-modal-attr{
       font-size: 16px;
    color: $redish;
    font-weight: 400;
  }

  .p-modal-seller {
    font-size: 12px;
    color: rgb(155, 155, 155);
    font-weight: 400;
  }

  .p-modal-price {
    font-size: 26px;
    letter-spacing: 0.3px;
    color: $cyan-darker;
    margin: 10px 0;
  }

    .p-modal-desc {
    font-size: 15px;
    color: rgb(155, 155, 155);
    margin:10px 0;


    p{
          font-size: 16px;
         
          padding-left:3px;
          font-weight: 500;
          margin-bottom:3px;
        
    }
   span {
   padding-top:1px;
   } 
  }

  .p-modal-time {
    font-size: 12px;
    color: gray;
  }
}

.p-modal-info {
  display: flex;
  flex-direction: column;
  padding: 15px;
}

.p-modal-info2 {
  display: flex;
  flex-direction: column;
  padding: 15px;
}

.p-modal-buy{
  margin-top:auto;
  *{
margin-top:auto;
  
    padding:5px 10px;
  }

  .addtocart{
    background-color:$redish;
    border-radius:5px;
    border:2px solid $redish-dark;
    color:white;
    margin-right:20px;
  }
  .addtocart:hover{
    background-color:$redish-dark;
    border:2px solid $redish-dark;
    color:white;
  box-shadow:$shadow;

  }

  .addtocart:active{
    transform:scale(0.98);
  }


    .buynow{
    border-radius:5px;
    border:2px solid $redish-dark;
color:$redish;
 
  margin-top:20px !important;
  }

     .buynow:hover{
    border:2px solid $redish-dark;
color:white;
 background-color:$redish-dark;
  box-shadow:$shadow;

  }

  .buynow:active{
    transform:scale(0.98);
  }
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