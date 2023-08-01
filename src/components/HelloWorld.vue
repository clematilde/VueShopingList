<script setup>

import { ref, defineProps, defineEmits } from 'vue';


// props are custom attribute you can register on a component

defineProps({
  msg: {
    type: String,
    required: true
  },
});

let newItem = ref('');
let newItemHighPriority = ref('false');
let editing = ref(false);

// defineEmits function to define the emit function, which is then used to emit the custom event "addItem" with the new item
// data when the button is clicked.
const emit = defineEmits(['addItem']);


// When emitting a custom event using the emit function, you do not need to use .value.
// When using ref to declare a reactive variable, you should use .value to access its value.


function addItem() {
  console.log(newItem.value)
  emit('addItem', { label: newItem.value, purchased: true }); // Pass the new item object with label and purchased properties
};


function doEdit() {
  editing.value = !editing.value;
};

</script>

<template>
  <div class="greetings">
    <div class="header">
      <h1 class="green">
        {{ msg.toLocaleUpperCase() }}
      </h1>
      <button v-if="editing" @click="doEdit(false)" class="btn btn-cancel">Cancel</button>
      <button v-else @click="doEdit(true)" class="btn btn-primary">Add Item</button>
    </div>
    <h3>
      Add your items on the list before forgetting about it!
    </h3>
  </div>

  <div v-if="editing" class="add-items-form">
    <input
    type="text"
    placeholder="Add an item"
    v-model="newItem"
    @keydown.enter="addItem"
  />

    <label>
      <input type="checkbox" v-model="newItemHighPriority">High Priority
    </label>


    <!-- <button @click="$emit('addItem')" class="btn btn-primary">Save Item</button> -->
    <!-- v-bind = :disabled // v-on: ©-->
    <button
      v-bind:disabled="newItem.length === 0"
      @click="addItem"
      class='btn btn-primary'
    >Save Item</button>


  </div>



</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
