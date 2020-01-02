<template>
	<div id="article" class="content3 container">
		<!-- <leftNav></leftNav> -->
		<div class="contentArt fr">
			<div class="catetorytitle">
				<h2 class="fl">{{topCatetory}}</h2>
				<div class="breadcrumb fr">
					<a href="/index">首页</a>&gt;<a :href="'/index/catetory/'+topCatetoryLink">{{topCatetory}}</a>
				</div>
			</div>
			<article>
				<div class="article_title container">
					<h4>{{article.name}}</h4>
				</div>
				<!-- <div style="text-align: center">
				<img :src="article.pic"></div> -->
				<span v-html="article.content"></span>
			</article>
		</div>
	</div>
</template>
<script>
	// import leftNav from './LeftNav.vue'
	import Carousel from './Carousel.vue'
	import 'whatwg-fetch'
	import {
		url
	} from '../config'
	export default{
		data : function(){
			return {
				article : [],
				allNavData : [],
				curCatetory : "",
				topCatetory : "",
				topCatetoryLink : "",
				secCatetory : []
			}
		},
		watch: {
    		// 如果路由有变化，会再次执行该方法
	    	'$route': 'updateLeftByUrl'
		},
		// components : {
		// 	'leftNav' : leftNav
		// },
		methods : {
			getArticle : function(){
				var _this = this;
				this.$http.get('http://' + url + '/' + _this.$route.params.catetoryId + '/find?id='+_this.$route.params.articleId).then(function(res){
					_this.article = res.data;
					if (_this.$route.params.catetoryId == 'news') {
						_this.article.name=_this.article.title
					}
					console.log("asd",_this.article)
				}).catch(function(err){
					console.log('请求文章出错');
				})
			},
			getLeftNav : function(){
				var _this = this;
				this.$http.get('/src/data/nav.data').then(function(res){
					_this.allNavData = res.data;
					_this.updateLeftByUrl();
				}).catch(function(err){
					console.log('请求左侧导航数据出错',err);
				})
			},
			updateLeftByUrl : function(){
				//首先清空有关左侧导航的数据
				this.curCatetory = "";
				this.topCatetory = "";
				this.topCatetoryLink = "";
				this.secCatetory = [];
				//根据导航中的参数来决定左侧导航中的内容
				this.curCatetory = this.$route.params.catetoryId;
				//由于知道最多二级导航，这里可以这么写,倘若有后台，可以传参直接请求对应数据
				for(var index in this.allNavData){
					//如果链接是一级栏目
					if(this.allNavData[index].link == this.curCatetory){
						this.topCatetory = this.allNavData[index].name;
						this.topCatetoryLink = this.allNavData[index].link;
					}
					//如果链接是二级栏目
					if(this.allNavData[index].havesub){
						for(var index2 in this.allNavData[index].sub){
							if(this.allNavData[index].sub[index2].subLink == this.curCatetory){
								this.secCatetory = this.allNavData[index].sub;
								this.topCatetory = this.allNavData[index].name;
								this.topCatetoryLink = this.allNavData[index].link;
							}
						}
					}
				}
				
			}
		},
		mounted : function(){
			this.getArticle();
			this.getLeftNav();
			console.log("aaaa",this.$route);
		}
	}
</script>
<style scoped>
	/* 三级页面 */
	/* .picture{text-align: center} */
	.content3{width:1200px;min-height:650px;margin-top: 38px;overflow: auto}
	.content3::-webkit-scrollbar{display: none;}
	.contentArt{width:1190px;margin-top:10px; margin-right: 10px;}
	.article_title{height:70px;line-height:70px;font-size: 18px;text-align: center;border-bottom:1px dotted #999;margin-bottom: 15px;}
	.article_title h4{font-size: 20px;}
	article span{text-indent: 2em;}
	article span p{line-height: 25px;letter-spacing: 2px;}
</style>