<script setup lang='ts'>

import { ref, reactive } from 'vue';
import LogoImage from '@/assets/wuji.svg';

</script>

<template>

  <div class="flex gap-1 items-center h-[60px]">
    <van-image :src="LogoImage" width="32" height="32" />
    <span class="text-white">无极</span>
  </div>

</template>

<style scoped lang='less'>

</style>