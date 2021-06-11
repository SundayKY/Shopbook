<template>
  <div class="about">
    <div class="container" id="form-group">
      <div class="Store">
        <div class="container-sidestore">
          <div class="row">
            <br />
            <div
              class="text-top"
              style="color: white; background-color: darkblue"
            >
              <h2>ร้านหนังสือ “บ้านนายดิน”</h2>
            </div>

            <br />
            <div class="row" style="margin-bottom: 20px; margin-top: 20px">
              <h1 class="col-md-9" style="text-align: left">Store</h1>
              <div class="col-md-3">
                <img
                  src="cart.png"
                  class="img-thumbnail"
                  style="max-width: 15%"
                />
              </div>
            </div>

            <br />
            <bookstore
              id="1"
              src="h1.jpg"
              price="100"
              name="แฮรี่พอตเตอร์กับ ศิลาอาถรรพ์"
              @buy="buyitem"
            ></bookstore>

            <bookstore
              id="2"
              src="h2.png"
              price="100"
              name="แฮรี่พอตเตอร์กับ ห้องแห่งความลับ"
              @buy="buyitem"
            ></bookstore>
            <bookstore
              id="3"
              src="p3.png"
              price="100"
              name="แฮร์รี่พอตเตอร์กับ นักโทษแห่งอัซคาบัน"
              @buy="buyitem"
            ></bookstore>
            <bookstore
              id="4"
              src="p4.jpg"
              price="100"
              name="แฮรี่พอตเตอร์กับ ถ้วยอัคนี"
              @buy="buyitem"
            ></bookstore>
            <bookstore
              id="5"
              src="p5.jpg"
              price="100"
              name="แฮรี่พอตเตอร์กับ ภาคีนักฟินิกช์"
              @buy="buyitem"
            ></bookstore>
            <bookstore
              id="6"
              src="p6.jpg"
              price="100"
              name="แฮรี่พอตเตอร์กับ เจ้าชายเลือดผสม"
              @buy="buyitem"
            ></bookstore>
            <bookstore
              id="7"
              src="p7.jpg"
              price="100"
              name="แฮรี่พอตเตอร์กับ เครื่องรางยมภูติ"
              @buy="buyitem"
            ></bookstore>
            <div class="container allprice" style="margin-top: 10%">
              <div class="row table">
                <h1
                  class="col-md-6"
                  style="text-align: initial; background: beige"
                >
                  ตระกร้าสินค้า
                </h1>
                <h1 class="col-md-6" style="mar">ราคาสินค้า</h1>
                <table class="table col-md-6" style="max-width: 40%">
                  <thead>
                    <tr>
                      <th scope="col">Number</th>
                      <th scope="col">Name</th>
                      <th scope="col">Price</th>
                      <th scope="col">Count</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="(item, index) in data" :key="index">
                      <td>{{ item.id }}</td>
                      <td>{{ item.name }}</td>
                      <td>{{ item.price }}</td>
                      <td>{{ item.count }}</td>
                    </tr>
                  </tbody>
                </table>
                <div class="col-md-6" style="text-align: end">
                  <div class="text-right col-md-12">
                    รวม {{ countAllBooks() }} เล่ม
                  </div>
                  <div class="text-right col-md-12">
                    ราคาร่วม {{ sumprice() }} บาท
                  </div>
                  <div class="text-right col-md-12">
                    ส่วนลด {{ discount() }} บาท
                  </div>
                  <div class="text-right col-md-12">
                    ร่วมสุทธิ {{ sumprice() - discount() }} บาท
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { defineComponent, reactive } from "vue";
import bookstore from "./bookstore.vue";
export default defineComponent({
  components: { bookstore },
  setup() {
    const data = reactive([]);
    //  นับitemที่ซื้อและขาย
    function buyitem(item) {
      data.push(item);
      console.log(data[0]);
      console.log(item);
    }
    //  รวมราคา
    function sumprice() {
      let price = 0;
      let count = 0;
      data.forEach((element) => {
        price += element.price * element.count;
        console.log(element);
      });
      return price;
    }
    // นับจำนวนหนังสือ
    function countAllBooks() {
      let books = 0;
      data.forEach((e) => (books += Number.parseInt(e.count)));
      return books;
    }
    // หาจำนวนที่น้อยที่สุด
    function minDuplicateBooks() {
      let min = Number.MAX_SAFE_INTEGER;
      data.forEach((e) => {
        if (e.count < min) min = e.count;
      });
      return min;
    }
    //  จำนวนส่วนลด
    function discount() {
      let discount = 0;
      const uniqueSubjectCount = data.length;
      const discountPercent = (uniqueSubjectCount - 1) * 10;
      discount = discountPercent * uniqueSubjectCount;
      const min = minDuplicateBooks();
      return discount * min;
    }

    return {
      buyitem,
      sumprice,
      countAllBooks,
      minDuplicateBooks,
      discount,
      data,
    };
  },
});
</script>

<style scoped></style>
