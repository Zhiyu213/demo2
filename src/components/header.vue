<template>

	<div class="header" >

		<div class="content-wrapper">
			<div class="avatar">
				<img width="64" height="64" :src="seller.avatar">
			</div>

			<div class="content">
				<div class="title">
					<span class="brand"></span>
					<span class="name">{{seller.name}}</span>
				</div>
				<div class="description">
					{{seller.description}}/{{seller.deliveryTime}}分钟送达
				</div>
				<div v-if="seller.supports" class="support">
					<span class="icon" :class="classMap[seller.supports[0].type]"></span>
					<span class="text">{{seller.supports[0].description}}</span>
				</div>
			</div>

		</div>
		<div class="bulletin-wrapper" @click="showDetail">
			<span class="bulletin-title"></span>
			<span class="bulletin-text">{{seller.bulletin}}</span>

		</div>
		<div class="bg">
			<div><img :src="seller.avatar"></div>
		</div>

		<div v-show="detailShow" class="detail" transition="fade" >

			<div class="detail-wrapper clearfix" >
				<div class="detail-main">
					<h1 class="name">{{seller.name}}</h1>

					<div class="title">
						<div class="line"></div>
						<div class="text">优惠信息</div>
						<div class="line"></div>
					</div>
					<ul v-if="seller.supports" class="supports">
						<li class="support-item" v-for="item in seller.supports">

						</li>
					</ul>
					<div class="title">
						<div class="line"></div>
						<div class="text">商家公告</div>
						<div class="line"></div>
					</div>
					<div class="bulletin">
						<p class="content">{{seller.bulletin}}</p>
					</div>
				</div>
			</div>
			<div class="detail-close" @click="hideDetail">
				 退出
			</div>
		</div>

	</div>
	</div>
</template>

<script>
	/*eslint-disable*/
	export
	default {
		data() {
				return {
					detailShow: false
				};
			},
			methods: {
				showDetail() {
						this.detailShow = true;
						console.log(1)
						
					},
					hideDetail() {
						this.detailShow = false;
					}
			},
			props: {
				seller: {
					type: Object
				}
			},
			created() {
				this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
			},
	};
</script>

<style scoped>
	.header {
		position: relative;
		overflow: hidden;
		color: #fff;
		background: rgba(7, 17, 27, 0.5);
	}
	.header .content-wrapper {
		padding: 24px 12px 18px 24px;
		font-size: 0px
	}
	.header .content-wrapper .avatar {
		display: inline-block;
		font-size: 0px
	}
	.header .content-wrapper .avatar img {
		border-radius: 3px
	}
	.header .content-wrapper .content {
		display: inline-block;
		font-size: 14px;
		margin-left: 16px
	}
	.header .content-wrapper .content .title {
		margin: 2px 0 8px 0
	}
	.header .content-wrapper .content .title .brand {
		display: inline-block;
		width: 30px;
		height: 18px;
		background: url(../../resource/img/brand@2x.png) no-repeat;
		background-size: 30px 18px;
		vertical-align: top
	}
	.header .content-wrapper .content .name {
		margin-left: 6px;
		font-size: 16px;
	}
	.header .content-wrapper .content .description {
		margin-bottom: 10px;
		line-hieght: 12px;
		font-size: 12px;
	}
	.header .content-wrapper .content .support .icon {
		display: inline-block;
		width: 12px;
		height: 12px;
		margin-right: 4px;
		background: url(../../resource/img/decrease_1@2x.png);
		background-size: 12px 12px;
	}
	.header .content-wrapper .content .support .text {
		line-height: 12px;
		font-size: 10px;
		color: white;
		vertical-align: top;
	}
	.bg img {
		width: 100%;
		position: absolute;
		left: 0;
		top: 0;
		height: 100%;
		z-index: -1;
		filter: blur(10px);
	}
	.bulletin-wrapper {
		font-size: 12px;
		width: 100%;
		position: relative;
		height: 28px;
		line-height: 28px;
		padding: 0 22px 0 12px;
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
		background: rgba(7, 17, 27, 0.2)
	}
	.bulletin-title {
		display: inline-block;
		vertical-align: top;
		margin-top: 8px;
		width: 20px;
		height: 12px;
		background: url(../../resource/img/discount_1@2x.png);
		background-size: 20px 12px;
		background-repeat: no-repeat
	}
	
	 .detail{
      position: fixed;
      z-index: 100;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      overflow: auto;
      transition: all 0.5s;
      backdrop-filter: blur(10px);
      opacity: 1;
      background: rgba(7, 17, 27, 0.8);
      }
      .detail .detail-wrapper{
      	width: 100%;
        min-height: 100%;
       }
  
      .detail .detail-wrapper .detail-main{
          margin-top: 64px;
          padding-bottom: 64px;
        }
        .detail .detail-wrapper .detail-main .name{
            line-height: 16px;
            text-align: center;
            font-size: 16px;
            font-weight: 700}
        .detail .detail-wrapper .detail-main .title{ 
            display: flex;
             width: 80%;
              margin: 28px auto 24px auto;
            
           
        }
        .detail .detail-wrapper .detail-main .line{
              flex: 1;
              position: relative;
              top: -6px;
              border-bottom: 1px solid rgba(255, 255, 255, 0.2);
          }
          
          .detail .detail-wrapper .detail-main .bulletin{
            width: 80%;
            margin: 0 auto}
           .detail .detail-wrapper .detail-main  .content{
              padding: 0 12px;
              line-height: 24px;
              font-size: 12px}
      .detail .detail-close {
      	
      	color:white;
        width: 32px;
        height: 32px;
        margin: -64px auto 0 auto;
        clear: both;
        font-size: 16px;
        position: relative;
       }
        
</style>