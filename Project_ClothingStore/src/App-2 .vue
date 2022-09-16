<script setup>
import { ref } from "vue";
// ข้อ2
const selectedColor = ref("");
const selectedSize = ref("");
const selectedDecoration = ref("");
const Text = ref("Hello");
const editText = () => {
  return (showEditText.value = true);
};
const showEditText = ref(false);
const newText = ref("");
const showNewText = () => {
  Text.value = newText.value
  showEditText.value = false
  newText.value = ""
  }
const reset = () => {
    selectedColor.value = ""
    selectedDecoration.value = ""
    selectedSize.value =""
    Text.value ="Hello"
}
</script>

<template>
  <div>
    <!-- ข้อ 2 -->
    <div>
      <!-- choose color -->
      <select class="bg-blue-50 border border-black" v-model="selectedColor">
        <option disabled value="">Please select color</option>
        <option value="red">red</option>
        <option value="yellow">yellow</option>
        <option value="green">green</option>
        <option value="blue">blue</option>
        <option value="purple">purple</option>
      </select>
      <!-- show color -->
      <span class="box border border-black">{{ selectedColor }}</span>
      <!-- choose size -->
      <select class="bg-blue-50 border border-black" v-model="selectedSize">
        <option disabled value="">Please select size</option>
        <option value="12px">12px</option>
        <option value="14px">14px</option>
        <option value="16px">16px</option>
        <option value="18px">18px</option>
        <option value="20px">20px</option>
      </select>
      <!-- choose decoration -->
      <select class="bg-blue-50 border border-black" v-model="selectedDecoration">
        <option disabled value="">Please select decoration</option>
        <option value="overline">overline</option>
        <option value="line-through">line through</option>
        <option value="underline">underline</option>
      </select>
    </div>
    <!-- button action -->
    <div>
      <button @click="editText" class="bg-red-100 border-2 border-black">
        Change
      </button>
      <button @click="reset" class="bg-red-100 mx-4 border-2 border-black">Reset</button>
    </div>
    <div v-show="showEditText">
      <input type="text" class="border-2 border-black" v-model="newText" />
      <button @click="showNewText" class="mx-2 border-2 border-black">
        Ok
      </button>
    </div>
    <!-- Text -->
    <div>
      <p class="textSize mt-2">
        {{ Text }}
      </p>
    </div>
  </div>
</template>

<style scope>
.box {
  width: 300px;
  height: 100px;
  padding-left: 20px;
  padding-right: 20px;
  background-color: v-bind(selectedColor);
}
.textSize {
  font-size: v-bind(selectedSize);
   background-color: v-bind(selectedColor);
   text-decoration: v-bind(selectedDecoration);
}
</style>
