<template>
	<view>
		<!-- 导航栏固定高度 -->
		<view :style="{ height: tabher }" />
		<!-- 可操作位置 -->
		<view id="topHar">
			<!-- 返回图标 -->
			<view class="iconfont iconhuitui" v-if="topicon||topicon==true" @click='toback'/>
			<!-- 页面文字 -->
			<text v-if="toptext||toptext==true">{{textvalue}}</text>
			<!-- 首页图片 -->
			<image id="img" v-if="topimg||topimg==true" src="/static/image/homelogo.png" mode=""></image>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			// 是否显示图片，默认不显示
			topimg:{
				type: [Boolean],
				default: false
			},
			// 导航栏文字
			textvalue:{
				type: [String],
				default: ''
			},
			// 是否显示图标，默认显示
			topicon:{
				type: [Boolean],
				default: true
			},
			// 是否显示文字，默认显示
			toptext:{
				type: [Boolean],
				default: true
			},
		},
		// 计算属性
		computed: {
			// 状态栏的高度
			tabher() {
				return this.until.device('BH') + 'px';
			}
		},
		methods: {
			// 页面回退
			toback() {
				// 节流
				this.until.throttle().then(res=>{
					this.until.jump(1,'bck')
				})
			}
		}
	}
</script>

<style lang="less" scoped>
	/* // 自定义头部 */
	#topHar {
		height: 44px;
		align-items: center;
		display: flex;
	}
	// 返回按钮
	.iconhuitui {
		margin-left: -15rpx;
		margin-right: 15rpx;
		font-size: 50rpx;
	}
	// 导航栏文字
	text {
		font-size: 30rpx;
	}
	// 首页logo
	image{
		height: 55rpx;
		width: 150rpx;
	}
</style>
