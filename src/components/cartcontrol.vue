<template>
	<div class="cartcontrol">
		<div class="cart-decrease" @click.stop.prevent="decreaseCart" transition="move"  v-show="food.count>0">
			<span class="inner icon-remove_circle_outline"></span>
		</div>
		<div class="cart-count" v-show="food.count>0">{{food.count}}</div>
		<div class="cart-add icon-add_circle" @click.stop.prevent="addCart"></div>
	</div>
</template>

<script type="text/ecmascript-6">
	/*eslint-disable*/
	  import Vue from 'vue';
	  
	  export default {

	  	props:{	
	  		  food: {
              type: Object
          }
	  		
	  	}
	    ,
	    methods: {
	    	addCart(event) {
		        if (!event._constructed) {
		          return;
		        }
		        if (!this.food.count) {
		          Vue.set(this.food, 'count', 1);
		        } else {
		          this.food.count++;
		        }
		        
		      },
		      decreaseCart(event) {
		        if (!event._constructed) {
		          return;
		        }
		        if (this.food.count) {
		          this.food.count--;
		        }
		      }
		    }
	    
	  };
</script>

<style lang="less" rel="stylesheet/less">
	.icon-remove_circle_outline:before {
		content: "\e907";
	}
	.icon-add_circle:before {
		content: "\e908";
	}
	.cartcontrol {
		font-size: 0;
		.cart-decrease {
			display: inline-block;
			padding: 6px;
			.inner {
				display: inline-block;
				line-height: 24px;
				font-size: 24px;
				color: rgb(0, 160, 220);
			}
		}
		.cart-count {
			display: inline-block;
			vertical-align: top;
			width: 12px;
			padding-top: 6px;
			line-height: 24px;
			text-align: center;
			font-size: 10px;
			color: rgb(147, 153, 159);
		}
		.cart-add {
			display: inline-block;
			padding: 6px;
			line-height: 24px;
			font-size: 24px;
			color: rgb(0, 160, 220);
		}
	}
</style>