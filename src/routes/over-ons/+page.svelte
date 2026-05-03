<script lang="ts">
	import ResponsiveImage from '$lib/ResponsiveImage.svelte';
	import RevealText from '$lib/RevealText.svelte';
</script>

<svelte:head>
	<title>Over ons | Samenbijeen</title>
</svelte:head>

<section class="page-hero compact">
	<h1>We doen het samen.</h1>
	<p>
		Samenbijeen biedt professionele begeleiding aan jongeren en volwassenen die tijdelijk vastlopen
		of de grip op hun leven zijn kwijtgeraakt.
	</p>
</section>

<ResponsiveImage
	class="wide-content-photo"
	src="/images/content/home-hero-900.webp"
	srcset="/images/content/home-hero-900.webp 900w, /images/content/home-hero-1800.webp 1800w"
	sizes="(max-width: 900px) 100vw, 1180px"
	alt="Handen die puzzelstukken samenbrengen"
/>

<section class="section split">
	<div>
		<RevealText text="Met praktische en doelgerichte begeleiding" />
	</div>
	<div class="copy-stack reveal delay-1">
		<p>
			Met praktische en doelgerichte begeleiding werken we aan haalbare doelen. Denk aan hulp bij
			administratie, huishouden en begeleiding om zelfvertrouwen weer terug te winnen.
		</p>
		<p>
			Onze missie is om mensen te begeleiden op weg naar zelfredzaamheid, rust en stabiliteit. Bij
			Samenbijeen staan we naast hen.
		</p>
		<p>
			Daarnaast ondersteunen wij zorgorganisaties, gemeenten en samenwerkingspartners bij het
			inzetten van gekwalificeerde zorgprofessionals.
		</p>
	</div>
</section>

<section class="section quote-section reveal delay-1">
	<blockquote>“Samen kijken we naar mogelijkheden en kracht.”</blockquote>
	<p>
		Wij geloven dat echte verandering ontstaat wanneer mensen zich gezien, gehoord en ondersteund
		voelen. Daarom werken wij vanuit verbinding, betrokkenheid en samenwerking.
	</p>
</section>
