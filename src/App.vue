<template>
  <div id="app">
     <v-header v-bind:seller="seller"></v-header>
     <v-banner></v-banner>
     <div class="tab">
     	    <div class="tab-item">
     	    	     <router-link to="/goods">商品</router-link></div>
     	    <div class="tab-item">
     	    	     <router-link to="/ratings">评论</router-link></div>
     	    <div class="tab-item">
     	           <router-link to="/seller">商家</router-link>
     	    </div>  

     </div>
     <router-view :seller="seller"></router-view>
  </div>
</template>

<script>
/*eslint-disable*/
 import header from "./components/header";
 import banner from "./components/banner";



 
 
export default {
    data (){ 
      return{ 
          seller:{}
          
      }

    }
    ,
    created (){ 

       this.$http.get("/api/seller").then(function(res){ 
           var res=res.body;
           
           if(res.errno=="0"){ 
              this.seller=res.data;
              
           }
       })

    },

  
   components:{ 
     "v-header":header,
     "v-banner":banner
   }
    
}
</script>

<style>


.tab{
   display:flex;
   width:100%;
   height:40px;
   line-height:40px;
}

.tab .tab-item{
     flex:1;
     text-align: center;
 }



</style>
