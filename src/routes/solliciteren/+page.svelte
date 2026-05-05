<script lang="ts">
	import { resolve } from '$app/paths';
	import ResponsiveImage from '$lib/ResponsiveImage.svelte';
	import RevealText from '$lib/RevealText.svelte';

	const points = [
		'Langdurige trajecten en projecten met betekenis',
		'Werken vanuit betrokkenheid, aandacht en professionaliteit',
		'Maatwerk bieden voor jongeren, volwassenen en gezinnen',
		'Samen bouwen aan begeleiding van hoge kwaliteit'
	];
</script>

<svelte:head>
	<title>Solliciteren | Samenbijeen</title>
</svelte:head>

<section class="page-hero compact centered-page-hero">
	<h1>Kom je werken bij Samenbijeen?</h1>
	<p>
		Samen maken we het verschil. Met langdurige trajecten en projecten zetten wij ons in voor
		begeleiding en ondersteuning van hoge kwaliteit. Wij werken vanuit betrokkenheid, aandacht en
		professionaliteit.
	</p>
	<a class="button primary" href={resolve('/contact')}>Neem contact op</a>
</section>

<section class="section split">
	<div class="reveal">
		<ResponsiveImage
			class="content-photo"
			src="/images/content/samen-sterk-900.webp"
			srcset="/images/content/samen-sterk-900.webp 900w, /images/content/samen-sterk-1400.webp 1400w"
			sizes="(max-width: 900px) 100vw, 46vw"
			alt="Mensen die elkaar helpen omhoog te klimmen"
		/>
	</div>
	<div class="copy-stack reveal delay-1">
		<RevealText text="Samen sterk" />
		<p>
			Door maatwerk te bieden, bouwen we samen elke dag verder aan sterke en betekenisvolle
			begeleiding.
		</p>
		<ul class="check-list">
			{#each points as point (point)}
				<li>{point}</li>
			{/each}
		</ul>
	</div>
</section>

<section class="cta-band reveal">
	<div>
		<h2>Wil je kennismaken of meer weten over werken bij Samenbijeen?</h2>
	</div>
	<a class="button primary" href={resolve('/contact')}>Stuur een bericht</a>
</section>
