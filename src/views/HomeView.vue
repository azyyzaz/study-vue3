<template>
  <div class="home">
    <h2>{{ count }}</h2>
    <button @click="btnClick">累加</button>
    <button @click="reduceClick">递减</button>
    <h2>{{ name }}</h2>
    <button @click="changeName">改名</button>

    <ChildrenView />
    <Suspense>
      <template #default>
        <PendingView />
      </template>
      <template #fallback>
        <p>玩命加载中...</p>
      </template>
    </Suspense>
    <button @click="editNum">修改子组件值</button>
  </div>
  <!-- 这里使用的teleport 只能是在index.html 中的#app 同级 -->
  <!-- teleport 传送门 样式不是共用的 -->
  <teleport to="#test">
    <ChildrenView />嘤嘤嘤
    <p>这段话是渲染在#test中的--1</p>
  </teleport>
  <div>我爱罗</div>
  <div>真刀真枪</div>
</template>
<style lang="stylus">
#test
  display: flex
  justify-content: center
  align-items: center
  color red
</style>
<script lang="js">
import { ref,reactive,toRefs,provide,nextTick  } from "vue";
import ChildrenView from "./ChildrenView.vue";
import PendingView from "./PendingView.vue";
export default {
  components: {
    ChildrenView,
    PendingView
  },
  methods: {
    btnClick() {
      this.count++;
    },
  },
  setup() {
    nextTick(() =>{
      //和DOM有关的一些操作
    })
    const obj = reactive({name:'yangjinshan'})
    const changeName = () =>{
     obj.name =  obj.name === "yangyouzhang" ? 'yangjinshan':'yangyouzhang'
    }
    const num = ref(999);
    const editNum = ()=>{
      num.value =1024
    }
    provide("num",num);
    // 通过toRefs方法
    let refObj = toRefs(obj);
    return {...clickFn(), obj,changeName,...refObj,editNum}
  },
};
function clickFn() {
  const count = ref(20);
  const addClick = () =>{
    count.value++;
  }
  const reduceClick = () =>{
    count.value--;
  }
  return{ count,addClick,reduceClick}
}
</script>
