<template>
	<div class="shopcart">
		<div class="content">
			<div class="content-left">
				<div class="logo-wrapper">
					<div class="logo">
						<i class="icon-shopping_cart"></i>
					</div>
					<div class="num" v-show="totalCount>0">{{totalCount}}</div>
				</div>

				<div class="price">￥{{totalPrice}}</div>

				<div class="desc">另需配送费￥{{minPrice}}元</div>
			</div>

			<div class="content-right">
				<div class="pay" > {{payDesc}} </div>
			</div>
		</div>
	</div>
</template>
<script type="text/ecmascript-6">
	/*eslint-disable*/
	
	
	export
	default {
	 
		props: {
			selectfoods: {
		        type: Array,
		        default() {
		          return [
		            {
		              price: 10,
		              count: 1
		            }
		          ];
		        }
		      },
			minPrice: {
		        type:Number, 
		        
		     },
		     
		    deliveryPrice:{
		    	type: Number,
                default: 0
		    }
		     
		},
		created(){ 
		    
		},
		computed: {
			  totalCount() {
		        let count = 0;
		        this.selectfoods.forEach((food) => {
		          count += food.count;
		        });
		        return count;
		      },
			  totalPrice() {
		        let total = 0;
		        this.selectfoods.forEach((food) => {
		          total += food.price * food.count;
		        });
		        return total;
		      },
			  payDesc() {
		        if (this.totalPrice === 0) {
		          return `￥${this.minPrice}元起送`;
		        } else if (this.totalPrice < this.minPrice) {
		          let diff = this.minPrice - this.totalPrice;
		          return `还差￥${diff}元起送`;
		        } else {
		          return '去结算';
		        }
		      },
					
		},

	}
</script>
<style lang="less" rel="stylesheet/less">
	.shopcart {
		position: fixed;
		left: 0;
		bottom: 0;
		z-index: 50;
		width: 100%;
		height: 48px;
		background: #ccc;
		.content {
			background: #141d27;
			font-size: 0;
			color: rgba(255, 255, 255, 0.4);
			display: flex;
			.content-left {
				flex: 1;
				.logo-wrapper {
					display: inline-block;
					top: -10px;
					position: relative;
					margin: 0 12px;
					padding: 6px;
					width: 56px;
					height: 56px;
					box-sizing: border-box;
					border-radius: 50%;
					background: #141d27;
					text-align: center;
					.logo {
						height: 100%;
						width: 100%;
						border-radius: 50%;
						background: #2b343c;
						.icon-shopping_cart:before {
							content: "\e903";
							line-height: 44px;
							font-size: 24px;
							color: #80858a;
							&.highlight {
								color: #fff
							}
						}
					}
					.num {
						position: absolute;
						top: 0;
						right: 0;
						width: 24px;
						height: 16px;
						line-height: 16px;
						text-align: center;
						border-radius: 16px;
						font-size: 9px;
						font-weight: 700;
						color: #fff;
						background: rgb(240, 20, 20);
						box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.4);
					}
				}
				.price {
					font-size: 16px;
					font-weight: 700;
					color: #fff;
					display: inline-block;
					padding-right: 12px;
					box-sizing: border-box;
					border-right: 1px solid rgba(255, 255, 255, 0.5);
					vertical-align: top;
					margin-top: 12px;
					line-height: 24px
				}
				.desc {
					display: inline-block;
					vertical-align: top;
					margin: 12px 0 0 12px;
					line-height: 24px;
					font-size: 10px;
				}
			}
			.content-right {
				flex: 0 0 105px;
				.pay {
					height: 48px;
					line-height: 48px;
					text-align: center;
					font-size: 12px;
					font-weight: 700;
				}
			}
		}
	}
</style>