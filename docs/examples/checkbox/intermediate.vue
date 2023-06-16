<template>
  <el-checkbox
    v-model="checkAll"
    :indeterminate="isIndeterminate"
    @change="handleCheckAllChange"
    >Check all</el-checkbox
  >
  <el-checkbox-group
    v-model="checkedCities"
    @change="handleCheckedCitiesChange"
  >
    <el-checkbox v-for="city in cities" :key="city" :label="city">{{
      city
    }}</el-checkbox>
  </el-checkbox-group>
</template>

<script lang="ts" setup>
import { ref } from 'vue'

const checkAll = ref(false)
const isIndeterminate = ref(true)
const checkedCities = ref(['Shanghai', 'Beijing'])
const cities = [ {
          props: "name",
          columnName: "候选人姓名",
          columnText: "候选人的姓名",
          isShow: true,
          width: "150px"
        },
        {
          props: "mobile",
          columnName: "手机号码",
          columnText: "候选人的手机号码",
          isShow: true,
          width: "150px"
        },
        {
          props: "organizationUnit",
          columnName: "应聘部门",
          columnText: "候选人的应聘的部门名称",
          isShow: true,
          width: "150px"
        },]

const handleCheckAllChange = (val: boolean) => {
  checkedCities.value = val ? cities : []
  isIndeterminate.value = false
}
const handleCheckedCitiesChange = (value: string[]) => {
  const checkedCount = value.length
  checkAll.value = checkedCount === cities.length
  isIndeterminate.value = checkedCount > 0 && checkedCount < cities.length
}
</script>
