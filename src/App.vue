<script setup>
import { ref } from 'vue'

let tasks = ref([{ name: 'Task 1', time: 60 }, { name: 'Task 2', time: 75 }])
let isAddBtnClicked = ref(false)
let nameError = ref("")
let name = ref("")
let time = ref(0)


const removeTask = (index) => {
  tasks.value = tasks.value.filter((_, i) => i !== index)
}

const handleToggle = () => {
  isAddBtnClicked.value = !isAddBtnClicked.value
}

const handleFormSubmit = () => {
  if (!name.value) {
    nameError.value = "Please enter a name!"
    return
  }
  tasks.value.push({ name: name.value, time: time.value })
  name.value = ""
  time.value = 0
  nameError.value = ""
  isAddBtnClicked.value = false
}

</script>

<template>
  <div class="flex justify-center items-center min-h-screen bg-gradient-to-b from-blue-300 via-indigo-300 to-purple-300">
    <div v-show="isAddBtnClicked" class="w-96 h-80 p-5 rounded-xl bg-slate-200">
      <form action="">
        <p class="text-3xl font-semibold text-center border-b-2 border-gray-300">Add Task</p>
        <div class="mt-2">
          <label for="" class="text-2xl">Name</label>
          <input type="text" class="block focus:outline-none border-2 border-blue-200 rounded p-1 w-full" v-model="name">
          <small v-show="nameError" class="text-red-500">*{{ nameError }}</small>
        </div>
        <div class="my-3">
          <label for="" class="text-2xl">Time</label>
          <input type="number" class="block focus:outline-none border-2 border-blue-200 rounded p-1 w-full"
            v-model="time">
        </div>
        <div class="mt-8">
          <input @click.prevent="handleFormSubmit()" type="button" value="Add"
            class="w-full bg-blue-400 text-white hover:bg-blue-500 p-2 rounded font-semibold">
        </div>
      </form>
    </div>
    <div v-show="!isAddBtnClicked" class="w-1/2 h-[700px] rounded-xl">
      <div class="flex h-full">
        <div
          class="w-1/3 min-h-full bg-gradient-to-b from-green-300 to-blue-400 rounded-xl flex flex-col items-center justify-center">
          <button
            class="w-40 border-2 font-semibold border-white text-white p-2 rounded-md hover:bg-white hover:text-black"
            @click="handleToggle">Add
            Task</button>
        </div>
        <div class="h-full w-full rounded-xl bg-gradient-to-b from-purple-300 via-indigo-300 to-blue-300">
          <div
            class="text-center font-semibold w-4/5 bg-slate-200 mx-auto my-2 px-3 py-3 rounded-full hover:bg-slate-200 flex justify-between items-center hover:shadow-lg">
            <div class="flex justify-between w-full">
              <span>Name</span>
              <span>Time</span>
              <span class="text-center w-40">Action</span>
            </div>
          </div>
          <div v-for="(task, index) in tasks"
            class="text-center font-semibold w-4/5 bg-slate-100 mx-auto my-2 px-3 py-1 rounded-full hover:bg-slate-200 flex justify-between items-center hover:shadow-lg hover:cursor-pointer">
            <div class="flex justify-between items-center w-full" :key="index">
              <span class="text-center">{{ task.name }}</span>
              <span class="text-center">{{ task.time }}</span>
              <span class="w-40 border-2 border-red-400 text-red-400 p-2 rounded-full hover:bg-red-400 hover:text-white"
                @click="removeTask(index)">Remove</span>
            </div>

          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped></style>
