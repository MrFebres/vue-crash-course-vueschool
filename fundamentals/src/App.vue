<script setup>
import { computed, reactive, ref } from "vue";

// const state = reactive({ count: 0 });
const characterCount = computed(() => newItem.value.length);
const header = ref("Shopping List App");
const editing = ref(false);
const items = ref([
  { id: 1, label: "10 party hats", purchased: true, highPriority: false },
  { id: 2, label: "2 board games", purchased: true, highPriority: false },
  { id: 3, label: "20 cups", purchased: false, highPriority: true },
]);
const reversedItems = computed(() => Array.from(items.value).reverse());
const newItem = ref("");
const newItemHighPriority = ref(false);
const doEdit = (e) => {
  editing.value = e;
  newItem.value = "";
};

const saveItem = () => {
  items.value.push({
    highPriority: newItemHighPriority.value,
    id: items.value.length + 1,
    label: newItem.value,
  });
  newItem.value = "";
  newItemHighPriority.value = false;
};

const togglePurchased = (item) => {
  item.purchased = !item.purchased;
};
</script>

<template>
  <div class="header">
    <h1>{{ header }}</h1>
    <button @click="doEdit(false)" class="btn" v-if="editing">Cancel</button>
    <button @click="doEdit(true)" class="btn btn-primary" v-else>
      Add Item
    </button>
  </div>
  <form @submit.prevent="saveItem" class="add-item-form" v-if="editing">
    <input placeholder="Add an item" type="text" v-model.trim="newItem" />
    <label>
      <input type="checkbox" v-model="newItemHighPriority" />
      High Priority
    </label>
    <button :disabled="newItem.length === 0" class="btn btn-primary">
      Save Item
    </button>
  </form>
  <p class="counter" v-if="editing">{{ characterCount }}/200</p>
  <br />
  <ul>
    <li
      :class="{ strikeout: purchased, priority: highPriority }"
      :key="id"
      @click="togglePurchased(items[index])"
      class="static-class"
      v-for="({ id, label, purchased, highPriority }, index) in reversedItems"
    >
      {{ label }}
    </li>
  </ul>
  <p v-if="!items.length">Nothin to see here</p>
</template>
