<template>
  <!-- Container หลัก -->
  <div class="container my-5">

    <!-- หัวข้อ -->
    <h2 class="text-center mb-4">แสดงข้อมูลสินค้า</h2>

     <div class="text-center mb-3">
      <!-- @click = event เมื่อกดปุ่ม -->
      <button class="btn btn-primary" @click="fetchProducts">
        🔄 อัปเดต
      </button>
    </div>

    <!-- ตารางสินค้า -->
    
      <table class="table table-bordered table-striped text-center">

        <!-- ส่วนหัวตาราง -->
        <thead class="table-dark">
          <tr>
            <th>รหัสสินค้า</th>
            <th>รูปภาพ</th>
            <th>ชื่อสินค้า</th>
            <th>จำนวน</th>
            <th>ราคา</th>
          </tr>
        </thead>

        <!-- ส่วนข้อมูลสินค้า -->
        <tbody>

          <!-- วนลูปแสดงสินค้า -->
          <tr v-for="product in products" :key="product.id"  >
            <!-- รหัสสินค้า -->
            <td class="text-center">
              {{ product.id }}
            </td>

            <!-- รูปสินค้า -->
            <td class="text-center">
              <img
                :src="product.thumbnail"
                alt="Product Image"
                width="100"
                height="80"
                style="object-fit: contain"
              />
            </td>

            <!-- ชื่อสินค้า -->
            <td class="text-success text-start">
              {{ product.title }}
            </td>
             <!-- จำนวน -->
             <td>
              {{ product.stock }}
            </td>
            <!-- ราคา -->
            <td class="text-danger">
              ${{ product.price }}
            </td>


          </tr>

        </tbody>
      </table>
    

  </div>
</template>

<script>
import { ref, onMounted } from "vue";

export default {
  setup() {
    // สร้างตัวแปร products เพื่อเก็บข้อมูลสินค้า
    const products = ref([]);

    // ฟังก์ชันดึงข้อมูลสินค้าจาก Fake Store API
    const fetchProducts = async () => {
      try {
        const response = await fetch("https://dummyjson.com/products");
        const data = await response.json();
        products.value = data.products;
 
      
      } catch (error) {
        console.error("Error fetching products:", error);
      }
    };

    // เรียก fetchProducts เมื่อคอมโพเนนต์ถูกโหลด
    onMounted(fetchProducts);

    return {
      products, // ส่งออกตัวแปร products เพื่อใช้ใน Template
    };
  },
};
</script>