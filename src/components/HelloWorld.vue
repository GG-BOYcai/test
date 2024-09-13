<template>
  <div>
    <my-button ref="myRef" ghost type="primary" title="请点击" @click="handleClick">
      查询
      <template #icon><SearchOutlined /></template>
    </my-button>

    <div @click="handleClick2" class="btn"></div>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { SearchOutlined } from '@ant-design/icons-vue'
import MyButton from './my-button.vue'

const myRef = ref()

onMounted(() => {
  console.log('myRef', myRef.value)
})
function handleClick(e: any) {
  console.log('父组件点击了：', e)
}

function handleClick2() {
  console.log('点击了')
  myRef.value.focus()
}
</script>
<style>
.content {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.logo {
  margin: 200rpx auto 50rpx;
  width: 200rpx;
  height: 200rpx;
}

.text-area {
  display: flex;
  justify-content: center;
}

.btn {
  width: 200px;
  height: 200px;
  background: aquamarine;
}
</style>
