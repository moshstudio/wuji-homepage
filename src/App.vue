<script setup>
import { ref, reactive } from "vue";
import Logo from "./components/Logo.vue";
import LogoImage from "./assets/wuji.svg";
import ImageShow from "./components/ImageShow.vue";
import AndroidSvg from "./assets/android.svg";
import WinSvg from "./assets/win.svg";
import { androidDownloadLink, WinDownloadLink } from "./links";

const scrollToDownload = () => {
  document.querySelector(".download").scrollIntoView({
    behavior: "instant",
  });
};

const images = [
  {
    winImage: "https://image-bed.s3.bitiful.net/wuji-home%2Fphoto_win.jpg",
    mobileImage:
      "https://image-bed.s3.bitiful.net/wuji-home%2Fphoto_mobile.jpg",
  },
  {
    winImage: "https://image-bed.s3.bitiful.net/wuji-home%2Fsong_win.jpg",
    mobileImage: "https://image-bed.s3.bitiful.net/wuji-home%2Fsong_mobile.jpg",
  },
  {
    winImage: "https://image-bed.s3.bitiful.net/wuji-home%2Fbook_win.jpg",
    mobileImage: "https://image-bed.s3.bitiful.net/wuji-home%2Fbook_mobile.jpg",
  },
  {
    winImage: "https://image-bed.s3.bitiful.net/wuji-home%2Fcomic_win.jpg",
    mobileImage:
      "https://image-bed.s3.bitiful.net/wuji-home%2Fcomic_mobile.jpg",
  },
];

function isMobileDevice() {
  return /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(
    navigator.userAgent
  );
}
function downloadFile(url) {
  const link = document.createElement("a");
  link.href = url;
  link.download = ""; // 设置 download 属性，确保文件下载而不是跳转
  link.style.display = "none"; // 隐藏链接
  document.body.appendChild(link);
  link.click(); // 触发点击
  document.body.removeChild(link); // 移除链接
}

function getDownloadLink() {
  if (isMobileDevice()) {
    downloadFile(androidDownloadLink);
  } else {
    downloadFile(WinDownloadLink);
  }
}
</script>

<template>
  <div
    class="flex flex-col gap-2 items-center justify-start w-screen h-screen overflow-y-auto hide-scrollbar bg-[#101218] text-white"
  >
    <div class="flex w-full items-center justify-between px-6">
      <Logo></Logo>
      <van-button
        size="small"
        @click="getDownloadLink"
        >立即下载</van-button
      >
    </div>
    <aos-vue
      animation="fade-up"
      :offset="10"
    >
      <p
        class="font-bold animated-gradient-text mx-auto pt-[20vh]"
        style="font-size: clamp(1.5rem, 8vw, 4rem); white-space: nowrap"
      >
        音乐、书籍、图片、漫画
      </p>
    </aos-vue>
    <aos-vue
      animation="fade-up"
      :duration="800"
    >
      <div class="flex flex-col gap-2 items-center w-[150px] pt-[20vh]">
        <van-button
          size="large"
          color="linear-gradient(to right, #ff6034, #ee0a24)"
          @click="getDownloadLink"
        >
          <template #icon>
            <div class="flex items-center">
              <van-image
                :src="LogoImage"
                width="28"
                height="28"
              />
            </div>
          </template>
          立即获取无极
        </van-button>
        <p
          class="text-base text-gray-500 underline underline-offset-4 cursor-pointer"
          @click="scrollToDownload"
        >
          查看所有下载选项
        </p>
      </div>
    </aos-vue>

    <div
      class="w-full flex justify-around flex-wrap gap-4 mt-[120px] mb-[20vh]"
    >
      <ImageShow
        v-for="(item, index) in images"
        :key="index"
        :winImage="item.winImage"
        :mobileImage="item.mobileImage"
      ></ImageShow>
    </div>
    <div class="download flex w-full justify-around gap-4 mt-[40px] mb-[30vh]">
      <div class="flex flex-col gap-2 items-center">
        <van-image
          :src="WinSvg"
          width="80"
          height="80"
        ></van-image>
        <p class="text-sm text-gray-400">windows10, 11</p>
        <van-button
          color="linear-gradient(to right, #ff6034, #ee0a24)"
          @click="() => downloadFile(WinDownloadLink)"
        >
          下载电脑版
        </van-button>
      </div>

      <div class="flex flex-col gap-2 items-center">
        <van-image
          :src="AndroidSvg"
          width="80"
          height="80"
          color="gray"
        ></van-image>
        <p class="text-sm text-gray-400">android</p>
        <van-button
          color="linear-gradient(to right, #ff6034, #ee0a24)"
          @click="() => downloadFile(androidDownloadLink)"
        >
          下载安卓版
        </van-button>
      </div>
    </div>
  </div>
</template>

<style scoped lang="less">
body {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
}
/* 隐藏滚动条 */
.hide-scrollbar::-webkit-scrollbar {
  display: none;
}

.hide-scrollbar {
  -ms-overflow-style: none; /* IE and Edge */
  scrollbar-width: none; /* Firefox */
}

@keyframes gradientBackground {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

.animated-gradient-text {
  background: linear-gradient(270deg, #313ddf, #feb47b, #ff7e5f);
  background-size: 200% 200%;
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  animation: gradientBackground 5s ease infinite;
}
</style>
