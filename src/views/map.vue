<template>
	<div>
		<h1>我是地图</h1>
		<p>{{ad_info.city}}</p>
		<p>{{ad_info2[index].day_weather}}</p>
	</div>
</template>

<script>
	import jsonp from 'jsonp'
	export default {
		data(){
			return {
				ad_info:{},
				ad_info2:{},
				index:0
			}
		},
		methods:{
			getLocation(){
				let url = 'https://apis.map.qq.com/ws/location/v1/ip?key=CAABZ-AVSAQ-RDR5L-GTBDJ-HLA4O-A5FDB&output=jsonp&_=1599183246631';
				let url2 = 'https://wis.qq.com/weather/common?weather_type=observe|forecast_24h|air&source=pc&province=%E6%B2%B3%E5%8D%97%E7%9C%81&city=%E9%83%91%E5%B7%9E%E5%B8%82'
				jsonp(url,{},(err,data)=>{
					console.log(data);
					this.ad_info = data.result.ad_info;
				}),
				jsonp(url2,{},(err,data)=>{
					console.log(data);
					this.ad_info2 = data.data.forecast_24h;
				})
			}
		},
		created(){
			this.getLocation();
		}
	}
</script>

<style>
	
</style>
