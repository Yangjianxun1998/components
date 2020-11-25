<template>
	<view class="tab">
		<view class="pagebox" :class="{borlef:leftshow}"  v-for="(item,index) in list" :key="index" @click="select(index)">
			<view class="textbox" :animation="animationData"  >
				<text :class="{ select: boomshow, active: index === sel }">{{item}}</text>
				<image v-if="icon==true&&index !== sel" src="/static/image/bacicon1.png" />
				<image v-if="icon==true&&direction==false&&index === sel" src="/static/image/bacicon3.png" />
				<image v-if="icon==true&&direction!=false&&index === sel" src="/static/image/bacicon2.png" />
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		props:{
			// 是否显示左边框，默认不显示
			leftshow:{
				type: [Boolean],
				default: false
			},
			// 是否显示下边框，默认显示
			boomshow:{
				type: [Boolean],
				default: true
			},
			// 传入标签数组
			list:{
				type: [Array]
			},
			// 是否显示图标（默认不显示
			icon:{
				type: [Boolean],
				default: false
			},
			// 当前的sel(默认0 )
			index:{
				type: [Number],
				default: 0
			}
		},
		// // 一注册执行
		created(){
			this.sel=this.index
		},
		data(){
			return{
				sel:0,//当前的点击效果id
				// animationData:{},//动画实例
				direction:false,
			}
		},
		methods:{
			select(index){
				if(index!=this.sel){
					this.sel=index
					this.direction=false
				}else{ 
					this.direction=!this.direction
				}
				// 防抖
				this.until.debounce().then(res=>{
					this.selectbreak(index)
				})
			},
			// 执行最后一次
			selectbreak(index){
				// 子组件给父组件传值（当前点击的sel，正序还是倒序）
				this.$emit('sel',{sel:index,direction:this.direction});
			}
		}
	}
</script>

<style lang="less" scoped>
	// 全局页面
	.tab{
		display: flex;
		width: 100%;
		height: 100%;
		// 点击
		.pagebox{
			flex: 1;
			box-sizing: border-box;
			height: 100%;
			justify-content: center;
			display: flex;
			align-items: center;
		}
		.textbox{
			display: flex;
			width: 0;
			flex: 1;
			height: 100%;
			align-items: center;
			justify-content: center;
			padding: 0 15rpx;
		}
		text{
			padding: 0 2rpx;
			height: 100%;
			display: flex;
			align-items: center;
		}
		image{
			width: 22rpx;
			height: 25rpx;
			margin-left: 5rpx;
		}
		.select.active{
			border-bottom: 4rpx solid #cb101b;
		}
		.active{
			color: #cb101b;
		}
		// 动态显示左边框
		.borlef{
			border-left: 1rpx solid #ececec;
		}
		.borlef:first-child{
			border-left: none;
		}
	}
</style>
