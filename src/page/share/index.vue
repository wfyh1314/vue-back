<template>
  	<div class="shareContainer" ref="shareContainer">
		<el-row :gutter="20">
			<el-col :span="6" v-for="(item,index) in list" :key="index">
			  <heng-share @shareToQQ="shareToQQ" @shareToQQzone="shareToQQzone" @shareToWeibo="shareToWeibo" @shareToDouban="shareToDouban"></heng-share>
			</el-col>
		</el-row>
		<el-row :gutter="20">
			<el-col :span="6" v-for="(item,index) in list" :key="index">
		       <heng-share @shareToQQ="shareToQQ" @shareToQQzone="shareToQQzone" @shareToWeibo="shareToWeibo" @shareToDouban="shareToDouban"></heng-share>
			</el-col>
		</el-row>
		<wx-code-modal v-if="wxModal.show" :wxModal="wxModal" @hideWxCodeModal="hideWxCodeModal"></wx-code-modal>
  	</div>
</template>

<script>
	import {
		HengShare,
		WxCodeModal
	} from "./components";
    import * as mutils from '@/utils/mUtils'

	export default {
	  data(){
			return {
				list: [1,2,3,4],
				wxModal:{
					show:false,
					width:"358px",
					height:"358px",
				}
			}
		},
		components:{
			HengShare,
			WxCodeModal
		},
		mounted(){
			mutils.setContentHeight(this,this.$refs.shareContainer,210);
		},
		methods: {
			hideWxCodeModal(){
				this.wxModal.show = false;
			},
			// 分享到微信，显示微信二维码弹框；
			shareToWeixin(){
				this.wxModal.show = true;
			},
			shareToQQ(){
				this.shareConfig('qq')
			},
			shareToQQzone(){
				this.shareConfig('qqZone')
			},
			shareToWeibo(){
				this.shareConfig('weibo')
			},
			shareToDouban(){
				this.shareConfig('douban')
			}
		}
	}
</script>

<style lang="less" scoped>
	.shareContainer{
		display: flex;
		flex-direction: column;
		justify-content: space-around;
		padding: 20px;
		.el-row:first-child{
			margin-bottom: 20px;
		}
		.el-row{
			height:210px;
			.el-col{
				height:100%;
				.shareArea{
					height: 100%;
					width:100%;
				}
			}
		}
	}
</style>
