<template>
  <div class="card">
  </div>
</template>

<script>
  export default {
    name: "DefaultCard",
    data(){
      return {

      }
    }
  }
</script>

<style scoped>
  .card {
    width: 200px;
    height: 232px;
    border-radius: 5px;
    border: 1px solid #666;
    transition: box-shadow .5s;
    background-image: url("../assets/vue-js-egitim-background.jpg");
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;
    box-shadow: 0px 9px 55px #666;
  }

  .card img {
    width: 100%;
    height: 100%;
  }
</style>
