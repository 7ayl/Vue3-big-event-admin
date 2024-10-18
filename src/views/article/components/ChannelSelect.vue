<script setup>
import { artGetChannelsService } from '@/api/article.js'
import { ref } from 'vue'

defineProps({
  modelValue: {
    type: [Number, String]
  },
  width: {
    type: String
  }
})

const emit = defineEmits(['update:modelValue'])

const channelList = ref([])
const getChannelList = async () => {
  const res = await artGetChannelsService()
  channelList.value = res.data.data
  console.log(channelList.value)
}
getChannelList()
</script>

<template>
  <!-- label 展示给用户看的， value 是收集起来提交给后台的 -->
  <!-- $event可以直接获取当前元素的value，就会得到你选的那个value -->
  <!-- :modelValue用来子取父值，@update用来监听select框用户修改的值，然后通过emit回传到父组件 -->
  <el-select
    style="width: 200px"
    :modelValue="modelValue"
    @update:modelValue="emit('update:modelValue', $event)"
    :style="{ width }"
  >
    <el-option
      v-for="channel in channelList"
      :key="channel.id"
      :label="channel.cate_name"
      :value="channel.id"
    ></el-option>
    <el-option label="体育" value="137"></el-option>
  </el-select>
</template>
