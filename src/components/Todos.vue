<template>
  <div class="todos">
      <div v-for="(item,index) in todo" :key="index">
          <TodoItem @deleteItem="$emit('handleDelete',item.id)" :todo="item" />
      </div>
  </div>
</template>

<script>
import TodoItem from '@/components/TodoItem.vue'

export default {
  name: 'Todos',
  props:{
      todo:Array
  },
  methods:{
    // deleteItem(id){
    //     // console.log(id)
    // }
  },
  components:{
      TodoItem
  }
}
</script>

<style scoped>

</style>
