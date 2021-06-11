<template>
  <div class="col-md-4" style="background-color: bisque">
    <div class="book1">
      <img :src="src" class="img-thumbnail" style="max-width: 60%" />
      <div class="card-body" style="margin-top: 20px; font-size: 15px">
        <div class="card-title">{{ name }}</div>
        <h3 class="price">ราคา {{ price }}</h3>
        <div class="group">
          <p style="margin-left: -50px; margin-bottom: 5px">จำนวนเล่ม</p>
          <input
            v-model="itemcount"
            type="number"
            min="1"
            style="text-align: center; max-width: 40px; margin-right: 5px"
          />

          <button type="button" class="btn btn-success" @click="clickbuy">
            ซื้อ
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent, onMounted, ref } from "@vue/runtime-core";

export default defineComponent({
  props: {
    src: String,
    name: String,
    price: Number,
    id: Number,
  },
  emits: ["buy"],
  setup(props, context) {
    const itemcount = ref(0);
    function clickbuy() {
      const data = {
        id: props.id,
        name: props.name,
        price: props.price,
        count: itemcount.value,
      };

      context.emit("buy", data);
    }
    function add() {
      itemcount++;
    }

    return { itemcount, clickbuy, add };
  },
});
</script>

<style></style>
