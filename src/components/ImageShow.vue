<script setup lang="ts">
import { ref, reactive } from "vue";

const props = defineProps({
  winImage: String,
  mobileImage: String,
});
</script>

<template>
  <div class="relative flex flex-col gap-4 items-center ">
    <van-image
      :src="props.winImage"
      width="250"
      height="130"
      class="shadow"
    />
    <div class="shadow-lg absolute right-0 bottom-[0px]">
      <van-image
        :src="props.mobileImage"
        width="100"
        height="200"
        class=""
      />
    </div>
  </div>
</template>

<style scoped lang="less"></style>
