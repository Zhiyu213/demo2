<template>
	<div>
		<div class="goodsContent">
			<div class="good-left" ref="menuWrapper">
				<ul>
					<li v-for="(item,index) in goods" class="menu-item" :class="{'current':currentIndex==index}" @click="selsectmeun(index)">
						{{item.name}}
					</li>
				</ul>
			</div>
			<div class="foods-wrapper" ref="foodsWrapper">
				<ul>
					<li v-for="item in goods" class="food-list food-list-hook">
						<h1 class="title">{{item.name}}</h1>
						<ul>
							<li  v-for="food in item.foods" class="food-item border-1px">
								<div class="icon">
									<img width="57" height="57" :src="food.icon">
								</div>
								<div class="content">
									<h2 class="name">{{food.name}}</h2>
									<p class="desc">{{food.description}}</p>
									<div class="extra">
										<span class="count">月售{{food.sellCount}}份</span><span>好评率{{food.rating}}%</span>
									</div>
									<div class="price">
										<span class="now">￥{{food.price}}</span><span class="old" v-show="food.oldPrice">￥{{food.oldPrice}}</span>
									</div>
									<div class="cartcontrol-wrapper">
                                         <cartcontrol :food="food"></cartcontrol>
									</div>
								</div>
							</li>
						</ul>
					</li>
				</ul>
			</div>
			<v-car v-bind:minPrice="seller.minPrice" :delivery-price="seller.deliveryPrice" :selectfoods="selectFoods"></v-car>
		</div>
	</div>
	
</template>

<script>
	/*eslint-disable*/
	import BScroll from 'better-scroll'
    import car from '@/components/car';
    import cartcontrol from '@/components/cartcontrol';
    
	export
	default {
        components:{ 
         "v-car":car,
         "cartcontrol":cartcontrol,
         
         
        },
		props: {
			seller:{}

		},
		data() {

			return {
				selectedFood: {},
			    minPrice:10,
				goods: [],
				listHeight: [],
				scrollY: 0,
				
			}
		},
		created() {
			
			this.$http.get('/api/goods').then((response) => {
				response = response.body;
				if (response.errno === 0) {
					this.goods = response.data;
					this.$nextTick(() => {
						
						this._initScroll();
						
						this.calculateHeight();
					})
				}
			});
		},
		computed: {
			currentIndex() {
				for (let i = 0; i < this.listHeight.length; i++) {
					let height1 = this.listHeight[i];
					let height2 = this.listHeight[i + 1];
					if (!height2 || (this.scrollY >= height1 && this.scrollY < height2)) {
						return i;
					}
				}
				return 0;
			},
		     selectFoods() {
		        let foods = [];
		        this.goods.forEach((good) => {
		          good.foods.forEach((food) => {
		            if (food.count) {
		              foods.push(food);
		            }
		          });
		        });
		        return foods;
		      }

		},
		methods: {
			
			_initScroll() {
				   
				  
					this.menuScroll = new BScroll(this.$refs.menuWrapper, {
						click: true,
						
					})
					
					this.foodsWrapper = new BScroll(this.$refs.foodsWrapper, {
						
						click: true,
						probeType: 3,
						
					});
					
					
					this.foodsWrapper.on('scroll', (pos) => {
						this.scrollY = Math.abs(Math.round(pos.y));
					});
					
				},
				calculateHeight() {
					let foodList = this.$refs.foodsWrapper.getElementsByClassName('food-list-hook');
					let height = 0;
					this.listHeight.push(height);
					for (let i = 0; i < foodList.length; i++) {
						let item = foodList[i];
						height += item.clientHeight;
						this.listHeight.push(height);
					}
				},
				selsectmeun(index) {
					if (!event._constructed) {
						return;
					};
					let foodList = this.$refs.foodsWrapper.getElementsByClassName('food-list-hook');
					let el = foodList[index];
					this.foodsWrapper.scrollToElement(el, 300);
				},
				
				
		}
	}
</script>
<style lang="less" rel="stylesheet/less">
	.goodsContent {
	    position: relative;
		display: flex;
		height:600px;
	    overflow: hidden;
	    width: 100%;
	    
	    
		.good-left {
			height:300px;
			
			flex: 0 0 80px;
			
			.menu-item {
				background: #f3f5f7;
				display: flex;
				align-items: center;
				justify-content: center;
				height: 53px;
				width: 56px;
				padding: 0 12px;
				font-size: 14px;
				border-bottom: 1px solid #eee;
				&.current {
					background:#ccc;
				}
			}
		}
		.foods-wrapper {
			flex: 1;
			font-size: 10px;
			height:300px;	
			.title {
				padding-left: 14px;
				height: 26px;
				line-height: 26px;
				border-left: 2px solid #d9dde1;
				font-size: 12px;
				color: rgb(147, 153, 159);
				background: #f3f5f7;
			}
			.food-item {
				display: flex;
				margin: 18px;
				padding-bottom: 18px;
				border-bottom: 1px solid #eee;
				&:last-child {
					border: none;
					margin-bottom: 0;
				}
				.icon {
					flex: 0 0 57px;
					margin-right: 10px;
				}
				.content {
					flex: 1;
					position: relative;
					.name {
						margin: 2px 0 8px 0;
						height: 14px;
						line-height: 14px;
						font-size: 14px;
						color: rgb(7, 17, 27);
					}
					.desc {
						line-height: 12px;
						margin-bottom: 8px;
					}
					.extra .count {
						margin-right: 12px
					}
					.price {
						font-weight: 700;
						line-height: 24px;
					}
					.now {
						margin-right: 8px;
						font-size: 14px;
						color: rgb(240, 20, 20);
					}
					.old {
						text-decoration: line-through;
						font-size: 10px;
						color: rgb(147, 153, 159);
					}
					.cartcontrol-wrapper{
			            position: absolute;
			            right: 0;
			            bottom: -8px;
		            }
				}
			}
		}
	}
</style>