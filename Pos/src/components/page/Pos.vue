<template>
	<div class="pos">
		<el-row>
			<el-col :span='7' class="pos-order" id="order-list">
				<el-tabs>
					<el-tab-pane label="点餐">
						<el-table :data="tableData" border style="width:100%">
							<el-table-column prop="goodsName" label="商品名称"></el-table-column>
							<el-table-column prop="count" label="数量"></el-table-column>
							<el-table-column prop="price" label="金额"></el-table-column>
							<el-table-column label="操作" fixed="right">
								<template scope='scope'>
									<el-button type="text" size="small" @click="delSingleGoods(scope.row)">删除</el-button>
									<el-button type="text" size="small" @click="addOrderList(scope.row)">增加</el-button>
								</template>
							</el-table-column>
						</el-table>
						<div class="totalDiv">
							数量:  {{totalCount}} &nbsp;&nbsp;&nbsp;金额:  {{totalMoney}}
						</div>
						<div class="div-btn">
							<el-button type="warning">挂单</el-button>
							<el-button type="danger" @click="delAllGoods()">删除</el-button>
							<el-button type="success" @click="checkout()">结账</el-button>
						</div>
					</el-tab-pane>
					<el-tab-pane label="挂单">
						
					</el-tab-pane>
					<el-tab-pane label="外卖">
						
					</el-tab-pane>
				</el-tabs>
			</el-col>
			<el-col :span="17">
				<div class="often-goods">
					<div class="title">常用商品</div>
					<div class="often-goods-list">
						<ul>
							<li v-for="(item) in oftenGoods" @click="addOrderList(item)">
								<span>{{item.goodsName}}</span>
								<span class="o-price">${{item.price}}元</span>
							</li>
						</ul>
					</div>
				</div>
				
				<div class="goods-type">
					<el-tabs>
						<el-tab-pane label="汉堡">
							<div>
								<ul class="cookList">
									<li v-for="(item) in type0Goods" @click="addOrderList(item)">
										<span class="foodImg"><img :src="item.goodsImg"></span>
										<span class="foodName">{{item.goodsName}}</span>
										<span class="foodPrice">￥{{item.price}}元</span>
									</li>
								</ul>
							</div>
						</el-tab-pane>
						<el-tab-pane label="小食">
							<div>
								<ul class="cookList">
									<li v-for="(item) in type0Goods" @click="addOrderList(item)">
										<span class="foodImg"><img :src="item.goodsImg"></span>
										<span class="foodName">{{item.goodsName}}</span>
										<span class="foodPrice">￥{{item.price}}元</span>
									</li>
								</ul>
							</div>
						</el-tab-pane>
						<el-tab-pane label="饮料">
							<div>
								<ul class="cookList">
									<li v-for="(item) in type0Goods" @click="addOrderList(item)">
										<span class="foodImg"><img :src="item.goodsImg"></span>
										<span class="foodName">{{item.goodsName}}</span>
										<span class="foodPrice">￥{{item.price}}元</span>
									</li>
								</ul>
							</div>
						</el-tab-pane>
						<el-tab-pane label="套餐">
							<div>
								<ul class="cookList">
									<li v-for="(item) in type0Goods" @click="addOrderList(item)">
										<span class="foodImg"><img :src="item.goodsImg"></span>
										<span class="foodName">{{item.goodsName}}</span>
										<span class="foodPrice">￥{{item.price}}元</span>
									</li>
								</ul>
							</div>
						</el-tab-pane>
					</el-tabs>
				</div>
				
			</el-col>
		</el-row>
	</div>
</template>

