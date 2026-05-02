<script lang="ts">
	let { src, alt }: { src: string; alt: string } = $props();
</script>

<figure class="wide-photo reveal delay-1">
	<img {src} {alt} loading="lazy" decoding="async" />
</figure>
