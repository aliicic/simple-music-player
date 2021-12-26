<template>
 
 <div class="music-player-container" :class="{ 'is-playing' : isPlaying  }">

		<div class="music-player">
			<div class="player-content-container">
				<h1 class="artist-name">AliAghAkhAni</h1><!--  /.track-title -->
	
				<h3 class="song-title">{{ currentMusic.title }}</h3><!--  /.song-title -->
				<div class="music-player-controls">
					<div class="control-back" @click="prev"></div><!--  /.control-back -->
					<div class="control-play" @click="play"></div><!--  /.control-play -->
					<div class="control-forwards" @click="next"></div><!--  /.control-forwards -->
				</div><!--  /.music-player-controls -->
			</div><!--  /.player-content-container -->
		</div><!--  /.music-player -->

		<div class="album">
			<div class="album-art" :style="`background-image: url(${currentMusic.photo}) `"></div><!--  /.album-art -->
			<div class="vinyl" :style="`background-image: url('../public/vinyl.png'), url(${currentMusic.photo})`"></div><!--  /.vinyl -->
		</div><!--  /.album-art -->

	</div><!--  /.music-player -->


</template>

<script>
import {ref} from 'vue';
import musics from './musics'

export default {

name : 'App',

setup (){
  
  const currentMusic = ref(null);
  const isPlaying = ref(false);
  const audio = ref(null);
  const current = ref(0);
  
  
  currentMusic.value = musics[current.value];

  audio.value = new Audio();
  audio.value.src = currentMusic.value.source;
  
  const play = () => {
  
  

  if(!isPlaying.value){
        isPlaying.value = true;
        audio.value.play();
  }else {
        isPlaying.value = false;
        audio.value.pause();
  }
  };
  
   const next = () => {
       if(isPlaying.value){
         audio.value.play();
       } 
       current.value ++ ; 
       if(current.value === musics.length){
         current.value = 0 ; 
       }
       currentMusic.value = musics[current.value];
       audio.value.src = currentMusic.value.source;
      
      play();
   };
   const prev = () => {
       if(isPlaying.value){
         audio.value.play();
       } 
      
       if(current.value ==0){
         current.value = musics.length - 1  ; 
       }else{
          current.value -- ; 
       }
       currentMusic.value = musics[current.value];
       audio.value.src = currentMusic.value.source;
      
      play();
       
   };



  return { 
  
  currentMusic,
  isPlaying,
  currentMusic,
  play,
  audio,
  current,
  next,
  prev



  }

}


}

</script>
