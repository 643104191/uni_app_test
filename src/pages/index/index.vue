<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view>
			<text class="title">{{title}}</text>
		</view>
		<view>
			<text class="title">[].flatMap功能{{hasFlatMap?'正常':'异常'}}</text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				hasFlatMap: true,
				title: 'Hello'
			}
		},
		created() {
			try {
				[].flatMap(v=>v)
			} catch (error) {
				this.hasFlatMap = false
				console.error(error)
			}
		},
		methods: {

		}
	}
</script>

<style>
	.content {
		text-align: center;
		height: 400upx;
	}

	.logo {
		height: 200upx;
		width: 200upx;
		margin-top: 200upx;
	}

	.title {
		font-size: 36upx;
		color: #8f8f94;
	}
</style>
