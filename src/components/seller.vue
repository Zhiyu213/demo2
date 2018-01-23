<template>
	<div ref="seller" class="box2">
		<div class="seller" >
			<div class="seller-content">
				<div class="overview">
					<h1 class="title">{{seller.name}}</h1>
					<div class="desc">
						<star :size="36" :score="seller.score"></star>
						<span class="text">({{seller.ratingCount}})</span>
						<span class="text">月售{{seller.sellCount}}单</span>
					</div>
					<ul class="remark">
						<li class="block">
							<h2>起送价</h2>
							<div class="content">
								<span class="stress">{{seller.minPrice}}元</span>
							</div>

						</li>
						<li class="block">
							<h2>商家配送</h2>
							<div class="content">
								<span class="stress">{{seller.deliveryPrice}}元</span>
							</div>

						</li>
						<li class="block">
							<h2>平均配送时间</h2>
							<div class="content">
								<span class="stress">{{seller.deliveryTime}}分钟</span>

							</div>

						</li>
					</ul>
				</div>
			</div>
			<split></split>
			<div class="bullentin">
				<h1 class="title">公告与活动</h1>
				<div class="content-wapper">
					<p class="content">{{seller.bulletin}}</p>
					<ul class="supports">
						<li class="support-item" v-for="(item,index) in seller.supports">
							<span class="icon" :class="classMap[seller.supports[index].type]"></span>
							<span class="text">{{seller.supports[index].description}}</span>
						</li>
					</ul>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	/*eslint-disable*/
	import star from "@/components/star/star"
	import split from "@/components/split"
	import BScroll from 'better-scroll'
	export
	default {
		props: {
			seller: {
				type: Object
			}
		},
		components: {
			"star": star,
			"split": split
		},
        mounted() {
		   this.$nextTick( () => {
		   	  this.scroll = new BScroll(this.$refs.seller, {})	
		   	 
		   })
		},
		data() {
			return {
				classMap: ['decrease', 'discount', 'special', 'invoice', 'guarantee']
			}
		}
	}
</script>
<style lang="less" rel="stylesheet/less">
	.box2{overflow: hidden;width: 100%;height:420px ;}
	.seller {
		
		position: relative;
		width: 100%;
		overflow: hidden;
		.overview {
			padding: 18px;
			position: relative;
			.title {
				margin-bottom: 8px;
				line-height: 14px;
				color: rgb(7, 17, 27);
				font-size: 14px;
			}
			.desc {
				padding-bottom: 18px;
				border-bottom: 1px solid (rgba(7, 17, 27, 0.1));
				font-size: 0;
				.star {
					display: inline-block;
					margin-right: 8px;
					vertical-align: top;
				}
				.text {
					display: inline-block;
					margin-right: 12px;
					line-height: 18px;
					vertical-align: top;
					font-size: 10px;
					color: rgb(77, 85, 93);
				}
			}
			.remark {
				display: flex;
				padding-top: 18px;
				.block {
					flex: 1;
					text-align: center;
					border-right: 1px solid rgba(7, 17, 27, 0.1);
					&:last-child {
						border: none;
					}
					h2 {
						margin-bottom: 4px;
						line-height: 10px;
						font-size: 10px;
						color: rgb(147, 153, 159);
					}
					.content {
						line-height: 24px;
						font-size: 10px;
						color: rgb(7, 17, 27);
						.stress {
							font-size: 24px;
						}
					}
				}
			}
		}
		.bullentin {
			padding: 18px 18px 0 18px;
			.title {
				margin-bottom: 8px;
				line-height: 14px;
				color: rgb(7, 17, 27);
				font-size: 14px;
			}
			.content-wapper {
				padding: 0 12px 16px 0px;
				border-bottom: (rgba(7, 17, 27, 0.1));
				.content {
					line-height: 24px;
					font-size: 12px;
					color: rgb(240, 20, 20);
				}
			}
			.supports {
				.support-item {
					padding: 16px 12px;
					border-bottom: rgba(7, 17, 27, 0.1);
					font-size: 0;
					.icon {
						display: inline-block;
						width: 16px;
						height: 16px;
						vertical-align: top;
						margin-right: 6px;
						background-size: 16px 16px;
						background-repeat: no-repeat;
						&.decrease {
							background-image: url(../assets/decrease_4@3x.png);
						}
						&.discount {
							background-image: url(../assets/discount_4@3x.png);
						}
						&.guarantee {
							background-image: url(../assets/guarantee_4@3x.png);
						}
						&.invoice {
							background-image: url(../assets/invoice_4@3x.png);
						}
						&.special {
							background-image: url(../assets/special_4@3x.png);
						}
					}
					.text {
						line-height: 16px;
						font-size: 12px;
						color: rgb(7, 17, 27);
					}
				}
			}
		}
	}
</style>