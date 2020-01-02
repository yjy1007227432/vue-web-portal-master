<template>
	<div id="content" class="content">
		<div class="contentA container">
			<carousel></carousel>
		</div>
		<div class="contentB container">
			<div class="left fl">
				<div class="title">
					<div class="title_name">
						<h3>产品介绍</h3>
					</div>
					<div class="more">
						<a href="/index/catetory/product">MORE+</a>
					</div>
				</div>
				<div class="main">
					<!-- <div class="focusBox2">
						<ul class="pic">
							<li v-for="index in 6">
								<a href="">
									<img :src="tzgg[index+1] && tzgg[index+1].pic" />
								</a>
							</li>
						</ul>
						<div class="txt-bg"></div>
						<ul class="num">
							<li v-for="index in 6">
								<a></a>
								<span></span>
							</li>
						</ul>
					</div> -->
					<!-- <div class="news">
						<div class="sec_title">
							<h4>{{tzgg[0] && tzgg[0].title}}</h4>
						</div>
						<div class="news_text">
							<p>{{tzgg[0] && tzgg[0].abstractContent}}
								<span class="xiangqing fr">【
									<a href="/index/catetory/aaa/article/bbb">详情</a>】</span>
							</p>
						</div>
					</div> -->
					<div class="news_list">
						<ul>
							<li v-for="(item,index) in productlist" v-if="index >= 0 && index <= 5">
								<i class="el-icon-share"></i>
								<a :href="`/index/catetory/product/article/${item.id}`">{{item.name}}</a>
								<!-- <span>[{{item.publicTime | normalTime}}]</span> -->
							</li>
						</ul>
					</div>
				</div>
			</div>
			<div class="right fr">
				<div class="title">
					<div class="title_name">
						<h3>需求提交</h3>
					</div>
				</div>
				<div class="login-info">
					<div class="doc">
						<a class="docbtn fl" @click="dialogFormVisible = true">
							<div class="A"></div>
							<h4>新增需求</h4>
						</a>
						<a class="docbtn fr" href="#">
							<div class="B"></div>
							<h4>故障申报</h4>
						</a>
					</div>
					<!-- <div class="login-form container">
						<form action="login" name="loginForm" id="loginForm" role="form">
							<label for="userName">用户账户</label>
							<div class="inputuser">
								<input t ype="text" id="userName" name="account" placeholder="请输入手机号"></br>
							</div>
							<label for="userPassword">输入密码</label>
							<div class="inputpwd">
								<input type="password" id="userPassword" name="password" placeholder="请输入密码">
							</div>
							<div class="remember">
								<div class="rememberme fl">
									<input class="fl" id="rememberMe" type="checkbox" value="true" name="rememberMe">
									<label class="fl" for="rememberMe">下次自动登录</label>
								</div>
								<div class="forget fr">
									<a href="#">忘记密码</a>
								</div>
							</div>
							<div class="buttons fl">
								<button class="login fl" type="submit"><span class="loginfor7">登 录</span><span class="arrow fr"><img src="/static/img/login_icon.png"></span></button>
								<button class="prologin">专家登录<span class="arrow fr"><img src="/static/img/login_icon.png"></span></button>
							</div>
							<div class="regist fr">
								<span>没有账号？<a href="">点击注册</a></span>
							</div>
						</form>
					</div> -->
				</div>
			</div>
		</div>

		<el-dialog title="新增需求" :visible.sync="dialogFormVisible" width="30%" center>
			<el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
				<el-form-item label="客户名称" :label-width="formLabelWidth" prop="name">
					<!-- <el-input v-model="form.name" autocomplete="off"></el-input> -->
					<el-autocomplete v-model="ruleForm.name" :fetch-suggestions="querySearch" placeholder="请输入客户名称" @select="handleSelect"></el-autocomplete>
				</el-form-item>
				<el-form-item label="联系人" :label-width="formLabelWidth" prop="contact">
					<el-input v-model="ruleForm.contact" auto-complete="off" placeholder="请输入联系人姓名"></el-input>
				</el-form-item>
				<el-form-item label="联系电话" :label-width="formLabelWidth" prop="contactPhone">
					<el-input v-model="ruleForm.contactPhone" auto-complete="off" placeholder="请输入联系电话"></el-input>
				</el-form-item>
				<el-form-item label="联系邮箱" :label-width="formLabelWidth" prop="contactMail">
					<el-input v-model="ruleForm.contactMail" auto-complete="off" placeholder="请输入联系邮箱"></el-input>
				</el-form-item>
				<el-form-item label="需求说明" :label-width="formLabelWidth" prop="content">
					<el-input type="textarea" v-model="ruleForm.content" placeholder="请输入具体需求说明"></el-input>
				</el-form-item>
			</el-form>
			<div slot="footer" class="dialog-footer">
				<el-button type="primary" @click="submitForm('ruleForm')">确 定</el-button>
				<el-button @click="resetForm('ruleForm')">重 置</el-button>
				<el-button @click="dialogFormVisible = false">取 消</el-button>
			</div>
		</el-dialog>
		<div class="contentC container">
			<div class="left fl">
				<div class="title">
					<div class="title_name">
						<h3>最新动态</h3>
					</div>
					<div class="more">
						<a href="/index/catetory/news">MORE+</a>
					</div>
				</div>
				<div class="main">
					<!-- <div class="pic fl">
						<a href="">
							<img src="/static/img/pic.png">
						</a>

					</div> -->
					<div class="txt fr">
						<p>
							随着杭州打造“数字经济第一城”的工作逐步展开，伴随“最多跑一次”、“城市大脑”等各类业务系统的不断扩建与大数据开发应用的不断深入，需要现有的基础资源具有扩容及能力升级，包括对现有平台资源容量的扩容、大数据工具及产品的升级和网络的扩容升级等。
						</p>
						<p>
							基础资源能力：目前政务云已经达到13000核，30T内存的规模，储存超过1500T
						</p>
							<p>
							数据分析能力：平台进一步提供PAAS层的能力，已经提供ODPS、ADS、DRDS、EDAS、MQ、DATAMALL等服务，为城市数据大脑提供大数据分析能力。
						</p>
							<p>
							数据服务能力：通过电信自有数据的运营，以及电信体系公司的开发能力，政务大数据提供数据服务能力。
						</p>
					</div>
					<div class="news_list">
						<ul>
							<li v-for="(item,index) in newslist" v-if="index >= 0 && index <= 5">&gt;
								<a :href="`/index/catetory/news/article/${item.id}`">{{item.title}}</a>
								<span>[{{item.createTime}}]</span>
							</li>
						</ul>
					</div>
				</div>
			</div>
			<div class="right fr">
				<div class="title">
					<div class="title_name">
						<h3>解决方案</h3>
					</div>
					<div class="more">
						<a href="/index/catetory/solution">MORE+</a>
					</div>
				</div>
				<div class="main">
					<div class="news_list2">
						<ul>
							<li v-for="(item,index) in solutionlist" v-if="index >= 0 && index <= 7">&gt;
								<a :href="`/index/catetory/solution/article/${item.id}`">{{item.name}}</a>
								<span>[{{item.createTime}}]</span>
							</li>
						</ul>
					</div>
				</div>
			</div>
		</div>
		<!-- <div class="contentD container">
			<div class="title">
				<div class="title_name">
					<h3>成果展示</h3>
				</div>
				<div class="more"><a href="">MORE+</a></div>
			</div>
			<div class="main">
				
			</div>
		</div> -->
		<!-- <div class="contentE container">
			<div class="title">
				<div class="title_name">
					<h3>校企合作</h3>
				</div>
				<div class="more"><a href="">MORE+</a></div>
			</div>
			<div class="main">
				<div class="cop cop1">
					<img src="/static/img/cop.png" />
					<span class="pic_tit"><a href="">首都经济贸易大学</a></span>
				</div>
				<div class="cop cop2">
					<img src="/static/img/cop.png" />
					<span class="pic_tit"><a href="">首都经济贸易大学</a></span>
				</div>
				<div class="cop cop3">
					<img src="/static/img/cop.png" />
					<span class="pic_tit"><a href="">首都经济贸易大学</a></span>
				</div>
				<div class="cop cop4">
					<img src="/static/img/cop.png" />
					<span class="pic_tit"><a href="">首都经济贸易大学</a></span>
				</div>
				<div class="cop cop5">
					<img src="/static/img/cop.png" />
					<span class="pic_tit"><a href="">首都经济贸易大学</a></span>
				</div>
			</div>
		</div> -->
	</div>
