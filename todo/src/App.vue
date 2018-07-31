<template>
  <div id="app">
    <div class="header">
      <app-header></app-header>
    </div>
    <div class="container">
      <app-content></app-content>
    </div>
    <div class="footer">
      <app-footer></app-footer>
    </div>
  </div>
</template>

<script>

  import Header from './components/Header';
  import Content from './components/Content';
  import Footer from './components/Footer';


  export default {
    name: 'app',
    data() {
      return {}
    },
    components: {
      appHeader: Header,
      appContent: Content,
      appFooter: Footer
    }
  }
</script>

<style lang="scss">
  @import '../node_modules/bootstrap/scss/bootstrap.scss';
  body {
    font-family: sans-serif;
    padding: 0;
    margin: 0;
    position: relative;
    #app{
      display: flex;
      flex-direction: column;
      height: 100vh;
    }
  }
  .header{
    flex: 1;
  }
  .container{
    flex: 10;
  }
  .footer{
    display: flex;
    align-items: center;
    justify-content: center;
    flex: 1;
    box-shadow: 0px 5px 40px -1px rgba(0, 0, 0, 0.57);
    background-color: #fafafa;
  }
</style>
