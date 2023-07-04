<script setup>
import { onMounted, ref } from 'vue';
import axios from 'axios';
import Edit from './components/Edit.vue'


// TODO: List Rendering
// Basic logic: 1. Declare a reactive list.
              //2. Call an API to fetch data.
              //3. Assign the backend data to the list.
              //4. Bind the list to the table component.
const list = ref([])
const getList = async () =>{
    
    // Call the API
    const res = await axios.get('/list')
    // Assign to the 'list' variable
    list.value = res.data
}
onMounted(() => getList())


// TODO: Delete functionality
// Basic logic: 
//1. Get the ID of the current item 
//2. Call the delete API with the ID 
//3. Update the latest list
const onDelete = async(id) => {
    console.log(id)
    await axios.delete(`/del/${id}`)
    getList()

}


// TODO: Edit functionality
// Basic logic: 1. Open the dialog 2. Populate data 3. Update data

// 1. Open the dialog (get the instance of the child component, call methods, or modify properties)
// 2. Populate data (call the detail endpoint or use static data of the current row)
const editRef = ref(null)
const onEdit = (row) => {
  editRef.value.open(row)
}




</script>

<template>
  <div class="app">
    <el-table :data="list">
      <el-table-column label="ID" prop="id"></el-table-column>
      <el-table-column label="NAME" prop="name" width="150"></el-table-column>
      <el-table-column label="Plac Of Birth" prop="place"></el-table-column>
      <el-table-column label="Operation" width="150">
        <template #default="{ row }">
          <el-button type="primary" @click="onEdit(row)" link>Edit</el-button>
          <el-button type="danger" @click="onDelete(row.id)" link>Delete</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
  <Edit ref="editRef"  @on-update="getList"/>
</template>

<style scoped>
.app {
  width: 980px;
  margin: 100px auto 0;
}
</style>
