<template>
  <li
    :style="{backgroundColor:bgColor,color:fontColor}"
    @mouseenter="enterHandler(true)"
    @mouseleave="enterHandler(false)"
  >
    <label>
      <input type="checkbox" v-model="isCompleted" />
      <span>{{todo.title}}</span>
    </label>
    <button class="btn btn-danger" v-show="isDisplay" @click="del">删除</button>
  </li>
</template>
<script>
export default {
  computed: {
    //get操作和set操作
    isCompleted:{
      //获取了一个todo对象.把该todo对象中的isShow属性值直接反给isCompleted属性
      get(){
        return this.todo.isShow
      },
      set(val){
        //如果何止了isCompleted属性的值,此时val就是设置的值(选中了:true,没选中:false)
        //设置当前的todo的isShow
        this.toggleTodo(this.todo)
      }
    }
  },
  methods: {
    //删除操作
    del() {
      if (confirm("您确定删除吗")) {
        this.deleteTodo(this.index);
      }
    },
    //鼠标进入和离开操作
    enterHandler(isEnter) {
      //如果是true则表示鼠标进入,如果是false则表示鼠标离开
      if (isEnter) {
        this.bgColor = "gray";
        this.fontColor = "pink";
        this.isDisplay = true;
      } else {
        this.bgColor = "white";
        this.fontColor = "black";
        this.isDisplay = false;
      }
    }
  },
  data() {
    return {
      //设置前景和背景颜色
      bgColor: "white",
      fontColor: "black",
      isDisplay: false
    };
  },
  props: {
    index: Number,
    todo: Object,
    deleteTodo: Function,
    toggleTodo: Function
  }
};
</script>
<style scoped>
/*item*/
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
  /* display: none; */
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}
</style>