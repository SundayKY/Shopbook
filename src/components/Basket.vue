<template>
  <div>DeFuQ!</div>
  <div class="container">
    <table class="table">
      <thead>
        <tr>
          <th scope="col">id</th>
          <th scope="col">name</th>
          <th scope="col">price</th>
          <th scope="col">count</th>
        </tr>
      </thead>
    </table>
    <div class="row" style="text-align: start">
      <div class="text-right col-md-12">รวม {{ countAllBooks() }} เล่ม</div>
      <div class="text-right col-md-12">ราคาร่วม {{ sumprice() }} บาท</div>
      <div class="text-right col-md-12">ส่วนลด {{ discount() }} บาท</div>
      <div class="text-right col-md-12">
        ร่วมสุทธิ {{ sumprice() - discount() }} บาท
      </div>
    </div>
  </div>
</template>
<script>
import { defineComponent } from "vue";

export default defineComponent({
  setup() {
    const data = [
      {
        id: "1",
        price: 100,
        name: "BOOK1",
        count: 2,
      },
      {
        id: "2",
        price: 100,
        name: "book2",
        count: 3,
      },
      {
        id: "3",
        price: 100,
        name: "BOOK3",
        count: 2,
      },
    ];

    function sumprice() {
      let price = 0;
      let count = 0;
      data.forEach((element) => {
        price += element.price * element.count;
      });
      return price;
    }

    function countAllBooks() {
      let books = 0;
      data.forEach((e) => (books += e.count));
      return books;
    }

    function minDuplicateBooks() {
      let min = Number.MAX_SAFE_INTEGER;
      data.forEach((e) => {
        if (e.count < min) min = e.count;
      });
      return min;
    }

    function discount() {
      let discount = 0;
      const uniqueSubjectCount = data.length;
      const discountPercent = (uniqueSubjectCount - 1) * 10;
      discount = discountPercent * uniqueSubjectCount;
      const min = minDuplicateBooks();
      return discount * min;
    }
    return { sumprice, countAllBooks, discount };
  },
});
</script>
<style scoped></style>
