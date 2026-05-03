<script lang="ts">
	import { resolve } from '$app/paths';
	import WidePhoto from '$lib/WidePhoto.svelte';

	const supportAreas = [
		{
			title: 'Overzicht, rust en richting',
			text: 'Soms kunnen gebeurtenissen of ervaringen veel invloed hebben op je dagelijks leven. Samen kijken we naar wat jij nodig hebt.'
		},
		{
			title: 'Passend dagritme',
			text: 'Samen werken we aan een passend dagritme, praktische vaardigheden en deelname aan werk, vrijwilligerswerk of dagbesteding.'
		},
		{
			title: 'Regie terugpakken',
			text: 'Ook ondersteunen we je bij het (her)pakken van de regie over je eigen leven.'
		},
		{
			title: 'Persoonlijke begeleiding',
			text: 'De begeleiding is persoonlijk en intensief. We staan dicht naast de persoon en kijken samen naar wat nodig is.'
		}
	];
</script>

<svelte:head>
	<title>Ik zoek hulp | Samenbijeen</title>
</svelte:head>

<section class="page-hero">
	<h1>Als het dagelijks leven vastloopt.</h1>
	<p>
		Soms kunnen gebeurtenissen of ervaringen veel invloed hebben op je dagelijks leven. Samen kijken
		we naar wat jij nodig hebt en werken we aan meer overzicht, rust en richting.
	</p>
	<a class="button primary" href={resolve('/contact')}>Bespreek je hulpvraag</a>
</section>

<WidePhoto
	class="with-cards"
	src="/images/page-help.svg"
	alt="Abstracte visual over hulpvraag en rust"
	title="Samen werken we stap voor stap"
	text="Onze begeleiding helpt je om weer overzicht, zelfvertrouwen en rust te vinden."
	cards={supportAreas}
/>
