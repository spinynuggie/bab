<script lang="ts">
	let {
		src,
		alt,
		title,
		text
	}: {
		src: string;
		alt: string;
		title: string;
		text: string;
	} = $props();
</script>

<figure class="wide-photo reveal delay-1">
	<img {src} {alt} loading="lazy" decoding="async" />
	<figcaption>
		<strong>{title}</strong>
		<span>{text}</span>
	</figcaption>
</figure>
