<script setup>
import { ref, reactive } from "vue";
import Logo from "./components/Logo.vue";
import LogoImage from "./assets/wuji.svg";
import ImageShow from "./components/ImageShow.vue";
import AndroidSvg from "./assets/android.svg";
import WinSvg from "./assets/win.svg";
import BookWin from "./assets/images/win/book_win.png";
import BookMobile from "./assets/images/mobile/book_mobile.png";
import ComicWin from "./assets/images/win/comic_win.png";
import ComicMobile from "./assets/images/mobile/comic_mobile.png";
import PhotoWin from "./assets/images/win/photo_win.jpg";
import PhotoMobile from "./assets/images/mobile/photo_mobile.png";
import SongWin from "./assets/images/win/song_win.png";
import SongMobile from "./assets/images/mobile/song_mobile.png";
import VideoWin from "./assets/images/win/video_win.jpg";
import VideoMobile from "./assets/images/mobile/video_mobile.jpg";
import { androidDownloadLink, WinDownloadLink } from "./links";

const scrollToDownload = () => {
  document.querySelector(".download").scrollIntoView({
    behavior: "instant",
  });
};

const images = [
  {
    winImage: PhotoWin,
    mobileImage: PhotoMobile,
  },
  {
    winImage: SongWin,
    mobileImage: SongMobile,
  },
  {
    winImage: BookWin,
    mobileImage: BookMobile,
  },
  {
    winImage: ComicWin,
    mobileImage: ComicMobile,
  },
  {
    winImage: VideoWin,
    mobileImage: VideoMobile,
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
    <p
      class="font-bold animated-gradient-text mx-auto pt-[20vh]"
      style="font-size: clamp(1.3rem, 7vw, 3.5rem); white-space: nowrap"
    >
      音乐、书籍、图片、漫画、影视
    </p>

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

    <div class="relative w-full overflow-hidden py-[200px]">
      <div class="flex gap-[10vw] animate-infinite-scroll">
        <!-- 第一组图片 -->
        <div
          v-for="(item, index) in images"
          :key="`first-${index}`"
        >
          <ImageShow
            :winImage="item.winImage"
            :mobileImage="item.mobileImage"
          />
        </div>

        <!-- 第二组重复图片 -->
        <div
          v-for="(item, index) in images"
          :key="`second-${index}`"
        >
          <ImageShow
            :winImage="item.winImage"
            :mobileImage="item.mobileImage"
          />
        </div>
      </div>
    </div>
    <div class="download flex w-full justify-around gap-4 pt-[20vh] pb-[50vh]">
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
.animate-infinite-scroll {
  animation: infinite-scroll 30s linear infinite;
  display: flex;
  width: max-content;
}

@keyframes infinite-scroll {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-50%);
  }
}

.hide-scrollbar {
  -ms-overflow-style: none;
  scrollbar-width: none;
}
.hide-scrollbar::-webkit-scrollbar {
  display: none;
}
</style>
