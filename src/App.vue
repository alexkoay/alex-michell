<template>
	<div id="overlay" :class="overlay ? 'show' : 'hide'">
		<h1>Welcome to our story</h1>
		<button @click="closeoverlay">Enter</button>
	</div>
	<audio id="song" autoplay preload="auto" loop controls src="/others/song.m4a" type="audio/aac">
	</audio>
	<button class="top action" @click="torsvp">RSVP</button>

	<div id="welcome"></div>

	<div class="content">

		<div id="logo">
			<Logo />
		</div>

		<p style="margin-top: 2em;">
			would&nbsp;like to&nbsp;have&nbsp;you<br />
			at&nbsp;our&nbsp;wedding&nbsp;celebration
		</p>

		<p style="margin-top: 2em;">
			<span style="display: inline-block; font-size: 2em">
				25.03.2023
			</span>
			<br />
			<span style="display: inline-block; font-family: 'zaoyiaishangni'; font-size: 1.3em; line-height: 1;
				margin-bottom: 0; padding-bottom: 0.4em">
				(闰二月&nbsp;初四)
			</span>
			<br />
			@ Elite House Penang 贵宾楼
		</p>

		<p style="font-size: 0.5em">
			<a
				href="https://www.google.com/calendar/render?action=TEMPLATE&text=Alex+%26+Michell+Wedding+Dinner&location=Elite+House%0A8%2C+Jalan+Perusahaan+Jelutong+2%0AFortune+Park%0A11600+George+Town%0APulau+Pinang%2C+Malaysia&dates=20230325T100000Z%2F20230325T133000Z">Add
				to Google Calendar</a>
			&nbsp;|&nbsp;
			<a href="/others/calendar.ics">Others</a>
		</p>


		<Schedule />
		<Location />
		<Hotel />
		<RSVP />

	</div>

	<div id="sep1"></div>

</template>

<script lang="ts">
import { defineComponent } from 'vue';
import RSVP from './components/RSVP.vue'
import Logo from './components/LogoC.vue'
import Schedule from './components/ScheduleD.vue'
import Hotel from './components/Hotel.vue'
import Location from './components/Location.vue'

export default defineComponent({
	components: {
		RSVP,
		Logo,
		Schedule,
		Hotel,
		Location,
	},
	data() {
		return { overlay: true }
	},
	mounted() {
		let played = false;
		let el = document.querySelector('audio') as HTMLAudioElement;
		el.addEventListener('play', () => played = true);

		function tryplay() {
			console.log('trying', played)
			if (played) return;
			let el = document.querySelector('audio') as HTMLAudioElement;
			if (!el) { return; }
			el.play();

			setTimeout(tryplay, 500);
		}
		tryplay();
	},
	methods: {
		closeoverlay() {
			let el = document.querySelector('audio') as HTMLAudioElement;
			el.play();
			this.overlay = false;
		},
		torsvp() {
			document.location.hash = 'rsvp';
		}
	}
});
</script>

<style lang="postcss">
@import "./fonts.css";

@import url('https://fonts.googleapis.com/css2?family=Nixie+One&family=Playfair+Display:ital,wght@0,400;0,700;1,400;1,700&display=swap');


:root {
	--bgcolor: #fffbee;
	--txtcolor: #333;
	--hdcolor: #333;
	--brdcolor: #999;
	--engfont: "Love Seed";
	--chnfont: "zaoyiaishangni";
}

* {
	box-sizing: border-box;
}

#overlay {
	position: fixed;
	z-index: 100;
	top: 0;
	left: 0;
	right: 0;
	bottom: 0;
	background: var(--bgcolor);

	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;

	& h1 {
		font-size: calc(min(15vw, 5em));
	}


	&.show {
		opacity: 1;
	}

	&.hide {
		transition: all 2s;
		opacity: 0;
		visibility: hidden;
	}
}

#welcome {
	background: linear-gradient(#fffbee00 80%, #fffbeeff), url('/images/IMG_7425.jpg') 55% 70%;
	background-size: cover;
	background-blend-mode: normal;
	top: 0;
	left: 0;
	width: 100vw;
	height: 100vh;
}


#sep1 {
	background: linear-gradient(#fffbeeff, #fffbee00 20%), url('/images/IMG_4416.jpg') 50% 30%;
	background-size: cover;
	background-blend-mode: normal;
	top: 0;
	left: 0;
	width: 100vw;
	height: 100vh;
}


#logo {
	padding: 3em 0 0;
}

#song {
	z-index: 10;
	position: fixed;
	bottom: 12pt;
	left: 12pt;
}

html,
input,
button {
	font: min(max(2vw, 14pt), 24pt)/1.2 "Playfair Display";
	font-weight: 400;
}

body {
	margin: 0;
	padding: 0;
}

body {
	background: var(--bgcolor);
	text-align: center;
	color: var(--txtcolor);
}

.content {
	max-width: min(max(70vw, 720px), 1080px);
	margin: 0 auto;
	padding: 2em;
}

h1,
h2,
h3,
h4,
h5,
h6 {
	color: var(--hdcolor);
	font: 1em/1 var(--engfont), var(--chnfont);
	font-weight: normal;
	margin: 0;
	padding: 0;
}

section {
	margin-top: 2em;
	--hdsize: 3em;

	& hr {
		padding-top: 2em;
		border-bottom: 1px solid var(--brdcolor);
		border-width: 0 0 1px 0;
	}

	& h3 {
		font-size: var(--hdsize);
		margin-top: -0.7em;
		text-align: center;
		margin-bottom: 0.2em;

		& span {
			background: var(--bgcolor);
			padding: 0.5em;
		}
	}
}

.top.action {
	position: fixed;
	bottom: 12pt;
	right: 12pt;
}

dd {
	margin: 0;
}
</style>