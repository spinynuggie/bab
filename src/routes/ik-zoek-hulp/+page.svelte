<script lang="ts">
	import { resolve } from '$app/paths';
	import RevealText from '$lib/RevealText.svelte';
	import WidePhoto from '$lib/WidePhoto.svelte';

	const supportAreas = [
		[
			'Overzicht, rust en richting',
			'Soms kunnen gebeurtenissen of ervaringen veel invloed hebben op je dagelijks leven. Samen kijken we naar wat jij nodig hebt.'
		],
		[
			'Passend dagritme',
			'Samen werken we aan een passend dagritme, het ontwikkelen van praktische vaardigheden en het deelnemen aan werk, vrijwilligerswerk of dagbesteding.'
		],
		[
			'Regie terugpakken',
			'Ook ondersteunen we je bij het (her)pakken van de regie over je eigen leven.'
		]
	];
</script>

<svelte:head>
	<title>Ik zoek hulp | Samenbijeen</title>
</svelte:head>

<section class="page-hero">
	<h1>Samen kijken we naar wat jij nodig hebt.</h1>
	<p>
		Soms kunnen gebeurtenissen of ervaringen veel invloed hebben op je dagelijks leven. Samen kijken
		we naar wat jij nodig hebt en werken we aan meer overzicht, rust en richting.
	</p>
	<a class="button primary" href={resolve('/contact')}>Bespreek je hulpvraag</a>
</section>

<WidePhoto
	src="/images/page-help.svg"
	alt="Abstracte visual over hulpvraag en rust"
	title="Overzicht, rust en richting"
	text="Onze begeleiding helpt je om weer overzicht, zelfvertrouwen en rust te vinden."
/>

<section class="section process">
	{#each supportAreas as area, index (area[0])}
		<article class="process-step reveal" style={`--delay: ${index * 110}ms`}>
			<span>0{index + 1}</span>
			<h2>{area[0]}</h2>
			<p>{area[1]}</p>
		</article>
	{/each}
</section>

<section class="cta-band">
	<div>
		<h2>Samen kijken we naar wat jij nodig hebt.</h2>
	</div>
	<a class="button secondary" href={resolve('/zorg-ondersteuning')}>Bekijk ondersteuning</a>
</section>

<section class="section split">
	<div>
		<RevealText text="Stap voor stap werken we aan meer overzicht, rust en richting." />
	</div>
	<div class="copy-stack reveal delay-1">
		<p>
			We helpen bij het ontwikkelen van praktische vaardigheden, het vinden van een passend dagritme
			en het terugpakken van regie over je eigen leven.
		</p>
		<p>
			De begeleiding is persoonlijk en intensief. We staan dicht naast je en kijken samen naar wat
			nodig is om verder te komen.
		</p>
	</div>
</section>
