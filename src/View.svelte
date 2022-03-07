<script>
	import Peer from 'peerjs';

	let peer = new Peer('bschwering-screenshare-view');

	let stream = null;
	let playing = false;

	peer.on('open', () => {
		peer.connect('bschwering-screenshare-share');	
	});

	peer.on('call', (call) => {
		call.answer(null);
        call.on('stream', function(s) {
            var video = document.getElementById('video');
			video.style.display = 'block';
            video.srcObject = s;
			stream = true;
        });
	});

	function play() {
		var video = document.getElementById('video');
		playing = true;
		video.play();
	}
</script>

<main>
	{#if stream && !playing}
		<h2>
			View
			<br>
			Screen
		</h2>
		<p>
			The host is ready!
		</p>
		<button on:click={play}>Start stream</button>
	{:else if !playing}
		<h2>
			View
			<br>
			Screen
		</h2>
		<p>
			Please wait for your host. You have to reload the page manually.
		</p>
	{/if}

	<div class="overflow">
		<video id="video" on:click={play}>
			<track kind="captions">
		</video>
	</div>
</main>

<style>
	h2 {
		color: #0099ff;
		text-transform: uppercase;
		font-size: 3em;
		font-weight: 200;
	}

	button {
		margin-top: 1em;
		background-color: #ff0063;
		color: white;
		border: none;
		padding: .75em;
		font-size: 1.25em;
		font-weight: 200;
		border-radius: 5px;
		margin: 1em;
		cursor: pointer;
	}

	video {
		width: calc(100vw);
		height: calc(100vh);
		max-width: 100vw;
		max-height: 100vh;
		display: none;
	}

	.overflow {
		overflow: hidden;
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
	}
</style>