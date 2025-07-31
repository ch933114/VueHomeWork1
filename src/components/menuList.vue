<template>
  <div class="p-5">
    <table class="mx-auto">
      <thead>
        <tr>
          <th scope="col">品項</th>
          <th scope="col">描述</th>
          <th scope="col">價格</th>
          <th scope="col">庫存</th>
          <th scope="col">編輯</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in menuData" :key="item.id">
          <td>
            <template v-if="editId === item.id"
              ><input
                v-model="tempEditData.name"
                class="border px-1 w-[120px]"
                @keyup.enter="editId = null"
            /></template>
            <template v-else> {{ item.name }}</template>
          </td>
          <td>
            <small>{{ item.des }}</small>
          </td>
          <td>{{ item.price }}</td>
          <td>
            <button
              :disabled="item.quantity <= 0"
              @click="removeQuantity(item)"
              class="inline-block w-[20px] h-[20px] bg-primary-light disabled:bg-secondary hover:bg-accent1 active:bg-accent2"
            >
              -
            </button>
            <input class="w-[60px] text-center" type="text" v-model.number="item.quantity" /><button
              @click="addQuantity(item)"
              class="inline-block w-[20px] h-[20px] bg-primary-light hover:bg-accent1 active:bg-accent2"
            >
              +
            </button>
          </td>
          <td>
            <template v-if="editId === item.id">
              <button
                @click="saveEdit(item)"
                class="text-xs w-[40px] h-[20px] bg-danger text-white mx-1"
              >
                儲存
              </button>
              <button @click="cancelEdit" class="text-xs w-[40px] h-[20px] bg-gray-400 text-white">
                取消
              </button>
            </template>
            <template v-else>
              <button
                @click="startEdit(item)"
                class="text-xs w-[80px] h-[20px] bg-primary-light hover:bg-accent1 active:bg-accent2"
              >
                編輯
              </button>
            </template>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script setup>
import { ref } from 'vue'
const editId = ref(null)
const menuData = ref([
  {
    id: 1,
    name: '珍珠奶茶',
    des: '香濃奶茶搭配QQ珍珠',
    price: 50,
    quantity: 20,
  },
  {
    id: 2,
    name: '冬瓜檸檬',
    des: '清新冬瓜配上新鮮檸檬',
    price: 45,
    quantity: 18,
  },
  {
    id: 3,
    name: '翡翠檸檬',
    des: '綠茶與檸檬的完美結合',
    price: 55,
    quantity: 34,
  },
  {
    id: 4,
    name: '四季春茶',
    des: '香醇四季春茶，回甘無比',
    price: 45,
    quantity: 10,
  },
  {
    id: 5,
    name: '阿薩姆奶茶',
    des: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
    quantity: 25,
  },
  {
    id: 6,
    name: '檸檬冰茶',
    des: '檸檬與冰茶的清新組合',
    price: 45,
    quantity: 20,
  },
  {
    id: 7,
    name: '芒果綠茶',
    des: '芒果與綠茶的獨特風味',
    price: 55,
    quantity: 18,
  },
  {
    id: 8,
    name: '抹茶拿鐵',
    des: '抹茶與鮮奶的絕配',
    price: 60,
    quantity: 20,
  },
])

const tempEditData = ref({})

const startEdit = (item) => {
  editId.value = item.id
  tempEditData.value = { ...item }
}

const saveEdit = (item) => {
  const index = menuData.value.findIndex((i) => i.id === item.id)
  if (index !== -1) {
    menuData.value[index] = { ...tempEditData.value }
  }
  editId.value = null
}

const cancelEdit = () => {
  editId.value = null
}

const removeQuantity = (item) => {
  item.quantity -= 1
}

const addQuantity = (item) => {
  item.quantity += 1
}
</script>
