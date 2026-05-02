<script lang="ts">
	import WidePhoto from '$lib/WidePhoto.svelte';

	const values = [
		'Vertrouwen',
		'Gelijkwaardigheid',
		'Wederzijds begrip',
		'Aandacht voor ontwikkeling'
	];
</script>

<svelte:head>
	<title>Over ons | Samenbijeen</title>
</svelte:head>

<section class="page-hero compact">
	<h1>Goede kwaliteitszorg is voor iedereen een recht.</h1>
	<p>
		Samenbijeen brengt zorgprofessionals en mensen met een zorgvraag bij elkaar voor persoonlijke,
		passende en kwalitatieve zorg.
	</p>
</section>

<WidePhoto src="/images/page-about.svg" alt="Abstracte visual over samenwerking in zorg" />

<section class="section split">
	<div>
		<h2>Samen de zorg verbeteren.</h2>
	</div>
	<div class="copy-stack reveal delay-1">
		<p>
			Wij ondersteunen cliënten, naasten en zorginstellingen met zorg die past bij de situatie. De
			relatie staat centraal: vertrouwen, gelijkwaardigheid, wederzijds begrip en aandacht voor
			ontwikkeling.
		</p>
		<p>
			Goede zorg is een recht voor jezelf, je ouders, je naasten en iedereen die het nodig heeft.
			Daarom kijken wij niet alleen naar de hulpvraag, maar ook naar het systeem en de mensen
			daaromheen.
		</p>
	</div>
</section>

<section class="section">
	<div class="section-heading">
		<h2>Een zorgrelatie die werkt.</h2>
	</div>
	<div class="value-grid">
		{#each values as value (value)}
			<div class="value-card reveal">
				<span></span>
				<strong>{value}</strong>
			</div>
		{/each}
	</div>
</section>
