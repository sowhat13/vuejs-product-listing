<template>
  <div class="about">
<p>Used Vue.js, SCSS, Tailwind, MockAPI</p>

<a href="https://5f7301beb63868001615f226.mockapi.io/api/products/" target="_blank" ><i class="fas fa-external-link-alt"></i> Data of Products</a>
<br>
<a href="https://5f7301beb63868001615f226.mockapi.io/api/products/1/product-details" target="_blank" ><i class="fas fa-external-link-alt"></i> Data of Product Details First Item </a>
<br>
<a href="https://github.com/sowhat13/vuejs-product-listing" target="_blank" ><i class="fas fa-external-link-alt"></i> Github</a>

  <p><i class="fas fa-check"></i> Skeleton Loader</p>
  <p><i class="fas fa-check"></i> Modal Loader</p>
  <p><i class="fas fa-check"></i> Filter By Color</p>
  <p><i class="fas fa-check"></i> Sort By ID Number(There is a problem in MockAPI, its order id numbers like 91-90-9-89), Price, Publish Time </p>
   <p><i class="fas fa-check"></i> Responsive Design</p>
   <p><i class="fas fa-check"></i> Accesibility</p>
   <p><i class="fas fa-check"></i> Components</p>

 
  </div>
</template>
<style lang="scss">
.about
{
  padding:50px;
  p{
    i {
      color:rgb(65, 228, 65);
    }
  }

  a{color:blue;}
}
</style>