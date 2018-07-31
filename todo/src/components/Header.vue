<template>
    <div class="header-wrap">
      <div class="header-wrap-logo">
        <img src="../assets/logo.png" alt="">
      </div>
      <div class="header-wrap-title">
        <h1>TODO</h1>
      </div>
    </div>
</template>

<script>
    export default {
        name: "Header"
    }
</script>

<style lang="scss" scoped>
  .header-wrap{
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    box-shadow: 0px 5px 40px -1px rgba(0,0,0,0.57);
    padding: 20px 0;
    background-color: #fafafa;
    &-logo {
       width: 45px;
       height: 45px;
      img{
        height: 100%;
      }
     }
  }
</style>