<script>
import axios from 'axios';
export default {
		name:'pos',
		data(){
			return{
				tableData:[],
				oftenGoods:[{
					goodsId:1,
					goodsName:'香辣鸡腿堡',
					price:18
				},
				{
					goodsId:2,
					goodsName:'田园鸡腿堡',
					price:15
				},
				{
					goodsId:3,
					goodsName:'和风汉堡',
					price:15
				},
				{
					goodsId:4,
					goodsName:'快乐全家桶',
					price:80
				},
				{
					goodsId:5,
					goodsName:'脆皮炸鸡腿',
					price:10
				},
				{
					goodsId:6,
					goodsName:'魔法鸡块',
					price:20
				},
				{
					goodsId:7,
					goodsName:'可乐大杯',
					price:10
				},
				{
					goodsId:8,
					goodsName:'雪顶咖啡',
					price:18
				},
				{
					goodsId:9,
					goodsName:'大块鸡米花',
					price:15
				},
				{
					goodsId:10,
					goodsName:'香脆鸡柳',
					price:17
				},],
				type0Goods:[
					{
					              goodsId:1,
					              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
					              goodsName:'香辣鸡腿堡',
					              price:18
					          }, {
					              goodsId:2,
					              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
					              goodsName:'田园鸡腿堡',
					              price:15
					          }, {
					              goodsId:3,
					              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
					              goodsName:'和风汉堡',
					              price:15
					          }, {
					              goodsId:4,
					               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
					              goodsName:'快乐全家桶',
					              price:80
					          }, {
					              goodsId:5,
					               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
					              goodsName:'脆皮炸鸡腿',
					              price:10
					          }, {
					              goodsId:6,
					               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
					              goodsName:'魔法鸡块',
					              price:20
					          }, {
					              goodsId:7,
					               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
					              goodsName:'可乐大杯',
					              price:10
					          }, {
					              goodsId:8,
					               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
					              goodsName:'雪顶咖啡',
					              price:18
					          }, {
					              goodsId:9,
					               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
					              goodsName:'大块鸡米花',
					              price:15
					          }, {
					              goodsId:20,
					               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
					              goodsName:'香脆鸡柳',
					              price:17
					          }

				],
				totalMoney:0,
				totalCount:0
			}
		},
		mounted:function(){
			var orderHeight=document.body.clientHeight;
			document.getElementById("order-list").style.height=orderHeight+'px';
		},
		methods:{
			addOrderList(item){
				this.totalMoney = 0;
				this.totalCount = 0;
				//商品是否已经存在与商品列表中
				let isHave = false;
				for(let i=0;i<this.tableData.length;i++){
					if(this.tableData[i].goodsId == item.goodsId){
						isHave = true;
					}
				}
				//根据判断的值编写业务逻辑
				if(isHave){
				let arr = this.tableData.filter(o=>o.goodsId == item.goodsId);
				arr[0].count++;
				}else{
					let newGoods={goodsId:item.goodsId,goodsName:item.goodsName,price:item.price,count:1}
					this.tableData.push(newGoods);
				}
				//计算汇总金额和数量
				this.tableData.forEach((element)=>{
					this.totalCount += element.count;
					this.totalMoney = this.totalMoney+(element.price*element.count);
				})
			},
			//删除单个商品
			delSingleGoods(item){
				this.tableData=this.tableData.filter(o=>o.goodsId !=item.goodsId);
				this.getAllMoney();
			},
			delAllGoods(){
				this.totalCount = 0;
				this.totalMoney = 0;
				this.tableData = [];
			},
			//模拟结账
			checkout(){
				if(this.totalCount != 0){
					this.totalCount = 0;
					this.totalMoney = 0;
					this.tableData = [];
					this.$message({
						message:'结账成功',
						type:'success'
					});
				}else{
						this.$message.error('傻逼!!');
					}
				
			},
			//计算汇总金额和数量
			getAllMoney(){
				this.totalCount = 0;
				this.totalMoney = 0;
				this.tableData.forEach((element)=>{
					this.totalCount += element.count;
					this.totalMoney = this.totalMoney+(element.price*element.count);
				})
			}
		}
	}
</script>

<style scoped>
	.pos-order{
		background-color: #f9fafc;
		border-right:1px solid #c0ccda;
	}
	.div-btn{
		margin-top:10px;
	}
	.title{
		height:20px;
		border-bottom:1px solid #d3dce6;
		background-color: #f9fafc;
		padding:10px;
		text-align: left;
	}
	.often-goods-list ul li{
		list-style: none;
		float:left;
		border:1px solid #e5e9f2;
		padding:10px;
		margin:10px;
		background-color: #fff;
		cursor: pointer;
	}
	.o-price{
		color:#58b7ff;
	}
	.goods-type{
		clear:both;
	}
	.cookList li{
	       list-style: none;
	       width:23%;
	       border:1px solid #E5E9F2;
	       height: auot;
	       overflow: hidden;
	       background-color:#fff;
	       padding: 2px;
	       float:left;
	       margin: 2px;
		   cursor: pointer;
	   }
	   .cookList li span{
	
	        display: block;
	        float:left;
	   }
	   .foodImg{
	       width: 40%;
	   }
	   .foodName{
	       font-size: 18px;
	       padding-left: 10px;
	       color:brown;
	
	   }
	   .foodPrice{
	       font-size: 16px;
	       padding-left: 10px;
	       padding-top:10px;
	   }
	   .totalDiv{
			background-color: #fff;
			padding:10px;
			border-bottom:1px solid #d3dce6;
	   }
</style>
