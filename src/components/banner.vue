<template>
	<div class="swiper-container">
		<div class="swiper-wrapper">
			<div class="swiper-slide"><img src="../assets/1.jpg"></div>
			<div class="swiper-slide"><img src="../assets/2.jpg"></div>
			<div class="swiper-slide"><img src="../assets/3.jpg"></div>
			<div class="swiper-slide"><img src="../assets/4.jpg"></div>
			<div class="swiper-slide"><img src="../assets/5.jpg"></div>
		</div>

		<div id="swiper-pagination"></div>

	</div>
</template>

<script>
	/*eslint-disable*/
	    import Swiper from 'swiper'
	    import 'swiper/dist/css/swiper.min.css'
	    import 'swiper/dist/js/swiper.js'
	
	
	
	    export default {
	        props: ['listImg'],
	        mounted() {
	           
	            var swiper = new Swiper('.swiper-container', {
	              
	                paginationClickable: true,
	                loop: true,
	                speed: 600,
	                delay: 3000,
	                height:80,
	                
	                pagination :{
	                	el:"#swiper-pagination",
	                	clickable:true
	                },
	
	                autoplay: {
					    disableOnInteraction: false,
					 }
	
	            
	            });
	        }
	    }
</script>
<style lang="less" rel="stylesheet/less">
	.swiper-container{position: relative;
			     height: 80px;
			     width:100%;
			     overflow:hidden;
			   .swiper-slide{
			  	  img { width:100%}
			  }
			  #swiper-pagination {
			  	text-align: center;
			  	position: absolute;
			  	top:60px;
			  	z-index: 1;
			  	}
	
		 }
</style>