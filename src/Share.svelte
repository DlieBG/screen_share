<script>
	import Peer from 'peerjs';

	var peer = new Peer('bschwering-screenshare-share');

	let stream = null;

	function startStream() {
		try {
			navigator.mediaDevices.getDisplayMedia()
			.then((s) => {
				stream = s;
			})
			.catch((e) => {
				alert(e)
			});
		} catch(e) {
			alert(e)
		}
		

		peer.on('open', () => {
			peer.on('connection', (view) => {
				view.close();
				peer.call('bschwering-screenshare-view', stream)
			});
		});
	}
</script>

<main>
	<h2>
		Share
		<br>
		Screen
	</h2>
	{#if stream}
	<p>
		Your stream is running...
	</p>
	{:else}
	<p>
		Please select your screen to share.
		<button on:click={startStream}>Select Screen</button>
	</p>
	{/if}
	
</main>

<style>
	h2 {
		color: #00ff9d;
		text-transform: uppercase;
		font-size: 3em;
		font-weight: 200;
	}

	button {

	}
</style>