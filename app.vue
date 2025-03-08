<script setup>
import { ref } from 'vue'

const products = ref([]) // Ürünleri saklayacak dizi
const currentIndex = ref(1) // baslangic urunu 1 ve kontrol eder

const fetchProduct = async () => { //kontrol et
    if (currentIndex.value > 20) return // Eğer 20'den büyükse dur

    const { data } = await useFetch(`https://fakestoreapi.com/products/${currentIndex.value}`)

    if (data.value) {
        products.value.push(data.value) // Yeni ürünü ekle
        currentIndex.value++ // Bir sonraki ürüne geç
    }
}
</script>

<template>
    <div>
        <div class="shopping-page-container">
                <button @click="fetchProduct" class="add-product-button">Ürün Ekle</button>
            <ul class="items-lists">
                <li v-for="product in products" :key="product.id" class="item-card">
                    <div class="image-section">
                        <img :src="product.image" alt="Ürün Resmi" class="product-image" />
                    </div>
                    <p class="item-title">{{ product.title }}</p>
                    <p class="item-price">{{ product.price }} TL</p>
                </li>
            </ul>
        </div>


    </div>
</template>
<style>
    .shopping-page-container {
        width: 100vw;
        height: 100vh;
        .add-product-button {
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 50px auto;
            font-family: Avenir, Helvetica, Arial, sans-serif;
            font-weight: 700;
            font-size: 20px;
            padding: 10px 20px;
            background-color: darkgoldenrod;
            border: 1px solid black;
            border-radius: 10px;


        }
        .items-lists {
            width: 100%;
            height: 100%;
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            row-gap: 3rem;
            .item-card {
                width: 300px;
                height: 500px;
                max-height: 500px;
                padding: 20px 30px;
                display: flex;

                flex-direction: column;
                border-radius: 16px;
                border: 1px solid black;
                position: relative;
                .image-section {
                    width: 300px;
                    height: 350px;
                    display: flex;
                    justify-content: center;
                    align-content: center;
                    .product-image {
                        max-width: 300px;
                        max-height: 350px;
                        width: auto;
                        height: 100%;
                    }
                }
                .item-title {
                    width: 100%;

                    background-color: red;
                    font-family: "SF Pro Display", sans-serif;
                    font-size: 22px;
                    font-weight: 500;
                    text-align: start;
                }
                .item-price {
                    position: absolute;
                    bottom: 10px;
                    align-items: center;
                    background-color: orange;
                    font-family: "Helvetica Neue", sans-serif;
                    font-size: 24px;
                    font-weight: bold;
                }
            }
        }
    }
</style>