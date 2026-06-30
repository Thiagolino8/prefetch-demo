<script lang="ts">
	const { params } = $props();

	const getProduct = async (id: number) => {
		const response = await fetch(`https://dummyjson.com/products/${id}`);
		const data = await response.json();
		return data as { title: string; description: string; price: number };
	};

	const product = $derived(await getProduct(Number(params.id)));
</script>

<a href="/">Back to products</a>
{#if params.id > 1}
	<a href="/product/{Number(params.id) - 1}">Previous product</a>
{/if}
{#if params.id < 193}
	<a href="/product/{Number(params.id) + 1}">Next product</a>
{/if}

<h1>Product {product.title} Details</h1>
<p>{product.description}</p>
<p>Price: ${product.price.toFixed(2)}</p>
