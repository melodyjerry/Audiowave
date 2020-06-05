<template>
	<div id="app">
		<Player :size="size" ref="wave"></Player>
		
		
	</div>
</template>

<script>
import Player from './components/Player.vue'
import {Musicvisualizer} from './assets/MusicVisualizer.js'
export default {
	name: 'App',
	components: {
		Player
	},
	data(){
		return{
			size:64
		}
	},
	mounted(){
		//this.mv.stop()
		this.mv = new Musicvisualizer({
			size:this.size*2,
			draw:this.$refs.wave.draw
		});
		this.mv.changeVolumn(0.6)
		this.mv.play("Gimme×Gimme.mp3");
	}
}
</script>

<style>
</style>
