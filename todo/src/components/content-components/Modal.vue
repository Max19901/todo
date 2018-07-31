<template>
  <div>
    <div class="modal-wrap" v-show="modal">
      <h2>{{ helloText }}</h2>
      <button @click="closeModal">Закрыть</button>
    </div>
  </div>
</template>

<script>
  import {eventBus} from "../../main";

  export default {
    name: "Modal",
    props: ['modalEvent'],
    data(){
      return{
        helloText: `Добро пожаловать, данное приложение поможет вам распланировать
        ваш день, поставить себе задачи на месяц и упорядочить все ваши дела`,
        modal: this.modalEvent
      }
    },
    methods: {
      closeModal(){
        this.modal = false;
        eventBus.$emit('modalBlock', this.modal);
        localStorage.accept = true;
      }
    }
  }

</script>

<style lang="scss" scoped>
  .modal-wrap{
    position: absolute;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 300px;
    box-shadow: 0px 0px 25px 2px rgba(0,0,0,0.47);
    top: 50%;
    padding: 20px;
    h2{
      font-size: 20px;
    }
    button{
      margin-top: 10px;
      width: 100%;
      border: none;
      background: #41b883;
      color: #fff;
      box-shadow: 0px 0px 10px 1px rgba(0,0,0,0.37);
    }
  }
</style>
