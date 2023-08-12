<template>
  <td>
    <div class="input" @click="changeBtn">
      <textarea
        type="text"
        rows="3"
        cols="15"
        v-show="setInput"
        @click.stop="preventHide"
        @input="$emit('update:modelValue', $event.target.value)"
        :value="modelValue"
      />
      <p class="text">{{ modelValue }}</p>
    </div>
    <input
      type="checkbox"
      @click.stop="preventHide"
      name="free"
      v-model="isChecked"
      @click="freeTime"
    />
  </td>
</template>

<script setup>
import { defineProps, defineEmits, ref, onUpdated } from "vue";

const props = defineProps(["modelValue", "val"]);
const emit = defineEmits(["update:modelValue", "checkbox"]);

const setInput = ref(false);
const isChecked = ref(false);
const changeBtn = () => {
  setInput.value = !setInput.value;
  props.val.task = props.modelValue;
  //   console.log(props.val);
};
const preventHide = (event) => {
  event.stopPropagation();
};

const freeTime = () => {
  isChecked.value = !isChecked.value;
  //   console.log(props.val);
  props.val.completed = isChecked.value;
};

onUpdated(() => {
  //   console.log(props.val);
  emit("checkbox", props.val);
});
</script>

<style scoped>
.input {
  border: 1px black solid;
  height: 80px;
  width: 150px;
  text-align: center;
  box-sizing: border-box;
  overflow: hidden;
  text-overflow: justify-self;
  margin: 3px;
  word-wrap: break-word;
}
.text {
  font-size: 18px;
}
textarea {
  resize: none;
}

.btn {
  top: 50%;
  margin-top: 30%;
}
</style>
