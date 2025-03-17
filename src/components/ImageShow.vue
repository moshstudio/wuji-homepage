<script setup lang="ts">
import { ref, reactive } from "vue";

const props = defineProps({
  winImage: String,
  mobileImage: String,
});
</script>

<template>
    <div class="relative flex flex-col gap-2 items-center w-[250px] h-[200px]">
    <van-image
      :src="props.winImage"
      width="250"
      height="130"
      class="shadow"
    />
    <div class="shadow-lg absolute right-0 bottom-8">
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
