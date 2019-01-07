<template>
  <div>
    <div class="vux-demo">
      <img class="logo blur" src="../assets/vux_logo.png">
      <div class="content">women</div>
    </div>
    <sticky>
      <tab>
        <tab-item disabled class="all-tab">
          <span class="all">全部</span>
        </tab-item>
        <tab-item @on-item-click="handler" v-for="(v, k) in list" v-bind:key=k+1>{{v.name}}</tab-item>
      </tab>
    </sticky>
    
    
    <!-- <group title="cell demo">
      <cell title="VUX" value="cool" is-link></cell>
    </group> -->
    <p v-for="i in num" v-bind:key=i>{{i + labelName}}<br></p>
  </div>
</template>

<script>
import { Group, Cell, Tab, TabItem, Sticky } from 'vux'

export default {
  components: {
    Group,
    Cell,
    Tab,
    TabItem,
    Sticky
  },
  data () {
    return {
      // note: changing this line won't causes changes
      // with hot-reload because the reloaded component
      // preserves its current state and we are modifying
      // its initial state.
      msg: 'Hello World!',
      list: [],
      num: 100,
      labelName: '',
    }
  },
  created(){
    for (let index = 0; index < 10; index++) {
      this.list.push({
        name: '标签'+ index
      })
    }
  },
  methods: {
    handler: function(index){
      this.labelName = this.list[index].name
    }
  }
}
</script>

<style>
.vux-demo {
  text-align: center;
  position: relative;
}
.logo {
  width: 100px;
  height: 100px
}
.all{
  font-size: .12rem;
  color: gray;
}
.blur {	
    filter: blur(10px);
}
.content{
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
</style>
