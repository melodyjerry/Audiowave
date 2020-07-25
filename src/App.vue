<template>
	<div id="app">
		
		<div class="main">
			<div class="bkground" :style="'background-image:url(' + imgurl + ')'"></div>
			<Headimg :url="imgurl"></Headimg>
			<Player :size="wavesize" ref="wave"></Player>
			<Input />
			<Pannel />
		</div>
		
	</div>
</template>

<script>
import Player from './components/Player.vue'
import Pannel from './components/Pannel.vue'

import Headimg from './components/Headimg.vue'
import Input from './components/Input.vue'
import {Musicvisualizer} from './assets/MusicVisualizer.js'
export default {
	name: 'App',
	components: {
		Player,
		Headimg,
		Input,
		Pannel
	},
	data(){
		return{
			wavesize:70,
			
			imgurl:"http://imge.kugou.com/stdmusic/20191111/20191111164001608863.jpg",
			musicurl:"test.mp3"
		}
	},
	methods:{
		getCurrentTime(){
			if(this.mv){
				return this.mv.analyser.context.currentTime
			}
			return 0
		},
		play(url){
			
			if(url)this.musicurl = url
			this.mv.play(this.musicurl,0);
		},
		setCurrentTime(time){
			this.mv.source[this.mv.source.start?"start":"noteOn"](0,time)
		},
		stop(){
			this.mv.stop()
		},
		chback(url){
			this.imgurl = url
		}
	},
	computed:{
		
	},
	mounted(){
		//this.mv.stop()
		var draw = this.$refs.wave?this.$refs.wave.draw:()=>{}
		this.mv = new Musicvisualizer({
			size:256,
			draw:draw
		});
		this.mv.changeVolumn(0.6)
		this.play()
	}
}
</script>

<style lang="scss">
	body{
		overflow-x: hidden;
	}
	.main{
		min-height: 100vh;
		
		
	}
	.bkground{
		height: 100vh;
		width: 100%;
		background: {
			repeat:no-repeat;
			size:cover;
			attachment:fixed;
			position:center;
		}
		filter: blur(10px);
	}
</style>
