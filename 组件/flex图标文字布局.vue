<template>
	<view class="pagebox">
		<view v-for="(item,index) in list" :key="index" @click="tolink(item.link,index)">
			<text :class="item.class" :style="{color:color}" class="iconfont" />
			<text>{{item.name}}</text>
		</view>
	</view>
</template>

<script>
	export default {
		// 父元素传递过来的值
		props: {
			// 列表的list
			list:{
				type: [Array]
			},
			// 图标的颜色
			color:{
				type:[String]
			},
			// 是否按照跳转路径跳转
			link:{
				type: [Boolean],
				default: true
			}
		},
		methods: {
			// 页面跳转
			tolink(link,index) {
				if(this.link==true){
					// 跳转到自己配置的路径
					this.until.throttle().then(res=>{
						this.until.jump(link)
					})
				}else{
					// 把需要传递的参数设置为本地缓存
					this.until.cacheSync('s','ordernum',index)
					//跳转到订单页
					this.until.jump('/pages/order/index','swt')
				}
			}
		}
	}
</script>

<style lang="less" scoped>
	.pagebox{
		width: 100%;
		height: 100%;
		display: flex;
		flex-wrap: wrap;
		align-items: center;
		view{
			width: 172rpx;
			display: flex;
			flex-direction: column;
			align-items: center;
			.iconfont{
				font-size: 45rpx;
				margin-bottom: 10rpx;
			}
			text{
				font-size: 24rpx;
				color: #2f3f50;
			}
		}
	}
</style>
