<template>
	<!-- 是否自动切换,是否显示面板指示点, 自动切换时间间隔,滑动动画时长,是否采用衔接滑动，即播放到末尾后重新回到开头,指示点颜色,当前选中的指示点颜色-->
	<swiper
		autoplay="true"
		indicator-dots="true"
		interval="2000"
		duration="1000"
		circular="true"
		indicator-color="rgba(219,220,222,0.5)"
		indicator-active-color="#c6010c"
	>
		<swiper-item v-for="(item, index) in bannerlist" :key="index"><image :src="srcs + item.item_pic_url[0].path" @click="tolink(item.item_link)" /></swiper-item>
	</swiper>
</template>

<script>
	export default {
		data(){
			return{
				srcs:this.$base.baseUrl,//请求头
			}
		},
		// 父元素传递过来的值
		props: {
			// 是否显示图片，默认不显示
			bannerlist:{
				type: [Array]
			}
		},
		methods: {
			// 页面跳转
			tolink(link) {
				// 节流
				this.until.throttle().then(res=>{
					this.until.jump(link)
				})
			}
		}
	}
</script>

<style lang="less" scoped>
	swiper{
		width: 100%;
		height: 100%;
	}
</style>
