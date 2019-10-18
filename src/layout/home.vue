<template>
    <div class="home rflex">
        <head-nav></head-nav>
        <div class="menu_box wflex el-scrollbar" ref="menu_box" >
            <left-menu></left-menu>
            <div class="menu_content" ref="menu_content" :style="{marginLeft:sidebar.width+'px'}">
                <top-menu></top-menu>
                <router-view></router-view><!--页面渲染入口-->
            </div>
            <!-- <footerNav></footerNav> -->
            <backTop :ele="$refs.menu_box"></backTop>
        </div>
    </div>
</template>
<script>
    import { mapState, mapGetters } from 'vuex'
    import HeadNav from './headNav.vue';
	import LeftMenu from './leftMenu.vue';
    import Bread from './bread.vue';
    import topMenu from "./topMenu";
	// import FooterNav from './footerNav.vue';
	import backTop from 'cps/backTop';

    export default {
        name: 'home',
        data(){
            return {
            }
        },
        computed:{
            ...mapGetters(['sidebar']),
        },
        components:{
            HeadNav,
            LeftMenu,
            Bread,
            // FooterNav,
            backTop,
            topMenu
        },
        created() {
        },
        mounted (){
        },
        watch:{
          
        }
    }
</script>
<style scoped lang='less'>
    .home{
        .menu_box{
            width: 100%;
            margin-top: 60px;
            background:#F6F7FC;
            .menu_content{
                background:#f0f2f5;
                overflow: auto;
            }
        }
    }
</style>
