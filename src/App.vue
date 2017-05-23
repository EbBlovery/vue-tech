<template>
	<div id="container">
	    <div class="header">
	    	<i @click="toA" class="header-btn"></i>
            <span>热门消息</span>
	    </div>
	    <router-view></router-view>
		<div class="toggle">
		    <button>跳转到B页面</button>
			<router-link to="/b">跳转到A页面</router-link>	
		</div>
		<router-view></router-view>
		<div v-for="item in list">
		  <div class="list" v-for="i in item">
		         <div v-html="i.title">
		         	 
		         </div>
		         <img v-bind:src="i.images">     	  
		  </div>
		</div>
	</div>
</template>

<style>
#container{width:400px;height:500px;position:relative;margin:0px auto;overflow:scroll;}
.header{width:100%;height:100px;background:blue;position:absolute;top:0px;left:0px;}
.header-btn{width:20px;height:20px;background-color:red;position:absolute;top:40px;left:20px;}
.header span{position:absolute;top:40px;left:50px;color:#fff;font-size:15px;font-weight:bold;}
.toggle{
	width:100%;background:red;
}
#container .list{width:280px;height:120px;border:1px solid #999;margin:10px auto;}
#container .list img{width:100px;height:100px;margin:10px;}

</style>


<script>
import axios from 'axios';
export default {
	name:"app",
	data(){
		return {			
			list:[]
		}
	},
	mounted(){
		axios("http://localhost:9999/api/4/news/latest").then((res)=>{
			this.list=res.data
		})
	},
	methods:{
		toA(){
			this.$router.push("/a")
		}
	}
}
</script>
