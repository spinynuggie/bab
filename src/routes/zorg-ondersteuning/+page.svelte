<script lang="ts">
	import ResponsiveImage from '$lib/ResponsiveImage.svelte';
	import RevealText from '$lib/RevealText.svelte';

	const support = [
		'Administratie en financiën',
		'Huishoudelijke ondersteuning',
		'Structuur in het dagelijks leven',
		'Passend dagritme opbouwen',
		'Werk, vrijwilligerswerk of dagbesteding',
		'Regie over het eigen leven terugpakken'
	];
</script>

<svelte:head>
	<title>Zorg / ondersteuning | Samenbijeen</title>
</svelte:head>

<section class="page-hero">
	<h1>Ambulante begeleiding voor rust en stabiliteit.</h1>
	<p>
		Samenbijeen biedt begeleiding aan huis voor jongeren, volwassenen en gezinnen die vastlopen op
		meerdere leefgebieden.
	</p>
</section>

<ResponsiveImage
	class="wide-content-photo"
	src="/images/content/road-900.webp"
	srcset="/images/content/road-900.webp 900w, /images/content/road-1400.webp 1400w"
	sizes="(max-width: 900px) 100vw, 1180px"
	alt="Een open weg als symbool voor stap voor stap vooruitgaan"
/>

<section class="section centered-support">
	<div class="section-heading reveal">
		<RevealText text="Ambulante begeleiding" />
		<p>
			Wij ondersteunen bij onder andere administratie, financiën, het huishouden en het aanbrengen
			van structuur in het dagelijks leven.
		</p>
	</div>
	<div class="glass-pills support-pills reveal">
		{#each support as item, index (item)}
			<span style={`--delay: ${index * 70}ms`}>{item}</span>
		{/each}
	</div>
</section>

<section class="section split">
	<div>
		<RevealText text="Samenwerkingen" />
	</div>
	<div class="copy-stack reveal delay-1">
		<p>
			Wij ondersteunen zorgorganisaties bij het creëren van een veilige en professioneel ingerichte
			zorglocatie van A tot Z. Denk aan structuur, aansturing van zorgteams, veiligheidsbeleid,
			werkprocessen, protocollen en begeleidingsmethodieken.
		</p>
		<p>
			Ook ondersteunen wij zorgorganisaties, thuiszorg en gemeenten bij het vinden van
			gekwalificeerde begeleiders. Ons doel is stabiliteit creëren, zodat passende ondersteuning
			gewaarborgd blijft.
		</p>
	</div>
</section>
