<script lang="ts">
	import ResponsiveImage from '$lib/ResponsiveImage.svelte';
	import RevealText from '$lib/RevealText.svelte';
</script>

<svelte:head>
	<title>Over ons | Samenbijeen</title>
</svelte:head>

<section class="page-hero compact centered-page-hero">
	<h1>We doen het samen.</h1>
	<p>
		Samenbijeen biedt professionele begeleiding aan jongeren en volwassenen die tijdelijk vastlopen
		of de grip op hun leven zijn kwijtgeraakt. Deze situatie kan voortkomen uit eerdere ervaringen
		of gebeurtenissen die impact hebben gehad op iemands leven.
	</p>
	<p>
		Met praktische en doelgerichte begeleiding werken we stap voor stap aan haalbare doelen. Denk
		bijvoorbeeld aan hulp bij administratie, huishouden en begeleiding om het zelfvertrouwen weer
		terug te winnen.
	</p>
	<p>
		Daarnaast ondersteunen wij zorgorganisaties, gemeenten en andere samenwerkingspartners bij het
		inzetten van gekwalificeerde zorgprofessionals. Ook bij complexe hulpvragen, crisissituaties of
		het organiseren van passende begeleiding zetten wij ervaren begeleiders in.
	</p>
</section>

<ResponsiveImage
	class="wide-content-photo"
	src="/images/content/home-hero-900.webp"
	srcset="/images/content/home-hero-900.webp 900w, /images/content/home-hero-1800.webp 1800w"
	sizes="(max-width: 900px) 100vw, 1180px"
	alt="Handen die puzzelstukken samenbrengen"
/>

<section class="section centered-support">
	<div class="section-heading reveal">
		<RevealText text="Missie" />
		<p>
			Wij geloven dat niemand er alleen voor hoeft te staan. Wij bieden persoonlijke begeleiding en
			coaching waarbij de mens centraal staat. Samen kijken we naar wat iemand nodig heeft om meer
			grip, vertrouwen en richting te vinden.
		</p>
	</div>
	<div class="section-heading reveal delay-1">
		<RevealText text="Visie" />
		<p>
			Wij geloven dat echte verandering ontstaat wanneer mensen zich gezien, gehoord en ondersteund
			voelen. Daarom werken wij vanuit verbinding, betrokkenheid en samenwerking. Ons uitgangspunt
			is dat je samen verder komt dan alleen.
		</p>
	</div>
</section>
