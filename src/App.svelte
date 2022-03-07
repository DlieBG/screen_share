<script>
	import { Router, Route, Link } from "svelte-navigator";
	import Share from './Share.svelte';
	import View from './View.svelte';
</script>

<Router>
	<main>
		<Route path="">
			<h1>
				Screen 
				<br>
				Share
			</h1>
			<div>
				<Link to="share"><button>Share Screen</button></Link>
				<Link to="view"><button>View Screen</button></Link>
			</div>
		</Route>

		<Route path="share">
			<Share/>
		</Route>

		<Route path="view">
			<View/>
		</Route>	
	</main>

	
</Router>

<style>
	:global(body) {
		background-color: black;
		color: white;
	}

	main {
		text-align: center;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	button {
		background-color: #00c1ff;
		color: white;
		border: none;
		padding: 1em;
		font-size: 1.5em;
		font-weight: 200;
		border-radius: 5px;
		margin: 1em;
		cursor: pointer;
	}	
</style>