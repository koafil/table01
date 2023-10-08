<template>
  <el-table :data="data" style="width: 100%">
  <el-table-column prop="id" label="#" width="70" sortable/>
  <el-table-column prop="title" label="Название" width="180" />
  <el-table-column prop="body" label="Текст" />
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

const limit = ref(5)
const page  = ref(1)
const url = computed(()=>{
  return `https://jsonplaceholder.typicode.com/posts?_page=${page.value}&_limit=${limit.value}`
})
const {isFetching, error, data} = useFetch(url, {
  refetch: true
}).json();
</script>

<style scoped>

</style>
