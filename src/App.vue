<template>
  <div class='container'>
    <tests v-if='testing'></tests>

    <div class='row mb-3'>
      <div class='col'>
        <nav-bar
          ref='navBar'
          :tests-open='testing'
          @toggle-tests='toggleTests'
          @changeMode='changeMode'
          >
        </nav-bar>
      </div>
    </div>
    
    <div class='row'>
      <div class='col'>
        <author-search ref='authorSearch' :authorsList="authorsList" @selectAuthor="selectAuthor"></author-search>

        <books-list ref='booksListView' :listArr="listArr"  @selectItem="selectItem" ></books-list>
        
        <books-list-pagination ref='booksListPagination'  :isFirst="isFirst" :isLast="isLast"  @preFun="preFun"  @nextFun="nextFun"></books-list-pagination>
      </div>

      <div class='col'>
        <book-view :bookDetail="bookDetail"></book-view>
      </div>
      
    </div>
  </div>
</template>

<script>

import AuthorSearch from './components/AuthorSearch.vue';
import BooksList from './components/BooksList.vue';
import BooksListPagination from './components/BooksListPagination.vue';
import BookView from './components/BookView.vue';
import NavBar from './components/NavBar.vue';
import Tests from './components/Tests.vue';

//引入booklist
import bookListArr from './assets/books'

export default {
  name: 'App',
  components: {
    AuthorSearch,
    BooksList,
    BooksListPagination,
    BookView,
    NavBar,
    Tests
  },
  data() {
    return {
      page: 0,
      windowSize: 5,
      selectedIndex: 0,
      filterFn: () => true,
      lightThemeUrl: 'https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css',
      darkThemeUrl: 'https://cdn.jsdelivr.net/npm/bootstrap-dark-5@1.1.3/dist/css/bootstrap-night.min.css',
      testing: false,
      listArr:[],
      isFirst:true,
      isLast:false,
      bookDetail:null
    };
  },
  computed: {
    booksList() {
      let bookArr =  bookListArr.sort((item1, item2) => {
                
        return item1.title.localeCompare(item2.title);
      });
      //替换分号
      bookArr.map((v)=>{
        v.authors = v.authors.replace(/;/g,', ')
      })
      debugger
       return bookArr // TODO: implement me
       
    },
    authorsList() {      
      let authors = [] 
      debugger
      bookListArr.map((v)=>{ 
          if(v.authors.includes(';')){ 
            authors = authors.concat(v.authors.split(';'))
          }else{
            if(v.authors) authors.push(v.authors)            
          }
      })
      return [...new Set(authors)].sort() // TODO: implement me
    },
  },
  methods: {
    toggleTests() {
      this.testing = !this.testing;
    },
    changeMode(status){
      let url = status?this.darkThemeUrl :this.lightThemeUrl
      this.changeStyle(url)
    },
    changeStyle(url) {
      let obj = document.getElementById("bootstrap-theme");
      obj.setAttribute("href",url);
    },
    selectAuthor(author){
      let a = author.target.value
      console.log(a)
      debugger
    },
    /**书籍列表展示 */    
    preFun(){  
      debugger
      if(this.page !== 0){
        this.page--
        this.getCurrentPageList()
        this.setPageStatus()
        //重置详情页
        this.bookDetail = null
      }
      
    },
    nextFun(){     
      let pageMax =  Math.ceil(this.booksList.length/5)
      if(this.page < pageMax){
        this.page++
        this.getCurrentPageList()
        this.setPageStatus()
         //重置详情页
        this.bookDetail = null
      }
      
    },
    selectItem(index){      
      this.selectedIndex = index
      let tempObj = this.listArr[index]
      let newObj = {}
      Object.keys(tempObj).sort().forEach((v)=> newObj[v]=tempObj[v]);      
      this.bookDetail = newObj
    },
    getCurrentPageList(){      
      let start = this.page* this.windowSize;
      let end = (this.page + 1) * this.windowSize;
      this.listArr = this.booksList.slice(start, end);
    },
    setPageStatus(){
      let pageMax =  Math.ceil(this.booksList.length/5)
      if(pageMax>1){
        if(this.page===0){
          this.isFirst = true
          this.isLast = false
        }else if(this.page===pageMax){
          this.isFirst = false
          this.isLast = true
        }else{
          this.isFirst = false
          this.isLast = false
        }
      }else{
        this.isFirst = true
        this.isLast = true
      }
    },
    init(){      
      this.getCurrentPageList()
      this.setPageStatus()
    }
    
  },
  mounted(){   
    this.init()

  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