</template>
<script>
	import Carousel from './Carousel.vue'
	import 'whatwg-fetch'
	import {
		url
	} from '../config'
	var qs = require('qs');

	export default {
		data: function () {
			var checkPhone = (rule, value, callback) => {
				const phoneReg = /^1[3|4|5|6|7|8][0-9]{9}$/
				if (!value) {
					return callback(new Error('电话号码不能为空'))
				}
				setTimeout(() => {

					if (!Number.isInteger(+value)) {
						callback(new Error('请输入数字值'))
					} else {
						if (phoneReg.test(value)) {
							callback()
						} else {
							callback(new Error('电话号码格式不正确'))
						}
					}
				}, 100)
			};
			return {
				tzgg: [],
				customerlist: [],
				productlist:[],
				newslist:[],
				solutionlist:[],
				restaurants:[],
				dialogFormVisible: false,
				ruleForm: {
					name: '',
					contact: '',
					contactPhone: '',
					contactMail: '',
					content: '',
					customerId:'',
					feedback:''
				},
				rules: {
					name: [{
						required: true,
						message: '请输入客户名称',
						trigger: 'change'
					}],
					contact: [{
						required: true,
						message: '请输入联系人姓名',
						trigger: 'blur'
					}],
					contactPhone: [{
						validator: checkPhone,
						required: true,
						trigger: 'blur'
					}],
					contactMail: [{
						type: 'email',
						required: true,
						message: '请输入正确的邮箱',
						trigger: 'blur'
					}],
					content: [{
						required: true,
						message: '请填写具体需求',
						trigger: 'blur'
					}]
				},
				formLabelWidth: '120px'
			}
		},
		methods: {
			// getTZGG: function () {
				
			// 	var _this = this;
			// 	this.$http.get('/src/data/catetory.data').then(function (res) {
			// 		_this.tzgg = res.data;
			// 	}).catch(function (err) {
			// 		console.log('获取通知公告数据出错');
			// 	})
			// },
			getproduct() {
				let that = this;
				fetch('http://' + url + '/product/list')
					.then(function (response) {
						return response.json()
					}).then(function (json) {
						that.productlist = json
						console.log("productlist", that.productlist);
					}).catch(function (ex) {
						console.log('parsing failed', ex)
					})
			},
			getnews() {
				let that = this;
				fetch('http://' + url + '/news/list')
					.then(function (response) {
						return response.json()
					}).then(function (json) {
						that.newslist = json
						console.log("newslist", that.newslist);
					}).catch(function (ex) {
						console.log('parsing failed', ex)
					})
			},
			getsolution() {
				let that = this;
				fetch('http://' + url + '/solution/list')
					.then(function (response) {
						return response.json()
					}).then(function (json) {
						that.solutionlist = json
						console.log("solutionlist", that.solutionlist);
					}).catch(function (ex) {
						console.log('parsing failed', ex)
					})
			},
			submitForm(formName) {
                let self = this;
				console.log(this.ruleForm);
				console.log(`http://`+url+`/order/add?${qs.stringify(this.ruleForm)}`);
                fetch(`http://`+url+`/order/add?${qs.stringify(this.ruleForm)}`)
                    .then(function (response) {
                        return response.json()
                    }).then(function (json) {
                        console.log('parsed json', json)
                        if (json.success == false) {
                            alert("需求重复")
                        } else if (json.success == true) {
                            self.pushQuestions(json.data)
                        }

                    }).catch(function (ex) {
                        console.log('parsing failed', ex)
                    });
				this.$refs[formName].validate((valid) => {
					if (valid) {
						alert('submit!');
						this.dialogFormVisible = false;
					} else {
						console.log('error submit!!');
						return false;
					}
				});
			},
			resetForm(formName) {
				this.$refs[formName].resetFields();
			},
			querySearch(queryString, cb) {
				this.restaurants=this.customerlist;
				this.restaurants.forEach(item => {
                    item.value = item.name
                });
				console.log("restaurants", this.restaurants);
				var restaurants = this.restaurants;
				var results = queryString ? restaurants.filter(this.createFilter(queryString)) : restaurants;
				// 调用 callback 返回建议列表的数据
				cb(results);
			},
			createFilter(queryString) {
				return (restaurant) => {
					return (restaurant.value.toLowerCase().indexOf(queryString.toLowerCase()) === 0);
				};
			},
			loadAll() {
				let that = this;
				fetch('http://' + url + '/customer/selectIdAndName')
					.then(function (response) {
						return response.json()
					}).then(function (json) {
						//console.log('json', json.question)
						// return
						//if (json.code == 200) {
						/*let arrlist = [],
						    questionList = json.question,
						    answer = json.answer;
						for (let i = 0; i < question.length; i++) {
						    let id = question[i].id,
						        dARR = [];
						    for (let j = 0; j < answer.length; j++) {
						        if (id == answer[j].questionID) {
						            dARR.push(answer[j])
						        }
						    }
						    question[i].answerList = dARR;
						}*/
						that.customerlist = json
						console.log("customerlist", that.customerlist);
						//} else {
						//   alert("failure")
						//}
					}).catch(function (ex) {
						console.log('parsing failed', ex)
					})
				// console.log("eee", this.customerlist);
				// return this.customerlist;
				// return [{
				// 		"value": "南京数龙计算机科技有限公司",
				// 		"id": "1"
				// 	},
				// 	{
				// 		"value": "杭州市林业水利局",
				// 		"id": "2"
				// 	},
				// 	{
				// 		"value": "浙江省电信有限公司",
				// 		"id": "3"
				// 	},
				// 	{
				// 		"value": "市总工会",
				// 		"id": "4"
				// 	},
				// ];
			},
			handleSelect(item) {
				console.log(item);
				this.ruleForm.customerId=item.id;
			}
		},
		// created: function () {
		// 	this.getTZGG();
		// },
		components: {
			carousel: Carousel
		},
		mounted() {
			this.loadAll();
			this.getproduct();
			this.getnews();
			this.getsolution();
		},
		// mounted: function () {
		// 	//增加jquery的操作,只有在updated之后，也才能使用jquery对样式绑定事件
		// 	$(".cop").hover(function () {
		// 		$(this).find("span").stop().animate({
		// 			bottom: "0"
		// 		}, 150)
		// 	}, function () {
		// 		$(this).find("span").stop().animate({
		// 			bottom: "-40px"
		// 		}, 150)
		// 	});
		// 	$(".focusBox2").slide({
		// 		titCell: ".num li",
		// 		mainCell: ".pic",
		// 		effect: "fold",
		// 		autoPlay: true,
		// 		trigger: "click",
		// 		interTime: 4000,
		// 	});
		// }
	};
