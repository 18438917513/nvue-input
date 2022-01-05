<template>
	<view class="ideaback">
		<!-- #ifdef APP-PLUS -->
		<view :style="[{ width: '750rpx' }, { height: statusBarHeight }]"></view>
		<!-- #endif -->
		<view class="header" id="header">
			<view class="left" @click="back">取消</view>
			<view class="title">意见反馈</view>
			<view class="right" @click="submit()">发送</view>
		</view>
		<view class="textarea" id="textarea" :style="[{ height: height }]">
			<textarea v-model="txt" :focus="focus" @focus="focusFn()" :auto-height="true" class="input" maxlength="1500" :placeholder="placeholder" :rows="rows"></textarea>
			<!-- <textarea :focus="true" placeholder-style="color:#F76260" placeholder="占位符字体是红色的"/> -->
			<!-- <input type="text" v-model="txt" :focus="focus" :auto-height="true" class="input" maxlength="1500" :placeholder="placeholder" :rows="rows" /> -->
		</view>
		<!-- <u-modal v-model="is_back" :show-cancel-button="true" cancel-text="取消" @confirm="confirmBack" @cancel="cancelBack" content="是否放弃本次编辑"></u-modal> -->
	</view>
</template>

<script>
// import { feedback } from '../../utils/api.js';
export default {
	data() {
		return {
			txt: '', //反馈意见
			placeholder: '请输入反馈意见', //占位符
			rows: 3, //文本域默认显示行数
			is_back: false, //是否显示模态框 默认不显示
			noClick: true,
			statusBarHeight: 32,
			header_height: 44,
			keyheight: 0,
			height: 736,
			focus: true
		};
	},

	onLoad() {
		this.initFullScreen();
	},
	onReady() {
		uni.createSelectorQuery()
			.select('#header')
			.boundingClientRect(res => {
				console.log(res);
				this.header_height = res.height;
				this.initFullScreen();
			})
			.exec();
	},
	// watch: {
	// 	txt(txt) {
	// 		console.log(txt);
	// 		return true
	// 		if (txt.indexOf('\n') != -1) {
	// 			console.log(txt);
	// 			//敲了回车键了
	// 			// uni.hideKeyboard(); //收起软键盘
	// 		}
	// 	}
	// },
	methods: {
		focusFn() {
			console.log('获取了焦点');
			return true;
		},
		// 屏幕信息
		initFullScreen() {
			uni.getSystemInfo({
				success: res => {
					console.log(res);
					this.statusBarHeight = res.statusBarHeight + 'px';
					this.height = `calc(100vh - ${res.statusBarHeight + this.header_height + 'px'})`;
					console.log(this.height);
					// _this.height = `calc(100vh - ${_this.input_height + 'px'})`
				}
			});
		},
		// 完成
		async submit() {
			console.log(this.txt);
			if (this.txt.trim() != '') {
				console.log(this.txt);
				// 发送意见反馈
			}
		},
		// 返回模态框  确定按钮
		confirmBack() {
			// uni.navigateBack();
			uni.reLaunch({
				url: '../../pages/profile/profile'
			});
		},
		// 返回模态框 取消按钮
		cancelBack() {
			this.is_back = false;
		},
		// 取消按钮
		back() {
			if (this.txt) {
				this.is_back = true;
			} else {
				this.is_back = false;
				// uni.navigateBack();
				uni.reLaunch({
					url: '../../pages/profile/profile'
				});
			}
		}
	}
};
</script>

<style scoped>
@import url('./ideaback.css');
</style>
