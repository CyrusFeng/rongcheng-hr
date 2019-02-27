<template>
  <ul class="tree-wrap">
    <items :model='model' v-for="(model,index) in data" :level="1" :key="index"></items>
  </ul>
</template>

<script>
  import items from './items'

  var data = [
    {
      name: 'My Tree',
      children: [
        { name: 'hello' },
        { name: 'wat' },
        {
          name: 'child folder',
          children: [
            {
              name: 'child folder',
              children: [
                { name: 'hello' },
                { name: 'wat' }
              ]
            },
            { name: 'hello' },
            { name: 'wat' },
            {
              name: 'child folder',
              children: [
                { name: 'hello' },
                { name: 'wat' }
              ]
            }
          ]
        }
      ]
    },
    {
      name: 'My Tree',
      children: [
        { name: 'hello' },
        { name: 'wat' },
        {
          name: 'child folder',
          children: [
            {
              name: 'child folder',
              children: [
                { name: 'hello' },
                { name: 'wat' }
              ]
            },
            { name: 'hello' },
            { name: 'wat' },
            {
              name: 'child folder',
              children: [
                { name: 'hello' },
                { name: 'wat' }
              ]
            }
          ]
        }
      ]
    },
    {
      name: 'child folder',
      children: [
        {
          name: 'child folder',
          children: [
            {
              name: 'child folder',
              children: [
                { name: 'hello' },
                { name: 'wat' }
              ]
            },
            {
              name: 'child folder',
              children: [
                { name: 'hello' },
                { name: 'wat' }
              ]
            },
          ]
        },
        {
          name: 'child folder',
          children: [
            {
              name: 'child folder',
              children: [
                { name: 'hello' },
                { name: 'wat' }
              ]
            },
            {
              name: 'child folder',
              children: [
                { name: 'hello' },
                { name: 'wat' }
              ]
            },
          ]
        },
      ]
    }
  ]
  export default {
    name: "tree",
    components: {
      items
    },
    data() {
      return {
        data:[]
      };
    },
    methods: {
      format(items,level) {
        return items.map((item) => {
          let currentLevel = level+1
          const result = { ...item, level: currentLevel }
          if (item.children) {
            result.children = this.format(item.children,currentLevel)
          }
          return result
        })
      }
    },
    mounted(){
      this.data = this.format(data,0)
    }
  }
</script>

<style scoped>

</style>
