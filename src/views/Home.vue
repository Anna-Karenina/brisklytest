<template>
  <div class="container">
    <router-link to="/work">
      <img src="./../assets/brisklyLogo.svg" />
    </router-link>
  </div>
</template>


<style scoped>
.container{
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-content : center;
}
img{
 box-shadow:  
    0 4px 5px 0 rgba(0,0,0,0.14), 
    0 1px 10px 0 rgba(0,0,0,0.12), 
    0 2px 4px -1px rgba(0,0,0,0.3);
 padding: 1rem 2rem;
}
img:hover{
  transform: scale(1.1);
  transition: all 0.5s ease-in-out;
 }

</style>