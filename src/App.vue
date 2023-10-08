<template>
  <el-table :data="data" style="width: 100%">
    <el-table-column prop="id" label="#" width="55" sortable/>
    <el-table-column prop="used" label="Used" width="55" />
    <el-table-column prop="articul" label="Артикул" width="155" />
  <el-table-column prop="date" label="Дата" width="190" />
  <el-table-column prop="info" label="Текст" />
  </el-table>
  <el-pagination background layout="prev, pager, next"
                 :pager-count="4"
                 :page-size="limit"
                 v-model:current-page="page"
                 :total="100" />
</template>

<script setup>

import {computed, ref} from "vue";
import { useFetch} from "@vueuse/core";

const limit = ref(15)
const page  = ref(1)
const url = computed(()=>{
  return `http://192.168.50.5:3002/tovars?page=${page.value-1}&npp=${limit.value}`
})
const {isFetching, error, data} = useFetch(url, {
  refetch: true
}).json();
</script>

<style scoped>

</style>
