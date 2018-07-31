<template>
  <div class="list-block">
    <li :key="idIndex">
      <p>#{{idIndex +1}} {{listProp}}</p>
      <button class="delete" @click="removeList(index, false)">
        <font-awesome-icon icon="ban"></font-awesome-icon>
      </button>
      <button class="done" @click="removeList(index, true)">
        <font-awesome-icon icon="check-circle"></font-awesome-icon>
      </button>
    </li>
  </div>
</template>

<script>
  import {eventBus} from "../../main";

  export default {
    name: "List",
    props: ['list','lists', 'index'],
    data() {
      return {
        listProp: this.list.todo,
        idIndex: this.index,
        listsObj: this.lists,
        doneCount: localStorage.getItem('done') || 0,
        notDoneCount: localStorage.getItem('notDone') || 0,
      }
    },
    methods: {
      removeList(index, flg){
        console.log(index, flg);
        if (flg === true) {
          this.doneCount++;
          eventBus.$emit('done', this.doneCount);
        } else {
          this.notDoneCount++;
          eventBus.$emit('notDone', this.notDoneCount)
        }
        this.listsObj.splice(index,1);
        this.$emit('listsRemove', this.listsObj);
      }
    }
  }
</script>

<style lang="scss" scoped>
  .list-block {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  li {
    list-style-type: none;
    font-size: 1.5rem;
    background-color: #fafafa;
    width: 100%;
    text-align: center;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 55px;
    position: relative;
    transition: .5s;
    margin-bottom: 30px;
    box-shadow: 1px 3px 27px -6px rgba(0,0,0,0.51);
    p {
      padding: 0;
      margin: 0;
    }
    &:hover{
      button.change{
        opacity: 1;
        z-index: 1;
      }
    }
  }
  button {
    color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 38px;
    height: 38px;
    border: none;
    cursor: pointer;
    transition: .5s;
    &.done {
      background-color: #4CAF50;
      position: absolute;
      top: 0;
      right: 0;
      height: 100%;
      &:hover{
        background-color: #8BC34A;
      }
    }
    &.delete {
      background-color: #FF5252;
      position: absolute;
      top: 0;
      left: 0;
      height: 100%;
      &:hover{
        background-color: #F44336;
      }
    }
  }


</style>
