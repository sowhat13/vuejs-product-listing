<template>
  <div id="nav">
    <router-link to="/">Store</router-link> 
    <router-link to="/foo">Foo</router-link>
  </div>
  <router-view/>
</template>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Rubik:ital,wght@0,400;0,500;0,600;0,700;0,800;1,300;1,400;1,500;1,600;1,700&display=swap');
body{
  font-family: 'Rubik', sans-serif;
overflow-x:hidden;
}

#nav {
  display:flex;
width:100%;
padding:15px;
background-color:cyan;
justify-content: center;
align-items: center;
color:white;
font-weight:700;
font-size:18px;
*{
  margin:0 10px;
}

*:hover{
   text-shadow:1px 1px 10px #a3a3a3 !important;
}

.router-link-active {
 text-shadow:1px 1px 5px #686868;
}
}
</style>
