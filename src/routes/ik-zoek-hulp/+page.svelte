<script lang="ts">
	import { resolve } from '$app/paths';
	import WidePhoto from '$lib/WidePhoto.svelte';

	const steps = [
		['Kennismaken', 'We luisteren naar je situatie en brengen samen je hulpvraag in kaart.'],
		['Plan maken', 'We bepalen doelen die haalbaar, duidelijk en persoonlijk zijn.'],
		['Aan de slag', 'Je krijgt begeleiding die past bij jouw tempo en dagelijks leven.']
	];
</script>

<svelte:head>
	<title>Ik zoek hulp | Samenbijeen</title>
</svelte:head>

<section class="page-hero">
	<h1>Extra steun wanneer het dagelijks leven even niet vanzelf gaat.</h1>
	<p>
		Of het nu gaat om structuur, zelfstandigheid, sociale vaardigheden, persoonlijke verzorging of
		weer meedoen in de maatschappij: Samenbijeen kijkt met je mee.
	</p>
	<a class="button primary" href={resolve('/contact')}>Bespreek je hulpvraag</a>
</section>

<WidePhoto src="/images/page-help.svg" alt="Abstracte visual over hulpvraag en rust" />

<section class="section process">
	{#each steps as step, index (step[0])}
		<article class="process-step reveal" style={`--delay: ${index * 110}ms`}>
			<span>0{index + 1}</span>
			<h2>{step[0]}</h2>
			<p>{step[1]}</p>
		</article>
	{/each}
</section>

<section class="cta-band">
	<div>
		<h2>Je hoeft de juiste zorgvraag niet perfect te formuleren. Daar helpen wij bij.</h2>
	</div>
	<a class="button secondary" href={resolve('/zorg-ondersteuning')}>Bekijk ondersteuning</a>
</section>
