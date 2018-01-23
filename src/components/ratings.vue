<template>
	<div ref="ratings" class="BOX">
		<div class="ratings">
			<div class="overview">
				<div class="overview-left">
					<h1 class="score">{{seller.score}}</h1>
					<div class="title">综合评分</div>
					<div class="rank">高于周边商家{{seller.rankRate}}%</div>
				</div>
				<div class="overview-right">
					<div class="score-wrapper">
						<span class="title">服务态度</span>
						<star :size="36" :score="seller.serviceScore"></star>
						<span class="score">{{seller.serviceScore}}</span>
					</div>
					<div class="score-wrapper">
						<span class="title">商品评分</span>
						<star :size="36" :score="seller.foodScore"></star>
						<span class="score">{{seller.foodScore}}</span>
					</div>
					<div class="delivery-wrapper">
						<span class="title">送达时间</span>
						<span class="delivery">{{seller.deliveryTime}}分钟</span>
					</div>
				</div>
			</div>
			<split></split>
			<div class="rating-wrapper">
				<ul>
					<li v-for="rating in ratings" class="rating-item">
						<div class="avatar">
							<img width="28" height="28" :src="rating.avatar">
						</div>
						<div class="content">
							<h1 class="name">{{rating.username}}</h1>
							<div class="star-wrapper">
								<star :size="36" :score="rating.score"></star>
								<span class="delivery" v-show="rating.deliveryTime">{{rating.deliveryTime}}分钟前</span>
							</div>
							<p class="text">{{rating.text}}</p>
							<div class="time">
								{{rating.rateTime | formatDate}}
							</div>
						</div>

					</li>
				</ul>
			</div>

		</div>
	</div>
</template>

<script>
	/*eslint-disable*/
	import star from '@/components/star/star';
	import split from '@/components/split';
	import BScroll from 'better-scroll';

	function formatDate(date, fmt) {
		if (/(y+)/.test(fmt)) {
			fmt = fmt.replace(RegExp.$1, (date.getFullYear() + '').substr(4 - RegExp.$1.length));
		}
		let o = {
			'M+': date.getMonth() + 1,
			'd+': date.getDate(),
			'h+': date.getHours(),
			'm+': date.getMinutes(),
			's+': date.getSeconds()
		};
		for (let k in o) {
			if (new RegExp(`(${k})`).test(fmt)) {
				let str = o[k] + '';
				fmt = fmt.replace(RegExp.$1, (RegExp.$1.length === 1) ? str : padLeftZero(str));
			}
		}
		return fmt;
	}

	function padLeftZero(str) {
		return ('00' + str).substr(str.length);
	}
	export
	default {
		components: {
			"star": star,
			"split": split
		},
		props: {
			seller: {
				type: Object
			}
		},
		data() {
			return {
				ratings: []
			}
		},
		filters: {
			formatDate(time) {
				let date = new Date(time);
				return formatDate(date, 'yyyy-MM-dd hh:mm');
			}
		},
		methods: {},
		created() {
			this.$http.get('/api/ratings').then((response) => {
				response = response.body;
				if (response.errno === 0) {
					this.ratings = response.data;
					this.$nextTick(() => {
						this.ratingsW = new BScroll(this.$refs.ratings, {
							click: true
						});
					});
				}
			});
		},
	}
</script>
<style lang="less" rel="stylesheet/less">
    .BOX{width: 100%;height:500px;overflow: hidden;}
	.ratings {
		width: 100%;
		position: relative;
		width: 100%;
		overflow: hidden;
		.overview {
			padding: 18px 0;
			display: flex;
			.overview-left {
				flex: 0 0 137px;
				border-right: 1px solid rgba(7, 17, 27, 0.1);
				text-align: center;
				.score {
					font-size: 24px;
					color: rgb(255, 153, 0);
					margin-bottom: 6px;
					line-height: 28px;
				}
				.title {
					font-size: 12px;
					color: rgb(7, 17, 27);
					margin-bottom: 8px;
				}
				.rank {
					line-height: 10px;
					font-size: 10px;
					color: rgb(147, 153, 159);
				}
			}
			.overview-right {
				flex: 1;
				padding: 6px 0 6px 24px;
				.score-wrapper {
					.title {
						font-size: 12px;
						color: rgb(7, 17, 27);
						vertical-align: top;
						line-height: 18px;
					}
					.star {
						display: inline-block;
						margin: 0 12px;
						vertical-align: top
					}
					.score {
						line-height: 18px;
						font-size: 12px;
						color: rgb(255, 153, 0);
					}
				}
				.delivery-wrapper {
					.title {
						line-height: 18px;
						font-size: 12px;
						color: rgb(7, 17, 27);
					}
					.delivery {
						margin-left: 12px;
						font-size: 12px;
						color: rgb(147, 153, 159);
					}
				}
			}
		}
		.rating-wrapper {
			padding: 0 18px;
			.rating-item {
				display: flex;
				padding: 18px 0;
				border-bottom: 1px solid rgba(7, 17, 27, 0.1);
				.avatar {
					flex: 0 0 28px;
					margin-right: 12px;
					img {
						border-radius: 50%;
					}
				}
				.content {
					position: relative;
					flex: 1;
					.name {
						margin-bottom: 4px;
						line-height: 12px;
						font-size: 10px;
						color: rgb(7, 17, 27)
					}
					.star-wrapper {
						margin-bottom: 6px;
						font-size: 0;
						.star {
							display: inline-block;
							margin-right: 6px;
							vertical-align: top;
						}
						.delivery {
							display: inline-block;
							vertical-align: top;
							line-height: 12px;
							font-size: 10px;
							color: rgb(147, 153, 159);
						}
					}
					.text {
						margin-bottom: 8px;
						line-height: 18px;
						color: rgb(7, 17, 27);
						font-size: 12px;
					}
					.time {
						position: absolute;
						top: 0;
						right: 0;
						line-height: 12px;
						font-size: 10px;
						color: rgb(147, 153, 159);
					}
				}
			}
		}
	}
</style>