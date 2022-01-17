<template>
  <!-- TODO: implement me -->
  <div class="search-main">
    <span class="search-title">Search books of author:</span>
    <input type="text" @input="testSearch" class="search-input" placeholder="Stephen King, Stephen Hawking,Steve Turner, ...">    
    <ul >
      <li v-for="(item ,index) in filterData" :key="index" @click="selectLi(item)">{{item}}</li>
    </ul>
  </div>
  <!-- <img src='@/assets/AuthorSearch.jpg' class='img-fluid rounded' alt=''> -->
</template>

<script>
export default {
  name: 'AuthorSearch',
  props: {    
    authorsList: {
      type: Object,
      default: null
    } 
  },
  data() {
    return {    
       filterData:[]
    };
  },
  methods: {
    testSearch(author) {
      let tempArr = []
      debugger
      this.authorsList.map((v)=>{
        if(v.author.includes(author)){
          tempArr.push(v)
        }
      })

      this.filterData = tempArr
      this.$emit('select-author', author);
    }
  }
}
</script>
<style>
.search-main{
  width: 636px;
  padding-bottom: 20px;
}
.search-title{
  font-weight: bold;
  display: block;
}
.search-input{
  width: 100%;
  border: 2px solid #eee;
  border-radius: 4px;
  height: 40px;
}
</style>