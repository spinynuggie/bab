<script lang="ts">
	import WidePhoto from '$lib/WidePhoto.svelte';

	const items = [
		'Structuur aanbrengen in de dag',
		'Zelfredzaamheid en sociale vaardigheden versterken',
		'Omgaan met emoties, spanning en verandering',
		'Praktische stappen richting wonen, school, werk of dagbesteding'
	];
</script>

<svelte:head>
	<title>Begeleiding / coaching | Samenbijeen</title>
</svelte:head>

<section class="page-hero">
	<h1>Doelgerichte begeleiding met aandacht voor de mens achter de vraag.</h1>
	<p>
		Wij begeleiden mensen bij groei, herstel en zelfstandigheid. De aanpak is persoonlijk, praktisch
		en gericht op duurzame vooruitgang.
	</p>
</section>

<WidePhoto src="/images/page-coaching.svg" alt="Abstracte visual over begeleiding en coaching" />

<section class="section split">
	<div>
		<h2>Wat begeleiding concreet kan opleveren.</h2>
	</div>
	<ul class="feature-list reveal-children">
		{#each items as item (item)}
			<li>{item}</li>
		{/each}
	</ul>
</section>

<section class="section quote-section reveal delay-1">
	<blockquote>“Bij Samenbijeen staan we naast je, zodat jij vooruit kunt.”</blockquote>
	<p>
		We werken vanuit vertrouwen en helderheid. Waar nodig sluiten we aan bij bewezen methodieken,
		zoals het 8-fasenmodel, zodat begeleiding meetbaar en begrijpelijk blijft.
	</p>
</section>
