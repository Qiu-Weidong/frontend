<template>
    <div class="sidebar">
        <el-menu class="sidebar-el-menu" :default-active="onRoutes" :collapse="collapse" background-color="#FFFFFF"
            text-color="#000000" active-text-color="#195FFF" unique-opened router>
            <template v-for="item in items">
                <template v-if="item.subs">
                    <el-submenu :index="item.index" :key="item.index">
                        <template #title>
                            <i :class="item.icon"></i>
                            <span>{{ item.title }}</span>
                        </template>
                        <template v-for="subItem in item.subs">
                            <el-submenu v-if="subItem.subs" :index="subItem.index" :key="subItem.index">
                                <template #title>{{ subItem.title }}</template>
                                <el-menu-item v-for="(threeItem, i) in subItem.subs" :key="i" :index="threeItem.index">
                                    {{ threeItem.title }}</el-menu-item>
                            </el-submenu>
                            <el-menu-item v-else :index="subItem.index" :key="subItem.index">{{ subItem.title }}
                            </el-menu-item>
                        </template>
                    </el-submenu>
                </template>
                <template v-else>
                    <el-menu-item :index="item.index" :key="item.index">
                        <i :class="item.icon"></i>
                        <template #title>{{ item.title }}</template>
                    </el-menu-item>
                </template>
            </template>
        </el-menu>
    </div>
</template>

<script>
import { computed, watch } from "vue";
import { useStore } from "vuex";
import { useRoute } from "vue-router";
export default {
    setup() {
        const items = [
            {
                icon: "el-icon-lx-home",
                index: "0",
                title: "现场空间定位",
                subs: [
                    { index: '3', title: '数据源选择',  subs: [
                        { index: '/cctv', title: 'CCTV' },
                        { index: '/videolist', title: '视频' }
                    ]},
                    { index: '/coordinate', title: '空间坐标变化' },
                    { index: '/coordinateoriginsetting', title: '坐标原点设置' }
                ]
            },
            {
                icon: "el-icon-lx-cascades",
                index: "1",
                title: "前期模型训练",
                subs: [
                    { index: '/datacollection', title: '数据采集'},
                    { index: '/xmlcollection', title: '标注工作'},
                    { index: '/newmodel', title: '训练模型选择' },
                    { index: '/ad', title: '模型介绍' }
                ]
            },


        ];

        const route = useRoute();

        const onRoutes = computed(() => {
            return route.path;
        });

        const store = useStore();
        const collapse = computed(() => store.state.collapse);

        return {
            items,
            onRoutes,
            collapse,
        };
    },
};
</script>

<style scoped>
.sidebar {
    display: block;
    position: absolute;
    left: 0;
    top: 70px;
    bottom: 0;
    overflow-y: scroll;
    /* background-color: #195FFF; */
}
.sidebar::-webkit-scrollbar {
    width: 0;
}
.sidebar-el-menu:not(.el-menu--collapse) {
    /* width: 250px; */
    width: 300px;
}
.sidebar > ul {
    height: 100%;
}
</style>
