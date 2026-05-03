<script lang="ts">
	import { onMount } from 'svelte';

	let {
		text,
		as = 'h2',
		class: className = ''
	}: {
		text: string;
		as?: 'h1' | 'h2' | 'h3' | 'p';
		class?: string;
	} = $props();

	let element: HTMLElement;
	let visible = $state(false);
	const words = $derived(text.split(' '));

	onMount(() => {
		if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
			visible = true;
			return;
		}

		const observer = new IntersectionObserver(
			([entry]) => {
				if (!entry?.isIntersecting) return;
				visible = true;
				observer.disconnect();
			},
			{ rootMargin: '0px 0px -18% 0px', threshold: 0.32 }
		);

		observer.observe(element);
		return () => observer.disconnect();
	});
</script>

<svelte:element this={as} bind:this={element} class={`reveal-text ${className}`} class:visible>
	{#each words as word, index (`${word}-${index}`)}
		<span style={`--i: ${index}`}>{word}{index < words.length - 1 ? ' ' : ''}</span>
	{/each}
</svelte:element>
