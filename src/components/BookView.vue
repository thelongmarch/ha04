<template>
  <!-- TODO: implement me -->
  <div class="detail-main" v-if="bookDetail">
    <div >
       <div class="detail-img">
          <img :src="bookDetail.thumbnail" alt="" class="img-main" id="book-image">
        </div>
        <div id="book-title">
          <span class="com-padd">{{bookDetail.title}}{{bookDetail.subtitle?+'-'+bookDetail.subtitle:''}}</span>
        </div>
        <div class="book-property" v-for="(value,key,index) in bookDetail" :key="index">
          <div v-if="!['title','thumbnail','subtitle'].includes(key)" class="com-one">
            <span class="com-key">{{key}}: </span>
            <span class="com-value">{{value}}</span>
          </div>
         
        </div>
    </div>
   
     <!-- <img src='@/assets/BookView.jpg' class='img-fluid rounded' alt=''> -->
  </div>
 
</template>

<script>
export default {
  name: 'BookVue',
   props: {    
    bookDetail: {
      type: Object,
      default: null
    } 
  },
}
</script>
<style>
.detail-main{
  border: 1px solid #eee;
  width: 454px;
  border-radius: 4px;
}
.detail-img{
  text-align: center;
  padding-top: 12px;
}
.com-padd{
  display: block;
  padding: 8px 10px 26px 10px;
  font-size: 12px;
  font-weight: 500;
}
.com-one{  
  padding: 8px 10px 12px 10px;
  font-size: 12px;  
  border-bottom: 1px solid #eee;
}
.img-main{
  width: 85px;
}
.com-key{
  font-size: 12px;
  font-weight: bold;
}
</style>