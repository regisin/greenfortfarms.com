<script>
	export let brand;
	export let items;
	export let path;

	let hidden = true;
	function toggleMenu() {
		hidden = !hidden;
	}
</script>

<header>
	<div>
		<a href={brand.url}>
			<img src={brand.image} alt={brand.title} />
		</a>
		<span>{brand.title}</span>
		<nav>
			{#each items as item}
				<a sveltekit:prefetch class:active={path === item.url} href={item.url}>{item.title}</a>
			{/each}
		</nav>
		<div>
			<button on:click={toggleMenu}>
				<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512">
					<path
						d="M0 96C0 78.33 14.33 64 32 64H416C433.7 64 448 78.33 448 96C448 113.7 433.7 128 416 128H32C14.33 128 0 113.7 0 96zM0 256C0 238.3 14.33 224 32 224H416C433.7 224 448 238.3 448 256C448 273.7 433.7 288 416 288H32C14.33 288 0 273.7 0 256zM416 448H32C14.33 448 0 433.7 0 416C0 398.3 14.33 384 32 384H416C433.7 384 448 398.3 448 416C448 433.7 433.7 448 416 448z"
					/>
				</svg>
			</button>
		</div>
	</div>
	<ul class:hidden>
		{#each items as item}
			<li>
				<a sveltekit:prefetch class:active={path === item.url} href={item.url}>{item.title}</a>
			</li>
		{/each}
	</ul>
</header>

<style lang="postcss" global>
	:local(header) {
		@apply bg-white py-2;
	}
	:local(header) div {
		@apply flex justify-between mx-auto md:max-w-3xl;
	}
	:local(header) div a {
		@apply mx-2;
	}
	:local(header) div span {
		@apply font-bold my-auto md:hidden;
	}
	:local(header) div a img {
		@apply w-12;
	}
	:local(header) div nav {
		@apply space-x-4 my-auto hidden md:block;
	}
	:local(header) div nav a {
		@apply font-normal;
	}
	:local(header) div div {
		@apply md:hidden w-6 mx-2 my-auto;
	}
	:local(.active) {
		@apply underline;
	}
</style>
