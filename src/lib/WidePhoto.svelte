<script lang="ts">
	let {
		src,
		alt,
		title,
		text,
		cards = [],
		class: className = ''
	}: {
		src: string;
		alt: string;
		title: string;
		text: string;
		cards?: { title: string; text: string }[];
		class?: string;
	} = $props();
</script>

<figure class={`wide-photo ${className} reveal delay-1`}>
	<img {src} {alt} loading="lazy" decoding="async" />
	<figcaption>
		<strong>{title}</strong>
		<span>{text}</span>
		{#if cards.length}
			<div class="wide-photo-cards">
				{#each cards as card (card.title)}
					<article>
						<h3>{card.title}</h3>
						<p>{card.text}</p>
					</article>
				{/each}
			</div>
		{/if}
	</figcaption>
</figure>
