<template>
	<view class="content"><button type="primary" @tap="download">下载</button></view>
</template>
<script>
export default {
	data() {
		return {
			title: 'Hello'
		};
	},
	onLoad() {},
	methods: {
		download() {
			const downloadTask = uni.downloadFile({
				url:'http://www.gov.cn/zhengce/pdfFile/2021_PDF.pdf',
				// url: 'http://img.netbian.com/file/2019/0414/7bee7eef5fc44417a0b02a46576e7e16.jpg', //仅为示例，并非真实的资源
				success: res => {
					if (res.statusCode === 200) {
						console.log('下载成功');
						uni.showToast({
							title:'下载成功'
						})
					}
					let that = this;
					uni.saveFile({
						tempFilePath: res.tempFilePath,
						success: function(red) {
							that.luj = red.savedFilePath;
							console.log(red);
						}
					});
				}
			});

			downloadTask.onProgressUpdate(res => {
				console.log('下载进度' + res.progress);
				console.log('已经下载的数据长度' + res.totalBytesWritten);
				console.log('预期需要下载的数据总长度' + res.totalBytesExpectedToWrite);
			});
		}
	}
};
</script>

<style>
.content {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
}

.logo {
	height: 200rpx;
	width: 200rpx;
	margin-top: 200rpx;
	margin-left: auto;
	margin-right: auto;
	margin-bottom: 50rpx;
}

.text-area {
	display: flex;
	justify-content: center;
}

.title {
	font-size: 36rpx;
	color: #8f8f94;
}
</style>
