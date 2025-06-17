<template>
	<loading :show="isLoading"></loading>
	<view class="page-container">
		<view class="app-title"><text class="www">口香糖缺陷检测系统</text></view>
		<view class="card">
			<view class="chat-header">实时图像展示</view>
			<view class="chat-window">
				<view class="imgs" v-for="item in items">
					<img :src="item.src" alt="" />
					<view class="time-text">{{ item.created }}</view>
				</view>
				<view style="width: 100%; height: 30px"> </view>
			</view>
		</view>
		<view class="datas">
			<view class="data-item">
				<view class="data-label">缺肉数量：</view>
				<view class="data-value">9</view>
			</view>
			<view class="data-item">
				<view class="data-label">堵塞状态：</view>
				<view class="data-value">正常</view>
			</view>
		</view>
		<view class="btns">
			<view class="btn" @click="kaishi(1.0)"> 开始 </view>
			<view class="btn" @click="kaishi(2.0)"> 暂停 </view>
			<view class="btn" @click="kaishi(0.0)"> 结束 </view>
		</view>
	</view>
</template>

<script setup>
	import {
		ref
	} from "vue";
	import {
		onShow,
		onLoad,
		onHide
	} from "@dcloudio/uni-app";
	import Loading from "../../components/Loading.vue";
	let timer = null;

	onShow(() => {
		getImages(); // 立即获取一次
		timer = setInterval(getImages, 3000); // 每3秒获取一次
	});

	onHide(() => {
		if (timer) {
			clearInterval(timer);
			timer = null;
		}
	});
	const items = ref([{
			src: "https://picsum.photos/200",
		},
		{
			src: "https://picsum.photos/200",
		},
		{
			src: "https://picsum.photos/200",
		},
		{
			src: "https://picsum.photos/200",
		},
		{
			src: "https://picsum.photos/200",
		},
		{
			src: "https://picsum.photos/200",
		},
	]);
	const getImages = () => {
		uni.request({
			url: "http://112.74.32.111:8000/images",
			success: (res) => {
				if (res.statusCode === 200) {
					items.value = res.data.images.map((item) => ({
						src: "http://112.74.32.111:8000" + item.url,
						created: item.created,
					}));
				} else {
					console.error("获取图片失败", res);
				}
			},
			fail: (err) => {
				console.error("请求失败", err);
			},
		});
	};
	const kaishi = (e) => {

		uni.request({
			url: "https://iot-api.heclouds.com/thingmodel/set-device-property", // 请求的 URL
			method: "POST", // 请求方法
			header: {
				"Content-Type": "application/json", // 设置请求头
				// 如果需要，可以在这里添加其他请求头，例如认证 token
				// "api-key": "your-api-key", // 示例：添加 API 密钥
				"authorization": "version=2018-10-31&res=products%2FOrT98dB198%2Fdevices%2Flotus1&et=1917513743&method=md5&sign=rski44rCWDk0cXSVrbJOWg%3D%3D",
			},

			data: {
				product_id: "OrT98dB198",
				device_name: "lotus1",
				params: {
					level: e
				},
			},
			success: (res) => {
				console.log("请求成功", res);
				// 在这里处理成功的逻辑
			},
			fail: (err) => {
				console.error("请求失败", err);
				// 在这里处理失败的逻辑
			},
		});
	};
</script>

<style lang="scss" scoped>
	.page-container {
		background: linear-gradient(to bottom, #f8f9ff, #ffffff);
		height: 100vh;
		width: 100vw;
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	.app-title {
		width: 100%;
		height: 34px;
		padding: 16px 8px;
		background: linear-gradient(135deg, #4f78ff 0%, #3a5bd9 100%);
		color: white;
		font-size: 20px;
		font-weight: bold;
		text-align: center;
		box-shadow: 0 4px 15px rgba(79, 120, 255, 0.3);
		margin-bottom: 15px;
		position: relative;
		letter-spacing: 1px;
	}

	.www {
		position: absolute;
		left: 50px;
		top: 21.5px;
	}

	.app-title::before {
		content: "";
		position: absolute;
		left: 20px;
		top: 24px;
		width: 24px;
		height: 24px;
		background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="white"><path d="M12 2L4 5v6.09c0 5.05 3.41 9.76 8 10.91 4.59-1.15 8-5.86 8-10.91V5l-8-3zm-1.06 13.54L7.4 12l1.41-1.41 2.12 2.12 4.24-4.24 1.41 1.41-5.64 5.66z"/></svg>');
		background-size: contain;
		background-repeat: no-repeat;
	}

	.card {
		margin-top: 5px;
		width: 90vw;
		background-color: #fff;
		border-radius: 12px;
		box-shadow: 0 4px 20px rgba(79, 120, 255, 0.1);
		overflow: hidden;
	}

	.chat-header {
		background-color: #4f78ff;
		color: #fff;
		padding: 12px 16px;
		font-size: 16px;
		font-weight: 500;
	}

	.chat-window {
		height: 58vh;
		overflow-y: auto;
		padding-left: 10px;
		padding-right: 10px;
	}

	.imgs {
		width: 94%;
		margin-left: 3%;
		margin-top: 10px;
		border-radius: 8px;
		overflow: hidden;
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
	}

	.imgs img {
		width: 100%;
		height: auto;
		display: block;
	}

	.time-text {
		color: #999;
		font-size: 12px;
		padding: 0px 8px 4px 8px;
	}

	.datas {
		width: 90vw;
		display: flex;
		justify-content: space-between;
		margin-top: 20px;
	}

	.data-item {
		width: 42%;
		background: #fff;
		border-radius: 10px;
		padding: 12px;
		box-shadow: 0 2px 10px rgba(79, 120, 255, 0.1);
	}

	.data-label {
		font-size: 14px;
		color: #666;
		margin-bottom: 8px;
	}

	.data-value {
		font-size: 18px;
		font-weight: bold;
		color: #4f78ff;
	}

	.btns {
		width: 90vw;
		display: flex;
		justify-content: space-between;
		margin-top: 20px;
		margin-bottom: 5px;
	}

	.btn {
		width: 30%;
		height: 42px;
		border-radius: 8px;
		background-color: #4f78ff;
		font-size: 14px;
		font-weight: 500;
		color: #fff;
		display: flex;
		align-items: center;
		justify-content: center;
		transition: all 0.2s;
		box-shadow: 0 2px 8px rgba(79, 120, 255, 0.3);
	}

	.btn:active {
		transform: scale(0.96);
		box-shadow: 0 1px 4px rgba(79, 120, 255, 0.3);
	}
</style>