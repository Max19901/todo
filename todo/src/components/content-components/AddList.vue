<template>
  <div>
    <button @click="showInput">Добавить действие</button>
    <div v-show="change">
      <input type="text" v-model="defaultList.todo">
      <button @click="addList">Добавить</button>
    </div>
  </div>
</template>

<script>
  export default {
    name: "AddList",
    props: ['lists'],
    data(){
      return{
        objLists: this.lists,
        defaultList: {
          todo: 'Some Text'
        },
        change: false
      }
    },
    methods:{
      showInput(){
        this.change = !this.change;
      },
      addList(){
        this.objLists.push(this.defaultList);
        this.$emit('listsEdit', this.objLists);
        this.change = !this.change;
      }
    }

  }
</script>

<style lang="scss" scoped>
  div {
    text-align: center;
    margin-top: 50px;
    margin-bottom: 20px;
    button {
      border: none;
      padding: 10px 15px;
      background-color: #455A64;
      color: #fff;
      transition: .3s;
      &:hover {
        transform: translateY(-10%);
        cursor: pointer;
      }
    }
  }
</style>
