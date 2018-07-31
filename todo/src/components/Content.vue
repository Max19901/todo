<template>
  <div class="container-wrap">
    <app-modal :modalEvent="modalShow"></app-modal>
    <app-add-list :lists="lists" @listsEdit="lists = $event"></app-add-list>
    <div class="list-wrap">
      <div class="status">
        <p class="notDone">Невыполнено: <span>{{notDone}}</span></p>
        <p class="done">Выполнено: <span>{{done}}</span></p>
      </div>
      <ul>
        <app-list v-for="(list, index) in lists"
                  :list="list"
                  :index="index"
                  :lists="lists"
                  :key="index"
                  @listsRemove="lists = $event"></app-list>
      </ul>
    </div>
  </div>
</template>

<script>
  import Modal from './content-components/Modal';
  import List from './content-components/List';
  import AddList from './content-components/AddList';
  import {eventBus} from "../main";

  export default {
    name: "Content",
    components: {
      appModal: Modal,
      appList: List,
      appAddList: AddList
    },
    data() {
      return {
        modalShow: false,
        lists: JSON.parse(localStorage.getItem('todoList')) || [],
        done: localStorage.getItem('done') || 0,
        notDone: localStorage.getItem('notDone') || 0
      }
    },
    created() {

      if (localStorage.getItem('accept')){
        this.modalShow = false;
      } else {
        this.modalShow = true;
      }
      eventBus.$on('modalBlock', (data)=>{
        this.modalShow = data;
      });
      eventBus.$on('done', (count)=>{
        this.done = count;
        localStorage.done = this.done
      });
      eventBus.$on('notDone', (count)=>{
        this.notDone = count;
        localStorage.notDone = this.notDone
      })
    },
    watch: {
      lists: function () {
        localStorage.todoList = JSON.stringify(this.lists);
      }
    }
  }
</script>

<style lang="scss" scoped>
  .container-wrap {
    padding: 0 20px;
  }
  .status {
    display: flex;
    justify-content: space-around;
    .notDone span {
      color: red;
      font-weight: bold;
    }
    .done span {
      color: green;
      font-weight: bold;
    }
  }
</style>
