<template>
  <div class="skeletoncredit h-full w-full  mx-auto flex"
  
   v-for="skeletoncount in 8"
      :key="skeletoncount">

    

      <div class="s-profile-name mx-auto"></div>
    </div>
</template>

<script>
export default {};
</script>

<style lang="scss">
$lightercolor: rgb(232, 232, 232);
$lightcolor: rgb(206, 206, 206);

$radius: 10px;
$margin: 10px;





.s-profile-name {
      display: flex;
  flex-direction: column;
  width:75%;
  margin: 15px auto;
  height: 275px;

    display:flex;

  background-image: linear-gradient(45deg,

    $lightcolor 0%,
    $lightercolor 25%,
    $lightcolor 50%,
 

    $lightcolor 50%,
    $lightercolor 75%,
    $lightcolor 100%
  );
  background-repeat: repeat;
  background-size: cover ;
  border-radius: 10px;
  animation: placeholderShimmer 3s linear infinite;
}

@keyframes placeholderShimmer {
  0% {
    background-position: 0px ;
  }

  100% {
    background-position: 269px ;
  }
 
}
</style>