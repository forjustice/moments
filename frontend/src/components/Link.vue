<script setup lang="ts" name="Link">
import { ref, onMounted } from 'vue'
import { useDefaultStore } from '@/store/default';
import { getLink } from '@/api/link'
import type { linkData } from '@/types/link';
import { Icon } from '@vicons/utils'
import { Times } from '@vicons/fa'

const isShowLink = ref(false)
const toggleShowLink = (): void => {
    isShowLink.value = !isShowLink.value
}
const defaultStore = useDefaultStore()
const links = ref<linkData[]>([])

// 跳转
function openUrl(url: string) {
    window.open(url, '_blank', 'noopener,noreferrer')
}
// 获取数据
onMounted(async () => {
    try {
        const res = await getLink();
        links.value = res.data;
    } catch (error) {
        console.error("加载链接数据失败:", error);
    }
})
defineExpose({ toggleShowLink })
</script>

<template>
    <transition name="slide">
        <div class="link-container" v-if="isShowLink">
            <div class="header">
                <span>友情链接</span>
                <Icon class="icon" @click="isShowLink = false">
                    <Times class="close" />
                </Icon>
            </div>
            <div class="link-header">
                <div class="link-header-top">
                    <img :src="defaultStore.configs.site_logo ? defaultStore.configs.site_logo : defaultStore.configs.site_avatar"
                        alt="站点LOGO">
                    {{ defaultStore.configs.sitename }}
                </div>
                <div class="link-header-bottom">
                    {{ defaultStore.configs.link_brief }}
                </div>
            </div>

            <div class="link-content">
                <ul>
                    <li v-for="link in links">
                        <div class="link-item" @click="openUrl(link.url)">
                            <img :src="link.logo ? link.logo : '/img/avatar.jpg'" alt="友联LOGO">
                            <div>{{ link.sitename }}</div>
                            <div>{{ link.brief ? link.brief : '暂时未设置站点介绍' }}</div>
                        </div>
                    </li>
                </ul>
            </div>
        </div>
    </transition>
</template>

<style scoped>
.link-container {
    display: flex;
    flex-direction: column;
    position: fixed;
    right: 10%;
    max-width: 520px;
    padding: 5px;
    box-shadow: 0 0 8px skyblue;
    border-radius: 5px;
}

.header {
    display: flex;
    justify-content: space-between;
}

.icon:hover {
    cursor: pointer;
    transform: scale(1.2);
}

/* 头部 */
.link-header {
    margin-top: 15px;
    display: flex;
    flex-direction: column;
}

.link-header-top {
    display: flex;
    justify-content: center;
    gap: 25px;
    align-items: center;
}

.link-header-bottom {
    display: flex;
    justify-content: center;
    padding: 5px;
    margin-top: 15px;
}

.link-header img {
    height: 50px;
    border-radius: 5px;
}

/* 内容区域 */
ul,
li {
    list-style: none;
    margin: 0px;
    padding: 5px 0px;
}

.link-item {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    padding: 5px;
    gap: 50px;
}

.link-item:hover {
    background-color: #f3f3f3;
    border-radius: 10px;
    cursor: pointer;
}

li img {
    width: 35px;
    height: 35px;
    border-radius: 50%;
    object-fit: cover;
}

/* 动画 */
.slide-enter-active,
.slide-leave-active {
    transition: transform 0.5s cubic-bezier(0.19, 1, 0.22, 1), opacity 0.4s ease-out;
}

.slide-enter-from {
    /* X 和 Y 同时向负方向移动 100%，确保从左上方移入 */
    transform: translate(-100%, -100%); 
    opacity: 0;
}

.slide-enter-to {
    /* 保持在原位 */
    transform: translate(0, 0); 
    opacity: 1;
}

.slide-leave-from {
    transform: translate(0, 0); 
    opacity: 1;
}

.slide-leave-to {
    transform: translate(0, -100%); 
    opacity: 0;
}
</style>