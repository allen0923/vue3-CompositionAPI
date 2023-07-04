<script setup>
// TODO: Edit
import { ref, defineExpose, onUpdated } from 'vue'
import axios from 'axios'
// Dialog visibility
const dialogVisible = ref(false)


//Prepare Form
const form = ref({
  name: '',
  place: '',
  id: ''
})

const open = (row) => {
  console.log(row)
  //name
  form.value.name = row.name
  //place
  form.value.place = row.place
  //id
  form.value.id = row.id
  dialogVisible.value = true
}
defineExpose({
  open
})

//Update
const emit = defineEmits(['on-update'])
const onUpdate = async () => {
  //1.Collect form data, call the API
  await axios.patch(`/edit/${form.value.id}`, {
    name: form.value.name,
    place: form.value.place,
  })
  //2.Close the dialog
  dialogVisible.value = false
  //3.Notify parent component to update the list
  emit('on-update')

}

</script>

<template>
  <el-dialog v-model="dialogVisible" title="Edit" width="400px">
    <el-form label-width="60px">
      <el-form-item label="Name ">
        <el-input placeholder="Enter your Name" v-model="form.name" />
      </el-form-item>
      <el-form-item label="Place" >
        <el-input placeholder="Enter your Place of Birth"  v-model="form.place" />
      </el-form-item>
    </el-form>
    <template #footer>
      <span class="dialog-footer">
        <el-button @click="dialogVisible = false">Cancel</el-button>
        <el-button type="primary" @click="onUpdate">Confirm</el-button>
      </span>
    </template>
  </el-dialog>
</template>

<style scoped>
.el-input {
  width: 290px;
}
</style>
