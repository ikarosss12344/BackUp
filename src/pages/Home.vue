<template>
    <div class="home">
        <van-search
            shape="round"
            v-model="value"
            placeholder="请输入搜索关键词"
            @search="onSearch"
            @cancel="onCancel"
        />
        <!-- 轮播图 -->
        <home-swiper></home-swiper>

        <!-- 功能按钮区 -->
        <home-grid></home-grid> 

        <!-- 商品信息展示区 -->
        <home-product></home-product> 

        <!-- 每周上新 -->
        <home-new></home-new>

        <!-- 人气推荐 -->
        <home-top></home-top> 
    </div>
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'
import HomeSwiper from '../components/HomeSwiper.vue'
import HomeGrid from '../components/HomeGrid.vue'
import HomeProduct from '../components/HomeProduct.vue'
import HomeNew from '../components/HomeNew.vue'
import HomeTop from '../components/HomeTop.vue' 

const value = ref('')
const onSearch = val => showToast(val)
const onCancel = () => showToast('取消')
</script>