</script>
<style scoped>
	.el-autocomplete {
		width: 100%
	}

	.contentA {
		width: 1200px;
		height: 320px;
		border: 1px solid #999;
		margin-top: 17px;
	}

	.focusBox {
		position: relative;
		width: 1180px;
		height: 310px;
		padding-top: 5px;
		z-index: 1;
	}

	.focusBox .pic {
		position: relative;
		z-index: 0;
	}

	.focusBox .pic img {
		width: 1180px;
		height: 310px;
		display: block;
	}

	.focusBox .hd {
		background: url(/static/img/slider_bg.png) no-repeat;
		margin: 0 auto;
		position: absolute;
		left: 550px;
		bottom: 0;
		text-align: center;
		font-size: 0;
		z-index: 1;
		height: 30px;
		width: 120px;
		*+bottom: 0;
	}

	.focusBox .hd li {
		margin: 7px 5px;
		background: url(/static/img/white.png) no-repeat;
		width: 15px;
		height: 15px;
		cursor: pointer;
		display: inline-block;
		*display: inline;
		zoom: 1;
		_background: url(/static/img/white.png) no-repeat;
	}

	.focusBox .hd li.on {
		background: url(/static/img/black.png) no-repeat;
	}

	.focusBox .prev {
		width: 40px;
		height: 40px;
		background: url(/static/img/left.png) no-repeat 0 0;
		position: absolute;
		top: 45%;
		left: -10px;
		z-index: 10;
		cursor: pointer;
		text-indent: -9999px;
		filter: alpha(opacity=50);
		opacity: 0.5;
	}

	.focusBox .next {
		width: 40px;
		height: 40px;
		background: url(/static/img/right.png) no-repeat 0 0;
		position: absolute;
		top: 45%;
		right: -10px;
		z-index: 10;
		cursor: pointer;
		text-indent: -9999px;
		filter: alpha(opacity=50);
		opacity: 0.5;
	}

	.focusBox .prev:hover,
	.focusBox .next:hover {
		filter: alpha(opacity=80) !important;
		opacity: 0.8 !important;
	}

	.title {
		height: 36px;
		border-bottom: 3px solid #B40E02;
	}

	.title .title_name {
		float: left;
		width: 120px;
		height: 36px;
		background: url(/static/img/title_bg.png);
		color: #fff;
		line-height: 36px;
	}

	.title .title_name h3 {
		display: block;
		margin-left: 40px;
		font-size: 17px;
		font-family: 'Microsoft Yahei';
	}

	.title .more {
		float: right;
		width: 45px;
		height: 15px;
		margin-top: 16px;
		margin-right: 20px;
	}

	.title .more a {
		font-size: 12px;
		color: #999;
	}

	.contentB {
		width: 1200px;
		height: 200px;
		margin-top: 30px;
	}

	.contentB .left {
		width: 825px;
		height: 200px;
	}

	.contentB .left .main {
		height: 140px;
		margin-top: 20px;
	}

	.focusBox2 {
		float: left;
		position: relative;
		width: 370px;
		height: 180px;
		overflow: hidden;
		font: 12px/1.5 Verdana, Geneva, sans-serif;
		text-align: left;
		background: white;
	}

	.focusBox2 .pic img {
		width: 370px;
		height: 180px;
		display: block;
	}

	.focusBox2 .txt-bg {
		position: absolute;
		bottom: 0;
		z-index: 1;
		height: 20px;
		width: 100%;
		background: #000;
		filter: alpha(opacity=50);
		opacity: 0.5;
		overflow: hidden;
	}

	.focusBox2 .num {
		position: absolute;
		z-index: 3;
		bottom: 5px;
		right: 8px;
	}

	.focusBox2 .num li {
		background: url(/static/img/dot_hui.png) no-repeat;
		float: left;
		position: relative;
		width: 8px;
		height: 8px;
		overflow: hidden;
		text-align: center;
		margin-right: 5px;
		cursor: pointer;
	}

	.focusBox2 .num li a,
	.focusBox .num li span {
		position: absolute;
		z-index: 2;
		display: block;
		color: white;
		width: 100%;
		height: 100%;
		top: 0;
		left: 0;
		text-decoration: none;
	}

	.focusBox2 .num li span {
		z-index: 1;
		background: black;
		filter: alpha(opacity=50);
		opacity: 0.5;
	}

	.focusBox2 .num li.on,
	.focusBox .num a:hover {
		background: url(/static/img/dot_white.png) no-repeat;
	}

	.xiangqing {
		font-size: 15px;
		color: red;
		*margin-top: -30px;
		color: #950600;
	}

	.xiangqing a {
		color: #950600;
	}

	.contentB .left .news {
		float: right;
		width: 410px;
		height: 180px;
	}

	.sec_title {
		height: 27px;
		width: 300px;
		border-bottom: 1px solid #ddd;
		line-height: 27px;
	}

	.sec_title h4 {
		font-size: 16px;
		font-family: 'Microsoft Yahei';
	}

	.contentB .left .news_text p {
		text-indent: 2em;
		margin-top: 5px;
		line-height: 30px;
		font-size: 14px;
		font-family: '宋体';
	}

	.news_list {
		margin-top: 10px;
		float: left;
		width: 100%;
		height: 95px;
	}

	.news_list ul {
		font-size: 15px;
		border-top: 1px solid #ddd;
	}

	.news_list ul li {
		margin-right: 40px;
		height: 32px;
		line-height: 32px;
		float: left;
		width: 45%;
		border-bottom: 1px dotted #666;
	}

	.news_list ul li a {
		margin-left: 13px;
		font-family: "宋体";
	}

	.news_list ul li:hover a {
		color: #B80C00;
		text-decoration: none;
	}

	.news_list ul li span {
		float: right;
		*margin-top: -34px;
	}
	.news_list2 {
		margin-top: 10px;
		float: left;
		width: 100%;
		height: 95px;
	}

	.news_list2 ul {
		font-size: 15px;
		border-top: 1px solid #ddd;
	}

	.news_list2 ul li {
		margin-right: 10px;
		height: 32px;
		line-height: 32px;
		float: left;
		width: 110%;
		border-bottom: 1px dotted #666;
	}

	.news_list2 ul li a {
		margin-left: 13px;
		font-family: "宋体";
	}

	.news_list2 ul li:hover a {
		color: #B80C00;
		text-decoration: none;
	}

	.news_list2 ul li span {
		float: right;
		*margin-top: -34px;
	}

	.contentB .right {
		width: 346px;
		height: 200px;
	}

	.contentB .right .login-info {
		width: 345px;
		height: 130px;
		/* border: 1px solid #ccc; */
		border-radius: 8px;
		margin-top: 20px;
	}

	.login-form {
		width: 240px;
	}

	.login-form label {
		display: block;
		height: 30px;
		line-height: 30px;
	}

	.inputuser,
	.inputpwd {
		width: 240px;
		height: 34px;
		line-height: 34px;
		position: relative;
	}

	.inputuser {
		background: url(/static/img/login_user.png);
	}

	.inputpwd {
		background: url(/static/img/login-pwd.png);
	}

	#userName,
	#userPassword {
		position: absolute;
		left: 37px;
		top: 2px;
		width: 200px;
		height: 30px;
		border: none;
		height: 25px\9;
		top: 6px\9;
	}

	.remember {
		margin-top: 17px;
	}

	.rememberme {
		width: 140px;
	}

	#rememberMe {
		height: 28px;
	}

	.forget {
		height: 28px;
		line-height: 28px;
		margin-right: 27px;
	}

	.login-form a {
		color: #188FED;
	}

	.buttons button {
		margin-top: 20px;
		height: 35px;
		background-color: #FF8E01;
		border: 1px solid #CECECE;
		border-radius: 5px;
		color: #fff;
		*border: none;
	}

	.buttons button span {
		*display: inline;
		*margin-left: 10px;
	}

	.buttons button .loginfor7 {
		*margin-right: 17px;
	}

	.buttons button .arrow {
		width: 16px;
		height: 16px;
		margin-right: 10px;
		margin-top: 2px;
		*margin-top: -17px;
	}

	.buttons .login {
		width: 85px;
	}

	.buttons .prologin {
		width: 115px;
		margin-left: 35px;
	}

	.regist {
		width: 154px;
		heihgt: 18px;
		margin-top: 18px;
	}

	.contentC {
		width: 1200px;
		height: 340px;
		margin-top: 30px;
	}

	.contentC .left {
		width: 825px;
		height: 220px;
	}

	.contentC .left .main {
		margin-top: 20px;
	}

	.contentC .left .main .pic {
		width: 380px;
		height: 160px;
	}

	.contentC .left .main .pic img {
		width: 380px;
		height: 168px;
	}

	.doc {
		width: 270px;
		height: 80px;
		margin: 10px 0 0 20px;
	}

	.doc .docbtn {
		display: block;
		text-align: center;
		width: 120px;
		height: 80px;
		border: 1px solid #7C7D7F;
		border-radius: 5px;
	}

	.doc .docbtn:hover {
		text-decoration: none;
	}

	.doc .docbtn div {
		display: inline-block;
		width: 46px;
		height: 46px;
		margin: 5px 0;
	}

	.doc .docbtn .A {
		background: url(/static/img/icon_shenbao_hui.png)
	}

	.doc .docbtn:hover .A {
		background: url(/static/img/icon_shenbao_red.png)
	}

	.doc .docbtn .B {
		background: url(/static/img/icon_zhicheng_hui.png)
	}

	.doc .docbtn:hover .B {
		background: url(/static/img/icon_zhicheng_red.png)
	}



	.contentC .left .main .txt {
		width: 815px;
		height: 210px;
	}

	.contentC .left .main .txt p {
		text-indent: 2em;
		line-height: 30px;
		font-size: 14px;
		font-family: '宋体';
	}

	.contentC .right {
		width: 345px;
		height: 220px;
	}

	.contentC .right .videoparent {
		margin-top: 20px;
	}

	.contentD {
		width: 1200px;
		height: 260px;
		margin-top: 20px;
	}

	.contentD .main {
		width: 1200px;
	}

	.ladyScroll {
		width: 1150px;
		height: 200;
		position: relative;
		margin-top: 20px;
	}

	.ladyScroll .prev {
		width: 23px;
		height: 40px;
		position: absolute;
		top: 75px;
		left: -23px;
		z-index: 100;
		cursor: pointer;
		background: url(/static/img/2340left.png) no-repeat;
	}

	.ladyScroll .next {
		width: 26px;
		height: 46px;
		position: absolute;
		top: 75px;
		right: -26px;
		z-index: 100;
		cursor: pointer;
		background: url(/static/img/2646right.png) no-repeat;
	}

	.ladyScroll .prev:hover {
		filter: alpha(opacity=90) !important;
		opacity: 0.9 !important;
	}

	.ladyScroll .next:hover {
		filter: alpha(opacity=90) !important;
		opacity: 0.9 !important;
	}

	.ladyScroll .scrollWrap {
		width: 1150px;
		overflow: hidden;
		position: absolute;
	}

	.ladyScroll dl {
		float: left;
		width: 260px;
		position: relative;
		margin-right: 34px;
		border: 1px solid #666;
		border-radius: 10px;
		overflow: hidden;
	}

	.ladyScroll span {
		display: block;
		width: 260px;
		height: 45px;
		position: absolute;
		bottom: -45px;
		background: #000;
		filter: alpha(opacity=70);
		opacity: 0.70;
		border-radius: 8px;
		/* transition:bottom 0.2s ease-in-out;-moz-transition:bottom 0.2s ease-in-out; Firefox 4-webkit-transition:bottom 0.2s ease-in-out; Safari and Chrome-o-transition:bottom 0.2s ease-in-out; Opera */
	}

	.ladyScroll dt {
		width: 260px;
		overflow: hidden;
	}

	.ladyScroll img {
		display: block;
		width: 260px;
		height: 200px;
	}

	.ladyScroll dd {
		display: block;
		width: 260px;
		height: 45px;
		line-height: 45px;
		font-size: 16px;
		color: #fff;
		overflow: hidden;
		position: absolute;
		bottom: -45px;
		text-align: center;
		/* transition:bottom 0.2s ease-in-out;-moz-transition:bottom 0.2s ease-in-out; Firefox 4-webkit-transition:bottom 0.2s ease-in-out; Safari and Chrome-o-transition:bottom 0.2s ease-in-out; Opera */
	}

	.ladyScroll dd a {
		color: #fff;
	}

	.ladyScroll dd .xiangqing {
		color: red;
	}

	.ladyScroll dd a:hover {
		text-decoration: none;
	}

	.contentE {
		width: 1200px;
		height: 217px;
		margin-top: 30px;
	}

	.contentE .main {
		margin-top: 20px;
		position: relative;
	}

	.contentE .cop {
		width: 233px;
		height: 155px;
		border: 1px solid #7C7D7F;
		border-radius: 9px;
		position: relative;
		overflow: hidden;
	}

	.contentE .cop img {
		width: 233px;
		height: 155px;
	}

	.contentE .cop1 {
		position: absolute;
		left: 0
	}

	.contentE .cop2 {
		position: absolute;
		left: 241px;
	}

	.contentE .cop3 {
		position: absolute;
		left: 482px;
	}

	.contentE .cop4 {
		position: absolute;
		left: 723px;
	}

	.contentE .cop5 {
		position: absolute;
		right: 0
	}

	.pic_tit {
		width: 233px;
		height: 40px;
		text-align: center;
		line-height: 30px;
		position: absolute;
		bottom: -40px;
		left: 0px;
		background: rgba(0, 0, 0, 0.7);
		filter: progid:DXImageTransform.Microsoft.gradient(startcolorstr=#4C000000, endcolorstr=#4C000000);
	}

	.pic_tit a {
		display: block;
		width: inherit;
		height: inherit;
		font-size: 14px;
		font-weight: 600;
		color: #ffffff;
	}
</style>