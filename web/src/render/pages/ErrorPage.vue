<template>
  <div class="result-page-wrap">
    <div class="result-page">
      <div class="error-wrapper">
        <img class="error-img" :src="errorImageUrl" />
        <div class="bottom-word" v-html="errorMsg"></div>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
import { computed } from 'vue'
import { useStore } from 'vuex'

const store = useStore()

const errorImageUrl = computed(() => {
  const errorType = store.state?.errorInfo?.errorType
  const imageMap = {
    overTime: '/imgs/icons/overtime.webp',
    default: '/imgs/icons/error.webp'
  }

  return imageMap[errorType as 'overTime'] || imageMap.default
})

const errorMsg = computed(() => store.state?.errorInfo?.errorMsg)
</script>
<style lang="scss" scoped>
.result-page-wrap {
  width: 100%;
  flex: 1;
  text-align: center;
  overflow: hidden;
  background: var(--primary-background-color);

  padding: 0 0.3rem;
  .result-page {
    background: rgba(255, 255, 255, var(--opacity));
    display: flex;
    flex-direction: column;
    height: 100%;
  }
}
.error-wrapper {
  text-align: center;
  font-size: 14px;
  flex: 1;

  p {
    text-align: center;
  }

  .error-img {
    margin-top: 2rem;
    margin-bottom: 30px;
    width: 2rem;
    height: auto;
  }

  .bottom-word {
    color: #999;
    margin-top: 10px;
  }
}
</style>
