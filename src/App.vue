<template>
    <div id="app">
        <van-nav-bar
            :title="$route.meta.title"
            v-show="$route.meta.isShowNav"
            @click-left="onClickLeft"
            :left-arrow="$route.meta.isShowBack"
            fixed
            placeholder
            style="height: 46px"
        /> 
        <router-view></router-view>
        <Tabbar v-if="isShowTabbar"></Tabbar> 
    </div>
</template>

<script setup>
import Tabbar from './components/TabBar.vue'
import { useRoute } from 'vue-router'
import { ref, watch, onMounted } from 'vue'
import { getUser } from './api'
import useUser from './stores/user'
import { useRouter } from 'vue-router'

const route = useRoute()
const isShowTabbar = ref(true)
const router = useRouter() 
const { user, updateUser } = useUser() 

onMounted(() => { 
 if (user.isLogin) { 
 loadUser() 
 } 
}) 

const loadUser = async () => { 
 const data = await getUser() 
 updateUser({ 
 isLogin: true, 
 username: data.username, 
 avatar: data.avatar 
 }) 
} 

const onClickLeft = () => { 
    if (history.length > 1) { 
        router.back() 
    } else { 
        router.push({ name: 'home' }) 
    } 
} 

// 监听路由的isTab是否为true，若为true，则展示底部
watch(
    () => route.meta,
    val => {
        isShowTabbar.value = val.isTab
    }
)
</script>

<style>
#app {
    color: #2c3e50;
    line-height: 24px;
    --van-nav-bar-background: #0022ff; 
    --van-nav-bar-title-text-color: #fff; 
    --van-nav-bar-icon-color: #fff; 
}
</style>
