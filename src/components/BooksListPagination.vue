<template>
  <!-- TODO: implement me -->
  <!-- <img src='@/assets/BooksListPagination.jpg' class='img-fluid rounded' alt=''> -->
  <div class="bottom-main">
    <button class="com-btn btn-left" :class="isFirst?'allow':null" @click="preFun" :disabled="isFirst">Previous</button>
    <button class="com-btn btn-right" :class="isLast?'allow':null" @click="nextFun" :disabled="isLast">Next</button>
  </div>

</template>

<script>
export default {
  name: 'BooksListPagination',
  props: {    
    isFirst: {
      type: Boolean,
      default: true
    }, 
    isLast: {
      type: Boolean,
      default: false
    }, 
  },
  methods: {
    preFun() {      
      this.$emit('preFun')
    },
    nextFun() {      
      this.$emit('nextFun')
    } 
  },
}
</script>
<style>
.bottom-main{
  margin: 20px auto;
  text-align: center;
}
.com-btn{
  background-color: white;
  padding: 5px 10px;
  border: 1px solid #eee;
  color: rgb(16, 56, 235);
  font-weight: 500;
}
.btn-left{
  border-top-left-radius:4px;
  border-bottom-left-radius:4px;
}
.btn-right{
  border-top-right-radius:4px;
  border-bottom-right-radius:4px;
}
.allow{
  color: rgb(148, 140, 140);
  cursor: not-allowed;
}
</style>