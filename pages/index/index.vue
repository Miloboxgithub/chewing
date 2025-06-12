<template>
  <loading :show="isLoading"></loading>
  <view class="page-container">
    <view class="app-title"><text class="www">口香糖缺陷检测系统</text></view>
    <view class="card">
      <view class="chat-header">实时图像展示</view>
      <view class="chat-window">
        <view class="imgs" v-for="item in items">
          <img :src="item.src" alt="" />
        </view>
        <view style="width: 100%; height: 30px;">
          
        </view>
          
      </view>
    </view>
    <view class="datas">
      <view class="data-item">
        <view class="data-label">缺肉数量：</view>
        <view class="data-value">0</view>
      </view>
      <view class="data-item">
        <view class="data-label">堵塞状态：</view>
        <view class="data-value">正常</view>
      </view>
    </view>
    <view class="btns">
      <view class="btn"> 开始 </view>
      <view class="btn"> 暂停 </view>
      <view class="btn"> 结束 </view>
    </view>
  </view>
</template>

<script setup>
import { ref } from "vue";
import { onShow, onLoad, onReachBottom } from "@dcloudio/uni-app";
import Loading from "../../components/Loading.vue";

const items = ref([
  { id: 1, src: "https://picsum.photos/200" },
  { id: 2, src: "https://picsum.photos/200" },
  { id: 3, src: "https://picsum.photos/200" },
  { id: 4, src: "https://picsum.photos/200" },
  { id: 5, src: "https://picsum.photos/200" },
  { id: 6, src: "https://picsum.photos/200" },
]);
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
  height: 64px;
  padding: 16px 8px;
  background: linear-gradient(135deg, #4F78FF 0%, #3a5bd9 100%);
  color: white;
  font-size: 20px;
  font-weight: bold;
  text-align: center;
  box-shadow: 0 4px 15px rgba(79, 120, 255, 0.3);
  margin-bottom: 15px;
  position: relative;
  letter-spacing: 1px;
}
.www{
  position: absolute;
  left: 50px;
  top: 51.5px;
}
.app-title::before {
  content: "";
  position: absolute;
  left: 20px;
  top: 54px;
  width: 24px;
  height: 24px;
  background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="white"><path d="M12 2L4 5v6.09c0 5.05 3.41 9.76 8 10.91 4.59-1.15 8-5.86 8-10.91V5l-8-3zm-1.06 13.54L7.4 12l1.41-1.41 2.12 2.12 4.24-4.24 1.41 1.41-5.64 5.66z"/></svg>');
  background-size: contain;
  background-repeat: no-repeat;
}

// .app-title::after {
//   content: "";
//   position: absolute;
//   right: 20px;
//   top: 50%;
//   transform: translateY(-50%);
//   width: 24px;
//   height: 24px;
//   background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="white"><path d="M12 2L4 5v6.09c0 5.05 3.41 9.76 8 10.91 4.59-1.15 8-5.86 8-10.91V5l-8-3zm-1.06 13.54L7.4 12l1.41-1.41 2.12 2.12 4.24-4.24 1.41 1.41-5.64 5.66z"/></svg>');
//   background-size: contain;
//   background-repeat: no-repeat;
// }

.card {
  margin-top: 5px;
  width: 90vw;
  background-color: #fff;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(79, 120, 255, 0.1);
  overflow: hidden;
}

.chat-header {
  background-color: #4F78FF;
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
  color: #4F78FF;
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
  background-color: #4F78FF;
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
