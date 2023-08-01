
<script setup>
// script setup indicates Option API
// Vue 3 = just need to use import components
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import { ref } from 'vue';


// with composition, the variable are reactives and can be used on the template without explicitely defining them in the data()
// or method options
let items = ref([]);

// we use the addItemToList method to handle the custom event emitted by the HelloWorld component and add the new item to
// the items array
// Regarding the addItemToList function in the App.vue component, since it receives newItem as a parameter, you do not need
// to use .value inside the function. Instead, you directly use newItem, which is already the reactive value of the input field.

function addItemToList(newItem) {
  if( newItem )
  {
    items.value.push(newItem);
    console.log(newItem) // Add the new item with the label and purchased properties
    // items.value.push(newItem); // Add the new item with the label and purchased properties
    //    newItem.value = ''; // Reset the input field after adding the item
  }
};

// // Declare the "addItem" event using the "emits" option
const emits = defineEmits(['addItem']);

</script>

<template>
  <header>
    <!-- <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" /> -->

    <div class="wrapper">
      <HelloWorld msg="Shopping App" @addItem="addItemToList" />
      <!-- <HelloWorld msg="Shopping App" />
      <HelloWorld @addItem="addItemToList" /> -->
    </div>
  </header>

  <main>
    <!-- <TheWelcome /> -->
    <TheWelcome :items=items />
    <!-- <TheWelcome ref="theWelcome" :items="items" /> -->

  </main>
</template>


<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
