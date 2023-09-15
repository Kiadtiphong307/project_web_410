<script setup>
import { ref } from "vue";

const travelList = ref([
  {
    Name: "Patom Organic Living",
    price: 300,
    count_tb: 0,
    date: "",
    customer: "",
    Tel: "",
    time: "",
    img: "https://cms.dmpcdn.com/food/2021/01/14/419314c0-562c-11eb-b22e-fd8b6bde0acf_original.jpg",
  },
  {
    Name: "Hookrajong Cafe",
    price: 245,
    count_tb: 0,
    date: "",
    customer: "",
    Tel: "",
    time: "",
    img: "https://cms.dmpcdn.com/food/2021/01/14/40f463c0-562c-11eb-8350-b3a0991ba51b_original.jpg",
  },
  {
    Name: "Portobello & Désiré Cafe",
    price: 235,
    count_tb: 0,
    date: "",
    customer: "",
    Tel: "",
    time: "",
    img: "https://cms.dmpcdn.com/food/2022/01/09/34c2df70-710e-11ec-9ca0-bd1143265365_original.jpg",
  },
  {
    Name: "Wood Cafe",
    price: 600,
    count_tb: 0,
    date: "",
    customer: "",
    Tel: "",
    time: "",
    img: "https://cms.dmpcdn.com/food/2022/01/09/35f45a90-710e-11ec-9ca0-bd1143265365_original.jpg",
  },
]);
  

const booking = ref([]);

function table_controll(Name, count_tb, date, customer, Tel, time) {
  if (count_tb > 0 && date !== "" && customer !== "" && Tel !== "" && time !== "")  {
    const box = {
      Name: Name,
      count_tb: count_tb,
      price: count_tb * travelList.value.find((box) => box.Name === Name).price,
      date: date,
      customer: customer,
      Tel: Tel,
      time: time,
    };
    booking.value.push(box);
  }
}

function cancle(index) {
  booking.value.splice(index, 1);
}

function reloadPage() {
            location.reload();
        }
</script>

<template>

  <div class="card_body">
    <nav class="navbar bg-body-tertiary">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">
      <img src="https://th.bing.com/th/id/OIP.KDwcobfbRmFzJ83lCy3PvQHaH-?pid=ImgDet&rs=1" alt="Logo" width="30" height="24" class="d-inline-block align-text-top">
      ร้านกาแฟ คาเฟ่ในสวน
    </a>
  </div>
</nav>
    <div class="ColShop">
      <div class="col" v-for="(i, index) in travelList" :key="index">
        <div class="card" style="width: 18rem">
          <img :src="i.img" class="card-img-top" />
          <div class="card-body">
            <h5 class="card-title">{{ i.Name }}</h5>
            <p>ราคา : {{ i.price }}</p>
            
           
            <div class="date_row">
              วันที่
              <input type="date" class="boxDate" v-model="i.date" required />
            </div>
            <div class="time_row">
             เวลา
              <input type="time" class="form-control" v-model="i.time" required />
            </div>
            ผู้จอง
            <input
              type="text"
              class="form-control"
              placeholder="ชื่อ-สกุล"
              v-model="i.customer"
              required
            />
            <div>
              <label class="form-label"> เบอร์</label>
              <div class="input-group">
                <input
                  type="text"
                  class="form-control"
                  v-model="i.Tel"
                  required
                  maxlength="10"
                />
              </div>
              <div class="form-text">โปรดใส่เบอร์ที่ติดต่อได้จริง</div>
            </div>
            <div>
              <P>จำนวน</P>
              <input
                type="number"
                class="boxCount"
                v-model="i.count_tb"
                required
              />
            </div><br>
            <a
              class="btn btn-primary"
              @click="
                table_controll(i.Name, i.count_tb, i.date, i.customer, i.Tel, i.time)">จอง</a>
          </div>
        </div>
      </div>
    </div>



  <div class="table_total"  v-if="booking.length > 0">
    <table class="table" v-if="booking.length > 0">
      <thead>
        <tr>
          <th scope="col" class="">ลำดับ</th>
          <th scope="col">ร้าน</th>
          <th scope="col">จำนวน</th>
          <th scope="col">ราคา</th>
          <th scope="col">วันที่</th>
          <th scope="col">เวลา</th>
          <th scope="col">ผู้จอง</th>
          <th scope="col">เบอร์</th>
          <th scope="col"></th>
        </tr>
      </thead>
      <tbody class="table_total">
        <tr v-for="(i, index) in booking" :key="index">
          <th scope="row" class="total_text">{{ index + 1 }}</th>
          <td class="total_text">{{ i.Name }}</td>
          <td>{{ i.count_tb }}</td>
          <td>{{ i.price }}</td>
          <td>{{ i.time }}</td>
          <td>{{ i.date }}</td>
          <td>{{ i.customer }}</td>
          <td>{{ i.Tel }}</td>
          <td><button type="button" class="cancle_bt" @click="cancle(index)">ยกเลิก</button></td>
        </tr>
      </tbody>
    </table>
    <br><button class="button" @click="reloadPage()">ยืนยันการจอง</button>
  </div>
</div>
  
</template>

<style>

.button{
  color: #000000;
  padding: 8px 22px;
  border-radius: 6px;
  background: #4dc61d;
  transition: all 0.2s ease;
  padding: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  
}
.button:active{
  transform: scale(0.96);
}


.ColShop {
  display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    justify-items: stretch;
    align-items: stretch;
    column-gap: 40px;
    row-gap: 40px;
    
    padding: 30px;
    
}



/* ปรับขนาดและสไตล์ */
.card {
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 10px;
  text-align: center;
}

.card-img-top {
  max-width: 100%;
  height:250px;
  transition: all 0.2 ease;
}
.card-img-top:active{
  transform: scale(0.96);
}
.boxCount {
    background-color: aliceblue;
    color: black;
    border-radius: 5px;
    box-shadow: 0px 0px 0px 1px rgba(0, 0, 0, 0.87);
    margin-bottom: 10px;
  }
  /* Style the table */
.table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}

/* Style the total_text class */
.total_text {
  font-weight: bold;
}



/* Style the cancel button */
.cancle_bt {
  background-color: #ff0000;
  color: #fff;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
  transition: all 0.2 ease;
}
.cancle_bt:active{
  transform: scale(0.96);
}

/* Add hover effect to the cancel button */
.cancle_bt:hover {
  background-color: #ff1f00;
}

.card_body{
  padding: 5px;
  margin: 0;
}

.title{
  text-align: center;
  padding-bottom: 10px;
}

.c-item{
  height: 480px;
}

.c-item{
  height: 100%;
  object-fit: cover;
}
</style>