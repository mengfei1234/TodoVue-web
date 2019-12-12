<template>
    <div>
  <li @mouseenter="handleEnter(true)" @mouseleave="handleEnter(false)" :style="{background: bgColor}">
    <label>
      <input type="checkbox" v-model="todo.complete"/>
      <span>{{ todo.title }}</span>
    </label>
    <button class="btn btn-danger" v-show="isShow" @click="deleteItem">删除</button>
    <button class="btn btn-danger" v-show="isShow" @click="editeItem" >编辑</button>
  </li>
    <div v-if="modalBoolean"  >
        <!--<capa-model-one @on-close-cancel="onCloseCancel"></capa-model-one>-->
        <todo-modal @on-close-cancel="onCloseCancel"></todo-modal>
    </div>
    </div>
</template>

<script>
    import TodoModal from "./TodoModal";
    let toDoList;
    export default {
        props:{
          todo: Object,
          index: Number,
          deleteTodo:Function
        },
      data(){
          return{
            bgColor:'#FFB6C1',  //默认的背景颜色
            isShow: false  ,   //按钮默认是否显示
              modalBoolean:false,//模态框默认不显示
              inpVal:'',//输入框值
          }
      },
        components:{
            TodoModal,
            capaModelOne: resolve => {
                require(['./TodoModal'], resolve)
            },
    },
      methods:{
            //显示
          handleClearFiles(){
              // alert(111)
              this.modalBoolean=true;
              this.$emit('on-open-modal');
          },
          // 隐藏
          onCloseCancel(bool){
              // console.log(bool)
              this.modalBoolean=bool;
          },
        handleEnter(isEnter){
          if(isEnter){
            this.bgColor = '#aaaaaa';
            this.isShow = true
          }else{
            this.bgColor = 'white';
            this.isShow = false
          }
        },
        deleteItem(){
          const {todo,index,deleteTodo} = this;
          if(window.confirm(`确认删除${todo.title}吗？`)){
            deleteTodo(index)     //调用函数更新
          }
        },//删除
          editeItem(){
              const {todo,index,editeTodo} = this;
              // console.log(this.todo)

              // console.log(this.todo)
              // toDoList=this.todo;
              this.handleClearFiles();
          }//编辑
      }
    }
</script>

<style scoped>
  li {
    list-style: none;
    height: 36px;
    line-height: 36px;
    padding: 0 5px;
    border-bottom: 1px solid #ddd;
  }

  li label {
    float: left;
    cursor: pointer;
  }

  li label li input {
    vertical-align: middle;
    margin-right: 6px;
    position: relative;
    top: -1px;
  }

  li button {
    float: right;
    margin-top: 3px;
  }

  li:before {
    content: initial;
  }

  li:last-child {
    border-bottom: none;
  }
</style>
