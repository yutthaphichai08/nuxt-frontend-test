<template>
    <div class="container my-4">
        <!-- ขนาด -->
        <div class="mb-3">
            <h5 class="fw-bold">ขนาด</h5>
            <div class="d-flex justify-content-between">
                <button type="button" class="btn w-100 mx-1 size-btn" :class="{ active: selectedSize === 'แนวตั้ง' }"
                    @click="selectedSize = 'แนวตั้ง'">
                    แนวตั้ง
                </button>
                <button type="button" class="btn w-100 mx-1 size-btn" :class="{ active: selectedSize === 'แนวนอน' }"
                    @click="selectedSize = 'แนวนอน'">
                    แนวนอน
                </button>
                <button type="button" class="btn w-100 mx-1 size-btn" :class="{ active: selectedSize === 'จตุรัส' }"
                    @click="selectedSize = 'จตุรัส'">
                    จตุรัส
                </button>
            </div>
        </div>

        <!-- โทนสี -->
        <div class="mb-3 mt-4">
            <h5 class="fw-bold">โทนสี</h5>
            <div class="d-flex flex-wrap">
                <div v-for="(color, index) in colors" :key="index" class="p-2 position-relative">
                    <input type="checkbox" class="btn-check" :id="'color-' + index" name="colors" :value="color"
                        v-model="selectedColors" />
                    <label class="color-btn btn position-relative"
                        :class="{ 'selected-color': selectedColors.includes(color) }"
                        :style="{ backgroundColor: color, borderRadius: '50%' }" :for="'color-' + index">
                        <i v-if="selectedColors.includes(color)"
                            class="bi bi-check-circle-fill position-absolute text-primary"></i>
                        <div v-if="color === '#ffffff'" class="border-highlight position-absolute rounded-circle"
                            style="border: 2px solid black; top: 0; left: 0; width: 100%; height: 100%;"></div>
                    </label>
                </div>
            </div>
        </div>

        <!-- สไตล์ภาพ -->
        <div class="mb-3 mt-4">
            <h5 class="fw-bold">สไตล์ภาพ</h5>
            <div class="row g-2">
                <div v-for="(style, index) in visibleStyles" :key="index" class="col-4 col-md-3">
                    <button class="btn w-100 text-center p-0 overflow-hidden position-relative"
                        @click="selectedStyle = style.label"
                        :class="{ 'btn-primary text-white': selectedStyle === style.label }">
                        <div class="image-wrapper position-relative">
                            <img :src="style.image" alt="" class="img-fluid" />
                            <div class="label-overlay position-absolute start-50 translate-middle-x px-3 py-1 text-dark"
                                :style="{ backgroundColor: selectedStyle === style.label ? 'rgba(0, 123, 255, 0.7)' : 'rgba(255, 255, 255, 0.5)' }">
                                {{ style.label }}
                            </div>
                            <i v-if="selectedStyle === style.label"
                                class="bi bi-check-circle-fill position-absolute start-50 translate-middle text-primary"></i>
                        </div>
                    </button>
                </div>
            </div>
        </div>

        <!-- ปุ่มโหลดเพิ่มเติม -->
        <div class="text-center mt-3">
            <button v-if="visibleStyles.length < styles.length" class="btn load-more-btn" @click="loadMore">
                โหลดเพิ่มเติม
            </button>
        </div>
    </div>
</template>


<script setup>
import { ref } from "vue";

// State สำหรับขนาด
const selectedSize = ref("แนวนอน");

// โทนสี (สีต่าง ๆ)
const colors = ref({
    green: "#00ff00",
    magenta: "#ff00ff",
    blue: "#0000ff",
    black: "#000000",
    white: "#ffffff",
    gray: "#cccccc",
    red: "#f00",
    cyan: "#0ff",
    yellow: "#ff0",
    brown: "#a52a2a",
    purple: "#800080",
    orange: "#ffa500",
    pink: "#ffc0cb",
    lightblue: "#add8e6",
    lightgreen: "#90ee90",
    darkgray: "#a9a9a9",
});

const selectedColors = ref([]);

const selectedStyle = ref("");

// จำนวนภาพเริ่มต้นและการโหลดเพิ่ม
const visibleCount = ref(12);
const visibleStyles = computed(() => styles.value.slice(0, visibleCount.value));

// ฟังก์ชันโหลดเพิ่มเติม
const loadMore = () => {
    visibleCount.value += 12; // เพิ่มจำนวนภาพที่แสดง
};
// สไตล์ภาพ
const styles = ref([
    {
        label: "Vintage",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },
    {
        label: "Modern",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },
    {
        label: "Romantic",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },
    {
        label: "Medieval",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },
    {
        label: "Renaissance",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },
    {
        label: "Greek",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },
    {
        label: "3D",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },
    {
        label: "Anime",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },
    {
        label: "Pixel Art",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },
    {
        label: "Fantasy",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },
    {
        label: "Sci-Fi",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },
    {
        label: "Street",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },

    {
        label: "Vintage2",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },
    {
        label: "Modern2",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },
    {
        label: "Romantic2",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },
    {
        label: "Medieval2",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },
    {
        label: "Renaissance2",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },
    {
        label: "Greek2",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },
    {
        label: "3D2",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },
    {
        label: "Anime2",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },
    {
        label: "Pixel Art2",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },
    {
        label: "Fantasy2",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },
    {
        label: "Sci-Fi2",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },
    {
        label: "Street2",
        image:
            "https://i.pinimg.com/736x/19/db/31/19db31732931019b73bedcf17924f814.jpg",
    },
]);

</script>

<style scoped>
/* ขนาด */
.size-btn {
    border-radius: 8px;
    border: 2px solid transparent;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    transition: all 0.3s ease;
}

.size-btn.active {
    border-color: #007bff;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    background-color: rgba(0, 123, 255, 0.1);
    color: #007bff;
}

.size-btn:hover {
    box-shadow: 0 3px 6px rgba(0, 0, 0, 0.15);
}

/* โทนสี */
.color-btn {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
    border: 2px solid transparent;
    transition: border-color 0.3s ease;
}

.color-btn.selected-color {
    border-color: #007bff;
}

.check-icon {
    font-size: 1.5rem;
    color: white;
    background-color: rgba(0, 0, 0, 0.5);
    border-radius: 50%;
    padding: 5px;
    width: 30px;
    height: 30px;
    display: flex;
    align-items: center;
    justify-content: center;
}

/* สไตล์ภาพ */
.image-wrapper {
    width: 100%;
    height: 120px;
    overflow: hidden;
    background-color: #f8f9fa;
    display: flex;
    align-items: center;
    justify-content: center;
}

.image-wrapper img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.label-overlay {
    bottom: 3px;
    left: 50%;
    font-size: 14px;
    pointer-events: none;
    width: 95%;
    text-align: center;
    border-radius: 8px;
    background-color: rgba(0, 123, 255, 0.7);
}

.load-more-btn {
    background: none;
    border: none;
    color: #007bff;
    font-size: 14px;
    padding: 0;
    cursor: pointer;
}

.load-more-btn:hover {
    text-decoration: none;
    color: #0056b3;
}

</style>
