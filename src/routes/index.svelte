<script>
	import successkid from 'images/successkid.jpg';
</script>

<style>
	figure {
		margin: 0 0 1em 0;
	}

	img {
		width: 100%;
		max-width: 400px;
		margin: 0 0 1em 0;
		border-radius: 8px;
	}

	p {
		margin: 1em auto;
	}

	@media (min-width: 480px) {
		h1 {
			font-size: 4em;
		}
	}

</style>

<svelte:head>
	<title>Sapper project template</title>
</svelte:head>


<figure>
	<h2>Have fun with Sapper!!</h2>
	<img alt="Success Kid" src="{successkid}">
	<figcaption></figcaption>
</figure>

