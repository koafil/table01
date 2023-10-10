<template>
  <div>
<!--    {{ data }}-->
  </div>
  <el-select v-model="limit" class="m-2" placeholder="Select">
    <el-option
        v-for="item in limitList"
        :key="item.value"
        :label="item.label"
        :value="item.value"
    >
      {{ item.label }}
    </el-option>>

  </el-select>
  <el-table :data="data?.rowData" border style="width: 100%">
    <el-table-column prop="id" label="id" width="65" sortable/>
    <el-table-column prop="used" label="Used" width="55" />
    <el-table-column prop="articul" label="Артикул" width="155" />
  <el-table-column prop="date" label="Дата" width="190" />
  <el-table-column prop="info" label="Текст" />
  </el-table>
  <el-pagination background layout="prev, pager, next"
                 :pager-count="7"
                 :page-size="limit"
                 v-model:current-page="page"
                 :total="data?.total?data.total:0" />
</template>

<script setup>

import {computed, ref} from "vue";
import { useFetch} from "@vueuse/core";

const limitList = [
  {
    value: 5,
    label: '5 строк',
  },
  {
    value: 15,
    label: '15 строк',
  },
  {
    value: 20,
    label: '20 строк',
  },
  {
    value: 50,
    label: '50 строк',
  },
]
const limit = ref(20)
const page  = ref(1)
const url = computed(()=>{
  return `http://192.168.50.5:3002/tovars?page=${page.value}&npp=${limit.value}`
})
const {isFetching, error, data } = useFetch(url, {
  refetch: true
}).json();
</script>

<style scoped>

</style>
