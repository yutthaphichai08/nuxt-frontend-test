<template>
    <div class="container my-4">
        <!-- ขนาด -->
        <div class="mb-3">
            <h5>ขนาด</h5>
            <div class="d-flex justify-content-between">
                <button type="button" class="btn btn-outline-primary w-100 mx-1"
                    :class="{ active: selectedSize === 'แนวตั้ง' }" @click="selectedSize = 'แนวตั้ง'">
                    แนวตั้ง
                </button>
                <button type="button" class="btn btn-outline-primary w-100 mx-1"
                    :class="{ active: selectedSize === 'แนวนอน' }" @click="selectedSize = 'แนวนอน'">
                    แนวนอน
                </button>
                <button type="button" class="btn btn-outline-primary w-100 mx-1"
                    :class="{ active: selectedSize === 'จตุรัส' }" @click="selectedSize = 'จตุรัส'">
                    จตุรัส
                </button>
            </div>
        </div>


        <!-- โทนสี -->
        <div class="mb-3">
            <h5>โทนสี</h5>
            <div class="d-flex flex-wrap">
                <div v-for="(color, index) in colors" :key="index" class="p-2">
                    <input type="radio" class="btn-check" :id="'color-' + index" name="colors" :value="color"
                        v-model="selectedColor" />
                    <label class="btn" :class="{
                        'btn-primary': selectedColor === color,
                        'btn-outline-secondary': selectedColor !== color,
                    }" :style="{ backgroundColor: color, borderRadius: '50%' }" :for="'color-' + index"></label>
                </div>
            </div>
        </div>

        <!-- สไตล์ภาพ -->

    <div class="mb-3">
      <h5>สไตล์ภาพ</h5>
      <div class="row g-2">
        <div
          v-for="(style, index) in styles"
          :key="index"
          class="col-6 col-md-3"
        >
          <button
            class="btn btn-outline-secondary w-100 text-center"
            @click="selectedStyle = style.label"
            :class="{
              'btn-primary text-white': selectedStyle === style.label,
            }"
          >
            <img :src="style.image" alt="" class="img-fluid mb-2" />
            <span>{{ style.label }}</span>
          </button>
        </div>
      </div>
    </div>

    </div>
</template>

<script setup>
import { ref } from "vue";

// State สำหรับขนาด
const selectedSize = ref("แนวนอน");

// โทนสี (สีต่าง ๆ)
const colors = ref([
    "#00ff00",
    "#ff00ff",
    "#0000ff",
    "#000000",
    "#ffffff",
    "#cccccc",
    "#f00",
    "#0ff",
    "#ff0",
]);
const selectedColor = ref("#00ff00");

// สไตล์ภาพ
const styles = ref([
    { label: "Vintage", image: "https://img.freepik.com/premium-vector/vector-young-man-anime-style-character-vector-illustration-design-manga-anime-boy_147933-12445.jpg" },
    { label: "Modern", image: "/path/to/modern.jpg" },
    { label: "Romantic", image: "/path/to/romantic.jpg" },
    { label: "Medieval", image: "/path/to/medieval.jpg" },
    { label: "Renaissance", image: "/path/to/renaissance.jpg" },
    { label: "Greek", image: "/path/to/greek.jpg" },
    { label: "3D", image: "/path/to/3d.jpg" },
    { label: "Anime", image: "/path/to/anime.jpg" },
    { label: "Pixel Art", image: "/path/to/pixel-art.jpg" },
    { label: "Fantasy", image: "/path/to/fantasy.jpg" },
    { label: "Sci-Fi", image: "/path/to/sci-fi.jpg" },
    { label: "Street", image: "/path/to/street.jpg" },
]);
const selectedStyle = ref("");
</script>

<style scoped>
.btn {
    width: 40px;
    height: 40px;
    padding: 0;
}
</style>
