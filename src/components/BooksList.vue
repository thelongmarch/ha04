<template>
  <!-- TODO: implement me -->
  
  <div class="main" id="books">
    <!-- <img src='@/assets/BooksList.jpg' class='img-fluid rounded' alt=''> -->
    <div v-for="(item,index) in listArr" :key="index" @click="selectItem(index)" class="list-one  book" >
      <span class="book-title">{{item.title}}</span>
      <span class="book-authors">{{item.authors}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BooksList',
  props: {
    listArr: {
      type: Array
    }   
  },
  data() {
    return {     
    };
  },
  methods: {
    selectItem(index) {
      this.$emit('selectItem',index)
    } 
  },
}
</script>
<style >
.main{
  width: 636px;
  border: 1px solid #eee;
  border-radius: 5px;
}
.list-one{  
  cursor: pointer;
  height: 80px;
  padding: 10px 0 15px 20px;
  border: 1px solid #eee;
}
.book-title{
  font-weight: bold;
  display: block;
}
.book-authors{
  display: block;
  font-size: 14px;
}
</style>