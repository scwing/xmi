<template>
	<div>
		<h1>爱笑话</h1>
		<div class="item" v-for="item in joks">
			{{item.summary}}
		</div>
		<button :disabled="!can" @click="getJoks()">加载更多</button>
	</div>
</template>
<script>
	export default {
		data() {
			return {
				joks: [],
				page: 1,
				can:true
			}
		},
		created() {
			this.getJoks();
			var str = localStorage.getItem('joks') || "[]";
			this.joks  = JSON.parse(str)
		},
		methods: {
			getJoks() {
				this.can = false;
				fetch("https://520mg.com/mi/list.php?page=" + this.page)
					.then(res => res.json())
					.then(res => {
						this.can = true;
						this.joks = this.joks.concat(res.result);
						this.page++;
						var str = JSON.stringify(this.joks);
						localStorage.setItem('joks',str)
					})
					.catch(err => {
						console.log(err)
					})
			}
		}
	}
</script>
<style>
	.item{
		padding: 15px;
		border-bottom: 1px solid #eee;
		text-align: justify;
	}
	button{
		margin-top: 10px;
	}
</style>
