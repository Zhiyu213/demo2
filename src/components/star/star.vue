<template>
	<div class="star" :class="starType">
		<span v-for="itemClass in itemClasses" :class="itemClass" class="star-item" track-by="$index"></span>
	</div>
</template>

<script type="text/ecmascript-6">
	/*eslint-disable*/
	const LENGTH = 5;
	  const CLS_ON = 'on';
	  const CLS_HALF = 'half';
	  const CLS_OFF = 'off';
	
	  export default {
	    props: {
	      size: {
	        type: Number
	      },
	      score: {
	        type: Number
	      }
	    },
	    computed: {
	      starType() {
	        return 'star-' + this.size;
	      },
	      itemClasses() {
	        let result = [];
	        let score = Math.floor(this.score * 2) / 2;
	        let hasDecimal = score % 1 !== 0;
	        let integer = Math.floor(score);
	        for (let i = 0; i < integer; i++) {
	          result.push(CLS_ON);
	        }
	        if (hasDecimal) {
	          result.push(CLS_HALF);
	        }
	        while (result.length < LENGTH) {
	          result.push(CLS_OFF);
	        }
	        return result;
	      }
	    }
	  };
</script>

<style lang="less" rel="stylesheet/less">
	.bg-image (@url) {
		background-image: url("@{url}@2x.png");
	}
	.star {
		font-size: 0px;
     
		&.star-36 {
				.star-item {
					display: inline-block;
					background-repeat: no-repeat;
					width: 15px;
					height: 15px;
					margin-right: 6px;
					background-size: 15px 15px;
						&:last-child {
							margin-right: 0
						}
						&.on {
							.bg-image('star36_on')
						}
						&.half {
							.bg-image('star36_half')
						}
						&.off {
							.bg-image('star36_off')
						}
				}
				
		}
		
		
	}
	
	

</style>