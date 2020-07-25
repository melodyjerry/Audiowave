<template>
	<div class="himg">
		<div class="img" :class="{'spin':spin}" :style="'background-image:url(' + url + ')'"></div>
	</div>
</template>

<script>
	export default {
		name: 'Headimg',
		props:{
			url:String,
			spin:{
				type: Boolean,
				default: true
			},
		},
		data(){
			return {

			}
		},
		methods:{
		},
		mounted(){
		}
	}
</script>

<style lang="scss">
	.himg{
		
		height: 300px;
		width: 300px;
		position: absolute;
		top: 0;
		bottom: 0;
		left: 0;
		right: 0;
		margin: auto auto;
		
		.dvd{
			height: 20px;
			width: 20px;
			position: absolute;
			top: 0;
			bottom: 0;
			left: 0;
			right: 0;
			margin: auto auto;
			border: {
				color: gray;
				width: 10px;
				style: solid;
				radius:100%;
			}
			background: {
				color: white;
			}
		}
		
		.img{
			height: 100%;
			width: 100%;
			border: {
				radius:100%;
				style:solid;
				color:deepskyblue;
				width:4px;
			}
			background: {
				attachment:default;
				repeat:no-repeat;
				size:cover;
				position: 50%;
			}
		}
	}
	.spin{
		animation:spin 9s linear 0.2s infinite;
	}
	@keyframes spin{
		0%{
			transform: rotate(0deg);
		}
		100%{
			transform: rotate(360deg);
		}
	}
</style>
