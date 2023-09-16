<script setup>
import { ref } from 'vue';
let booking = null;
const showBookingForm = ref(false);
const tableBooking = ref([]);
const showTable = ref(false);

const cafes = [
  {
    name: 'Good view',
    image: 'src/goodview.jpg',
    price: 120,
    size: { s: 120, m: 160, l: 220 }
  },
  {
    name: 'ตะวันแดง มหาชน',
    image: 'src/tawandang.webp',
    price: 90,
    size: { s: 50, m: 190, l: 280 }
  },
  {
    name: 'ท่าช้าง',
    image: 'src/thachang_3-1.jpg',
    price: 80,
    size: { s: 80, m: 150, l: 200 }
  },
  {
    name: 'Warmup cafe',
    image: 'src/warmup-cafe-5.jpg',
    price: 100,
    size: { s: 100, m: 180, l: 260 }
  }
];

function openBookingForm(cafe) {
  booking = { cafe, name: '', phone: '', date: '', time: '', size: '', tableCount: 0 };
  showBookingForm.value = true;
}

function reserveTable() {
  if (booking) {
    alert('บันทึกข้อมูลการจองเรียบร้อยแล้ว');
    console.log('ข้อมูลการจอง:', booking);
   
    tableBooking.value.push({ 
      cafe: booking.cafe.name,
      name: booking.name,
      phone: booking.phone,
      date: booking.date,
      size: booking.size,
      tableCount: booking.tableCount,
    });

    booking = null;
    showBookingForm.value = false;
    showTable.value = true;
  } else {
    alert('ไม่พบข้อมูลการจอง');
  }
}
</script>

<template>
  <div class="container-card">
    <div class="card" v-for="cafe in cafes" :key="cafe.name" style="width: 18rem;">
      <img :src="cafe.image" class="card-img-top" :alt="cafe.name">
      <div class="card-body">
        <h5 class="card-title">{{ cafe.name }}</h5>
        <p class="card-text">Price: {{ cafe.price }}</p>
        <p class="card-text">Size: S: {{ cafe.size.s }}, M: {{ cafe.size.m }}, L: {{ cafe.size.l }}</p>
        <a href="#" class="btn btn-primary" @click="openBookingForm(cafe)">จองโต๊ะ</a>
      </div>
    </div>

    <div v-if="showBookingForm" class="booking-form">
      <h2>ข้อมูลการจองโต๊ะ</h2>
      <p>ร้าน: {{ booking.cafe.name }}</p>
      <label for="name">ชื่อผู้จอง:</label>
      <input type="text" id="name" v-model="booking.name">
      <label for="phone">เบอร์โทร:</label>
      <input type="text" id="phone" v-model="booking.phone">
      <label for="date">วันที่:</label>
      <input type="date" id="date" v-model="booking.date">
      <label for="time">เวลา:</label>
      <input type="time" id="time" v-model="booking.time" >
      <label for="size">ขนาดโต๊ะ(S,M,L):</label>
      <input type="text" id="size" v-model="booking.size">
      <label for="tableCount">จำนวนโต๊ะ:</label>
      <input type="number" id="tableCount" v-model="booking.tableCount">
      <button @click="reserveTable">ยืนยันการจอง</button>
    </div>
    
    <div v-if="showTable" class="booking-list">
  <h2>รายการโต๊ะที่ถูกจอง</h2>
  <table class="table">
    <thead>
      <tr>
        <th scope="col">ร้าน</th>
        <th scope="col">ชื่อผู้จอง</th>
        <th scope="col">เบอร์โทร</th>
        <th scope="col">วันที่</th>
        <th scope="col">ขนาดโต๊ะ(S,M,L)</th>
        <th scope="col">จำนวนโต๊ะ</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(booking, index) in tableBooking" :key="index">
  <td>{{ booking.cafe }}</td>
  <td>{{ booking.name }}</td>
  <td>{{ booking.phone }}</td>
  <td>{{ booking.date }}</td>
  <td>{{ booking.size }}</td>
  <td>{{ booking.tableCount }}</td>
</tr>

    </tbody>
  </table>
</div>
  </div>
</template>


<style scoped>
.card{
  margin: 100px;
  margin-left: 150px;
  background-color: #f4f4f4; 
  border: 1px solid #ddd; 
  border-radius: 5px; 
  text-decoration-color: antiquewhite;
}
.container-card{
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: repeat(2, 1fr);
  gap: 20px; 
  place-self: center;
}

.booking-form {
  display: grid;
  grid-template-columns: repeat(1, 1fr);
  margin: 20px;
  background-color: #fff; 
  padding: 10px; 
  border: 1px solid #ccc; 
  border-radius: 5px; 
}
</style>
