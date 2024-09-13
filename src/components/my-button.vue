<template>
  <div>{{ title }}:</div>
  <a-button ref="buttonRef" v-bind="attrs">
    <template #[slotName] v-for="(slot, slotName) in $slots">
      <slot :name="slotName"></slot>
    </template>
  </a-button>
</template>

<script setup lang="ts">
import { computed, onMounted, ref, unref, useAttrs, useSlots } from 'vue'
import { Button } from 'ant-design-vue'

defineProps({
  title: { type: String, default: '点击' }
})

const buttonRef = ref()

// 获取 $attrs 对象
const attrs = useAttrs()
console.log(`output->attrs`, attrs)
const filteredAttrs = computed(() => {
  return { ...attrs, class: undefined }
})

const slots = useSlots()
console.log(`output->slots`, slots)

const expose: Record<string, () => any> = {}

onMounted(() => {
  console.log('buttonRef', buttonRef.value)
  const entries = Object.entries(buttonRef.value)
  console.log(`output->entries`, entries)

  Object.keys(buttonRef.value).forEach((key) => {
    if (typeof buttonRef.value[key] === 'function') {
      expose[key] = buttonRef.value[key]
    }
  })
})

function updated() {
  console.log('子组件updated')
}

// 暴露方法出去
expose['updated'] = updated
defineExpose(
  expose as unknown as InstanceType<typeof Button> & {
    updated: typeof updated
  }
)
//defineExpose({...expose,updated});
</script>
