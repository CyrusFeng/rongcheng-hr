<template>
  <li :class="[isMain?'':'branch-style']">
    <div class="wrap" :class="[open?'wrap-open':'']" @click='toggle'>
      <div class="name">{{model.name}}</div>
      <div>

          <!--<i v-if='isFolder' class="hr-icon" :class="[open?'folder-open':'folder']"></i>-->
          <!--<i v-if='isFolder' class="hr-icon" :class="[open?'icon-rotate':'']"></i>-->
          <i v-if='isFolder' class="hr-icon" :class="[open?'icon-rotate':'',isMain?'icon-master':'icon-branch']"></i>
          　　　　　<!--isFolder判断是否存在子级改变图标-->
          <i v-if='!isFolder' class="hr-icon file-text"></i>

      </div>
    </div>

    <ul v-show="open" v-if='isFolder'>
      <items v-for='(cel,index) in model.children' :level="level+1" :key="index" :model='cel'></items>
    </ul>
  </li>
</template>

<script>
  export default {
    name: 'items',
    props:{
      model:Object,
      level:Number
    },
    components: {},
    data() {
      return {
        open: false,
        // isFolder: true,
      }
    },
    computed: {
      isFolder: function () {
        return this.model.children && this.model.children.length
      },
      isMain:function () {
        return this.level === 1
      },
    },
    methods: {
      toggle: function () {
        if (this.isFolder) {
          this.open = !this.open
        }
      },
    }
  }
</script>

<style scoped>
  li {
    font-size: 12px;
    /*border-bottom: 1px solid #ccc;*/
  }

  ul {
    margin-left: 1em;
    line-height: 1.5em;
    /*list-style-type: dot;*/
    list-style: none;
  }

  .wrap {
    padding-top: 0.08rem;
    padding-bottom: 0.08rem;
    padding-right: 0.12rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .wrap-open{
    border-bottom: 1px solid #ccc;
  }
.icon-master{
  background: url(../assets/renyuan.png) no-repeat;
  background-size: contain;
}
  .icon-branch{
    background: url(../assets/hr-tree-up.png) no-repeat;
    background-size: contain;
  }
  .hr-icon{
    display: block;
    width: 0.14rem;
    height: 0.14rem;
  }
  /*.folder-open{*/
    /*background: url(../assets/hr-tree-up.png) no-repeat;*/
    /*background-size: contain;*/
  /*}*/
  /*.folder{*/
    /*background: url(../assets/hr-tree-down.png) no-repeat;*/
    /*background-size: contain;*/
  /*}*/

  .icon-rotate {
    /*animation: rotate-in 1s;*/
    transform:rotate(180deg);
  }
  /*.icon-rotate-back {*/
    /*animation: rotate-in 1s reverse;*/
    /*!*transform:rotate(0deg);*!*/
  /*}*/
  /*@keyframes rotate-in {*/
    /*0% {*/
      /*transform:rotate(0deg);*/
    /*}*/
    /*100% {*/
      /*transform:rotate(180deg);*/
    /*}*/
  /*}*/
  .branch-style{
    font-size:0.1rem;
    color:#999999;
  }
</style>
