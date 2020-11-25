<template>
	<view class="inpubox">
		<!-- 左边文字，左边的值 -->
		<view :style="{width:leftwidth,fontSize:leftsize}">{{textval}}</view>
		<!-- input 输入文字  获取焦点  是否可输入 输入键盘  输入的值  最大输入  默认值 键盘按钮 -->
		<input @input="search" @focus="obtain" :disabled="disabled" :type="type" v-model.trim="serc" :maxlength="max" :placeholder="poler" confirm-type='完成'/>
		<!-- 如果文字为0 不显示  清空  图标大小 -->
		<icon v-if="serc.length>0" type="clear" @click="empty" :size="iconsize"/>
	</view>
</template>

<script>
export default {
	props:{
		// 左边的宽
		leftwidth:{
			type: [String],
			default: '160rpx'
		},
		// 左边文字的大小
		leftsize:{
			type: [String],
			default: '24rpx'
		},
		// clear图标的大小
		iconsize:{
			type: [String],
			default: '30rpx'
		},
		// inut的值
		val:{
			type: [String],
			default: ''
		},
		// inut是否禁止输入(默认不禁止)
		disabled:{
			type: [Boolean],
			default: false
		},
		// 左边的值
		textval:{
			type: [String],
			default: ''
		},
		// input的最大值
		max:{
			type: [Number],
			default: -1
		},
		// input的输入键盘类型，默认文字类型
		type:{
			type: [String],
			default: 'text'
		},
		// input的默认文字
		poler:{
			type: [String],
			default: '请输入文字'
		}
	},
	data() {
		return {
			serc:'',//input的内容
		};
	},
	methods:{
		// 清空按钮
		empty(){
			this.serc='';
			this.$emit('empty', this.serc);
		},
		// 输入事件，输入了文字
		search(){
			// 防抖
			this.until.debounce().then(res=>{
				this.searchbreak()
			})
		},
		 // 执行最后一次
		searchbreak(){
			// 子组件给父组件传值（当前的文字）
			this.$emit('search', this.serc);
		},
		// input获得到焦点
		obtain(){
			// 子组件给父组件传值（）
			this.$emit('obtain', this.serc);
		}
	},
	// 注册组件
	created() {
		// 一注册执行
		this.serc=this.val
	}
	
};
</script> 
<style lang="less" scoped>
	.inpubox{
		width: 100%;
		height: 100%;
		display: flex;
		align-items: center;
		view{
			height: 100%;
			display: flex;
			align-items: center;
			justify-content: center;
		}
		input{
			height: 100%;
			width: 100%;
			flex: 1;
		}
		icon{
			padding: 15rpx;
			margin-right: 10rpx;
		}
	}
</style>
