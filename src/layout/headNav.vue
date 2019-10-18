<template>
    <header class="head-nav rflex " id='header_container'>
        <div class="menu_page_top rflex">
            <img class='logo closeLogo' :src="logo" alt="Fang后台管理系统" >
            <span class='title'>{{$t('commons.adminName')}}</span>
        </div>
        
        <div class="userinfo-right rflex">
            <div class="userinfo">
                <el-menu 
                    class="el-menu-demo" 
                    mode="horizontal" 
                    >
                    <el-submenu index="1" popper-class="langItem">
                        <template slot="title">
                            <img :src="langLogo" class='langAvatar' alt="">
                        </template>
                        <el-menu-item index="1-1" @click="changeLocale('zh')">
                            <img :src="chinaImg" class='langAvatar' alt="">
                            <span class="intro">中文</span>
                        </el-menu-item>
                        <el-menu-item index="1-2" @click="changeLocale('en')">
                            <img :src="americaImg" class='langAvatar' alt="">
                            <span class="intro">EngList</span>
                        </el-menu-item>
                    </el-submenu>

                    <el-submenu index="2"  popper-class="infoItem">
                        <template slot="title">
                            <div class='welcome'>
                                <span class="name">{{$t('commons.hi')}},</span>
                                <span class='name avatarname'> {{ $t(`commons.${name}`)}}</span>
                            </div>
                            <img :src="avatar" class='avatar' alt="">
                        </template>
                        <el-menu-item index="2-1" @click="setDialogInfo('info')">{{ $t('commons.infoShow') }}</el-menu-item>
                        <el-menu-item index="2-2" @click="setDialogInfo('pass')">{{ $t('commons.infoModify') }}</el-menu-item>
                        <el-menu-item index="2-3" @click="setDialogInfo('logout')">{{ $t('commons.quit') }}</el-menu-item>
                    </el-submenu>
                </el-menu>
            </div>
        </div>
    </header>
</template>

<script>
    import { mapGetters } from "vuex";
    import * as mUtils from '@/utils/mUtils'
    import { setToken,getToken } from '@/utils/auth'
    import store from "@/store";
    import logoImg from "@/assets/img/logo.png";
    import chinaImg from "@/assets/img/china.svg";
    import americaImg from "@/assets/img/america.svg";
    import { github } from "@/utils/env";


    export default {
          name: 'head-nav',
          data(){
            return{
                logo:logoImg,
                langLogo:getToken('langLogo') || americaImg,
                chinaImg:chinaImg,
                americaImg:americaImg,
                github:github,
                menu:{
                    userBgcolor:'#f0f2f5'
                }
            }
          },
          components:{
          },
          computed:{
            ...mapGetters(['name','avatar','sidebar']),
            headNavWidth(){
                return document.body.clientWidth - this.sidebar.width
            }  
          },
          created(){
            
          },
          mounted(){
          },
          methods:{
            logout(){
                this.$store.dispatch('LogOut').then(() => {
                    location.reload();
                })
            },
            /**
             * 弹出框-修改密码或者系统设置   
             * @param {string} cmditem 弹框类型
            */
            setDialogInfo(cmditem) {
                switch (cmditem) {
                    case 'info':
                        this.$router.push('/infoManage/infoShow/infoShow1');
                        break;
                    case 'pass':
                        this.$router.push('/infoManage/infoModify/infoModify1');
                        break;
                    case 'logout':
                        this.logout();
                        break;
                }
            },
            // 切换语言
            changeLocale(type){
                setToken('lang',type);
                this.$i18n.locale = type;
                if(type === 'en'){
                    this.langLogo = this.americaImg;
                }else{
                    this.langLogo = this.chinaImg;
                }
                setToken('langLogo',this.langLogo);
            }
        }
    }
</script>

<style scoped lang='less'>
    .head-nav {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        z-index: 29;
        transition: width .2s;
        justify-content: space-between;
        height: 60px;
        box-sizing: border-box;
        background: #333;
        color: #fff;
        .logout {
            vertical-align: middle;
            cursor: pointer;
        }
    }
    .menu_page_top{
        height: 60px;
        align-items: center;
        justify-content: space-around;
        text-transform: uppercase;
        box-sizing: border-box;
        padding: 0 10px;
        .logo {
            height: 36px;
            width: 36px;
            margin-right: 10px;
            vertical-align: middle;
            display: inline-block;
        }
        .closeLogo{
            width:30px;
            height:30px;
        }
        .title{
            font-size: 22px;
            i{
                color:#FF6C60;
            }
        }
    }
    .middle{
       align-items: center;
       border:1px solid;
    }
    .userinfo-right{
        width: 160px;
        padding: 0 10px;
        justify-content: space-between;
    }
    .el-menu-demo {
        background: #333;
    }
    .userinfo {
        line-height: 60px;
        text-align:right;
    }
    .avatar{
        width: 32px;
        height: 32px;
        border-radius: 50%;
        vertical-align: middle;
        display: inline-block;
    }
    .langAvatar{
        width: 24px;
        height: 24px;
        border-radius: 50%;
        vertical-align: middle;
        display: inline-block;
    }
    .welcome{
        display: inline-block;
        vertical-align: middle;
        padding: 0 5px;
        .name{
            line-height: 20px;
            text-align: center;
            font-size: 12px;
        }
        .avatarname{
            color:#a9d86e;
            font-weight:bolder;
            font-size: 13px;
        }
    }

    .username {
        cursor: pointer;
        margin-right: 5px;
    }
    .border{
        border:1px solid;
    }
    ul.top-menu > li {
        position: relative;
    }
</style>
