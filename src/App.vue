<script setup>
import { reactive, ref, watch, computed } from "vue";

const leftItems = reactive([
  {
    id: 1,
    name: "Shoes 1",
  },
  {
    id: 2,
    name: "Shoes 2",
  },
  {
    id: 3,
    name: "Shoes 3",
  },
  {
    id: 4,
    name: "Shoes 4",
  },
  {
    id: 5,
    name: "T-shirt 1",
  },
  {
    id: 6,
    name: "T-shirt 2",
  },
  {
    id: 7,
    name: "T-shirt 3",
  },
  {
    id: 8,
    name: "T-shirt 4",
  },
]);

const rightItems = reactive([
  {
    id: 11,
    name: "Jacket 1",
  },
  {
    id: 12,
    name: "Jacket 2",
  },
  {
    id: 13,
    name: "Jacket 3",
  },
  {
    id: 14,
    name: "Jacket 4",
  },
  {
    id: 15,
    name: "Hoodie 1",
  },
  {
    id: 16,
    name: "Hoodie 2",
  },
  {
    id: 17,
    name: "Hoodie 3",
  },
  {
    id: 18,
    name: "Hoodie 4",
  },
]);

const selectedRight = ref([]);
const selectedLeft = ref([]);

// Счетчик
const count = ref(6);
</script>

<template>
  <div class="layout">
    <div class="box-left">
      <div class="box-top">
        <div v-if="selectedLeft.length > 0" class="box-top__items">
          <div v-for="(item, index) in selectedLeft" :key="item.id" class="box-top__item item">{{ item.name }}</div>
        </div>
        Selected: {{ selectedLeft.length }} / {{ count }}
      </div>
      <div class="box-items">
        <div
          v-for="(item, index) in leftItems"
          :key="item.id"
          :class="['item', { disabled: selectedLeft.length >= count && !selectedLeft.some((selected) => selected.id === item.id) }]"
        >
          <input :id="item.id" type="checkbox" v-model="selectedLeft" :value="item" />
          <label :for="item.id">{{ item.name }}</label>
        </div>
      </div>
    </div>
    <div class="box-right">
      <div class="box-top">
        Selected: {{ selectedRight.name }}
        <div v-if="selectedRight.length > 0" class="box-top__items">
          <div class="box-top__item item">{{ selectedRight.name }}</div>
        </div>
      </div>
      <div class="box-items">
        <div v-for="(item, index) in rightItems" :key="item.id" class="item">
          <input :id="item.id" type="radio" v-model="selectedRight" :value="item" />
          <label :for="item.id">{{ item.name }}</label>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.layout {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
  width: 100%;
}
.box-left {
  display: grid;
  gap: 20px;
}
.box-top {
  border: 2px solid black;
  min-height: 300px;
}
.box-top__items {
  display: grid;
  gap: 10px;
  grid-template-columns: repeat(3, 1fr);
}

.box-items {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}
.box-right {
  display: grid;
  gap: 20px;
}

.item {
  width: 100px;
  height: 100px;
  border: 1px solid black;
  display: grid;
  place-items: center;
}
.item input {
  clip: rect(0 0 0 0);
  clip-path: inset(50%);
  height: 1px;
  overflow: hidden;
  position: absolute;
  white-space: nowrap;
  width: 1px;
}
.item label {
  font-weight: 600;
  cursor: pointer;
  border: 1px solid black;
  width: 100%;
  height: 100px;
}
.item.disabled {
  background-color: gray;
  pointer-events: none;
}
</style>
