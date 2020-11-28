<script>
	// export let segment;
	let page = 'home';
</script>

<style>
	nav {
		display: grid;
		grid-template-columns: 1fr 2fr;
		border-bottom: 1px solid rgba(255,62,0,0.1);
		font-weight: 300;
		padding: 0 1em;
	}

	ul {
		margin: 0;
		padding: 0;
	}

	/* clearfix */
	ul::after {
		content: '';
		display: block;
		clear: both;
	}

	li {
		display: block;
		float: left;
	}

	a {
		text-decoration: none;
		padding: 0 0.5em;
		display: block;
	}
	a.active {
		background-color: #999999;
		color: #f9f9f9;
	}
</style>

<nav>
	<h2>Demo Apps</h2>
	<ul>
		<li><a on:click={() => page = 'home'} class:active={page === 'home'} href=".">Home</a></li>
		<li><a on:click={() => page = 'about'} class:active={page === 'about'} href="about">About</a></li>
		<li><a on:click={() => page = 'worldtimes'} class:active={page === 'worldtimes'} href="worldtimes">World Times</a></li>
		<li><a on:click={() => page = 'games'} class:active={page === 'games'} href="games">Games</a></li>
	</ul>
</nav>
