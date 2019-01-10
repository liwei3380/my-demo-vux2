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
    <div v-for="i in movieList" v-bind:key=i>
      <cell
      :title=i.title
      is-link
      :border-intent="false"
      :arrow-direction="i.show ? 'up' : 'down'"
      @click.native="i.show = !i.show"></cell>

      <p class="slide" :class="i.show?'animate':''">blablabla...<br/>blablabla...<br/>blablabla...<br/>blablabla...</p>
    </div>
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
      movieList: [],
      showContent004: false,
    }
  },
  created(){
    for (let index = 0; index < 10; index++) {
      this.list.push({
        name: '标签'+ index
      })
    }
    this.axiosFun({start: 25,count: 25})
  },
  methods: {
    handler: function(index){
      this.labelName = this.list[index].name
      this.axiosFun({start: index,count: 25})
    },
    axiosFun: function(params){
      this.$axios.get('/api/v2/movie/top250',{params: params}).then((data)=>{
          this.movieList = data.data.subjects
      }).catch((err)=>{
          console.log(err)
      })
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
.slide {
  padding: 0 20px;
  overflow: hidden;
  max-height: 0;
  transition: max-height .5s cubic-bezier(0, 1, 0, 1) -.1s;
}
.animate {
  max-height: 9999px;
  transition-timing-function: cubic-bezier(0.5, 0, 1, 0);
  transition-delay: 0s;
}
</style>
