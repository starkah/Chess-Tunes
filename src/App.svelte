

<script>
	import pgnParser from 'pgn-parser';
	import * as Tone from 'tone'
	import { note, Note, Scale } from "@tonaljs/tonal";
	// const pgnParser = require('pgn-parser');

	
	let files;
	let len; let i; 
	var notes1 = []
	var scale; var pp;
	var notes = ['A5','A#5','B5','C4','C#4','D4','D#4','E4','F4','F#4','G4','G#4'];
	function upload() {
  var reader = new FileReader();
  reader.onload = function(evt) {
	// console.log(evt.target.result);
	const [result] = pgnParser.parse(evt.target.result);
	len = result.moves.length
	scale = notes[len%12]
	if(len%2 == 0) 
		scale = scale + " minor";
	else 
		scale = scale + " major";
	//var notes1 = []
	for(i=0;i<len;i++) {
		notes1[i] = result.moves[i].move.slice(-1);
	}
	var snotes = Scale.get(scale).notes;
	//create a synth and connect it to the main output (your speakers)
	const synth = new Tone.Synth().toDestination();
	//play a middle 'C' for the duration of an 8th note
	const now = Tone.now()
	pp=1;
	for( i=0; i <notes1.length;i++) {
		synth.triggerAttackRelease(snotes[notes1[i]-1], "0.5", now + (0.2*i));	  
	}
	console.log(scale)
	console.log(snotes)
  };
  reader.readAsText(files[0]);
}
</script>

<main>
	<div class="enter">
	<input type="file" bind:files>
	{#if files}
		   <button  class="submit s1" on:click={upload}>Play</button>
	{:else}
		<button  class="submit s1" on:click={upload} disabled>Play</button>
	{/if}
 </div>
 
 <h1>CHESS TUNES</h1>
 <h2>A place to turn your strategic chess matches into some fun musical tunes!</h2>
 <div class="text">
	<p>Upload you PGN files and enjoy!</p>
 </div>
 <div class="spinner">
	<div class="rect1"></div>
	<div class="rect2"></div>
	<div class="rect3"></div>
	<div class="rect4"></div>
	<div class="rect5"></div>
  </div>
 


  <button class="button button2"> <a href="https://www.chess.com/" target="_blank" ><p1>Chess.com</p1> </a></button> 
  <button class="button button2"> <a href="https://lichess.org/?any" target="_blank"><p1>Lichess.com</p1></a></button>

 
</main>
 
<style>
	p{
		color: #659db5;
		font-family: 'Noto Serif KR', serif;
		font-size: 25px;
		position: relative;
       left: 18px;
       top: 60px;
	}
	main {
	   
		background:url('https://mir-s3-cdn-cf.behance.net/project_modules/max_632/11664a102041989.5f2d2c33b253e.jpg');
		background-size: cover;
		 padding:0;
		  margin:0;
 
	  text-align: center;
		padding:4em;
		max-width: 340px;
		margin: 0 auto;
	}
 
	h1 {
		color:#05cde3;
		font-family: 'Noto Serif KR', serif;
		text-transform: uppercase;
		font-size: 100px;
		font-weight: 100;
	   
	}

	h2 {
		color: #659db5;
		font-family: 'Noto Serif KR', serif;
		font-size: 25px;
		font-weight: 100;
		position: relative;
       left: 18px;
       top: -63px;
	   
	}
 
	.spinner {
  margin: 200px auto;
  width: 150px;
  height: 90px;
  text-align: center;
  font-size: 10px;
 }
 
 .spinner > div {
  background-color: rgb(255, 244, 244);
  height: 100%;
  width: 6px;
  display: inline-block;
  position: relative;
  left: 31px;
  top: -18px;
   -webkit-animation: sk-stretchdelay 1.2s infinite ease-in-out;
  animation: sk-stretchdelay 1.2s infinite ease-in-out;
 }
 
 .spinner .rect2 {
  -webkit-animation-delay: -1.1s;
  animation-delay: -1.1s;
 }
 
 .spinner .rect3 {
  -webkit-animation-delay: -1.0s;
  animation-delay: -1.0s;
 }
 
 .spinner .rect4 {
  -webkit-animation-delay: -0.9s;
  animation-delay: -0.9s;
 }
 
 .spinner .rect5 {
  -webkit-animation-delay: -0.8s;
  animation-delay: -0.8s;
 }
 
 @-webkit-keyframes sk-stretchdelay {
  0%, 40%, 100% { -webkit-transform: scaleY(0.4) } 
  20% { -webkit-transform: scaleY(1.0) }
 }
 
 @keyframes sk-stretchdelay {
  0%, 40%, 100% {
	transform: scaleY(0.4);
	-webkit-transform: scaleY(0.4);
  }  20% {
	transform: scaleY(1.0);
	-webkit-transform: scaleY(1.0);
  }
 }
 .enter{
	position: absolute;
	 left: 500px;
	 top: 457px;
	display: inline-block;
	font-size: 19px;
	padding: 0.5%;
	background-color:black;
	color:white;
 }
	
 .submit {
  background-color: black; /* Green */
  border: 2px solid white;
  color: white;
  padding: 16px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  transition-duration: 0.4s;
  cursor: pointer;
 }
 
 
 .s1 {
  background-color:black;
  color: white;
  border: 2px solid white;
 }
 
 .s1:hover {
  background-color: #008CBA;
  color: white;
 }

 .button {
	position: relative;
	 left: 32px;
	 top: -582px;
  background-color:black; 
  border: 2px solid white;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  -webkit-transition-duration: 0.4s; /* Safari */
  transition-duration: 0.4s;
}
.button2:hover {
  box-shadow: 0 12px 16px 0 rgba(0,0,0,0.24),0 17px 50px 0 rgba(0,0,0,0.19);
}
 
 p1{
	 color:white;
 }
 
	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
 </style>

