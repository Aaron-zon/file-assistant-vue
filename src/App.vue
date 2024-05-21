<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { RouterLink, RouterView } from 'vue-router'
import axios from 'axios'

onMounted(() => {
  axios.get('http://localhost:8080/getFolderStructure')
    .then((resp) => {
      console.log(resp.data.data)
      data.value = resp.data.data
    })
})
const columns = [
  {
    key: 'name',
    dataKey: 'fileName',
    title: 'Name',
    width: 150,
  },
  {
    key: 'size',
    dataKey: 'fileSize',
    title: 'Size',
    width: 150,
  },
  {
    key: 'date',
    dataKey: 'updateDate',
    title: 'Last update date',
    width: 150,
  }
]
const data = ref([
  {
    fileName: '123',
    fileSize: '1554k',
    date: '2023-01-01'
  }
])
</script>

<template>
  <div class="wrapper">
    <div class="box-left"></div>
    <div class="box-right">
      <div class="breadcrumb">
        <el-breadcrumb separator="/">
          <el-breadcrumb-item :to="{ path: '/' }">homepage</el-breadcrumb-item>
          <el-breadcrumb-item>
            <a href="/">promotion management</a>
          </el-breadcrumb-item>
          <el-breadcrumb-item>promotion list</el-breadcrumb-item>
          <el-breadcrumb-item>promotion detail</el-breadcrumb-item>
        </el-breadcrumb>

      </div>

      <div class="table-cantainer">
        <el-table-v2
          :columns="columns"
          :data="data"
          :width="700"
          :height="400"
          fixed
        />
      </div>
    </div>
  </div>
</template>

<style scoped>
.wrapper {
  border: 1px solid black;

}
</style>
