<template>
	<div class="wave">
		<div><canvas class="canwave" ref="wavebody"></canvas></div>
		
	</div>
</template>

<script>
import Two from 'two.js'
export default {
	name: 'Player',
	props:{
		size:Number
	},
	data(){
		return {
			circlesize:200,
			wavesize: 66,
			cuthead:14
		}
	},
	methods:{
		draw(arr){
			this.two.clear()
			var lines = []
			arr = arr.slice(this.cuthead,arr.length)
			var wcenter = this.two.width / 2
			var hcenter = this.two.height / 2
			for(var i=0;i<this.size;i++){
				var sinwave = Math.pow(arr[i],5) / Math.pow(256,5) * this.wavesize
				
				var x1 = wcenter + Math.sin(Math.PI * this.deg*i / 180) * (this.circlesize + sinwave)
				var y1 = hcenter + Math.cos(Math.PI * this.deg*i / 180) * (this.circlesize + sinwave)
				var x2 = wcenter + Math.sin(Math.PI * this.deg*i / 180) * (this.circlesize - sinwave)
				var y2 = hcenter + Math.cos(Math.PI * this.deg*i / 180) * (this.circlesize - sinwave)
				lines.push([x1, y1, x2, y2])
				var line = this.two.makeLine(x1, y1, x2, y2)
				line.stroke = 'skyblue'
				line.linewidth = 2
				
			}
			
			for(i=0;i<lines.length-1;i++){
				var line1 = this.two.makeLine(lines[i][0], lines[i][1], lines[i+1][0], lines[i+1][1])
				line1.stroke = 'skyblue'
				line1.linewidth = 2
				
				var line2 = this.two.makeLine(lines[i][2], lines[i][3], lines[i+1][2], lines[i+1][3])
				line2.stroke = 'skyblue'
				line2.linewidth = 2
			}
			line1 = this.two.makeLine(lines[lines.length-1][0], lines[lines.length-1][1], lines[0][0], lines[0][1])
			line1.stroke = 'skyblue'
			line1.linewidth = 2
			
			line2 = this.two.makeLine(lines[lines.length-1][2], lines[lines.length-1][3], lines[0][2], lines[0][3])
			line2.stroke = 'skyblue'
			line2.linewidth = 2
			
		}
	},
	mounted(){
		var canvas = this.$refs.wavebody
		this.two = new Two({
			fullscreen:false,
			autostart: true,
			width:800,
			height:800,
			type:Two.Types.canvas,
			domElement: canvas
			})
		this.deg = 360/(this.size)
	}
}
</script>
<style lang="scss">
	.wave{
		height: 1px;
		width: 1px;
		position: absolute;
		top: 0;
		bottom: 0;
		left: 0;
		right: 0;
		margin: auto auto;
		.canwave{
			display: inline-flex;
			position: absolute;
			left: 50%;
			top: 50%;
			margin-left: -400px;
			margin-top: -400px;
		}
	}
</style>