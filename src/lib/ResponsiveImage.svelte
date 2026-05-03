<script lang="ts">
	let {
		src,
		srcset = '',
		sizes = '100vw',
		alt,
		loading = 'lazy',
		class: className = ''
	}: {
		src: string;
		srcset?: string;
		sizes?: string;
		alt: string;
		loading?: 'eager' | 'lazy';
		class?: string;
	} = $props();
</script>

<img class={className} {src} {srcset} {sizes} {alt} {loading} decoding="async" />
