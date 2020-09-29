<template>
  <div class="home">
    <div class="grid grid-cols-1 md:grid-cols-3 ">
      <product></product>
         
    </div>

    <!-- 
      <div id="filters" class="filters">
        <form>
  <fieldset>
  <label for="all">All 
  <input type="radio" id="all" name="color" value="all" checked>
  </label>
  <label for="red">Red 
  <input type="radio" id="red" name="color" value="red">
  </label>
   <label for="blue">Blue 
  <input type="radio" id="blue" name="color" value="blue">
  </label>
  </fieldset>
  </form>
   </div> -->
  </div>
</template>

<script>
// @ is an alias to /src
import product from "@/components/product.vue";

export default {
  components: {
    product,
  },
};
</script>
