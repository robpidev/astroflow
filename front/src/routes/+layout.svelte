<script lang="ts">
	import favicon from '$lib/assets/favicon.svg';
	import { Willow, WillowDark } from '@svar-ui/svelte-core';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<WillowDark>
	<div>
		{@render children?.()}
	</div>
</WillowDark>

<style>
	/* div { */
	/* height: 100vh; */
	/* } */
</style>
