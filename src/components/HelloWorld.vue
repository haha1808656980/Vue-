<template>
  <div class="hello">
    <div class="box-wrap">
      <ul>
        <li v-for="item in prizeList" :key="item.id" :class="active == item.id ? 'active':''">
          <span v-if="item.id == 5"  @click="start">
            <img src="../assets/logo.png" alt="" style="width:160px;height:160px">
          </span>
          <span v-else>
            {{item.name}}
          </span>
        </li>
      </ul>
    </div>
    <div class="btn">
      <button  @click="start">开始</button>
      <button  @click="stop">停止</button>
      <button  @click="reset">重置</button>
    </div>
    
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      active:1,
      prizeList:[
        {id:1,name:'辣条'},
        {id:2,name:'方便面'},
        {id:3,name:'矿泉水'},
        {id:9,name:'电脑'},
        {id:5,name:'开始游戏'},
        {id:4,name:'电动车'},
        {id:8,name:'汽车'},
        {id:7,name:'手机'},
        {id:6,name:'水杯'},
      ],
      timer:'',
      luckObj:{},
      luck:false,
      isStart:false
    }
  },
  watch:{
    active(val){
      if(val == 10) {
        this.active = 1
      }
    }
  },
  mounted(){

  },
  methods:{
    start(){
      if(this.isStart){
        return
      }
      this.isStart = true
      this.timer= setInterval(() => {
        if(this.active == 4){
          this.active = 6
        }else {
          this.active++
        }
      },80)
    },
    stop(){
      clearInterval(this.timer)
      this.prizeList.forEach((obj) =>{
        if(this.active == obj.id){
          this.luckObj = obj
          this.isStart = false
          return
        }
      })

      console.log(this.luckObj.name)
    },
    reset(){
      if(this.timer){
        clearInterval(this.timer)
      }
      this.active = 1
    }
  }
}
</script>

<style scoped>
@keyframes shan {
  0%{
    border-color: rebeccapurple;
    transform: scale(1)
  }
  100%{
    border-color: red;
    transform: scale(1.1)
  }
}
.box-wrap ul li.active {
   border-color: rebeccapurple;
  animation: shan .3s ease 5;
}
.box-wrap{
  width: 600px;
  height:600px;
  margin: 0 auto;
}
.box-wrap ul {
  display: flex;
  flex-wrap: wrap;
  list-style: none;
}

.box-wrap ul li {
  background: pink;
  width: 160px;
  height: 160px;
  line-height: 160px;
  text-align: center;
  padding: 10px;
  border: 10px solid gold;
  border-radius: 10px;
}
.box-wrap ul li .start-btn {
  font-size: 24px;
  color: yellow;
  padding: 20px
}

.hello .btn{
  display: flex;
  justify-content: center;
  flex-wrap: nowrap;
  font-size: 24px
}

.hello .btn button {
  width: 100px;
  height: 50px;
  line-height: 50px;
  margin: 10px
}

</style>
