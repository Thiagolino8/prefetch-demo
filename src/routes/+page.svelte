<script lang="ts">
	let search = $state("");

	const getProducts = async (search: string) => {
		const response = await fetch(`https://dummyjson.com/products/search?q=${search}`);
		const data = await response.json();
		return data.products as { title: string; id: string }[];
	};
</script>

<input type="text" placeholder="Search for products..." bind:value={search} />

<ul>
	{#each await getProducts(search) as product (product.id)}
		<li><a href="/product/{product.id}">{product.title}</a></li>
		''
	{/each}
</ul>
